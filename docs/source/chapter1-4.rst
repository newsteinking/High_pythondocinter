chapter 4: Functions, the Building Blocks of Code
==================================================


4.1 Why use functions?
-------------------------



4.2 Scopes and name resolution
---------------------------------




4.3 Input parameters
----------------------




4.4 Return values
-------------------




4.5 A few useful tips
-----------------------



4.6 Recursive functions
--------------------------



4.7 Anonymous functions
---------------------------




4.8 Function attributes
-----------------------------

다음 코드를 출력해 보자

.. code-block:: python

    def multiplication(a, b=1):
    """Return a multiplied by b. """
    return a * b


    if __name__ == "__main__":

    special_attributes = [
        "__doc__", "__name__", "__qualname__", "__module__",
        "__defaults__", "__code__", "__globals__", "__dict__",
        "__closure__", "__annotations__", "__kwdefaults__",
    ]

    for attribute in special_attributes:
        print(attribute, '->', getattr(multiplication, attribute))

.




4.9 Built-in functions
---------------------------
파이썬은 다양한 내장 함수들이 있다.
내장함수를 다 거론하기는 힘들고 아래 정도가 많이 쓰이는 것들이다.

.. sourcecode:: bash

    $any, bin, bool, divmod, filter, float, getattr, id, int, len, list, min, print, set, tuple, type, and zip



4.10 One final example
-----------------------------
이 장을 끝내기 전에 다음 예제을 풀어보자.
일정 숫자 리스트에서 소수를 찾는 코드이다.

여기서 수학적 함수들은 파이썬 문서에서 찾아보면 된다.
https://docs.python.org/2/library/math.html

math.ceil(x)
Return the ceiling of x as a float, the smallest integer value greater than or equal to x.

math.sqrt(x)
Return the square root of x.

.. code-block:: python

    from math import sqrt, ceil


    def get_primes(n):
        """Calculate a list of primes up to n (included). """
        primelist = []
        for candidate in range(2, n + 1):
            is_prime = True
            root = int(ceil(sqrt(candidate)))  # division limit
            for prime in primelist:  # we try only the primes
                if prime > root:  # no need to check any further
                    break
                if candidate % prime == 0:
                    is_prime = False
                    break
            if is_prime:
                primelist.append(candidate)
        return primelist


    if __name__ == "__main__":

        def test():
            primes = get_primes(10**3)
            primes2 = [
                2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43,
                47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101, 103,
                107, 109, 113, 127, 131, 137, 139, 149, 151, 157, 163,
                167, 173, 179, 181, 191, 193, 197, 199, 211, 223, 227,
                229, 233, 239, 241, 251, 257, 263, 269, 271, 277, 281,
                283, 293, 307, 311, 313, 317, 331, 337, 347, 349, 353,
                359, 367, 373, 379, 383, 389, 397, 401, 409, 419, 421,
                431, 433, 439, 443, 449, 457, 461, 463, 467, 479, 487,
                491, 499, 503, 509, 521, 523, 541, 547, 557, 563, 569,
                571, 577, 587, 593, 599, 601, 607, 613, 617, 619, 631,
                641, 643, 647, 653, 659, 661, 673, 677, 683, 691, 701,
                709, 719, 727, 733, 739, 743, 751, 757, 761, 769, 773,
                787, 797, 809, 811, 821, 823, 827, 829, 839, 853, 857,
                859, 863, 877, 881, 883, 887, 907, 911, 919, 929, 937,
                941, 947, 953, 967, 971, 977, 983, 991, 997
            ]
            return primes == primes2

        print(test())

        print(get_primes(100))



소수 구하는 프로그램은 앞장에서도 다른 함수를 이용해서 배웠다.

.. code-block:: python

    primes = []  # this will contain the primes in the end
    upto = 100  # the limit, inclusive
    for n in range(2, upto + 1):
        is_prime = True  # flag, new at each iteration of outer for
        for divisor in range(2, n):
            if n % divisor == 0:
                is_prime = False
                break
        if is_prime:  # check on flag
            primes.append(n)

    print(primes)





4.11 Documenting your code
----------------------------
이 장에서는 코드에서 코멘트를 다는 연습을 하겠다.

기본적으로 파이썬 코멘트는 다음과 같이 쓰인다.

#  : 해당 기호 이후의 모든 코드를 코멘트 처리한다.
""" comment """  : 전,후 기호까지 코멘트 처리한다.

예제를 보자

.. code-block:: python

    def square(n):
        """Return the square of a number n. """
        return n ** 2

    def get_username(userid):
        """Return the username of a user given their id. """
        return db.get(user_id=userid).username


    def connect(host, port, user, password):
        """Connect to a database.

        Connect to a PostgreSQL database directly, using the given
        parameters.

        :param host: The host IP.
        :param port: The desired port.
        :param user: The connection username.
        :param password: The connection password.
        :return: The connection object.
        """
        # body of the function here...
        return connection





4.12 Importing objects
--------------------------

파이썬에서는 많은 함수들을 쓸수 있다.
이러한 함수를 쓰려면 다음의 방법들이 있다.

.. code-block:: python

    import module_name
    from module_name import function_name
    from mymodule import myfunc as better_named_func  ## 다른 함수 이름으로 변경
    from module_name import *    ## 모듈의 모든 함수를 import, 성능 문제 고민

예제에서 다음과 같은 lib와 함수 호출하는것을 생각해 보자

::

    ├── func_from.py
    ├── func_import.py
    ├── lib
    ├── funcdef.py
    └── __init__.py

파이썬에서는 패키지를 정의할때 __init__.py 파일을 집어 넣어야 한다.

코드는 다름과 같다.
fundef.py

.. code-block:: python

    def square(n):
        return n ** 2


    def cube(n):
        return n ** 3

func_import.py

.. code-block:: python

    import lib.funcdef


    print(lib.funcdef.square(10))
    print(lib.funcdef.cube(10))

func_from.py

.. code-block:: python

    from lib.funcdef import square, cube

    print(square(10))
    print(cube(10))




4.13 Ralative import
----------------------

Absolute Imports

  An absolute import specifies the resource to be imported using its full path from the project’s root folder.

다음과 같은 구조를 가지고 있다고 하자.
::

    └── project
        ├── package1
        │   ├── module1.py
        │   └── module2.py
        └── package2
            ├── __init__.py
            ├── module3.py
            ├── module4.py
            └── subpackage1
                └── module5.py

Absolute imports는 다음과 같이 호출한다.
.. code-block:: python

    from package1 import module1
    from package1.module2 import function1
    from package2 import class1
    from package2.subpackage1.module5 import function2


Relative Imports
  A relative import specifies the resource to be imported relative to the current location—that is, the location where the import statement is

예제를 보면 다음과 같다.

.. code-block:: python

    from .some_module import some_class
    from ..some_package import some_function
    from . import some_class


One clear advantage of relative imports is that they are quite succinct(간결하다)


4.14 Summary
-------------------

이장에서 함수에 대해서 배웠고 import 방법을 배웠다.
















