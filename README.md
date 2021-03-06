# kafka cookbook

[![Build Status](https://travis-ci.org/mthssdrbrg/kafka-cookbook.png?branch=master)](https://travis-ci.org/mthssdrbrg/kafka-cookbook)

Installs Kafka `v0.8.0`, and probably any newer versions.

Based on the Kafka cookbook released by WebTrends (thanks!), but with a few
notable differences:

* supports both source and binary releases (`>= v0.8.0`).
* does not depend on runit cookbook.
* does not depend on zookeeper cookbook, thus it will not search for nodes with
  a specific role or such, that is left up to you to decide.
* only tested on Vagrant boxes.
* intended to be used by wrapper cookbooks.

## Requirements

This cookbook does not depend on any specific cookbooks, but it requires that
java is installed on the system, thus the `java` cookbook is recommended.

Ruby 1.9.3+ and Chef 11.8.2+.

### Platform

* Debian 7.2.0
* Ubuntu 12.04 & 13.10
* CentOS 6.5
* Fedora 18

Might work on other platforms / versions, but these are the ones that are
included in `.kitchen.yml`, so YMMV.
For some reason the `java` cookbook does not set the correct java path on Fedora
19 and 20, which is why Fedora 18 is used rather than the 19 or 20 releases.

## Attributes

In order to keep the README in some kind of manageable state (and thus in sync
with attributes), attributes are documented inline (in the `attribute` files
that is).

All of the configuration parameters defined in the official Kafka documentation
should be available as attributes (this applies to `v0.8.0`, `v0.8.1` and
`v0.8.1.1`).

Almost all of the attributes are set to `nil` by default, thus the default
values defined in Kafka will be used instead, since the Kafka team will most
likely be better at keeping values up-to-date, and this cookbook won't have to
be responsible for setting "correct" default values.

Configuration attributes that are `nil` will still show up in the rendered
configuration file, but they will be "commented".

In the case that there's a new release of Kafka and you notice that there are
configuration parameters that are not included in this cookbook, pull requests
are welcome.

## Recipes

This section describes the different recipes that exists, and how to use them.

### default

Includes either `source` or `binary` recipe depending on what
`node[:kafka][:install_method]` is set to (`:source, :binary`).

### source

Downloads, compiles and installs Kafka from the official source releases.
Defaults to installing `v0.8.1.1` of Kafka.

### binary

Downloads and installs Kafka from the official binary releases.
Defaults to installing `v0.8.1.1` of Kafka.

### zookeeper

Sets up a standalone ZooKeeper server, using the ZooKeeper version that is
bundled with Kafka.

This should not be used in production (Kafka and ZooKeeper should generally not
run on the same machine) and is just useful for testing (i.e. in Vagrant or
other testing environment).

## Copyright

Copyright :: 2013-2014 Mathias Söderberg and contributors

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

## Contributing

1. Fork the repository on Github
2. Create a named feature branch (like `add-component-x`)
3. Write your change
4. Check that your change works, for example with Vagrant
5. Submit a Pull Request using Github
