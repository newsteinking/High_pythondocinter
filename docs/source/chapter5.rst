chapter 5: Conditionals,Loops, and Some Other Statements
============================================================
지금까지는 좀 더 힘든 부분을 다루었다. 모든 데이터 타입은 멋쟁이이다. 그것으로 충분할까요?
약간 페이스를 올려봅시다. conditionals 과 loop를 살펴보기전에 잠깐 기본 용법에 대하 알아 봅시다.


5.1 More About print and import
----------------------------------------
여기서는 print문과 import의 다른 특성들을 알아보도록 하자.

Printing Multiple Arguments
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
print는 어떤 string 또는 어떤 하나로 변환된 표현을 나타낼때 쓰인다.
print는 ,로 구분을 하면  한개이상 표현을 할 수 있다.

.. code-block:: python

    >>> print('Age:', 42)

보다시피 스페이스 문자가 각 전달자 사이에 들어간다.이것은 유용할때가 있는데 text와 변수값을 string format을 쓰지 않고 쓸 수 있다.


.. code-block:: python


    >>> name = 'Gumby'
    >>> salutation = 'Mr.'
    >>> greeting = 'Hello,'
    >>> print(greeting, salutation, name)
    Hello, Mr. Gumby

첫번째처럼 쓰이게 되면 스페이스값이 들어가기 때문에 두번째처럼 써야 된다.

.. code-block:: python

    >>> name = 'Gumby'
    >>> salutation = 'Mr.'
    >>> greeting = 'Hello'
    print(greeting, ',', salutation, name)
    >>>Hello , Mr gumby
    print(greeting + ',', salutation, name)
    >>>Hello, Mr gumby

또한 특정 구분자를 넣어도 된다.

.. code-block:: python

    >>> print("I", "wish", "to", "register", "a", "complaint", sep="_")
    I_wish_to_register_a_complaint

다음처럼 특정 end string을 넣어도 된다.


.. code-block:: python

    print('Hello,', end='')
    print('world!')

Importing Something as Something Else
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
보통 다음처럼 import를 사용한다.

.. code-block:: python

    import somemodule
    or use
    from somemodule import somefunction
    or
    from somemodule import somefunction, anotherfunction, yetanotherfunction
    or
    from somemodule import *

네번째의 경우는 주어진 모듈의 모든것을 쓰고자할때만 쓰여져야 한다.
만약 2개 모듈을 중에 동일한 함수가 있을 경우에는 다음처럼 사용해야 한다.

.. code-block:: python

    module1.open(...)
    module2.open(...)

다음처럼 모듈 전체를 as로 처리해서 쓰일수도 있다.

.. code-block:: python

    >>> import math as foobar
    >>> foobar.sqrt(4)
    2.0

또는

.. code-block:: python

    >>> from math import sqrt as foobar
    >>> foobar(4)
    2.0
open 함수에 대해서 다음처럼 사용할 수 있다.

.. code-block:: python


    from module1 import open as open1
    from module2 import open as open2



5.2 Assignment Magic
-----------------------

Sequence Unpacking
~~~~~~~~~~~~~~~~~~~~
다음처럼 할당할 수 있다.

.. code-block:: python


    x,y,z=1,2,3
    print(x,y,z)

변수 위치를 바꿀때도 유용하다.

.. code-block:: python

    x,y=y,x
    print(x,y,z)

여기서는 sequence unpacking을 알아보도록 하자.

.. code-block:: python

    >>> values = 1, 2, 3
    >>> values
    (1, 2, 3)
    >>> x, y, z = values
    >>> x
    1
이것은 함수나 메쏘드가 tuple로 리턴할때 유용하다.
dictionary로부터 임의의 key-value를 가져오는것을 생각해 보자.당신은 tuple로 리턴하는 popitem을 사용할 것이다.
그리고 tuple을 풀어서 각각의 변수값으로 리턴할 수 있다.

.. code-block:: python

    >>> scoundrel = {'name': 'Robin', 'girlfriend': 'Marion'}
    >>> key, value = scoundrel.popitem()
    >>> key
    'girlfriend'
    >>> value
    'Marion'

다음처럼 풀고자 하는 sequence는 동일한 item 수를 가져야 한다.
다음처럼 서로 틀리면 오류를 표시한다.

.. code-block:: python

    >>> x, y, z = 1, 2
    Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
    ValueError: need more than 2 values to unpack
    >>> x, y, z = 1, 2, 3, 4
    Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
    ValueError: too many values to unpack

다음처럼 * 사용하여 나머지를 처리할 수도 있다.

.. code-block:: python

    >>> a, b, *rest = [1, 2, 3, 4]
    >>> rest
    [3, 4]

    >>> name = "Albus Percival Wulfric Brian Dumbledore"
    >>> first, *middle, last = name.split()
    >>> middle
    ['Percival', 'Wulfric', 'Brian']

Chained Assignments
~~~~~~~~~~~~~~~~~~~~~
여러개 변수를 하나로 묶을때 체인할당이 사용된다.
이전장에서 동시할당과 비슷하다. 예외적으로 하나의 값만 취급한다는것은 차이점이다.

.. code-block:: python

    x = y = somefunction()

    y = somefunction()
    x = y

첫번째것은 두번째것과 동일하다.

Augmented Assignments
~~~~~~~~~~~~~~~~~~~~~~
모든 연산처리시 다음과 같이 축약해서 할 수 있다.

.. code-block:: python

    >>> x = 2
    >>> x += 1
    >>> x *= 2
    >>> x
    6

data type 처리도 가능하다.

.. code-block:: python

    >>> fnord = 'foo'
    >>> fnord += 'bar'
    >>> fnord *= 2
    >>> fnord
    'foobarfoobar'

증분 할당자는 코드를 좀더 간략하게 간소하게 정리할 수 있다.그리고 가독성도 있다.



5.3 Blocks:The Joy of Indentation
---------------------------------------
블락은 구문의 일종은 아니다.다음 두장을 공부할때 필요한 부분이다.
블락은 조건이 참값일경우에 또는 여러번 사용할 수 있는 구문의 집합이다



5.4 Conditions and Conditional Statements
--------------------------------------------




5.5 Loops
-------------------



5.6 Comprehesions- Slightly Loopy
----------------------------------------



5.7 And Three for the Road
-------------------------------




5.8 A Quick Summary
----------------------

