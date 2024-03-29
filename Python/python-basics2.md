 #### Q1. 파이썬은 인터프리터언어인가 
 파이썬은 1990년 귀도 반 로섬이 개발한 인터프리터 언어이다
 인터프리터 언어는 작성된 소스코드를 바로 실행하는 컴퓨터 프로그램/환경을 뜻한다. 소스코드를 한줄씩 읽기 때문에 별도의 실행파일이나 시작지점이 존재하지 않는다
 
 #### Q2. 인터프리터 언어와 컴파일 언어의 차이점은 무엇인가 
인터프리터 언어는 소스코드를 한줄씩 읽기 때문에 별도의 실행 파일이나 시작지점이 존재하지 않다. 동적언이다. 변수의 타입이 언제든지 바뀔 수 있기 때문에 코드가 간결해진다.    
컴파일 언어는 코드를 기계어로 변환하는 과정과 실행 과정이 따로 존재한다.    
컴파일 언어의 경우 컴파일 후 코드가 기계어로 변환되어 있기 때문에 실행시간이 빠르다. 인터프리터언어는 컴파일 언어에 비해 속도가 느리지만 빌드 과정없이 바로 실행이 가능하다 

#### Q3. 인터프리터언어와 컴파일언어의 장단점 무엇인가
인터프리터언어는 실행과 컴파일을 동시에 수행한다. 필요한 부분만 컴파일하여 그때그때 실행하기 때문에 속도가 빠르지만 프로그램 실행과 컴파일을 동시에 수행하기 때문에 프로그램 구동에 걸리는 시간이 느리다    
컴파일언어는 한번에 모든 코드를 기계어로 번역한다. 따라서 큰 프로젝트에서 컴파일 속도는 느리지만 이미 컴파일을 수행했기 때문에 프로그램 구동이 매우 빠르다

> 동적언어   
> 해당 언어의 자료형 타입이 컴파일시 정해지는 것이 아니고 실행시 자료형 타입이 결정된다(javascript, ruby, python)   

> 정적언어
> 자료형 타입을 컴파일시에 결정한다. 변수에 들어갈 값의 형태에 자료형을 지정해주어야 한다.(c, c#, java) 

> 컴파일    
>  사람이 이해하는 언어를 __컴퓨터가 이해할수 있는 언어로 변역하는 과정__ (컴퓨터는 모든 명령을 CPU가 처리하고 CPU는 명령을 0과 1로 이해하고 실행한다.)

#### Q4. 인터프리터언어와 컴파일언어의 종류는 무엇이 있는가
인터프리터언어로는 html, javascript, sql, python, ruby등이 있다
컴파일언어로는 c, c#, c++, java등이 있다


#### Q5. 버그를 찾거나 정적 분석을 할 수 있는 어플리케이션이 있는가
pychecker, 정적 분석에 사용된다. 
```python
pychecker python_file_name.py
```
pylint, 파이썬 모듈들이 표준 코딩을 만족하는지 체크한다


#### Q6. decorator는 언제 사용되는가
데코레이터는 함수를 받아 명령을 추가한 뒤 이를 다시 함수의 형태로 반환하는 함수이다. __즉 함수의 내부를 수정하지 않고 기능에 변화를 주고 싶을때 사용한다__   
데코레이터는 여러 함수들에 부분적으로 중복되는 작업이 있는 경우 코드의 재사용성을 높이기 위해 사용된다. 
```python
def decorator_name(func):
  def wrapper(*args, **kwargs):
    # 명령 작성
    return func(*args, **kwargs) # 받아온 함수 실행
  return wrapper
```

#### Q7. 리스트와 튜플의 차이점은 무엇인가
공통점으로는 두 자료형 모두 순서가 있기 때문에 순서를 관리할 수 있다.   

리스트는 mutable(가변적)한 자료형으로 값을 인덱스로 수정하는 것이 가능하다. 리스트는 객체값이 변경될 때 메모리가 재할당 되지 않고 메모리가 동일하기 때문에 원했던 값이 나오지 않을 수 있다
```python
a = ['a', 'b']
b = a
a.append('c')

# 원했던 값 : a = ['a', 'b', 'c'], b = ['a', 'b']
# 실제 값 : a = ['a', 'b', 'c'], b = [['a', 'b', 'c']
```
튜플의 경우 immutable(불변적)한 자료형으로 값을 수정할 수 없다. 튜플은 객체값이 변경될때 메모리가 재할당되어 메모리 주소가 변경된다    

+ a ) 리스트를 딕셔너리에서 키로 사용할 수 없다. 불변값만 해시를 만들 수 있기 때문에 딕셔너리의 키에는 불변값만 사용이 가능하다. 대신 리스트를 키로 사용하고 싶다면 리스트를 튜플로 변경하여 사용 가능하다   

#### Q8. 파이썬에서 메모리를 어떻게 관리하는가
[파이썬의 내부 메모리 관리 정리](https://github.com/heejung-gjt/tech-interview/blob/main/Python/%EB%82%B4%EB%B6%80%20%EB%A9%94%EB%AA%A8%EB%A6%AC%20%EA%B4%80%EB%A6%AC.md)   

#### Q9. GC 작동방식을 설명해라
  - 레퍼런스 카운팅이 무엇인가   
  - 순환 참조가 무엇인가    
  - 가비지 컬렉션(Garbage collection)과 레퍼런스 카운팅(reference counting)에 대해 설명해라    
[파이썬의 내부 메모리 관리 정리](https://github.com/heejung-gjt/tech-interview/blob/main/Python/%EB%82%B4%EB%B6%80%20%EB%A9%94%EB%AA%A8%EB%A6%AC%20%EA%B4%80%EB%A6%AC.md)   


#### Q10. Lambda와 Def의 주된 차이점은 무엇인가요?
둘 다 함수를 정의하는 방법이다.    
lambda의 경우 임시적으로 만들어지는 함수이기 때문에 사용후에는 메모리에서 사라진다. 즉 일회성 함수라고 할 수 있다. def 키워드는 메모리에 할당되어 재사용이 필요한 함수를 만들때 사용한다   

#### Q11. Docstring은 무엇인가요?
쌍따옴표 세개를 사용하여 여러줄의 주석을 작성할 수 있다. 
함수나 클래스를 선언한 다음 라인에 해당 클래스나 함수의 기능이 무엇인지에 대한 주석을 달때 사용한다   
__doc__를 사용해 주석을 읽을 수 있다 ```User.__doc__```


#### Q12. Function call 혹은 A callable Object는 무엇인가요?
- function call은 함수 호출이며 함수를 실행하는 명령문, 함수 이름과 인자 리스트로 구성된다        
- callable object는 __상태를 가지는 함수를 매직메서드인 __call__ 을 사용하여 만들 수 있다.__ callable은 함수, 클래스 인스턴스, 메서드 등이 호출 가능한지 점검해주는 함수이다. 파이썬에는 callable내장함수가 있다. 매직메서드인 __call__메서드를 확인하면 된다.     

객체는 함수가 아니기 때문에 에러가 발생한다
```python
class User:
    pass

user = User()
n = plus(1, 2) # TypeError: 'Plus' object is not callable
```

매직 메소드인 __call__을 사용하면 객체를 함수처럼 사용할 수 있다
```python
class User:

    def __call__(self, name, age):
        return f'{name}의 나이는 {age}'

user = User()
n = user('kim', 24)
print(n) # kim의 나이는 24


```

```python
```


Call by value는 무엇인가요?

call by value와 call by reference의 차이점은 무엇인가요?

*args는 무엇은 하는 앤가요?

*kwargs는 무엇을 하는 앤가요?

파이썬에서 main() 메소드가 있나요?

GIL이란 무엇인가요(???)?

- 왜 GIL이 필요한가요?
    - thread-safe하다는게 어떤 뜻인가요?
    - 어떤 상황에서 성능 문제가 생기나요?
    - 다중 스레드가 동시에 실행될 때의 문제점이 무엇인가요?
    - race condition으로 인해 발생한 메모리 유실을 파이썬에서는  어떻게 해결할 수 있나요?
    - C에서는 이런 상황(이전 문제에서의 상황)을 막기위해 어떤 것을 사용하나요?
    - 멀티 스레드와 멀티 프로세서의 차이점이 무엇인가요?
    - 어떤 상황에서 멀티 스레드를 사용해야할까요?
    - 그래서 GIL의 문제를 어떻게 해결할 수있을까요? - cpu가 바쁘게 계산하는 일들은 numpy, scipy같이 GIL 밖에서 C코드로 연산할 수 있고, 병렬처리에 관해서는 멀티 프로세싱 사용할 수 있다. 굳이 thread 간의 동시처리가 필요하다면 Jython, IronPython, PyPy같은 것들 고려해볼 수 있다.
- 파이썬에서 스레드의 안정성은 어떻게 보장되나요?

- 힙 매니저는 어떤 일을 하나요?

- 파이썬에서 튜플은 무엇인가요?

- 파이썬에서 딕셔너리는 무엇인가요?

- 파이썬에서 Set은 무엇인가요?

- 파이썬에서 딕셔너리는 어떻게 사용되나요?

- 파이썬의 리스트의 자료구조는 어떻게 생겼을까요?
  - C에서 공부한 연결리스트와 같은 건가요?

- 파이썬에서 클래스는 무엇인가요?

  - OOP란 무엇인가요?
- 파이썬 클래스에서 Attributes와 Methods는 무엇인가요?

- 런타임 클래스 속성에 값을 할당하는 방법은 무엇인가요?

- 파이썬에서 상속은 무엇인가요?

  - 파이썬에서 Composition은 무엇인가요?
  - 클래스를 상속했을 때 메서드 실행 방식을 설명해주세요    

- 파이썬에서 Errors와 Exceptions는 무엇인가요?

Try / Exception / Finally는 어떻게 사용하나요?

파이썬에서 미리 정의된 조건에 대한 Exception를 어떻게 발생시키나요?

파이썬의 Iterator는 무엇인가요?

왜 이터레이터를 사용하나요?
iterators와 iterable의 차이는 무엇인가요?

사용하는 함수가 있나요? 무엇인가요?
이터러블한 객체와 시퀀스 객체의 종류와 차이점을 설명해주세요.
파이썬의 generator은 무엇인가요(?)?

이터레이터와 제너레이터의 차이점을 설명해주세요.
파이썬에서 Enumerate는 무엇인가요?

파이썬에서 Globals() 함수는 무엇인가요?

Self 는 어떤 키워드인가요?

python debugger 사용해본적 있나요?

pypy가 Cpython보다 빠른 이유가 무엇인가요?

JIT가 무엇인가요?
메모리 누수가 발생할 수 있는 경우 어떤 경우가 있을까요?