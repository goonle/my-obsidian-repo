Numpy란?

1. 정의 . 
Numarray와 Numeric이라는 오래된 Python 패키지를 계승해서 나온 수학 및 과학 연산을 위한 파이썬 패키지이다. Py는 파이썬을 나타내기 때문에, 일반적으로 넘파이라고 읽는다.

2. 사용하는 곳
파이썬으로 수치해석, 통계 관련 기능을 구현한다고 할 때 Numpy는 가장 기본이 되는 모듈이다. 그만큼 Numpy는 수치해석, 통계 관련 작업시 중요한 역할을 하므로, 파이썬으로 관련 분야에 도전하고자 한다면 반드시 이에 대한 기초를 잘 쌓아두고 가자.

- 데이터분석

3. Numpy의 기본 
- NumPy array로 파이썬 기본 list에 호환되는 array를 사용합니다.
- 기본 list 대신 array를 사용하는 이유는 배열 계산이 더 쉬울 뿐만 아니라 성능적인 면에서도 메모리를 덜 차지하여 빠른 속도를 가질 수 있다고 합니다.
- 더 빠른 속도를 가질 수 있는 전제조건은 데이터 타입이 같은 경우 혹은 동질성을 지닌 경우에 한 해 빠르지만 그렇지 않을 경우 느리다고 효율적이지 못하다고 합니다.

4. 기본 사용 method
- numpy.array()
- numpy.zeros()
- numpy.ones()
- numpy.twos() -- 존재 x
- numpy.empty()
- np.empty((3,5)) 차원 배열
- arr3.dtype 데이터타입
- arr3.shape 모양 
- np.arange(10) range와 비슷
- np.arange(3,10) 3에서 10까지 (3포함 10 미포함)
- 덧셈과 뺄셈은 기본 배열의 덧셈 뺄셈과 같음
- 곱셈은 학교에서 배우는 행열의 복잡한 곱셈이 아닌 같은 자리수의 곱셈
- 브로드 캐스트 (서로다른 형태의 array가 연산이 가능하게 하는것)
= 예제 ) array([[1, 2, 3],[4, 5, 6]]) + array([10, 11, 12])
=       = array([[11, 13, 15],[14, 16, 18]])
- 인덱싱 arr1[3]




docs
https://numpy.org/doc/stable/user/absolute_beginners.html

examples
https://firework-ham.tistory.com/33

examples 2
https://doorbw.tistory.com/171

#python
#numpy
