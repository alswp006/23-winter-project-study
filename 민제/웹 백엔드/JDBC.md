# JDBC(Java DataBase Connectivity)

- 자바를 이용한 데이터베이스 접속과 SQL 문장의 실행, 그리고 실행 결과로 얻어진 데이터의 핸들링을 제공하는 방법과 절차에 관한 규약
- 자바 프로그램 내에서 SQL문을 실행하기 위한 자바 API
- SQL과 프로그래밍 언어의 통합 접근 중 한 형태
- JAVA는 표준 인터페이스인 JDBC API를 제공
- 데이터베이스 벤더, 또는 기타 써드파티에서는 JDBC 인터페이스를 구현한 드라이버(driver)를 제공한다.

## **JDBC를 이용한 프로그래밍 방법**

1. import java.sql.*;
2. 드라이버를 로드 한다.
3. Connection 객체를 생성한다. (DB에 접속)
    - Connection은 인터페이스이고 실제 객체는 각각의 벤더가 구현하고 있는 객체여야 한다.
    - 벤더가 제공해주는 라이브러리를 사용할 수 있게끔해주는 것이 2단계이다.
4. Statement 객체(쿼리문 생성)를 생성 및 질의 수행(쿼리문 실행)
    - Statement 또한 인터페이스이고 DB 벤더에 따라서 구현 객체가 리턴된다.
5. SQL문에 결과물이 있다면 ResultSet 객체를 생성한다.
6. 모든 객체를 닫는다

## JDBC 클래스의 상관 관계

DriverManager → Connection → Statement → ResultSet

1. DriverManager를 통해 Connection 인스턴스를 얻는다.
2. Connection을 통해 Statement를 얻는다.
3. Statement를 통해 ResultSet을 얻는다.
- **닫을 때는 열었을 때의 반대 방향으로 닫아준다.**

## JDBC 연습

- JDBC와 mysql을 사용하여 직원 정보를 담은 테이블을 사용하는 연습을 해보았습니다!

### Employee

- 직원의 고유 ID, 부서 ID, 생년월일과 getter, setter, toString 메소드를 담은 데이터 클래스

```java
public class Employee {
    private Integer empno;
    private Integer depno;
    private String birthDate;

    public Employee(){}
    public Employee(Integer empno, Integer depno, String birthDate) {
        this.empno = empno;
        this.depno = depno;
        this.birthDate = birthDate;
    }

    @Override
    public String toString() {
        return "Employee{" +
                "empno=" + empno +
                ", depno=" + depno +
                ", birthDate='" + birthDate + '\'' +
                '}';
    }

    public Integer getEmpno() {
        return empno;
    }

    public void setEmpno(Integer empno) {
        this.empno = empno;
    }

    public Integer getDepno() {
        return depno;
    }

    public void setDepno(Integer depno) {
        this.depno = depno;
    }

    public String getBirthDate() {
        return birthDate;
    }

    public void setBirthDate(String birthDate) {
        this.birthDate = birthDate;
    }
}
```

### EmployeeDao

- mysql 데이터베이스의 직원 정보를 추가, 삭제, 수정, 읽어오기 등의 동작을 수행하는 클래스

```java
public class EmployeeDao {
    private static String dburl = "jdbc:mysql://localhost:3306/example2";
    private static String dbUser = "root";
    private static String dbpasswd = "5188";

    public int addEmployee(Employee employee){
        int insertCount = 0;
        Connection conn = null;
        PreparedStatement ps = null;

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
        String sql = "INSERT INTO employee (empno, detno, birthDate) VALUES ( ?, ?, ? )";

        try{
            conn=DriverManager.getConnection(dburl,dbUser,dbpasswd);
            ps=conn.prepareStatement(sql);

            ps.setInt(1, employee.getEmpno());
            ps.setInt(2, employee.getDepno());
            ps.setString(3, employee.getBirthDate());

            insertCount = ps.executeUpdate();

        } catch (Exception ex) {
            ex.printStackTrace();
        }
        return insertCount;
    }

    public Employee getEmployee(Integer empno){
        Employee employee = null;
        Connection conn = null; //연결을 맺어내는 객체
        PreparedStatement ps = null ; //명령을 선언하는 객체
        ResultSet rs = null; //결과를 담아낼 객체

        try{
            Class.forName("com.mysql.cj.jdbc.Driver"); //드라이버 로드
            conn = DriverManager.getConnection(dburl, dbUser, dbpasswd);
            String sql = "SELECT empno, detno, birthDate FROM employee WHERE empno = ?";
            ps = conn.prepareStatement(sql);
            ps.setInt(1, empno);
            rs = ps.executeQuery(); // 실행

            if (rs.next()){
                int emp = rs.getInt(empno);
                int det = rs.getInt(2);
                String birth = rs.getString(3);

                employee = new Employee(emp, det, birth);
            }
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            if (rs != null){
                try {
                    rs.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }

            if (ps != null){
                try {
                    ps.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }

            if (conn != null){
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }

        return employee;
    }

    public List<Employee> getEmployees(){
        List<Employee> list = new ArrayList<>();

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }

        String sql = "SELECT empno, detno, birthDate FROM employee order by empno desc";
        try (Connection conn = DriverManager.getConnection(dburl, dbUser, dbpasswd);
             PreparedStatement ps = conn.prepareStatement(sql)) {

            try (ResultSet rs = ps.executeQuery()) {

                while (rs.next()) {
                    int empno = rs.getInt("empno");
                    int detno = rs.getInt(2);
                    String description = rs.getString(3);

                    Employee employee = new Employee(empno, detno, description);
                    list.add(employee); // list에 반복할때마다 Role인스턴스를 생성하여 list에 추가한다.
                }
            } catch (Exception e) {
                e.printStackTrace();
            }
        } catch (Exception ex) {
            ex.printStackTrace();
        }

        return list;
    }

    public int deleteEmployee(Integer emp_no) {
        int deleteCount = 0;

        Connection conn = null;
        PreparedStatement ps = null;

        try {
            Class.forName( "com.mysql.cj.jdbc.Driver" );

            conn = DriverManager.getConnection ( dburl, dbUser, dbpasswd );

            String sql = "DELETE FROM employee WHERE empno = ?";

            ps = conn.prepareStatement(sql);

            ps.setInt(1,  emp_no);

            deleteCount = ps.executeUpdate();

        }catch(Exception ex) {
            ex.printStackTrace();
        }finally {
            if(ps != null) {
                try {
                    ps.close();
                }catch(Exception ex) {}
            } // if

            if(conn != null) {
                try {
                    conn.close();
                }catch(Exception ex) {}
            } // if
        } // finally

        return deleteCount;
    }

    public int updateEmployee(Employee employee){
        int updateCount = 0;

        Connection conn = null;
        PreparedStatement ps = null;

        try {
            Class.forName( "com.mysql.cj.jdbc.Driver" );

            conn = DriverManager.getConnection ( dburl, dbUser, dbpasswd );

            String sql = "update employee set detno = ? where empno = ?";

            ps = conn.prepareStatement(sql);

            ps.setInt(1, employee.getDepno());
            ps.setInt(2, employee.getEmpno());

            updateCount = ps.executeUpdate();

        }catch(Exception ex) {
            ex.printStackTrace();
        }finally {
            if(ps != null) {
                try {
                    ps.close();
                }catch(Exception ex) {}
            }
            if(conn != null) {
                try {
                    conn.close();
                }catch(Exception ex) {}
            } // if
        } // finally

        return updateCount;
    }
}
```

### JDBCExamAddEmpl

- 데이터베이스에 직원 정보를 추가하는 클래스

```java
public class JDBCExamAddEmpl {
    public static void main(String[] args) {
        int empno = 4;
        int detno = 500;
        String birthDate = "1997-03-06";

        Employee employee = new Employee(empno, detno, birthDate);

        EmployeeDao employeeDao = new EmployeeDao();
        int insertCoin = employeeDao.addEmployee(employee);

        System.out.println(insertCoin);
    }
}
```

### JDBCExamDelEmpl

- 데이터베이스의 직원 정보를 삭제하는 클래스

```java
public class JDBCExamDelEmpl {
    public static void main(String[] args) {
        int empno = 4;

        EmployeeDao dao = new EmployeeDao();
        int deleteCount = dao.deleteEmployee(empno);

        System.out.println(deleteCount);
    }
}
```

### JDBCExamGetEmpl

- 데이터베이스에서 직원 정보를 가져오는 클래스

```java
public class JDBCExamGetEmpl {
    public static void main(String[] args) {
        EmployeeDao employeeDao = new EmployeeDao();
        Employee employee = employeeDao.getEmployee(1);
        System.out.println(employee);
    }
}
```

### JDBCExamGetEmpls

- 데이터베이스의 모든 직원 정보를 가져오는 클래스

```java
public class JDBCExamGetEmpls {
    public static void main(String[] args) {

        EmployeeDao dao = new EmployeeDao();

        List<Employee> list = dao.getEmployees();

        for(Employee employee : list) {
            System.out.println(employee);
        }
    }
}
```

### JDBCExamUpdateEmpl

- 데이터베이스의 직원 정보를 수정하는 클래스

```java
public class JDBCExamUpdateEmpl {
    public static void main(String[] args) {
        int empno = 3;
        int detno = 1000;
        String birthDate = "2012-01-01";

        Employee employee = new Employee(empno, detno, birthDate);

        EmployeeDao dao = new EmployeeDao();
        int updateCount = dao.updateEmployee(employee);

        System.out.println(updateCount);
    }
}
```
