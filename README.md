[![Build Status](https://travis-ci.org/ben-manes/caffeine.svg)](https://travis-ci.org/ben-manes/caffeine)
[![Coverage Status](https://img.shields.io/coveralls/ben-manes/caffeine.svg)](https://coveralls.io/r/ben-manes/caffeine?branch=master)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.github.ben-manes.caffeine/caffeine/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.github.ben-manes.caffeine/caffeine)
[![JavaDoc](http://www.javadoc.io/badge/com.github.ben-manes.caffeine/caffeine.svg)](http://www.javadoc.io/doc/com.github.ben-manes.caffeine/caffeine)
[![License](http://img.shields.io/:license-apache-brightgreen.svg)](http://www.apache.org/licenses/LICENSE-2.0.html)
[![Stack Overflow](http://img.shields.io/:stack%20overflow-caffeine-brightgreen.svg)](http://stackoverflow.com/questions/tagged/caffeine)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fjeffdinotoriverbed%2Fcaffeine.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Fjeffdinotoriverbed%2Fcaffeine?ref=badge_shield)
<a href="https://github.com/ben-manes/caffeine/wiki">
<img align="right" height="90px" src="https://raw.githubusercontent.com/ben-manes/caffeine/master/wiki/logo.png">
</a>

Caffeine is a [high performance][benchmarks], [near optimal][efficiency] caching library based on
Java 8. For more details, see our [user's guide][users-guide] and browse the [API docs][javadoc] for
the latest release.

### Cache

Caffeine provides an in-memory cache using a Google Guava inspired API. The improvements draw on our
experience designing [Guava's cache][guava-cache] and [ConcurrentLinkedHashMap][clhm].

```java
LoadingCache<Key, Graph> graphs = Caffeine.newBuilder()
    .maximumSize(10_000)
    .expireAfterWrite(5, TimeUnit.MINUTES)
    .refreshAfterWrite(1, TimeUnit.MINUTES)
    .build(key -> createExpensiveGraph(key));
```

#### Features at a Glance

Caffeine provides flexible construction to create a cache with a combination of the following features:
 * [automatic loading of entries][population] into the cache, optionally asynchronously
 * [size-based eviction][size] when a maximum is exceeded based on [frequency and recency][efficiency]
 * [time-based expiration][time] of entries, measured since last access or last write
 * [asynchronously refresh][refresh] when the first stale request for an entry occurs
 * keys automatically wrapped in [weak references][reference]
 * values automatically wrapped in [weak or soft references][reference]
 * [notification][listener] of evicted (or otherwise removed) entries
 * [writes propagated][writer] to an external resource
 * accumulation of cache access [statistics][statistics]

In addition, Caffeine offers the following extensions:
 * [JSR-107 JCache][jsr107]
 * [Guava adapters][guava-adapter]
 * [Simulation][simulator]

Use Caffeine in a community provided integration:
 * [Play Framework][play]: High velocity web framework
 * [Micronaut][micronaut]: A modern, full-stack framework
 * [Spring Cache][spring]: As of Spring 4.3 & Boot 1.4
 * [Akka][akka-http]: Build reactive applications easily
 * [Scaffeine][scaffeine]: Scala wrapper for Caffeine
 * [ScalaCache][scala-cache]: Simple caching in Scala
 * [Camel][camel]: Routing and mediation engine
 * [jooby][jooby]: Modular micro framework
 * [Druid][druid]: Real-time analytics

Powering infrastructure near you:
 * [Dropwizard][dropwizard]: Ops-friendly, high-performance, RESTful APIs
 * [Cassandra][cassandra]: Manage massive amounts of data, fast
 * [Accumulo][accumulo]: A sorted, distributed key/value store
 * [HBase][hbase]: A distributed, scalable, big data store
 * [Infinispan][infinispan]: Distributed in-memory data grid
 * [Ratpack][ratpack]: Lean & powerful HTTP apps
 * [Corfu][corfu]: A cluster consistency platform
 * [Grails][grails]: Groovy-based web framework
 * [Orbit][orbit]: Virtual actors on the JVM
 * [Finagle][finagle]: Extensible RPC system
 * [Neo4j][neo4j]: Graphs for Everyone

### In the News

 * An in-depth description of Caffeine's architecture.
   * [Design of a Modern Cache: part #1][modern-cache-1], [part #2][modern-cache-2] ([slides][modern-cache-slides]) at [HighScalability][HighScalability]
 * Caffeine is presented as part of research papers evaluating its novel eviction policy.
   * [TinyLFU: A Highly Efficient Cache Admission Policy][tinylfu] by Gil Einziger, Roy Friedman, Ben Manes
   * [Adaptive Software Cache Management][adaptive-tinylfu] by Gil Einziger, Ohad Eytan, Roy Friedman, Ben Manes

### Download

Download from [Maven Central][maven] or depend via Gradle:

```gradle
compile 'com.github.ben-manes.caffeine:caffeine:2.7.0'

// Optional extensions
compile 'com.github.ben-manes.caffeine:guava:2.7.0'
compile 'com.github.ben-manes.caffeine:jcache:2.7.0'
```

See the [release notes][releases] for details of the changes.

Snapshots of the development version are available in
[Sonatype's snapshots repository][snapshots].

[benchmarks]: https://github.com/ben-manes/caffeine/wiki/Benchmarks
[users-guide]: https://github.com/ben-manes/caffeine/wiki
[javadoc]: http://www.javadoc.io/doc/com.github.ben-manes.caffeine/caffeine
[guava-cache]: https://github.com/google/guava/wiki/CachesExplained
[clhm]: https://code.google.com/p/concurrentlinkedhashmap
[population]: https://github.com/ben-manes/caffeine/wiki/Population
[size]: https://github.com/ben-manes/caffeine/wiki/Eviction#size-based
[time]: https://github.com/ben-manes/caffeine/wiki/Eviction#time-based
[refresh]: https://github.com/ben-manes/caffeine/wiki/Refresh
[reference]: https://github.com/ben-manes/caffeine/wiki/Eviction#reference-based
[listener]: https://github.com/ben-manes/caffeine/wiki/Removal
[writer]: https://github.com/ben-manes/caffeine/wiki/Writer
[statistics]: https://github.com/ben-manes/caffeine/wiki/Statistics
[simulator]: https://github.com/ben-manes/caffeine/wiki/Simulator
[guava-adapter]: https://github.com/ben-manes/caffeine/wiki/Guava
[jsr107]: https://github.com/ben-manes/caffeine/wiki/JCache
[maven]: https://maven-badges.herokuapp.com/maven-central/com.github.ben-manes.caffeine/caffeine
[releases]: https://github.com/ben-manes/caffeine/releases
[snapshots]: https://oss.sonatype.org/content/repositories/snapshots
[efficiency]: https://github.com/ben-manes/caffeine/wiki/Efficiency
[tinylfu]: https://dl.acm.org/authorize?N41277
[adaptive-tinylfu]: https://dl.acm.org/authorize?N675830
[add-a-boost]: https://www.voxxed.com/blog/2015/12/add-a-boost-of-caffeine-to-your-java
[voxxed]: https://www.voxxed.com
[modern-cache-1]: http://highscalability.com/blog/2016/1/25/design-of-a-modern-cache.html
[modern-cache-2]: http://highscalability.com/blog/2019/2/25/design-of-a-modern-cachepart-deux.html
[modern-cache-slides]: https://docs.google.com/presentation/d/1NlDxyXsUG1qlVHMl4vsUUBQfAJ2c2NsFPNPr2qymIBs
[highscalability]: http://highscalability.com
[spring]: https://docs.spring.io/spring/docs/current/spring-framework-reference/integration.html#cache-store-configuration-caffeine
[scala-cache]: https://github.com/cb372/scalacache
[scaffeine]: https://github.com/blemale/scaffeine
[hbase]: https://hbase.apache.org
[cassandra]: http://cassandra.apache.org
[solr]: https://issues.apache.org/jira/browse/SOLR-8241
[infinispan]: http://infinispan.org/docs/stable/user_guide/user_guide.html#eviction_strategy
[neo4j]: https://github.com/neo4j/neo4j
[ratpack]: https://github.com/ratpack/ratpack
[finagle]: https://github.com/twitter/finagle
[druid]: http://druid.io/docs/latest/development/extensions-core/caffeine-cache.html
[jooby]: http://jooby.org/doc/caffeine
[orbit]: https://github.com/orbit/orbit
[camel]: https://github.com/apache/camel/blob/master/components/camel-caffeine/src/main/docs/caffeine-cache-component.adoc
[corfu]: https://github.com/CorfuDB/CorfuDB
[akka-http]: https://doc.akka.io/docs/akka-http/current/common/caching.html
[micronaut]: https://docs.micronaut.io/latest/guide/index.html#caching
[play]: https://www.playframework.com/documentation/latest/JavaCache
[accumulo]: https://accumulo.apache.org
[dropwizard]: https://www.dropwizard.io
[grails]: https://grails.org


## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fjeffdinotoriverbed%2Fcaffeine.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Fjeffdinotoriverbed%2Fcaffeine?ref=badge_large)