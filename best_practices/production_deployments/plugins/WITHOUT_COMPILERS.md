# Pre-compiling native extensions for Sensu Plugins gem dependencies

## What is this about

Basically many of the plugins require the use of a compiler (typically c) on install time. There are good reasons to avoid compilers on systems and bad reasons to do so.

### Good reasons

1. Reduce spin-up time, if you have instances in some sort of scaling group and you want to reduce the amount of time it takes for a machine to come up with monitoring. An alternative to this is to bake the gem installs into your image.
1. Compilers are dev tools, they have no business being in a production environment.

### Bad reasons

1. Security: I have heard the argument many times that somehow having a compiler makes you less secure. This statement is often made by security teams that have no idea what they are talking about. If the attacker has enough access to a system to use a compiler then they would opt for either compiling on their machine and dropping the executable on the client or leverage the tools that are already on the box. The 2 most common targets at this point become the various shell such as `sh` or `bash` and interpretors such as `python` or `ruby`. Python is almost always guaranteed on \*nix. Ruby is currently guaranteed on any sensu install. This is **Security Theater** and does not really reduce any **real** attack vectors. This creates extra complexity in deployment without a good reason.

### Options

If you are here because some security team believes compilers are really a valid attack vector, you have my sympathy. I hope the points above will be helpful. You also have 2 options to meet the request:

#### Install compiler, install gems, remove compiler

This has the benefit of ease of development, portability, and nicely complements methodologies attempting to achieve immutable infrastructure. This has the most flexibility in terms of os/architecture support as it will compile the specific `native extensions` for the appropriate architectures and os at install time. If you have multiple os's and cpu architectures to support this makes more sense. If you need to reduce bootstrap time just add this to your existing build process with a tools such as `packer`,`docker`, `chef`, etc.

#### Pre-compile native extensions for distribution

The major benefit here is that you only need the compiler on the **build machine** and not the **deployed server**. That being said if you have to support multiple cpu architectures or upgrading software with a new version of Ruby you will need to compile it for each.

## Sources and Assumptions

Sources:
* [GitHub - luislavena/gem-compiler: A RubyGems plugin that generates binary gems](https://github.com/luislavena/gem-compiler)

Assumptions:
* CentOS 7 platform
* You have some way to store these artifacts and make them available for systems in your environment

Caveats:
* Compiled gems are tied to Ruby version they are compiled for
	* If Sensu upgrades Ruby 2.4 -> Ruby 2.5, then packages have to be rebuilt
* Compiled gems are tied to CPU architecture for which they are compiled


## Install build toolchain

1. Drop off yum repository definition and install Sensu

    ```bash
    $ printf '[sensu]
    name=sensu
    baseurl=https://repositories.sensuapp.org/yum/$releasever/$basearch/
    gpgcheck=0
    enabled=1' | sudo tee /etc/yum.repos.d/sensu.repo && yum install -y sensu
    ```

2. Install EPEL and dev tools

    ```bash
    $ yum install -y epel-release
    $ yum groupinstall -y "Development Tools"
    ```

3. Add Sensu's embedded bin to our path

    ```bash
    $ which gem
    /usr/bin/which: no gem in (/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin)
    $ export PATH=$PATH:/opt/sensu/embedded/bin
    $ which gem
    /opt/sensu/embedded/bin/gem
    ```

## Install gems

1. Install `gem-compiler`

   ```bash
   $ gem install gem-compiler
   ```

2. Install the source gems into a cache directory

   We're going to install `sensu-plugins-aws` because its dependency on nokogiri is one of the thornier examples I can think of:

    ```bash
    $ mkdir /tmp/gems
    $ gem install --no-ri --no-rdoc --install-dir /tmp/gems sensu-plugins-aws
    ```

    Observing the `gem install` output, we that nokogiri and unf_ext build native extensions.
    These are the gems we will compile so we can install them from our own repository.

### Compile gems

1. Use gem-compiler to rebuild gem packages including native extensions

    ```
    $ cd /tmp/gems/cache
    $ gem compile unf_ext-0.0.7.4.gem

    # gem-compiler readme notes nokogiri as a specific example of gems that need the --prune flag

    $ gem compile nokogiri-1.8.1.gem --prune
    ```

2. Note that the resulting compiled gem files have a x86_64-linux in their file name:

    ```bash
    $ ls  -1 *-x86_64-linux.gem
    nokogiri-1.8.1-x86_64-linux.gem
    unf_ext-0.0.7.4-x86_64-linux.gem
    ```

## Install on target system and test

1. Install compiled gem into embedded Ruby

    Now we can copy these gems to another system, install them into the Sensu embedded Ruby runtime. In real life you'd want to put these on a rubygems server of your own (e.g. [Geminabox](https://github.com/geminabox/geminabox), Artifactory or similar) or maybe use a tool like `fpm` to convert them to system packages.

    ```bash
    # Here we've copied the compiled gems to a system with Sensu installed, but no gcc or other compile toolchain
    # Note that nokogiri needs libxml2 and possibly libxslt to be present on your system
    $ /opt/sensu/embedded/bin/gem install unf_ext-0.0.7.4-x86_64-linux.gem
    $ /opt/sensu/embedded/bin/gem install nokogiri-1.8.1-x86_64-linux.gem
    ```

2. Install Sensu plugins as normal

    With these prerequisites in place we can install `sensu-plugins-aws` without a compiler. You can use `sensu-install` or `gem` commands:

    ```bash
    $ sensu-install -p aws
    [SENSU-INSTALL] installing Sensu plugins ...                                                                                                              
    [SENSU-INSTALL] determining if Sensu gem 'sensu-plugins-aws' is already installed ...                                                                     
    false                                                                                                                                                     
    [SENSU-INSTALL] Sensu plugin gems to be installed: ["sensu-plugins-aws"]                                                                                  
    [SENSU-INSTALL] installing Sensu gem 'sensu-plugins-aws'                                                                                                  
    Fetching: unf-0.1.4.gem (100%)                                                                                                                            
    Successfully installed unf-0.1.4                                                                                                                          
    Fetching: domain_name-0.5.20170404.gem (100%)                                                  
    Successfully installed domain_name-0.5.20170404                                                                                                           
    Fetching: http-cookie-1.0.3.gem (100%)                                                          
    Successfully installed http-cookie-1.0.3                                                                                                                  
    Fetching: mime-types-2.99.3.gem (100%)                                                        
    Successfully installed mime-types-2.99.3                                                                                                                  
    Fetching: netrc-0.11.0.gem (100%)                                                                              
    Successfully installed netrc-0.11.0                                                                                                                       
    Fetching: rest-client-1.8.0.gem (100%)                                                                                                                    
    Successfully installed rest-client-1.8.0                                                                                                                  
    Fetching: sensu-plugins-aws-10.0.3.gem (100%)                                                                                                             
    You can use the embedded Ruby by setting EMBEDDED_RUBY=true in /etc/default/sensu                                                                         
    Successfully installed sensu-plugins-aws-10.0.3                                                                                                           
    7 gems installed                                                                                                                                          
    [SENSU-INSTALL] successfully installed Sensu plugins: ["sensu-plugins-aws"]  
    ```

3. Set up our environment and test. I believe `check-elb-health-fog.rb` should exercise the nokogiri dependency:

    ```bash
    $ export AWS_ACCESS_KEY=fatchance
    $ export AWS_SECRET_KEY=noway
    $ /opt/sensu/embedded/bin/check-elb-health-fog.rb -n foo -r us-east-1                                        
    ELBHealth WARNING: An issue occured while communicating with the AWS EC2 API: There is no ACTIVE Load Balancer named 'foo'
    ```

    _Seems legit!_ 😉
