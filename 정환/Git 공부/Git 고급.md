**Branch: commit을 하게되면 main branch가 생긴다 main branch에 있는 하나의 공통조상으로 부터의 기능들을 새로운 branch에 가져올 수 있다.**

ex) main branch에 있는 기능들 중 공통 조상을 가지고 있는 새로운 기능들을 추가하여 만들어 볼 수 있음! 이때 main branch 기능들은 변하지 않음!

- **3 - way merge: 새롭게 만든 branch와 main branch를 합칠 수 있다. main branc는 새롭게 만든 branch의 기능들을 병합해서 만들어짐! 형상이 달라도 병합 가능**
- **fast-forward-merge: 같은 형상끼리 병합!**

 ****

**Branch pointer: commit에 있는 기능들은 branch pointer를 가진다. 새롭게 만든 branch의 기능들과 main branch와 병합 되고 싶으면 그 기능의 같은 branch pointer를 가르키며 병합된다.**

## Git 명령어

- **touch**: 파일을 만드는 명령어
- **git branch (branch 이름)**: 새로운 branch를 만드는 명령어
- **git checkout (branch 이름)**: branch 이동(switch) 명령어
- **git merge (branch 이름)**:  branch 병합 명령어
- **git checkout -b (branch 이름)**: checkout을 하면서 branch를 한방에 만드는 명령어

## Merge 충돌

master branch에서 수정한 기능과 새로만든 branch에서 수정한 기능이 동일한 기능일때(공통조상을 가질 때) 예를들어 로그인 기능을 서로다른 branch에서 동시에 수정후 병합할때!

병합하면 충돌이 발생 코드를(coflict) 다시 수정해서 commit해야 한다.!!

## Git rebase

git rebase란 log 를 정리 (깔끔하게)

squash: 압축하다 예를 들어 log에 있은 로그인의 여러 로그들을 하나의 로그인으로 압축 로그를 밑에서 위로 압축!! 반드시!

- **git reabase -i HEAD~( 압축할 로그 갯수)**: 로그 압축 명령어

**Branch: commit을 하게되면 main branch가 생긴다 main branch에 있는 하나의 공통조상으로 부터의 기능들을 새로운 branch에 가져올 수 있다.**

ex) main branch에 있는 기능들 중 공통 조상을 가지고 있는 새로운 기능들을 추가하여 만들어 볼 수 있음! 이때 main branch 기능들은 변하지 않음!

- **3 - way merge: 새롭게 만든 branch와 main branch를 합칠 수 있다. main branc는 새롭게 만든 branch의 기능들을 병합해서 만들어짐! 형상이 달라도 병합 가능**
- **fast-forward-merge: 같은 형상끼리 병합!**

 ****

**Branch pointer: commit에 있는 기능들은 branch pointer를 가진다. 새롭게 만든 branch의 기능들과 main branch와 병합 되고 싶으면 그 기능의 같은 branch pointer를 가르키며 병합된다.**

## Git 명령어

- **touch**: 파일을 만드는 명령어
- **git branch (branch 이름)**: 새로운 branch를 만드는 명령어
- **git checkout (branch 이름)**: branch 이동(switch) 명령어
- **git merge (branch 이름)**:  branch 병합 명령어
- **git checkout -b (branch 이름)**: checkout을 하면서 branch를 한방에 만드는 명령어

## Merge 충돌

master branch에서 수정한 기능과 새로만든 branch에서 수정한 기능이 동일한 기능일때(공통조상을 가질 때) 예를들어 로그인 기능을 서로다른 branch에서 동시에 수정후 병합할때!

병합하면 충돌이 발생 코드를(coflict) 다시 수정해서 commit해야 한다.!!

## Git rebase

git rebase란 log 를 정리 (깔끔하게)

squash: 압축하다 예를 들어 log에 있은 로그인의 여러 로그들을 하나의 로그인으로 압축 로그를 밑에서 위로 압축!! 반드시!

- **git reabase -i HEAD~( 압축할 로그 갯수)**: 로그 압축 명령어
