## git 실행 원리

- git은 분산 버전 관리 시스템(DVCS)
- git에는 작업 영역이 있다. → git init
    - 이 작업 영역은 변경 감지를 한다. 가령 텍스트나 폴더가 새로 생기면 이를 감지한다.
    - 이 변경을 기록할 것인지 개발자가 결정한다.
    - 이 변경(BLOB 객체)은 인덱스 영역에 트리(디렉토리) 구조로 저장된다. → git add
    - 이를 영구적으로 저장하고 싶으면 Header 영역에 넣는다.
        - 인덱스 영역의 트리를 그대로 가져와 영구히 기록한다. → git commit
        - 이는 버전 1과 같은 형태로 저장된다.
    - 새로운 변경을 저장하면 이는 버전 2의 형태로 저장된다.
    - 기존 파일의 내용을 변경하고 저장하면 새로운 디렉토리가 만들어지고 그 안에 위에서의 변경내용이 함께 저장된다.
- 버전을 복구하기가 용이하다는 장점이 있다.
    - history가 다 남아있기 때문에 모두 완전 복구가 가능하다.
- 인덱스 영역도 따로 복제가 되어 백업된다.

## 실습

### 명령어

- git init : 작업 영역을 현재 디렉토리로 설정 (.git 폴더 생성)
- git status : 상태 확인
- git add . : 변경된 모든 파일 추가 → tracked
- git commit -m “메시지” :
- git config —list : 깃 설정들을 리스트로 보여준다.
- git log : git의 로그들을 보여준다.
- git reset : git의 로그를 복구한다.
    - soft : commit 로그만 날린다. → header만 변경
        - 커밋 로그만 바꿈
        - git reset —soft “해시코드 4자리”
    - mixed : 인덱스 영역과 commit 로그만 날린다. → add하기 전 상태로 돌린다.
        - 작업 영역의 내용 변경이 필요
        - git reset —mixed “해시코드 4자리”
        - 웬만하면 mixed보다 add→commit을 하고 버전 2를 만들어주는 것이 낫다.
    - hard : 모든 파일을 날린다.
        - 이전 상태로 돌아가기를 원함
        - git reset —hard “해시코드 4자리”
- git reflog : 모든 ref의 로그를 보여준다. (해시코드 포함)
    - reset한 곳으로 돌아가고싶으면 reflog를 사용하여 다시 reset —hard하여 돌아간다.
- git amend : 최종 커밋 로그 변경
    - git commit —amend -m “~”
    - == git reset —soft “이전 해시코드 4자리” → git commit -m “~”
- git rebase : commit로그 합치기
    - git rebase -i HEAD~3
        - vi 에디터 : i로 입력 모드로 들어가서 로그를 변경하고 esc로 :wq(저장 후 빠져나감)

### 상태

- untracked file : 변경 감지된 파일
- modified : 수정
- .git/refs/heads/master.txt는 header가 가리키는 commit 파일의 해시값을 가진다.
