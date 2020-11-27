---
title: Verification for Automated Production Systems
layout: default
---

# Verification for Automated Production Systems

VerifAPS is a software project that consists out of multiple subprojects for the
verification of automated production plants, i.e. programmable logic controller
software.

VerifAPS can be used as a library. For this several facades are exposed, for e.
g. parsing Structured Text, PLCOpenXML or symbolic execution. [More
Information](library/) 

Or you can use the exposed programs.


## Applications

-   [rvt-aps](rvt/) – Regression Verification
-   [geteta](geteta/) – Genteralized Test Tables for functional
    verification
-   [stvs](stvs/) – A graphical user interface for Generalized Test
    Tables.

## Getting Started

You can obtain the library via
[github](https://github.com/verifaps/verifaps-lib). Please follow the
instruction on the
[README.md](https://github.com/verifaps/verifaps-lib/README.md).

## Maven Repository

You can find old versions of VerifAPS here:

```xml
<repositories>
  ...
  <repository>
    <id>github</id>
    <name>GitHub VERIFAPS Maven Packages</name>
    <url>https://maven.pkg.github.com/verifaps/verifaps-lib</url>
  </repository>
</repositories>
```

Funded by [IMPROVE APS](https://formal.iti.kit.edu/improve-aps/)
