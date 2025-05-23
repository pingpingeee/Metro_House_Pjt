# Metro_House_Pjt

  <img src="https://img.shields.io/badge/java-007396?style=for-the-badge&logo=java&logoColor=white"> 
  <img src="https://img.shields.io/badge/oracle-F80000?style=for-the-badge&logo=oracle&logoColor=white"> 
  <img src="https://img.shields.io/badge/spring-6DB33F?style=for-the-badge&logo=spring&logoColor=white"> 

## 📦 개발 환경 구조 요약

| 구분 | 내용
|-----|-----
| **개발 언어** | Java (JDK 8 이상), JavaScript
| **프레임워크** | Spring Boot + MyBatis
| **DB** | Oracle 11g 이상
| **빌드 도구** | Gradle
| **내장 WAS** | Spring Boot 내장 Tomcat
| **형상관리** | Git / GitHub
| **협업 도구** | Jira, Notion


## 기술 스택 (Tech Stack)

### 🌐 프론트엔드 (Frontend)

| 기술 | 설명
|-----|-----
| JSP | 서버 측에서 HTML을 생성하는 렌더링 기술<br>동적인 웹 페이지 구현에 사용
| js/jQuery | 클라이언트 측에 필요한 동작처리, 동적 콘텐츠 로딩<br>AJAX를 통한 비동기 통신으로 좋아요 기능 구현
| CSS | 반응형 디자인 구현, 게시판 및 상세 페이지 스타일링 <br>좋아요 버튼 애니메이션 및 상태 표시 효과
| Font Awesome | 아이콘 라이브러리를 활용한 UI 개선<br>좋아요, 조회수 등 아이콘 강화
| Bootstrap | 반응형 UI 컴포넌트 활용


### ⚙️ 백엔드 (Backend)

| 기술 | 설명
|-----|-----
| Spring Boot | 자동 설정과 내장 서버를 통한 빠른 개발 환경 구축<br>Spring MVC 기반 RESTful API 구현
| Spring MVC | 컨트롤러, 서비스 계층의 구현을 위해 사용<br>표준 MVC 패턴 기반으로 구조화
| MyBatis | SQL과 서버 객체간 매핑담당 도구<br>좋아요 기능 구현을 위한 쿼리 매핑
| Oracle | 대규모 데이터 관리를 위한 관계형 데이터베이스 사용<br>게시글, 댓글, 좋아요 정보 저장
| Spring Security | 사용자 인증 및 권한 관리 (선택적)


### 🛠️ 개발 도구 (Development Tools)

| 도구 | 사용 목적
|-----|-----
| Visual Studio Code | JS, CSS, 프론트 등 코드 작성용 에디터
| IntelliJ IDEA/STS | Spring Boot 기반 프로젝트 개발 환경
| Jira | 이슈 관리 및 구체적인 일정 계획 수립을 위한 협업 도구
| GitHub | 코드 버전 관리 및 팀 협업
| Postman | API 테스트


<details>
  <summary>게시글 더미값 삽입</summary>
  <pre><code>
BEGIN
  FOR i IN 1..300 LOOP
    INSERT INTO board (boardNumber, userName, boardTitle, boardContent, boardWriteDate, boardViews)
    VALUES (i, '사용자'||i, '제목'||i, '내용'||i, SYSDATE, 0);
    
    IF MOD(i, 100) = 0 THEN
      COMMIT;
    END IF;
  END LOOP;
  COMMIT;
END;
  </code></pre>
</details>


<details>
  <summary>쿼리(2025-04-27)</summary>
  <pre><code>
GRANT CREATE SESSION, CREATE TABLE, CREATE VIEW, CREATE SEQUENCE, 
      CREATE SYNONYM, CREATE PROCEDURE, CREATE TRIGGER, CREATE MATERIALIZED VIEW 
TO METRO_HOUSE;
GRANT SELECT ANY TABLE, INSERT ANY TABLE, UPDATE ANY TABLE, DELETE ANY TABLE
TO METRO_HOUSE;
ALTER USER METRO_HOUSE DEFAULT TABLESPACE USERS;
ALTER USER METRO_HOUSE QUOTA UNLIMITED ON USERS;


CREATE TABLE USERINFO (
userNumber      NUMBER PRIMARY KEY,
userId          VARCHAR2(100),
userPw          VARCHAR2(100),
userName        VARCHAR2(100),
userTel         VARCHAR2(20),
userEmail       VARCHAR2(200),
userBirth       VARCHAR2(50),
userZipCode     VARCHAR2(50),
userAddress     VARCHAR2(300),
userDetailAddress VARCHAR2(500),
userAdmin       NUMBER DEFAULT 0,
userRegdate     DATE DEFAULT SYSDATE
);


CREATE TABLE BOARD (
boardNumber     NUMBER PRIMARY KEY,
userNumber      NUMBER,
userName        VARCHAR2(50),
boardTitle      VARCHAR2(1000),
boardContent    VARCHAR2(4000),
boardWriteDate  DATE DEFAULT SYSDATE,
boardHit        NUMBER DEFAULT 0,
boardViews      NUMBER DEFAULT 0,
boardLikes      NUMBER DEFAULT 0,
FOREIGN KEY (userNumber) REFERENCES USERINFO(userNumber)ON DELETE CASCADE
);


CREATE TABLE board_likes (
boardNumber number,
userNumber number,
PRIMARY KEY (boardNumber, userNumber)
);


CREATE TABLE BOARD_COMMENT (
commentNumber       NUMBER PRIMARY KEY,
commentSubNumber    NUMBER,
commentSubStepNumber NUMBER,
boardNumber         NUMBER,
userNumber          NUMBER,
userName            VARCHAR2(50),
commentContent      VARCHAR2(4000),
commentWriteDate    DATE DEFAULT SYSDATE
);


ALTER TABLE BOARD_COMMENT
ADD CONSTRAINT fk_comment_board
FOREIGN KEY (boardNumber)
REFERENCES BOARD(boardNumber)
ON DELETE CASCADE;


ALTER TABLE BOARD_COMMENT
ADD CONSTRAINT fk_comment_user
FOREIGN KEY (userNumber)
REFERENCES USERINFO(userNumber)
ON DELETE CASCADE;
DESC board_comment;


create table apartmentinfo(
    apartmentId number primary key,
    sggcd VARCHAR2(10),
    umdnm VARCHAR2(100),
    aptnm VARCHAR2(200),
    jibun VARCHAR2(100),
    excluusear VARCHAR2(50),
    dealYear VARCHAR2(4),
    dealMonth VARCHAR2(2),
    dealDay VARCHAR2(2),
    dealAmount VARCHAR2(100),
    floor VARCHAR2(10),
    buildYear VARCHAR2(4),
    cdealType VARCHAR2(50),
    cdealDay VARCHAR2(50),
    dealingGbn VARCHAR2(50),
    estateAgentSggnm VARCHAR2(100),
    rgstDate VARCHAR2(50),
    aptDong VARCHAR2(50),
    slerGbn VARCHAR2(50),
    buyerGbn VARCHAR2(50),
    landLeaseHoldGbn VARCHAR2(50),
    aptSeq VARCHAR2(50),
    bonbun VARCHAR2(50),
    bubun VARCHAR2(50),
    landCd VARCHAR2(50),
    roadNm VARCHAR2(200),
    roadNmBonbun VARCHAR2(50),
    roadNmBubun VARCHAR2(50),
    roadNmCd VARCHAR2(50),
    roadNmSeq VARCHAR2(50),
    roadNmSggcd VARCHAR2(50),
    roadNmBcd VARCHAR2(50),
    umdcd VARCHAR2(50),
    lat NUMBER(12,8),
    lng NUMBER(12,8),
    subwayStation VARCHAR2(100),
    subwayDistance VARCHAR2(50)
);

-- 위도/경도에 복합 인덱스 생성
CREATE INDEX idx_apartmentinfo_latlng ON APARTMENTINFO(lat, lng);


CREATE SEQUENCE seq_apartmentinfo
    START WITH 1
    INCREMENT BY 1
    NOCACHE
    NOCYCLE;
create table apartment_favorite(
    favoriteId number primary key,
    apartmentId number,
    userNumber number,
    createdAt date default sysdate,

    FOREIGN KEY (apartmentId) REFERENCES APARTMENTINFO(apartmentId)ON DELETE CASCADE,
    FOREIGN KEY (userNumber) REFERENCES USERINFO(userNumber)ON DELETE CASCADE
);
CREATE SEQUENCE seq_apartment_favorite
START WITH 1
INCREMENT BY 1
NOCACHE
NOCYCLE;

create table apartment_review(
REVIEWID NUMBER PRIMARY KEY,                -- 리뷰 고유 ID (시퀀스 사용)
apartmentId NUMBER NOT NULL,                 -- 도서 번호 (외래키) - 실제 타입으로 수정 필요
USERNUMBER NUMBER NOT NULL,                 -- 사용자 ID (외래키) - VARCHAR2(50)에서 NUMBER로 수정
REVIEWTITLE VARCHAR2(200) NOT NULL,         -- 리뷰 제목
REVIEWCONTENT CLOB NOT NULL,                -- 리뷰 내용 (긴 텍스트)
REVIEWRATING NUMBER(1) NOT NULL,            -- 평점 (1-5)
REVIEWDATE DATE DEFAULT SYSDATE,            -- 작성일
REVIEWMODIFIED_DATE DATE,                   -- 수정일
REVIEWSTATUS VARCHAR2(10) DEFAULT 'ACTIVE',           -- 상태 (Y: 활성, N: 삭제)

CONSTRAINT FK_REVIEW_apartment FOREIGN KEY (apartmentId) REFERENCES apartmentinfo(apartmentId),
CONSTRAINT FK_REVIEW_USER FOREIGN KEY (USERNUMBER) REFERENCES USERINFO(USERNUMBER),
CONSTRAINT CHK_REVIEW_RATING CHECK (REVIEWRATING BETWEEN 1 AND 5)

);

-- 리뷰 ID 시퀀스
CREATE SEQUENCE SEQ_REVIEW_ID
START WITH 1
INCREMENT BY 1
NOCACHE;


CREATE TABLE REVIEW_HELPFUL (
HELPFUL_ID NUMBER PRIMARY KEY,
REVIEWID NUMBER NOT NULL,
USERNUMBER NUMBER NOT NULL,
HELPFUL_DATE DATE DEFAULT SYSDATE,
CONSTRAINT FK_REVIEW_HELPFUL_REVIEW FOREIGN KEY (REVIEWID) REFERENCES apartment_REVIEW(REVIEWID),
CONSTRAINT FK_REVIEW_HELPFUL_USER FOREIGN KEY (USERNUMBER) REFERENCES USERINFO(USERNUMBER),
CONSTRAINT UQ_REVIEW_HELPFUL UNIQUE (REVIEWID, USERNUMBER)
);


-- 리뷰(도움됨)시퀀스 생성
CREATE SEQUENCE SEQ_HELPFUL_ID
START WITH 1
INCREMENT BY 1
NOCACHE
NOCYCLE;


-------------------------------------------------------------------------아파트 큐(년,월,시군구코드)
CREATE TABLE "METRO_HOUSE"."APARTMENTINFO_QUEUE" 
   (   "QUEUE_ID" NUMBER, 
   "APARTMENTID" NUMBER, 
   "SGGCD" VARCHAR2(10), 
   "UMDNM" VARCHAR2(100), 
   "APTNM" VARCHAR2(200), 
   "JIBUN" VARCHAR2(100), 
   "EXCLUUSEAR" VARCHAR2(50), 
   "DEALYEAR" VARCHAR2(4), 
   "DEALMONTH" VARCHAR2(2), 
   "DEALDAY" VARCHAR2(2), 
   "DEALAMOUNT" VARCHAR2(100), 
   "FLOOR" VARCHAR2(10), 
   "BUILDYEAR" VARCHAR2(4), 
   "CDEALTYPE" VARCHAR2(50), 
   "CDEALDAY" VARCHAR2(50), 
   "DEALINGGBN" VARCHAR2(50), 
   "ESTATEAGENTSGGNM" VARCHAR2(100), 
   "RGSTDATE" VARCHAR2(50), 
   "APTDONG" VARCHAR2(50), 
   "SLERGBN" VARCHAR2(50), 
   "BUYERGBN" VARCHAR2(50), 
   "LANDLEASEHOLDGBN" VARCHAR2(50), 
   "APTSEQ" VARCHAR2(50), 
   "BONBUN" VARCHAR2(50), 
   "BUBUN" VARCHAR2(50), 
   "LANDCD" VARCHAR2(50), 
   "ROADNM" VARCHAR2(200), 
   "ROADNMBONBUN" VARCHAR2(50), 
   "ROADNMBUBUN" VARCHAR2(50), 
   "ROADNMCD" VARCHAR2(50), 
   "ROADNMSEQ" VARCHAR2(50), 
   "ROADNMSGGCD" VARCHAR2(50), 
   "ROADNMBCD" VARCHAR2(50), 
   "UMDCD" VARCHAR2(50), 
   "LAT" NUMBER(12,8), 
   "LNG" NUMBER(12,8), 
   "SUBWAYSTATION" VARCHAR2(100), 
   "SUBWAYDISTANCE" VARCHAR2(50), 
   "PROCESSED" CHAR(1) DEFAULT 'N'
   )
CREATE INDEX idx_apartmentqueue_id ON APARTMENTINFO_QUEUE(apartmentid);
CREATE SEQUENCE SEQ_APARTMENTINFO_QUEUE
START WITH 1
INCREMENT BY 1
NOCACHE
NOCYCLE;

----------------------------------------------------------------------------------------------apartment procedure
CREATE OR REPLACE PROCEDURE process_apartmentinfo_queue IS
    -- 테이블 생성을 위한 변수들
    v_table_name VARCHAR2(100);
    v_sql        VARCHAR2(4000);
    v_count      NUMBER;
    
    -- 처리할 레코드를 위한 커서
    CURSOR cur IS
        SELECT * FROM APARTMENTINFO_QUEUE WHERE PROCESSED = 'N';
    
    -- 테이블 생성을 위한 커서
    CURSOR tab_cur IS
        SELECT DISTINCT DEALYEAR, DEALMONTH, SGGCD
        FROM APARTMENTINFO_QUEUE
        WHERE PROCESSED = 'N';
BEGIN
    -- 1. 먼저 필요한 테이블 생성 (동일)
    FOR tab_rec IN tab_cur LOOP
        v_table_name := 'Z_' || tab_rec.DEALYEAR;
        
        SELECT COUNT(*) INTO v_count FROM user_tables WHERE table_name = UPPER(v_table_name);
        
        IF v_count = 0 THEN
            -- 테이블 생성 (동일한 구조)
            v_sql := 'CREATE TABLE ' || v_table_name || ' (
                APARTMENTID         NUMBER PRIMARY KEY,
                SGGCD               VARCHAR2(10),
                UMDNM               VARCHAR2(100),
                APTNM               VARCHAR2(200),
                JIBUN               VARCHAR2(100),
                EXCLUUSEAR          VARCHAR2(50),
                DEALYEAR            VARCHAR2(4),
                DEALMONTH           VARCHAR2(2),
                DEALDAY             VARCHAR2(2),
                DEALAMOUNT          VARCHAR2(100),
                FLOOR               VARCHAR2(10),
                BUILDYEAR           VARCHAR2(4),
                CDEALTYPE           VARCHAR2(50),
                CDEALDAY            VARCHAR2(50),
                DEALINGGBN          VARCHAR2(50),
                ESTATEAGENTSGGNM    VARCHAR2(100),
                RGSTDATE            VARCHAR2(50),
                APTDONG             VARCHAR2(50),
                SLERGBN             VARCHAR2(50),
                BUYERGBN            VARCHAR2(50),
                LANDLEASEHOLDGBN    VARCHAR2(50),
                APTSEQ              VARCHAR2(50),
                BONBUN              VARCHAR2(50),
                BUBUN               VARCHAR2(50),
                LANDCD              VARCHAR2(50),
                ROADNM              VARCHAR2(200),
                ROADNMBONBUN        VARCHAR2(50),
                ROADNMBUBUN         VARCHAR2(50),
                ROADNMCD            VARCHAR2(50),
                ROADNMSEQ           VARCHAR2(50),
                ROADNMSGGCD         VARCHAR2(50),
                ROADNMBCD           VARCHAR2(50),
                UMDCD               VARCHAR2(50),
                LAT                 NUMBER(12,8),
                LNG                 NUMBER(12,8),
                SUBWAYSTATION       VARCHAR2(100),
                SUBWAYDISTANCE      VARCHAR2(50)
            )';
            EXECUTE IMMEDIATE v_sql;
        END IF;
    END LOOP;
    
    -- 2. MERGE 문을 사용하여 데이터 처리
    FOR rec IN cur LOOP
        v_table_name := 'Z_' || rec.DEALYEAR;
        
        -- MERGE 문으로 중복 방지
        v_sql := 'MERGE INTO ' || v_table_name || ' target
                  USING (SELECT :1 as APARTMENTID, :2 as SGGCD, :3 as UMDNM, :4 as APTNM, :5 as JIBUN, 
                               :6 as EXCLUUSEAR, :7 as DEALYEAR, :8 as DEALMONTH, :9 as DEALDAY, :10 as DEALAMOUNT,
                               :11 as FLOOR, :12 as BUILDYEAR, :13 as CDEALTYPE, :14 as CDEALDAY, :15 as DEALINGGBN,
                               :16 as ESTATEAGENTSGGNM, :17 as RGSTDATE, :18 as APTDONG, :19 as SLERGBN, :20 as BUYERGBN,
                               :21 as LANDLEASEHOLDGBN, :22 as APTSEQ, :23 as BONBUN, :24 as BUBUN, :25 as LANDCD,
                               :26 as ROADNM, :27 as ROADNMBONBUN, :28 as ROADNMBUBUN, :29 as ROADNMCD, :30 as ROADNMSEQ,
                               :31 as ROADNMSGGCD, :32 as ROADNMBCD, :33 as UMDCD, :34 as LAT, :35 as LNG,
                               :36 as SUBWAYSTATION, :37 as SUBWAYDISTANCE FROM dual) source
                  ON (target.SGGCD = source.SGGCD AND target.APTNM = source.APTNM AND 
                      target.DEALYEAR = source.DEALYEAR AND target.DEALMONTH = source.DEALMONTH AND 
                      target.DEALDAY = source.DEALDAY AND target.EXCLUUSEAR = source.EXCLUUSEAR AND 
                      target.FLOOR = source.FLOOR AND target.DEALAMOUNT = source.DEALAMOUNT)
                  WHEN NOT MATCHED THEN
                      INSERT (APARTMENTID, SGGCD, UMDNM, APTNM, JIBUN, EXCLUUSEAR, DEALYEAR, DEALMONTH, DEALDAY,
                              DEALAMOUNT, FLOOR, BUILDYEAR, CDEALTYPE, CDEALDAY, DEALINGGBN, ESTATEAGENTSGGNM,
                              RGSTDATE, APTDONG, SLERGBN, BUYERGBN, LANDLEASEHOLDGBN, APTSEQ, BONBUN, BUBUN,
                              LANDCD, ROADNM, ROADNMBONBUN, ROADNMBUBUN, ROADNMCD, ROADNMSEQ, ROADNMSGGCD,
                              ROADNMBCD, UMDCD, LAT, LNG, SUBWAYSTATION, SUBWAYDISTANCE)
                      VALUES (source.APARTMENTID, source.SGGCD, source.UMDNM, source.APTNM, source.JIBUN, 
                              source.EXCLUUSEAR, source.DEALYEAR, source.DEALMONTH, source.DEALDAY, source.DEALAMOUNT,
                              source.FLOOR, source.BUILDYEAR, source.CDEALTYPE, source.CDEALDAY, source.DEALINGGBN,
                              source.ESTATEAGENTSGGNM, source.RGSTDATE, source.APTDONG, source.SLERGBN, source.BUYERGBN,
                              source.LANDLEASEHOLDGBN, source.APTSEQ, source.BONBUN, source.BUBUN, source.LANDCD,
                              source.ROADNM, source.ROADNMBONBUN, source.ROADNMBUBUN, source.ROADNMCD, source.ROADNMSEQ,
                              source.ROADNMSGGCD, source.ROADNMBCD, source.UMDCD, source.LAT, source.LNG,
                              source.SUBWAYSTATION, source.SUBWAYDISTANCE)';
        
        EXECUTE IMMEDIATE v_sql USING
            rec.APARTMENTID, rec.SGGCD, rec.UMDNM, rec.APTNM, rec.JIBUN, rec.EXCLUUSEAR, rec.DEALYEAR, rec.DEALMONTH, rec.DEALDAY,
            rec.DEALAMOUNT, rec.FLOOR, rec.BUILDYEAR, rec.CDEALTYPE, rec.CDEALDAY, rec.DEALINGGBN, rec.ESTATEAGENTSGGNM,
            rec.RGSTDATE, rec.APTDONG, rec.SLERGBN, rec.BUYERGBN, rec.LANDLEASEHOLDGBN, rec.APTSEQ, rec.BONBUN, rec.BUBUN,
            rec.LANDCD, rec.ROADNM, rec.ROADNMBONBUN, rec.ROADNMBUBUN, rec.ROADNMCD, rec.ROADNMSEQ, rec.ROADNMSGGCD,
            rec.ROADNMBCD, rec.UMDCD, rec.LAT, rec.LNG, rec.SUBWAYSTATION, rec.SUBWAYDISTANCE;
        
        -- 처리 완료 표시
        UPDATE APARTMENTINFO_QUEUE 
        SET PROCESSED = 'Y' 
        WHERE APARTMENTID = rec.APARTMENTID;
    END LOOP;
    
    COMMIT;
END;
----------------------------------------------------------------------------------------------apartment trigger
create or replace TRIGGER trg_apartmentinfo_insert
AFTER INSERT ON apartmentinfo
FOR EACH ROW
BEGIN
  INSERT INTO apartmentinfo_queue (
    apartmentId, sggcd, umdnm, aptnm, jibun, excluusear,
    dealYear, dealMonth, dealDay, dealAmount, floor, buildYear, cdealType, cdealDay,
    dealingGbn, estateAgentSggnm, rgstDate, aptDong, slerGbn, buyerGbn,
    landLeaseHoldGbn, aptSeq, bonbun, bubun, landCd, roadNm, roadNmBonbun,
    roadNmBubun, roadNmCd, roadNmSeq, roadNmSggcd, roadNmBcd, umdcd,
    lat, lng, subwayStation, subwayDistance
  ) VALUES (
    :NEW.apartmentId, :NEW.sggcd, :NEW.umdnm, :NEW.aptnm, :NEW.jibun, :NEW.excluusear,
    :NEW.dealYear, :NEW.dealMonth, :NEW.dealDay, :NEW.dealAmount, :NEW.floor, :NEW.buildYear, :NEW.cdealType, :NEW.cdealDay,
    :NEW.dealingGbn, :NEW.estateAgentSggnm, :NEW.rgstDate, :NEW.aptDong, :NEW.slerGbn, :NEW.buyerGbn,
    :NEW.landLeaseHoldGbn, :NEW.aptSeq, :NEW.bonbun, :NEW.bubun, :NEW.landCd, :NEW.roadNm, :NEW.roadNmBonbun,
    :NEW.roadNmBubun, :NEW.roadNmCd, :NEW.roadNmSeq, :NEW.roadNmSggcd, :NEW.roadNmBcd, :NEW.umdcd,
    :NEW.lat, :NEW.lng, :NEW.subwayStation, :NEW.subwayDistance
  );
END;


  </code></pre>
</details>
