[![][Build Status img]][Build Status]
[![][license img]][license]
[![][Maven Central img]][Maven Central]
[![][Javadocs img]][Javadocs]

# influx4j

InfluxDB is a high-performance time-series database.  You need a Java driver to match.

When jamming tens-of-thousands of metrics into InfluxDB *per minute*, you can't afford Stop-The-World garbage collection times reaching into the hundreds (or thousands) of milliseconds.  And you can't afford to senselessly burn CPU cycles.

### *10x* Faster.&nbsp;&nbsp;*10x* Less CPU.&nbsp;&nbsp;*Infinity* Less Garbage.

*influx4j is wickedly fast.* 10 times faster than the offical driver.  *influx4j is a CPU miser.*  10 times less CPU consumption persisting a datapoint than the official driver.  *influx4j generates ZERO garbage from Point to Protocol.*  Infinitely less garbage than the official driver.

As measured by the [JMH](http://www.oracle.com/technetwork/articles/java/architect-benchmarking-2266277.html) benchmark, included in this project, comparing *influx4j* with the official driver, Point-to-protocol ...

#### 45 Second run:
| Driver           | Points Produced<br><sup>(approx.)</sup> | Points/ms<br><sup>(approx.)</sup> | Garbage<br>Produced  | Avg Garbage<br>Creation Rate | G1 Garbage<br>Collections |
|:---------------- | ---------------------------------------:| ------:|:--------------------:|:--------------------:|:----------------------:|
| *influx4j*       | 192 million  | 4267 | *zero*   | *zero*       | *zero* |
| *influxdb-java*  | 18 million   |  406 | 334.64 gb | 6.17 gb/sec | 766 |
<br>
Zero garbage means the JVM interrupts your performance critical code less.<sup>1</sup>  The extreme efficiency of the Point-to-protocol buffer serialization pipeline means you burn 10x less CPU producing the same number of points compared to the official driver.

<sub><sup>1</sup>&nbsp;Note: While influx4j generates zero garbage, *your application*, and *associated libraries* likely generate garbage that will still require collection.</sub>

See the [InsertionTest](https://github.com/brettwooldridge/influx4j/blob/master/src/test/java/com/zaxxer/influx4j/InsertionTest.java) for example usage, until I have time to write full docs.

:warning: This driver currently only supports *write-only* operation to InfluxDB, where performance is critical.  I *do* intend to add query support, but the schedule for doing so is currently uncommitted.


[Build Status]:https://travis-ci.org/brettwooldridge/influx4j
[Build Status img]:https://travis-ci.org/brettwooldridge/influx4j.svg?branch=master

[license]:LICENSE
[license img]:https://img.shields.io/badge/license-Apache%202-blue.svg

[Maven Central]:https://maven-badges.herokuapp.com/maven-central/com.zaxxer/influx4j
[Maven Central img]:https://maven-badges.herokuapp.com/maven-central/com.zaxxer/influx4j/badge.svg

[Javadocs]:http://javadoc.io/doc/com.zaxxer/influx4j
[Javadocs img]:http://javadoc.io/badge/com.zaxxer/influx4j.svg
