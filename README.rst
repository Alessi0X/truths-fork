truths - auto generate truth tables
===================================

truths is a simple tool that allows you to quickly generate truth tables
from Python variable names and logical expressions.

Installation
------------

.. code:: bash

    pip install truths

Or clone and install for development:

.. code:: bash

    git clone <repository-url>
    cd truths
    pip install -e .

Basic Usage
-----------

Simple Truth Table
~~~~~~~~~~~~~~~~~~

Start by creating a truth table with base variables:

.. code:: python

    from truths import Truths
    print(Truths(['A', 'B', 'C']))

::

    +---+---+---+
    | A | B | C |
    +---+---+---+
    | 0 | 0 | 0 |
    | 0 | 0 | 1 |
    | 0 | 1 | 0 |
    | 0 | 1 | 1 |
    | 1 | 0 | 0 |
    | 1 | 0 | 1 |
    | 1 | 1 | 0 |
    | 1 | 1 | 1 |
    +---+---+---+

Truth Table with Logical Expressions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Add logical expressions as phrases:

.. code:: python

    from truths import Truths
    print(Truths(['A', 'B'], ['A and B', 'A or B', 'not A']))

::

    +---+---+---------+--------+-------+
    | A | B | A and B | A or B | not A |
    +---+---+---------+--------+-------+
    | 0 | 0 |    0    |   0    |   1   |
    | 0 | 1 |    0    |   1    |   1   |
    | 1 | 0 |    0    |   1    |   0   |
    | 1 | 1 |    1    |   1    |   0   |
    +---+---+---------+--------+-------+

Supported Operators
-------------------

truths supports all standard logical operators in a **case-insensitive**
manner:

-  **AND** - Logical conjunction (e.g., ``A AND B``, ``A and B``)
-  **OR** - Logical disjunction (e.g., ``A OR B``, ``A or B``)
-  **NOT** - Logical negation (e.g., ``NOT A``, ``not A``)
-  **XOR** - Exclusive OR (e.g., ``A XOR B``, ``A xor B``)
-  **NAND** - NOT AND (e.g., ``A NAND B``, ``A nand B``)
-  **NOR** - NOT OR (e.g., ``A NOR B``, ``A nor B``)

Examples with Different Operators
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: python

    from truths import Truths

    # XOR example
    print(Truths(['A', 'B'], ['A XOR B']))

    # NAND example
    print(Truths(['A', 'B'], ['A NAND B']))

    # NOR example
    print(Truths(['A', 'B'], ['A NOR B']))

    # Mixed case operators
    print(Truths(['A', 'B'], ['A And B', 'a OR b', 'Not A']))

Configuration Options
---------------------

Boolean Display Format
~~~~~~~~~~~~~~~~~~~~~~

By default, truth values are displayed as integers (0 and 1). Use
``ints=False`` to display as True/False:

.. code:: python

    from truths import Truths
    print(Truths(['A', 'B'], ['A and B'], ints=False))

::

    +-------+-------+-----------+
    |   A   |   B   | A and B   |
    +-------+-------+-----------+
    | False | False |   False   |
    | False |  True |   False   |
    |  True | False |   False   |
    |  True |  True |   True    |
    +-------+-------+-----------+

CSV Export
~~~~~~~~~~

Save truth tables to a CSV file by setting ``save=True``:

.. code:: python

    from truths import Truths

    # This will create 'truth_table.csv' when the table is printed
    table = Truths(['A', 'B'], ['A and B', 'A or B'], save=True)
    print(table)

The CSV file will contain the same data as the printed table with proper
headers.

Advanced Examples
-----------------

Complex Expressions
~~~~~~~~~~~~~~~~~~~

.. code:: python

    from truths import Truths
    print(Truths(
        ['p', 'q', 'r'],
        ['(p and q) or r', 'p and (q or r)', 'not (p and q)']
    ))

Using All Parameters
~~~~~~~~~~~~~~~~~~~~

.. code:: python

    from truths import Truths

    # Create a truth table with:
    # - Base variables: A, B, C
    # - Logical expressions
    # - Display as True/False
    # - Save to CSV
    table = Truths(
        base=['A', 'B', 'C'],
        phrases=['A and B', 'A NAND B', 'A XOR B', '(A or B) and C'],
        ints=False,
        save=True
    )
    print(table)

How It Works
------------

Behind the scenes, truths:

1. Generates all possible combinations of truth values for base variables
2. Normalizes logical operators to be case-insensitive
3. Evaluates each expression in the context of each combination
4. Formats the results into a readable table using PrettyTable
5. Optionally exports to CSV format

Requirements
------------

-  Python 3.x
-  prettytable

License
-------

Apache License 2.0

Acknowledgments
---------------

This is a fork of the original `truths <https://github.com/tr3buchet/truths>`_
library by `Trey Morris <https://github.com/tr3buchet>`_. The original library
provided the foundational truth table generation functionality. This fork adds:

-  Case-insensitive operator support (AND, OR, NOT, XOR, NAND, NOR)
-  CSV export functionality
-  Additional logical operators (XOR, NAND, NOR)
-  Enhanced documentation and examples

Thank you to Trey Morris for creating the original ``truths`` library!
