# Git 고급

## branch

- master branch : 주 브랜치
- slave branch : 복제된 브랜치
- 브랜치 생성
    - git branch : 현재 브랜치 출력
    - git branch "브랜치 명” : “브랜치 명”의 브랜치 생성
- 주 브랜치에서 다른 분기를 만든 것이라고 생각
- 분기점을 공통 조상이라 한다.
- 브랜치를 합치는 것을 merge라고 한다.
    - git merge “복제된 브랜치 명”
- branch pointer
    - commit을 하면 main branch pointer가 그 커밋 로그를 가리킨다.
    - 새로운 브랜치가 생기면 새로운 브랜치의 포인터도 현재 커밋 로그를 가리킨다.
    - 각 브랜치의 포인터는 각 브랜치에서 수행되는 작업 로그를 가리킨다.
- fast-foward merge
    - 주 브랜치의 로그가 복제된 브랜치에 모두 포함될 때 사용되는 merge
    - main branch pointer가 현재 복제된 브랜치 포인터가 가리키는 곳으로 옮겨진다.
    - 속도가 매우 빠름!
- 3-way merge
    - 주 브랜치와 복제된 브랜치 모두 새로운 로그를 만들었을 때 사용되는 merge
    - 복제된 브랜치 포인터가 가리키는 로그가 메인 브랜치에 복제되고 메인 브랜치 포인트가 이 로그를 가리킨다. 복제된 브랜치 포인터는 변하지 않는다.
- 브랜치 이동
    - git checkout “브랜치 명” : 헤더가 해당 브랜치 포인트로 이동한다.
- Merge Conflict
    - 마스터 브랜치와 복제 브랜치가 같은 파일을 수정하여 merge하면 merge conflict이 일어날 수 있다.
    - 바뀐 두 파일 중 어떤 것을 사용할건지 결정한 후 commit해야 한다.
- rebase : 로그 정리
    - squash(찌그러뜨리다, 압축하다) : 로그를 정리할 때는 항상 윗 방향으로 압축함
    - pick : 사용할 커밋 로그
    - drop : 커밋 로그 삭제(파일도 삭제)
    - reword : 커밋 로그 이름 수정

# Github

- 깃허브 레포지토리를 생성하면 깃허브 컴퓨터에 디렉토리를 생성하고 그 곳을 연결할 수 있는 http주소가 생성된다. → 클라우드 저장소
    - git init가 되어있는 상태
- 깃허브 클라우드 저장소를 origin(리모트 저장소)이라 한다.
- git remote : 원격지를 관리하는 명령어
    - git remote add origin “깃허브 주소” : origin과 본인의 저장소 연결
- git push : 원격 저장소에 저장 (업로드 + 병합)
    - git push origin remote
- git pull : 파일 다운받기 (다운로드 + 병합)
    - git pull origin master : origin에서 데이터 당겨오기
- git clone : 모든 파일 다운로드 (git init + git remote + git pull)
- 브랜치 만들고 병합시키기
    - git fetch origin : 모든 브랜치 다운로드 → 데이터 동기화
    - git checkout -b “브랜치 명” origin/”브랜치 명” : 브랜치 생성 및 merge
        
        → git checkout -b “브랜치 명” (브랜치 생성) + git pull origin “브랜치 명”(브랜치 다운로드 및 머지)
        
- git merge —squash “브랜치 명” : 모든 커밋을 한 개로 압축한 후 병합
