# DDL(Data Definition Language)

데이터베이스의 구조와 스키마를 정의하거나 변경하는데 사용되는 SQL 명령어 집합

주로 테이블, 뷰, 인덱스, 스키마 등 데이터베이스 객체를 생성, 변경, 삭제하는 작업을 수행함

## 주요 명령어

### 1. CREATE

데이터베이스 객체를 새로 생성할 때 사용됨

- #### 테이블 생성

    ```sql
    CREATE TABLE users (
        id INT PRIMARY KEY
        name VARCHAR(50) NOT NULL,
        email VARCHAR(100),
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    );
    ```
    * `id`: 기본키로 지정(PRIMARY KEY)

    * `name`: 문자열 값, 반드시 값이 입력되어야 함(NOT NULL)

    * `create_at`: 기본값으로 현재 시간 설정

- #### 데이터베이스 생성

    ```sql
    CREATE DATABASE my_database;
    ```

    * `my_database`라는 데이터베이스 생성

- #### 뷰(View) 생성

    테이블의 특정 데이터를 조회하기 위해 사용되는 가상 테이블

    ```sql
    CREATE VIEW active_users AS
    SELECT id, name, email
    FROM users
    WHERE active = TRUE;
    ```

### 2. ALTER

기존 데이터베이스 객체를 수정할 때 사용됨

- #### 테이블에 컬럼 추가

    ```sql
    ALTER TABLE users
    ADD age INT;
    ```
    * users 테이블에 age 추가

- #### 컬럼 이름 변경

    ```sql
    ALTER TABLE users
    RENAME COLUMN age TO user_age;
    ```

    * `users` 테이블의 `age`를 `user_age`로 변경

- #### 컬럼 데이터 타입 변경

    ```sql
    ALTER TABLE users
    MODIFY user_age SMALLINT;
    ```

    * `users` 테이블의 `user_age` 데이터 타입을 `SMALLINT`로 변경

- #### 테이블 이름 변경

    ```sql
    ALTER TABLE users
    RENAME TO customers;
    ```

    * `users` 테이블의 이름을 `customers`로 변경

### 3. DROP

데이터베이스 객체를 삭제할 때 사용

**삭제된 데이터는 복구할 수 없음**

- #### 테이블 삭제

    ```sql
    DROP TABLE users;
    ```

- #### 데이터베이스 삭제

    ```sql
    DROP DATABASE my_database;
    ```

- #### 뷰 삭제

    ```sql
    DROP VIEW active_users;
    ```

### 4. TRUNCATE

테이블의 데이터를 모두 삭제하지만 테이블 구조는 유지

`DELETE`와는 다르게 트랜잭션을 지원하지 않고, 빠르게 데이터를 제거

```sql
TRUNCATE TABLE users;
```

### 5. COMMENT

데이터베이스 객체에 주석을 추가함

- #### 테이블에 주석 추가

    ```sql
    COMMENT ON TABLE users IS '주석 내용';
    ```

- #### 컬럼에 주석 추가

    ```sql
    COMMENT ON COLUMN users.email IS '주석 내용';
    ```
## DDL 사용 예시

### 1. 테이블 생성

```sql
CREATE TABLE products (
    product_id INT AUTO_INCREMENT PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    stock INT DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 2. 테이블 수정

```sql
ALTER TABLE products
ADD COLUMN descripstion TEXT;
```

### 3. 테이블 삭제

```sql
DROP TABLE products;
```

