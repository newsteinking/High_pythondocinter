chapter 5: Saving Time and Memory
==================================

이 장에서는 절대적인 성능과 최적화에 대한 한계에 맞춰서 코딩하는법을 배우도록 하자.



5.1 map, zip, and filter
----------------------------

빌드인 함수로 map,zip,filter를 많이 사용하는데 성능측면에서 고려를 해보자.

Map
~~~~~~~~~~~~~~~~
Map 함수는 파이썬 문서에서 다음과 같이 설명되어 있다

.. code-block::Python

    map(function, iterable, ...) returns an iterator that applies function
    to every item of iterable, yielding the results. If additional iterable arguments are
    passed, function must take that many arguments and is applied to the items from
    all iterables in parallel. With multiple iterables, the iterator stops when the shortest
    iterable is exhausted
.
다음 예제를 보자.

.. code-block::Python

    >>> map(lambda *a: a, range(3))  # without wrapping in list...
    <map object at 0x7f563513b518>  # we get the iterator object
    >>> list(map(lambda *a: a, range(3)))  # wrapping in list...
    [(0,), (1,), (2,)]  # we get a list with its elements
    >>> list(map(lambda *a: a, range(3), 'abc'))  # 2 iterables
    [(0, 'a'), (1, 'b'), (2, 'c')]
    >>> list(map(lambda *a: a, range(3), 'abc', range(4, 7)))  # 3
    [(0, 'a', 4), (1, 'b', 5), (2, 'c', 6)]
    >>> # map stops at the shortest iterator
    >>> list(map(lambda *a: a, (), 'abc'))  # empty tuple is shortest
    []
    >>> list(map(lambda *a: a, (1, 2), 'abc'))  # (1, 2) shortest
    [(1, 'a'), (2, 'b')]
    >>> list(map(lambda *a: a, (1, 2, 3, 4), 'abc'))  # 'abc' shortest
    [(1, 'a'), (2, 'b'), (3, 'c')]

.

위 예제에서 range(3)을 이용하여 lamda 함수를 이용하여 map object를 만들었고 다음은 list에 넣었다.
그 다음은 반복적으로 2번,3번 수행한 것들이다.

continue ...



zip
~~~~~~~~~~~~~~~~
파이썬 문서의 의하면 다음과 같이 정의되어 있다.

.. code-block::Python

    zip(*iterables) returns an iterator of tuples, where the i-th tuple contains the
    i-th element from each of the argument sequences or iterables. The iterator stops
    when the shortest input iterable is exhausted. With a single iterable argument, it
    returns an iterator of 1-tuples. With no arguments, it returns an empty iterator.
.


이전 장에서 zip의 용법을 사용했었다.
다음 예제을 보자.

.. code-block::Python

    >>> grades = [18, 23, 30, 27, 15, 9, 22]
    >>> avgs = [22, 21, 29, 24, 18, 18, 24]
    >>> list(zip(avgs, grades))
    [(22, 18), (21, 23), (29, 30), (24, 27), (18, 15), (18, 9), (24, 22)]
    >>> list(map(lambda *a: a, avgs, grades))  # equivalent to zip
    [(22, 18), (21, 23), (29, 30), (24, 27), (18, 15), (18, 9), (24, 22)]
.

zip과 map이 사용되는 다음 예제를 보자.

.. code-block::Python

    >>> a = [5, 9, 2, 4, 7]
    >>> b = [3, 7, 1, 9, 2]
    >>> c = [6, 8, 0, 5, 3]
    >>> maxs = map(lambda n: max(*n), zip(a, b, c))
    >>> list(maxs)
    [6, 9, 2, 9, 7]
.


filter
~~~~~~~~~~~~~~~~
파이썬 문서의 의하면 다음과 같이 정의되어 있다.

.. code-block::Python

    filter(function, iterable) construct an iterator from those elements
    of iterable for which function returns True. iterable may be either a sequence, a
    container which supports iteration, or an iterator. If function is None, the identity
    function is assumed, that is, all elements of iterable that are false are removed.
.
예제를 보도록 하자

.. code-block::Python

    >>> test = [2, 5, 8, 0, 0, 1, 0]
    >>> list(filter(None, test))
    [2, 5, 8, 1]
    >>> list(filter(lambda x: x, test))  # equivalent to previous one
    [2, 5, 8, 1]
    >>> list(filter(lambda x: x > 4, test))  # keep only items > 4
    [5, 8]
.





5.2 Comprehensions
-------------------
파이썬에서 comprehensions로 list,dict,set을 제공한다.

다음 예제를 보자

.. code-block::Python

    >>> squares = []
    >>> for n in range(10):
    ...     squares.append(n ** 2)
    ...
    >>> list(squares)
    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

    # This is better, one line, nice and readable
    >>> squares = map(lambda n: n**2, range(10))
    >>> list(squares)
    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

.
상기 코드와 동일하게 다음과 같이 표현할 수 있다.

.. code-block::Python

    >>> [n ** 2 for n in range(10)]
    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

.


Nested Comprehensions
~~~~~~~~~~~~~~~~~~~~~~~~~

다음 예제를 보자.

.. code-block::Python

    items = 'ABCDE'
    pairs = []

    for a in range(len(items)):
        for b in range(a, len(items)):
            pairs.append((items[a], items[b]))

    print(pairs)

.
list comprehensions으로 변경한 다음 코드를 보자.

.. code-block::Python

    items = 'ABCDE'
    pairs = [(items[a], items[b])
        for a in range(len(items)) for b in range(a, len(items))]

    print(pairs)
.

Filtering a comprehension
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Pythagorean triple 예제를 보자 (a2 + b2 = c2)

.. code-block::Python

    from math import sqrt

    # this will generate all possible pairs
    mx = 10
    legs = [(a, b, sqrt(a**2 + b**2))
        for a in range(1, mx) for b in range(a, mx)]
    # this will filter out all non pythagorean triples
    legs = list(
        filter(lambda triple: triple[2].is_integer(), legs))

    print(legs)  # prints: [(3, 4, 5.0), (6, 8, 10.0)]
.
inter로 리턴하는 예제를 보자.

.. code-block::Python

    from math import sqrt

    mx = 10
    legs = [(a, b, sqrt(a**2 + b**2))
        for a in range(1, mx) for b in range(a, mx)]
    legs = filter(lambda triple: triple[2].is_integer(), legs)

    # this will make the third number in the tuples integer
    legs = list(
        map(lambda triple: triple[:2] + (int(triple[2]), ), legs))

    print(legs)  # prints: [(3, 4, 5), (6, 8, 10)]
.

list comprehesion으로 표현해 보자.

.. code-block::Python

    from math import sqrt
    # this step is the same as before
    mx = 10
    legs = [(a, b, sqrt(a**2 + b**2))
        for a in range(1, mx) for b in range(a, mx)]
    # here we combine filter and map in one CLEAN list comprehension
    legs = [(a, b, int(c)) for a, b, c in legs if c.is_integer()]

    print(legs)  # prints: [(3, 4, 5), (6, 8, 10)]
.








5.3 Generators
-------------------




5.4 Some performance considerations
-------------------




5.5 Don't overdo comprehensions and generators
-------------------



5.6 Name localization
-------------------



5.7 Generation behavior in built-ins
-------------------




5.8 One last example
-------------------




5.9 Summary
-------------------









