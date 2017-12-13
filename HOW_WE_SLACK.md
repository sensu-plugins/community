# How We Slack

Thanks for joining our Community Slack! This page will walk you through our approach. If you have any questions about anything here, please don't hesitate to contact the Community team at [community@sensu.io](mailto:community@sensu.io).

## Who We Are

The Sensu Community is a mix of open source users, developers, enterprise customers and monitoring enthusiasts. We encourage all members to participate in the collective learning happening everyday.

## Why We're here

Maintainers of Sensu made this Slack channel for the community to have a friendly place for real-time peer support, collaboration and fun.

## Register for Slack

To register for our Slack team, enter your email into the landing page at [slack.sensu.io](http://slack.sensu.io).

[<img width="345" alt="logging into Slack" src="https://user-images.githubusercontent.com/1744971/30298337-d5df6e5c-96ff-11e7-924d-8cec16c6c613.png">](http://slack.sensu.io)

## Channels of Interest

We have a somewhat unique approach to channels that we hope you enjoy. Here are the highlights:

| Channel             | Purpose                                                                  |
|:--------------------|:-------------------------------------------------------------------------|
| **#monitoringlove** | Default channel for all things Sensu as well as open discussion          |
| **#announcements**  | A read-only channel for major updates from the leadership team           |
| **#contributing**   | Dedicated place to offer or discussion contribution to the Sensu project |
| **#help**           | A breakout channel for detailed troubleshooting                          |

There's a pattern of Slack usage that says more channels is better. We don't subscribe to it 😛. We want to have as few channels as makes sense, where each on has a purpose and a maintainer. We also occasionally break out into speciality topics. Here are a few scenarios:

* You start a conversation in one of the project-focused channels, like `#plugins`, `#extensions` or `#core`, and then hop into `#help` to dive deeper
* You open a PR to fix a known issue and mention it in `#contributing`
* You find a new topic of interest has an active following and a new plugin, so we create `#new-topic`

You will also see channels for each major configuration management tool (like `#puppet`, `#chef`, and so on). Additional channels are welcome as needed.

### Sidecar Channels

If activity in one channel or its integrations (GitHub, Travis, etc) gets to be too high a volume, we can break it out into a separate place we call a **sidecar**.

If the volume is lower than our threshold (5 messages per day averaged over a week), it should go into the primary channel. For example, GitHub activity on [Sensu Ansible Playbook](https://github.com/sensu/sensu-ansible) and [Ansible Plugin](https://github.com/sensu-plugins/sensu-plugins-ansible) is low, so it goes directly into the `#ansible` channel. Plugins, on the other hand, are very active and have a `#plugins-activity` sidecar.

Naming is still up for debate, but here were some proposed naming conventions for any "sidecar" channels:

    contribute-to-$THING (apply below variations here)
    $THING-contributing
    $THING-activity
    $THING-github
    $THING-feed
    $THING-raw

## Administration

This Slack organization is maintained by the community team of Sensu Inc with help from maintainers. The list of all maintainers [is available here](README.md). You can reach all of us in #monitoringlove by asking for maintainers. If you want to privately contact an administrator, please email `community@sensu.io`.

### When Moderation Happens

In the rare occasions when [our Code of Conduct](https://sensuapp.org/conduct) is not followed, administrators of Slack have permission to delete content. Maintainers are required to review the incident with the rest of the project leads as well as to notify those who have had their content deleted.

## Slack-tiquette

Here are a few tips to make your time on Slack fun and productive. When in doubt, refer to [our Code of Conduct](https://sensuapp.org/conduct). It's really clear on acceptable communication and expectations. Feel free to ask questions in the `#monitoringlove` channel at any time as well.

### Non-SLA on Questions

This Slack is full of helpful folks, but is not bound by an SLA. For Sensu Enterprise customers, use [support@sensu.io](mailto:support@sensu.io) if you need a speedy response. If you are interested in paid support for Sensu, please [visit the website to compare options](https://sensuapp.org/support#compare).

### Notification Policies

Slack offers two channel-wide broadcast aliases: `@channel` and `@here`. This community is setup where only Admins can use them in order to prevent alert fatigue.

### Repeat Questions

Please post a question in one channel at a time. If you're not sure where, default to `#monitoringlove` to get the most visibility. There will be times when questions are asked and do not receive an answer. Feel free to repeat your question later on when more people are around, or wait for a community member to scrollback and answer it.

### Setup your Profile

Once registered, all members have access to customize their profile [through the Slack
website](https://sensucommunity.slack.com/account/profile). We appreciate when you add a distinct avatar and other details about themselves so others can get to know you.

### Sharing Policies

We do ask any content that is not directly related to Sensu or the monitoring ecosystem is kept out of this Slack. When in doubt, use thoughtful judgement and always consider [our Code of Conduct](https://sensuapp.org/conduct).

We also ask that community members help in the curation of the conversations happening in the channels they care about. If a member posts something not relevant to a channel you're in, ask them to share it in `#monitoringlove` or to not share links like that in the future. If you run into any challenges with this policy, please email [community@sensu.io](mailto:community@sensu.io).

### Vote with your Feet

You are more than welcome to leave channels and rejoin them at any time. The only "required" channel for everyone to be in is `#announcements`.

## FAQ

* **What do you like about Slack?**
  * Slack is an application that almost everyone has open all the time. Signing into the Sensu community gets that much easier thanks to it. It also gives us multiple channels, app integrations that are easy to setup and a beautiful user experience.
* **Why did you leave IRC?**
  * It came down to a judgement call that IRC was too difficult for new Users to get involved. We needed more channels like Slack offers with consistent accounts so people can find answers after that logout.  
* **I Really Like IRC, What Do I Do?**
  * Slack does offer an [IRC gateway](https://get.slack.help/hc/en-us/articles/201727913-Connecting-to-Slack-over-IRC-and-XMPP),
though it has historically had some quirky behavior
