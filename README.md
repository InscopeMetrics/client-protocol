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
that `Record`. For more information about `Identifier` encoding please see below.

### Samples

Encode each metric's measurements into each `MetricSampleEntry` instance.

### Statistics

Encode each metric's statistics into each `MetricStatisticsEntry` instance. The `Statistics` is extensible supporting encoding
of different types of statistics. At present, only `AugmentedHistogram` is supported.

### Identifiers

Even under extensive measurement, the identifiers in a payload occupy a non-trivial amount of static space in each requset. Instead of
clients sending the actual `string` identifiers with each request, the client and server can agree on a `int64` id to use during a session
for a particular `string`.

#### Flow

1) Client sends a request with `string` identifiers
2) Server responds with a mapping of each `string` identifier to a `int64` identifier
3) Client sends subsequent requests with `int64` identifiers for recognized values and `string` identifiers for unrecognized ones
4) Server responds with a mapping of each `string` identifier to a `int64` id

#### Resets

* If the server restarts then the server will reject a request with `int64` identifiers
* If the client restarts then the client will send a new "first" request with only `string` identifiers

#### Clustering

The servers must compute the `int64` identifiers for each `string` identifier in a predictable manner. Therefore, a client talking to a
cluster of K servers will be rejected at most K times (without restarts) before enuring all servers have the same identifier mapping. Since
Metrics Aggregator Daemon instances are typically not clustered this way (use the Cluster Aggregator instead!) this is not a significant
concern.


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
