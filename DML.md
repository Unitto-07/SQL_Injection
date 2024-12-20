# DML(Data Manipulation Language)

데이터베이스에서 데이터를 조작(삽입, 수정, 삭제)하거나 검색하는데 사용되는 SQL 명령어

주로 사용자가 데이터베이스 테이블에 저장된 데이터를 다루는데 초점이 맞춰져 있음

## DML의 주요 명령어

### 1. INSERT

테이블에 새로운 데이터를 삽입

- #### 기본 문법
    
    ```sql
    INSERT INTO 테이블이름 (컬럼1, 컬럼2, ...) VALUES (값1, 값2, ...);
    ```

- #### 예제

    ```sql
    INSERT INTO users (id, name, email)
    VALUES (1, 'ALICE', 'alice@example.com');
    ```

    결과: `user`테이블에 한 행이 추가됨

- #### 여러 행 삽입

    ```sql
    INSERT INTO users(id, name, email)
    VALUES
        (2, 'Bob', 'bob@example.com'),
        (3, 'charlie', 'charlie@example.com')
    ```
### 2. UPDATE

기존 데이터를 수정함

- #### 기본 문법

    ```sql
    UPDATE 테이블이름
    SET 컬럼1 = 값1, 컬럼2 = 값2, ...
    WHERE 조건;
    ```

- #### 예제

    ```sql
    UPDATE users
    SET email = 'newalice@example.com'
    WHERE id = 1;
    ```
    결과: `id`가 1인 사용자의 이메일 주소가 수정됨

- #### 조건 없이 사용

    조건 없이 실행하면 모든 행이 업데이트 됨

    ```sql
    UPDATE users
    SET name = 'Unknown';
    ```

    결과: `users` 테이블의 모든 사용자의 `name`값이 `Unknown`으로 변경됨

### 3. DELETE

테이블에서 데이터를 삭제

- #### 기본 문법

    ```sql
    DELETE FROM 테이블이름 WHERE 조건;
    ```

- #### 예제

    ```sql
    DELETE FROM users
    WHERE id = 3;
    ```

    결과: `id`가 3인 사용자가 삭제됨

- #### 조건 없이 사용

    조건 없이 실행하면 모든 데이터가 삭제됨

    ```sql
    DELETE FROM users;
    ```

    결과: `users`테이블의 모든 데이터가 삭제되지만, 테이블 구조는 유지됨

### 4. SELECT

데이터베이스에서 데이터를 조회함

기본적으로 DQL로 분류되지만 DML로도 간주될 수 있음

- #### 기본 문법

    ```sql
    SELECT 컬럼1, 컬럼2, ... FROM 테이블이름 WHERE 조건;
    ```

- #### 모든 데이터 조회

    ```sql
    SELECT * FROM users;
    ```

    결과: `users` 테이블의 모든 데이터를 가져옴

- #### 조건부 데이터 조회

    ```sql
    SELECT name, email
    FROM users
    WHERE id = 2;
    ```

- #### 정령된 데이터 조회

    ```sql
    SELECT *
    FROM users
    ORDER BY name ASC;
    ```

## DML의 특징

### 1. 트랜잭션 지원

- DML 명령어는 트랜잭션 처리가 가능함

- 데이터 변경 작업을 묶어서 처리하고, 오류 발생 시 변경 사항 롤백할 수 있음

- 관련 명령어:
    * `COMMIT`: 변경 사항 저장
    * `ROLLBACK`: 변경 사항 취소
  

    #### 예제:

    ```sql
    BEGIN;
    UPDATE users SET email = 'test@example.com' WHERE id = 1;
    ROLLBACK;
    ```

### 2. 데이터 중심 작업

- DML은 데이터베이스의 **내용**을 변경하거나 조회하는데 사용됨
- 데이터베이스 구조를 다루는 DDL과는 구분됨

### 3. 영향 범위

- `WHERE` 조건을 지정하지 않으면 모든 행이 영향을 받을 수 있으므로 주의가 필요함

## 예제 테이블

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL,
    age INT
);
```

### 초기 데이터 삽입

```sql
INSERT INTO users (id, name, email, age)
VALUES
    (1, 'Alice', 'alice@example.com', 25),
    (2, 'Bob', 'bob@example.com', 30),
    (3, 'Charlie', 'charlie@example.com', 35);
```

### 예제 데이터 조작

1. **UPDATE**
   
   ```sql
   UPDATE users
   SET age = 40
   WHERE name = 'Charlie';
   ```

2. **DELETE**

    ```sql
    DELETE FROM users
    WHERE id = 2;
    ```

3. **SELECT**

    ```sql
    SELECT *
    FROM users
    WHERE age > 25;
    ```

