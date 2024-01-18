# Git 초급

## **Git 실행 원리**

DVCS(분산관리 버전 시스템) = Git

1. git init: 파일 폴더(tree) 생성 (작업 영역)
2. git add: 변경된 파일을 인덱스 영역에 저장 tree가 생성되면서 하위 tree에 저장이 됨 (tree 형태로 계속해서 저장이 된다. 백업을 언제든 할 수 있는 형태로 기록됨!(최고)
3. git commit: 헤더 영역에 파일을 영구 기록 ex) 버전 1, 버전 2, 버전 3 여러가지 version들을 영구히 기록!

## Git 기본기(명령어)

SCM(형상관리): 어떠한 변경사항이 있을때 마다 추적할 수 있는 것

git init: 작업 영역 생성 

git status: 현재 파일 상태를 볼 수 있다.

git add . :  인덱스 영역에 저장 (tree가 하나 만들어 지고 ex) text1.txt가 만들어 진다)

git commit -m: 헤더 영역에 파일을 영구 기록 (실제로 인덱스 영역에 해시 값을 참조) (ex 첫번째 사진이 헤더 영역에 생긴다)

git log: 헤더에 기록된 로그들을 보여준다 (ex 첫번째 사진이 기록되어져 있음)

## Git 초기 세팅

Gitd을 설치하고 나서 가장 먼저 해야하는 것은 사용자 이름과 이메일 주소를 설정해야한다 Git은 커밋 할 때마다 이 정보를 사용한다. 한 번 커밋한 후에는 정보를 변경할 수 없다.

**초기 설정 명령어**

**git config --global [user.name](http://user.name/) "Jeong Hwan"
git config --global user.email Jeong [Hwan@naver.com](mailto:Hwan@naver.com)**
