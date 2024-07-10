# 설치
```cmd
[install fast api]
pip install fastapi

[pip upgrade]
C:\Users\user_id\AppData\Local\Programs\Python\Python310\python.exe -m install --upgrade pip

[install uvicorn]
pip install "uvicorn[standard]"
```

# 예제
##### 1. 파일 만들기

```cmd
[파일 만들기]
cd 원하는경로
mkdir fastapi
copy NUL main.py

[파일 열기]
main.py

```

##### 2. 파일 작성하기
```python
import typing from Union
import fastapi from FastAPI

app = FastAPI()

@app.get("/")
def read_root():
	return {"Hello" : "World"}

@app.get("/items/{item_id})
def read_item(item_id:int, q:Union[str, None]= None) :
	 return {"item_id" : item_id, "q" : q}
	
```

##### 3. 서버 실행하기
```cmd
uvicorn main:app --reload
```

##### 4.확인하기
```url
1. http://127.0.0.1:8000
2. http://127.0.0.1:8000/items/5?q=somequery
3. http://127.0.0.1:8000/docs
4. http://127.0.0.1:8000/redoc
```

##### 5. 느낀점
세상에 API문서를 만들어주다니

# 요약
1. 타입과 본문을 한번에 선언
2. 데이터 검증

#fastapi
#python