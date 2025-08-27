---
title:  "파이썬: 데코레이터"
author: "Woohyuk Jang"
draft: false

date: "2021-06-15"
description: ""
categories:
  - CS
tags:
  - TIL
  - fastai
last_modified_at: 2021-06-15
---

## 1. 데코레이터의 소개
```python
def bad_func_1():
    print("중복되는 기능")
    print("func_1만의 기능")


def bad_func_2():
    print("중복되는 기능")
    print("func_2만의 기능")
```

다음과 같은 코드는 무엇이 문제일까? 가장 큰 문제는 코드가 불필요하게 반복되고 있다는 것이다. 이런 식으로 코드를 짜면 재사용도 잘 안되고 func_1만 고치고 func_2는 고치는 것을 잊을 수도 있다.

그러면 다음과 같이 코드를 짜면 좋을 것이다.
```python
def add_feature(func):
    def wrapper():
        print("중복된 기능")
        func()
    return wrapper

def func_1():
    print("func_1만의 기능")

def func_2():
    print("func_2만의 기능")

add_feature(func_1)()
add_feature(func_2)()
```
재사용이 잘 된 코드다. 여기서 파이썬은 `add_feature(func_1)` 대신에 데코레이터 구문을 쓸 수 있도록 하고 있다.

```python
def add_feature(func):
    def wrapper():
        print("중복된 기능")
        func()
    return wrapper

@add_feature
def func_1():
    print("func_1만의 기능")

@add_feature
def func_2():
    print("func_2만의 기능")

func_1()
func_2()
```

## 2. 데코레이터의 일반적인 구조
```python
def decorator(func):

    def wrapper(*args, **kwargs):
        print("some feature of the decorator")
        return func(*args, **kwargs)

    return wrapper

@decorator
def example_1(n):
    return n * n

print(example_1(3))
```
- 이것이 입력값과 출력값을 가진 함수에 데코레이터를 적용하는 방법이다.
- `@decorator`는 기본적으로 `decorator(example_1)`과 같다는 것을 잊지 말자.

한편, 복수의 데코레이터를 적용할 수도 있다. 이때 실행순서는 위의 데코레이터부터 실행된다.
```python
def decorator1(func):

    def wrapper(*args, **kwargs):
        print("decorator 1")
        return func(*args, **kwargs)
    
    return wrapper

def decorator2(func):

    def wrapper(*args, **kwargs):
        print("decorator 2")
        return func(*args, **kwargs)
    
    return wrapper

@decorator1
@decorator2
def example_1(n):
    return n * n

print(example_1(3))
# decorator 1
# decorator 2
# 9
```

## 3. functools.wraps
```python
def decorator(func):

    def wrapper(*args, **kwargs):
        print("some feature of the decorator")
        return func(*args, **kwargs)

    return wrapper

@decorator
def example_1(n):
    return n * n

def example_2(n):
    return n

f = example_2

print(f.__name__)
print(example_1.__name__)
```
다음 예제를 실행해보자. 파이썬의 함수는 `__name__` 변수를 통해 정의될 당시의 이름을 저장하고 있다. 그래서 `f.__name__`을 실행하면 `example_2`가 나온다. 그런데 `example_1.__name__`의 값은 데코레이터에서 사용한 `wrapper`이다!

**이처럼 데코레이터를 적용하면 함수 메타데이터가 바뀐다는 문제점이 있다.** 이 문제점을 해결하기 위한 방법이 바로 `functools.wraps`를 이용하는 것이다. 

```python
from functools import wraps

def decorater(func):
    
    @wraps(func)
    def wrapper(*args, **kwargs):
        print("some feature of the decorator")
        return func(*args, **kwargs)

    return wrapper

@decorater
def example_1(n):
    return n * n

def example_2(n):
    return n

f = example_2

print(f.__name__)
print(example_1.__name__)
```

바뀐 점은 `@wraps(func)`를 적용했다는 점 뿐이다. 그런데 example_1의 메타데이터가 사라지지 않고 제대로 남아있음을 알 수 있다. 

## 4. 클래스 형태의 데코레이터
그렇게 자주 사용되지는 않지만 클래스 형태의 데코레이터도 있다. 클래스 형태의 데코레이터를 씌우면 나오는 객체는 클래스의 인스턴스이다.
```python
class DecoratorClass():
    original_name = ''

    def __init__(self, func):
        self.original_name += func.__name__
        self.func = func

    def __call__(self, *args, **kwargs):
        print("some feature of the decorater")
        return self.func(*args, **kwargs)

@DecoratorClass
def example_1(n):
    return n * n

print(example_1)
print(example_1(3))
print(example_1.original_name)
```

## 5. 데코레이터의 사용 예시
- 유저가 로그인 상태가 아니면 로그인 페이지로 리다이렉트
- 로그 남기기
- 테스팅

## 6. 참고자료
[School Of Web](http://schoolofweb.net/blog/posts/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EB%8D%B0%EC%BD%94%EB%A0%88%EC%9D%B4%ED%84%B0-decorator/)         
[Tistory 블로그](https://bluese05.tistory.com/30)        
[코딩 도장](https://dojang.io/mod/page/view.php?id=2427)
