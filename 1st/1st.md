###  FastAPI 개발 Preparation 

## 초기 셋팅

1. 파이썬 설치 후 (python3 -V) 파이썬 버전 출력하여 설치 확인하기
2. 파이썬 가상 환경 <br>

+ 가상 환경 디렉터리 생성하기
```tsx
mkdir DirectoryName
cd DirectoryName
pwd
c:\Users\사용자이름\DirectoryName
```
+ 가상 환경 만들기
  파이썬 가상 환경을 만들어 주는 명령어
```tsx
python -m venv myapi
```
+ 가상 환경에 진입하기
  가상 환경에 진입하기 위해서면, myapi 가상 환경에 있는 Scripts Directory의 activate 라는 명령어를 사용해야함. <br>
  아래의 명령을 입력해 myapi 가상 환경에 진입. <br>
  맥인 경우, myapi 의 하위 디렉토리인 bin 에 접근하여 가상환경에 진입할 수 있음. 
```tsx
  cd myapi
  cd bin
  source activate
```
진입 하고 나면 이렇게 뜸. 
```tsx
  (myapi) -> bin
```
현재 진입한 가상 환경에서 벗어나고자 하면
```ts```

가상 환경에 진입했다는 것은 해당 환경 내에서 Python과 관련 라이브러리들의 독립적인 관리를 가능하게 하는 것이지, 작업 디렉토리의 위치를 변경하는 것은 아님. <br>
따라서, 가상 환경에 진입하기 전과 후에 pwd 명령어를 사용하여 현재 위치를 확인하면, 둘 다 동일한 경로를 나타낼 것임.<br>
## FastAPI 설치
myapi 가상환경에 진입하여, FastAPI 설치함. <br> 
꼭 가상환경에서 FastAPI 설치할 필요는 없음. 다만, 많은 프로젝트를 하게되면 해야하는 프로젝트에 따라 FastAPI 버전이 다르게 필요할 수 있기에<br>
가상 환경을 사용하면 유용해서 myapi 가상환경에 진입하여 진행함.
+ 가상 환경에서 FastAPI 설치
```tsx
   pip install fastapi
   pip list // 설치 확인
```

