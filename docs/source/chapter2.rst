chapter 2: Lists and Tuples
==============================
파이썬 기본 빌트인 데이터 타입중에  list 와 tuple에 대해서 알아보자.


2.1 Sequence Overview
------------------------
list와 tuple의 차이점은 변경이 가능하냐이다.
list는 변경이 가능하고 tuple은 변경할 수 없다.

리스트는 다음과 같이 표현할 수 있다.

.. code-block:: python


    >>> edward = ['Edward Gumby', 42]
    >>> john = ['John Smith', 50]


2.2 Common Sequence Operators
-------------------------------
indexing, slicing, adding, multiplying, and checking for membership 등의 빌드인 연산자를 알아보자.

Indexing
~~~~~~~~~~
시퀀스 안에 있는 모든 요소는 숫자로 구성되어 있다.

.. code-block:: python

    >>> greeting = 'Hello'
    >>> greeting[0]
    'H'

마이너스 숫자는 마지막부터 시작해서 반대로 시작된다.

.. code-block:: python

    >>> greeting[-1]
    'o'

다음처럼 입력한 값을 직접 호출할 수 있다.


.. code-block:: python

    >>> fourth = input('Year: ')[3]
    Year: 2005
    >>> fourth
    '5'

Listing 2-1 Indexing Example

.. code-block:: python

    # Print out a date, given year, month, and day as numbers
    months = [
    'January',
    'February',
    'March',
    'April',
    'May',
    'June',
    'July',
    'August',
    'September',
    'October',
    'November',
    'December'
    ]
    # A list with one ending for each number from 1 to 31
    endings = ['st', 'nd', 'rd'] + 17 * ['th'] \
    + ['st', 'nd', 'rd'] + 7 * ['th'] \
    + ['st']
    year = input('Year: ')
    month = input('Month (1-12): ')
    day = input('Day (1-31): ')
    month_number = int(month)
    day_number = int(day)
    # Remember to subtract 1 from month and day to get a correct index
    month_name = months[month_number-1]
    ordinal = day + endings[day_number-1]
    print(month_name + ' ' + ordinal + ', ' + year)


Slicing
~~~~~~~~~~
다음처럼 두개로 나눌 수 있다.

.. code-block:: python

    >>> tag = '<a href="http://www.python.org">Python web site</a>'
    >>> tag[9:30]
    'http://www.python.org'
    >>> tag[32:-4]
    'Python web site'

슬라이싱은 본것과 같이 시퀀스에서 특정부분을 분리하는데 자주 쓰인다.
여기서 앞숫자와 뒷숫자가 중요하다.
처음숫자는 포함하고자하는 첫번째 엘리먼트 숫자이고 두번째는 첫 엘리먼트 이후 자르고자 하는 숫자이다.






Slicing
~~~~~~~~~~


Slicing
~~~~~~~~~~



Slicing
~~~~~~~~~~



Slicing
~~~~~~~~~~






2.3 Lists: Python's Workhorse
-------------------------------




2.4 Tuples:Immutable Sequence
-------------------------------




2.5 A Quick Summary
----------------------


