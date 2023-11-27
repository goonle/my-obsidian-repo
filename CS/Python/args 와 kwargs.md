[출처 : brunch - princox - 나름 중급 파이썬1 *args와 *kwargs](https://brunch.co.kr/@princox/180)
### \*args
---
args = arguments
꼭 args를 써야할 필요는 없다
\*a,\*asdfagasdf 도 가능하다.

> 이 지시어는 복수개의 인자를 함수로 받고자 할 때 쓰인다.

### \*\*kwargs
---
kwargs = keyword argment

##### 예제
```python
def introduceEnglishName(**kwargs):
	for key, value in kwargs.items():
		print('{0} : {1}'.format(key, value))

introduceEnglishName(MyName = 'Chris!!')
```

```bash
$ python main.py
MyName : Chris!!
```

딕셔너리 형태로 내부에 전달 된다.

#python 
#args
#kwargs
