**Github** == (클라우드 저장소) 분산 버전관리가 가능한 저장소!!! 

**Origin(클라우드 저장소의 키워들)**: 변경 가능하지만 변경하지 말고 사용해라

## github 명령어

- **git remote add origin (http 주소)**: github와 연동
- **git remote -v, git ls-remote**: github와 연동이 되어있는지 확인’
- **git push origin master**: github에 업로드 후 병합(merge)를 한번에
- **git remote rm origin**: github와 연결되어 있는 주소를 해제
- **git pull origin master**: github에 있는 파일 다운로드 + merge
- **git clone (주소)**: git init. git remote, git pull을 한방해 준다 최고임!

## Github remote Branch

1. **git fetch origin**: origin에 모든 branch 다운로드 후
2. **git checkout -b (다른 branch명) origin/(다른 branch명)** 

다른 branch에 있는 데이터 와 origin branch와 병합 시킬 수 있다.

Log 정리

1. **git checkout master**
2. **git merge —squash (새로만든 branch)**
3. **git commit -m (남겨둘 log)**

rebase를 사용하지 않아도 log를 하나만 남겨둘 수 있다.
