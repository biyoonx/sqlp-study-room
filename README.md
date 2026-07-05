# SQL 전문가 스터디🔥

## 스터디 내용 : 과목 III. SQL 고급 활용 및 튜닝

### 1주차 : 제1장 SQL 수행 구조(2026-06-27)
#### 제1절 데이터베이스 아키텍처
#### 제2절 SQL 처리 과정
#### 제3절 데이터베이스 I/O 메커니즘

<details>
  <summary>이시향🙋🏻‍♀️</summary>
  
  - [x] 주제 핵심 및 문제풀이 전략
  - [[SQLP 스터디] 1주차 - 제1장 SQL 수행 구조 : Ⅰ-Ⅸ](https://blog.naver.com/biyoonx/224329298300)
  - [x] 주제에 대한 서술형 문제 및 풀이 공유

<dl>
<dd>
<details>
  <summary>문제 1. COMMIT 이후 데이터 유실처럼 보이는 장애 원인 분석</summary>
  
  애플리케이션 또는 DB 클라이언트 도구에서 데이터를 INSERT 또는 UPDATE한 뒤 COMMIT까지 완료했고, 직후 조회 시 해당 데이터가 정상적으로 확인되었다.
  그러나 며칠 후 동일 데이터를 조회해보니 해당 데이터가 사라진 장애가 발생했다.
  단, 명시적인 DELETE, 데이터 삭제 배치, 사용자에 의한 고의 삭제는 확인되지 않았다고 가정한다.
  이때 정상적인 COMMIT의 영속성 보장 구조를 설명하고, 그럼에도 불구하고 데이터 유실처럼 보일 수 있는 가능한 원인을 다음 관점에서 분류하여 설명하라.
  
  1. 애플리케이션 / 트랜잭션 관점
  2. 데이터베이스 아키텍처 관점
  3. Redo / Undo / Checkpoint / Recovery 관점
  4. 백업 복구, 이중화, 스토리지 I/O 관점
  5. 실제 장애 분석 시 우선 확인해야 할 로그와 증거

**답변**

- [[SQLP 스터디] 1주차 - 제1장 SQL 수행 구조 : Ⅹ.문제풀이 문제 1](https://blog.naver.com/biyoonx/224329298300)
</details>
</dd>
</dl>

<dl>
<dd>
<details>
  <summary>문제 2. 기존 상세 조회 SQL 재사용과 별도 단순 SQL 작성의 성능 비교</summary>
  
  애플리케이션에서 상세 조회용 SQL이 이미 존재한다. 이 SQL은 여러 테이블을 조인하고 많은 컬럼을 조회한다.
  그런데 목록 화면 또는 검증 로직에서는 상세 조회 결과 중 일부 컬럼과 일부 조건만 필요하다.
  이 경우 기존 상세 조회 SQL을 재사용하는 방식과, 필요한 컬럼 / 조인 / 조건만 포함한 별도 SQL을 작성하는 방식 중 어느 쪽이 성능상 유리한지 판단 기준을 설명하라.
  단, 다음 관점을 포함하여 설명한다.
  
  1. SQL 파싱 비용
  2. 실행계획 재사용 가능성
  3. 옵티마이저의 쿼리 변환 가능성
  4. 불필요한 조인 및 테이블 액세스 여부
  5. 인덱스 활용 가능성
  6. 데이터베이스 I/O 발생량
  7. 네트워크 전송량
  8. 애플리케이션 유지보수성
  
  또한 어떤 조건에서는 별도 SQL 작성이 유리하고, 어떤 조건에서는 기존 SQL 재사용이 성능상 큰 문제가 없을 수 있는지 구분하여 설명하라.

**답변**

- [[SQLP 스터디] 1주차 - 제1장 SQL 수행 구조 : Ⅹ.문제풀이 문제 2](https://blog.naver.com/biyoonx/224329298300)
</details>
</dd>
</dl>
</details>

<details>
<summary>이지은🙋🏻‍♀️</summary>

- [x] 주제에 대한 서술형 문제 및 풀이 공유

<dl>
<dd>
<details>
    <summary>Q. 동일 SQL의 성능이 갑자기 느려진 원인 분석</summary>
  
  어떤 조회 SQL은 수개월 동안 1초 이내에 수행되었다.
  그러나 어느 날부터 동일 SQL이 30초 이상 소요되기 시작하였다.
  애플리케이션 코드 변경은 없었으며 SQL 문장도 변경되지 않았다.
  DBA가 실행계획을 확인해보니 기존에는 Index Range Scan을 수행하던 SQL이 Full Table Scan으로 수행되고 있었다.
  이때 다음 관점에서 원인을 설명하라.
  
  1. SQL 파싱과 실행계획 생성 과정
  2. 옵티마이저가 액세스 경로를 선택하는 기준
  3. 통계정보(Statistics)의 역할
  4. 데이터 분포 변화가 실행계획에 미치는 영향
  5. Bind Variable Peeking 문제
  6. 실제 장애 분석 시 확인해야 할 자료

**답변**

- [제1장 SQL 수행 구조](https://app.notion.com/p/leeeden/1-SQL-38a70b7b39f480658434c038fa799090?source=copy_link)
</details>
</dd>
</dl>
</details>

<details>
  <summary>최수연🙋🏻‍♀️</summary>

  - [x] 주제에 대한 서술형 문제 및 풀이 공유

<dl>
<dd>
<details>
    <summary>Q. 배치 수행 중 OLTP 응답 지연 원인 분석</summary>
  
  평소에는 정상적으로 동작하던 OLTP 서비스가 대용량 배치 작업이 시작된 이후부터 응답 지연이 발생하기 시작했다.
  OLTP SQL의 실행 계획은 변경되지 않았고, SQL 텍스트와 인덱스 모두 변경되지 않았으며, 배치 SQL과 OLTP SQL은 서로 다른 테이블을 조회하고 있다.
  그럼에도 불구하고 OLTP SQL의 Physical Reads가 배치 수행 전보다 현저히 높아졌다.
  
  단, 하드웨어 이상, 네트워크 이상, 잠금(Lock) 경합은 없다고 가정한다.
  
  이때 배치 SQL이 OLTP 성능에 영향을 미치는 원인을 설명하고, 대응 방안을 다음 관점에서 분류하여 설명하라.

  1. Buffer Cache와 논리적/물리적 I/O 관점
  2. Single Block I/O와 Multi Block I/O 관점
  3. 래치(Latch) 경합 관점
  4. 배치와 OLTP 혼재 환경에서의 아키텍처적 분리 방안

**답변**

- **핵심 쟁점** : 배치 SQL과 OLTP SQL이 서로 무관한 것처럼 보이지만 사실 영향을 받고 있다. 배치 SQL로 인해 발생한 물리적 I/O를 다양한 관점에서 어떻게 바라볼 것인가.
- **핵심 키워드** : Buffer Cache, LRU 알고리즘, 논리적 I/O, 물리적 I/O, Single Block I/O, Multi Block I/O, Full Table Scan, 래치(Latch)

1. Buffer Cache와 논리적/물리적 I/O 관점
  
    Buffer Cache란 디스크에서 읽은 데이터 블록을 메모리에 캐싱하여 물리적 I/O를 줄이는 공간이다. 배치 SQL 실행으로 인해 Buffer Cache의 데이터 블록이 가득 차게 되며, LRU 알고리즘에 의해 OLTP SQL이 참조하던 기존 데이터 블록마저 교체된다. 따라서 OLTP SQL도 디스크를 다녀와야 하는 물리적 I/O가 대량 증가하게 된다.
  
2. Single Block I/O와 Multi Block I/O 관점
  
    Single Block I/O는 단일 데이터 블록을 읽는 방식이고, Multi Block I/O는 다량의 데이터 블록을 한 번에 읽는 방식이다. 배치 SQL은 Full Table Scan을 수행하면서 Multi Block I/O 방식으로 대량의 데이터 블록을 Buffer Cache에 한꺼번에 적재한다. 이로 인해 Buffer Cache가 빠르게 가득 차게 되고, LRU 알고리즘에 의해 OLTP SQL이 참조하던 데이터 블록이 밀려나 물리적 I/O가 증가하게 된다.
  
3. 래치(Latch) 경합 관점
  
    래치란 공유 자원인 Buffer Cache에 여러 프로세스가 동시에 접근할 때 데이터 일관성을 보장하기 위한 잠금장치이다. 배치 SQL이 대량의 블록을 Buffer Cache에 올리는 과정에서 대량의 래치를 획득하게 된다. 그 결과 OLTP SQL은 래치를 획득하지 못하고 대기하게 되어 응답 지연이 발생하게 된다.
  
4. 배치와 OLTP 혼재 환경에서의 아키텍처적 분리 방안
  
    배치 SQL과 OLTP SQL이 혼재된 환경에서는 두 가지 방법으로 분리할 수 있다. 첫째, 시간적으로 분리한다. 배치 SQL을 OLTP SQL이 실행되지 않는 한적한 시간대에 실행하여 두 SQL의 실행이 겹치지 않도록 한다. 둘째, 물리적으로 분리한다. 배치와 OLTP가 실행되는 서버를 분리하여 동시간대에 실행되더라도 Buffer Cache 경합이 발생하지 않도록 한다.
</details>
</dd>
</dl>
</details>

---

### 2주차 : 제2장 SQL 분석 도구(2026-07-05)
#### 제1절 예상 실행계획
#### 제2절 SQL 트레이스
#### 제3절 응답 시간 분석

<details>
  <summary>최수연🙋🏻‍♀️</summary>

  - [x] 주제에 대한 서술형 문제 및 풀이 공유

<dl>
<dd>
<details>
    <summary>Q. 트레이스 결과를 활용한 SQL 응답 시간 및 대기 이벤트 분석</summary>
  
  다음 트레이스 결과를 분석하여 질문에 답하시오.
  
  ```
  call     count    cpu    elapsed    disk    query    current    rows
  -------- ------  -----  ---------  ------  -------  ---------  -----
  Parse         1   0.00       0.00       0        0          0      0
  Execute       1   0.00       0.00       0        0          0      0
  Fetch        11   0.10      25.40      90      200          0   1000
  -------- ------  -----  ---------  ------  -------  ---------  -----
  total        13   0.10      25.40      90      200          0   1000
  
  Elapsed times include waiting on following events:
  Event waited on                   Times  Max.Wait  Total Waited
  --------------------------------- -----  --------  ------------
  db file sequential read              85      0.30         20.00
  db file scattered read                5      0.50          2.50
  SQL*Net message from client           1      2.00          2.00
  buffer busy waits                     2      0.15          0.30
  ```
  
  1. 대기 이벤트와 연관지어 ```cpu```와 ```elapsed``` 의 차이 설명
  2. 각 대기 이벤트의 의미와 발생 원인
  3. ```SQL*Net message from client``` 의 DB 성능 문제 여부
  4. 가장 먼저 튜닝해야 할 대기 이벤트

**답변**

- [[SQLP] 제2장 문제 및 풀이](https://evergreen-lupin-69c.notion.site/SQLP-2-391894b3ff328096b6d9d8ff65bf4a59?pvs=143)
</details>
</dd>
</dl>
</details>

<details>
<summary>이지은🙋🏻‍♀️</summary>

- [x] 주제에 대한 서술형 문제 및 풀이 공유

<dl>
<dd>
<details>
    <summary>Q. 월별 매출 집계 리포트 SQL 분석</summary>
  
  다음 SQL은 관리자 화면에서 상품 카테고리별 월 매출 요약을 조회하는 SQL이다. 운영 환경에서 특정 월 조회 시 평균 40초 이상 소요된다.
  
  #### 인덱스 정보
  
  ```
  ORDER_MASTER
  - PK_ORDER_MASTER (ORDER_NO)
  - IDX_ORDER_MASTER01 (ORDER_DT)
  - IDX_ORDER_MASTER02 (ORDER_STATUS)
  
  ORDER_ITEM
  - IDX_ORDER_ITEM01 (ORDER_NO)
  - IDX_ORDER_ITEM02 (PRODUCT_ID)
  
  PRODUCT
  - PK_PRODUCT (PRODUCT_ID)
  - IDX_PRODUCT01 (USE_YN)
  
  CATEGORY
  - PK_CATEGORY (CATEGORY_ID)
  ```
  
  #### **SQL**
  
  ```sql
  SELECT /*+ GATHER_PLAN_STATISTICS */
         c.category_nm,
         TO_CHAR(o.order_dt, 'YYYY-MM') AS order_month,
         COUNT(DISTINCT o.order_no) AS order_cnt,
         SUM(oi.order_qty) AS total_qty,
         SUM(oi.order_qty * oi.sale_price) AS total_amt
  FROM order_item oi
       JOIN order_master o
         ON o.order_no = oi.order_no
       JOIN product p
         ON p.product_id = oi.product_id
       JOIN category c
         ON c.category_id = p.category_id
  WHERE TO_CHAR(o.order_dt, 'YYYYMM') = '202506'
    AND o.order_status IN ('PAYED', 'DELIVERED')
    AND p.use_yn = 'Y'
  GROUP BY c.category_nm,
           TO_CHAR(o.order_dt, 'YYYY-MM')
  HAVING SUM(oi.order_qty * oi.sale_price) >= 1000000
  ORDER BY total_amt DESC;
  ```
  
  #### 실행계획 일부
  
  ```
  Id  Operation                       Starts  E-Rows   A-Rows   Buffers
  --  ------------------------------  ------  ------   ------   -------
   1  SORT ORDER BY                        1      20       12    980000
   2   FILTER                              1               12    980000
   3    HASH GROUP BY                      1      20       12    980000
   4     HASH JOIN                         1  120000   850000    940000
   5      HASH JOIN                        1   80000   620000    510000
   6       HASH JOIN                       1   30000   180000    230000
   7        TABLE ACCESS FULL ORDER_MASTER 1    5000   180000    160000
   8        TABLE ACCESS FULL ORDER_ITEM   1  300000  1200000    360000
   9       TABLE ACCESS FULL PRODUCT       1   50000    50000     70000
  10      TABLE ACCESS FULL CATEGORY       1     100      100       500
  ```
  
  #### Predicate Information
  
  ```sql
  7 - filter(TO_CHAR("O"."ORDER_DT",'YYYYMM')='202506'
             AND "O"."ORDER_STATUS" IN ('PAYED','DELIVERED'))
  
  9 - filter("P"."USE_YN"='Y')
  ```
  
  1. 최종 결과는 12건인데 ORDER_ITEM에서 120만 건이 처리되는 이유를 설명하시오.
  2. TO_CHAR(o.order_dt, 'YYYYMM') = '202506' 조건이 인덱스 사용에 미치는 영향을 설명하시오.
  3. HASH JOIN, HASH GROUP BY, SORT ORDER BY가 각각 어떤 작업을 의미하는지 설명하시오.
  4. 실행계획에서 Logical I/O가 많이 발생하는 연산을 찾고, 각 연산이 전체 SQL 성능에 미치는 영향을 A-Rows와 Buffers를 근거로 설명하시오. 또한 이러한 연산들이 연쇄적으로 성능 저하를 유발하는 이유를 기술하시오.
  5. COUNT(DISTINCT o.order_no)가 일반 COUNT(*)보다 부담이 큰 이유를 설명하시오.
  6. 이 SQL을 튜닝한다면 우선순위대로 개선 방안을 제시하시오.
  7. Predicate Information을 참고하여 조건절이 어떤 방식으로 처리되고 있는지 설명하고, 이것이 튜닝 판단에 주는 의미를 기술하시오.

**답변**

- [제2장 SQL 분석 도구](https://app.notion.com/p/leeeden/2-SQL-39170b7b39f480aa8ce1eb7cbd63c30f?source=copy_link)
</details>
</dd>
</dl>
</details>

<details>
  <summary>이시향🙋🏻‍♀️</summary>
  
  - [x] 주제 핵심 및 문제풀이 전략
  - [[SQLP 스터디] 2주차 - 제2장 SQL 분석 도구 : Ⅰ-Ⅴ](https://blog.naver.com/biyoonx/224336649386)
  - [x] 주제에 대한 서술형 문제 및 풀이 공유

<dl>
<dd>
<details>
  <summary>문제 1. SCOTT 기반 대량 데이터 조회 SQL 분석</summary>
  
  다음은 Oracle SCOTT 계정의 EMP, DEPT, SALGRADE 테이블을 기반으로 대량 실습 테이블 EMP_BIG을 생성한 뒤, 일부러 비효율적인 목록 조회 SQL을 실행하는 문제이다.
  
  주어진 SQL을 실행하고 실행계획 및 실행 통계를 확인하여 병목 원인을 분석하라.
  
  * 데이터 생성 및 부하 쿼리
  
  ```sql
  --------------------------------------------------------------------------------
  -- 문제 1. SCOTT 기반 대량 데이터 조회 SQL 분석
  --
  -- 아래 SQL은 전체 일괄 실행용이 아니라, 실습 환경에 따라 필요한 블록을 선택 실행한다.
  --------------------------------------------------------------------------------
  
  --------------------------------------------------------------------------------
  -- 0. 실행계획/시간 확인용 설정
  -- SQL*Plus 또는 SQLcl 기준
  --------------------------------------------------------------------------------
  
  SET TIMING ON
  SET LINESIZE 200
  SET PAGESIZE 1000
  SET SERVEROUTPUT ON
  
  -- AUTOTRACE 사용 가능 환경이면 필요 시 사용
  -- SET AUTOTRACE ON
  -- SET AUTOTRACE TRACEONLY STATISTICS
  
  
  --------------------------------------------------------------------------------
  -- 1. 기존 실습 테이블 삭제
  --------------------------------------------------------------------------------
  
  BEGIN
      EXECUTE IMMEDIATE 'DROP TABLE emp_big PURGE';
  EXCEPTION
      WHEN OTHERS THEN
          IF SQLCODE != -942 THEN
              RAISE;
          END IF;
  END;
  /
  
  
  --------------------------------------------------------------------------------
  -- 2. 실습 테이블 생성
  -- SCOTT 계정의 EMP 테이블을 기반으로 대량 데이터 생성
  --------------------------------------------------------------------------------
  
  CREATE TABLE emp_big (
      emp_big_id NUMBER NOT NULL,
      src_empno  NUMBER,
      ename      VARCHAR2(100),
      job        VARCHAR2(30),
      mgr        NUMBER,
      hiredate   DATE,
      sal        NUMBER,
      comm       NUMBER,
      deptno     NUMBER,
      retire_yn  CHAR(1),
      work_area  VARCHAR2(20),
      memo       VARCHAR2(100)
  );
  
  
  --------------------------------------------------------------------------------
  -- 3. 데이터 추가
  --
  -- 조절 위치:
  -- CONNECT BY LEVEL <= 3000
  --
  -- 3000  : 약  42,000건
  -- 5000  : 약  70,000건
  -- 10000 : 약 140,000건
  -- 20000 : 약 280,000건
  --
  -- 처음에는 3000으로 시작하고, 너무 빠르면 5000 또는 10000으로 올린다.
  --------------------------------------------------------------------------------
  
  INSERT /*+ APPEND */ INTO emp_big (
      emp_big_id,
      src_empno,
      ename,
      job,
      mgr,
      hiredate,
      sal,
      comm,
      deptno,
      retire_yn,
      work_area,
      memo
  )
  SELECT
         e.empno * 1000000 + n.seq AS emp_big_id,
         e.empno                   AS src_empno,
         e.ename || '_' || n.seq   AS ename,
         e.job,
         e.mgr,
         e.hiredate + MOD(n.seq, 3650) AS hiredate,
         e.sal + MOD(n.seq, 3000)      AS sal,
         CASE
           WHEN MOD(n.seq, 5) = 0 THEN MOD(n.seq, 1000)
           ELSE e.comm
         END AS comm,
         e.deptno,
         CASE
           WHEN MOD(n.seq, 10) = 0 THEN 'Y'
           ELSE 'N'
         END AS retire_yn,
         CASE
           WHEN MOD(n.seq, 3) = 0 THEN 'SEOUL'
           WHEN MOD(n.seq, 3) = 1 THEN 'BUSAN'
           ELSE 'INCHEON'
         END AS work_area,
         RPAD('x', 100, 'x') AS memo
  FROM emp e
  CROSS JOIN (
      SELECT LEVEL AS seq
      FROM dual
      CONNECT BY LEVEL <= 3000
  ) n;
  
  COMMIT;
  
  
  --------------------------------------------------------------------------------
  -- 선택 실행: 부하가 약할 경우에만 실행
  --
  -- 예: 기본 3000배 데이터에서 5000배 데이터로 늘리기
  -- 추가 범위: 3001 ~ 5000
  --
  -- 주의:
  -- 이 블록은 기본 생성 직후 반드시 실행해야 하는 SQL이 아니다.
  -- 부하 쿼리가 너무 빨리 끝나 분석 포인트가 잘 보이지 않을 때만 실행한다.
  --------------------------------------------------------------------------------
  
  INSERT /*+ APPEND */ INTO emp_big (
      emp_big_id,
      src_empno,
      ename,
      job,
      mgr,
      hiredate,
      sal,
      comm,
      deptno,
      retire_yn,
      work_area,
      memo
  )
  SELECT
         e.empno * 1000000 + n.seq AS emp_big_id,
         e.empno                   AS src_empno,
         e.ename || '_' || n.seq   AS ename,
         e.job,
         e.mgr,
         e.hiredate + MOD(n.seq, 3650) AS hiredate,
         e.sal + MOD(n.seq, 3000)      AS sal,
         CASE
           WHEN MOD(n.seq, 5) = 0 THEN MOD(n.seq, 1000)
           ELSE e.comm
         END AS comm,
         e.deptno,
         CASE
           WHEN MOD(n.seq, 10) = 0 THEN 'Y'
           ELSE 'N'
         END AS retire_yn,
         CASE
           WHEN MOD(n.seq, 3) = 0 THEN 'SEOUL'
           WHEN MOD(n.seq, 3) = 1 THEN 'BUSAN'
           ELSE 'INCHEON'
         END AS work_area,
         RPAD('x', 100, 'x') AS memo
  FROM emp e
  CROSS JOIN (
      SELECT LEVEL + 3000 AS seq
      FROM dual
      CONNECT BY LEVEL <= 2000
  ) n;
  
  COMMIT;
  
  BEGIN
    DBMS_STATS.GATHER_TABLE_STATS(
        ownname => USER,
        tabname => 'EMP_BIG',
        cascade => TRUE
    );
  END;
  /
  
  SELECT COUNT(*) AS emp_big_cnt
  FROM emp_big;
  
  
  --------------------------------------------------------------------------------
  -- 4. 인덱스 생성
  --------------------------------------------------------------------------------
  
  CREATE INDEX emp_big_x01 ON emp_big(deptno, hiredate);
  CREATE INDEX emp_big_x02 ON emp_big(job, sal);
  CREATE INDEX emp_big_x03 ON emp_big(hiredate);
  CREATE INDEX emp_big_x04 ON emp_big(ename);
  CREATE INDEX emp_big_x05 ON emp_big(retire_yn, hiredate);
  CREATE INDEX emp_big_x06 ON emp_big(deptno, sal);
  
  
  --------------------------------------------------------------------------------
  -- 5. 통계 수집
  --------------------------------------------------------------------------------
  
  BEGIN
    DBMS_STATS.GATHER_TABLE_STATS(
        ownname => USER,
        tabname => 'EMP_BIG',
        cascade => TRUE
    );
  END;
  /
  
  
  --------------------------------------------------------------------------------
  -- 6. 데이터 건수 확인
  --------------------------------------------------------------------------------
  
  SELECT COUNT(*) AS emp_big_cnt
  FROM emp_big;
  
  
  --------------------------------------------------------------------------------
  -- 7. 부하 쿼리 실행
  --------------------------------------------------------------------------------
  
  SELECT /*+ GATHER_PLAN_STATISTICS */ /* emp_big_heavy_test_001 */
         *
  FROM (
      SELECT
             e.emp_big_id,
             e.ename,
             e.job,
             e.deptno,
             e.hiredate,
             e.sal,
             d.dname,
             s.grade,
             (
               SELECT /*+ NO_UNNEST */ COUNT(*)
               FROM emp_big x
               WHERE x.deptno = e.deptno
             ) AS dept_emp_cnt,
             (
               SELECT /*+ NO_UNNEST */ AVG(x.sal)
               FROM emp_big x
               WHERE x.deptno = e.deptno
             ) AS dept_avg_sal,
             (
               SELECT /*+ NO_UNNEST */ MAX(x.sal)
               FROM emp_big x
               WHERE x.job = e.job
             ) AS job_max_sal,
             (
               SELECT /*+ NO_UNNEST */ COUNT(*)
               FROM emp_big x
               WHERE x.deptno = e.deptno
                 AND x.sal BETWEEN e.sal - 300 AND e.sal + 300
             ) AS similar_sal_cnt,
             (
               SELECT /*+ NO_UNNEST */ COUNT(*)
               FROM emp_big x
               WHERE x.job = e.job
                 AND x.hiredate BETWEEN e.hiredate - 30 AND e.hiredate + 30
             ) AS similar_hire_cnt,
             ROW_NUMBER() OVER (
                 ORDER BY
                     (
                       SELECT /*+ NO_UNNEST */ COUNT(*)
                       FROM emp_big x
                       WHERE x.deptno = e.deptno
                         AND x.sal BETWEEN e.sal - 300 AND e.sal + 300
                     ) DESC,
                     (
                       SELECT /*+ NO_UNNEST */ COUNT(*)
                       FROM emp_big x
                       WHERE x.job = e.job
                         AND x.hiredate BETWEEN e.hiredate - 30 AND e.hiredate + 30
                     ) DESC,
                     e.sal DESC,
                     e.hiredate DESC
             ) AS rn
      FROM emp_big e
           JOIN dept d
             ON d.deptno = e.deptno
           JOIN salgrade s
             ON e.sal BETWEEN s.losal AND s.hisal
      WHERE TO_CHAR(e.hiredate, 'YYYY') = '1981'
        AND UPPER(e.ename) LIKE '%A%'
        AND NVL(e.retire_yn, 'N') = 'N'
  )
  WHERE rn BETWEEN 1 AND 50
  ORDER BY rn;
  
  
  --------------------------------------------------------------------------------
  -- 8. SQL ID 찾기
  --
  -- 부하 쿼리 실행 직후 아래 SQL 실행
  --------------------------------------------------------------------------------
  
  SELECT sql_id,
         child_number,
         executions,
         fetches,
         rows_processed,
         elapsed_time,
         buffer_gets,
         disk_reads,
         sql_text
  FROM v$sql
  WHERE sql_text LIKE '%emp_big_heavy_test_001%'
    AND sql_text NOT LIKE '%v$sql%'
  ORDER BY last_active_time DESC;
  
  
  --------------------------------------------------------------------------------
  -- 9. 실행 후 실제 실행계획/통계 확인용 쿼리
  --
  -- 부하 쿼리 실행 직후 아래 SQL 실행
  --------------------------------------------------------------------------------
  
  SELECT *
  FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(
      '8의_SQL_ID',
      8의_CHILD_NUMBER,
      'ALLSTATS LAST +PREDICATE +ALIAS +IOSTATS'
  ));
  ```
  
  ### 실습 목표
  
  * 함수 조건이 인덱스 사용에 미치는 영향 확인
  * 스칼라 서브쿼리 반복 접근 확인
  * ORDER BY 및 페이징 처리 전 중간 처리량 확인
  * 실행계획과 실제 실행 통계를 함께 보는 연습
  
  ### 질문
  
  1. 실행계획에서 EMP_BIG 테이블이 반복 접근되는 구간은 어디인가?
  
  2. 실행 통계에서 반복 실행을 확인할 수 있는 지표는 무엇인가?
  
  3. 최종 결과는 50건인데, 실행계획상 그보다 많은 데이터가 처리되는 구간은 어디인가?
  
  4. 정렬 또는 WINDOW SORT가 발생하는 구간은 어디인가?
  
  5. 예상 실행계획의 Rows/Cost만 보고 판단하면 위험한 이유는 무엇인가?
  
  6. 실제 실행 통계에서 병목으로 의심되는 근거를 2개 이상 제시하라.
  
  7. 이 SQL을 개선한다면 어떤 부분부터 의심하겠는가?

**답변**

- [[SQLP 스터디] 2주차 - 제2장 SQL 분석 도구 : Ⅵ.문제풀이 문제 1](https://blog.naver.com/biyoonx/224336649386)
</details>
</dd>
</dl>

<dl>
<dd>
<details>
  <summary>문제 2. 실무 SQL 튜닝 전후 비교</summary>
  
  실무 튜닝 전후 실행계획과 실행 통계를 비교하여 성능 개선 여부와 개선 원인을 분석한다.
  
  ### 업무 상황
  
  * 대상 기능 / 주요 조건 / 주요 출력 / 문제 상황
  
  ### 튜닝 전 SQL / 튜닝 후 SQL
  
  ### 튜닝 전 실행결과 / 튜닝 후 실행결과
  
  ### 질문
  
  1. 튜닝 전후 실행계획에서 접근 방식이 어떻게 달라졌는가?
  
  2. 튜닝 전후 실행 통계에서 가장 크게 줄어든 지표는 무엇인가?
  
  3. 수행 시간이 줄었다면 그 원인을 실행계획/통계 기준으로 설명하라.
  
  4. Cost만 낮아졌다고 개선됐다고 단정할 수 없는 이유는 무엇인가?
  
  5. 튜닝 후에도 추가로 확인해야 할 조건은 무엇인가?

**답변**

- 공유 X
</details>
</dd>
</dl>
</details>
</dd>
</dl>
</details>

---

### 3주차 : 제3장 인덱스 튜닝
#### 제1절 인덱스 기본 원리
#### 제2절 테이블 액세스 최소화

---

### 4주차 : 제3장 인덱스 튜닝
#### 제3절 인덱스 스캔 효율화
#### 제4절 인덱스 설계

---

### 5주차 : 제4장 조인 튜닝
#### 제1절 NL 조인
#### 제2절 소트 머지 조인
#### 제3절 해시 조인
#### 제4절 스칼라 서브쿼리
#### 제5절 고급 조인 기법

---

### 6주차 : 제5장 SQL 옵티마이저
#### 제1절 SQL 옵티마이저 원리
#### 제2절 SQL 공유 및 재사용
#### 제3절 쿼리 변환

---

### 7주차 : 제6장 고급 SQL 튜닝
#### 제1절 소트 튜닝
#### 제2절 DML 튜닝
#### 제3절 데이터베이스 Call 최소화
#### 제4절 파티셔닝
#### 제5절 대용량 배치 프로그램 튜닝
#### 제6절 고급 SQL 활용

---

### 8주차 : 제7장 Lock과 트랜잭션 동시성 제어
#### 제1절 Lock
#### 제2절 트랜잭션
#### 제3절 동시성 제어

