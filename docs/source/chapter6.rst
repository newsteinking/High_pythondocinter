chapter 6: Abstraction
=======================
이장에서는 어떤것을 하는방법을 컴퓨터에게 말할 수 있는 그룹문을 함수로 표현하는 법을 배우도록 하겠다.
그것은 단 한번만 말한다.
계속해서 똑같은 상세 명령을 내릴 필요가 없다.
이장에서는 파라미터와 스코핑에 대한 내용으로 반복이 무엇이고 어떻게 실행되는지 배워보자.



6.1 Laziness is a Virtue
---------------------------
피노나치 숫자에 대한 예를 들어 보자
*피보나치 수(영어: Fibonacci numbers)는 첫째 및 둘째 항이 1이며 그 뒤의 모든 항은 바로 앞 두 항의 합인 수열이다. 처음 여섯 항은 각각 1, 1, 2, 3, 5, 8이

.. code-block:: python


    fibs = [0, 1]
    for i in range(8):
    fibs.append(fibs[-2] + fibs[-1])

    fibs = [0, 1]
    num = int(input('How many Fibonacci numbers do you want? '))
    for i in range(num-2):
    fibs.append(fibs[-2] + fibs[-1])
    print(fibs)

6.2 Abstraction and Struture
-------------------------------
축약은 단순 작업에 편리하다. 인간에게 컴퓨터 프로그램을 이해시킬 수 있는 중요 요소이다.
컴퓨터는 그 자체로 매우 간결하고 특별한 지시에 대해서 아주 좋아한다. 그러나 인간은 그렇지 않다.
만약 영화관을 가는길을 물어 보면, 앞으로 10걸음 가고 90도 돌아서 ....., 아마도 당신은 금방 잊어 버릴것이다.
길을 건너서 다리를 건너면 오른편으로 영화관이 보일것이다라고 얘기했다면 이해했을 것이다.
어떻게 겆고 다리를 어떻게 건너는지를 아는 조건에서는 당신은 상세한 설명이 필요없다.
컴퓨터 프로그램도 똑같은 구조로 되어 있다. 당신의 프로그램은 간결해야 한다. 페이지 다운,빈번도 계산,각 빈도수 프린트
이러한 것은 쉽게 이해할 수 있다.
다음 설명을 파이썬으로 변경해 보자.

.. code-block:: python

    page = download_page()
    freqs = compute_frequencies(page)
    for word, freq in freqs:
    print(word, freq)



6.3 Creating Your Own Functions
---------------------------------
함수라른 것은 파라미터를 매개체로 해서 호출할 수 있는 것을 의미한다.
함수를 실행하면 어떤 액션을 취하고 리턴값을 주게 되어 있다.
일반적으로 어떤것이 호출할 수 있는지 아니면 빌트인 함수 callable이 아닌지 말할 수 있다.

.. code-block:: python

    >>> import math
    >>> x = 1
    >>> y = math.sqrt
    >>> callable(x)
    False
    >>> callable(y)
    True

이전장에서 말했듯이 함수는 구조적 프로그래밍의 중심이다.

.. code-block:: python

    def hello(name):
        return 'Hello, ' + name + '!'

Documenting Functions
~~~~~~~~~~~~~~~~~~~~~~
코드에 코멘트를 처리하는것 이외에 함수 앞단에 string으로 넣는것을 docstring 이라고 한다.

.. code-block:: python

    def square(x):
        'Calculates the square of the number x.'
        return x * x

docstring은 다음처럼 접근할 수 있다.

.. code-block:: python

    >>> square.__doc__
    'Calculates the square of the number x.'

특별한 빌트인 함수로 help도 유용하다.

.. code-block:: python

    >>> help(square)
    Help on function square in module __main__:
    square(x)
    Calculates the square of the number x.

Functions That Aren’t Really Functions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
함수는 수학적 의미에서 항상 파라미터들로부터 계산되어진 어떤 값을 리턴한다.
파이썬에서는 어떤 함수는 리턴을 하지 않는다.
파이썬에서 리턴하지 않는 함수는 리턴값을 가지지 않는다.리턴 문구를 쓴다면 리턴 이후는 값이 없다.


6.4 The Magic of Parameters
-----------------------------
함수를 사용하는것은 직관적이고 그것을 생성하는것은 복잡하지 않다.

Can I Change a Parameter?
~~~~~~~~~~~~~~~~~~~~~~~~~
함수가 파리미터를 통해 값을 얻는다. 그 값을 변경할 수 있는가?
파라미터는 변수값이다.
함수안에서 할당한 값은 밖에 있는 값을 변화 시키지 않는다.
함수 안에서의 strings(numbers,tuples)는 변경할 수 없다.따라서 그것은 변경할 수 없다.

.. code-block:: python

    >>> def try_to_change(n):
    ... n = 'Mr. Gumby'
    ...
    >>> name = 'Mrs. Entity'
    >>> try_to_change(name)
    >>> name
    'Mrs. Entity'

    >>> name = 'Mrs. Entity'
    >>> n = name # This is almost what happens when passing a parameter
    >>> n = 'Mr. Gumby' # This is done inside the function
    >>> name
    'Mrs. Entity'

.. code-block:: python

    >>> def change(n):
    ... n[0] = 'Mr. Gumby'
    ...
    >>> names = ['Mrs. Entity', 'Mrs. Thing']
    >>> change(names)
    >>> names
    ['Mr. Gumby', 'Mrs. Thing']

    >>> names = ['Mrs. Entity', 'Mrs. Thing']
    >>> n = names # Again pretending to pass names as a parameter
    >>> n[0] = 'Mr. Gumby' # Change the list
    >>> names
    ['Mr. Gumby', 'Mrs. Thing']
위에서 함수에서 변경 불가능한것과 같이 아래 처험 동일하게 처리할 수 있다.
이런 종류를 봐왔을 것이다.
이런것을 피하기 위해서 list를 복사해서 쓴다.

.. code-block:: python

    >>> names = ['Mrs. Entity', 'Mrs. Thing']
    >>> n = names[:]
    >>> n is names
    False
    >>> n == names
    True

여기서 n을 변경하더라도 names에는 영향을 미치지 않는다.

.. code-block:: python

    >>> n[0] = 'Mr. Gumby'
    >>> n
    ['Mr. Gumby', 'Mrs. Thing']
    >>> names
    ['Mrs. Entity', 'Mrs. Thing']


Why Would I Want to Modify My Parameters?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
데이터 구조를 변경하기 위하여 함수를 사용하는것은 프로그램에 축약을 소개하기에 좋은 방법이다.
이름을 저장하고 first name,middle name,last name을 검색하는 프로그램을 짜보자.
데이터 구조는 다음과 같다.

.. code-block:: python

    storage = {}
    storage['first'] = {}
    storage['middle'] = {}
    storage['last'] = {}

데이터 구조 저장소는 first,middle,last를 갖는 dictionary이다. 각 키 아래 각자 dictionary를 저장한다.
first,middle,last를 key로 하고 각각 값으로 사람의 리스트를 집어 넣는다.

.. code-block:: python

    >>> me = 'Magnus Lie Hetland'
    >>> storage['first']['Magnus'] = [me]
    >>> storage['middle']['Lie'] = [me]
    >>> storage['last']['Hetland'] = [me]

    >>> storage['middle']['Lie']
    ['Magnus Lie Hetland']

앞서 본것과 같이 이러한 구조에 사람을 집어 넣는것은 단순 작업이다.특히 fist,middle,last 이름을 가진 사람의 경우이다.
다음의 예를 보자.

.. code-block:: python

    >>> my_sister = 'Anne Lie Hetland'
    >>> storage['first'].setdefault('Anne', []).append(my_sister)
    >>> storage['middle'].setdefault('Lie', []).append(my_sister)
    >>> storage['last'].setdefault('Hetland', []).append(my_sister)
    >>> storage['first']['Anne']
    ['Anne Lie Hetland']
    >>> storage['middle']['Lie']
    ['Magnus Lie Hetland', 'Anne Lie Hetland']

큰 프로그램을 짤 경우 다음 예를 보자.

.. code-block:: python

    def init(data):
        data['first'] = {}
        data['middle'] = {}
        data['last'] = {}

    >>> storage = {}
    >>> init(storage)
    >>> storage
    {'middle': {}, 'last': {}, 'first': {}}

이름을 저장하기 전에 얻어오는 경우를 생각해 보자.

.. code-block:: python


    def lookup(data, label, name):
        return data[label].get(name)

    >>> lookup(storage, 'middle', 'Lie')
    ['Magnus Lie Hetland']

다음 예를 보자

.. code-block:: python

    def store(data, full_name):
        names = full_name.split()
        if len(names) == 2: names.insert(1, '')
        labels = 'first', 'middle', 'last'
        for label, name in zip(labels, names):
            people = lookup(data, label, name)
            if people:
                people.append(full_name)
            else:
            data[label][name] = [full_name]

    >>> MyNames = {}
    >>> init(MyNames)
    >>> store(MyNames, 'Magnus Lie Hetland')
    >>> lookup(MyNames, 'middle', 'Lie')
    ['Magnus Lie Hetland']

다음 또한 동작이 된다.

.. code-block:: python

    >>> store(MyNames, 'Robin Hood')
    >>> store(MyNames, 'Robin Locksley')
    >>> lookup(MyNames, 'first', 'Robin')
    ['Robin Hood', 'Robin Locksley']
    >>> store(MyNames, 'Mr. Gumby')
    >>> lookup(MyNames, 'middle', '')
    ['Robin Hood', 'Robin Locksley', 'Mr. Gumby']


6.4 What If My Parameter is Immutable?
-----------------------------------------
어떤 언어들(C++, Pascal,Ada) 파라미터를 엮고 함수밖에서 변경하는 것이 다반사이다.
파이썬은 이것이 직접적으로 가능하지 않다. 파라미터 오브젝트들만 단지 변경가능하다.
숫자같은 변경 불가능한 것은 어떻게 할까?
미안하지만 그것은 할 수 없다. 당신의 함수로 부터 필요로 하는 모든 값을 리턴해야하기때문이다.
다음 예를 보자.

.. code-block:: python

    >>> def inc(x): return x + 1
    ...
    >>> foo = 10
    >>> foo = inc(foo)
    >>> foo
    11
파라미터값을 변경하고자 하면 다음처럼 리스트에 랩핑해서 얻을 수 있다.

.. code-block:: python

    >>> def inc(x): x[0] = x[0] + 1
    ...
    >>> foo = [10]
    >>> inc(foo)
    >>> foo
    [11]



6.5 Parameter Practice
-----------------------------





6.6 Scoping
-----------------------------






6.7 Recursion
-----------------------------





6.8 Another Classi:Binary Search
------------------------------------



6.9 A Quick Summary
------------------------------------



6.10 New Functions in This Chapter
------------------------------------

6.11 What Now?
------------------------------------

