### How to transfer a repo to the community

Basically this will outline the basic process to transfer a repo over to be community maintained. It consists of a few steps:

1. Create an issue on [Our Plugin Community Issues](https://github.com/sensu-plugins/community/issues/new) which should have a template that asks a few questions to determine if you would like to continue maintaining it or not.
1. A maintainer will evaluate and assign the issue to themselves.
1. Attempt to bring the plugin into as much alignment as possible to our [Skel](https://github.com/sensu-plugins/sensu-plugins-skel)
1. Depending on whether it is a personal or an organizational repo the requirements are slightly different. In order to transfer the repo out you must be an owner on the repo and to transfer in you must be an owner in the `sensu-plugins` org to accept it.
   - [Transfer a personal repo](https://help.github.com/articles/transferring-a-repository-owned-by-your-personal-account)
   - [Transfer a org repo](https://help.github.com/articles/transferring-a-repository-owned-by-your-organization/)
1. Once the transfer has been initiated to the maintainer he will then transfer it to their account and then to the org (unless they happen to be an owner in both but they would probably not need this guide)
1. Once this has been completed the maintainer should then mark the issue with a label of `Repo Created` and then do the required setup to do various things like:
   - terraform setup
   - travis setup
   - rubygems setup
   - badges
   - cleanup
1. Once everything is setup the issue should be closed and any concerns like adding additional documentation, testing, etc should create issues in the respective repo.
