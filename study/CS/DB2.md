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