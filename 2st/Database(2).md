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
#### Error 관련 
```tsx

File "/Users/yanghwayeong/FastAPI_Study_Sanchae/projects/myapi/main.py", line 3, in <module>
from domain. question import question_router


File "/Users/yanghwayeong/FastAPI_Study_Sanchae/projects/myapi/domain/question/question_router.py", line 3, in ‹module>
from models import Question

ModuleNotFoundError: No module named 'domain. question models'

```
위에 Error가 발생하면 아래의 과정을 수행했는지 확인해야 할 필요가 있음. 
<br>
이 에러가 Question 테이블이 없어서 생긴 에러일 수도 있음. 그리고 파일구조가 달라서 import 가 안되서 생긴 에러일 수도 있음. 
 1. Question 모델 객체 생성 <br>
    위의 과정은 cmd 창에서 Mac인 경우 python3 을 입력후 파이썬 셀에 진입해서 수행함.
   
   ```tsx
        from models import Question, Answer
        from datetime import datetime
        from database import SessionLocal
        q = Question(subject='pybo가 무엇인가요?', content='pybo에 대해서 알고 싶습니다.', create_date=datetime.now()) // 데이터 생성
        db = SessionLocal() 
        db.add (q) // 추가
        db.commit() //db객체 커밋 : 커밋해야 데이터 베이스에 데이터 저장
        //Commit의 반대는 Rollback (db.rollback() 되돌리기)
        q.id() // 해당 명령어를 실행하면, 데이터가 정상적으로 생성되면 id 1 (데이터가 한개 저장되어 있는경우) 출력
   ```
2. 데이터 조회
 ```tsx
    db.query(Question).all()
   ```
  해당 명령어를 실행시키면 <br> 
`  [<models.Question object at 0x10d419510>, <models.Question object at 0x10d393580>]
`
