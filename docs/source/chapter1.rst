chapter 1: Instant Hacking: The Basics
=======================================


1.1 The Interactive Interpreter
---------------------------------

.

1.2 Algo....What?
-------------------

Algorithm is just a fancy word for a procedure or recipe—a detailed
description of how to do something


1.3 Numbers and Expressions
-----------------------------


.. code-block:: python


    >>> 10 // 3
    3
    >>> 10 % 3
    1
    >>> 9 // 3
    3
    >>> 9 % 3
    0
    >>> 2.75 % 0.5
    0.25
    >>> 10 % 3
    1
    >>> 10 % -3
    -2
    >>> -10 % 3
    2
    >>> -10 % -3
    -1
    >>> 10 // 3
    3
    >>> 10 // -3
    -4
    >>> -10 // 3
    -4
    >>> -10 // -3
    3
    >>> 2 ** 3
    8
    >>> -3 ** 2
    -9
    >>> (-3) ** 2
    9

    >>> 0xAF
    175
    >>> 010
    8
    >>> 0b1011010010
    722


1.4 Variables
-------------------

>>> x = 3
x를 변수라고 하고 x에 3을 할당한다고 한다.




1.5 Statements
-------------------
Statements
expression



1.6 Getting Input from the User
----------------------------------

사용자 입력을 요구할때 쓰인다.

.. code-block:: python


    >>> input("The meaning of life: ")
    The meaning of life: 42
    '42'


1.7 Functions
-------------------
exponentiation operator (**) to calculate powers
다음과 같이 쓰인다.

.. code-block:: python

    >>> 2 ** 3
    8
    >>> pow(2, 3)
    8

    >>> abs(-10)
    10
    >>> 2 // 3
    0
    >>> round(2 / 3)
    1.0



1.8 Modules
-------------------
math 모듈은 다양한 수식 계산 함수들이 있다.

.. code-block:: python

    >>> import math
    >>> math.floor(32.9)
    32
the opposite of floor is ceil

.. code-block:: python


    >>> math.ceil(32.3)
    33
    >>> math.ceil(32)
    32


모듈 함수는 불필요하게 다 로딩할 필요가 없다.
필요한 함수만 로딩해서 쓰는게 메모리 관리에 좋다.

.. code-block:: python

    >>> from math import sqrt
    >>> sqrt(9)
    3.0


The square root of a negative number is a so-called imaginary
number, and numbers that are the sum of a real and an imaginary part are called complex


.. code-block:: python

    >>> import cmath
    >>> cmath.sqrt(-1)
    1j

.. code-block:: python

    >>> (1 + 3j) * (9 + 4j)
    (-3 + 31j)



1.9 Saving and Executing Your Programs
------------------------------------------

프린트 함수를 써서 간단한 텍스트를 표현해 보자.

test.py 로 저장하고

.. code-block:: python

    print("test")
    print('test')

입력을 받아서 표현하는 코드를 짜보자

.. code-block:: python

    name = input("What is your name? ")
    print("Hello, " + name + "!")



1.10 Strings
-----------------


1.11 A Quick Summary
-----------------------

