[출처 : cori 티스토리 - One-Hot Encoding ](https://cori.tistory.com/163)
### 정의
---
N개의 클래스를 N차원의 One-Hot 벡터로 표현되도록 변환한다. (고유값들을 피처로 만들고 정답에 해당하는 열은 1, 나머진 0으로 -)

```python
from sklearn.preprocessing import OneHotEncoder import pandas as pd 
# 예제 데이터 생성 
data = {'색깔': ['빨강', '파랑', '노랑', '빨강']} 
df = pd.DataFrame(data) 
# OneHotEncoder 객체 생성 
encoder = OneHotEncoder() 
# '색깔' 특성에 대해 원핫 인코딩 적용 
encoded_data = encoder.fit_transform(df[['색깔']]).toarray() 
# 인코딩 결과를 DataFrame으로 변환
encoded_df = pd.DataFrame(encoded_data, columns=encoder.get_feature_names_out(['색깔'])) # 인코딩 결과 출력 
print("원본 데이터:\n", df) print("\n원핫 인코딩 결과:\n", encoded_df)
```

#one-hot-encoding
#python 