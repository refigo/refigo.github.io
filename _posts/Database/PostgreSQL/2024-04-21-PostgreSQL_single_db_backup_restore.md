---
title: PostgreSQL 단일 데이터베이스 백업, 복원하기
date: 2024-04-21
categories: [Database, PostgreSQL]
tags: [PostgreSQL, DB Backup, DB Restore]
---

PostgreSQL로 단일 데이터베이스를 백업(Backup)하고 복원(Restore)하는 방법에 대해서 알아보자.

## 백업(Backup)

단일 데이터베이스를 백업할 때 `pg_dump`를 이용할 수 있다.

명령어는 다음과 같다.

```bash
pg_dump -U username dbname > dbname_backup.sql
```

- `-U usearname`: 해당 데이터베이스를 백업할 PostgreSQL 유저

`pg_dump`로 백업할 데이터베이스의 데이터를 다시 만들어주기 위해(recreate) 필요한 SQL 명령어들(commands)이 담긴 SQL Script를 만든다.

즉, 생성된 SQL Script가 덤프 백업 파일이 되는 것이다.

### postgres 계정 접속 후 백업

만약, `postgres` 계정으로 접속해서 `pg_dump`를 이용한다면 아래와 같이 `-U` 옵션을 넣지 않고도 가능하다.

- postgres 계정으로 접속

```bash
sudo su postgres
```

- `pg_dump`를 이용해서 SQL script 생성

```bash
pg_dump dbname > dbname_backup.sql
```

## 복원(Restore)

`pg_dump`를 이용해서 만든 덤프 백업 파일인 SQL Script가 있다면 `psql` 명령어로 복원이 가능하다.

명령어는 다음과 같다.

```bash
psql -U username -d dbname -f backupfile.sql
```

- `-U usearname`: 명령어들을 실행할 PostgreSQL 유저
- `-d dbname`: 명령어들이 실행될 데이터베이스
- `-f backupfile.sql`: SQL 명령어들이 담긴 파일

`psql`를 이용하면 PostgreSQL 데이터베이스에 접근이 가능하지만 SQL 명령어를 실행하고 바로 종료하도록 할 수 있다. `-f`옵션을 이용하면 특정 파일의 SQL 명령어들을 실행하는 것도 가능하다.

`pg_dump`로 만든 SQL Script는 백업 당시 데이터베이스의 데이터들을 Recreate하는 SQL 명령어들이 적혀있으므로 해당 파일을 넘겨주면 복원이 가능하다.

### 새 데이터베이스 생성과 함께 복원

만약 데이터베이스를 새로 만들어야 한다면 아래와 같이 입력하자.

```bash
createdb -U username dbname
psql -U username -d dbname -f backupfile.sql
```

### postgres 계정 접속 후 복원

`postgres` 계정으로 접속해서 `psql`를 이용한다면 아래와 같이 `-U` 옵션을 넣지 않고도 가능하다.

- postgres 계정으로 접속

```bash
sudo su postgres
```

- dump된 스크립트인 db.sql을 이용해서 newdb를 업데이트한다.

```bash
psql -d dbname -f backupfile.sql
```

## 특징

pg_dump(SQLDumps)의 특징은 다음과 같다.

- 장점
  - 이식성(Portable): SQL을 이해하는 다양한 SQL 데이터베이스 시스템에서 사용 가능
  - 세분화(Granular): 특정 데이터베이스, 테이블 또는 테이블의 일부를 선택적으로 백업 가능
- 단점
  - 대규모 데이터베이스에 적합하지 않음
- 중립
  - Index 정보는 백업하지 않음

### 장점

#### 이식성(Portable)

pg_dump를 이용하면 백업 SQL Script를 생성하기 때문에 SQL문을 이해하는 다양한 DBMS에 적용하여 백업이 가능하다.

#### 세분화(Granular)

pg_dump의 여러 기능을 이용하면 사용자 입맛에 맞게 커스텀하여 백업이 가능하다.

### 단점

#### 대규모 데이터베이스에 적합하지 않음

다만, 전체 데이터베이스 데이터가 처음부터 다시 작성되기 때문에 복원 시간이 늘어난다.

또한 PostgreSQL 작동을 멈추지 않고 복원이 가능한 것이 장점이 될 수 있으나 복원 중에 해당 데이터베이스에 작업이 일어나는 경우 경합이 발생할 수 있고 이로 인해 성능이 저하될 수 있다.

그러므로 대규모 데이터베이스를 백업하고 복원하는데 적합하지 않다.

### 중립: Index 정보 백업하지 않는 것의 장단점

추가적으로 Index 정보는 백업하지 않기 때문에 사이즈가 작아지는 것이 장점이 된다.

하지만 다시 Index 정보를 설정해줘야 하는 부분은 단점이 될 수 있다.

## Reference

- [pg_dump](https://www.postgresql.org/docs/current/app-pgdump.html)
- [psql](https://www.postgresql.org/docs/current/app-psql.html)
- [PostgreSQL Backups](https://www.highgo.ca/2020/09/03/postgresql-backups/)
