## How we version

### Semver

We follow the principles of [semver](https://semver.org/spec/v2.0.0.html) and this document some of our interpretations of semver and anything that we agree to disagree on.

### Who updates versions

Maintainers should be the only ones to update versions in changelog or any version files/constants. This should never be done in a PR and should be done post merge commit to ensure that all the required changelog, readme, etc are done before creating a release.

### When do we version

We version in the commit that will be tagged and released as an artifact such as a gem. Typically all the work should be done in previous commits to bring all but version changes in and should just be a commit like `prep for x.y.z release` this commit then should be tagged and artifacts will be created and pushed with the new version. We strive to version and deploy changes to the majority of community projects within 24 hours after merge. This rule should always apply to:
- sensu-plugins
- sensu-extensions (needs some love to get there)
- chef cookbooks

Many of the core projects have very different release time frames and they should call out their own expectations on releases.

### Security

This is inspired by the following RFC: https://github.com/sensu-plugins/community/issues/78

#### Fixes

##### Breaking Changes

##### TL;DR

Security does not overrule the semver principle of any breaking change regardless of % of users impacted must always be versioned as a major version. As part of our [changelog guidelines](https://github.com/sensu-plugins/community/blob/master/HOW_WE_CHANGELOG.md) it needs to be called out as a `### Breaking Change`. If a vulnerability is serious enough to warrant an exception we have a process to evaluate and approve such cases. This is not the default, must have very serious impacts to consider for this, and requires multiple approvals validate the need.

##### Why

There are many arguments to be made that security updates depending on their impact should be versioned as a patch even in the case of a breaking change if it's minor impact or not part of the "public api". For example if you have to drop ruby 2.0 support to pull in a newer version of a gem to patch a vulnerability. There are a few interesting points here:
- Ruby 2.0 was never bundled/embedded with sensu, this could be argued that this version therefore is not a supported public api. While it is not recommended people use other versions of ruby.
- Ruby 2.0 is EOL and is a major security risk.
- By never breaking running systems we _enable_ people to continue running _insecure systems_ that put them at **greater risk** by not updating than say breaking `0.0001%` of users. Even still these systems that are critical enough could always pin on the exact version and not rely on pessimistic version constraints at all.

This makes this quite a gray area and leaves too much to interpretation by the individual maintainer. Depending on their background this could lead to an inconsistent experience which creates a trust issue with `semver`. As this is **very** important we decided to honor the principles of semver on pretty much any breaking change. In extreme cases we have a process below to evluate and approve breaking this. This comes at the cost of allowing scenarios like _Windows XP_ all over again. Security updates are hopefully pretty rare, we currently do not have a system to notify users when they need to consider upgrades for security concerns and is something that we will consider in the future. If you have comments or thoughts on how we should accomplish this please open an issue on this repo.

###### Process for exception

With all rules there will always need to be an exception. This talks about the types of exceptions and what it takes to get approval to **knowingly violate** `semver` for the customers greater good. If they want to bypass this then specify exact versions and avoid any kind of pessimistic version constraints and host your own rubygem repository/server.

In the face of something **VERY SERIOUS** such as credential leakage, privilege escalation or backdoors such as [this](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-13872). We should make such considerations with a heavy heart and as infrequently as possible. This require buy in from at least 2 maintainers one of them must be an org wide maintainer. In this case you would version as a patch but include the `### Breaking Change` section explaining what use cases might be broken. Along these lines `yanking` gem versions in the name of security need the same kind of approval and scrutiny.

##### Non Breaking Changes

These should be patches just like any other `(bug|hot)fix`.

### Pinning Versions

There is no a one size fits all but please no `YOLOver` for anything but local development! If you blindly install versions across major versions then the only thing you guarantee is that your systems will break eventually. The response of a maintainer will always be to pin your versions with either exact versions or by pessimistic version constraints.

#### Exact Versions

If you are severely risk adverse or support life saving technologies this is the only way to actually make sure that you will not automatically bring in new changes which could potentially break you.

This would look something like this in chef (principles are tech agnostic):
```
sensu_gem 'sensu-plugins-aws' do
  version '10.0.3'
end
```

#### Pessimistic Version constraints

Pessimistic Versioning allows you specify an acceptable comfort level for auto upgrading. You could either lock to the major or to the minor.

Example locking to major:
````
sensu_gem 'sensu-plugins-aws' do
  version '~> 10.0'
end
````
 The example above says pull in any new version that is greater than `10.0` but less than `11.0`. In the context of semver this is generally a very safe place to be as long as you have a stable code base with lots of automated testing.

 Example locking to a minor:
 ```
sensu_gem 'sensu-plugins-aws' do
  version '~> 10.0.2'
end
 ```

 The above example says pull in any new version that is greater than `10.0.2` but less than `10.1.0` in the context of semver this is a very safe place to be as no new features will be brought in. Only fixes can potentially break you. In the context of security updates unless they require a breaking change they will be a patch and therefore should be pulled in.
