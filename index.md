---
title: Verification for Automated Production Systems
layout: default
---

# Verification for Automated Production Systems

VerifAPS is library and a set of programs for the formal verification of
software for automated production systems (programmable logic controller, PLC).

VerifAPS can be used as a [library](library/). For this several facades are
exposed, for e.g. parsing Structured Text, PLCOpenXML or symbolic execution , or
by the several exposed programs.


## Applications

- [rvt-aps](/rvt/) – Regression Verification
- [geteta](/geteta/) – Genteralized Test Tables for functional verification
- [Editor](/ide/) - A simple editor with support of IEC61131 and test tables
- [stvs](/stvs/) – A graphical user interface for Generalized Test Tables.

## Demonstrations

- [Final Event of SPP1953](demofinal/)


## Getting Started

VerifAPS is available on [github](https://github.com/verifaps/verifaps-lib). You
can compile your own executables with:

```
$ git clone https://github.com/verifaps/verifaps-lib
$ ./gradlew :exec:installDist
```

For compiliation, the only requirement is a recent version of Java. The rest is
bootstrapped. For development IntelliJ IDEA is recommended. For the latest
development version you should checkout the `develop` branch.

You find the executables after a successfully assembly under
`<project-path>/exec/build/install/exec/bin/`. The generated BAT files have
problems on Windows due to long arguments, please use the exe files.


## Maven Repository

You can find versions of VerifAPS here:

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


## Publications

- [Alexander Weigl, Mattias Ulbrich, Suhyun Cha, Bernhard Beckert, Birgit
  Vogel-Heuser: Relational Test Tables: A Practical Specification Language for
  Evolution and Security. FormaliSE@ICSE 2020: 77-86](https://doi.org/10.1145/3372020.3391566)
- [Alexander Weigl, Mattias Ulbrich, Daniel Lentzsch: Modular Regression
  Verification for Reactive Systems. ISoLA (2) 2020: 25-43](https://doi.org/10.1007/978-3-030-61470-6_3)
- [Suhyun Cha, Mattias Ulbrich, Alexander Weigl, Bernhard Beckert, Kathrin Land,
Birgit Vogel-Heuser: On the Preservation of the Trust by Regression Verification
of PLC software for Cyber-Physical Systems of Systems. INDIN 2019: 413-418](https://doi.org/10.1109/INDIN41052.2019.8972210)
- [Bernhard Beckert, Jakob Mund, Mattias Ulbrich, Alexander Weigl: Formal
  Verification of Evolutionary Changes. Managed Software Evolution 2019: 309-332](https://doi.org/10.1007/978-3-030-13499-0_11)
- [Suhyun Cha, Alexander Weigl, Mattias Ulbrich, Bernhard Beckert, Birgit
  Vogel-Heuser: Applicability of generalized test tables: a case study using the
  manufacturing system demonstrator xPPU. Autom. 66(10): 834-848 (2018)](https://doi.org/10.1515/auto-2018-0028)
- [Suhyun Cha, Alexander Weigl, Mattias Ulbrich, Bernhard Beckert, Birgit
Vogel-Heuser: Achieving delta description of the control software for an
automated production system evolution. CASE 2018: 1170-1176](https://doi.org/10.1109/COASE.2018.8560588)
- [Bernhard Beckert, Suhyun Cha, Mattias Ulbrich, Birgit Vogel-Heuser, Alexander
Weigl: Generalised Test Tables: A Practical Specification Language for Reactive
Systems. IFM 2017: 129-144](https://doi.org/10.1007/978-3-319-66845-1_9)
- [Suhyun Cha, Sebastian Ulewicz, Birgit Vogel-Heuser, Alexander Weigl, Mattias
Ulbrich, Bernhard Beckert: Generation of monitoring functions in production
automation using test specifications. INDIN 2017: 339-344](https://doi.org/10.1109/INDIN.2017.8104795)
- [Alexander Weigl, Franziska Wiebe, Mattias Ulbrich, Sebastian Ulewicz, Suhyun
Cha, Michael Kirsten, Bernhard Beckert, Birgit Vogel-Heuser: Generalized test
tables: A powerful and intuitive specification language for reactive systems.
INDIN 2017: 875-882](https://doi.org/10.1109/INDIN.2017.8104887)
- [Sebastian Ulewicz, Birgit Vogel-Heuser, Mattias Ulbrich, Alexander Weigl,
Bernhard Beckert: Proving equivalence between control software variants for
Programmable Logic Controllers. ETFA 2015: 1-5](https://doi.org/10.1109/ETFA.2015.7301603)
- [Bernhard Beckert, Mattias Ulbrich, Birgit Vogel-Heuser, Alexander Weigl:
Regression Verification for Programmable Logic Controller Software. ICFEM 2015:
234-251](https://doi.org/10.1007/978-3-319-25423-4_15)


Funded by [IMPROVE APS](https://formal.iti.kit.edu/improve-aps/)
