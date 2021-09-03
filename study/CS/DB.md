**DB**
[DB](https://gyoogle.dev/blog/computer-science/data-base/Anomaly.html)

# [Anomaly,DB Index]

## 1)Anomaly 3가지를 설명해주세요. 
    불필요한 데이터를 추가해야지, 삽입할 수 있는 상황 = Insertion Anomaly
    일부만 변경하여, 데이터가 불일치 하는 모순의 문제 = Update Anomaly
    튜플 삭제로 인해 꼭 필요한 데이터까지 함께 삭제되는 문제 = Deletion Anomaly

## 2)DB Index를 사용하는 이유와 어떤 데이터 구조로 이루어져 있는지 말해주세요. 
    검색 속도를 높이기 위해서, B+ Tree

## 3)DB Index를 사용의 단점과 사용하지 않는게 좋은 경우의 예시를 주세요. 
    파일의 크기가 커진다. 
    동시 수정할 병행성이 준다.
    index의 record를 수정, 추가, 삭제가 자주 일어나면 성능이 떨어진다. 

    사용을 피해야 하는경우. 
    DML이 자주 일어나는 Column
    Data 중복도가 높은 Column


**CS 면접** **범위: 키(Key) , 조인 (Join)**

### 0 ) Key란?

→ 데이터베이스에서 조건에 만족하는 튜플을 찾거나 순서대로 정렬할 때 다른 튜플들과 구별할 수 있는 유일한 기준이 되는 Attribute(속성)
**(키 무결성)**

---
### 0-1 ) Candidate Key (후보키) 란?

→ 튜플을 유일하게 식별할 수 있는 속성들의 부분집합 

(기본키로 사용할 수 있는 속성들)

ex) <학생> 릴레이션에서는 [학번], [주민번호] 가 후보키다

<img width="704" alt="스크린샷_2021-08-26_오후_12 25 36" src="https://user-images.githubusercontent.com/38073401/130913113-0500523f-d134-4b36-b9d8-232d709388b4.png">

- 모든 릴레이션은 하나 이상의 후보키를 가져야 한다
- 2가지 조건을 만족해야 한다

1) **유일성**: Key 로 하나의 Tuple을 유일하게 식별할 수 있음
2) **최소성**: 꼭 필요한 속성으로만 구성

---

### 0-2 ) Primary Key (기본키) 란?

→ 후보키 중 선택한 Main Key

- NULL 값을 가질 수 없다 (⇒ 개체 무결성의 첫번째 조건)
- 동일한 값이 중복될 수 없다 (⇒ 개체 무결성의 두번째 조건)

    ex)  [수강] 릴레이션에는 **학번+과목명**으로 조합해야 기본키가 만들어질 수 있다. 왜냐하면 [수강] 릴레이션에서는 **학번** 속성과 **과목명** 속성은 개별적으로 기본키로 사용할 수 없다. 다른 튜플들과 구별되지 않기 때문이다. 

<img width="496" alt="스크린샷_2021-08-26_오후_1 09 30" src="https://user-images.githubusercontent.com/38073401/130912891-7540d744-fac6-4f98-bf58-e91d5f69da7c.png">

---

### 0-3 ) Alternate Key (대체키) 란?

→ 후보키가 둘 이상일 때, 기본키를 제외한 나머지 후보키들
 (=보조키)

ex) <학생> 릴레이션에서 '학번'을 기본키로 정의하면 '주민번호'는 대체키가 된다.

<img width="704" alt="스크린샷_2021-08-26_오후_12 25 36" src="https://user-images.githubusercontent.com/38073401/130913113-0500523f-d134-4b36-b9d8-232d709388b4.png">

---

### 0-4 ) Super Key (슈퍼키) 란?

→ 유일성은 만족하지만 최소성은 만족하지 못하는 키

→ 한 릴레이션내에 있는 속성들의 집합으로 구성된 키다. 
한편, A 슈퍼키로 분류된 집합이 A의 부분집합이 되는 슈퍼키로 분류된 집합이랑 다를 수 있다.

ex) <학생> 릴레이션에서 [학번], [주민번호], [학번+주민번호], [학번+주민번호+성명] 등으로 슈퍼키를 구성할 수 있다.

최소성을 만족시키지 못한다는 말은 [학번+주민번호+ 성명]이 슈퍼키인 경우, 3개의 속성 조합을 통해 다른 튜플과 구별이 가능하지만,
[성명] 단독으로 슈퍼키를 사용했을 때는 구별이 가능하지 않기에 "최소성"을 만족시키지 못한다는 것이다.

→ 뭉치면 유일성이 생기고, 흩어지면 몇몇 속성들이 독단적으로 유일성이 있는 키로 사용할 수 없다는 것이다

---

### 0-5 ) Foreign Key (외래키) 란?

→ 다른 릴레이션의 기본키를 그대로 참조하는 속성의 집합

- 외래키로 지정되면 참조 테이블의 기본키에 없는 값은 입력할 수 없다 
**(참조 무결성 조건)**

    ex)  [수강] 릴레이션이 [학생] 릴레이션을 참조하고 있으므로, [학생] 릴레이션의 **학번**은 기본키이고,  [수강] 릴레이션의 **학번**은 외래키이다.
    한편 [수강] 릴레이션의 학번에는 [학생] 릴레이션의 학번에 없는 것은 입력할 수 없다.

<img width="496" alt="스크린샷_2021-08-26_오후_1 09 30" src="https://user-images.githubusercontent.com/38073401/130913293-4437c81d-b820-4cd9-9110-79f58581013c.png">


---

### 1 ) Join 이란?

두 개 이상의 테이블이나 데이터베이스를 연결해 데이터를 검색하는 방법
적어도 하나의 컬럼을 공유하고 있어야 하므로 이를 이용해 데이터 검색에 활용된다.

---

### 1 -1 ) Inner Join 이란?

두 테이블의 교집합으로, 두 테이블간 JOIN 조건을 만족하는 행을 반환한다.

<img width="192" alt="스크린샷_2021-08-26_오후_1 21 10" src="https://user-images.githubusercontent.com/38073401/130913502-bfd46661-5b1a-4c7e-b691-c272e19263a8.png">


**1) 명시적 조인 표현**

테이블에 조인을 하라는 것을 지정하기 위해 'JOIN' 키워드를 사용하고 ON의 키워드를 조인에 대한 구문을 지정하는데 사용한다.

```sql
SELECT *
FROM EMPLOYEE 
INNER JOIN DEPARTMENT
ON EMPLOYEE.DepartmentID = DEPARTMENT.DepartmentID;
```

**2) 암시적 조인 표현**

SELECT 구문의 FROM절에서 콤마(,)를 사용하여 단순히 조인을 위한 여러 테이블을 나열한다.

```sql
SELECT *
FROM EMPLOYEE, DEPARTMENT
WHERE EMPLOYEE.DepartmentID = DEPARTMENT.DepartmentID;
```
---

### 1 -2 ) Outer Join 이란?

OUTER JOIN이란 **조인 조건에서 동일한 값이 없는 행도 반환**할 때 사용한다.

  - LEFT OUTER JOIN

    조인문의 왼쪽에 있는 테이블의 모든 결과를 가져온 후 오른쪽 테이블의 데이터를 매칭하고, 매칭되는 데이터가 없는 경우 NULL 표시

    ```sql
    SELECT *
    FROM EMPLOYEE E LEFT OUTER JOIN DEPARTMENT D 
    ON E.DEPARTMENTID = D.DEPARTMENTID;
    ```
    <img width="193" alt="스크린샷_2021-08-26_오후_1 21 59" src="https://user-images.githubusercontent.com/38073401/130913724-8039f1c2-7b26-49f0-98b8-ca5a3f3a1bc8.png">


-  RIGHT OUTER JOIN

    조인문의 오른쪽에 있는 테이블의 모든 결과를 가져온 후 왼쪽의 테이블의 데이터를 매칭하고 매칭되는 데이터가 없는 경우 NULL 표시
    
    <img width="184" alt="스크린샷_2021-08-26_오후_2 45 07" src="https://user-images.githubusercontent.com/38073401/130920229-9b4082e5-a520-431f-a0bf-fdbf93a9f9fb.png">


    ```sql
    SELECT *
    FROM EMPLOYEE E RIGHT OUTER JOIN DEPARTMENT D
    ON E.DepartmentID = D.DepartmentID;
    ```

-  FULL OUTER JOIN

    LEFT OUTER JOIN과 RIGHT OUTER JOIN을 합친 것으로, 양쪽 모두 조건이 일치하지 않는 것들까지 모두 결합하여 출력한다. 이것 역시 매칭되는 데이터가 없는 경우 NULL을 표시한다.

    ```sql
    SELECT *
    FROM EMPLOYEE E FULL OUTER JOIN DEPARTMENT D
    ON E.DepartmentID = D.DepartmentID;
    ```
---

### 1 -3 ) Cross Join 이란?

→ Cartesian Product (카디션 곱) 이라고도 하며 조인되는 두 테이블에서 곱집합을 반환한다

<img width="356" alt="스크린샷_2021-08-26_오후_2 59 52" src="https://user-images.githubusercontent.com/38073401/130920494-974a47f2-13cc-412a-8c86-7475403631a2.png">


- 특정 기준이 필요 없으므로 ON 절이 없어짐
- ex) m 열을 가진 테이블과 n 열을 가진 테이블이 교차 조인되면 m*n개의 열을 생성한다

```sql
SELECT *
FROM EMPLOYEE 
CROSS JOIN DEPARTMENT;
```
---

### 1 -4 ) Self Join 이란?

→ 자기 자신과 자기 자신을 조인하는 것으로, 하나의 테이블을 여러번 복사해서 조인한다고 생각하면 편하다. 같은 테이블을 사용하기 때문에 테이블에 반드시 별명을 붙여야 한다.

<img width="356" alt="스크린샷_2021-08-26_오후_3 02 10" src="https://user-images.githubusercontent.com/38073401/130920843-1faf80ca-299a-4d31-8534-55b9e309e114.png">

```sql
SELECT
A.NAME, B.AGE
FROM TABLE_A A, TABLE_A B
```


참고 출처: [https://jhkang-tech.tistory.com/55](https://jhkang-tech.tistory.com/55)


1. SQL이 무엇인가요?
    - 구조화된 쿼리언어의 약자(Structured Query Langauge)
    - 관계형 데이터베이스에서 사용하는 쿼리언어
    - 정해진 데이터 스키마에따라 데이터 베이스 테이블이 저장됨
    - 관계를 통해서 연결된 여러개의 테이블에 분산된다. 

2. NoSQL이 무엇일까요?
    - 정해진 스키마와 관계가 없음
    - 레코드들을 문서라고 불림
    - NoSQL에서는 다른 구조의 데이터를 같은 컬렉션에 추가할 수 있음
    - JSON과 유사한 형태를 가지고있음
3. 둘의 공통점과 차이점을 알고있나요?
    - 언어
        - SQL: 스키마가 필요함 
        - NoSQL: 정적스키마가 필요하지 않음 key-value형태로 저장됨
    - 타입
        - SQL: 관계형데이터베이스
        - NoSQL: 비관계형데이터베이스
    - 확장성
        - SQL: 수직적확장
            : RAM, CPU, SSD와 같이 DB 성능을 향상시키는 것
        - NoSQL: 수평적확장
            : 하나의 데이터베이스에서 작동하는것처럼 보이지만 여러 호스트에서 작동함, 전체적으로 분산된다.

4. 어느때 두개를 사용하면 좋을까요?
    - SQL
        - 관계를 맺고 있는 데이터가 자주 변경(수정)되는 애플리케이션일 경우 (NoSQL에서라면 여러 컬렉션을 모두 수정해줘야만 합니다.)
        - 변경될 여지가 없고, 명확한 스키마가 사용자와 데이터에게 중요한 경우
    - NoSQL
        - 정확한 데이터 구조를 알 수 없거나 변경 / 확장 될 수 있는 경우
        - 읽기(read)처리를 자주하지만, 데이터를 자주 변경(update)하지 않는 경우 (즉, 한번의 변경으로 수십 개의 문서를 업데이트 할 필요가 없는 경우)
        - 데이터베이스를 수평으로 확장해야 하는 경우 ( 즉, 막대한 양의 데이터를 다뤄야 하는 경우)
5. 인스타그램의 데이터배이스 구조는 어떻게 되어있을까요?

    - 출처:https://blog.joon-lab.com/146
    ```sql
    model User {
    id          Int       @default(autoincrement()) @id
    userName    String    @unique
    avatar      String    @default(value: "https://3.bp.blogspot.com/-qtEejOg1NHA/Xobmg2y_QeI/AAAAAAAAIVE/UFKPvpeHjKUqCEFOX8lT4MsKz-PwpEGJgCLcBGAsYHQ/s1600/default_user.png")
    email       String    @unique
    firstName   String    @default(value: "")
    lastName    String    @default(value: "")
    name        String    @default(value: "")
    bio         String    @default(value: "")
    posts       Post[]
    followers   User[]    @relation("UserFollows", references: [id])
    following   User[]    @relation("UserFollows", references: [id])
    likes       Like[]
    comments    Comment[]
    createdAt   DateTime  @default(now())
    updatedAt   DateTime  @updatedAt
    }

    model Post {
    id          Int     @default(autoincrement()) @id
    user        User    @relation(fields: [userId], references: [id])
    userId      Int
    location    String
    caption     String
    files       File[]
    comments    Comment[]
    likes       Like[]
    createdAt   DateTime  @default(now())
    updatedAt   DateTime  @updatedAt
    }

    model Like {
    id          Int       @default(autoincrement()) @id
    user        User      @relation(fields: [userId], references: [id])
    userId      Int
    post        Post      @relation(fields: [postId], references: [id])
    postId      Int
    createdAt   DateTime  @default(now())
    updatedAt   DateTime  @updatedAt
    }

    model Comment {
    id          Int       @default(autoincrement()) @id
    text        String
    user        User      @relation(fields: [userId], references: [id])
    userId      Int
    post        Post      @relation(fields: [postId], references: [id])
    postId      Int
    createdAt   DateTime  @default(now())
    updatedAt   DateTime  @updatedAt
    }

    model File {
    id          Int       @default(autoincrement()) @id
    url         String
    post        Post      @relation(fields: [postId], references: [id])
    postId      Int
    createdAt   DateTime  @default(now())
    updatedAt   DateTime  @updatedAt
    }
    ```
6. sql injection이 뭔가요? 
    - sql문에 특수문자나 추가적인 쿼리를 넣어서 데이터베이스내의 내용을 조작시키는것
7. 예방할 수 있는 방법은 뭘까요?
    - escape문자 사용하기
    - 데이터와 코드를 분리하기
    - 에러메시지 감추가ㅣ