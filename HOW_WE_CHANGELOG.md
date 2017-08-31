### What is a CHANGELOG?

A CHANGELOG is simple way for users to look at to know what has changed. While there are many philosophies on what a good CHANGELOG should look like. We have decided how this should be presented based on our target audiences which are sysadmins, system engineers, app developers, etc. The one thing they all have in common is that they want to evaluate when and how to upgrade. Because of this we decided to focus on this.

### Where is the CHANGELOG?

We should have a `CHANGELOG.md` file in the root of each repository.

### How we CHANGELOG

For the most part we are very much inline with [Keep A Changelog](http://keepachangelog.com/) but as noted before we wanted to docus on making it easy to evaluate upgrade needs we found it got us 99% of the way there but there was something missing. After getting feedback from users that even though we bumped the major version they still felt it was not clear what was needed to proceed. Thus we decided to add an additional flavor change in the form of a header called `### Breaking Changes`. This allowed it to be more loud and clear when reading the CHANGELOG when you really need to pay attention. We also try to encourage giving enough information that allows the user to understand the upgrade steps required such as you need to install system package x.

#### The anatomy of a good CHANGELOG

##### Version Scheme

It should detail how things are versioned by maintainers:
```
This project adheres to [Semantic Versioning](http://semver.org/)
```

One thing to note is that when proposing a new change (via pull request) you should always put your changes under:
```
## [Unreleased]
### TYPE_OF_CHANGE
- thing changed
```

The reason for this is that there is no guarantee as to when a maintainer will review it, when it will be merged, or when it will be released.

##### CHANGELOG Format
Give information on CHANGELOG format.
```
This CHANGELOG follows the format listed at [Our CHANGELOG Guidelines ](https://github.com/sensu-plugins/community/blob/master/HOW_WE_CHANGELOG.md).
Which is based on [Keep A Changelog](http://keepachangelog.com/)
```

##### Keep A CHANGELOG
Read through [Keep A Changelog](http://keepachangelog.com/) as they have some great stuff and this is just a few flavor and process changes.

##### The Breaking Change
While usually a breaking change is avoided where possible there will always be times where it either has no path forward or greatly improves the user experience and has a reasonable upgrade path. In these cases per [Semver](http://semver.org/) we bump to a major version. In some cases you can remove things that are not a breaking change. For example removing test code is not a breaking change but bumping the required version of a major dependency (if using semver) or any breaking change with another versioning scheme. In these breaking changes we should think about what the end user needs to do other than simply install the new version. This can include steps like:
- you need to install some new system library
- a parameter for a unit of code is removed in a way that requires human intervention.

##### The version Diffs
We talked about how the focus was on human readable changelogs to be easily evaluated for upgrades but we still might need to look at the whole change especially if you are triaging a recently introduced bug or found a saw a new feature and wanted to know how it worked more.

The following should only be done by a maintainer but basically will give the version released with a diff link and a date as outlined per the convention of [Keep A Changelog](http://keepachangelog.com).

Example:
```
## [Unreleased]

## [8.1.0] - 2017-08-28
### Fixed
check-ebs-burst-limit.rb: Only compare the warning threshold if a `-w` option was specified on the command-line, as usage shows `-w` is optional. (@ivanfetch)

### Added
- check-ebs-burst-limit.rb: Only check volumes attached to the current instance with a new `-s` option, which also overrides the `-r` option for EC2 region. (@ivanfetch)

## [8.0.0] - 2017-08-20
### Breaking Changes
- check-beanstalk-elb-metric.rb and check-cloudwatch-metric.rb: `--opertor` flag was a typo, please use `--operator` now. (@guikcd)

TRUNCATED OUTPUT

[Unreleased]: https://github.com/sensu-plugins/sensu-plugins-aws/compare/8.0.0...HEAD
[8.1.0]: https://github.com/sensu-plugins/sensu-plugins-aws/compare/8.0.0...8.1.0
[8.0.0]: https://github.com/sensu-plugins/sensu-plugins-aws/compare/7.1.0...8.0.0
```



### Just give me some examples

#### Adding a new feature
This can be a new script, library, etc or a new feature within existing code.
```
## [Unreleased]
### Added
- `check-something-shiny.rb`: new script that helps with monitoring something shiny (@mygithubuser)
- `metric-something-shiny.rb`: added flag of `--very` to add very shiny metrics to the existing output. (@mygithubuser)
- added testing for `check-something-shiny.rb` (@mygithubuser)
```

#### Changing an existing feature
##### Fixing a bug
This can be a breaking change that does not need to be specifically called out or versioned as a major if it only affects broken functionality.
```
## [Unreleased]
### Fix
- `check-something-shiny.rb`: fixed a bug that when it was too shiny it hurt your eyes. (@mygithubuser)
```
##### Non Breaking
This can either be functional or styalistic changes and are not limited to code.
```
## [Unreleased]
### Changed
- updated the README to have helpful information about `handler-something-shiny.rb` configuration to how to configure how shiny you want it. (@mygithubuser)
- to a new version of rubocop and appeased the new cops. (@mygithubuser)
```

##### Breaking Changes
Please read [The Breaking Change](#the-breaking-change).
```
## [Unreleased]
### Breaking Change
- to allow users who want to only use `metric-something-shiny.rb` which does not require a c compiler but not `check-something-shiny.rb` which would have a dependency on one we removed the `shiny-extended` gem from the gemspec and users will need to refer to the REAMDE on how to install this manually. (@mygithubuser)
- dropping ruby support for x.y
- `check-something-shiny.rb`: changed the defaults for `--lighting` from 3 to 5 as this is a better sane default. (@mygithubuser)
```
