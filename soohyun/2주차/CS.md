1. SQL이 무엇인가요?
- 구조화된 쿼리언어의 약자(Structured Query Langauge)
- 관계형 데이터베이스에서 사용하는 쿼리언어
- 정해진 데이터 스키마에따라 데이터 베이스 테이블이 저장됨
- 관계를 통해서 연결된 여러개의 테이블에 분산된다. 
- 
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