chapter 8: Exceptions
=======================
컴퓨터 프로그램을 하다보면 정상적인 경우와 예외적인 경우를 만나게 될것이다. 그러한 예외적인 경우 또는 자주 발생되지 않는 어떤것을
오류라고 한다.그러한 오류를 다루기 위해서 이벤트가 발생하는 조건을 만들 수 있다.어찌됐건 이런것은 비효율적이고 고정적이지 않을 뿐 아니라
프로그램을 비합리적으로 만든다.
당신은 이러한 이벤트를 무시할 수도 있다.그러나 파이썬은 exception-handling-mechanism을 제공한다.
이장에서는 excetion을 만들고 관리하는 방법과 다양한 방법으로 처리하는 법을 배우도록 하겠다.



8.1 What is Exception?
-------------------------
exception 환경을 표현하기 위하여 파이썬은 exception objects를 사용한다. 에러를 발생했을 경우, exception을 발생한다.
그러한 오류를 다루지 못한다면, 그러한 프로그램은 trace-back으로 종료한다.

.. code-block:: python

    >>> 1 / 0
    Traceback (most recent call last):
    File "<stdin>", line 1, in ?
    ZeroDivisionError: integer division or modulo by zero

그러한 에러 메세지들이 exception을 위해서 할수 있는것이 전부라면, 재미가 없을 것이다.
사실은 각각의 exception은 어떤 클래스( ZeroDivisionError)의 인스턴스라는 것이다. 이러한 인스턴스를은 생성되고 다양하게 표현된다.




8.2 Making Things Go Wrong....Your Way
-------------------------------------------
본것처럼,어떤것이 잘못되었을때 exception이 자동으로 표현되어진다. 이러한것들을 어떻게 처리할지를 보기전에 어떻게 하면 exception이
나오는지 한번 보자.

The raise Statement
~~~~~~~~~~~~~~~~~~~~
Exception을 만들기 위해서 raise 문을 쓰면 된다.


.. code-block:: python

    >>> raise Exception
    Traceback (most recent call last):
    File "<stdin>", line 1, in ?
    Exception
    >>> raise Exception('hyperdrive overload')
    Traceback (most recent call last):
    File "<stdin>", line 1, in ?
    Exception: hyperdrive overload

많은 build-in class들이 가능하다.

.. code-block:: python

    >>> raise ArithmeticError
    Traceback (most recent call last):
    File "<stdin>", line 1, in ?
    ArithmeticError


.. image:: ./img/chapter8-1.png

Custom Exception Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~
build-in exception이 많은 범위에서 그리고 많은 목적으로 지원할지라도,당신만의 exception을 만들 필요가 있다.
다음처험 exception 클래스의 하위 클래스로 추가해서 쓰면 된다.

.. code-block:: python

    class SomeCustomException(Exception): pass




8.3 Catching Exceptions
-------------------
이전에 얘기했듯이, exception에 관한 재미있는 것은 그것을 다룬다는 것이다.
다음 예를 보자 두 숫자를 입력해서 처리하는 것을 보자.

.. code-block:: python

    x = int(input('Enter the first number: '))
    y = int(input('Enter the second number: '))
    print(x / y)

    Enter the first number: 10
    Enter the second number: 0
    Traceback (most recent call last):
    File "exceptions.py", line 3, in ?
    print(x / y)
    ZeroDivisionError: integer division or modulo by zero

상기 프로그램을 Exception을 넣어 처리하면 다음과 같다.

.. code-block:: python

    try:
        x = int(input('Enter the first number: '))
        y = int(input('Enter the second number: '))
        print(x / y)
    except ZeroDivisionError:
        print("The second number can't be zero!")

Look, Ma, No Arguments!
~~~~~~~~~~~~~~~~~~~~~~~
다음 예를 보자.

.. code-block:: python

    class MuffledCalculator:
        muffled = False
        def calc(self, expr):
            try:
                return eval(expr)
            except ZeroDivisionError:
                if self.muffled:
                    print('Division by zero is illegal')
                else:
                    raise

    ma=MuffledCalculator()
    print(ma.calc('10/2'))


More Than One except Clause
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    Enter the first number: 10
    Enter the second number: "Hello, world!"
    Traceback (most recent call last):
    File "exceptions.py", line 4, in ?
    print(x / y)
    TypeError: unsupported operand type(s) for /: 'int' and 'str'

위 예에서처럼 숫자가 아닌 string을 넣었을 경우 에러 처리를 해야 한다.
다음처럼 오류처리를 추가하면 된다.

.. code-block:: python

    try:
        x=int(input('input your first number:'))
        y=int(input('input your second number:'))
        print(x/y)

    except ZeroDivisionError:
        print('The Second number cannot be zero')
    except TypeError:
        print('That was not number,was it?')

Catching Two Exceptions with One Block
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
다음처럼 한 블럭안에 한개 이상의 exception을 처리하고 싶으면 다음처럼 tuple로 처리 가능하다.

.. code-block:: python

    try:
        x = int(input('Enter the first number: '))
        y = int(input('Enter the second number: '))
        print(x / y)
    except (ZeroDivisionError, TypeError, NameError):
        print('Your numbers were bogus ...')

Catching the Object
~~~~~~~~~~~~~~~~~~~~~~
각각의 에러 메세지를 처리하는것을 보고 싶으면 다음처럼 하면 된다.
에러 메세지를 e로 받아서 처리하는 것이다.

.. code-block:: python

    try:
        x = int(input('Enter the first number: '))
        y = int(input('Enter the second number: '))
        print(x / y)
    except (ZeroDivisionError, TypeError, NameError) as e:
        print(e)


A Real Catchall
~~~~~~~~~~~~~~~~~
다음처럼 실제 메세지를 보고 싶을때 처리하면 좋다.

.. code-block:: python

    try:
        x = int(input('Enter the first number: '))
        y = int(input('Enter the second number: '))
        print(x / y)
    except Except as e:
        print(e)

When All Is Well
~~~~~~~~~~~~~~~~~~~
다음처럼 오류처리를 하고 다음에 else 처리로 가능하다.

.. code-block:: python

    try:
        print('A simple task')
    except:
        print('What? Something went wrong?')
    else:
        print('Ah ... It went as planned.')

이렇게 되면 이전에 배웠던 중복 exception을 다음처럼 처리할 수 있다.

.. code-block:: python

    while True:
        try:
            x = int(input('Enter the first number: '))
            y = int(input('Enter the second number: '))
            value = x / y
            print('x / y is', value)
        except:
            print('Invalid input. Please try again.')
        else:
            break

And Finally
~~~~~~~~~~~~~~
마지막으로 finally 구문을 소개하도록 하겠다.
try 구문과 같이 어떤 에러가 나는지 상관없이 처리를 종료할때 쓰인다.

.. code-block:: python

    x = None
    try:
        x = 1 / 0
    finally:
        print('Cleaning up ...')
        del x

다음 구문처럼 여러개를 혼용해서 써도 유용할때가 있다.

.. code-block:: python

    try:
        1 / 0
    except NameError:
        print("Unknown variable")
    else:
        print("That went well!")
    finally:
        print("Cleaning up.")


8.4 Exceptions and Functions
--------------------------------


8.5 The Zen of Exceptions
--------------------------------


8.6 Not All That Exceptional
--------------------------------



8.7 A Quick Summary
--------------------------------


