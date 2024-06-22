## FastAPI BASE PART

### Directory 구조 

```tsx
├── main.py

├── database.py
├── models.py
├── domain
│   ├── answer
│   ├── question
│   └── user
└── frontend
```
### Main.py 
main.py 파일에 생성한 app 객체는 FastAPI의 핵심 객체
```tsx
app = FastAPI()
```
이 객체를 통해 FastAPI의 설정을 할 수 있음. 이에 FastAPI 프로젝트의 전체적인 환경을 설정하는 파일임.

### DataBase
database.py 파일은 데이터 베이스와 관련된 설정을 하는 파일 <br>
이 파일에는 데이터 베이스를 사용하기 위한 변수, 함수들을 정의하고 접속할 데이터 베이스의 주소와 사용자, 비밀번호등을 
관리함.
### Models
Pybo 프로젝트는 ORM(object relational mapping)을 지원하는 파이썬 데이터베이스 도구인 SQLAlchemy를 사용함. <br>
**_SQL Alchemy_** : 모델 기반으로 데이터베이스 처리함.
### Domain
Pybo 프로젝트는 질문과 답변을 작성하는 게시판을 만드는것이 최종 목표임 <br>
이에 "질문","답변","사용자" 라는 총 3개의 도메인을 두어 그 하위에 관련된 파일을 작성하고자함 <br>
`도메인은 "질문" "답변" "사용자" 처럼 굵직한 요구사항 또는 문제 영역을 대표하는 말임`
그리고 각 도메인은 API를 생성하기 위해서 다음과 같은 파일들이 필요하다.

* 라우터 파일 - URL과 API의 전체적인 동작을 관리
* 데이터베이스 처리 파일 **(CRUD)**
  * 생성(Create)
  * 조회(Read)
  * 수정(Update)
  * 삭제(Delete)를 처리 
* 입출력 관리 파일 - 입력 데이터와 출력 데이터의 스펙 정의 및 검증
### Frontend
**Svelte 프레임워크를 설치한 디렉터리** :Svelte의 소스 및 빌드 파일들을 저장하기 위해 사용함
**최종적으로 frontend/dist 디렉터리에 생성된 빌드 파일들을 배포시에 사용할 것임.**

