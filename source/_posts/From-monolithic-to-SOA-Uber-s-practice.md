---
title: From monolithic to SOA - Uber's practice
date: 2016-12-24 21:05:13
description: Why and how Uber change its architecture from monolithic mode to SOA
tags: 
- SOA
- Architecture
- Uber

category: Architecture
---
### Why
As core domain models grew and new features were introduced, our components became tightly coupled, and enforcing encapsulation made separation of concerns difficult. Continuous integration turned into a liability because deploying the codebase meant deploying everything at once.

### New Challenges
  - Obviousness
Too many services would bring complexities on how to find and use them.
  - Distributed API Safety
Dealing with unexpected argument, schema, calling...
  - Resilience
How to deal with fault tolerance and latency?

### Solution
- **Thrift**
Thrift use strict contract binding to resolve 'Safety' concern.

- **Hystrix** 
Hystrix is a latency and fault tolerance library designed to isolate points of access to remote systems, services and 3rd party libraries, stop cascading failure and enable resilience in complex distributed systems where failure is inevitable.
http://hot66hot.iteye.com/blog/2155036
https://segmentfault.com/a/1190000005988895

- **Finagle**
Finagle is an extensible RPC system for the JVM, used to construct high-concurrency servers. Finagle implements uniform client and server APIs for several protocols, and is designed for high performance and concurrency.
Core value: type Service[Req, Rep] = Req => Future[Rep]

### Reference
[Uber's article](https://eng.uber.com/soa/)
[Hystrix](https://github.com/Netflix/Hystrix)
[Finagle](https://twitter.github.io/finagle/)