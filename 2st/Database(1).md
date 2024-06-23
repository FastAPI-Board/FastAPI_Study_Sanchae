## FastAPI Database(1)

### Project Pybo 데이터 생성 원리
`질문 / 답변 작성 -> 데이터 생성(추가)`<br>
`질문 / 답변 삭제 -> 데이터 삭제` <br>
이러한 기능을 구현하기 위해서라면 데이터베이스가 필요한데 데이터 베이스를 사용하려면 SQL 쿼리라는 구조화된 질의를 작성하고 실행하는 등의 과정이 필요함 <br>
ORM (Object relational mapping)을 이용하여 파이썬 문법만으로도 데이터 베이스를 다루고자함.
ORM 을 이용하면 개발자가 쿼리를 직접 작성하지 않아도 데이터베이스의 데이터를 처리 할 수 있음. 

### ORM 과 SQL 비교
###### 만들고자 하는 Question 테이블
| id | subject | content      |
|----|---------|--------------|
| 1  | 안녕하세요   | 야식이 먹고 싶습니다. |
| 2  | 질문 있습니다 | 참아야 하는것일까    |
| 3  | 안녕하세요   | 잠이 와요... 커어어 |
>표에서 ID는 각 데이터를 구분하는 고윳값

 **SQL 로 데이터 삽입을 작성**<br>
``insert into question (subject, content) values ('안녕하세요', '야식이 먹고 싶습니다');``
 ``insert into question (subject, content) values ('질문 있습니다', '참아야 하는것인가');
``<br>
 ``insert into question (subject, content) values ('안녕하세요', '잠이 와요.. 커어어');
``<br>
 
**ORM을 이용한 데이터 삽입 작성** <br>

``question1 = Question(subject='안녕하세요',content='야식이 먹고 싶습니다')``<br>
 ``question2 = Question(subject='질문 있습니다',content='참아야 하는것인가');
``<br>
 ``question3 = Question(subject='안녕하세요',content='잠이 와요.. 커어어');
``<br>
 ``db.add(question1, question2, question3)
``<br>
<<<<<<< HEAD
=======
## 질문 목록을 위한 API 만들기
#### 파일 구조
```tsx
├──myapi
 ├── main.py
 ├── database.py
 ├── models.py
 ├── alembic.ini
 ├── myapi.db
 ├── domain
 │   ├── question
 │       ├──__init__.py
 │       ├──__question_router.py
 ├── migrations
 │   ├──versions
 │   ├──env.py
 └── frontend
```
#### Step1 라우터
1. 위의 파일 구조에 맞게 파일 생성 (파일 위치가 다르면 import 가 안되는 에러가 발생함 유의해야 함)<br>
2. 파일 중, question_router.py 파일에 아래 코드 입력
```tsx
from fastapi import APIRouter
>>>>>>> 7138760 (2-2까지 수행)

from database import SessionLocal
from models import Question

router = APIRouter(
    prefix="/api/question",
)


@router.get("/list")
def question_list():
    db = SessionLocal()
    _question_list = db.query(Question).order_by(Question.create_date.desc()).all()
    db.close()
    return _question_list
```
라우터 파일에는 APIRouter 클래스로 생성한 router 객체가 반드시 필요함 <br>
router 객체를 생성하여 FastAPI 앱에 등록해야만 라우팅 기능을 동작함. 
>라우팅이란 FastAPI가 요청받은 URL을 해석하여 그에 맞는 함수를 실행하여 그 결과를 리턴하는 행위를 말함.

 **위의 코드에 해당 개념 적용 및 코드 이해** 
```tsx
router = APIRouter(
    prefix="/api/question",
)
```
이 코드가 라우터 객체를 생성하는 코드 <br>
' API Router ' 클래스는 FastAPI의 라우터 객체를 생성함. 이 라우터 객체를 사용함으로써 엔드포인트 정의 할 수 있음. <br>
`/api/question/list` 라는 URL 요청이 발생하면` /api/question` 이라는 prefix가 등록된 `question_router.py` 파일의` /list`로 등록된 함수 `question_list`가 실행
```tsx
@router.get("/list")
def question_list():
    db = SessionLocal()
    _question_list = db.query(Question).order_by(Question.create_date.desc()).all()
    db.close()
    return _question_list
```
`question_list`함수: db 세션을 생성하고 해당 세션을 이용하여 질문 목록을 조회하여 return 하는 함수. <br>
세션 반환은 `db.close()`<br>
3. question_router.py 파일에 생성한 router 객체를 FastAPI 앱에 등록해야 함. 이에 main.py 파일 수정

```tsx
from fastapi import FastAPI
from starlette.middleware.cors import CORSMiddleware

from domain.question import question_router

app = FastAPI()

origins = [
    "http://127.0.0.1:5173",
]

app.add_middleware(
    CORSMiddleware,
    allow_origins=origins,
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)


app.include_router(question_router.router)

```
```tsx
app.include_router(question_router.router)

```
include_router 매서드를 사용하여 question_router.py 파일의 router 객체 등록. 
