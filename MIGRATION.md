Apache Camel 3 Migration Guide
==============================

This document is intended for helping you migrate your Apache Camel applications
from version 2.x to 3.0.

Before you start
----------------

// TODO when we drop Java8
// TODO Apache Camel 3 requires Java 11. Java 8 are no longer supported.

Modularization of camel-core
----------------------------

One of the biggest change is the modularization of camel-core.
In Camel 2.x camel-core was one JAR file, which now has been splitup into many JARs as follows:

TODO: as table of all the modules
- camel-core
- camel-api
 
Maven users of Apache Camel can keep using the dependency *camel-core* which will have transitive dependency on all of its modules, and therefore no migration is needed.
However users whom wants to trim the size of the classes on the classpath, can use fine grained Maven dependency on only the modules needed.

TODO: we need camel-core-minimal dependency for just basic Camel


Migrating custom components
---------------------------

You should depend on `camel-support` and not `camel-core` directly.

The classes from `org.apache.camel.impl` that was intended to support Camel developers building custom components has been moved out of `camel-core` into `camel-support` into the `org.apache.camel.support` package. For example classes such as `DefaultComponent`, `DefaultEndpoint` etc has been moved and migration is nessasary.

// TODO: Should we create a camel2-support JAR with an adapter to bridge between 2.x and 3.0

Deprecated APIs and Components
------------------------------

All deprecated APIs and components from Camel 2.x has been removed in Camel 3.

Migration Camel applications
----------------------------

The following API changes may affect your existing Camel applications, which needs to be migrated.

### Moved APIs

TODO: Should this be a table?
TODO: Add the other moved classes/packages etc

The classes from `org.apache.camel.impl` that was intended to support Camel developers building custom components has been moved out of `camel-core` into `camel-support` into the `org.apache.camel.support` package. If you have built custom Camel components that may have used some of these APIs you would then need to migrate.

All the classes in `org.apache.camel.util.component` has been moved from the camel-core JAR to the package `org.apache.camel.support.component` in the `camel-support` JAR.

The class `ServiceHelper` has been moved from `org.apache.camel.util.ServiceHelper` in the camel-core JAR to `org.apache.camel.support.service.ServiceHelper` and moved to the `camel-api` JAR.

The class `FileIdempotentRepository` has been moved from `org.apache.camel.processor.idempotent.FileIdempotentRepository` in the camel-core JAR to `org.apache.camel.support.processor.idempotent.FileIdempotentRepository` and moved to the `camel-suppor` JAR.

The class `MemoryIdempotentRepository` has been moved from `org.apache.camel.processor.idempotent.MemoryIdempotentRepository` in the camel-core JAR to `org.apache.camel.support.processor.idempotent.MemoryIdempotentRepository` and moved to the `camel-suppor` JAR.

The class `XsltAggregationStrategy` has been moved from `org.apache.camel.builder.XsltAggregationStrategy` in the camel-core JAR to `org.apache.camel.component.xslt.XsltAggregationStrategy` and moved to the `camel-xslt` JAR.

The method `xslt` has been removed from `org.apache.camel.builder.AggregationStrategies`. Instead use the `XsltAggregationStrategy` from `camel-xslt` JAR directly.

The getter/setter for `bindingMode` on `RestEndpoint` has been changed to use type `org.apache.camel.spi.RestConfiguration.RestBindingMode` from `camel-api` JAR. Instead of using this type class you can also call the setter method with string type instead.

