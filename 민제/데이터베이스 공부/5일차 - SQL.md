# SQL

- 인덱싱 : 특정 요소를 더 빨리 조회하기 위해 데이터베이스가 취하는 행동
    - 빨리 찾아야 하는 것들에만 인덱싱 처리를 해야하고 너무 많은 인덱싱이 되어있으면 성능에 문제가 발생한다.

## 문법

- SELECT * FROM Customers;
    - Customer 테이블의 모든 요소 가져오기
- SELECT CustomerID, CustomerName FROM Customers;
    - Customer 테이블의 CustomerID, CustomerName 가져오기

### WHERE : 조건문

- SELECT * FROM Customers WHERE Country = 'Mexico';
    - Customer 테이블에서 Country = 'Mexico'인 요소 가져오기
    - AND, OR, NOT 등의 연산 가능

### ORDER BY : 정렬

- SELECT * FROM Customers ORDER BY CustomerName;
    - 기본 오름차순 정렬
- SELECT * FROM Customers ORDER BY CustomerName DESC;
    - 내림차순 정렬
- SELECT * FROM Customers ORDER BY Country DESC, CustomerName;
    - 우선 Country을 기준으로 내림차순 정렬하고 그 안에서 CustomerName으로 오름차순 정렬

### INSERT : 데이터 추가

```sql
INSERT INTO Categories (CategoryName, Discription)
VALUES('Computer', 'NoteBook, DeskTop');
```

- Categories 테이블의 CategoryName, Discription 열에 각각 데이터 추가
- 만약 pk가 AI값으로 지정되어 있으면 그 열은 따로 값을 넣어주지 않아도 된다. (Not Null도)

```sql
INSERT INTO Categories
VALUES(1, 'Computer', 'NoteBook, DeskTop');
```

- 테이블의 모든 열의 데이터를 추가한다면 첫 괄호 생략 가능
- 이와 같은 경우 AI로 지정된 값에 강제로 데이터를 넣어줄 수 있지만 이런 것은 데이터가 많아지면 관리가 힘들어지고 실수가 발생할 수 있기 때문에 웬만하면 사용하지 않기

### UPDATE : 데이터 수정(업데이트)

```sql
UPDATE Categories
SET Description = 'drinks, coffees, teas, beers'
WHERE CategoryID = 1;
```

- Categories테이블의 CategoryID가 1인 열의 Description을 'drinks, coffees, teas, beers'으로 변경

### DELETE : 데이터 삭제

```sql
DELETE FROM Categories;
```

- 테이블의 모든 데이터 삭제

```sql
DELETE FROM Categories WHERE CategoryID = 1;
```

- Categories테이블의 CategoryID가 1인 데이터 삭제
- 중간 데이터가 삭제되도 AI로 생성된 값이 바로 업데이트되는 것은 아님
- 사용자 화면에서 삭제가 일어난다고 실제로 바로 삭제하는 것이 아니라 사용자 화면에서만 삭제하고 그 데이터를 보관하고 싶으면 특정 컬럼을 만들어서 플래그를 만들어서 사용자 화면에 보일것인지 여부를 체크할 수 있음

### DROP TABLE : 테이블 자체를 삭제

### LIKE : 특정 패턴으로 검색

- WHERE 컬럼 1 LIKE ‘a%’ : 컬럼 1의 값이 a로 시작하는 값
- WHERE 컬럼 1 LIKE ‘%a’ : 컬럼 1의 값이 a로 끝나는 값
- WHERE 컬럼 1 LIKE ‘%a%’ : 컬럼 1의 값이 a를 포함하는 값
- WHERE 컬럼 1 LIKE ‘_a%’ : 컬럼 1의 값이 두번째 문자가 a인 값
- WHERE 컬럼 1 LIKE ‘a_%’ : 컬럼 1의 값이 a로 시작하고 문자의 길이가 2 이상인 값
- WHERE 컬럼 1 LIKE ‘a%o’ : 컬럼 1의 값이 a로 시작하고 o로 끝나는 값

```sql
SELECT * FROM Customers WHERE Country LIKE 'br%';
```

- Country컬럼에서 br로 시작하는 데이터

### IN

```sql
SELECT * FROM Customers WHERE Country IN ('Korea', 'Mexico', 'Brazil')
```

- 여러 조건이 필요한데 조건이 동적으로 바뀌는 경우
    - ex) 체크박스 : 사용자가 체크박스를 체크하면 그 내용이 IN 안으로 들어가도록 만들기
- NOT 연산 가능

### BETWEEN : 사이값 추출

```sql
SELECT * FROM Customers WHERE Price BETWEEN 20 AND 30;
```

- 20 이상 30 이하 값 추출
- NOT 연산 가능

### LIMIT : 갯수 제한

```sql
SELECT * FROM Customers ORDER BY Price LIMIT 5;
```

- price가 가장 높은 5개
    - 네이버 실시간 검색 순위 같은 곳에 사용

```sql
SELECT * FROM Customers ORDER BY Price LIMIT 10, 10;
```

- 10번 인덱스부터 10개 가져오기
- (페이지 번호 - 1) * 한 페이지에 보여주는 수, 한 페이지에 보여주는 수로 LIMIT뒤에 사용하면 잡으면 점차 늘려갈 수 있음.
    - 실무에서 많이 사용
    - 10건씩 보기, 20건씩 보기 사용 가능

### MIN(), MAX()

```sql
SELECT MIN(price) FROM Customers
```

- price의 최솟값

```sql
SELECT ProductID, MAX(price) AS Price FROM Customers
```

- 최댓값의 컬럼 가져오기

### AVG(), SUM(), COUNT()

- 각각 해당 컬럼의 평균, 합, 갯수 구하기

### GROUP BY : 같은 값을 가진 데이터들 그룹화

```sql
SELECT Country, COUNT(*) AS CountCountry FROM Customers GROUP BY Country;
```

<img width="695" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/9c63c57b-5e5b-4b7f-826c-421c9b03cc4e">

```sql
SELECT CategoryID, AVG(Price) AS PriceAverage FROM Products GROUP BY CategoryID;
```

<img width="695" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/cc4a3f42-57f2-402f-9515-75be86be8b81">

### JOIN문

<img width="695" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/1ab582ba-1c81-4564-958f-3ac55da743c7">

```sql
SELECT Products.*, Categories.CategoryName 
FROM Products INNER JOIN Categories 
ON Products.CategoryID = Categories.CategoryID;
```

- 양테이블의 카테고리 ID가 같은 값들을 가져와서 합친다.
- Inner : on으로 조건을 주어 양 테이블에서 해당 조건이 만족하는 데이터만 가져와서 합친다
- Left : 왼쪽 테이블은 모두 가져오고 on으로 조건을 주어 오른쪽 테이블에서 해당 조건이 만족하는 데이터만 가져와서 합친다
- Right : 오른쪽 테이블은 모두 가져오고 on으로 조건을 주어 왼쪽 테이블에서 해당 조건이 만족하는 데이터만 가져와서 합친다
- Cross : 양 테이블의 모든 데이터를 합친다.

### INNER JOIN 실전 활용

```sql
SELECT T1.*, T2.CategoryName FROM Products T1, Categories T2 
WHERE T1.CategoryID = T2.CategoryID;
```

- Inner join과 같은 결과

```sql
SELECT T1.*, T2.CategoryName, T3.SupplierName 
FROM Products T1, Categories T2,Suppliers T3 
WHERE T1.CategoryID = T2.CategoryID AND T1.SupplierID = T3.SupplierID;
```

- 3개의 테이블 합치기
