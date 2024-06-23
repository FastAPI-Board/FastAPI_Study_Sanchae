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

 **SQL 로 데이터 삽입을 작성**
>``insert into question (subject, content) values ('안녕하세요', '야식이 먹고 싶습니다');``
 ``insert into question (subject, content) values ('질문 있습니다', '참아야 하는것인가');
``
 ``insert into question (subject, content) values ('안녕하세요', '잠이 와요.. 커어어');
``
 
**ORM을 이용한 데이터 삽입 작성** 

>``question1 = Question(subject='안녕하세요',content='야식이 먹고 싶습니다')``
 ``question2 = Question(subject='질문 있습니다',content='참아야 하는것인가');
``
 ``question3 = Question(subject='안녕하세요',content='잠이 와요.. 커어어');
``
 ``db.add(question1, question2, question3)
``

