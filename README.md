Metrics Client Protocol
===========================

<a href="https://raw.githubusercontent.com/InscopeMetrics/client-protocol/master/LICENSE">
    <img src="https://img.shields.io/hexpm/l/plug.svg"
         alt="License: Apache 2">
</a>
<a href="https://travis-ci.org/InscopeMetrics/client-protocol/">
    <img src="https://travis-ci.org/InscopeMetrics/client-protocol.png"
         alt="Travis Build">
</a>
<a href="http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22io.inscopemetrics.metrics%22%20a%3A%22client-protocol%22">
    <img src="https://img.shields.io/maven-central/v/io.inscopemetrics.metrics/client-protocol.svg"
         alt="Maven Artifact">
</a>

Defines a protocol for transmitting metric samples or statistics from a client to an aggregator.

Features
--------

### Dimensions

Encode each record's dimensions as a key-value pair of identifiers. The dimensions on a `Record` apply to all samples and statistics on
that `Record`.

### Samples

Encode each metric's measurements into each `MetricSampleEntry` instance. The samples are all of one type. Currently, only `double` values
are supported for samples.

### Statistics

Encode each metric's statistic into each `MetricStatisticsEntry` instance. Encoding a statistic and samples for the same metric is valid
so long as the statistic and samples are of compatible types. Currently, only `AugmentedHistogram` statistic is supported and can be paired
with `DoubleSamples` type samples.

### Identifiers

Even under intensive (broad and frequent) measurement, the identifiers in a payload occupy a non-trivial amount of static space in each
request. Instead, of clients sending the actual `string` identifiers with each request this format will support sending identifiers instead.
The client and server would agree on a `int64` id to use during a session for a particular `string`. _This feature is not yet implemented_.

Building
--------

Prerequisites:
* _None_

Building:

    client-protocol> ./jdk-wrapper.sh ./mvnw verify

To use the local version you must first install it locally:

    client-protocol> ./jdk-wrapper.sh ./mvnw install

You can determine the version of the local build from the pom file.  Using the local version is intended only for testing or development.

You may also need to add the local repository to your build in order to pick-up the local version:

* Maven - Included by default.
* Gradle - Add *mavenLocal()* to *build.gradle* in the *repositories* block.
* SBT - Add *resolvers += Resolver.mavenLocal* into *project/plugins.sbt*.

License
-------

Published under Apache Software License 2.0, see LICENSE

&copy; Inscope Metrics Inc., 2016
