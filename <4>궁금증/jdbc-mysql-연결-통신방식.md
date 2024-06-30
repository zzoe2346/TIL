# jdbc와 mysql은 어떻게 연결이 되고 어떤방식으로 서로 통신하는가?

JDBC(Java Database Connectivity)는 자바 프로그램에서 데이터베이스와 상호작용하기 위한 표준 API입니다. JDBC를 사용하여 자바 애플리케이션이 MySQL 데이터베이스와 연결되고 통신하는 방식에 대해 설명하겠습니다.

### 1. JDBC와 MySQL의 연결 과정

#### 1.1. JDBC 드라이버 로드
자바 애플리케이션에서 MySQL 데이터베이스와 연결하려면 먼저 MySQL JDBC 드라이버를 로드해야 합니다. 이는 `Class.forName` 메서드를 사용하여 수행됩니다.

```java
Class.forName("com.mysql.cj.jdbc.Driver");
```

#### 1.2. 데이터베이스 연결 설정
드라이버를 로드한 후, `DriverManager`를 사용하여 데이터베이스에 연결합니다. 이때 데이터베이스 URL, 사용자 이름 및 비밀번호가 필요합니다.

```java
Connection connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydatabase", "username", "password");
```

### 2. JDBC와 MySQL의 통신 방식

#### 2.1. SQL 쿼리 전송
연결이 설정되면 `Statement` 객체를 사용하여 SQL 쿼리를 실행할 수 있습니다.

```java
Statement statement = connection.createStatement();
ResultSet resultSet = statement.executeQuery("SELECT * FROM mytable");
```

#### 2.2. 결과 처리
쿼리가 실행되면 결과는 `ResultSet` 객체를 통해 반환됩니다. 이를 사용하여 결과를 처리합니다.

```java
while (resultSet.next()) {
    int id = resultSet.getInt("id");
    String name = resultSet.getString("name");
    // 처리 로직
}
```

### 3. 프로세스 간 통신 (Inter-process Communication)

JDBC와 MySQL이 통신하는 방식은 클라이언트-서버 모델을 따릅니다. 자바 애플리케이션과 MySQL 데이터베이스 서버는 서로 다른 프로세스에서 실행되며, **네트워크를 통해 통신**합니다. 통신 과정은 다음과 같습니다:

1. **TCP/IP 소켓을 통한 연결**: 자바 애플리케이션의 JDBC 드라이버는 TCP/IP 소켓을 사용하여 MySQL 서버에 연결합니다. 연결이 설정되면 클라이언트와 서버는 소켓을 통해 데이터 패킷을 주고받습니다.
   
2. **프로토콜 사용**: MySQL은 클라이언트-서버 프로토콜을 사용하여 쿼리를 전송하고 응답을 받습니다. JDBC 드라이버는 SQL 쿼리를 MySQL 서버가 이해할 수 있는 형식으로 변환하여 전송합니다. 서버는 쿼리를 처리한 후 결과를 클라이언트로 반환합니다.

### 4. 요약
- **JDBC 드라이버 로드**: 자바 애플리케이션은 MySQL JDBC 드라이버를 로드합니다.
- **데이터베이스 연결 설정**: `DriverManager.getConnection`을 통해 데이터베이스에 연결합니다.
- **SQL 쿼리 전송 및 결과 처리**: `Statement` 객체를 사용하여 SQL 쿼리를 실행하고, `ResultSet` 객체로 결과를 처리합니다.
- **프로세스 간 통신**: 자바 애플리케이션과 MySQL 서버는 TCP/IP 소켓을 통해 통신하며, MySQL 프로토콜을 사용하여 데이터를 주고받습니다.

이 과정을 통해 자바 애플리케이션은 MySQL 데이터베이스와 상호작용하며 필요한 데이터를 효율적으로 처리할 수 있습니다.