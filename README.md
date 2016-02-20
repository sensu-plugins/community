## Sensu-Plugins-feature-requests

[![Build Status](https://travis-ci.org/sensu-plugins/sensu-plugins-feature-requests.svg?branch=master)](https://travis-ci.org/sensu-plugins/sensu-plugins-feature-requests)
[![Code Climate](https://codeclimate.com/github/sensu-plugins/sensu-plugins-feature-requests/badges/gpa.svg)](https://codeclimate.com/github/sensu-plugins/sensu-plugins-feature-requests)
[![Test Coverage](https://codeclimate.com/github/sensu-plugins/sensu-plugins-feature-requests/badges/coverage.svg)](https://codeclimate.com/github/sensu-plugins/sensu-plugins-feature-requests)
[![Dependency Status](https://gemnasium.com/sensu-plugins/sensu-plugins-feature-requests.svg)](https://gemnasium.com/sensu-plugins/sensu-plugins-feature-requests)

## Functionality

## Files
 *
 *
 *
 *

## Usage

## Installation

Add the public key (if you haven’t already) as a trusted certificate

```
gem cert --add <(curl -Ls https://raw.githubusercontent.com/sensu-plugins/sensu-plugins.github.io/master/certs/sensu-plugins.pem)
gem install sensu-plugins-feature-requests -P MediumSecurity
```

You can also download the key from /certs/ within each repository.

#### Rubygems

`gem install sensu-plugins-feature-requests`

#### Bundler

Add *sensu-plugins-sensu-plugins-feature-requests* to your Gemfile and run `bundle install` or `bundle update`

#### Chef

Using the Sensu **sensu_gem** LWRP
```
sensu_gem 'sensu-plugins-feature-requests' do
  options('--prerelease')
  version '0.0.1'
end
```

Using the Chef **gem_package** resource
```
gem_package 'sensu-plugins-feature-requests' do
  options('--prerelease')
  version '0.0.1'
end
```

## Notes
