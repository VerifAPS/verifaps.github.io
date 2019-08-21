geteta — Generalized Test Tables |Codacy Badge| |CircleCI|
==========================================================

Generalized Test Tables ensures safety in automation software.

.. figure:: ../geteta-logo.svg


- Authors:

   - Alexander Weigl weigl@kit.edu

- License: GPL v3

Getting Started
---------------


Download
--------

These are jar files include all dependencies:

-  0.5.0-SNAPSHOT: **not released**

   -  new automata model
   -  different verification techniques (IC3, BMC, LTL)
   -  **latest useable version for `stvs <../stvs/index.md>`__**

-  0.4.4: `geteta-0.4.4-exe.jar <downloads/geteta-0.4.4-exe.jar>`__

   -  Fix a bug in the clocks.

      .. raw:: html

         </li>

-  0.4.3: `geteta-0.4.3-exe.jar <downloads/geteta-0.4.3-exe.jar>`__

   -  Change clock initial value to 1 as off-by-one error

-  0.4.2: `geteta-0.4.2-exe.jar <downloads/geteta-0.4.2-exe.jar>`__

   -  Kills nuXmv, if geteta is killed
   -  depends on new version of ``iec61131lang``

-  0.4.1: `geteta-0.4.1-exe.jar <downloads/geteta-0.4.1-exe.jar>`__

   -  bug fixes: missing constraint on free variables are treated as
      don’t cares

      .. raw:: html

         </li>

-  If a free variable is an enum, every allowed enum literal is allowed
   (super-enum to rule them all).

   .. raw:: html

      </li>

   -  0.4.0: `geteta-0.4.0-exe.jar <downloads/geteta-0.4.0-exe.jar>`__

-  Counter examples in the semantic of traces in the test table

   -  0.3.0: `geteta-0.3.0-exe.jar <downloads/geteta-0.3.0-exe.jar>`__

-  enum support tested and fixed

   -  0.2.2-beta:
      `geteta-0.2.2-beta.jar <downloads/geteta-0.2.2-beta.jar>`__

-  better nuxmv output parser

   -  0.2.1-beta:
      `geteta-0.2.1-beta.jar <downloads/geteta-0.2.1-beta.jar>`__

-  Internal changes

   -  0.2.0: `geteta-0.2.0.jar <downloads/geteta-0.2.0.jar>`__

From Source
~~~~~~~~~~~

::

    $ git clone https://github.com/VerifAPS/geteta.git
    $ mvn package

.. _getting-started-1:

Getting started
---------------

Ensure, that you have installed `nuXmv <http://nuxmv.fbk.eu>`__. You
need to set the ``NUXMV`` environment variable to the nuXmv executable.

::

    export NUXMV=/home/weigl/work/nuXmv-1.1.1-Linux/bin/nuXmv

After this, you can call geteta with:

::

    java -jar geteta-${project.version}.jar -c program.st -t testtable.xml [-x]

Command Line Arguments
----------------------

-  ``-x`` geteta writes the output in an XML format.
-  ``-m <mode>``
-  ``-t <table.xml>``
-  ``-c <code.st>``
-  ``-v (IC3|INVAR|LTL|BMC)``

XML-Format of Generalized Test tables
=====================================

What is a test table?
---------------------

A test table describe a behaviour of a reactive system by ensuring
allowed input and output values for specific time frames.

Semantics
---------

A system is conform to a test table if and only if the system response
with the corresponding (after the test table) output sequence given a
valid sequence of input values.

Input format
------------

The test tables are serialized into XML, following the scheme of
```exteta-1.0.xsd`` <>`__. The XML contains three parts under the root
entry.

``<variables>``
~~~~~~~~~~~~~~~

These tag contains the two types of variables: i/o and constraint.

``<variable>``
^^^^^^^^^^^^^^

**Attributes:**

+-------------------+--------------------------------------------------+
| Name              | Description                                      |
+===================+==================================================+
| identifier        | variable identifier                              |
+-------------------+--------------------------------------------------+
| io                | ``input`` or ``output``                          |
+-------------------+--------------------------------------------------+
| data-type         | IEC61131-3 builtin datatype. Currently           |
|                   | supported: AnyInt and AnyBit                     |
+-------------------+--------------------------------------------------+

-  I/O variables talk about the the input and output variables of the
   given program.

``<constraint>``
^^^^^^^^^^^^^^^^

Constraint variables (*specification variable*) are not visible to the
program.

**Attributes:**

+-------------------+--------------------------------------------------+
| Name              | Description                                      |
+===================+==================================================+
| identifier        | variable identifier                              |
+-------------------+--------------------------------------------------+
| constraint        | a valid cell expression                          |
+-------------------+--------------------------------------------------+
| data-type         | IEC61131-3 builtin datatype. Currently           |
|                   | supported: AnyInt and AnyBit                     |
+-------------------+--------------------------------------------------+

``<steps>``
~~~~~~~~~~~

``<region>`` and ``<step>``
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The ``<steps>`` tag contains the row (``<step>``) of the test tables.
Each row the value of the cells (cell expressions) in the order of the
defined i/o variables.

You repeat a bunch of steps, by wrapping them into a region block.

A region and step tag has the ``duration`` attribute, which defines how
often the step is applied. The ``duration`` is an interval ``[m,n]``
with constant values for ``m,n``.

Cell Expression (``<cell>``)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Formally, a cell expression is generated by the `grammar <>`__.
Informally, a cell expression is a boolean expression over the following
operators

-  arithmetic ``+, -, *, /``
-  logical ``and, or, xor``.

The syntax and semantic, e.g. the operator precedence is tight on the
definition of Structured Text and SMV (nuXmv). For example, ``OR`` and
``|`` is allowed for logical or.

Additionally, we introduce abbreviations.

-  Constants

A simple constant means the equivalence with this value.

``5`` means ``X = 5`` and ``FALSE`` is ``NOT X``.

-  Single-sided comparison

A construct with a relational operator, ``<,<=,<>,=, >=, >``, compares
the column variable ``X`` with the given expression.

Example: ``<1`` means ``X<1`` resp. ``>=a+2`` expands to ``X>=a+2``.

-  Interval

You can specify an interval ``[m,n]`` to enforce a lower and upper bound
for ``X``: ``m<=X & X>=n``.

Example: ``[x+2, x+4]`` means ``(x+2) <= X <= (x+4)``.

-  Don’t-Care

If you don’t want to force a value, you can use “don’t-care” ``-``.

Operators with Precedence
^^^^^^^^^^^^^^^^^^^^^^^^^

0. constants and variable names
1. parens ``()`` and unary operators ``! NOT -``
2. point operators ``MOD % / *``
3. Substraction and Addition ``+ -``
4. Comparision ``< <= >= >``
5. equality
6. antivalence
7. logical and ``& AND``
8. logical or ``| OR``
9. logical xor ``xor XOR``

``<options>``
^^^^^^^^^^^^^

Options are key-value pairs of the kind ``<option key="" value=""/>``.
They give additional information for the processing of the given table.

Currently allowed options:

Program mode
''''''''''''

-  Key: ``mode``
-  Values: ``CONFORMANCE`` or ``CONCRETE_TABLE`` or
   ``INPUT_SEQUENCE_EXISTS`` \| Controls

The mode of test tables has following effect:

-  ``CONFORMANCE`` - **default** Checks the system conformity against
   the test table. Returns a counter example, iff the system is not
   compilant against the above semantic.
-  ``CONCRETE_TABLE`` Returns a counter example, that represents a
   concrete run through the test table.
-  ``INPUT_SEQUENCE_EXISTS`` The above semantics has one problem, if no
   possible *input sequence extension* exists. This mode checks if there
   exists always an input extension.

Cycles through the steps
''''''''''''''''''''''''

In dependence of ``mode = CONCRETE_TABLE`` you can give the wanted cycle
count for each step.

-  Keys: ``cycles.<id>``
-  Value: ``int``

where ``<id>`` is the number of the region/step (starting with zero, in
order of appearance).

Data types
''''''''''

You can select the bit width of the ST data types. **currently not
implemented**

``<functions>``
^^^^^^^^^^^^^^^

Between this tag you can define arbitrary function as Structured Text code.
These function are usable within the cell expressions as regular function calls.

.. |Codacy Badge| image:: https://api.codacy.com/project/badge/Grade/655e1ba61c2040eb8bccdb8f8a3799d1
   :target: https://www.codacy.com/app/wadoon/geteta?utm_source=github.com&utm_medium=referral&utm_content=VerifAPS/geteta&utm_campaign=badger
.. |CircleCI| image:: https://circleci.com/gh/VerifAPS/geteta.svg?style=svg
   :target: https://circleci.com/gh/VerifAPS/geteta
