
[출처 : schoolofweb - 이상희  : 파이썬 - 데코레이터](https://schoolofweb.net/blog/posts/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EB%8D%B0%EC%BD%94%EB%A0%88%EC%9D%B4%ED%84%B0-decorator/)

Decorator : 사전적 의미 - 장식가 또는 인테리어 디자이너
기존의 코드에 여러가지 기능을 추가하는 파이썬 구문
##### 예제 1

```python
def outer_function(msg):
	def inner_function():
		print(msg)
	return inner_function

hi_func = outer_function('Hi')
bye_func = outer_function('Bye')

hi_func()
bye_func()
```

```bash
$ python decoratoer.py
Hi
Bye
```

데코레이터 코드와 아주 비슷한 코드지만 함수를 다른 함수의 인자로 전달한다는 점이 다르다.
##### 예제2

```python
def decorator_function(original_function):
	def wrapper_function():
		return original_function()

def displat():
	print('display 함수가 실행되었습니다.')

decorated_display = decorator_function(display)

decorated_display()
```

```shell
$ python decorator.py
display 함수가 실행됐습니다.
```

---
### 사용이유
---
기존 코드를 수정하지 않고도, 래퍼(wrapper)함수를 이용하여 여러가지 기능을 추가할 수  있다.
##### 예제3
```python
def decorator_function(original_function):
	def wrapper_function():
		print('{}함수가 호출되기 전입니다.'.format(original_function.__name__))
		return original_function()
	return wrapper_function

def display_1():
	print('display_1 함수가 실행됐습니다.')

def displya_2():
	print('display_2 함수가 실행됐습니다.')

display_1 = decorator_function(display_1)
display_2 = decorator_function(display_2)

display_1()
print()
display_2()
```

```bash
$ python decorator.py
display_1 함수가 호출되기 전 입니다.
display_1 함수가 실행되었습니다.

display_2 함수가 호출되기 전 입니다.
display_2 함수가 실행되었습니다.
```

위의 예제와 같이 하나의 데코레이터 함수를 만들어 display_1과 display_2 두개의 함수에 기능을 추가할 수 있다. 다만 일반적으로는 @심볼과 데코레이터 함수의 이름을 붙여 간단한 구문을 사용한다.
##### 예제4

```python
def decorator_function(original_function):
	def wrapper_function():
		print('{} 함수가 호출되기 전 입니다. '.format(original_function.__name__))
		return original_function()
	return wrapper_function

@decorator_function
def display_1():
	print('display_1 함수가 실행되었습니다.')

@decorator_function
def display_2():
	print('display_2 함수가 실행됐습니다.')

display_1()
print()
display_2()
```

```bash
$ python decorator.py
display_1 함수가 호출되기 전 입니다.
display_1 함수가 실행되었습니다.

display_2 함수가 호출되기 전 입니다.
display_2 함수가 실행되었습니다.
```

#### 인수를 갖진 함수를 데코레이팅 하고 싶은 경우
---
##### 예제5
```python
def decorator_function(original_function):
	def wrapper_function():
		print('{} 함수가 호출되기 전 입니다.'.format(original_function.__name__))
		return original_function()
	return wrapper_function()

@decorator_function
def display():
	print('display 함수가 실행됐습니다.')

@decorator_function
def display_info(name, age):
	print('display_info({},{}) 함수가 실행됐습니다. '.format(name, age))

display()
print()
display_info('John', 25)
```

```bash
$ python decorator.py
display 함수가 호출되기전 입니다.
display 함수가 실행됐습니다.

Traceback (most recent call last):
  File "decorator.py", line 21, in <module>
    display_info('John', 25)
TypeError: wrapper_function() takes 0 positional arguments but 2 were given
```

다음과 같이 코드를 수정하면 문제가 해결됩니다.
##### 예제6
```python
def decorator_function(original_function):
	def wrapper_function(*argsm **kwargs):
		print('{} 함수가 호출되기 전 입니다.'.format(original_function.__name__))
	return wapper_function

@decorator_function
def display():
	print('display 함수가 실행되었습니다.')

@decorator_function
def display_info(name, age):
	print('display_info({}{}) 함수가 실행됐습니다.'.format(name, age))

display()
print()
display_info('John', 25)
```

```bash
$ python decorator.py
display 함수가 호출되기전 입니다.
display 함수가 실행됐습니다.

display_info 함수가 호출되기전 입니다.
display_info(John, 25) 함수가 실행됐습니다.
```

#python 
#decorator
