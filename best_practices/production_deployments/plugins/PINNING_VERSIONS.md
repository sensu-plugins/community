# Pinning Versions

## How we version plugins

Plugins follow [Semantic Versioning (semver)](https://semver.org/spec/v2.0.0.html), which requires breaking changes to be communicated through the release version number. Please see [this documentation](https://github.com/sensu-plugins/community/blob/master/HOW_WE_VERSION.md) for an in-depth look at how we do so.

## No YOLOver

In production, pinning of plugin versions is an absolute must do for stability of your monitoring infrastructure. Said another way, you should never use unpinned versions of plugins when you install them. This practice is sometimes referred to as `YOLOver` since the only guarantee is that you will break at some point in the future.

Chances are you don't realize you are following this pattern. What this really means is that at install time you are not providing any guidelines on the version to install which will pick up the latest version, even across major versions, which will pretty much always include some form of [breaking changes](https://github.com/sensu-plugins/community/blob/master/HOW_WE_CHANGELOG.md#the-breaking-change). **Keep reading on to verify you're not in this dangerous situation!**

Pinning consists of two components:
- during install specify the specific version you want to install or a set of constraints
- a mechanism to ensure that they remain within the constraints specified

If you are using the `CLI` or `sensu-install` methods you should probably use a config management solution or orchestration tool as a wrapper to ensure that it is consistently has that version installed.

## Pinning with various tools

Please read through [this](https://github.com/sensu-plugins/community/blob/master/HOW_WE_VERSION.md#pinning-versions) to get a base understanding on the different types of version constraints.

### Installing a specific version with the CLI

#### Bad
```
$ /opt/sensu/embedded/bin/gem install sensu-plugins-aws
```

#### Good
```
$ /opt/sensu/embedded/bin/gem install sensu-plugins-aws -v 10.0.2
```

### Pinning with `sensu-install`

#### Bad
```
$ sensu-install -p aws
```

#### Good
```
$ sensu-install -p 'aws:10.0.2'
```

### Pinning with Chef

#### Bad
```
sensu_plugin 'sensu-plugins-aws'
```

#### Good
```
sensu_plugin 'sensu-plugins-aws' do
  version '~> 10.0'
end
```

### Pinning with Puppet

#### Bad
```
node 'sensu-server.foo.com' {
  class { 'sensu':
    plugins           => {
      'puppet:///data/sensu/plugins/ntp.rb' => {
        'install_path' => '/alternative/path',
      'puppet:///data/sensu/plugins/postfix.rb'
        'type'         => 'package'
    },
    ...
  }
}
```

#### Good
```
node 'sensu-server.foo.com' {
  class { 'sensu':
    plugins           => {
      'puppet:///data/sensu/plugins/ntp.rb' => {
        'install_path' => '/alternative/path',
      'puppet:///data/sensu/plugins/postfix.rb'
        'type'         => 'package',
        'pkg_version'  => '2.4.2',
    },
    ...
  }
}
```



### Pinning with Ansible

#### Bad
```
sensu_remote_plugins:
  - graphite
  - process-checks
```

#### Good
```
sensu_remote_plugins:
  - process-checks:0.0.6
```

### Pinning with SaltStack

#### Bad
state:
```
"Install gem aws":
  gem.installed:
    - name: sensu-plugins-aws
    - gem_bin: /opt/sensu/embedded/bin/gem
```

cli:
```
salt '*' gem.install sensu-plugin-aws gem_bin=/opt/sensu/embedded/bin/gem
```
#### Good

state:
```
"Install gem aws:10.0.2'":
  gem.installed:
    - name: sensu-plugins-aws
    - version: 10.0.2
    - gem_bin: /opt/sensu/embedded/bin/gem
```

cli:
```
salt '*' gem.install sensu-plugin-aws gem_bin=/opt/sensu/embedded/bin/gem version='10.0.2'
```
