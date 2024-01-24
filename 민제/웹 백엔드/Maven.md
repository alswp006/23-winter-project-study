- 빌드(Build), 패키징, 문서화, 테스트와 테스트 리포팅, git, 의존성관리, svn등과 같은 형상관리서버와 연동(SCMs), 배포 등의 작업을 손쉽게 할 수 있도록 도와주는 도구

## 장점

- 편리한 의존성 라이브러리 관리
- JSTL을 학습할 때, 몇 가지 파일을 다운로드 하여 /WEB-INF/lib폴더에 복사하여 사용했었는데 관련된 라이브러리가 많아질수록 이러한 방식은 불편해진다. Maven을 사용하면 설정 파일에 몇 줄 적어줌으로써 직접 다운로드 받거나 하는 것을 하지 않아도 라이브러리를 사용할 수 있다.
- 또한 프로젝트에 참여하는 개발자가 많아지게 되면, 프로젝트를 빌드하는 방법에 대하여 가이드하는 것도 Maven을 사용하게 되면 Maven에 설정한 대로 모든 개발자가 일관된 방식으로 빌드를 수행할 수 있게 됩니다.

## 태그

- 실습 프로젝트의 pom.xml

```java
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>demo1</artifactId>
    <version>1.0-SNAPSHOT</version>
    <name>demo1</name>
    <packaging>war</packaging>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.target>1.8</maven.compiler.target>
        <maven.compiler.source>1.8</maven.compiler.source>
        <junit.version>5.9.2</junit.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>4.0.1</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>${junit.version}</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-engine</artifactId>
            <version>${junit.version}</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>3.3.2</version>
            </plugin>
        </plugins>
    </build>
</project>
```

- **project** : pom.xml 파일의 최상위 루트 엘리먼트(Root Element)
- **modelVersion** : POM model의 버전
- **groupId** : 프로젝트를 생성하는 조직의 고유 아이디를 결정합니다. 일반적으로 도메인 이름을 거꾸로 적.
- **artifactId** : 해당 프로젝트에 의하여 생성되는 artifact의 고유 아이디, Maven을 이용하여 pom.xml을 빌드할 경우 “artifactid-version.packaging”과 같은 규칙으로 artifact가 생성됩니다.
- **packaging** : 해당 프로젝트를 어떤 형태로 packaging 할 것인지 결정한다. (jar, war, ear 등등)
- **version** : 프로젝트의 현재 버전. 프로젝트가 개발 중일 때는 SNAPSHOT을 접미사로 사용한다. Maven의 버전 관리 기능은 라이브러리 관리를 편하게 한다.
- **name** : 프로젝트의 이름
- **url** : 프로젝트 사이트가 있다면 사이트 URL을 등록하는 것이 가능하다.
- **properties** : 중복 설정을 제거하기 위해 모아서 설정
- **dependencies** : 의존 관계 중복을 제거하기 위해 의존 관계를 모아서 설정
