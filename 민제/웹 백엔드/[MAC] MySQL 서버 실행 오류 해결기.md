- 터미널에서 mysql 서버를 실행하려고 아래의 코드를 입력하였습니다.

```sql
mysql.server start
```

- 하지만 발생된 오류..

```sql
Starting MySQL
./Users/minje/anaconda3/bin/mysqld_safe: line 647: /Users/minje/anaconda3/data/gimminje-ui-MacBookAir.local.err: No such file or directory
Logging to '/Users/minje/anaconda3/data/gimminje-ui-MacBookAir.local.err'.
/Users/minje/anaconda3/bin/mysqld_safe: line 144: /Users/minje/anaconda3/data/gimminje-ui-MacBookAir.local.err: No such file or directory
/Users/minje/anaconda3/bin/mysqld_safe: line 198: /Users/minje/anaconda3/data/gimminje-ui-MacBookAir.local.err: No such file or directory
/Users/minje/anaconda3/bin/mysqld_safe: line 906: /Users/minje/anaconda3/data/gimminje-ui-MacBookAir.local.err: No such file or directory
/Users/minje/anaconda3/bin/mysqld_safe: line 144: /Users/minje/anaconda3/data/gimminje-ui-MacBookAir.local.err: No such file or directory
 ERROR! The server quit without updating PID file (/Users/minje/anaconda3/data/gimminje-ui-MacBookAir.local.pid).
```

- No such file or directory가 뜨는 것을 보아 어떤 디렉토리가 없어서 발생하는 문제인 것 같습니다.
- 구글 서칭을 해보던 결과 데이터 디렉토리 초기화를 해주면 괜찮아진다는 글을 보았습니다.
- 그래서 MySQL 공식 문서의 [데이터 디렉토리 초기화](https://dev.mysql.com/doc/refman/8.0/en/data-directory-initialization.html)를 보며 초기화를 진행하였습니다.
1. 우선 터미널의 현재 위치를 MySQL 설치의 최상위 디렉토리로 변경합니다.

```sql
cd /usr/local/mysql
```

1. 시스템 `[secure_file_priv](https://dev.mysql.com/doc/refman/8.0/en/server-system-variables.html#sysvar_secure_file_priv)`변수의 값으로 위치를 지정할 수 있는 디렉터리를 만듭니다.

```bash
mkdir mysql-files
```

- 여기서 문제가 발생하였습니다.

```bash
mkdir: mysql-files: Permission denied
```

- 허가가 거부되었다라는 말인 것 같아서 “관리자 권한으로 실행해줘야겠다!”라는 생각을 하고 앞에 sudo를 붙여서 진행하였습니다.

```bash
sudo mkdir mysql-files
```

1. `mysql`사용자 및 그룹 에 디렉터리 사용자 및 그룹 소유권을 부여 `mysql` 하고 디렉터리 권한을 적절하게 설정합니다.
- 이 코드들도 관리자 권한으로 실행하였습니다.

```bash
sudo chown mysql:mysql mysql-files
sudo chmod 750 mysql-files
```

1. `mysql`사용자가 서버에 연결하는 것이 허용되는 방법을 결정하는 초기 MySQL 부여 테이블이 포함된 스키마를 포함하여 서버를 사용하여 데이터 디렉터리를 초기화합니다 .

```bash
sudo bin/mysqld --initialize --user=mysql
```

- 오류가 났습니다..

```bash
mysqld: Can't create directory '/usr/local/mysql-8.0.32-macos13-arm64/data/' (OS errno 13 - Permission denied)
2024-01-05T11:33:35.673690Z 0 [System] [MY-013169] [Server] /usr/local/mysql-8.0.32-macos13-arm64/bin/mysqld (mysqld 8.0.32) initializing of server in progress as process 8591
2024-01-05T11:33:35.677155Z 0 [ERROR] [MY-013236] [Server] The designated data directory /usr/local/mysql-8.0.32-macos13-arm64/data/ is unusable. You can remove all files that the server added to it.
2024-01-05T11:33:35.677173Z 0 [ERROR] [MY-010119] [Server] Aborting
2024-01-05T11:33:35.677684Z 0 [System] [MY-010910] [Server] /usr/local/mysql-8.0.32-macos13-arm64/bin/mysqld: Shutdown complete (mysqld 8.0.32)  MySQL Community Server - GPL.
```

- Can't create directory '/usr/local/mysql-8.0.32-macos13-arm64/data/' 오류가 발생한 것으로 보아 저 경로로 들어가서 data폴더를 지워줘야할 것 같습니다.
- 백업은 꼭 해둡시다!
- 다시 실행

```bash
sudo bin/mysqld --initialize --user=mysql
```

1. 서버 실행

```bash
mysql.server start
```

- 오류가 발생했습니다..

```bash
ERROR! MySQL server PID file could not be found!
```

- PID file이 없다는 것 같네요!
- 위에서 data 폴더를 삭제할 때 잘못 삭제한 것 같으니 mysql을 삭제하고 재설치 해보려 합니다!
