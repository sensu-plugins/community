# Pull Request Process

This document was *heavily* influenced (with permission) by the [kubernetes community](https://github.com/kubernetes/community) as it has some great practices and maturity.

 [//]:  https://github.com/kubernetes/community/blob/master/contributors/devel/pull-requests.md

This doc explains the process and best practices for submitting a PR to [Sensu Plugin projects](https://github.com/sensu-plugins). It should serve as a reference for all contributors, and be useful especially to new and infrequent submitters.


- [Pull Request Process](#pull-request-process)
- [Before You Submit a PR](#before-you-submit-a-pr)
  * [Run Local Verifications](#run-local-verifications)
- [The PR Submit Process](#the-pr-submit-process)
  * [Add a CHANGELOG ENTRY](#add-changelog)
  * [The Testing and Merge Workflow](#the-testing-and-merge-workflow)
  * [Marking Unfinished Pull Requests](#marking-unfinished-pull-requests)
  * [Automation](#automation)
  * [How the Tests Work](#how-the-tests-work)
- [Why was my PR closed?](#why-was-my-pr-closed)
- [Why is my PR not getting reviewed?](#why-is-my-pr-not-getting-reviewed)
- [Best Practices for Faster Reviews](#best-practices-for-faster-reviews)
  * [0. Familiarize yourself with project conventions](#0-familiarize-yourself-with-project-conventions)
  * [1. Is there an open issue for this bug/feature?](#1-is-there-an-open-issue-for-this-bug-or-feature)
  * [2. Is there an existing PR for this bug or feature?](#2-is-there-an-existing-pr-for-this-bug-or-feature)
  * [3. Is the feature wanted? Are there many ways forward?](#3-is-the-feature-wanted-are-there-many-ways-forward)
  * [4. Smaller Is Better: Small Commits, Small PRs](#4-smaller-is-better-small-commits-small-prs)
  * [5. Open a Different PR for Fixes and Generic Features](#5-open-a-different-pr-for-fixes-and-generic-features)
  * [6. Comments matter](#6-comments-matter)
  * [7. Testing artifacts](#7-testing-artifacts)
  * [8. Squashing and Commit Titles](#8-squashing-and-commit-titles)
  * [9. KISS, YAGNI, MVP, etc.](#9-kiss--yagni--mvp--etc)
  * [10. It's OK to Push Back](#10-it-s-ok-to-push-back)
  * [Common Sense and Courtesy](#common-sense-and-courtesy)

# Before You Submit a PR

This guide is for contributors who already have a PR to submit. If you're looking for information on setting up your developer environment and creating code to contribute to Sesnu Plugins, see the [development guide](development.md).

**Make sure your PR adheres to our best practices. These include following project conventions, making small PRs, and commenting thoroughly. Please read the more detailed section on [Best Practices for Faster Reviews](#best-practices-for-faster-reviews) at the end of this doc.**

## Run Local Verifications

You can run these local verifications before you submit your PR to predict the
pass or fail of continuous integration. Each project has different needs but for the ruby projects you should always run and ensure this passes:

* `bundle exec rake default`

# The PR Submit Process

Merging a PR requires the following steps to be completed before the PR will be merged automatically. For details about each step, see the [The Testing and Merge Workflow](#the-testing-and-merge-workflow) section below.

- Create a branch off master
- Make changes
- Add a CHANGELOG entry based on our [CHANGELOG conventions](https://github.com/sensu-plugins/community/blob/master/HOW_WE_CHANGELOG.md)
- Make the PR
- provide test artifact per [here](#testing-artifacts)
- Pass all tests
- Get a `LGTM` from a reviewer
- Get approval from a project maintainer

If your PR meets all of the steps above, a maintainer should merge and release it within 24 hours of the *merge* under normal circumstances.

## Add Changelog

Please refer to our  [CHANGELOG conventions](https://github.com/sensu-plugins/community/blob/master/HOW_WE_CHANGELOG.md)

## The Testing and Merge Workflow

The Sensu plugins projects automatically run tests on each PR and on source branches. For pull requests that are in progress but not ready for review, prefix the PR title with `[WIP]` and track any remaining TODOs in a checklist in the pull request description.

Here's the process the PR goes through on its way from submission to merging:

1. Make the pull request
1. Assuming tests pass a maintainer will tag the issue appropriately and assign themselves to the PR. Then they will request a review from themselves, other maintainers or subject matter experts.
1. Reviews the change:
  - If the PR needs changes
    - Comments back the *required* and _desired_ changes and assigns the label `Feedback Requested`
    - Submitter, community members, subject matter experts, and maintainers discuss the PR and hopefully come to a consensus.
    - If no consensus can be made then the PR will be closed and further discussed in an issue. Otherwise changes are made and git history is cleaned up (squash|rebase). Afterwards a maintainer accepts the pull request and releases.
  - Else
    - maintainer accepts the pull request and releases

## Marking Unfinished Pull Requests

If you want to solicit reviews before the implementation of your pull request is complete, you should hold your pull request to ensure that the merge queue does not pick it up and attempt to merge it.

The best way to put a hold on an issue is to add either `[WIP]` or `WIP` as a prefix to your pull request title. When it is ready to review you can remove this to let a maintainer know you are ready for review. We encourage you to open a PR and discuss early implementation.

## Automation

The Sensu plugins developer community relies on [travis](https://travis-ci.org) to automatically run tests and manage releases of rubygems.

## How the Tests Work

Each repo will contain a `.travis.yml` which will define the automated tests that are run. Ruby projects will use a `Rakefile` to provide a simple standard interface. Depending on the nature of the repository the testing may be very different.

For ruby based plugins:
- `Rakefile` interface
- `rspec`, `mini-test`, or `serverspec` (preferred)

The serverspec tests should be used with `kitchen-docker` to provide lightweight and portable testing. Depending on the check it might make sense to link several containers and run real services while others might want to stub the response in something like nginx.

# Why was my PR closed?

Pull requests older than 30 days will be closed. Exceptions can be made for PRs that have active review comments, or that are awaiting other dependent PRs. Closed pull requests are easy to recreate, and little work is lost by closing a pull request that subsequently needs to be reopened. We want to limit the total number of PRs in flight to:
* Maintain a clean project
* Remove old PRs that would be difficult to rebase as the underlying code has changed over time
* Encourage code velocity

# Why is my PR not getting reviewed?

A few factors affect how long your PR might wait for review.

If it's the last few weeks of a milestone, we need to reduce churn and stabilize.

Or, it could be related to best practices. One common issue is that the PR is too big to review. Let's say you've touched 39 files and have 8657 insertions. When your would-be reviewers pull up the diffs, they run away - this PR is going to take 4 hours to review and they don't have 4 hours right now. They'll get to it later, just as soon as they have more free time (ha!).

There is a detailed rundown of best practices, including how to avoid too-lengthy PRs, in the next section.

But, if you've already followed the best practices and you still aren't getting any PR love, here are some
things you can do to move the process along:

   * Make sure that your PR has an assigned reviewer (assignee in GitHub). If not after 24 hours, please post a message in [Slack](http://slack.sensu.io) in the `#contributing` channel asking for an assignee.

   * Ping the assignee (@username) on the PR comment stream, and ask for an estimate of when they can get to the review.

   * Ping the assignee on [Slack](http://slack.sensu.io). Remember that a person's GitHub username might not be the same as their Slack username.

   * Ping the assignee by email (many of us have publicly available email addresses).

   * If you're a member of the organization ping the [team](https://github.com/orgs/sensu-plugins/teams) (via @team-name) that works in the area you're submitting code. You may also assign the appropriate person if there is someone who should specifically handle it.

   * If you have fixed all the issues from a review, and you haven't heard back, you should ping the assignee on the comment stream with a "please take another look" (`PTAL`) or similar comment indicating that you are ready for another review.

Read on to learn more about how to get faster reviews by following best practices.

# Best Practices for Faster Reviews

Most of this section is not specific to Sensu plugins, but it's good to keep these best practices in mind when you're making a PR.

You've just had a brilliant idea on how to make Sensu plugins better. Let's call that idea Feature-X. Feature-X is not even that complicated. You have a pretty good idea of how to implement it. You jump in and implement it, fixing a bunch of stuff along the way. You send your PR - this is awesome! And it sits. And sits. A week goes by and nobody reviews it. Finally, someone offers a few comments, which you fix up and wait for more review. And you wait. Another week or two go by. This is horrible.

Let's talk about best practices so your PR gets reviewed quickly.

## 0. Familiarize yourself with project conventions

* [Developer Guidelines](https://github.com/sensu-plugins/documentation/blob/master/docs/developer_guidelines.md)
* [CHANGELOG Guidelines](https://github.com/sensu-plugins/community/blob/master/HOW_WE_CHANGELOG.md)

## 1. Is there an open issue for this bug or feature?

If so link to it in the PR (e.g. Fixes #NN) in the body of the PR so the issue is linked and updated.

## 2. Is there an existing PR for this bug or feature?

Is there an existing PR for this bug/feature? Check the open PRs before submitting a duplicate.

## 3. Is the feature wanted? Are there many ways forward?

Are you sure Feature-X is something the Sensu plugin community wants or will accept? Is it implemented to fit with other changes in flight? Are you willing to bet a few days or weeks of work on it?

It's better to get confirmation beforehand. The best way to get onboard with maintainers is to create an issue with a `[PROPOSAL]` prefix.

Minimum Requirements:
- what you want?
- why you want it?
- what are the impacts to the best of your knowledge?
- proposed solution (if missing the PR titled with `[Feature REQUEST]`, `[QUESTION]`, etc)
- in some cases such as `sensu-plugins-http` and `sensu-plugins-ssl` there is overlap, in these scenerios you should include why this is the right place to put the new feature

Preferred Requirements:
- all of the min requirements
- questions on concepts or implementation
- design docs, pseudo code, etc

If these are missing a maintainer can ask for the required information and discuss on issue or in [Slack](http://slack.sensu.io) in the `#plugins` channel.

Or, do all of the above.

Be clear about what type of feedback you are asking for when you submit a proposal doc or sketch PR.

Now, if we ask you to change the design, you won't have to re-write it all.

## 4. Smaller Is Better: Small Commits, Small PRs

Small commits and small PRs get reviewed faster and are more likely to be correct than big ones.

Attention is a scarce resource. If your PR takes 60 minutes to review, the reviewer's eye for detail is not as keen in the last 30 minutes as it was in the first. It might not get reviewed at all if it requires a large continuous block of time from the reviewer.

**Breaking up commits**

Break up your PR into multiple commits on large PRs, at logical break points.

Making a series of discrete commits is a powerful way to express the evolution of an idea or the
different ideas that make up a single feature. Strive to group logically distinct ideas into separate commits.

For example, if you found that Feature-X needed some prefactoring to fit in, make a commit that JUST does that prefactoring. Then make a new commit for Feature-X.

Strike a balance with the number of commits. A PR with 25 commits is still very cumbersome to review, so use
judgment.

**Breaking up PRs**

Or, going back to our prefactoring example, you could also fork a new branch, do the prefactoring there and send a PR for that. If you can extract whole ideas from your PR and send those as PRs of their own, you can avoid the painful problem of continually rebasing.

Sensu plugins is a fast-moving codebase - lock in your changes ASAP with your small PR, and make merges be someone else's problem.

Multiple small PRs are often better than multiple commits. Don't worry about flooding us with PRs. We'd rather have 100 small, obvious PRs than 10 unreviewable monoliths.

We want every PR to be useful on its own, so use your best judgment on what should be a PR vs. a commit.

As a rule of thumb, if your PR is directly related to Feature-X and nothing else, it should probably be part of the Feature-X PR. If you can explain why you are doing seemingly no-op work ("it makes the Feature-X change easier, I promise") we'll probably be OK with it. If you can imagine someone finding value independently of Feature-X, try it as a PR. (Do not link pull requests by `#` in a commit description, because GitHub creates lots of spam. Instead, reference other PRs via the PR your commit is in.)

## 5. Open a Different PR for Fixes and Generic Features

**Put changes that are unrelated to your feature into a different PR.**

Often, as you are implementing Feature-X, you will find bad comments, poorly named functions, bad structure, weak type-safety, etc.

You absolutely should fix those things (or at least file issues, please) - but not in the same PR as your feature. Otherwise, your diff will have way too many changes, and your reviewer won't see the forest for the trees.

**Look for opportunities to pull out generic features.**

For example, if you find yourself touching a lot of checks, think about using shared library code within the plugin or even pulling in another dependency. Can some of what you're doing be made more generic and moved up and out of the Feature-X check/plugin? Do you need to use a function or type from an otherwise unrelated package? If so, promote! We have places for hosting more generic code.

Likewise, if Feature-X is similar in form to Feature-W which was checked in last month, and you're duplicating some tricky stuff from Feature-W, consider prefactoring the core logic out and using it in both Feature-W and
Feature-X. (Do that in its own commit or PR, please.)

## 6. Comments Matter

In your code, if someone might not understand why you did something (or you won't remember why later), comment it. Many code-review comments are about this exact issue.

If you think there's something pretty obvious that we could follow up on, add a TODO.

Read up on [Rubocop Style Guide](https://github.com/bbatsov/ruby-style-guide#comments) - follow those *general* rules for comments. If you disagree with the style guide just explain why, we're pretty reasonable people. Mostly.

## 7. Testing artifacts

### Today

Tests are very much lacking, please feel free to check [This github issue](https://github.com/sensu-plugins/community/issues/41) for how you can help us change this.

If you are not willing to write an automated test then you should either in the PR stream add the redacted IO to the comment stream or description, if it is quite large please create a [gist](https://gist.github.com/) and link to it.

#### Bugs

For bugs you should include the before and after input and output in comments or gists.

#### Examples

##### Small output in description/comment

Check all target groups in a region:
```
$ ./check-alb-target-group-health.rb -r us-west-2
CheckALBTargetGroupHealth WARNING: Unhealthy ALB target groups: example-service - 2/2 unhealthy targets: {i-00e31e3878b7ff800, i-08dfc79e79fa36f9c}
```
Check a single target group in a region:
```
$ ./check-alb-target-group-health.rb -r us-west-2 -t example-service
CheckALBTargetGroupHealth WARNING: Unhealthy ALB target groups: example-service - 2/2 unhealthy targets: {i-00e31e3878b7ff800, i-08dfc79e79fa36f9
```
Check multiple target groups in a region:
```
$ ./check-alb-target-group-health.rb -r us-west-2 -t example-service,another-service
CheckALBTargetGroupHealth WARNING: Unhealthy ALB target groups: another-service - 1/2 unhealthy targets: {i-049021d0efd2d5784}, example-service - 2/2 unhealthy targets: {i-00e31e3878b7ff800, i-08dfc79e79fa36f9c}
```
Output when all target groups are healthy:
```
$ ./check-alb-target-group-health.rb -r us-west-2
CheckALBTargetGroupHealth OK: All ALB target groups are healthy
```
##### Large output and gist

Here is a gist showing two runs, the second one using the new -s option. Let me know if you would like more than [this](https://gist.github.com/ivanfetch/430af66a78f4fcb9a168b8ece985d618)

##### Bugs

As mentioned bugs should include before and after output.

###### Comment

Before:
```
$ ./check-alb-target-group-health.rb -r us-west-2
ExceptionBlagh
```

After:
```
$ ./check-alb-target-group-health.rb -r us-west-2
CheckALBTargetGroupHealth OK: All ALB target groups are healthy
```

Here is a real one: https://github.com/sensu-plugins/sensu-plugins-ssl/pull/28#issue-232465754

###### Gists

Before: https://gist.github.tld/user/somegist (find a real example and come back later to update)

After: https://gist.github.com/rwky/e5eabfa4ae1e7713c0503498cdc37dca

### Future

Nothing is more frustrating than starting a review, only to find that the tests are inadequate or absent. Very few PRs can touch code and NOT touch tests.

If you don't know how to test Feature-X, please ask!  We'll be happy to help you design things for easy testing or to suggest appropriate test cases.

## 8. Squashing and Commit Titles

Your reviewer has finally sent you feedback on Feature-X.

### Large Pull Requests

Make the requested changes, and don't `squash`/`fixup` yet. Put them in a new commit, and re-push. That way your reviewer can look at the new commit on its own, which is much faster than starting over.

We might still ask you to clean up your commits on large PRs at the very end for the sake of a more readable history, but don't do this until asked: typically at the point where the PR would otherwise be tagged `LGTM`.

### Small Pull Requests

On small pull requests after making requested changes we encourage you to `squash`/`fixup` as it is not a ton of effort to re-review and it means one less exchange to get merged.

### Commit Titles

Each commit should have a good title line (<80 characters) and include an additional description paragraph describing in more detail the change intended. For small *and* simple commits a paragraph may be overkill.

**General squashing guidelines:**

* Sausage => squash

 Do squash when there are several commits to fix bugs in the original commit(s), address reviewer feedback, etc. Really we only want to see the end state and commit message for the whole PR.

* Layers => don't squash

 Don't squash when there are independent changes layered to achieve a single goal.

A commit, as much as possible, should be a single logical change.

## 9. KISS, YAGNI, MVP, etc.

Sometimes we need to remind each other of core tenets of software design - Keep It Simple, You Aren't Gonna Need It, Minimum Viable Product, and so on. Adding a feature "because we might need it later" is antithetical to software that ships. Add the things you need NOW and (ideally) leave room for things you might need later - but don't implement them now.

## 10. It's OK to Push Back

Sometimes reviewers make mistakes and can disagree. It's OK to push back on changes your reviewer requested. If you have a good reason for doing something a certain way, you are absolutely allowed to debate the merits of a requested change. Both the reviewer and submitter should strive to discuss these issues in a polite and respectful manner.

You might be overruled, but you might also prevail. We're pretty reasonable people. Mostly.

Another phenomenon of open-source projects (where anyone can comment on any issue) is the dog-pile - your PR gets so many comments from so many people it becomes hard to follow. In this situation, you can ask the primary reviewer (assignee) whether they want you to fork a new PR to clear out all the comments. You don't HAVE to fix every issue raised by every person who feels like commenting, but you should answer reasonable comments with an explanation.

## Common Sense and Courtesy

No document can take the place of common sense and good taste. Use your best judgment, while you put
a bit of thought into how your work can be made easier to review. If you do these things your PRs will get merged with less friction.
