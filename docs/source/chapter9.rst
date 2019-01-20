chapter 9: Magic Methods,Properties,and Iterators
====================================================
파이썬에서는 앞뒤로 2개의 언더 스코어를 붙이는 독특한 이름을 가진것이 있다.
예를 들면 (__future__) 어리한 spelling은 중요한 의미를 가진다는 것이다.
그런 이름을 생성하지 말아야 한다. 언어에 있어서 그런 유명한 것들은 매직으로 구성되어 있다.
만약 당신의 object가 그런 method중에 하나를 구현한다고 하면 이러한 method는 특별한 환경하에서 호출될 것이다.
이것은 드물게 직접 호출될 필요가 있다.
이 장에서는 이러한 magic method를 다룰것이다.

9.1 If You're Not Using Python 3
------------------------------------



9.2 Constructors
-------------------
첫번째 magic method는 constructor이다.이전에 이런 어구를 들어보지 못했다면, 이미 이전 예제에서 사용되어 왔던
초기화 method이다.

.. code-block:: python

    >>> f = FooBar()
    >>> f.init()
constructor는 다음처럼 만들 수 있다.

.. code-block:: python

    >>> f = FooBar()

파이썬에서 constructor는 매우 쉽다.
단지 init 함수를 변경하면 __init__ 으로 바꿔주면 된다.

.. code-block:: python

    class FooBar:
        def __init__(self):
        self.somevar = 42
    >>> f = FooBar()
    >>> f.somevar
    42

어떤 파라미터와 어떻게 constructor가 동작되는지 궁금할지도 모르겠다.

.. code-block:: python

    class FooBar:
        def __init__(self, value=42):
        self.somevar = value

    >>> f = FooBar('This is a constructor argument')
    >>> f.somevar
    'This is a constructor argument'

Overriding Methods in General, and the Constructor in Particular
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
7장에서 inheritance를 봤다. 각 클래스는 한개 이상의 superclass를 가지고 있다.
class B 인스턴스에서 이러한 함수가 호출되고 이것이 발견되지 않으면 superclass A를 찾게 될것이다.

.. code-block:: python

    class A:
        def hello(self):
            print("Hello, I'm A.")
    class B(A):
        pass

    a = A()
    b = B()
    a.hello()
    #Hello, I'm A.
    b.hello()
    #Hello, I'm A


    class B(A):
        def hello(self):
            print("Hello, I'm B.")

    b = B()
    b.hello()

아래처험 상속받아 method를 다시 정의 하면 결과가 달라진다.
overriding은 일반적으로 상속 메카니즘에서 중요한 요소이다.특히나 constructor에 있어서는 중요하다.
constructor는 새로운 constructor ojbect를 초기화 한다.
모든 하위 클래스들은 상위 클래스 뿐 아니라 그 자신의 초기화 코드가 필요할 것이다.
overriding 메카니즘이 모든 method들에 똑같을지라도,보통의 method를 만났을때보다 constructor를 만났을때 종종 특별한 문제를 만나게
될것이다.
클래스의 constructor를 override하게 되면 상위 클래스의 constructor를 호출할 필요가 있다.
그리고 초기화 되지 않은 object를 가지게 될것이다.

.. code-block:: python

    class Bird:
        def __init__(self):
            self.hungry = True
        def eat(self):
            if self.hungry:
                print('Aaaah ...')
                self.hungry = False
            else:
                print('No, thanks!')


    b = Bird()
    b.eat()
    b.eat()

    class SongBird(Bird):
        def __init__(self):
            self.sound = 'Squawk!'
        def sing(self):
            print(self.sound)

    sb = SongBird()
    sb.sing()
    sb.eat()

    Traceback (most recent call last):
    File "<stdin>", line 1, in ?
    File "birds.py", line 6, in eat
    if self.hungry:
    AttributeError: SongBird instance has no attribute 'hungry'

SongBrid는 Bird의 하위 클래스이다.그래서 eat method를 상속받는다.만약 그것을 호출한다면 오류가 날것이다.
constructor가 override 되면 hungry atrribute를 초기화 하는 코드가 포함되지 않는다.


Calling the Unbound Superclass Constructor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
이 장에서 얘기하는것은 이야기기 이어질 것이다.
현재 버젼에서 super 함수를 사용한다는 것은 명확히 길이 있다.
이전 내용에서 super class의 constructor를 호출하는 것은 매우 쉽다. 앞에서 언급했던 초기화 문제에 대해서 답을 주고자 한다.






9.3 Item Access
-------------------




9.4 More Magic
-------------------


9.5 Properties
-------------------


9.6 Iterators
-------------------



9.7 Generators
-------------------



9.8 The Eight Queens
----------------------



9.9 A Quick Summary
-------------------


