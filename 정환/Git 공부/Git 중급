## Git reset

reset(되돌리기) 에는 3가지 옵션이 있다.

1. Soft: 헤더 영역에 있는 파일들을 날림 (커밋 로그 변경시 사용!)
    
    git reset —soft (해시값 4자리)
    
2. Mixed: 헤더 영역, 인덱스 영역에 잇는 파일들을 모두 날림 (작업영역에 파일은 아직 있고 add는 하지 않은 상태) 작업 영역의 내용 변경이 필요할 때  잘 안씀 내용변경해서 새로 만드는게 낫다!!
    
    git reset —mixed(해시값 4자리) 
    

1. Hard:  작업 영역, 인덱스 영역, 헤더 영역에 있는 파일들 모두 다 날림 ( 처음 상태로 되돌아 갈때) 복구할 방법이 없어서 조심해야한다!! 잘 써야함
    
    git reset —hard(해시값 4자리)
    

## Git reflog

reflog에는 한번이라도 commit했던 파일들의 로그가 다 남아있다.!

1. git reflog: commit했던 파일들의 로그기록을 볼 수 있게 해준다.
2. git reset —hard(기록된 해시값):  다시 되돌아 갈 수 있음 삭제를 했더라도!!

## Git amend

최종 커밋 로그를 바꿀때 사용한다 amend는 커밋 로그가 하나밖에 없을때 amend를 사용해야한다.!

1. git commit —amend -m “제목”
