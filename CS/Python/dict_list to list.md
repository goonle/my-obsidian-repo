
### 발단
---
데이터 중에 하나의 키만 존재하는 리스트가 있었다.
```python
data = [{'a': 123}, {'a':312}, ...]
```

키 값은 알 수 없는 상태에서 키를 알아내기 위해 dictionary.keys() 함수를 사용했고 
다른 코드를 짤 땐, 키값의 비교를 위해 for문을 사용했기 때문에 당연히 list라고 판단,
키는 한개만 존재한다고 생각하니 0번째 값을 받으려고 했는데

```python
data = [...]
keyList = data[0].keys()
the_key  = keyList[0]
```

the_key에서 에러가 발생했다.  dict_list는 list의 형식이 아니기 때문에 사용할 수 없다는 에러였다.
그래서 검색을 했더니 아래의 코드가 나왔다.

```python
data = [...]
keyList = [*data[0]]
the_key = keyList[0]
```

### 아스테리스크\(\*\)
---
처음엔 뭐지 싶었다. 포인터인가? 일단 넘어가고 생각을 해보니 노트를 적었었던
\*args 와 \*\*kargs 가 생각났다.

#### 내 이해
---
\*args를 언제 사용하는가?  파라미터를 전달 받을때.
순차적인 데이터를 받을 때 사용했다. 
```python
def test(*args):
	print(args)
test('a','b','c')
#출력 : 'a', 'b' , 'c'
```

그렇다면 objcet의 순차적으로 선언된 값은 key 값일 것이다. object의 key에 해당되는 값이 value이기에 object 안에서는 key가 선언되었다고 이해했다. 그래서 아래의 코드로 테스트를 해봤다.

```python
a = { 'a' : 1, 'b' : 2, 'c': 3 }
print(*a)
# 출력 : a b c
```

출력 값에서는 세개의 값이 들어 있기 때문에 a b c로 표현된 것으로 보인다. 세개의 값을 리스트로 감쌌기 때문에 예제 코드가 나온 것을 보인다.

그렇다면 \*\*kwargs도 체크해야 했다
```python
a = { 'a' : 1, 'b' : 2, 'c': 3 }
print(**a)
#  출력 : TypeError: 'a' is an invalid keyword argument for print()
print({**a})
# { 'a' : 1, 'b' : 2, 'c': 3 }
```

\*\*의 값은 'a' : 1 의 형식의 키 와 벨류 선언 형식이기 때문에 사용할 수 없었다.


#python 