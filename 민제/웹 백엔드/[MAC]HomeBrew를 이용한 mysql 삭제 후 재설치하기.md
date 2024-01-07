## MySQL 프로세스 종료

```bash
brew services stop mysql
```

## 관련 파일 삭제

- 먼저 설치 경로 확인해줍니다

```bash
which mysql
/usr/local/bin/mysql
```

- homebrew로 mysql을 삭제해줍니다.

```bash
brew uninstall --force mysql
```

혹은

```bash
brew uninstall mysql --ignore-dependencies
brew remove mysql
brew cleanup
```

- 다음의 코드를 입력해서 폴더 및 파일을 강제로 삭제해줍니다.

```bash
sudo rm -rf /usr/local/mysql
sudo rm -rf /usr/local/bin/mysql
sudo rm -rf /usr/local/var/mysql
sudo rm -rf /usr/local/Cellar/mysql
sudo rm -rf /usr/local/mysql*
sudo rm -rf /tmp/mysql.sock.lock
sudo rm -rf /tmp/mysqlx.sock.lock
sudo rm -rf /tmp/mysql.sock
sudo rm -rf /tmp/mysqlx.sock
sudo rm -rf /Library/StartupItems/MySQLCOM
sudo rm -rf /Library/PreferencePanes/My*

```

- 완전 삭제한 이후 컴퓨터를 재부팅해줍니다.

## mysql 재설치하기

- homebrew를 이용하여 mysql을 재설치 해줍니다.

```bash
brew install mysql

```

- mysql 서비스를 시작해줍니다.

```
brew services start mysql

```

- 비밀번호 없이 root 로그인을 합니다.

```
mysql -uroot

```

- root 비밀번호 설정합니다.

```
mysql_secure_installation

```

- Would you like to setup VALIDATE PASSWORD plugin? : 비밀번호 가이드로 비밀번호 설정을 한다면 yes, 저는 N으로 진행했습니다.
- Remove anonymous users? : 익명사용자를 삭제할지? yes하면 접속시 -u 옵션을 반드시 명시해야 합니다, 저는 N으로 진행했습니다.
- Disallow root login remotely? : localhost외 ip에서 root 아이디로 접속가능을 허락할지? yes하면 원격접속 불가능하니 no
- Remove test database and access to it? : mysql에 기본적으로 설치되는 test 디비를 삭제할지? 저는 Y로 진행했습니다.
- Reload privilege tables now? : 권한을 변경했을 경우 yes, 하나라도 권한을 변경했을 경우 Y로 선택하는 것이 정신 건강에 이롭다는 말을 듣고 Y로 진행했습니다.
