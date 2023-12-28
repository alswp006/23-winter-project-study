- 실제 서비스를 개발할 때는 master, dev, topic 브랜치를 주로 사용한다.
- git merge 로그 남기기
    - git merge —no—ff “브랜치 명” : 패스트 포워드 머지 로그 남기기
    - dev 브랜치에서 merge할 때는 merge log를 남겨주는 것이 좋다.
- git tag “태그 명” : 커밋 로그에 태그 달기
    - git tag -n으로 태그 확인 가능
    - git push —tags origin main : 태그까지 푸시
- 협업할 때는 collaborator 추가 후 브랜치 보호(푸시 아무나 못하게)
    - require a pull request before merging

### 팀원 개발 절차

1. branch 생성
2. 개발하기
3. commit log 정리하기
4. 생성한 branch에 push
5. dev 브랜치에 pr 요청
6. merge되면 브랜치 삭제
7. dev 브랜치 pull
