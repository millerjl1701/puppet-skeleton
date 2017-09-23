## Thank you!

Wanting a streamlined puppet skeleton for working on just Puppet 4 and beyond, I started using the excellent puppet-module-skeleton repository (https://github.com/garethr/puppet-module-skeleton) as a starting point. Hence me starting out with a huge and hearty thank you to Gareth and all the contributors to this prior. Before starting this, I looked at the new Puppet Development Kit (https://docs.puppet.com/pdk/latest/index.html) from Puppet which I think eventually replace this. However, it is currently just starting up. Perhaps, one day...

Many of the changes in here as well came from standard practices used by the Vox Pupuli community (https://voxpupuli.org/ , https://github.com/voxpupuli/modulesync_config ) and their assorted already published modules.

Another source of inspiration for files to change and add is the Puppet NTP module v.6.2.0 (https://github.com/puppetlabs/puppetlabs-ntp/)- the gold standard for Puppet's view of module development.


## Introduction

Puppet modules often take on the same file system structure. The
built-in puppet-module tool makes starting modules easy, but the built
in skeleton module is very simple. This skeleton is very opinionated.
It's going to assume you're going to start out with tests (both unit and
system), that you care about the puppet style guide, test using Travis,
keep track of releases and structure your modules according to strong
conventions.

## Installation

As a feature, puppet module tool will use `~/.puppetlabs/opt/puppet/cache/puppet-module/` as template for its `generate` command. The files provided here are meant to be better templates for use with the puppet module tool.

A note about development: I currently am using rvm to manage multiple Ruby environments (2.0.0, 2.1.10, 2.3.1, 2.4.1) on macOS 10.12. This may or may not work on your particular operating system or version of Ruby.

## Manual install

As we don't want to have our .git files and this README in our skeleton, we export it like this :

### for puppet 4.x

    git clone https://github.com/millerjl1701/puppet-skeleton
    cd puppet-skeleton
    find skeleton -type f | git checkout-index --stdin --force --prefix="$HOME/.puppetlabs/opt/puppet/cache/puppet-module/" --

## the install.sh

There is an installation script that Gareth wrote and is still in the repository; however, I don't use it.

## Usage

Then just generate your new module structure like so:

    puppet module generate user-module

Once you have your module then install the development dependencies:

    cd user-module
    bundle install --path=.vendor --without system_tests

Now you should have a bunch of rake commands to help with your module development similar to the below list. There will likely be many more than these when the bundle command completes:

    bundle exec rake -T
    rake acceptance        # Run acceptance tests
    rake build             # Build puppet module package
    rake clean             # Clean a built module package
    rake contributors      # Populate CONTRIBUTORS file
    rake coverage          # Generate code coverage information
    rake help              # Display the list of available rake tasks
    rake lint              # Check puppet manifests with puppet-lint / Run puppet-lint
    rake spec              # Run spec tests in a clean fixtures directory
    rake spec_clean        # Clean up the fixtures directory
    rake spec_prep         # Create the fixtures directory
    rake spec_standalone   # Run spec tests on an existing fixtures directory
    rake syntax            # Syntax check Puppet manifests and templates
    rake syntax:manifests  # Syntax check Puppet manifests
    rake syntax:templates  # Syntax check Puppet templates

Of particular interst should be:

* `rake spec` - run unit tests
* `rake lint` - checks against the puppet style guide
* `rake syntax` - to check your have valid puppet and erb syntax
* `rake metadata_lint` - to check your have a valid metadata.json file

## Thanks

The trick used in the installation above, and a few other bits came from
another excellent module skeleton from [spiette](https://github.com/spiette/puppet-module-skeleton).
