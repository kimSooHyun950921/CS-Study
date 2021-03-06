**DB2**
[DB](https://gyoogle.dev/blog/computer-science/data-base/Anomaly.html)


# KEY & JOIN (수현)
### 1. 조인이란 무엇인가요?

```
두개이상의 테이블이나 데이터를 검색하는 방법을 말합니다.
```
### 2. 크로스 조인은 왜쓸까요?
```
결과의 모든 행의 조합을 만들고싶을때.
모든 행의 조합을 만들고싶을때 크로스 조인을 씀
https://www.essentialsql.com/sql-cross-join/
```
### 3. 수퍼키, 기본키 (대체키, 후보키)에 대해서 설명하고 이들의 포함환계를 설명해주세요
```
수퍼키: 릴레이션 내에서 튜플을 고유하게 식별하는 애트리뷰트의 집합
후보키:각 튜플을 고유하게 식별하는 최손의 애트리뷰트의 모임
기본키: 후보키가 두개있으면 이들중 하나를 기본키로 설정
대리키: 인위적으로 추가된 기본키
대체키: 기본키로 설정되지 않은 후보키
외래키: 어떤 릴레이션의 키를 참조하는 애트리뷰트
수퍼키 > (대체키|기본키)
```

# SQL 인젝션과 noSQL
## 1. SQL 인젝션 공격법 2가지와 방어법 3가지
```
우회
1) 인증 우회
2) 데이터 노출

방어
1) 인풋에 포함된 특수문자 검사
2) SQL 서버 오류 발생시 에러 메세지 감추기
3) preparestatement 사용
```

## 2. noSQL에 대해 설명해주세요
```
비관계형 디비 여러 형태로 저장
```

#  Anomaly(이상 현상)

### 1-1) **이상 현상이 무엇인지 설명해주세요**
```
이상 현상은 테이블 내의 데이터들이 불필요하게 중복될 경우, 테이블을 조작할 때 발생하는 데이터 불일치 현상입니다.
```
### 1-2) **갱신 이상이 어떤 상황에서 발생하는지 설명해주세요**
```
반복된 데이터 중 일부를 갱신 할 때 발생합니다.
```
### 1-3) **삽입 이상이 어떤 상황에서 발생하는지 설명해주세요**
```
내가 원하는 값만 테이블에 삽입하고 싶은데, 테이블에 필요하지 않은 필드들 때문에 원치 않는 필드의 값도 삽입해야 하는 경우에 발생합니다.
```

# Index

### 1-1) **Index를 사용하지 않을 경우와 사용할 경우, MYI파일이 어떻게 활용되는지 설명해주세요**
```
Index를 사용하지 않을 경우에는 MYI파일은 비어져 있습니다. 반면에, Index를 사용하는 경우에는 MYI파일이 생성됩니다.
생성된 MYI파일은 사용자가 Select 쿼리로 Index를 사용하는 Column을 탐색할 때, MYI 파일의 내용을 검색하는 방식으로 활용됩니다.
```

# 정규화, 트랜잭션, 트랜잭션 격리수준 (지안)

## 1) 정규화가 무엇이며 정규화 단계에 대해 말해주세요.
```
 → 정규화란 데이터의 중복을 없애면서 불필요한 데이터를 최소화시키는 과정입니다.

제 1 정규화 : 테이블 컬럼이 원자값(하나의 값)을 갖도록 테이블을 분리하는 과정

제 2 정규화 : 테이블의 모든 컬럼이 완전 함수적 종속을 만족하도록 하는 과정

제 3정규화 : 이행적 종속을 제거하는 과정

```

## 1-1) 정규화 장단점은 무엇인가요?
```
장점)

1. 데이터베이스 변경 시 이상 현상을 제거한다.
2. 데이터베이스 구조 확장 시 재디자인 최소화
3. 사용자에게 데이터 모델을 더욱 의미있게 제공

단점)

테이블의 수가 많아져서 JOIN 연산등으로 인해 질의에 대한 응답시간이 늦어질 수도 있다. (성능저하의 가능성)
```
출처: [https://asfirstalways.tistory.com/341](https://asfirstalways.tistory.com/341)

## 2) 트랜잭션이 무엇이며 트랜잭션의 특징에 대해 말해주세요
```
→ 데이터베이스의 상태를 변화시키기 위해 수행하는 작업 단위

특징)

1. 원자성 : 트랜잭션이 DB에 모두 반영되거나, 혹은 전혀 반영되지 않아야 한다.
2. 일관성: 트랜잭션의 작업 처리 결과는 항상 일관성 있어야 한다.
3. 독립성: 둘 이상의 트랜잭션이 동시에 병행 실행되고 있을 때, 어떤 트랜잭션도 다른 트랜잭션 연산에 끼어들 수 없다.
4. 지속성: 트랜잭션이 성공적으로 완료되었으면, 결과는 영구적으로 반영되어야 한다.
```

## 2-1) 트랜잭션을 병행으로 처리 (동시성 제어) 할 때 발생할 수 있는 문제를 설명하세요.
```
1. 갱신 내용 손실 : 동시에 하나의 데이터가 갱신될 때 하나의 갱신이 누락되는 경우
2. 현황 파악 오류 : 하나의 데이터 갱신이 끝나지 않은 시점에서 다른 트랜잭션이 해당 데이터를 조회하는 경우
3. 모순성 : 두 트랜잭션이 동시에 실행될 때 데이터베이스가 일관성이 없는 모순된 상태로 남는 문제
4. 연쇄 복귀 : 두 트랜잭션이 하나의 레코드를 갱신할 때 하나의 트랜잭션이 롤백하면 다른 하나의 트랜잭션 마저 롤백이 되는 문제
```
```
## 2-2) 트랜잭션을 병행으로 처리할 때 발생하는 문제점들을 방지하기 위한 방법을 설명하세요.**

→ 로킹 제어 기법을 사용한다.

어떤 트랜잭션이 특정 DB의 데이터를 사용할 때 DB의 일정부분을 Lock시키고 트랜잭션이 완료될때 해당부분을 Unlock시키는 방법이다. 종류는 크게 두가지가 있는데 공유 로킹은 Lock한 부분을 읽기는 가능하지만 쓰기는 불가능한 것이고 배타 로킹은 읽기,쓰기 둘다 불가능하게 한 것이다.
```

추가 출처: [https://yubh1017.tistory.com/56](https://yubh1017.tistory.com/56)

## 3) 트랜잭션 격리 수준이 무엇이며 종류에 대해 설명해주세요.
```
→ 트랜잭션에서 일관성 없는 데이터를 허용하도록 하는 수준

 Read Uncommitted (레벨 0)
: 어떤 트랜잭션이 특정 테이블을 잡고 있더라도 다른 트랜잭션에서 조회가 가능

Read Committed (레벨 1)
: 어떤 트랜잭션의 작업이 완료된 후 COMMIT이 되어야만 다른 트랜잭션에서 조회가 가능

Repeatable Read (레벨2)
: 반복해서 읽기 작업을 수행하더라도 일관성 있는 데이터 읽기를 보장

Serializable (레벨 3)
:  쓰기 작업 뿐만 아니라 읽기 작업에도 LOCK 을 설정하는 격리 수준
```

## 3-1) DB별 default isolation 을 말해주세요.
```
MSSQL : READ COMMITTED
MYSQL : REPEATABLE READ
ORACLE : READ COMMITTED
```

[https://ybdeveloper.tistory.com/69](https://ybdeveloper.tistory.com/69)
[https://snow-line.tistory.com/145](https://snow-line.tistory.com/145)
