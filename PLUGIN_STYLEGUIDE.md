# Contents
---
- [Objective](#objective)
- [Format](#format)
- [Structure](#structure)
    - [Overview](#overview)
    - [Files](#files)
    - [Usage Examples](#usage-examples)
    - [Configuration](#configuration)
        - [Asset registration](#asset-registration)
        - [Asset definition](#asset-definition)
        - [Resource definitions](#resource-definitions)
    - [Installation from source](#installation-from-source)
    - [Additional notes](#additional-nodes)
    - [Contributing](#contributing)
- [Plugin collections](#plugin-collections)
- [Tables of contents](#tables-of-contents)

# Objective

Thank you for your interest in contributing to the Sensu community! Contributing plugins is a great way to get involved, and we want to help you effectively explain  how to use your plugin.  

This guide is designed to help you and other Sensu plugin authors describe your plugin’s use and facilitate consistency among community plugin READMEs. Because many users throughout the Sensu community rely on plugins, we value plugin documentation that:

* Is readable and free of jargon
* Focuses on users
* Clearly describes what the plugin does
* Includes examples of how to use and deploy the plugin

# Format

Plugin READMEs are Markdown documents. Write your README in [GitHub-flavored Markdown](https://guides.github.com/features/mastering-markdown/) to ensure it is properly rendered on Bonsai. 

# Structure

Organize your plugin README according to this overall structure:

* Overview
* Files
* Usage examples
* Configuration
  * Asset registration
  * Asset definition
  * Resource definitions
* Installation from source
* Additional notes
* Contributing
* Contributing



## Overview

Begin with an overview of the plugin’s functionality. Describe what the plugin does and what it’s used for. Here are some examples of good overviews from Sensu plugins:



*   [Prometheus Collector](https://github.com/sensu/sensu-prometheus-collector#overview)
*   [Linux System Profiler](https://github.com/sensu/system-profile-linux#overview)
*   [Influxdb Handler](https://github.com/sensu/sensu-influxdb-handler#sensu-influxdb-handler)
*   [Fatigue Check Filter](https://github.com/nixwiz/sensu-go-fatigue-check-filter#sensu-go-fatigue-check-filter)
*   [Has Contact Filter](https://github.com/sensu/sensu-go-has-contact-filter#sensu-go-has-contact-filter)


## Files

If the project is a collection (grouping of multiple plugins), the README should include a list of executable plugin files. If the project is not a collection, you do not need to include a list of files.


## Usage

Plugin documentation should include a usage section, which should show the help output for the plugin, if available. Otherwise, any supported configuration via command-line arguments or environment variables should be thoroughly documented in the usage section.


## Configuration

The bulk of a plugin’s README is often in the configuration section, which includes asset registration, asset definition, and resource definition examples.


### Asset registration

The **Asset registration** section should contain the following boilerplate language:


    Assets are the best way to make use of this plugin. If you're not using an asset, please consider doing so! If you're using sensuctl 5.13 with Sensu Backend 5.13 or later, you can use the following command to add the asset: 


    `sensuctl asset add CHANGEME/sensu-CHANGEME:VERSION`


    If you're using an earlier version of sensuctl, you can find the asset on the [Bonsai Asset Index]([https://bonsai.sensu.io/assets/CHANGEME/sensu-CHANGEME](https://bonsai.sensu.io/assets/CHANGEME/sensu-CHANGEME)).

In general, avoid recommending building the plugin from source. Instead, use sensuctl asset add or create a definition manually via sensuctl create -f /path/to/asset-definition.yml.


### Asset definition

Users can install asset definitions using `sensuctl asset add`, but we recommend including an example asset definition in your plugin README. Format your example in yaml.


### Resource definitions

In the resource definitions, include example check, filter, mutator, or handler definitions (depending on the resources in your plugin). Format your resource definitions in yaml.


## Installation from source

Assets are the preferred plugin installation method. If you cannot use an asset to install your plugin, make sure to provide all the documentation users will need to compile your plugin from source. Some useful examples of plugins providing instructions for installing from source are:

*   [InfluxDB Handler](https://github.com/sensu/sensu-influxdb-handler#dependencies)
*   [Slack Handler](https://github.com/sensu/sensu-slack-handler#installing-from-source-and-contributing)

## Additional notes

Use the **Additional notes** section to provide further context for users who will download and deploy your plugin. For example, you might explain whether your plugin requires an on-disk configuration file to properly operate (such as templates for notification plugins) or recommend that users create RBAC roles that allow your plugin to make calls to the Sensu backend API. Describe any additional configuration needed to operate your plugin in this section.

## Contributing

We recommend that all community plugins include a **CONTRIBUTING** document in their repositories. If you create a plugin from the [Sensu Go Plugin](https://github.com/sensu/sensu-go-plugin) repository, a CONTRIBUTING document is included in the repository. If you create a plugin using a different method, you can add your own CONTRIBUTING document. Examples of CONTRIBUTING documents from the community include:

*   [Contributing to Sensu Go](https://github.com/sensu/sensu-go/blob/master/CONTRIBUTING.md)
*   [Sensu Plugins Developer Guidelines](http://sensu-plugins.io/docs/developer_guidelines.html)


# Plugin collections

We recommend adopting the [Unix Philosophy](https://homepage.cs.uri.edu/~thenry/resources/unix_art/ch01s06.html): write a plugin that does one thing well, and avoid collections of plugins. Collections may simplify deployment, but they complicate documenting your plugin’s functionality. 

If your plugin is a collection, please document each plugin component so it’s clear what each does. 

# Tables of contents

The table of contents is a reader’s first impression of a plugin and should help them find the information they need. Each plugin’s README should include a table of contents that follows the structure described in this style guide.

Here’s an example table of contents:

```markdown
- [Overview](#overview)
- [Files](#files)
- [Usage examples](#usage-examples)
- [Configuration](#configuration)
  - [Asset registration](#asset-registration)
  - [Asset definition](#asset-definition)
  - [Resource definition](#resource-definition)
- [Installation from source](#installation-from-source)
- [Additional notes](#additional-notes)
- [Contributing](#contributing)
```
