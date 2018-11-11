chapter 4: Functions, the Building Blocks of Code
=======================


4.1 Why use functions?
-------------------

4.1.1 Linux
~~~~~~~~~~~~~~~~


.. image:: ./img/chapter0_2.png


.. sourcecode:: bash

    $ pip install recommonmark

Then in your ``conf.py``:

.. code-block:: python

    test




 .. code-block:: html


    <div data-date="12/03/2012"></div>




4.2 Scopes and name resolution
-------------------




4.3 Input parameters
-------------------




4.4 Return values
-------------------




4.5 A few useful tips
-------------------



4.6 Recursive functions
-------------------



4.7 Anonymous functions
-------------------




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
.


4.10 One final example
-------------------
이 장을 끝내기 전에 다음 예제을 풀어보자.
일정 숫자 리스트에서 소수를 찾는 코드이다.

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
.




4.11 Documenting your code
-------------------




4.12 Importing objects
-------------------




4.13 Summary
-------------------















