* [What is a CHANGELOG?](#what-is-a-changelog)
* [Where is the CHANGELOG?](#where-is-the-changelog)
* [How we CHANGELOG](#how-we-changelog)
   * [The anatomy of a good CHANGELOG](#the-anatomy-of-a-good-changelog)
      * [Version Scheme](#version-scheme)
      * [CHANGELOG Format](#changelog-format)
      * [Unreleased Change](#unreleased-change)
      * [The Breaking Change](#the-breaking-change)
      * [The Version Diffs (for Maintainers)](#the-version-diffs-for-maintainers)
   * [Example scenarios](#example-scenarios)
      * [Adding a new feature](#adding-a-new-feature)
      * [Fixing a Bug](#fixing-a-bug)
      * [Non-Breaking Changes](#non-breaking-changes)
      * [Breaking Changes](#breaking-changes)

<!-- Created by [gh-md-toc](https://github.com/ekalinin/github-markdown-toc) -->

## What is a CHANGELOG?

A CHANGELOG is simple way for users quickly identify what has changed between two versions of a project. There are many philosophies on what a good CHANGELOG should look like. Our community has decided to focus on the user, who are most often sysadmins, system engineers, app developers, etc. The important common denominator of our users is that they must evaluate software before an upgrade to ensure stability. Because of this observation, we decided to take the CHANGELOG as an important point in all repositories.

## Where is the CHANGELOG?

A `CHANGELOG.md` file in expected at the root of every repository.

## How we CHANGELOG

We align with [Keep A Changelog](http://keepachangelog.com/) with a few exceptions. Our primary focus is ease of evaluate before choosing to upgrade. Sensu user feedback found that bumps in the major version alone are not sufficient to make the call. Thus we decided to add an additional flavor change in the form of a header called `### Breaking Changes`. This emphasis on potential risk allows helps all users make the right call. We also encourage giving enough information that any user can understand the upgrade steps required to adapt to any breaking changes.

### The anatomy of a good CHANGELOG

These are the essential features to a CHANGELOG.
Start by reading through [Keep A Changelog](http://keepachangelog.com/) to familiarize yourself with a majority our practices. See [a live example here](https://github.com/sensu-plugins/sensu-plugins-sensu/blob/master/CHANGELOG.md) for the TL;DR version.

#### Version Scheme

Clearly state how the repository is versioned by maintainers:

```
This project adheres to [Semantic Versioning](http://semver.org/)
```

#### CHANGELOG Format

Give information on CHANGELOG format. By default:

```
This CHANGELOG follows the format listed at [Our CHANGELOG Guidelines](https://github.com/sensu-plugins/community/blob/master/HOW_WE_CHANGELOG.md).
Which is based on [Keep A Changelog](http://keepachangelog.com/)
```

#### Unreleased Change

Part of the maintainer workflow for Sensu plugins is to propose a new change (via Pull Request) under a header that reflects the code has not yet been released:

```
## [Unreleased]
### TYPE_OF_CHANGE
- thing changed
```

This convention helps since there is no guarantee as to when a maintainer will review it, when it will be merged, or when it will be released.

#### The Breaking Change

While avoidance of breaking changes is preferred, there will always be times where improvement requires incompatibility with previous versions. These moments are most appreciated when they greatly improve the user experience and also includes reasonable upgrade path. In these cases, per [SemVer](http://semver.org/), we bump to a major version.

Some helpful considerations:

* Removal of functionality is more often than not a breaking change (one exception would be removal of test code)
* Bumping the required version of a significant dependency (if also using semver)
* Breaking change within dependencies that may not follow semver is also considered breaking in these projects

In these breaking changes we should think about what the end user needs to do other than install the new version. This can include steps like:

* Installation of new system library
* Changes to environmental variables or directory paths
* A parameter for a unit of code is removed

Or any other changes that will require human intervention.

#### The Version Diffs (for Maintainers)

**Concern for Maintainers only**

We talked about how the focus was on human-readable changelogs for easy evaluation for upgrades. We still might need to look at the whole change between versions, especially if you are triaging a recently introduced bug or found an undocumented feature and wanted to know more of how it works. A maintainer can provide the version released with a diff link and a date as outlined per the convention of [Keep A Changelog](http://keepachangelog.com). For example:

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

### Example scenarios

Here are some common situations that warrant updates to the `CHANGLOG.md` file.

#### Adding a new feature

A new script, library or feature added:

```
## [Unreleased]
### Added
- `check-something-shiny.rb`: new script that helps with monitoring something shiny (@mygithubuser)
- `metric-something-shiny.rb`: added flag of `--very` to add very shiny metrics to the existing output. (@mygithubuser)
- added testing for `check-something-shiny.rb` (@mygithubuser)
```

#### Fixing a Bug

Note that this can be a breaking change that does not need to be specifically called out or versioned as a major if it only affects broken functionality:

```
## [Unreleased]
### Fix
- `check-something-shiny.rb`: fixed a bug that when it was too shiny it hurt your eyes. (@mygithubuser)
```

#### Non-Breaking Changes

This can either be functional or stylistic changes (not limited to code):

```
## [Unreleased]
### Changed
- updated the README to have helpful information about `handler-something-shiny.rb` configuration to how to configure how shiny you want it. (@mygithubuser)
- to a new version of rubocop and appeased the new cops. (@mygithubuser)
```

#### Breaking Changes

These are the ones that change behavior as mentioned above. Please read [The Breaking Change](#the-breaking-change). Example:

```
## [Unreleased]
### Breaking Change
- to allow users who want to only use `metric-something-shiny.rb` which does not require a c compiler but not `check-something-shiny.rb` which would have a dependency on one we removed the `shiny-extended` gem from the gemspec and users will need to refer to the REAMDE on how to install this manually. (@mygithubuser)
- dropping ruby support for x.y
- `check-something-shiny.rb`: changed the defaults for `--lighting` from 3 to 5 as this is a better sane default. (@mygithubuser)
```
