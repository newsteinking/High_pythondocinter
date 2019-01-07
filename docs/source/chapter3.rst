chapter 3: Working with Strings
====================================


3.1 Basic String Operations
------------------------------
모든 표준 sequence 연산자는(indexing, slicing, multiplication, membership, length, minimum,
and maximum) String과 함께 쓰인다.
string은 변경할 수 없다.따라서 item에 대한 모는것과 slic 할당은 쓸 수 없다.

.. code-block:: python

    >>> website = 'http://www.python.org'
    >>> website[-3:] = 'com'
    Traceback (most recent call last):
    File "<pyshell#19>", line 1, in ?
    website[-3:] = 'com'
    TypeError: object doesn't support slice assignment


3.2 String Formatting: The Short Version
-----------------------------------------
여기서는 string format에 대한 간략한 버젼을 보도록 하자. 상세한 것은 String Formatting 버젼을 찾아 보도록 하자.
string으로서 값을 표현하는것은 중요한 부분이다.

다음 예를 보도록 하자.

.. code-block:: python

    >>> format = "Hello, %s. %s enough for ya?"
    >>> values = ('world', 'Hot')
    >>> format % values
    'Hello, world. Hot enough for ya?

%s 연산자는 변환 특별자로 불리는 format string의 일부분이다.
그것은 값이 넣어지는 곳에  표시된다.
s의 의미는 string으로 형태를 하도록 되어져야만 한다.그렇지 않으면 그것은 str으로 변환될것이다.
%.3f의 경우는 3자릿수 float 숫자값으로 표현된다.
또다른 솔루션은 다음처럼 template을 사용하는것이다.

.. code-block:: python

    >>> from string import Template
    >>> tmpl = Template("Hello, $who! $what enough for ya?")
    >>> tmpl.substitute(who="Mars", what="Dusty")
    'Hello, Mars! Dusty enough for ya?'

다음처럼 format을 이용하여 표현할 수 있다.

.. code-block:: python

    >>> "{}, {} and {}".format("first", "second", "third")
    'first, second and third'
    >>> "{0}, {1} and {2}".format("first", "second", "third")
    'first, second and third'

    >>> "{3} {0} {2} {1} {3} {0}".format("be", "not", "or", "to")
    'to be or not to be'

다음처럼 표현될 수 있다.

.. code-block:: python


    >>> from math import pi
    >>> "{name} is approximately {value:.2f}.".format(value=pi, name="π")
    'π is approximately 3.14.'

만약 값이 특정되지 않으면 다음처럼 표현된다.

.. code-block:: python

    >>> "{name} is approximately {value}.".format(value=pi, name="π")
    'π is approximately 3.141592653589793.'

python 3.6에서는 대체되는 필드에 상응하는 동일한 이름을 가진 변수를 가질때 쓸 수 있는 숏컷이 있다.
그러한 경우 f로 시작하는 so-called-string이라고 한다.

.. code-block:: python

    >>> from math import e
    >>> f"Euler's constant is roughly {e}."
    "Euler's constant is roughly 2.718281828459045."



3.3 String Formatting: The Long Version
-----------------------------------------




3.4 String Methods
-------------------




3.5 A Quick Summary
------------------------


