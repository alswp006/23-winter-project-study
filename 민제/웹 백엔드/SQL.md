- SQL은 데이터를 보다 쉽게 검색하고 추가, 삭제, 수정 같은 조작을 할 수 있도록 고안된 컴퓨터 언어이다.
- DML (Data Manipulation Language): 데이터를 조작하기 위해 사용
    - INSERT, UPDATE, DELETE, SELECT 등 → 조작어
- DDL (Data Definition Language): 데이터베이스의 스키마를 정의하거나 조작하기 위해 사용
    - CREATE, DROP, ALTER 등 → 정의어
- DCL (Data Control Language) : 데이터를 제어하는 언어
    - 권한을 관리하고, 테이터의 보안, 무결성 등을 정의합니다. GRANT, REVOKE 등 → 제어어

## 데이터베이스 생성하기

1. MySQL 관리자 계정인 root로 데이터베이스 관리 시스템에 접속

```bash
mysql-uroot -p 
```

- -uroot : user는 root
- -p : 패스워드 접속
1. 데이터베이스 생성

```bash
create database DB이름;
```

## 데이터베이스 사용자 생성과 권한 주기

- Database를 생성했다면, 해당 데이터베이스를 사용하는 계정을 생성하고 해당 계정이 데이터베이스를 이용할 수 있는 권한을 줘야 한다.

```bash
grant all privileges on db이름.* to 계정이름@'%' identified by ＇암호’;
grant all privileges on db이름.* to 계정이름@'localhost' identified by ＇암호’;
flush privileges;
```

- db이름 뒤의 * 는 모든 권한을 의미한다.
- @’%’는 어떤 클라이언트에서든 접근 가능하다는 의미이고, @’localhost’는 해당 컴퓨터에서만 접근 가능하다는 의미이다.
- flush privileges는 DBMS에게 적용을 하라는 의미이다.
- 해당 명령을 반드시 실행해줘야 한다.
- 위 첫 번째 라인을 실행하였는데 아래와 같은 오류가 발생하였습니다.

```bash
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'identified by 'connect123!@#'' at line 1
```

→ MySQL8부터는 grant로 user 생성이 불가능하다고 합니다.

- 오류 해결 코드

```bash
CREATE USER 'connectuser'@'%' IDENTIFIED BY 'connect123!@#';
	-> Query OK, 0 rows affected (0.02 sec)
GRANT ALL PRIVILEGES ON *.* TO 'connectuser'@'%' WITH GRANT OPTION;
	-> Query OK, 0 rows affected (0.01 sec)
GRANT ALL PRIVILEGES ON connectdb.* to 'connectuser'@'%' WITH GRANT OPTION;
	-> Query OK, 0 rows affected (0.00 sec)
*flush privileges;*
	-> Query OK, 0 rows affected (0.00 sec)
```

## 생성한 데이터베이스에 접속

- 원하는 데이터베이스에 접속하는 방법

```bash
mysql -h호스트명 -u데이터베이스계정명 -p 데이터베이스이름
```

## MySQL 연결 끊기

```bash
mysql> QUIT
mysql> exit
```

## MySQL 버전과 현재 날짜 구해보기

```bash
mysql> select version(), current_date;
```

- 출력

```bash
+-----------+--------------+
| version() | current_date |
+-----------+--------------+
| 8.2.0     | 2024-01-07   |
+-----------+--------------+
1 row in set (0.00 sec)
```

- 키워드는 대소문자를 구분하지 않는다.

## 테이블

- 마이크로소프트의 엑셀(Excel)을 실행하면 표가 나오고 각종 값을 저장할 수 있다.
- 데이터베이스도 엑셀의 표와 유사한 테이블을 가질 수 있다.
- 엑셀과 다른 점은 데이터베이스를 생성해도 테이블은 존재하지 않는다는 것이다.
- 테이블을 사용하려면 테이블을 생성하고 저장하는 SQL을 사용해야 합니다.

### 테이블의 구성 요소

- 테이블 : RDBMS의 기본적 저장구조, column과 row로 구성된다.
- 열(Column) : 테이블 상에서의 단일 종류의 데이터, 특정 데이터 타입 및 크기를 가지고 있다.
- 행(Row) : Column들의 값의 조합. 레코드라고도 불림. 중복을 허용하지 않는 기본키(PK)로 구분한다.
- Field : Row와 Column의 교차점으로 Field는 데이터를 포함할 수 있고 없을 때는 NULL 값을 가지고 있다.

### 쿼리문

- concat : 문자열 결합
    
    ```sql
    SELECT concat( empno, '-', deptno) AS '사번-부서번호' 
    FROM employee;
    ```
    
- distinct : 중복 제거
    
    ```sql
    select distinct deptno from employee;
    ```
    
- order by : 정렬
    
    ```sql
    select empno, name, job from employee order by name;
    ```
    
- UPPER, UCASE : 대문자 변환
    
    ```sql
    SELECT UPPER('SEoul'), UCASE('seOUL');
    ```
    
- substring : 문자열 자르기
    
    ```sql
    SELECT SUBSTRING('Happy Day', 3, 2);
    ```
    
- LPAD, RPAD : 원하는 문자열의 길이만큼 채우기
    
    ```sql
    SELECT LPAD('hi', 5, '?'), RPAD('hi', 7, '.')
    출력
    ???hi, hi.....
    ```
    
- TRIM, LTRIM, RTRIM : 공백 제거
    
    ```sql
    SELECT LTRIM(' hello '), RTRIM(' hello ');
    ```
    
- COUNT : 갯수 세기
    - COUNT(expr) : non-null인 갯수 세기
    - COUNT(DISTINCT expr, [expr…] : non-null인 중복되지 않은 갯수 세기
    - COUNT(*) : 모든 갯수 세기
- AVG, SUM, MIN, MAX
- INSERT : 데이터 입력
    
    ```sql
    INSERT INTO 테이블명(필드1, 필드2, 필드3, 필드4, … ) 
            VALUES ( 필드1의 값, 필드2의 값, 필드3의 값, 필드4의 값, … )
    ```
    
    ```sql
    insert into ROLE (role_id, description) values ( 200, 'CEO');
    ```
    
- UPDATE : 데이터 업데이트
    
    ```sql
    UPDATE  테이블명
    SET  필드1=필드1의값, 필드2=필드2의값, 필드3=필드3의값, …
    WHERE  조건식
    ```
    
    - WHERE 절을 생략하면 전체 테이블 데이터가 다 바뀜

## 데이터 정의어(Data Definition Language,DDL

### 테이블 생성

```sql
create table 테이블명( 
          필드명1 타입 [NULL | NOT NULL][DEFAULT ][AUTO_INCREMENT], 
          필드명2 타입 [NULL | NOT NULL][DEFAULT ][AUTO_INCREMENT], 
          ........... 
          PRIMARY KEY(필드명) 
          );
```

```sql
CREATE TABLE EMPLOYEE2(   
            empno      INTEGER NOT NULL PRIMARY KEY,  
           name       VARCHAR(10),   
           job        VARCHAR(9),   
           boss       INTEGER,   
           hiredate   VARCHAR(12),   
           salary     DECIMAL(7, 2),   
           comm       DECIMAL(7, 2),   
          deptno     INTEGER);
)
```

### 테이블 수정(컬럼 추가/삭제)

```sql
alter table 테이블명
          add  필드명 타입 [NULL | NOT NULL][DEFAULT ][AUTO_INCREMENT];

alter table 테이블명
         drop  필드명;
```

```sql
alter table EMPLOYEE2
				add birthdate varchar(12);

alter table EMPLOYEE2
				drop birthdate;
```

### 테이블 수정(컬럼 수정)

```sql
alter table  테이블명
		    change  필드명  새필드명 타입 [NULL | NOT NULL][DEFAULT ][AUTO_INCREMENT];
```

```sql
alter table EMPLOYEE2
				change deptno dept_no int(11);
```

### 테이블명 수정

```sql
alter table  테이블명 rename 변경이름
```

### 테이블 삭제

```sql
drop table 테이블이름;
```

- 제약 조건이 있을 경우(테이블 내 외래키 존재 등)에는 drop table 명령으로도 테이블이 삭제되지 않을 수 있다.
- 그럴 경우는 테이블을 생성한 반대 순서로 삭제를 해야한다.
