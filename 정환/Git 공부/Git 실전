**git  merge —no-ff (브랜치 이름)**: log에 merge기록을 남기면서 브랜치를 서로 merge한다

**git tag -n (태그명)**:  태그를 달기

**git push —tags origin main:** 태그 단걸 main으로 푸쉬

**git push o -f origin (브랜치 이름)**: 기존에 푸시한 커밋들을 무시하고 강제로 새롭게 푸시

**태그를 달면 개발 완료 시점을 알 수 있다.!**

**git push —delete origin (브랜치 이름)**: git hub에 branch 삭제 (github에서도 할 수 있다!!)

## 실전 시작

1. 새로운 branch 생성 ex) **git checkout -b login_topic**
2. 개발이 다되었으면 login_topic branch에 push: **git push origin login_topic**
3. 로그 지저분 하면 rebase해서 요청 해도 됨! rebase는 자기 토픽(branch)에서만 해야한다.
4. 개발 branch에 완성된 login_topic branc pr요청
5. 개발 완료된 branch 삭제: **git push —delete origin login_topic**
6. 개발 branch 동기화: 개발 branch로 checkout하고 동기화 **git pull origin dev**
