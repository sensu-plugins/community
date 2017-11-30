## Sensu Plugins Feature Requests

Your place to contribute to Sensu plugins and their maintainers.

## Background

Sensu plugins can be found [all over GitHub](https://github.com/search?utf8=%E2%9C%93&q=sensu-plugin&type=). Community maintainers of Sensu collect them, code review and manage their releases under the [Sensu Plugins organization](https://github.com/sensu-plugins). This results in [the many gems](https://rubygems.org/search?utf8=%E2%9C%93&query=sensu-plugin) we all rely on.

## How to Use This Repo

Please [open Issues](https://github.com/sensu-plugins/sensu-plugins-feature-requests/issues) for anything on your mind that will help the community succeed at having **the best collection of monitoring plugins.**

Common requests are:

* Transfer ownership of your rad Sensu plugin to this organization ([example][1])
* Offer an awesome idea that will help others make great plugins ([example][3])

## How You Can Help

The success of Sensu depends on its contributors. You can always help the maintainers by:

* [Reviewing open PRs][4] (especially if you're familiar with technology involved)
* Reviewing and commenting on [open Issues][5] (especially older ones)
* Opening PRs that resolve [open Issues][5]
* Volunteer as a maintainer (after you've done these :point_up: for some time)

And **thank you** for your contribution. It adds to the monitoring love :heart:.

## Maintained Areas

Maintainers do their best to cover the diverse set of plugins and adjacent technologies that make using Sensu a joy.

| Area                         | Major Links                                                    | Maintainers                                                                                                                                        | Needs Contributors?                                                                           |
|:-----------------------------|:---------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------|
| ![Sensu Org][sensu_pic]      | [Plugins Org][plug_org]</br>[Extensions Org][ext_org]          | **[Matt (@mbbroberg) - Lead][11]**</br>[Ben (@majormoses)][9]</br>[Eric (@eheydrick)][10]</br>[Luis (@luisdavim)][12]</br>[Shane (@sstarcher)][13] | **Yes!** [Read about how!][volunteer]                                                         |
| ![Ruby Plugin][ruby_pic]     | [Ruby Plugin Library][ruby_lib]                                | **[Cameron (@cwjohnston) - Lead][17]**</br>[Eric (@eheydrick)][10]</br>[Ben (@majormoses)][9]                                                      | **Yes!** [Please claim an open issue!](https://github.com/sensu-plugins/sensu-plugin/issues)  |
| ![Python Plugin][python_pic] | [Python Plugin Library][py_lib]                                | **[Barry (@barryorourke) - Lead][14]**</br>[Ben (@majormoses)][9]</br>[James (@absolutejam)][22]                                                   | **Yes!** [Help wanted on testing 🙏][py_helpwanted]                                           |
| ![Windows][windows_pic]      | [Windows Plugins][windows]                                     | **[James (@absolutejam) - Lead][22]**                                                                                                              | **Yes!** [Help review issues.](https://github.com/sensu-plugins/sensu-plugins-windows/issues) |
| ![Puppet][puppet_pic]        | [Puppet Module][puppet]                                        | **[Garrett (@ghoneycutt) - Lead](https://github.com/ghoneycutt)**                                                                                  | **Yes!** [Help review issues.](https://github.com/sensu/sensu-puppet/issues)                  |
| ![Chef][chef_pic]            | [Chef Cookbook][chef_sensu]</br>[Uchiwa Cookbook][chef_uchiwa] | **[Ben (@majormoses) - Lead][9]**</br>[Tom (@thomasriley)][18]                                                                                     | **Yes!** [Help review issues.](https://github.com/sensu/sensu-chef/issues)                    |
| ![Ansible][ansible_pic]      | [Ansible Role][ansible]</br>[Ansible Module][ans_module]       | **[Jared (@jaredledvina) - Lead][19]**</br>[Chris (@cjchand)][21]</br>[Calum (@cmacrae)][20]                                                       | **Yes!** [Help review issues.](https://github.com/sensu/sensu-ansible/issues)                 |
| ![SaltStack][salt_pic]       | [SaltStack Formula][saltstack]                                 |                                                                                                                                                    | **Yes!** [Please volunteer.](https://github.com/sensu-plugins/community/issues/79)            |

[sensu_pic]: https://avatars0.githubusercontent.com/u/10713628?s=50
[ruby_pic]: https://avatars2.githubusercontent.com/u/210414?s=50
[python_pic]: https://avatars0.githubusercontent.com/u/1525981?s=50
[windows_pic]: https://user-images.githubusercontent.com/1744971/32962538-aff30f08-cb81-11e7-86c2-b8aa226d211d.png
[puppet_pic]: https://avatars1.githubusercontent.com/u/9100?s=50
[chef_pic]: https://avatars3.githubusercontent.com/u/29740?s=50
[salt_pic]: https://avatars2.githubusercontent.com/u/1147473?s=50
[ansible_pic]: https://avatars1.githubusercontent.com/u/1507452?s=50
[plug_org]: https://github.com/sensu-plugins
[ext_org]: https://github.com/sensu-extensions
[ruby_lib]: https://github.com/sensu-plugins/sensu-plugin
[py_lib]: https://github.com/sensu-plugins/sensu-plugin-python
[windows]: https://github.com/sensu-plugins/sensu-plugins-windows
[saltstack]: https://github.com/sensu/sensu-salt
[puppet]: https://github.com/sensu/sensu-puppet
[chef_sensu]: https://github.com/sensu/sensu-chef
[chef_uchiwa]: https://github.com/sensu/uchiwa-chef
[ansible]: https://github.com/sensu/sensu-ansible
[ans_module]: https://github.com/ansible/ansible/tree/devel/lib/ansible/modules/monitoring
[volunteer]: https://github.com/sensu-plugins/community/blob/master/CONTRIBUTING.md
[py_helpwanted]: https://github.com/sensu-plugins/sensu-plugin-python/issues?q=is%3Aissue+is%3Aopen+label%3A%22Status%3A+Help+Wanted%22
[11]: https://github.com/sstarcher
[9]: https://github.com/majormoses
[10]: https://github.com/eheydrick
[12]: https://github.com/luisdavim
[13]: https://github.com/sstarcher
[15]: https://github.com/mattyjones
[14]: https://github.com/barryorourke
[16]: https://github.com/calebhailey
[17]: https://github.com/cwjohnston
[18]: https://github.com/thomasriley
[19]: https://github.com/jaredledvina
[20]: https://github.com/cmacrae
[21]: https://github.com/cjchand
[22]: https://github.com/absolutejam

## Other Resources

If you're working on building your own plugins, use [the skeleton plugin](https://github.com/sensu-plugins/sensu-plugins-skel) to get started!


[1]: https://github.com/sensu-plugins/sensu-plugins-feature-requests/issues/23
[2]: https://github.com/sensu-plugins/sensu-plugins-feature-requests/issues/17
[3]: https://github.com/sensu-plugins/sensu-plugins-feature-requests/issues/19
[4]: https://github.com/pulls?utf8=%E2%9C%93&q=is%3Aopen+is%3Apr+user%3Asensu-plugins
[5]: https://github.com/issues?q=is%3Aopen+is%3Aissue+user%3Asensu-plugins+sort%3Acomments-desc
