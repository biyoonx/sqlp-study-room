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

### 3주차 : 제3장 인덱스 튜닝(2026-07-11)
#### 제1절 인덱스 기본 원리
#### 제2절 테이블 액세스 최소화

<details>
  <summary>이시향🙋🏻‍♀️</summary>
  
  - [x] 주제 핵심 및 문제풀이 전략
  - [[SQLP 스터디] 3주차 - 제3장 인덱스 튜닝 1-2 Ⅰ~Ⅸ](https://blog.naver.com/biyoonx/224343603076)
  - [x] 주제에 대한 서술형 문제 및 풀이 공유

<dl>
<dd>
<details>
  <summary>클러스터링 팩터, 테이블 랜덤 액세스, 커버링 인덱스 개선 효과 비교</summary>
  
  주문 테이블에서 다음 두 가지 SQL이 자주 수행된다.

### SQL-1. 고객 구간별 주문 금액 조회

```sql
SELECT SUM(O.PAY_AMT)
FROM   TB_ORDER O
WHERE  O.CUST_ID BETWEEN 1001 AND 2000
AND    O.ORD_DT  BETWEEN DATE '2025-01-01' AND DATE '2025-03-31'
AND    O.ORD_STAT_CD = 'PAY';
```

### SQL-2. 일자별 결제 주문 금액 조회

```sql
SELECT SUM(O.PAY_AMT)
FROM   TB_ORDER O
WHERE  O.ORD_DT BETWEEN DATE '2025-01-01' AND DATE '2025-01-10'
AND    O.ORD_STAT_CD = 'PAY';
```

현재 인덱스는 다음과 같다.

```text
X01 : CUST_ID + ORD_DT
X02 : ORD_DT + ORD_STAT_CD
```

SQL-1의 성능 개선을 위해 다음 인덱스를 추가하였다.

```text
X03 : CUST_ID + ORD_DT + ORD_STAT_CD
```

그러나 SQL-1의 성능은 기대만큼 개선되지 않았다.

이후 같은 데이터를 `CUST_ID, ORD_DT` 순서로 재구성한 테이블을 만들어 비교하였다.
마지막으로 SQL-1 전용 커버링 인덱스를 추가하였다.

```text
X04 : CUST_ID + ORD_DT + ORD_STAT_CD + PAY_AMT
```

---

### 문제 1. 랜덤 액세스가 줄지 않은 원인 분석

`X03(CUST_ID, ORD_DT, ORD_STAT_CD)` 인덱스를 추가했음에도 SQL-1의 성능 개선 효과가 크지 않은 이유를 설명하시오.

단, 다음 관점에서 설명하시오.

```text
- INDEX RANGE SCAN 이후 TABLE ACCESS BY INDEX ROWID가 계속 발생하는 이유
- PAY_AMT 조회를 위해 테이블 액세스가 필요한 이유
- 클러스터링 팩터가 나쁠 때 Buffers가 크게 발생하는 이유
```

---

### 문제 2. 서로 다른 인덱스의 클러스터링 팩터 비교

`X01(CUST_ID, ORD_DT)`과 `X02(ORD_DT, ORD_STAT_CD)`의 클러스터링 팩터를 비교하시오.

또한 테이블을 `CUST_ID, ORD_DT` 순서로 재구성하면 SQL-1에는 유리할 수 있지만, SQL-2에는 어떤 영향이 있을 수 있는지 설명하시오.

---

### 문제 3. 커버링 인덱스와 클러스터링 팩터 개선 중 선택

SQL-1의 성능 개선 방안으로 다음 두 방법을 비교하시오.

```text
1. 테이블을 CUST_ID, ORD_DT 순서로 재구성한다.
2. PAY_AMT까지 포함한 커버링 인덱스 X04를 생성한다.
```

각 방법의 장단점을 다음 관점에서 설명하시오.

```text
- TABLE ACCESS BY INDEX ROWID 제거 여부
- Buffers 감소 효과
- 인덱스 크기 증가
- INSERT / UPDATE / DELETE 부하
- SQL-2 같은 다른 조회 패턴에 미치는 영향
- 운영 반영 난이도
```

---

### 전체 실습 SQL

```sql
/* =========================================================
   1. 기존 객체 삭제
   ========================================================= */

BEGIN
    EXECUTE IMMEDIATE 'DROP TABLE TB_ORDER_GOOD PURGE';
EXCEPTION
    WHEN OTHERS THEN
        IF SQLCODE != -942 THEN
            RAISE;
        END IF;
END;
/

BEGIN
    EXECUTE IMMEDIATE 'DROP TABLE TB_ORDER_BAD PURGE';
EXCEPTION
    WHEN OTHERS THEN
        IF SQLCODE != -942 THEN
            RAISE;
        END IF;
END;
/


/* =========================================================
   2. BAD 테이블 생성

   의도:
   - 실제 적재 순서는 ORD_DT, CUST_ID에 가까움
   - 따라서 CUST_ID, ORD_DT 인덱스 기준으로는 클러스터링 팩터가 나쁘게 나올 수 있음
   - 반대로 ORD_DT, ORD_STAT_CD 인덱스 기준으로는 상대적으로 좋게 나올 수 있음
   ========================================================= */

CREATE TABLE TB_ORDER_BAD
(
    ORD_NO       NUMBER        NOT NULL,
    CUST_ID      NUMBER        NOT NULL,
    ORD_DT       DATE          NOT NULL,
    ORD_STAT_CD  VARCHAR2(3)   NOT NULL,
    PAY_AMT      NUMBER        NOT NULL,
    DLVY_STAT_CD VARCHAR2(3),
    FILLER       VARCHAR2(80)
)
NOLOGGING;


/* =========================================================
   3-A. 기본 버전 데이터 생성: 30만 건

   기본 실습만 할 경우 여기까지만 데이터 적재하고,
   아래 3-B 추가 데이터 구간은 실행하지 않는다.
   ========================================================= */

INSERT /*+ APPEND */ INTO TB_ORDER_BAD
SELECT
    LEVEL AS ORD_NO,
    MOD(LEVEL - 1, 10000) + 1 AS CUST_ID,
    DATE '2025-01-01' + TRUNC((LEVEL - 1) / 10000) AS ORD_DT,
    CASE
        WHEN MOD(LEVEL, 10) = 0 THEN 'CAN'
        ELSE 'PAY'
    END AS ORD_STAT_CD,
    MOD(LEVEL, 100000) + 1000 AS PAY_AMT,
    CASE
        WHEN MOD(LEVEL, 3) = 0 THEN 'DLV'
        WHEN MOD(LEVEL, 3) = 1 THEN 'RDY'
        ELSE 'ING'
    END AS DLVY_STAT_CD,
    RPAD('X', 80, 'X') AS FILLER
FROM DUAL
CONNECT BY LEVEL <= 300000;

COMMIT;


/* =========================================================
   3-B. 추가 버전 데이터 생성: 70만 건 추가

   이 구간까지 실행하면 총 100만 건이 된다.
   기본 30만 건만 실습할 경우 이 구간은 실행하지 않는다.
   ========================================================= */

INSERT /*+ APPEND */ INTO TB_ORDER_BAD
SELECT
    300000 + LEVEL AS ORD_NO,
    MOD(300000 + LEVEL - 1, 10000) + 1 AS CUST_ID,
    DATE '2025-01-01' + TRUNC((300000 + LEVEL - 1) / 10000) AS ORD_DT,
    CASE
        WHEN MOD(300000 + LEVEL, 10) = 0 THEN 'CAN'
        ELSE 'PAY'
    END AS ORD_STAT_CD,
    MOD(300000 + LEVEL, 100000) + 1000 AS PAY_AMT,
    CASE
        WHEN MOD(300000 + LEVEL, 3) = 0 THEN 'DLV'
        WHEN MOD(300000 + LEVEL, 3) = 1 THEN 'RDY'
        ELSE 'ING'
    END AS DLVY_STAT_CD,
    RPAD('X', 80, 'X') AS FILLER
FROM DUAL
CONNECT BY LEVEL <= 700000;

COMMIT;


/* =========================================================
   4. 데이터 확인
   ========================================================= */

SELECT COUNT(*) AS CNT,
       MIN(ORD_DT) AS MIN_ORD_DT,
       MAX(ORD_DT) AS MAX_ORD_DT,
       MIN(CUST_ID) AS MIN_CUST_ID,
       MAX(CUST_ID) AS MAX_CUST_ID
FROM TB_ORDER_BAD;


/* =========================================================
   5. 초기 인덱스 생성

   X01 : SQL-1 고객 기준 조회용
   X02 : SQL-2 일자 기준 조회용
   ========================================================= */

CREATE INDEX TB_ORDER_BAD_X01
ON TB_ORDER_BAD (CUST_ID, ORD_DT)
NOLOGGING;

CREATE INDEX TB_ORDER_BAD_X02
ON TB_ORDER_BAD (ORD_DT, ORD_STAT_CD)
NOLOGGING;


/* =========================================================
   6. 통계 수집
   ========================================================= */

BEGIN
    DBMS_STATS.GATHER_TABLE_STATS(
        OWNNAME    => USER,
        TABNAME    => 'TB_ORDER_BAD',
        CASCADE    => TRUE,
        METHOD_OPT => 'FOR ALL COLUMNS SIZE 1'
    );
END;
/


/* =========================================================
   7. 세그먼트 크기 확인
   ========================================================= */

SELECT
    SEGMENT_NAME,
    SEGMENT_TYPE,
    ROUND(BYTES / 1024 / 1024, 1) AS MB
FROM USER_SEGMENTS
WHERE SEGMENT_NAME LIKE 'TB_ORDER%'
ORDER BY BYTES DESC;


/* =========================================================
   8. 클러스터링 팩터 확인: BAD 테이블
   ========================================================= */

SELECT
    I.TABLE_NAME,
    I.INDEX_NAME,
    T.NUM_ROWS,
    T.BLOCKS,
    I.LEAF_BLOCKS,
    I.CLUSTERING_FACTOR,
    ROUND(I.CLUSTERING_FACTOR / NULLIF(T.BLOCKS, 0), 2) AS CF_PER_BLOCKS,
    ROUND(I.CLUSTERING_FACTOR / NULLIF(T.NUM_ROWS, 0), 4) AS CF_PER_ROWS
FROM USER_INDEXES I
JOIN USER_TABLES T
  ON T.TABLE_NAME = I.TABLE_NAME
WHERE I.TABLE_NAME = 'TB_ORDER_BAD'
ORDER BY I.INDEX_NAME;


/* =========================================================
   9. 실행계획 통계 확인 세션 설정
   ========================================================= */

ALTER SESSION SET STATISTICS_LEVEL = ALL;


/* =========================================================
   10. SQL-1 실행: BAD + X01

   확인 대상:
   - INDEX RANGE SCAN
   - TABLE ACCESS BY INDEX ROWID
   - TABLE ACCESS 단계의 A-Rows / Buffers
   - ORD_STAT_CD 조건이 테이블 필터로 처리되는지
   ========================================================= */

SELECT /*+ GATHER_PLAN_STATISTICS INDEX(O TB_ORDER_BAD_X01) NO_BATCH_TABLE_ACCESS_BY_ROWID(O) */
       SUM(O.PAY_AMT) AS SUM_PAY_AMT
FROM   TB_ORDER_BAD O
WHERE  O.CUST_ID BETWEEN 1001 AND 2000
AND    O.ORD_DT  BETWEEN DATE '2025-01-01' AND DATE '2025-03-31'
AND    O.ORD_STAT_CD = 'PAY';

SELECT *
FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL, 'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));


/* =========================================================
   11. SQL-2 실행: BAD + X02

   확인 대상:
   - X02 기준 클러스터링 팩터와 Buffers
   - SQL-1과 비교
   ========================================================= */

SELECT /*+ GATHER_PLAN_STATISTICS INDEX(O TB_ORDER_BAD_X02) NO_BATCH_TABLE_ACCESS_BY_ROWID(O) */
       SUM(O.PAY_AMT) AS SUM_PAY_AMT
FROM   TB_ORDER_BAD O
WHERE  O.ORD_DT BETWEEN DATE '2025-01-01' AND DATE '2025-01-10'
AND    O.ORD_STAT_CD = 'PAY';

SELECT *
FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL, 'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));


/* =========================================================
   12. X03 추가: SQL-1 조건 컬럼 추가 인덱스

   X03 : CUST_ID + ORD_DT + ORD_STAT_CD
   ========================================================= */

CREATE INDEX TB_ORDER_BAD_X03
ON TB_ORDER_BAD (CUST_ID, ORD_DT, ORD_STAT_CD)
NOLOGGING;

BEGIN
    DBMS_STATS.GATHER_TABLE_STATS(
        OWNNAME    => USER,
        TABNAME    => 'TB_ORDER_BAD',
        CASCADE    => TRUE,
        METHOD_OPT => 'FOR ALL COLUMNS SIZE 1'
    );
END;
/


/* =========================================================
   13. 클러스터링 팩터 확인: BAD + X03 추가 후
   ========================================================= */

SELECT
    I.TABLE_NAME,
    I.INDEX_NAME,
    T.NUM_ROWS,
    T.BLOCKS,
    I.LEAF_BLOCKS,
    I.CLUSTERING_FACTOR,
    ROUND(I.CLUSTERING_FACTOR / NULLIF(T.BLOCKS, 0), 2) AS CF_PER_BLOCKS,
    ROUND(I.CLUSTERING_FACTOR / NULLIF(T.NUM_ROWS, 0), 4) AS CF_PER_ROWS
FROM USER_INDEXES I
JOIN USER_TABLES T
  ON T.TABLE_NAME = I.TABLE_NAME
WHERE I.TABLE_NAME = 'TB_ORDER_BAD'
ORDER BY I.INDEX_NAME;


/* =========================================================
   14. SQL-1 실행: BAD + X03

   확인 대상:
   - ORD_STAT_CD를 인덱스에 추가했는데도 TABLE ACCESS BY INDEX ROWID가 남는지
   - X01 대비 Buffers가 얼마나 줄었는지
   - 기대만큼 줄지 않는다면 이유는 무엇인지
   ========================================================= */

SELECT /*+ GATHER_PLAN_STATISTICS INDEX(O TB_ORDER_BAD_X03) NO_BATCH_TABLE_ACCESS_BY_ROWID(O) */
       SUM(O.PAY_AMT) AS SUM_PAY_AMT
FROM   TB_ORDER_BAD O
WHERE  O.CUST_ID BETWEEN 1001 AND 2000
AND    O.ORD_DT  BETWEEN DATE '2025-01-01' AND DATE '2025-03-31'
AND    O.ORD_STAT_CD = 'PAY';

SELECT *
FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL, 'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));


/* =========================================================
   15. GOOD 테이블 생성

   같은 데이터를 CUST_ID, ORD_DT 순서로 재구성한다.
   이 작업은 ORDER BY 정렬 때문에 CPU / TEMP 사용량이 가장 클 수 있다.
   ========================================================= */

CREATE TABLE TB_ORDER_GOOD
NOLOGGING
AS
SELECT *
FROM TB_ORDER_BAD
ORDER BY CUST_ID, ORD_DT;


/* =========================================================
   16. GOOD 테이블 인덱스 생성

   BAD 테이블과 동일한 구조의 인덱스를 만든다.
   ========================================================= */

CREATE INDEX TB_ORDER_GOOD_X01
ON TB_ORDER_GOOD (CUST_ID, ORD_DT)
NOLOGGING;

CREATE INDEX TB_ORDER_GOOD_X02
ON TB_ORDER_GOOD (ORD_DT, ORD_STAT_CD)
NOLOGGING;

CREATE INDEX TB_ORDER_GOOD_X03
ON TB_ORDER_GOOD (CUST_ID, ORD_DT, ORD_STAT_CD)
NOLOGGING;


/* =========================================================
   17. GOOD 테이블 통계 수집
   ========================================================= */

BEGIN
    DBMS_STATS.GATHER_TABLE_STATS(
        OWNNAME    => USER,
        TABNAME    => 'TB_ORDER_GOOD',
        CASCADE    => TRUE,
        METHOD_OPT => 'FOR ALL COLUMNS SIZE 1'
    );
END;
/


/* =========================================================
   18. BAD / GOOD 클러스터링 팩터 비교

   확인 대상:
   - GOOD_X01은 BAD_X01보다 클러스터링 팩터가 좋아졌는가?
   - GOOD_X02는 BAD_X02보다 나빠졌는가?
   ========================================================= */

SELECT
    I.TABLE_NAME,
    I.INDEX_NAME,
    T.NUM_ROWS,
    T.BLOCKS,
    I.LEAF_BLOCKS,
    I.CLUSTERING_FACTOR,
    ROUND(I.CLUSTERING_FACTOR / NULLIF(T.BLOCKS, 0), 2) AS CF_PER_BLOCKS,
    ROUND(I.CLUSTERING_FACTOR / NULLIF(T.NUM_ROWS, 0), 4) AS CF_PER_ROWS
FROM USER_INDEXES I
JOIN USER_TABLES T
  ON T.TABLE_NAME = I.TABLE_NAME
WHERE I.TABLE_NAME IN ('TB_ORDER_BAD', 'TB_ORDER_GOOD')
ORDER BY I.INDEX_NAME, I.TABLE_NAME;


/* =========================================================
   19. SQL-1 실행: GOOD + X01

   확인 대상:
   - BAD + X01 대비 TABLE ACCESS BY INDEX ROWID의 Buffers 변화
   ========================================================= */

SELECT /*+ GATHER_PLAN_STATISTICS INDEX(O TB_ORDER_GOOD_X01) NO_BATCH_TABLE_ACCESS_BY_ROWID(O) */
       SUM(O.PAY_AMT) AS SUM_PAY_AMT
FROM   TB_ORDER_GOOD O
WHERE  O.CUST_ID BETWEEN 1001 AND 2000
AND    O.ORD_DT  BETWEEN DATE '2025-01-01' AND DATE '2025-03-31'
AND    O.ORD_STAT_CD = 'PAY';

SELECT *
FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL, 'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));


/* =========================================================
   20. SQL-1 실행: GOOD + X03

   확인 대상:
   - BAD + X03 대비 TABLE ACCESS BY INDEX ROWID의 Buffers 변화
   ========================================================= */

SELECT /*+ GATHER_PLAN_STATISTICS INDEX(O TB_ORDER_GOOD_X03) NO_BATCH_TABLE_ACCESS_BY_ROWID(O) */
       SUM(O.PAY_AMT) AS SUM_PAY_AMT
FROM   TB_ORDER_GOOD O
WHERE  O.CUST_ID BETWEEN 1001 AND 2000
AND    O.ORD_DT  BETWEEN DATE '2025-01-01' AND DATE '2025-03-31'
AND    O.ORD_STAT_CD = 'PAY';

SELECT *
FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL, 'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));


/* =========================================================
   21. SQL-2 실행: GOOD + X02

   확인 대상:
   - BAD + X02 대비 TABLE ACCESS BY INDEX ROWID의 Buffers 변화
   - CUST_ID, ORD_DT 순서 재구성이 SQL-2에 미친 영향
   ========================================================= */

SELECT /*+ GATHER_PLAN_STATISTICS INDEX(O TB_ORDER_GOOD_X02) NO_BATCH_TABLE_ACCESS_BY_ROWID(O) */
       SUM(O.PAY_AMT) AS SUM_PAY_AMT
FROM   TB_ORDER_GOOD O
WHERE  O.ORD_DT BETWEEN DATE '2025-01-01' AND DATE '2025-01-10'
AND    O.ORD_STAT_CD = 'PAY';

SELECT *
FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL, 'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));


/* =========================================================
   22. X04 커버링 인덱스 생성

   SQL-1에서 필요한 PAY_AMT까지 인덱스에 포함한다.
   ========================================================= */

CREATE INDEX TB_ORDER_BAD_X04
ON TB_ORDER_BAD (CUST_ID, ORD_DT, ORD_STAT_CD, PAY_AMT)
NOLOGGING;

CREATE INDEX TB_ORDER_GOOD_X04
ON TB_ORDER_GOOD (CUST_ID, ORD_DT, ORD_STAT_CD, PAY_AMT)
NOLOGGING;


/* =========================================================
   23. X04 생성 후 통계 수집
   ========================================================= */

BEGIN
    DBMS_STATS.GATHER_TABLE_STATS(
        OWNNAME    => USER,
        TABNAME    => 'TB_ORDER_BAD',
        CASCADE    => TRUE,
        METHOD_OPT => 'FOR ALL COLUMNS SIZE 1'
    );

    DBMS_STATS.GATHER_TABLE_STATS(
        OWNNAME    => USER,
        TABNAME    => 'TB_ORDER_GOOD',
        CASCADE    => TRUE,
        METHOD_OPT => 'FOR ALL COLUMNS SIZE 1'
    );
END;
/


/* =========================================================
   24. SQL-1 실행: BAD + X04

   확인 대상:
   - TABLE ACCESS BY INDEX ROWID가 제거되는지
   - BAD 테이블이어도 Buffers가 크게 줄어드는지
   ========================================================= */

SELECT /*+ GATHER_PLAN_STATISTICS INDEX(O TB_ORDER_BAD_X04) */
       SUM(O.PAY_AMT) AS SUM_PAY_AMT
FROM   TB_ORDER_BAD O
WHERE  O.CUST_ID BETWEEN 1001 AND 2000
AND    O.ORD_DT  BETWEEN DATE '2025-01-01' AND DATE '2025-03-31'
AND    O.ORD_STAT_CD = 'PAY';

SELECT *
FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL, 'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));


/* =========================================================
   25. SQL-1 실행: GOOD + X04

   확인 대상:
   - GOOD + X03과 비교
   - BAD + X04와 비교
   ========================================================= */

SELECT /*+ GATHER_PLAN_STATISTICS INDEX(O TB_ORDER_GOOD_X04) */
       SUM(O.PAY_AMT) AS SUM_PAY_AMT
FROM   TB_ORDER_GOOD O
WHERE  O.CUST_ID BETWEEN 1001 AND 2000
AND    O.ORD_DT  BETWEEN DATE '2025-01-01' AND DATE '2025-03-31'
AND    O.ORD_STAT_CD = 'PAY';

SELECT *
FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL, 'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));


/* =========================================================
   26. 최종 세그먼트 크기 비교

   확인 대상:
   - X04가 다른 인덱스보다 얼마나 커졌는지
   ========================================================= */

SELECT
    SEGMENT_NAME,
    SEGMENT_TYPE,
    ROUND(BYTES / 1024 / 1024, 1) AS MB
FROM USER_SEGMENTS
WHERE SEGMENT_NAME LIKE 'TB_ORDER%'
ORDER BY SEGMENT_NAME;


/* =========================================================
   27. 최종 클러스터링 팩터 비교
   ========================================================= */

SELECT
    I.TABLE_NAME,
    I.INDEX_NAME,
    T.NUM_ROWS,
    T.BLOCKS,
    I.LEAF_BLOCKS,
    I.CLUSTERING_FACTOR,
    ROUND(I.CLUSTERING_FACTOR / NULLIF(T.BLOCKS, 0), 2) AS CF_PER_BLOCKS,
    ROUND(I.CLUSTERING_FACTOR / NULLIF(T.NUM_ROWS, 0), 4) AS CF_PER_ROWS
FROM USER_INDEXES I
JOIN USER_TABLES T
  ON T.TABLE_NAME = I.TABLE_NAME
WHERE I.TABLE_NAME IN ('TB_ORDER_BAD', 'TB_ORDER_GOOD')
ORDER BY I.INDEX_NAME, I.TABLE_NAME;

```

**답변**

- [[SQLP 스터디] 3주차 - 제3장 인덱스 튜닝 1-2 Ⅹ.문제풀이](https://blog.naver.com/biyoonx/224343603076)
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
    <summary>Q. 인덱스 추가 후 조회는 빨라졌지만 운영 반영에 실패한 사례 분석</summary>
  
  한 의료기관의 `TB_MEDICAL_HISTORY` 테이블에는 최근 5년간 진단 이력 약 1억 2천만 건이 저장되어 있으며 진단이력 조회를 위해 아래와 같은 SQL이 자주 수행된다.

```sql
SELECT
       M.HISTORY_NO,
       M.MEDICAL_DT,
       M.PATIENT_NO,
       M.MEDICAL_STAT_CD,
       M.MEDICAL_AMT,
       M.DEPT_CD
FROM   TB_MEDICAL_HISTORY M
WHERE  M.MEDICAL_DT BETWEEN DATE '2025-06-01' AND DATE '2025-06-30'
AND    M.MEDICAL_STAT_CD = 'COMPLETE'
AND    M.PATIENT_NO BETWEEN 1000000 AND 1999999
ORDER BY M.MEDICAL_DT DESC,
         M.HISTORY_NO DESC;
```

현재 인덱스는 다음과 같다.

```sql
X01 : MEDICAL_DT
X02 : PATIENT_NO + MEDICAL_DT
```

운영 중 평균 응답시간은 약 18초였다.

#### 1차 튜닝

```sql
X03 : MEDICAL_DT + MEDICAL_STAT_CD --18초 → 16.8초
```

**실행계획 일부**

```
INDEX RANGE SCAN X03
A-Rows 1,800,000
Buffers 45,000

TABLE ACCESS BY INDEX ROWID TB_MEDICAL_HISTORY
A-Rows 1,650,000
Buffers 2,100,000

SORT ORDER BY
A-Rows 120,000
Buffers 2,180,000
```

#### 2차 튜닝

DBA는 PATIENT_NO 조건까지 인덱스에 포함하면 성능이 좋아질 것이라고 판단하여 다음 인덱스를 생성하였다.

```sql
X04 : MEDICAL_DT + MEDICAL_STAT_CD + PATIENT_NO --16.8초 → 15.9초
```

**실행계획 일부**

```
INDEX RANGE SCAN X04
A-Rows 1,800,000
Buffers 58,000

TABLE ACCESS BY INDEX ROWID TB_MEDICAL_HISTORY
A-Rows 120,000
Buffers 1,450,000

SORT ORDER BY
A-Rows 120,000
Buffers 1,510,000
```

#### 3차 튜닝

다른 DBA는 인덱스 컬럼 순서가 잘못되었다고 판단하여 다음 인덱스를 생성하였다.

```sql
X05 : PATIENT_NO + MEDICAL_DT + MEDICAL_STAT_CD --15.9초 → 7.5초
```

**실행계획 일부**

```
INDEX RANGE SCAN X05
A-Rows 130,000
Buffers 35,000

TABLE ACCESS BY INDEX ROWID TB_MEDICAL_HISTORY
A-Rows 120,000
Buffers 720,000

SORT ORDER BY
A-Rows 120,000
Buffers 760,000
```

#### 4차 튜닝

마지막으로 다음 인덱스를 생성하였다.

```sql
X06 : PATIENT_NO + MEDICAL_DT + MEDICAL_STAT_CD + HISTORY_NO + MEDICAL_AMT + DEPT_CD --7.5초 → 1.2초
```

**실행계획 일부**

```
INDEX RANGE SCAN X06
A-Rows 120,000
Buffers 95,000

SORT ORDER BY
A-Rows 120,000
Buffers 120,000
```

그러나 X06 적용 후 다음 문제가 발생하였다.

- 진단 등록 배치 지연
- 진단정보 수정(Update) 처리시간 증가
- 인덱스 세그먼트 크기 급증
- Buffer Cache 사용량 증가
- 일부 다른 진단 조회 SQL의 실행계획 변경

결국 운영팀은 X06을 삭제하고 X05까지만 운영에 반영하였다.

1. X03 인덱스의 성능 개선 효과가 작았던 이유를 설명하시오.
2. X04에서 `PATIENT_NO`를 추가했음에도 성능 개선 효과가 제한적이었던 이유를 설명하시오.
3. X05가 X04보다 더 개선된 이유를 설명하시오.
4. X06에서 응답시간이 크게 개선된 이유를 설명하시오.
5. X06이 조회 성능은 가장 좋았지만 운영에서 삭제된 이유를 설명하시오.
6. 운영팀이 X06 대신 X05까지만 반영한 판단이 타당한지 평가하고, 최종적으로 이 사례에서 배울 수 있는 인덱스 튜닝 원칙을 서술하시오.

**답변**

- [https://app.notion.com/p/leeeden/3-39670b7b39f480f69e7ac81416cd31d4?source=copy_link](https://app.notion.com/p/leeeden/3-39670b7b39f480f69e7ac81416cd31d4?source=copy_link)
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
    <summary>인덱스 설계와 손익분기점 문제</summary>
  
  쇼핑몰 상품 리뷰 테이블 TB_REVIEW가 있다. 현재 인덱스는 PK(REVIEW_NO)만 존재한다.

### 데이터 특성

```
전체 리뷰 건수         : 200만 건
PRD_ID(상품) distinct  : 5,000개, 상품당 평균 리뷰 약 400건
REVIEW_STAT_CD         : 'NOR'(정상) 98%, 'BLK'(차단) 2%
예외 상품 1개 (P00001) : 이벤트로 리뷰가 폭증, 6만 건 (전체의 3%, 다른 상품 평균의 150배)
```

### SQL-1. 상품 상세 화면 - 특정 상품의 정상 리뷰 평점 평균 (초당 수십 회 실행)
```sql
SELECT AVG(L.RATING)
FROM   TB_REVIEW L
WHERE  L.PRD_ID          = :prd_id
AND    L.REVIEW_STAT_CD  = 'NOR';
```

### SQL-2. 관리자 화면 - 상품별 전체 리뷰 건수 (상태 무관, 수시 조회)
```sql
SELECT COUNT(*)
FROM   TB_REVIEW L
WHERE  L.PRD_ID = :prd_id;
```

---

### 문제 1. 두 SQL을 지원하는 결합인덱스 컬럼 순서 설계

위 데이터 특성을 참고하여 SQL-1, SQL-2를 함께 지원할 결합인덱스를 설계하시오.

```
- 컬럼 구성을 (PRD_ID + REVIEW_STAT_CD)로 할지, (REVIEW_STAT_CD + PRD_ID)로 할지
  근거를 들어 정하시오.
```

### 문제 2. 실행계획 판독

문제 1에서 설계한 인덱스를 직접 생성하고, 평범한 상품(PRD_ID='P02500', 리뷰 약 400건)에 대해 SQL-1을 실행하여 실행계획을 확인하시오. (아래 실습 SQL의 STEP 3 참고)

```
- 나온 실행계획이 정상적인 Index Range Scan인지 Predicate Information을 근거로
  판단하시오.
- TABLE ACCESS 관련 오퍼레이션이 실행계획에 나타나는 이유를 설명하고, 이 단계를
  생략하려면 인덱스를 어떻게 바꾸면 되는지 설명하시오. (커버링 인덱스 개념 활용)
- Buffers 값이 크게 나오는지 작게 나오는지 확인하고, 그 이유를 인덱스 구조
  (수직적 탐색 + 수평적 탐색) 관점에서 설명하시오.
```

### 문제 3. 손익분기점 계산

동일한 인덱스로 이벤트 상품(PRD_ID='P00001', 정상 리뷰 약 58,800건)에 대해 SQL-1을 실행해보고(아래 실습 SQL의 STEP 4 참고), 문제 2의 결과와 비교하시오.

```
- 두 경우의 Buffers 차이를 직접 비교하시오.
- 인덱스 손익분기점이 무엇인지 설명하고, 왜 이런 차이가 생기는지 TABLE FULL SCAN
  (Sequential Access, Multiblock I/O)과 인덱스 ROWID를 이용한 TABLE ACCESS
  (Random Access, Single Block I/O)의 차이를 근거로 설명하시오.
- 읽어야 할 행이 전체 테이블의 몇 % 정도를 넘어서면 일반적으로 Full Scan이
  유리해지는지, 이번 실습 결과를 근거로 대략적인 감을 잡아보시오.
- 이런 상품이 섞여 있을 때 SQL 전체(모든 상품 조회)를 하나의 인덱스 전략으로만
  최적화하기 어려운 이유를 설명하시오.
```

---

### 전체 실습 SQL

```sql
/* =========================================================
   STEP 0. 기존 객체 삭제
   ========================================================= */

BEGIN
    EXECUTE IMMEDIATE 'DROP TABLE TB_REVIEW PURGE';
EXCEPTION
    WHEN OTHERS THEN
        IF SQLCODE != -942 THEN
            RAISE;
        END IF;
END;
/


/* =========================================================
   STEP 1. 테이블 생성
   ========================================================= */

CREATE TABLE TB_REVIEW
(
    REVIEW_NO       NUMBER         NOT NULL,
    PRD_ID          VARCHAR2(6)    NOT NULL,
    MBR_NO          VARCHAR2(8)    NOT NULL,
    RATING          NUMBER(1)      NOT NULL,
    REVIEW_STAT_CD  VARCHAR2(3)    NOT NULL,
    REG_DT          DATE           NOT NULL,
    REVIEW_TXT      VARCHAR2(200)
)
NOLOGGING;


/* =========================================================
   STEP 1-A. 이벤트 상품(P00001) 데이터 생성: 6만 건
   ========================================================= */

INSERT /*+ APPEND */ INTO TB_REVIEW
SELECT
    LEVEL AS REVIEW_NO,
    'P00001' AS PRD_ID,
    LPAD(TO_CHAR(MOD(LEVEL - 1, 50000) + 1), 8, '0') AS MBR_NO,
    MOD(LEVEL, 5) + 1 AS RATING,
    CASE WHEN MOD(LEVEL, 50) = 0 THEN 'BLK' ELSE 'NOR' END AS REVIEW_STAT_CD,
    DATE '2025-01-01' + MOD(LEVEL, 180) AS REG_DT,
    'review text ' || LEVEL AS REVIEW_TXT
FROM DUAL
CONNECT BY LEVEL <= 60000;

COMMIT;


/* =========================================================
   STEP 1-B. 나머지 4,999개 상품 데이터 생성: 194만 건
   ========================================================= */

-- 1번째 (1 ~ 500,000)
INSERT /*+ APPEND */ INTO TB_REVIEW
SELECT
    60000 + LEVEL AS REVIEW_NO,
    'P' || LPAD(TO_CHAR(MOD(LEVEL - 1, 4999) + 2), 5, '0') AS PRD_ID,
    LPAD(TO_CHAR(MOD(LEVEL - 1, 50000) + 1), 8, '0') AS MBR_NO,
    MOD(LEVEL, 5) + 1 AS RATING,
    CASE WHEN MOD(LEVEL, 50) = 0 THEN 'BLK' ELSE 'NOR' END AS REVIEW_STAT_CD,
    DATE '2025-01-01' + MOD(LEVEL, 180) AS REG_DT,
    'review text ' || (60000 + LEVEL) AS REVIEW_TXT
FROM DUAL
CONNECT BY LEVEL <= 500000;
COMMIT;

-- 2번째 (500,001 ~ 1,000,000)
INSERT /*+ APPEND */ INTO TB_REVIEW
SELECT
    560000 + LEVEL AS REVIEW_NO,
    'P' || LPAD(TO_CHAR(MOD(LEVEL - 1, 4999) + 2), 5, '0') AS PRD_ID,
    LPAD(TO_CHAR(MOD(LEVEL - 1, 50000) + 1), 8, '0') AS MBR_NO,
    MOD(LEVEL, 5) + 1 AS RATING,
    CASE WHEN MOD(LEVEL, 50) = 0 THEN 'BLK' ELSE 'NOR' END AS REVIEW_STAT_CD,
    DATE '2025-01-01' + MOD(LEVEL, 180) AS REG_DT,
    'review text ' || (560000 + LEVEL) AS REVIEW_TXT
FROM DUAL
CONNECT BY LEVEL <= 500000;
COMMIT;

-- 3번째 (1,000,001 ~ 1,500,000)
INSERT /*+ APPEND */ INTO TB_REVIEW
SELECT
    1060000 + LEVEL AS REVIEW_NO,
    'P' || LPAD(TO_CHAR(MOD(LEVEL - 1, 4999) + 2), 5, '0') AS PRD_ID,
    LPAD(TO_CHAR(MOD(LEVEL - 1, 50000) + 1), 8, '0') AS MBR_NO,
    MOD(LEVEL, 5) + 1 AS RATING,
    CASE WHEN MOD(LEVEL, 50) = 0 THEN 'BLK' ELSE 'NOR' END AS REVIEW_STAT_CD,
    DATE '2025-01-01' + MOD(LEVEL, 180) AS REG_DT,
    'review text ' || (1060000 + LEVEL) AS REVIEW_TXT
FROM DUAL
CONNECT BY LEVEL <= 500000;
COMMIT;

-- 4번째 (1,500,001 ~ 1,940,000)
INSERT /*+ APPEND */ INTO TB_REVIEW
SELECT
    1560000 + LEVEL AS REVIEW_NO,
    'P' || LPAD(TO_CHAR(MOD(LEVEL - 1, 4999) + 2), 5, '0') AS PRD_ID,
    LPAD(TO_CHAR(MOD(LEVEL - 1, 50000) + 1), 8, '0') AS MBR_NO,
    MOD(LEVEL, 5) + 1 AS RATING,
    CASE WHEN MOD(LEVEL, 50) = 0 THEN 'BLK' ELSE 'NOR' END AS REVIEW_STAT_CD,
    DATE '2025-01-01' + MOD(LEVEL, 180) AS REG_DT,
    'review text ' || (1560000 + LEVEL) AS REVIEW_TXT
FROM DUAL
CONNECT BY LEVEL <= 440000;
COMMIT;


/* =========================================================
   STEP 2. 데이터 및 상품별 분포 확인
   ========================================================= */

SELECT COUNT(*) AS CNT,
       COUNT(DISTINCT PRD_ID) AS CNT_PRD_ID
FROM TB_REVIEW;

SELECT PRD_ID, COUNT(*) AS CNT,
       ROUND(COUNT(*) / (SELECT COUNT(*) FROM TB_REVIEW) * 100, 2) AS PCT
FROM TB_REVIEW
WHERE PRD_ID IN ('P00001', 'P02500')
GROUP BY PRD_ID
ORDER BY CNT DESC;


/* =========================================================
   STEP 3. (직접 작성) 문제 1에서 설계한 인덱스를 만들고,
            SQL-1을 P02500 상품으로 실행하여 실행계획을 확인해보시오.

   힌트:
   - CREATE INDEX ...
   - DBMS_STATS.GATHER_TABLE_STATS(...)
   - ALTER SESSION SET STATISTICS_LEVEL = ALL;
   - SELECT /*+ GATHER_PLAN_STATISTICS */ ... (원하면 INDEX 힌트로 강제해도 됨)
   - SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL,
     'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));
 ========================================================= */

ALTER SESSION SET STATISTICS_LEVEL = ALL;

SELECT /*+ GATHER_PLAN_STATISTICS */
       AVG(L.RATING)
FROM   TB_REVIEW L
WHERE  L.PRD_ID         = 'P02500'
AND    L.REVIEW_STAT_CD = 'NOR';

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL,
'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));


/* =========================================================
   STEP 4. (직접 작성) 같은 인덱스로 P00001 상품에 대해 SQL-1을 실행해보고,
            STEP 3 결과와 Buffers를 비교해보시오.

   추가로 시도해볼 것:
   - 힌트 없이 실행했을 때 옵티마이저가 어떤 방식을 선택하는지
   - INDEX 힌트로 강제했을 때와 FULL 힌트로 강제했을 때 Buffers가 어떻게 다른지
   ========================================================= */
-- 힌트 없이 실행 (옵티마이저 선택)
SELECT /*+ GATHER_PLAN_STATISTICS */
       AVG(L.RATING)
FROM   TB_REVIEW L
WHERE  L.PRD_ID         = 'P00001'
AND    L.REVIEW_STAT_CD = 'NOR';

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL,
'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));

-- 인덱스 강제
SELECT /*+ GATHER_PLAN_STATISTICS INDEX(L TB_REVIEW_X01) */
       AVG(L.RATING)
FROM   TB_REVIEW L
WHERE  L.PRD_ID         = 'P00001'
AND    L.REVIEW_STAT_CD = 'NOR';

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL,
'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));
```

**답변**

- [https://app.notion.com/p/SQLP-3-1-398894b3ff32802391e0c9e8a85be556?source=copy_link](https://app.notion.com/p/SQLP-3-1-398894b3ff32802391e0c9e8a85be556?source=copy_link)
</details>
</dd>
</dl>
</details>

---

### 4주차 : 제3장 인덱스 튜닝(2026-07-18)
#### 제3절 인덱스 스캔 효율화
#### 제4절 인덱스 설계

<details>
  <summary>이시향🙋🏻‍♀️</summary>
  
  - [x] 주제 핵심 및 문제풀이 전략
  - [[SQLP 스터디] 4주차 - 제3장 인덱스 튜닝 3-4 Ⅰ~Ⅸ](https://blog.naver.com/biyoonx/224350422640)
  - [x] 주제에 대한 서술형 문제 및 풀이 공유

<dl>
<dd>
<details>
  <summary>대형 블로그 플랫폼 인덱스 설계</summary>
  
  ### 문제 상황

국내 대형 블로그 플랫폼을 운영하고 있다.

서비스 이용자가 증가하면서 게시글과 댓글 데이터가 급격히 증가하였고, 최근 다음과 같은 문제가 발생하였다.

일부 목록 조회 SQL의 응답 시간이 지속적으로 증가하고 있다.
관리자 조회는 데이터가 증가할수록 성능 저하가 심해지고 있다.
유사한 인덱스가 계속 추가되면서 게시글과 댓글의 `INSERT` 및 `UPDATE` 성능이 저하되고 있다.
운영팀에서는 실제 업무에 필요한 인덱스만 유지하도록 인덱스 구조를 재설계해 달라고 요청하였다.

DBA는 업무 SQL의 수행 특성과 데이터 분포를 분석하여, 인덱스 튜닝과 저장 구조 개선을 포함한 전체적인 인덱스 재설계를 요청하였다.

### 1. 데이터 특성

#### BLOG_POST
- 전체 게시글 수: 200,000,000건
- 하루 평균 게시글 등록 수: 400,000건
- 데이터는 대부분 `CREATED_AT` 순서로 입력된다.
- 공개글(`PUBLIC`): 전체의 95%
- 비공개 글(`PRIVATE`): 전체의 5%
- 공지글(`NOTICE_YN = 'Y'`): 전체의 0.1%
- 일반 블로그에는 수백 건의 게시글이 존재한다.
- 일부 유명 블로그에는 수백만 건의 게시글이 존재한다.
- 일반 작성자는 수십∼수백 건의 게시글을 작성한다.
- 일부 운영 계정과 전문 작성자는 수백만 건의 게시글을 작성한다.

#### BLOG_COMMENT
- 전체 댓글 수: 1,500,000,000건
- 하루 평균 댓글 등록 수: 8,000,000건
- 댓글은 `POST_ID`별로 매우 편중되어 있다.
- 일반 게시글의 댓글 수: 평균 10건
- 인기 게시글의 댓글 수: 최대 수백만 건
- 정상 댓글(`NORMAL`): 전체의 98%
- 삭제 댓글(`DELETED`): 전체의 2%
- 댓글 데이터도 대체로 `CREATED_AT` 순서로 입력되며, 동일 게시글의 댓글이 테이블 내에 연속해서 저장되지는 않는다.

### 2. 현재 테이블 구조

#### BLOG_POST

```sql
CREATE TABLE BLOG_POST
(
    POST_ID         NUMBER          NOT NULL,
    BLOG_ID         NUMBER          NOT NULL,
    AUTHOR_ID       NUMBER          NOT NULL,
    CATEGORY_ID     NUMBER,
    STATUS_CD       VARCHAR2(10)    NOT NULL,
    NOTICE_YN       CHAR(1)         DEFAULT 'N' NOT NULL,
    CREATED_AT      DATE            NOT NULL,
    UPDATED_AT      DATE            NOT NULL,
    VIEW_CNT        NUMBER          DEFAULT 0 NOT NULL,
    TITLE           VARCHAR2(300)   NOT NULL,
    CONTENT         CLOB,
    CONSTRAINT BLOG_POST_PK
        PRIMARY KEY (POST_ID)
);
```

#### BLOG_COMMENT

```sql
CREATE TABLE BLOG_COMMENT
(
    COMMENT_ID      NUMBER          NOT NULL,
    POST_ID         NUMBER          NOT NULL,
    AUTHOR_ID       NUMBER          NOT NULL,
    STATUS_CD       VARCHAR2(10)    NOT NULL,
    CREATED_AT      DATE            NOT NULL,
    UPDATED_AT      DATE            NOT NULL,
    CONTENT         VARCHAR2(1000)  NOT NULL,
    CONSTRAINT BLOG_COMMENT_PK
        PRIMARY KEY (COMMENT_ID)
);
```

### 3. 현재 운영 중인 인덱스

기본키 인덱스를 제외하고 다음 보조 인덱스가 운영 중이다.

#### BLOG_POST 인덱스

```sql
CREATE INDEX BLOG_POST_X01
    ON BLOG_POST
       (BLOG_ID, CREATED_AT DESC);

CREATE INDEX BLOG_POST_X02
    ON BLOG_POST
       (BLOG_ID, STATUS_CD, CREATED_AT DESC);

CREATE INDEX BLOG_POST_X03
    ON BLOG_POST
       (BLOG_ID, CATEGORY_ID, CREATED_AT DESC);

CREATE INDEX BLOG_POST_X04
    ON BLOG_POST
       (BLOG_ID, CATEGORY_ID, STATUS_CD, CREATED_AT DESC);

CREATE INDEX BLOG_POST_X05
    ON BLOG_POST
       (AUTHOR_ID, CREATED_AT DESC);

CREATE INDEX BLOG_POST_X06
    ON BLOG_POST
       (CREATED_AT);

CREATE INDEX BLOG_POST_X07
    ON BLOG_POST
       (STATUS_CD, CREATED_AT);
```

#### BLOG_COMMENT 인덱스

```sql
CREATE INDEX BLOG_COMMENT_X01
    ON BLOG_COMMENT
       (POST_ID, CREATED_AT DESC);

CREATE INDEX BLOG_COMMENT_X02
    ON BLOG_COMMENT
       (POST_ID, STATUS_CD, CREATED_AT DESC);

CREATE INDEX BLOG_COMMENT_X03
    ON BLOG_COMMENT
       (STATUS_CD, POST_ID, CREATED_AT DESC);

CREATE INDEX BLOG_COMMENT_X04
    ON BLOG_COMMENT
       (AUTHOR_ID, CREATED_AT DESC);
```

현재 운영 중인 보조 인덱스는 총 11개이다.

운영팀은 다음과 같은 문제를 제기하였다.

- `BLOG_POST_X01`과 `BLOG_POST_X02`는 선두 컬럼과 주요 용도가 유사하다.
- `BLOG_POST_X03`과 `BLOG_POST_X04`도 카테고리 목록 조회를 위해 유사하게 구성되어 있다.
- `BLOG_POST_X06`과 `BLOG_POST_X07`은 관리자 조회 외에는 거의 사용되지 않는다.
- `STATUS_CD`는 게시글과 댓글 모두 특정 값에 데이터가 편중되어 있다.
- 댓글 인덱스 역시 동일한 업무 SQL을 지원하기 위한 유사 인덱스가 중복되어 있다.
- 인덱스 추가 이후 게시글과 댓글 등록 처리 시간이 증가하였다.

### 4. 업무 SQL

#### SQL-1. 블로그 메인 최신 게시글 조회

특정 블로그의 공개 게시글 중 기준 시각보다 이전에 작성된 최신 게시글 20건을 조회한다.

```sql
SELECT POST_ID, BLOG_ID, AUTHOR_ID, CATEGORY_ID, NOTICE_YN, CREATED_AT, TITLE, VIEW_CNT
FROM BLOG_POST
WHERE BLOG_ID = :BLOG_ID
	AND STATUS_CD = 'PUBLIC'
	AND CREATED_AT < :LAST_DT
ORDER BY CREATED_AT DESC
FETCH FIRST 20 ROWS ONLY;
```

##### 업무 특성

- 초당 약 15,000회 수행
- 블로그 메인 화면의 핵심 SQL
- 첫 20건을 조회한 후 더 이상 데이터를 읽을 필요가 없다.
- 공개 게시글은 전체 게시글의 95%이다.
- `CONTENT`는 목록 화면에서 조회하지 않는다.

#### SQL-2. 카테고리별 최신 게시글 조회

특정 블로그의 특정 카테고리에 속한 공개 게시글 중 최신 게시글 20건을 조회한다.

```sql
SELECT POST_ID, BLOG_ID, AUTHOR_ID, CATEGORY_ID, CREATED_AT, TITLE, VIEW_CNT
FROM BLOG_POST
WHERE BLOG_ID = :BLOG_ID
	AND CATEGORY_ID = :CATEGORY_ID
	AND STATUS_CD = 'PUBLIC'
	AND CREATED_AT < :LAST_DT
ORDER BY CREATED_AT DESC
FETCH FIRST 20 ROWS ONLY;
```

##### 업무 특성

- 초당 약 3,000회 수행
- 하나의 블로그에는 평균 20개의 카테고리가 존재한다.
- 일부 블로그에는 500개 이상의 카테고리가 존재한다.
- 카테고리별 게시글 수의 편차가 크다.
- 첫 20건을 조회한 후 더 이상 데이터를 읽을 필요가 없다.

#### SQL-3. 게시글 상세 조회

게시글 번호를 이용해 게시글 상세 정보를 조회한다.

```sql
SELECT POST_ID, BLOG_ID, AUTHOR_ID, CATEGORY_ID, STATUS_CD, NOTICE_YN, CREATED_AT, UPDATED_AT, VIEW_CNT, TITLE, CONTENT
FROM BLOG_POST
WHERE POST_ID = :POST_ID;
```

##### 업무 특성

- 초당 약 8,000회 수행
- 항상 한 건 이하를 조회한다.
- `CONTENT` CLOB 컬럼을 포함한 게시글 전체 정보를 조회한다.
- `POST_ID`는 기본키이다.

#### SQL-4. 게시글별 최신 댓글 조회

특정 게시글의 정상 댓글 중 최신 댓글 50건을 조회한다.

```sql
SELECT COMMENT_ID, POST_ID, AUTHOR_ID, STATUS_CD, CREATED_AT, CONTENT
FROM BLOG_COMMENT
WHERE POST_ID = :POST_ID
	AND STATUS_CD = 'NORMAL'
	AND CREATED_AT < :LAST_DT
ORDER BY CREATED_AT DESC
FETCH FIRST 50 ROWS ONLY;
```

##### 업무 특성

- 초당 약 10,000회 수행
- 첫 50건을 조회한 후 더 이상 데이터를 읽을 필요가 없다.
- 정상 댓글은 전체 댓글의 98%이다.
- 일반 게시글에는 평균 10건의 댓글이 존재한다.
- 인기 게시글에는 수백만 건의 댓글이 존재한다.
- `CONTENT` 컬럼을 반드시 조회해야 한다.
- 동일 게시글의 댓글이 Heap 테이블 내에 연속적으로 저장되어 있지는 않다.

#### SQL-5. 작성자별 게시글 이력 조회

특정 작성자가 일정 기간 작성한 게시글 전체를 조회한다.

```sql
SELECT POST_ID, BLOG_ID, CATEGORY_ID, STATUS_CD, CREATED_AT, TITLE, VIEW_CNT
FROM BLOG_POST
WHERE AUTHOR_ID = :AUTHOR_ID
	AND CREATED_AT >= :FROM_DT
	AND CREATED_AT < :TO_DT
ORDER BY CREATED_AT DESC;
```

##### 업무 특성

- 분당 약 100회 수행
- 조회된 게시글 전체를 반환한다.
- 일반 작성자의 결과 건수는 수십∼수백 건이다.
- 일부 운영 계정과 전문 작성자는 조회 기간에 따라 수백만 건이 반환될 수 있다.
- 결과 건수 제한이 없으므로 부분범위 처리 효과를 기대하기 어렵다.

#### SQL-6. 관리자 기간별 게시글 추출

관리자가 일정 기간에 등록된 모든 게시글을 추출한다.

```sql
SELECT POST_ID, BLOG_ID, AUTHOR_ID, CATEGORY_ID, STATUS_CD, NOTICE_YN, CREATED_AT, UPDATED_AT, VIEW_CNT, TITLE, CONTENT
FROM BLOG_POST
WHERE CREATED_AT >= :FROM_DT
	AND CREATED_AT < :TO_DT;
```
##### 업무 특성

- 하루 1회 이하로 수행
- 1일, 7일, 30일 또는 90일 범위를 조회한다.
- 조건에 해당하는 모든 게시글을 반환한다.
- `CONTENT` CLOB 컬럼을 포함한 전체 데이터를 추출한다.
- 부분범위 처리가 불가능하다.
- 테이블 데이터는 대부분 `CREATED_AT` 순서로 적재되어 있다.

### 5. 운영 제약

- SQL 문장은 변경할 수 없다.
- 테이블의 물리 저장 구조는 변경할 수 있다.
- 기본키 인덱스를 제외하고 두 테이블에 유지할 수 있는 보조 인덱스는 합계 최대 4개이다.
- IOT를 선택하는 경우 IOT 기본키는 보조 인덱스 개수에서 제외한다.
- 기존 보조 인덱스는 필요에 따라 유지, 제거, 통합 또는 컬럼 순서 변경이 가능하다.
- 게시글 및 댓글의 `INSERT` 성능 저하가 심하므로 인덱스 개수와 인덱스 크기를 최소화해야 한다.
- SQL-1과 SQL-4는 핵심 온라인 SQL로서 성능 저하를 허용하기 어렵다.
- 관리자 조회인 SQL-6은 하루 한 번 이하로 수행되며, 일정 수준의 Full Table Scan은 허용할 수 있다.
- 특정 SQL 하나에 최적인 인덱스를 모두 생성하기보다 전체 업무 성능과 DML 부하를 종합적으로 고려해야 한다.

### 6. 검토 대상

다음 저장 구조를 비교·검토한다.

- Heap Table
- Index Organized Table(IOT)
- Index Cluster
- Hash Cluster

필요한 경우 다음 인덱스 접근 방식과 설계 요소도 함께 검토한다.

- Composite Index
- Covering Index
- Index Range Scan
- Index Range Scan Descending
- Index Skip Scan
- Index Full Scan
- Index Fast Full Scan
- Table Full Scan
- 부분범위 처리
- 인덱스 클러스터링 팩터
- 인덱스 손익분기점

### 7. 요구사항

#### 문제 1. SQL별 인덱스 접근 방식 분석

SQL-1부터 SQL-6까지 각 SQL에 대해 현재 인덱스를 사용했을 때 예상할 수 있는 Access Path를 설명하시오.

필요한 경우 다음 항목을 포함한다.

- Index Range Scan
- Index Range Scan Descending
- Table Access By Index Rowid
- Index Unique Scan
- Table Full Scan
- 정렬 연산 발생 여부

#### 문제 2. Access Predicate와 Filter Predicate 분석

현재 인덱스 및 새롭게 설계할 인덱스를 기준으로 각 SQL 조건을 다음과 같이 구분하시오.

- Index Access Predicate
- Index Filter Predicate
- Table Filter Predicate

범위 조건 뒤에 위치한 인덱스 컬럼이 스캔 범위에 미치는 영향도 함께 설명하시오.

#### 문제 3. 부분범위 처리 및 정렬 생략

SQL-1, SQL-2, SQL-4에서 다음 사항을 분석하시오.

- 부분범위 처리가 가능한가?
- 인덱스를 이용해 `ORDER BY` 정렬을 생략할 수 있는가?
- 결과 건수는 적더라도 많은 인덱스 엔트리를 읽을 가능성이 있는가?
- 조건절 컬럼과 정렬 컬럼의 순서가 부분범위 처리에 어떤 영향을 미치는가?

#### 문제 4. 인덱스 스캔 효율을 고려한 컬럼 순서 설계

각 SQL에 가장 적합한 복합 인덱스의 컬럼 구성과 순서를 설계하시오.

다음 사항을 종합적으로 고려한다.

- SQL 수행 빈도
- 컬럼 선택도
- 동등 조건과 범위 조건
- 인덱스 스캔 시작점과 종료점
- 정렬 생략
- 부분범위 처리
- 특정 값에 편중된 `STATUS_CD`
- 일반 사용자와 대량 데이터 보유 사용자의 차이

#### 문제 5. 커버링 인덱스 적용 가능성

SQL-1, SQL-2, SQL-4, SQL-5에 커버링 인덱스를 적용할 수 있는지 검토하시오.

다음 사항을 함께 설명한다.

- 테이블 랜덤 액세스 감소 효과
- `TITLE`, `CONTENT`, `VIEW_CNT`를 인덱스에 포함할 때의 영향
- 인덱스 크기 증가
- 리프 블록 수와 인덱스 높이 증가 가능성
- `INSERT` 및 `UPDATE` 부하
- 수행 빈도를 고려한 커버링 인덱스의 실익

#### 문제 6. 클러스터링 팩터와 Heap Table 검토

다음 사항을 설명하시오.

- `CREATED_AT` 인덱스와 `BLOG_ID`, `AUTHOR_ID`, `POST_ID` 선두 인덱스의 클러스터링 팩터가 서로 다를 것으로 예상되는 이유
- 클러스터링 팩터가 테이블 랜덤 액세스와 손익분기점에 미치는 영향
- 현재 Heap Table을 유지하는 것이 적절한지
- 테이블을 특정 인덱스 순서로 재구성할 경우 다른 SQL에 미치는 영향

#### 문제 7. `BLOG_COMMENT` 저장 구조 설계

BLOG_COMMENT 테이블을 다음 중 어떤 구조로 설계하는 것이 적절한지 판단하시오.

- Heap Table
- IOT
- Index Cluster
- Hash Cluster

다음 사항을 종합적으로 고려한다.

- `POST_ID`별 최신 댓글 50건 조회
- 인기 게시글의 댓글 편중
- 댓글 `INSERT` 빈도
- `COMMENT_ID`를 이용한 단건 조회·수정 가능성
- `CONTENT` 컬럼의 크기
- IOT Overflow 사용 가능성
- 보조 인덱스 추가 필요성
- 게시글과 댓글을 `POST_ID`로 클러스터링할 때의 장단점

#### 문제 8. 관리자 조회의 인덱스 손익분기점

SQL-6의 수행 결과가 다음과 같다고 가정한다.

| 조회 기간 | Index Range Scan | Full Table Scan |
| ----- | ---------------: | --------------: |
| 1일    |               4초 |             48초 |
| 7일    |              21초 |             48초 |
| 30일   |              66초 |             48초 |
| 90일   |             181초 |             48초 |

다음 사항을 설명하시오.

- 현재 환경에서 인덱스 손익분기점이 존재하는 구간
- 조회 기간이 증가할수록 Index Range Scan의 수행 시간이 급격히 증가하는 이유
- `CREATED_AT` 인덱스의 클러스터링 팩터가 양호하더라도 Full Table Scan보다 느려질 수 있는 이유
- SQL-6을 위해 `BLOG_POST_X06` 또는 `BLOG_POST_X07`을 유지해야 하는지 여부
- SQL 수행 빈도와 전체 DML 부하를 고려한 최종 판단

#### 문제 9. 최종 인덱스 및 저장 구조 재설계

DBA는 현재 인덱스 구성이 비효율적이라고 판단하였다.

문제 1부터 문제 8까지 분석한 내용을 바탕으로 `BLOG_POST`와 `BLOG_COMMENT`의 저장 구조 및 인덱스를 재설계하시오.

다음 내용을 모두 제시한다.

- 각 테이블의 최종 저장 구조
- 유지할 기존 인덱스
- 제거할 기존 인덱스
- 통합하거나 컬럼 순서를 변경할 인덱스
- 새롭게 생성할 인덱스
- 인덱스를 생성하지 않는 SQL과 그 처리 방식
- 최종 보조 인덱스 4개의 구성과 컬럼 순서
- 각 인덱스가 지원하는 업무 SQL
- 최종 설계가 조회 성능과 `INSERT`·`UPDATE` 성능에 미치는 영향

기본키를 위한 인덱스는 보조 인덱스 개수에서 제외한다.

두 테이블에 유지할 수 있는 보조 인덱스는 합계 최대 4개이다.

IOT를 선택할 경우 IOT 기본키는 보조 인덱스 개수에서 제외한다.

**답변**

- [[SQLP 스터디] 4주차 - 제3장 인덱스 튜닝 3-4 Ⅹ.문제풀이](https://blog.naver.com/biyoonx/224350422640)
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
    <summary>Q. 의료기관 월별 백업 배치의 인덱스 스캔 효율화 및 인덱스 설계</summary>
  
  한 의료정보 시스템에서는 매월 의료기관 마스터 정보를 백업 테이블에 적재한다.

원본 테이블 `TB_HPROVIDER`에는 약 7,000건의 의료기관 정보가 저장되어 있다.

백업 테이블 `TB_HPROVIDER_BKUP`에는 최근 5년간의 월별 백업 데이터 약 40만 건이 누적되어 있다.

배치 프로그램은 같은 연도와 월에 동일한 의료기관이 중복 적재되지 않도록 기존 백업 데이터의 존재 여부를 확인한 후 신규 데이터만 입력한다.

### 주요 테이블

`TB_HPROVIDER`

<img width="846" height="484" alt="Image" src="https://github.com/user-attachments/assets/cf99615b-95be-4b1d-9e2e-fc19af7a5271" />

`TB_HPROVIDER_BKUP`

<img width="1105" height="484" alt="Image" src="https://github.com/user-attachments/assets/fdfd5244-d92b-4da1-a2a0-655a6d0038e2" />

### 현재 인덱스

<img width="968" height="129" alt="Image" src="https://github.com/user-attachments/assets/2098bf8c-ff4a-4c9a-b040-0112aeb74447" />

### 기존 SQL

```sql
INSERT INTO dbo.tb_hprovider_bkup
            (c_mdins_id,
             c_bkup_yr,
             c_bkup_mm,
             c_mdins_oid,
             c_mdins_nm,
             c_mdins_cls_cd,
             c_use_yn)
SELECT H.c_mdins_id,
       Year(@STARTDATE),
       Month(@STARTDATE),
       H.c_mdins_oid,
       H.c_mdins_nm,
       H.c_mdins_cls_cd,
       H.c_use_yn
FROM   dbo.tb_hprovider H
WHERE  H.c_reg_dtm < @ENDDATE
       AND ( CONVERT(NVARCHAR, H.c_mdins_id) + '-'
             + CONVERT(NVARCHAR, Year(@STARTDATE)) + '-'
             + CONVERT(NVARCHAR, Month(@STARTDATE)) + '-'
             + H.c_mdins_oid ) NOT IN (SELECT
           CONVERT(NVARCHAR, B.c_mdins_id) + '-'
           + CONVERT(NVARCHAR, B.c_bkup_yr) + '-'
           + CONVERT(NVARCHAR, B.c_bkup_mm) + '-'
           + B.c_mdins_oid
FROM   dbo.tb_hprovider_bkup B); 
```

### 기존 실행계획 주요 형태

<img width="2048" height="683" alt="Image" src="https://github.com/user-attachments/assets/b2322c37-9f65-42b1-b27c-a1dba9328b4b" />

주요 특징은 다음과 같다.

- 백업 테이블 예상 스캔 건수: 약 40만 건
- INSERT 예상 대상 건수: 약 7천 건
- 백업 테이블 중복 확인: 2회
- 비클러스터드 인덱스 수: 5개

### 개선 SQL

```sql
DECLARE @BKUP_YR INT = Year(@STARTDATE);
DECLARE @BKUP_MM INT = Month(@STARTDATE);

INSERT INTO dbo.tb_hprovider_bkup
            (c_mdins_id,
             c_bkup_yr,
             c_bkup_mm,
             c_mdins_oid,
             c_mdins_nm,
             c_mdins_cls_cd,
             c_use_yn)
SELECT H.c_mdins_id,
       @BKUP_YR,
       @BKUP_MM,
       H.c_mdins_oid,
       H.c_mdins_nm,
       H.c_mdins_cls_cd,
       H.c_use_yn
FROM   dbo.tb_hprovider H
WHERE  H.c_reg_dtm < @ENDDATE
       AND H.c_mdins_oid IS NOT NULL
       AND NOT EXISTS (SELECT 1
                       FROM   dbo.tb_hprovider_bkup B
                       WHERE  B.c_mdins_id = H.c_mdins_id
                              AND B.c_bkup_yr = @BKUP_YR
                              AND B.c_bkup_mm = @BKUP_MM
                              AND B.c_mdins_oid = H.c_mdins_oid); 
```

### 개선 실행계획

<img width="1887" height="475" alt="Image" src="https://github.com/user-attachments/assets/3b952536-3e91-42f9-936e-827a36f91610" />

---

#### 문제 1. 인덱스가 있는데도 Scan이 발생한 이유

백업 테이블에 다음 클러스터드 인덱스가 존재한다.

```
(C_MDINS_ID, C_BKUP_YR, C_BKUP_MM, C_MDINS_OID)
```

그럼에도 기존 SQL에서 `Index Scan`이 발생한 이유를 인덱스 스캔 효율화 관점에서 설명하시오.

---

#### 문제 2. 기존 SQL의 개선

기존 SQL의 중복 확인 조건을 개선하여 작성하시오.

또한 변경된 SQL이 기존 SQL보다 효율적인 이유를 다음 관점에서 설명하시오.

- 인덱스 액세스 방식
- 스캔량
- CPU 연산
- 중복 확인 방식

---

#### 문제 3. 실행계획 기반 인덱스 선택 분석

개선 SQL의 실행계획에서는 다음과 같이 `TB_HPROVIDER_BKUP`에 대해 `IDX_HPROVIDER_BKUP_PERIOD_OID`를 이용한 Index Seek가 수행되었다.

다음 사항을 설명하시오.

1. 옵티마이저가 해당 인덱스를 선택한 이유를 설명하시오.
2. 실행계획에서 `Merge Join (Left Anti Semi Join)`이 선택된 이유를 설명하시오.
3. WHERE 절의 조건 작성 순서가 실행계획에 영향을 주는지 설명하시오.

---

#### 문제 4. 신규 인덱스 추가 여부

개선 SQL의 성능을 더 높이기 위해 다음 인덱스를 추가하려고 한다.

```sql
CREATE UNIQUE NONCLUSTERED INDEX UX_TB_HPROVIDER_BKUP_01
ON dbo.TB_HPROVIDER_BKUP
(
      C_BKUP_YR
    , C_BKUP_MM
    , C_MDINS_ID
    , C_MDINS_OID
);
```

현재 인덱스 구성에서 위 인덱스를 추가하는 것이 적절한지 판단하고 그 이유를 설명하시오.

---

#### 문제 5. 중복 인덱스 분석

다음 두 인덱스의 중복 가능성을 분석하시오.

```sql
IDX_C_REG_MDINS_OID
(
    C_MDINS_OID
)
IDX_HPROVIDER_BKUP_OID
(
    C_MDINS_OID
)
INCLUDE
(
    C_MDINS_NM
)
```

둘 중 하나를 제거할 수 있는 조건과 제거 전에 확인해야 할 사항을 설명하시오.

---

#### 문제 6. 유사한 결합 인덱스 비교

다음 두 인덱스를 비교하시오.

```sql
IDX_HPROVIDER_BKUP_PERIOD_OID
(
      C_BKUP_YR
    , C_BKUP_MM
    , C_MDINS_OID
)
INCLUDE
(
      C_MDINS_CLS_CD
    , C_MDINS_NM
)
IDX_HPROVIDER_BKUP_YR_MDINS_OID
(
      C_BKUP_YR
    , C_MDINS_OID
)
INCLUDE
(
      C_BKUP_MM
    , C_MDINS_CLS_CD
    , C_MDINS_NM
)
```

두 인덱스가 완전히 동일한 용도로 사용할 수 없는 이유를 설명하고, 각각에 적합한 검색 조건을 제시하시오.

---

#### 문제 7. INSERT와 인덱스 유지 비용

개선 후 백업 테이블 조회가 `Index Scan`에서 `Clustered Index Seek`로 변경되었지만 실행계획에는 여전히 다음 연산자가 나타난다.

- Sort
- Table Spool
- Index Insert

중복 확인 성능이 개선되었음에도 위 연산자가 남아 있는 이유를 설명하시오.

또한 비클러스터드 인덱스 개수가 INSERT 성능에 미치는 영향을 설명하시오.

---

#### 문제 8. Access Predicate와 Filter Predicate

다음 인덱스가 존재한다고 가정한다.

```sql
(C_BKUP_YR, C_BKUP_MM, C_MDINS_OID)
```

아래 조건을 수행할 때 인덱스의 액세스 조건과 필터 조건을 구분하여 설명하시오.

```sql
WHERE c_bkup_yr = 2026
AND c_bkup_mm BETWEEN 1 AND 6
AND c_mdins_oid = '1.2.410.100110.10.10000001'
```

또한 다음 인덱스 순서로 변경할 경우의 차이를 설명하시오.

```
(C_BKUP_YR, C_MDINS_OID, C_BKUP_MM)
```

---

#### 문제 9. 현재 인덱스 재설계

현재 백업 테이블에 다음 인덱스가 존재한다.

```
PK_TB_HPROVIDER_BKUP
IDX_C_REG_MDINS_OID
IDX_HPROVIDER_BKUP_OID
IDX_HPROVIDER_BKUP_PERIOD_OID
IDX_HPROVIDER_BKUP_YR_MDINS_OID
IDX_HPROVIDER_BKUP_YYYYMM_OID
```

다음 조회 유형이 주로 수행된다고 가정한다.

- 의료기관 ID와 백업 연월, OID를 이용한 중복 확인
- 특정 연월의 의료기관 목록 조회
- OID를 이용한 의료기관명 조회
- 연도와 OID를 이용한 월별 이력 조회
- 사용 여부별 연도 의료기관 조회

현재 인덱스 중 유지할 인덱스, 통합 또는 제거를 검토할 인덱스를 구분하고 인덱스 재설계 시 고려해야 할 원칙을 설명하시오.

**답변**

- [https://app.notion.com/p/leeeden/4-39d70b7b39f480a29223c34052e204ff?source=copy_link](https://app.notion.com/p/leeeden/4-39d70b7b39f480a29223c34052e204ff?source=copy_link)
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
    <summary>상품 리뷰 평점 조회 - 인덱스 스캔 효율화 및 설계 문제</summary>
  
  쇼핑몰 상품 리뷰 테이블 TB_REVIEW가 있다. 현재 아래와 같이 인덱스가 구성되어 있다.

### 현재 인덱스 구성

```sql
CREATE UNIQUE INDEX TB_REVIEW_PK  ON TB_REVIEW (REVIEW_NO);
CREATE INDEX TB_REVIEW_X01 ON TB_REVIEW (PRD_ID, REVIEW_STAT_CD);
CREATE INDEX TB_REVIEW_X02 ON TB_REVIEW (PRD_ID);
CREATE INDEX TB_REVIEW_X03 ON TB_REVIEW (REVIEW_STAT_CD, PRD_ID);
CREATE INDEX TB_REVIEW_X04 ON TB_REVIEW (PRD_ID, REVIEW_STAT_CD, RATING);
```

### 데이터 특성

```
전체 리뷰 건수         : 200만 건
PRD_ID(상품) distinct : 5,000개 (P00001 ~ P05000)
REVIEW_STAT_CD        : 'NOR'(정상) 98%, 'BLK'(차단) 2%
RATING                : 1 ~ 5
```

### SQL-1. 특정 상품 범위의 정상 리뷰 평점 평균 (초당 수십 회 실행)

```sql
SELECT AVG(RATING)
FROM   TB_REVIEW
WHERE  REVIEW_STAT_CD = 'NOR'
AND    PRD_ID BETWEEN 'P00100' AND 'P00199';
```

### SQL-2. 특정 상품의 상태별 리뷰 평점 평균 (초당 수십 회 실행)

```sql
SELECT AVG(RATING)
FROM   TB_REVIEW
WHERE  PRD_ID = 'P00100'
AND    REVIEW_STAT_CD = :stat_cd;
```

### SQL-3. 특정 상태의 전체 리뷰 평점 평균

```sql
SELECT AVG(RATING)
FROM   TB_REVIEW
WHERE  REVIEW_STAT_CD = :stat_cd;
```

---

### 문제 1. 중복 인덱스 식별

현재 인덱스 X01 ~ X04 중 SQL-1, SQL-2, SQL-3을 기준으로
제거 가능한 인덱스와 반드시 유지해야 할 인덱스를 각각 선정하고 그 이유를 아래 관점에서 서술하시오.

1. DML 부하
2. 스캔 효율
3. 유지보수 비용

---

### 문제 2. BETWEEN → IN-LIST 전환

SQL-1을 실행했을 때 아래 두 실행계획을 비교하고 물음에 답하시오.

```
[변경 전 실행계획]
| Id | Operation                     | Name          |
|  0 | SELECT STATEMENT              |               |
|  1 |  SORT AGGREGATE               |               |
|  2 |   TABLE ACCESS BY INDEX ROWID | TB_REVIEW     |
|* 3 |    INDEX RANGE SCAN           | TB_REVIEW_X01 |

Predicate Information:
  3 - access("PRD_ID" >= 'P00100' AND "PRD_ID" <= 'P00199')
      filter("REVIEW_STAT_CD" = 'NOR')

[변경 후 실행계획]
| Id | Operation                     | Name          |
|  0 | SELECT STATEMENT              |               |
|  1 |  SORT AGGREGATE               |               |
|  2 |   TABLE ACCESS BY INDEX ROWID | TB_REVIEW     |
|  3 |    INLIST ITERATOR            |               |
|* 4 |     INDEX RANGE SCAN          | TB_REVIEW_X01 |

Predicate Information:
  4 - access("PRD_ID" = 'P00100' AND "REVIEW_STAT_CD" = 'NOR')
      access("PRD_ID" = 'P00101' AND "REVIEW_STAT_CD" = 'NOR')
      ...
```

1. 변경 전 실행계획에서 `REVIEW_STAT_CD`가 `filter`로 처리되는 이유를 인덱스 스캔 범위 관점에서 설명하시오.
2. 변경 후 실행계획에서 `REVIEW_STAT_CD`가 `access`로 바뀐 이유를 IN-LIST Iterator 동작 방식과 연관지어 설명하시오.
3. IN 조건은 등치(=) 조건인지 IN-List Iterator 동작 방식을 근거로 설명하시오.

---

### 문제 3. BETWEEN vs LIKE

SQL-1의 PRD_ID 조건을 아래와 같이 변경했을 때
발생하는 문제를 설명하시오.

```sql
SELECT AVG(RATING)
FROM   TB_REVIEW
WHERE  REVIEW_STAT_CD = 'NOR'
AND    PRD_ID LIKE 'P001%';
```

1. 스캔 범위 관점에서 BETWEEN과 LIKE의 차이
2. `PRD_ID` 포맷이 고정 길이가 아닌 경우 어떤 문제가 발생하는지 설명하고 BETWEEN과의 스캔 범위 차이를 설명하시오.
3. 둘 중 권장하는 방법과 이유

---

### 문제 4. 옵션 조건 처리 방식 비교

SQL-2에서 `:stat_cd`가 옵션 조건일 때 아래 세 가지 방식으로 처리할 수 있다.
각각의 장단점을 아래 관점에 따라 비교하시오.

```sql
-- 방식 1. OR 조건
SELECT AVG(RATING)
FROM   TB_REVIEW
WHERE  PRD_ID = 'P00100'
AND   (REVIEW_STAT_CD = :stat_cd OR :stat_cd IS NULL);

-- 방식 2. NVL
SELECT AVG(RATING)
FROM   TB_REVIEW
WHERE  PRD_ID = 'P00100'
AND    REVIEW_STAT_CD = NVL(:stat_cd, REVIEW_STAT_CD);

-- 방식 3. UNION ALL
SELECT AVG(RATING)
FROM   TB_REVIEW
WHERE  PRD_ID = 'P00100'
AND    :stat_cd IS NULL
UNION ALL
SELECT AVG(RATING)
FROM   TB_REVIEW
WHERE  PRD_ID = 'P00100'
AND    REVIEW_STAT_CD = :stat_cd
AND    :stat_cd IS NOT NULL;
```

1. 인덱스 액세스 조건 사용 가능 여부
2. NULL 허용 컬럼일 때 결과 누락 여부

---

### 실습 SQL
```SQL
/* =========================================
   STEP 0. 기존 객체 삭제
   ========================================= */
BEGIN
    EXECUTE IMMEDIATE 'DROP TABLE TB_REVIEW PURGE';
EXCEPTION
    WHEN OTHERS THEN
        IF SQLCODE != -942 THEN RAISE; END IF;
END;
/

/* =========================================
   STEP 1. 테이블 생성
   ========================================= */
CREATE TABLE TB_REVIEW
(
    REVIEW_NO       NUMBER         NOT NULL,
    PRD_ID          VARCHAR2(6)    NOT NULL,
    MBR_NO          VARCHAR2(8)    NOT NULL,
    RATING          NUMBER(1)      NOT NULL,
    REVIEW_STAT_CD  VARCHAR2(3)    NOT NULL,
    REG_DT          DATE           NOT NULL,
    REVIEW_TXT      VARCHAR2(200)
) NOLOGGING;

/* =========================================
   STEP 2. 데이터 생성 (총 200만 건)
   ========================================= */
INSERT /*+ APPEND */ INTO TB_REVIEW
SELECT
    LEVEL AS REVIEW_NO,
    'P' || LPAD(TO_CHAR(MOD(LEVEL-1, 5000)+1), 5, '0') AS PRD_ID,
    LPAD(TO_CHAR(MOD(LEVEL-1, 50000)+1), 8, '0') AS MBR_NO,
    MOD(LEVEL, 5)+1 AS RATING,
    CASE WHEN MOD(LEVEL, 50) = 0 THEN 'BLK' ELSE 'NOR' END AS REVIEW_STAT_CD,
    DATE '2025-01-01' + MOD(LEVEL, 180) AS REG_DT,
    'review text ' || LEVEL AS REVIEW_TXT
FROM DUAL
CONNECT BY LEVEL <= 500000;
COMMIT;

INSERT /*+ APPEND */ INTO TB_REVIEW
SELECT
    500000 + LEVEL AS REVIEW_NO,
    'P' || LPAD(TO_CHAR(MOD(LEVEL-1, 5000)+1), 5, '0') AS PRD_ID,
    LPAD(TO_CHAR(MOD(LEVEL-1, 50000)+1), 8, '0') AS MBR_NO,
    MOD(LEVEL, 5)+1 AS RATING,
    CASE WHEN MOD(LEVEL, 50) = 0 THEN 'BLK' ELSE 'NOR' END AS REVIEW_STAT_CD,
    DATE '2025-01-01' + MOD(LEVEL, 180) AS REG_DT,
    'review text ' || (500000+LEVEL) AS REVIEW_TXT
FROM DUAL
CONNECT BY LEVEL <= 500000;
COMMIT;

INSERT /*+ APPEND */ INTO TB_REVIEW
SELECT
    1000000 + LEVEL AS REVIEW_NO,
    'P' || LPAD(TO_CHAR(MOD(LEVEL-1, 5000)+1), 5, '0') AS PRD_ID,
    LPAD(TO_CHAR(MOD(LEVEL-1, 50000)+1), 8, '0') AS MBR_NO,
    MOD(LEVEL, 5)+1 AS RATING,
    CASE WHEN MOD(LEVEL, 50) = 0 THEN 'BLK' ELSE 'NOR' END AS REVIEW_STAT_CD,
    DATE '2025-01-01' + MOD(LEVEL, 180) AS REG_DT,
    'review text ' || (1000000+LEVEL) AS REVIEW_TXT
FROM DUAL
CONNECT BY LEVEL <= 500000;
COMMIT;

INSERT /*+ APPEND */ INTO TB_REVIEW
SELECT
    1500000 + LEVEL AS REVIEW_NO,
    'P' || LPAD(TO_CHAR(MOD(LEVEL-1, 5000)+1), 5, '0') AS PRD_ID,
    LPAD(TO_CHAR(MOD(LEVEL-1, 50000)+1), 8, '0') AS MBR_NO,
    MOD(LEVEL, 5)+1 AS RATING,
    CASE WHEN MOD(LEVEL, 50) = 0 THEN 'BLK' ELSE 'NOR' END AS REVIEW_STAT_CD,
    DATE '2025-01-01' + MOD(LEVEL, 180) AS REG_DT,
    'review text ' || (1500000+LEVEL) AS REVIEW_TXT
FROM DUAL
CONNECT BY LEVEL <= 500000;
COMMIT;

/* =========================================
   STEP 3. 인덱스 생성
   ========================================= */
CREATE UNIQUE INDEX TB_REVIEW_PK
    ON TB_REVIEW (REVIEW_NO);
CREATE INDEX TB_REVIEW_X01
    ON TB_REVIEW (PRD_ID, REVIEW_STAT_CD) NOLOGGING;
CREATE INDEX TB_REVIEW_X02
    ON TB_REVIEW (PRD_ID) NOLOGGING;
CREATE INDEX TB_REVIEW_X03
    ON TB_REVIEW (REVIEW_STAT_CD, PRD_ID) NOLOGGING;
CREATE INDEX TB_REVIEW_X04
    ON TB_REVIEW (PRD_ID, REVIEW_STAT_CD, RATING) NOLOGGING;

/* =========================================
   STEP 4. 통계 수집
   ========================================= */
BEGIN
    DBMS_STATS.GATHER_TABLE_STATS(
        OWNNAME    => USER,
        TABNAME    => 'TB_REVIEW',
        CASCADE    => TRUE,
        METHOD_OPT => 'FOR ALL COLUMNS SIZE 1'
    );
END;
/

/* =========================================
   STEP 5. 데이터 분포 확인
   ========================================= */
SELECT COUNT(*) AS TOTAL_CNT
FROM   TB_REVIEW;

SELECT REVIEW_STAT_CD,
       COUNT(*) AS CNT,
       ROUND(COUNT(*) / (SELECT COUNT(*) FROM TB_REVIEW) * 100, 2) AS PCT
FROM   TB_REVIEW
GROUP BY REVIEW_STAT_CD;

SELECT COUNT(DISTINCT PRD_ID) AS PRD_CNT
FROM   TB_REVIEW;

/* =========================================
   STEP 6. 문제 2 - BETWEEN vs IN-LIST
   ========================================= */
ALTER SESSION SET STATISTICS_LEVEL = ALL;

-- [변경 전] BETWEEN
SELECT /*+ GATHER_PLAN_STATISTICS INDEX(T TB_REVIEW_X01) */
       AVG(RATING)
FROM   TB_REVIEW T
WHERE  REVIEW_STAT_CD = 'NOR'
AND    PRD_ID BETWEEN 'P00100' AND 'P00199';

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL,
'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));

-- [변경 후] IN-LIST
SELECT /*+ GATHER_PLAN_STATISTICS INDEX(T TB_REVIEW_X01) */
       AVG(RATING)
FROM   TB_REVIEW T
WHERE  REVIEW_STAT_CD = 'NOR'
AND    PRD_ID IN (
    'P00100','P00101','P00102','P00103','P00104',
    'P00105','P00106','P00107','P00108','P00109',
    'P00110','P00111','P00112','P00113','P00114',
    'P00115','P00116','P00117','P00118','P00119',
    'P00120','P00130','P00140','P00150','P00199'
);

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL,
'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));

/* =========================================
   STEP 7. 문제 3 - BETWEEN vs LIKE
   ========================================= */

-- LIKE 사용
SELECT /*+ GATHER_PLAN_STATISTICS INDEX(T TB_REVIEW_X01) */
       AVG(RATING)
FROM   TB_REVIEW T
WHERE  REVIEW_STAT_CD = 'NOR'
AND    PRD_ID LIKE 'P001%';

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL,
'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));

-- BETWEEN 사용
SELECT /*+ GATHER_PLAN_STATISTICS INDEX(T TB_REVIEW_X01) */
       AVG(RATING)
FROM   TB_REVIEW T
WHERE  REVIEW_STAT_CD = 'NOR'
AND    PRD_ID BETWEEN 'P00100' AND 'P00199';

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL,
'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));

-- 실제 조회 범위 확인
SELECT COUNT(DISTINCT PRD_ID) AS LIKE_CNT
FROM   TB_REVIEW
WHERE  PRD_ID LIKE 'P001%';

SELECT COUNT(DISTINCT PRD_ID) AS BETWEEN_CNT
FROM   TB_REVIEW
WHERE  PRD_ID BETWEEN 'P00100' AND 'P00199';

/* =========================================
   STEP 8. 문제 4 - 옵션 조건 처리 방식 비교
   ========================================= */

-- 방식 1. OR 조건 (:stat_cd = 'NOR' 입력 시)
SELECT /*+ GATHER_PLAN_STATISTICS */
       AVG(RATING)
FROM   TB_REVIEW
WHERE  PRD_ID = 'P00100'
AND   (REVIEW_STAT_CD = 'NOR' OR 'NOR' IS NULL);

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL,
'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));

-- 방식 1. OR 조건 (:stat_cd = NULL 미입력 시)
SELECT /*+ GATHER_PLAN_STATISTICS */
       AVG(RATING)
FROM   TB_REVIEW
WHERE  PRD_ID = 'P00100'
AND   (REVIEW_STAT_CD = NULL OR NULL IS NULL);

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL,
'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));

-- 방식 2. NVL (:stat_cd = 'NOR' 입력 시)
SELECT /*+ GATHER_PLAN_STATISTICS */
       AVG(RATING)
FROM   TB_REVIEW
WHERE  PRD_ID = 'P00100'
AND    REVIEW_STAT_CD = NVL('NOR', REVIEW_STAT_CD);

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL,
'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));

-- 방식 2. NVL (:stat_cd = NULL 미입력 시)
SELECT /*+ GATHER_PLAN_STATISTICS */
       AVG(RATING)
FROM   TB_REVIEW
WHERE  PRD_ID = 'P00100'
AND    REVIEW_STAT_CD = NVL(NULL, REVIEW_STAT_CD);

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL,
'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));

-- 방식 3. UNION ALL (:stat_cd = 'NOR' 입력 시)
SELECT /*+ GATHER_PLAN_STATISTICS */
       AVG(RATING)
FROM   TB_REVIEW
WHERE  PRD_ID = 'P00100'
AND    'NOR' IS NULL
UNION ALL
SELECT AVG(RATING)
FROM   TB_REVIEW
WHERE  PRD_ID = 'P00100'
AND    REVIEW_STAT_CD = 'NOR'
AND    'NOR' IS NOT NULL;

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL,
'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));

-- 방식 3. UNION ALL (:stat_cd = NULL 미입력 시)
SELECT /*+ GATHER_PLAN_STATISTICS */
       AVG(RATING)
FROM   TB_REVIEW
WHERE  PRD_ID = 'P00100'
AND    NULL IS NULL
UNION ALL
SELECT AVG(RATING)
FROM   TB_REVIEW
WHERE  PRD_ID = 'P00100'
AND    REVIEW_STAT_CD = NULL
AND    NULL IS NOT NULL;

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL,
'ALLSTATS LAST +PREDICATE +ALIAS +NOTE'));
```

**답변**

- [[SQLP] 제3장(2) 문제 및 풀이](https://app.notion.com/p/SQLP-3-2-3a0894b3ff328055ba85e7e252d390c6?source=copy_link)
</details>
</dd>
</dl>
</details>

---

### 5주차 : 제4장 조인 튜닝(2026-07-26)
#### 제1절 NL 조인
#### 제2절 소트 머지 조인
#### 제3절 해시 조인
#### 제4절 스칼라 서브쿼리
#### 제5절 고급 조인 기법

<details>
  <summary>이시향🙋🏻‍♀️</summary>
  
  - [x] 주제 핵심 및 문제풀이 전략
  - [[SQLP 스터디] 5주차 - 제4장 조인 튜닝 Ⅰ~Ⅸ](https://m.blog.naver.com/biyoonx/224357799010)
  - [x] 주제에 대한 서술형 문제 및 풀이 공유

<dl>
<dd>
<details>
  <summary>판매 당시 상품가격 조회 및 정산</summary>
  
  ### 문제 상황

### 1. 테이블 및 데이터 특성

#### `SALE_TXN`

```sql
CREATE TABLE SALE_TXN
(
    SALE_ID       NUMBER        NOT NULL,
    CUSTOMER_ID   NUMBER        NOT NULL,
    PRODUCT_ID    NUMBER        NOT NULL,
    SALE_DTM      DATE          NOT NULL,
    SALE_QTY      NUMBER        NOT NULL,
    SALE_AMT      NUMBER        NOT NULL,
    STATUS_CD     VARCHAR2(2)   NOT NULL,
    CONSTRAINT SALE_TXN_PK PRIMARY KEY (SALE_ID)
);
```

- 전체 3억 건
- 일평균 50만 건
- 한 달 조회 시 약 1,500만 건
- 고객 1명의 최근 3개월 판매 건수는 평균 30건
- `STATUS_CD = '01'`인 정상 판매가 전체의 95%

#### `PRODUCT`

```sql
CREATE TABLE PRODUCT
(
    PRODUCT_ID    NUMBER        NOT NULL,
    CATEGORY_ID   NUMBER        NOT NULL,
    PRODUCT_NM    VARCHAR2(200) NOT NULL,
    USE_YN        CHAR(1)       NOT NULL,
    CONSTRAINT PRODUCT_PK PRIMARY KEY (PRODUCT_ID)
);
```

- 전체 50만 건
- 대부분 사용 중
- 모든 `SALE_TXN.PRODUCT_ID`에 대응하는 `PRODUCT` 행이 존재함

#### `PRODUCT_PRICE_HIST`

```sql
CREATE TABLE PRODUCT_PRICE_HIST
(
    PRODUCT_ID    NUMBER       NOT NULL,
    VALID_FROM    DATE         NOT NULL,
    VALID_TO      DATE         NOT NULL,
    SALE_PRICE    NUMBER       NOT NULL,
    CONSTRAINT PRODUCT_PRICE_HIST_PK
        PRIMARY KEY (PRODUCT_ID, VALID_FROM)
);
```

- 전체 1,500만 건
- 상품당 평균 30개의 가격이력
- 유효기간은 `[VALID_FROM, VALID_TO)` 형식
- 동일 상품의 이력 구간은 중복되지 않음
- 가격이력은 판매 시점 전체에 대해 빠짐없이 존재함

```sql
CREATE INDEX SALE_TXN_X01
    ON SALE_TXN (CUSTOMER_ID, SALE_DTM DESC, SALE_ID DESC);

CREATE INDEX SALE_TXN_X02
    ON SALE_TXN (SALE_DTM);
```

---

### 문제 1. 소량 조회와 NL 조인

#### 업무 요구사항

특정 고객의 최근 정상 판매 20건에 대해 상품명과 판매 당시 적용 가격을 조회한다.

- 기존 SQL

```sql
SELECT SALE_ID,
       SALE_DTM,
       PRODUCT_ID,
       PRODUCT_NM,
       SALE_QTY,
       SALE_PRICE
FROM (
    SELECT S.SALE_ID,
           S.SALE_DTM,
           S.PRODUCT_ID,
           P.PRODUCT_NM,
           S.SALE_QTY,
           H.SALE_PRICE,
           ROW_NUMBER() OVER (
               ORDER BY S.SALE_DTM DESC, S.SALE_ID DESC
           ) AS RN
    FROM SALE_TXN S
         JOIN PRODUCT P
           ON P.PRODUCT_ID = S.PRODUCT_ID
         JOIN PRODUCT_PRICE_HIST H
           ON H.PRODUCT_ID = S.PRODUCT_ID
          AND S.SALE_DTM >= H.VALID_FROM
          AND S.SALE_DTM <  H.VALID_TO
    WHERE S.CUSTOMER_ID = :CUSTOMER_ID
      AND S.STATUS_CD = '01'
      AND S.SALE_DTM >= ADD_MONTHS(SYSDATE, -3)
)
WHERE RN <= 20
ORDER BY SALE_DTM DESC, SALE_ID DESC;
```

- 출제 질문
1. 이 SQL에서 가장 적합한 조인 방식과 조인 순서를 설명하시오.
2. 상품 및 가격이력 조인 전에 판매 20건을 먼저 확정하도록 SQL을 개선하시오.
3. `PRODUCT_PRICE_HIST_PK(PRODUCT_ID, VALID_FROM)`가 선분이력 검색에 어떻게 사용되는지 설명하시오.
4. 상위 20건을 먼저 추출해도 결과가 동일하기 위한 전제조건을 설명하시오.

---

### 문제 2. 대량 집계와 해시 조인

#### 업무 요구사항

한 달 동안 발생한 정상 판매를 상품 카테고리별로 집계한다.

- 기존 SQL

```sql
SELECT P.CATEGORY_ID,
       COUNT(*) AS SALE_CNT,
       SUM(S.SALE_QTY) AS SALE_QTY,
       SUM(S.SALE_AMT) AS SALE_AMT
FROM SALE_TXN S
     JOIN PRODUCT P
       ON P.PRODUCT_ID = S.PRODUCT_ID
WHERE S.SALE_DTM >= :FROM_DT
  AND S.SALE_DTM <  :TO_DT
  AND S.STATUS_CD = '01'
GROUP BY P.CATEGORY_ID;
```

- 기존 실행 특성
	- SALE_TXN 조건 결과: 1,400만 건
	- PRODUCT PK 탐색 Starts: 1,400만 회
	- PRODUCT 테이블 랜덤 액세스: 약 1,400만 회
	- 최종 결과: 카테고리 120건

- 출제 질문
1. 현재 NL 조인이 비효율적인 이유를 실행통계에 근거하여 설명하시오.
2. 적절한 조인 방식과 Build Input을 설명하시오.
3. `SALE_TXN_X02(SALE_DTM)`를 이용한 Index Range Scan과 Full Table Scan의 비용을 비교할 때 확인해야 할 요소를 설명하고, 현재 정보만으로 어느 방식이 유리하다고 단정할 수 있는지 논하시오.

---

### 문제 3. 선분이력과 소트 머지 조인

#### 업무 요구사항

최근 1년간 전체 판매에 대해 판매 당시 적용된 상품가격을 연결하여 정산자료를 생성한다.

- SQL

```sql
SELECT S.SALE_ID,
       S.PRODUCT_ID,
       S.SALE_DTM,
       S.SALE_QTY,
       H.SALE_PRICE,
       S.SALE_QTY * H.SALE_PRICE AS CALC_AMT
FROM SALE_TXN S
     JOIN PRODUCT_PRICE_HIST H
       ON H.PRODUCT_ID = S.PRODUCT_ID
      AND S.SALE_DTM >= H.VALID_FROM
      AND S.SALE_DTM <  H.VALID_TO
WHERE S.SALE_DTM >= :FROM_DT
  AND S.SALE_DTM <  :TO_DT
  AND S.STATUS_CD = '01';
```

- 기존 실행통계 예시

```text
------------------------------------------------------------------------------------------------
| Id | Operation              | Starts | E-Rows | A-Rows | Buffers  |
------------------------------------------------------------------------------------------------
|  0 | SELECT STATEMENT       |      1 |        |  170M  | 9,500,000|
|* 1 |  HASH JOIN             |      1 |   180M |  170M  | 9,500,000|
|* 2 |   TABLE ACCESS FULL    |      1 |    15M |   15M  |   450,000|
|* 3 |   TABLE ACCESS FULL    |      1 |   170M |  170M  | 9,050,000|
------------------------------------------------------------------------------------------------

Predicate Information
---------------------------------------------------
1 - access("H"."PRODUCT_ID" = "S"."PRODUCT_ID")
1 - filter("S"."SALE_DTM" >= "H"."VALID_FROM"
           AND "S"."SALE_DTM" < "H"."VALID_TO")
```

- 추가 정보
	- 상품당 평균 가격이력은 30건
	- 해시 조인의 Access Predicate는 `PRODUCT_ID`뿐
	- 해시 버킷에서 동일한 `PRODUCT_ID`를 가진 가격이력 평균 30건이 판매 1건의 후보가 되며, 각 후보에 대해 기간 조건이 평가됨
	- 논리적인 후보 비교 및 기간 조건 평가 횟수는 수십억 회까지 증가할 수 있음

- 출제 질문
1. 해시 조인의 Access Predicate와 Filter Predicate를 구분하여 설명하시오.
2. 해시 조인에서 최종 결과 건수보다 과도하게 많은 이력 후보에 대해 기간 조건이 평가되는 이유를 설명하시오.
3. 가격이력 중 조회 기간과 겹치는 선분만 먼저 추출하도록 SQL을 개선하시오.
4. 이 조인에서 소트 머지 조인 또는 Band Join을 검토할 수 있는 이유를 설명하고, 입력 집합 정렬 비용까지 고려하여 해시 조인보다 유리할 수 있는 조건을 설명하시오.
5. 조회 대상이 특정 상품군의 하루 판매 약 3,000건으로 축소되는 경우, 전체 상품의 1년 조회와 비교하여 적합한 조인 방식이 달라질 수 있는 이유를 설명하시오.

---

### 문제 4. 선분이력 자체를 만드는 문제

- 변경점 이력

```sql
CREATE TABLE PRODUCT_PRICE_CHANGE
(
    PRODUCT_ID    NUMBER NOT NULL,
    CHANGE_DTM    DATE   NOT NULL,
    SALE_PRICE    NUMBER NOT NULL,
    CONSTRAINT PRODUCT_PRICE_CHANGE_PK
        PRIMARY KEY (PRODUCT_ID, CHANGE_DTM)
);
```

- 데이터 저장 형태

| PRODUCT_ID | CHANGE_DTM | SALE_PRICE |
|------------|------------|-----------:|
| 100        | 2026-01-01 | 10,000원   |
| 100        | 2026-03-01 | 12,000원   |
| 100        | 2026-06-15 | 11,000원   |

- 추가 정보
  - 전체 1,500만 건
  - 상품당 평균 30개의 가격 변경이력
  - 동일 상품에 동일한 `CHANGE_DTM`을 가진 이력은 존재하지 않음
  - 최초 가격부터 현재 가격까지의 변경 시점만 저장하며 종료일은 별도로 관리하지 않음

- 출제 질문
1. 변경점 이력을 선분이력으로 변환한 후 판매 당시 가격을 조회하도록 SQL을 작성하시오.
2. 매번 1,500만 건에 `LEAD`를 수행하면 어떤 비용이 발생하는지 설명하시오.
3. 선분이력을 매번 계산하지 않고 별도 테이블로 관리하는 방안의 장단점을 설명하시오.
4. 종료일을 `DATE '9999-12-31'`로 관리하는 방식과 `NULL`로 관리하는 방식의 차이를 설명하시오.
5. 기간 조건에서 `BETWEEN` 대신 `>= VALID_FROM AND < VALID_TO`를 사용하는 이유를 설명하시오.

**답변**

- [[SQLP 스터디] 5주차 - 제4장 조인 튜닝 Ⅹ.문제풀이](https://m.blog.naver.com/biyoonx/224357799010)
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
  <summary>Q. 환자 진료 및 입원/처방 환경에서의 조인 튜닝</summary>
  
  ### 주요 테이블

1.  환자 마스터 : `TB_PATIENT`
    - 데이터 규모 : 100만 건
    - PK : PATIENT_ID
2. 진료 트랜잭션 : `TB_TREATMENT`
    - 데이터 규모 : 5,000만 건
    - PK : TREATMENT_ID
    - FK : PATIENT_ID, DOCTOR_ID
    - 데이터 분포 : 환자 1명당 평균 50건의 진료 내역 보유
3.  입원 내역 : `TB_ADMISSION`
    - 데이터 규모 : 200만 건
    - PK : ADMISSION_ID
    - FK : PATIENT_ID
    - 데이터 분포 : 전체 환자 100만 명 중 입원 경험이 있는 환자는 약 10만 명 (10% 수준)
4. 처방 상세 : `TB_PRESCRIPTION`
    - 데이터 규모 : 1억 5,000만 건
    - PK : PRESCRIPTION_ID
    - FK : TREATMENT_ID
    - 데이터 분포 : 진료 1건당 평균 3건의 약제/처방 내역 발생 (1:N 관계)
5. 의사 마스터 : `TB_DOCTOR_MASTER`
    - 데이터 규모 : 5,000건
    - PK : DOCTOR_ID
    - 재직 의사 : WORK_STATUS = 'Y'는 4,000건
6. 진료과 마스터 : `TB_DEPARTMENT`
    - 데이터 규모 : 100건
    - PK : DEPT_CD

### 주요 인덱스

```sql
TB_PATIENT_PK          (PATIENT_ID)
TB_PATIENT_X01         (REG_DATE, PATIENT_ID)

TB_ADMISSION_X01       (PATIENT_ID, ADMIT_DT)
TB_ADMISSION_X02       (ADMIT_DT, PATIENT_ID)

TB_TREATMENT_X01       (PATIENT_ID, TREATMENT_DTM, TREATMENT_ID)
TB_TREATMENT_X02       (DOCTOR_ID, TREATMENT_DTM)

TB_PRESCRIPTION_X01    (TREATMENT_ID, DRUG_CD)
TB_PRESCRIPTION_X02    (DRUG_CD, TREATMENT_ID)

TB_DOCTOR_MASTER_X01   (DEPT_CD, WORK_STATUS, DOCTOR_ID)
```

---

#### 문제 1. 다중 1:N 조인의 행 증폭과 세미 조인 전환

2026년에 입원한 이력이 있고, 같은 해에 특정 약제 `D001`을 처방받은 적이 있는 환자의 중복 없는 목록을 조회한다.

```sql
SELECT DISTINCT
       P.PATIENT_ID,
       P.PATIENT_NM
FROM TB_PATIENT P
JOIN TB_ADMISSION A
  ON A.PATIENT_ID = P.PATIENT_ID
JOIN TB_TREATMENT T
  ON T.PATIENT_ID = P.PATIENT_ID
JOIN TB_PRESCRIPTION R
  ON R.TREATMENT_ID = T.TREATMENT_ID
WHERE A.ADMIT_DT >= DATE '2026-01-01'
  AND A.ADMIT_DT <  DATE '2027-01-01'
  AND T.TREATMENT_DTM >= DATE '2026-01-01'
  AND T.TREATMENT_DTM <  DATE '2027-01-01'
  AND R.DRUG_CD = 'D001';
```

동일 환자에게 입원 이력이 여러 건 있고 `D001` 처방 이력도 여러 건 존재하면, 환자별 입원 건수와 처방 건수의 조합만큼 중간 결과가 증가한다. 이후 `DISTINCT`로 환자 중복을 제거하면서 정렬 또는 해시 기반 중복 제거 부하가 발생한다.

1. 조인 조건이 모두 존재함에도 중간 결과가 크게 증가하는 이유를 집합 관점에서 설명하시오.
2. `DISTINCT`를 제거하고 `EXISTS`를 이용해 존재 여부만 확인하도록 SQL을 재작성하시오.
3. `EXISTS`를 사용하면 항상 행별 조기 종료 방식으로 실행되는지 설명하시오.

---

#### 문제 2. Outer Join 이후 집계와 선집계 튜닝

전체 진료과별로 재직 의사 수와 최근 1개월 총 진료비를 조회한다. 재직 의사가 없거나 진료가 없는 진료과도 출력해야 한다.

```sql
SELECT D.DEPT_CD,
       COUNT(DISTINCT M.DOCTOR_ID) AS DOCTOR_CNT,
       SUM(T.TREATMENT_COST)       AS TOTAL_COST
FROM TB_DEPARTMENT D
LEFT JOIN TB_DOCTOR_MASTER M
  ON M.DEPT_CD = D.DEPT_CD
 AND M.WORK_STATUS = 'Y'
LEFT JOIN TB_TREATMENT T
  ON T.DOCTOR_ID = M.DOCTOR_ID
 AND T.TREATMENT_DTM >= :FROM_DT
 AND T.TREATMENT_DTM <  :TO_DT
GROUP BY D.DEPT_CD;
```

최근 한 달 진료 데이터는 약 900만 건이다.

1. 의사와 진료 데이터를 먼저 조인한 뒤 `COUNT(DISTINCT)`와 `GROUP BY`를 수행할 때 발생하는 집합 팽창을 설명하시오.
2. `TB_TREATMENT`를 의사별로 먼저 집계한 뒤 의사 마스터와 조인하도록 SQL을 개선하시오.
3. 선집계 방식에서도 전체 진료과와 진료 없는 의사가 누락되지 않게 하려면 무엇을 주의해야 하는지 설명하시오.

---

#### 문제 3. 비병합 집계 뷰와 조건절 푸시

특정 환자의 기본 정보와 누적 진료비를 조회한다.

```sql
SELECT P.PATIENT_ID,
       P.PATIENT_NM,
       V.TOTAL_COST
FROM TB_PATIENT P
JOIN (
    SELECT PATIENT_ID,
           SUM(TREATMENT_COST) AS TOTAL_COST
    FROM TB_TREATMENT
    GROUP BY PATIENT_ID
) V
  ON V.PATIENT_ID = P.PATIENT_ID
WHERE P.PATIENT_ID = :PATIENT_ID;
```

실제 실행계획을 확인한 결과, 인라인 뷰에서 `TB_TREATMENT` 5,000만 건 전체를 환자별로 집계한 뒤 특정 환자 한 명과 조인하는 계획이 선택되었다고 가정한다.

1. View Merging과 Predicate Pushing의 차이를 설명하시오.
2. 집계 뷰가 Merge되지 않더라도 상위의 환자 조건이 내부로 전달될 수 있는지 설명하시오.
3. 전체 집계를 확실하게 방지하도록 SQL을 리팩토링하시오.
4. 상관 스칼라 서브쿼리로 변경할 경우 유리한 조건과 불리한 조건을 설명하시오.

---

#### 문제 4. NOT EXISTS Unnesting과 Anti Join

2025년 이후 가입한 환자 중 2026년 이후 입원 이력이 없는 외래 전용 환자를 조회한다.

```sql
SELECT P.PATIENT_ID,
       P.PATIENT_NM,
       P.PHONE_NO
FROM TB_PATIENT P
WHERE P.REG_DATE >= DATE '2025-01-01'
  AND NOT EXISTS (
      SELECT /*+ QB_NAME(SQ) NO_UNNEST */ 1
      FROM TB_ADMISSION A
      WHERE A.PATIENT_ID = P.PATIENT_ID
        AND A.ADMIT_DT >= DATE '2026-01-01'
  );
```

실행계획에서 외부 환자 후보는 50만 건이며, 서브쿼리 Row Source의 Starts가 약 50만 회로 확인되었다고 가정한다.

실제 실행 통계 일부는 다음과 같다.

```sql
--------------------------------------------------------------------------------
| Id | Operation                           | Starts | A-Rows | Buffers           |
--------------------------------------------------------------------------------
|  1 | FILTER                              |      1 | 450000 | 1800000           |
|  2 |  TABLE ACCESS BY INDEX ROWID PATIENT|      1 | 500000 |  600000           |
|  3 |   INDEX RANGE SCAN PATIENT_X01      |      1 | 500000 |  100000           |
|  4 |  INDEX RANGE SCAN ADMISSION_X01     | 500000 |  50000 | 1200000           |
--------------------------------------------------------------------------------
```

1. `NOT EXISTS`가 Unnesting될 때 Anti Join으로 변환되는 원리를 설명하시오.
2. Unnesting되지 않고 FILTER 방식으로 처리될 때 Starts가 증가하는 이유를 설명하시오.
3. NO_UNNEST를 제거한 SQL과 명시적 Anti Join 재작성 SQL을 각각 작성하시오.
4. Hash Anti Join이 항상 FILTER 또는 Nested Loops Anti Join보다 좋은지 설명하시오.
5. INDEX RANGE SCAN ADMISSION_X01의 A-Rows는 5만 건인데 Starts는 50만 건인 이유를 설명하시오.

**답변**

- [https://app.notion.com/p/leeeden/4-3a670b7b39f480968dafdf02765751c2?source=copy_link](https://app.notion.com/p/leeeden/4-3a670b7b39f480968dafdf02765751c2?source=copy_link)
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
  <summary>해시 조인 / 스칼라 서브쿼리 튜닝</summary>
  
  ### 데이터 특성

```
주문    테이블 : 일별 약 100만건, 누적 약 3억건
반품    테이블 : 일별 약 10만건,  누적 약 3천만건
고객    테이블 : 총 10만명 (고객번호 NDV = 10만)
VIP고객 테이블 : 총 1만명
```

### 테이블 및 인덱스 구성

```
주문    : 주문_PK    (주문일자, 고객번호)
반품    : 반품_PK    (반품일자, 고객번호)
고객    : 고객_PK    (고객번호)
VIP고객 : VIP고객_PK (고객번호)
```

### 상황

```
운영팀으로부터 월별 주문/반품 현황 집계 쿼리가 매우 느리다는 신고가 들어왔다.
담당자는 아래와 같이 두 차례 튜닝을 시도했으나 여전히 성능이 개선되지 않고 있다.
```

### 현재 쿼리

```sql
SELECT a.고객번호,
       b.고객명,
       SUM(a.주문금액) AS 주문금액합계,
       SUM(c.반품금액) AS 반품금액합계
FROM   주문 a,
       고객 b,
       반품 c
WHERE  a.고객번호  = b.고객번호
AND    a.고객번호  = c.고객번호(+)
AND    a.주문일자  BETWEEN :시작일자 AND :종료일자
AND    c.반품일자  BETWEEN :시작일자 AND :종료일자
GROUP BY a.고객번호, b.고객명
ORDER BY 주문금액합계 DESC;
```

### 실행계획 1 (현재)

```sql
------------------------------------------------------------------------------------------------------
| Id  | Operation                     | Name    | E-Rows  | E-Bytes | Cost (%CPU)  | Time     |
------------------------------------------------------------------------------------------------------
|   0 | SELECT STATEMENT              |         |  100000 |    6M   |  3820K  (3)  | 12:42:00 |
|   1 |  SORT ORDER BY                |         |  100000 |    6M   |  3820K  (3)  | 12:42:00 |
|   2 |   HASH GROUP BY               |         |  100000 |    6M   |  3820K  (3)  | 12:42:00 |
|   3 |    NESTED LOOPS OUTER         |         |  30000K |    1G   |  3820K  (3)  | 12:42:00 |
|   4 |     NESTED LOOPS              |         |  30000K |  900M   |  1910K  (2)  | 06:22:00 |
|*  5 |      TABLE ACCESS FULL        | 주문    |  30000K |  570M   |   955K  (1)  | 03:11:00 |
|   6 |      TABLE ACCESS BY ROWID    | 고객    |       1 |      26 |       2 (0)  | 00:00:01 |
|*  7 |       INDEX UNIQUE SCAN       | 고객_PK |       1 |         |       1 (0)  | 00:00:01 |
|*  8 |     TABLE ACCESS FULL         | 반품    |   3000K |      48M|       2 (0)  | 00:00:04 |
------------------------------------------------------------------------------------------------------

Predicate Information (identified by operation id):
---------------------------------------------------
   5 - filter("A"."주문일자" BETWEEN :시작일자 AND :종료일자)
   7 - access("A"."고객번호" = "B"."고객번호")
   8 - filter("C"."고객번호"(+) = "A"."고객번호"
           AND "C"."반품일자"(+) BETWEEN :시작일자 AND :종료일자)
```

### 1차 튜닝 - 인덱스 추가

```sql
CREATE INDEX 주문_IDX01 ON 주문 (주문일자, 고객번호, 주문금액);
CREATE INDEX 반품_IDX01 ON 반품 (반품일자, 고객번호, 반품금액);
```

### 실행계획 2 (1차 튜닝 후)

```sql
------------------------------------------------------------------------------------------------------
| Id  | Operation                     | Name       | E-Rows  | E-Bytes | Cost (%CPU)  | Time     |
------------------------------------------------------------------------------------------------------
|   0 | SELECT STATEMENT              |            |  100000 |    6M   |  1250K  (3)  | 04:10:00 |
|   1 |  SORT ORDER BY                |            |  100000 |    6M   |  1250K  (3)  | 04:10:00 |
|   2 |   HASH GROUP BY               |            |  100000 |    6M   |  1250K  (3)  | 04:10:00 |
|   3 |    NESTED LOOPS OUTER         |            |  30000K |    1G   |  1250K  (3)  | 04:10:00 |
|   4 |     NESTED LOOPS              |            |  30000K |  900M   |   625K  (2)  | 02:05:00 |
|*  5 |      INDEX RANGE SCAN         | 주문_IDX01 |  30000K |  570M   |   310K  (1)  | 01:02:00 |
|   6 |      TABLE ACCESS BY ROWID    | 고객       |       1 |      26 |       2 (0)  | 00:00:01 |
|*  7 |       INDEX UNIQUE SCAN       | 고객_PK    |       1 |         |       1 (0)  | 00:00:01 |
|*  8 |      INDEX RANGE SCAN         | 반품_IDX01 |   3000K |     48M |       2 (0)  | 00:00:04 |
------------------------------------------------------------------------------------------------------

Predicate Information (identified by operation id):
---------------------------------------------------
   5 - access("A"."주문일자" BETWEEN :시작일자 AND :종료일자)
   7 - access("A"."고객번호" = "B"."고객번호")
   8 - access("C"."반품일자"(+) BETWEEN :시작일자 AND :종료일자)
       filter("C"."고객번호"(+) = "A"."고객번호")
```

### 2차 튜닝 - 해시 조인으로 변경

```sql
SELECT /*+ USE_HASH(a b c) */
       a.고객번호,
       b.고객명,
       SUM(a.주문금액) AS 주문금액합계,
       SUM(c.반품금액) AS 반품금액합계
FROM   주문 a,
       고객 b,
       반품 c
WHERE  a.고객번호  = b.고객번호
AND    a.고객번호  = c.고객번호(+)
AND    a.주문일자  BETWEEN :시작일자 AND :종료일자
AND    c.반품일자  BETWEEN :시작일자 AND :종료일자
GROUP BY a.고객번호, b.고객명
ORDER BY 주문금액합계 DESC;
```

### 실행계획 3 (2차 튜닝 후)

```sql
------------------------------------------------------------------------------------------------------
| Id  | Operation                     | Name       | E-Rows  | E-Bytes | Cost (%CPU)  | Time     |
------------------------------------------------------------------------------------------------------
|   0 | SELECT STATEMENT              |            |  100000 |    6M   |   850K  (5)  | 02:50:00 |
|   1 |  SORT ORDER BY                |            |  100000 |    6M   |   850K  (5)  | 02:50:00 |
|   2 |   HASH GROUP BY               |            |  100000 |    6M   |   850K  (5)  | 02:50:00 |
|*  3 |    HASH JOIN OUTER            |            |  30000K |    1G   |   820K  (5)  | 02:44:00 |
|   4 |     HASH JOIN                 |            |  30000K |  900M   |   410K  (4)  | 01:22:00 |
|*  5 |      INDEX RANGE SCAN         | 주문_IDX01 |  30000K |  570M   |   310K  (1)  | 01:02:00 |
|   6 |      TABLE ACCESS FULL        | 고객       |  100000 |    2M   |    50K  (1)  | 00:10:00 |
|*  7 |     INDEX RANGE SCAN          | 반품_IDX01 |   3000K |     48M |   100K  (1)  | 00:20:00 |
------------------------------------------------------------------------------------------------------

Predicate Information (identified by operation id):
---------------------------------------------------
   3 - access("A"."고객번호" = "C"."고객번호"(+))
       filter("C"."반품일자"(+) BETWEEN :시작일자 AND :종료일자)
   4 - access("A"."고객번호" = "B"."고객번호")
   5 - access("A"."주문일자" BETWEEN :시작일자 AND :종료일자)
   7 - access("C"."반품일자" BETWEEN :시작일자 AND :종료일자)
```

---

### 문제

1. 실행계획 1에서 주문 테이블에 TABLE ACCESS FULL이 발생한 이유

2. 1차 튜닝(인덱스 추가) 후 실행계획 2에서 Cost는 감소했으나
   여전히 느린 이유를 아래 관점에서 설명하시오.
   - NL 조인과 대량 데이터의 관계
   - 반품 테이블 Predicate Information에서 filter가 발생한 이유와 그 영향

3. 2차 튜닝(해시 조인) 후 실행계획 3에서도 여전히 느릴 수 있는 이유를
   아래 관점에서 설명하시오.
   - 해시 조인의 동작 방식 (Build Input / Probe Input)
   - PGA 부족 시 발생하는 문제

4. 해시 조인 성능을 높이기 위한 Build Input과 Probe Input 선택 기준을 설명하고
   현재 실행계획 3에서 조인 순서가 적절한지 판단하여
   힌트와 함께 개선 쿼리를 작성하시오.

5. 고객명을 조인 대신 아래와 같이 스칼라 서브쿼리로 변경했을 때의
   장단점을 설명하고 현재 데이터 특성(고객번호 NDV = 10만)에서
   캐싱 효과가 효율적인지 판단하시오.

```sql
   SELECT a.고객번호,
          (SELECT 고객명 FROM 고객 WHERE 고객번호 = a.고객번호) AS 고객명,
          SUM(a.주문금액) AS 주문금액합계,
          SUM(c.반품금액) AS 반품금액합계
   FROM   주문 a,
          반품 c
   WHERE  a.고객번호  = c.고객번호(+)
   AND    a.주문일자  BETWEEN :시작일자 AND :종료일자
   AND    c.반품일자  BETWEEN :시작일자 AND :종료일자
   GROUP BY a.고객번호
   ORDER BY 주문금액합계 DESC;
```

6. 아래 EXISTS 서브쿼리에서 Unnesting과 No-Unnesting의
   실행계획 차이를 설명하고 각각 유리한 상황을 서술하시오.

```sql
   SELECT a.고객번호,
          SUM(a.주문금액) AS 주문금액합계
   FROM   주문 a
   WHERE  a.주문일자 BETWEEN :시작일자 AND :종료일자
   AND    EXISTS (SELECT 1 FROM VIP고객 WHERE 고객번호 = a.고객번호)
   GROUP BY a.고객번호
   ORDER BY 주문금액합계 DESC;
```

**답변**

- [https://app.notion.com/p/SQLP-4-3a7894b3ff3280348ae8e0503223f37b?source=copy_link](https://app.notion.com/p/SQLP-4-3a7894b3ff3280348ae8e0503223f37b?source=copy_link)
</details>
</dd>
</dl>
</details>

---

### 6주차 : 제5장 SQL 옵티마이저(2026-08-01)
#### 제1절 SQL 옵티마이저 원리
#### 제2절 SQL 공유 및 재사용
#### 제3절 쿼리 변환

### 제6장 고급 SQL 튜닝
#### 제1절 소트 튜닝

<details>
  <summary>최수연🙋🏻‍♀️</summary>

  - [x] 주제에 대한 서술형 문제 및 풀이 공유

<dl>
<dd>
<details>
    <summary>소트 튜닝 + 쿼리 변환</summary>
  
  ### 데이터 특성

```
주문    테이블 : 전체 500만건, 최근 1년 데이터
고객번호 NDV   : 100,100명
                 - 일반 고객 100,000명 : 1인당 평균 40건 (총 400만건)
                 - 헤비유저      100명 : 1인당 평균 10,000건 (총 100만건)
주문상태       : COMPLETE 95%, CANCEL 5%
```

### 테이블 및 인덱스 구성

```sql
CREATE TABLE 주문
(
    주문번호   NUMBER        NOT NULL,
    고객번호   VARCHAR2(10)  NOT NULL,
    주문일자   DATE          NOT NULL,
    주문상태   VARCHAR2(10)  NOT NULL,
    주문금액   NUMBER        NOT NULL,
    CONSTRAINT 주문_PK PRIMARY KEY (주문번호)
);

CREATE INDEX 주문_X01 ON 주문 (고객번호, 주문상태, 주문일자 DESC);
```

### 상황

```
쇼핑몰 고객 상세 페이지에서 "최근 주문 내역 TOP 10"을 보여주는 쿼리가
고객마다 응답 속도 편차가 심하다는 신고가 들어왔다.
```

### 현재 쿼리

```sql
SELECT 주문번호, 주문일자, 주문금액, 주문상태
FROM   주문
WHERE  고객번호 = :cust_no
AND   (주문상태 = :status OR :status IS NULL)
ORDER BY 주문일자 DESC
FETCH FIRST 10 ROWS ONLY;
```

### 실행계획 1 (일반 고객, :status = 'COMPLETE' 로 조회)

```sql
------------------------------------------------------------------------------
| Id  | Operation                     | Name       | E-Rows | Cost (%CPU) |
------------------------------------------------------------------------------
|   0 | SELECT STATEMENT              |            |     10 |      12 (0) |
|*  1 |  SORT ORDER BY STOPKEY        |            |     10 |      12 (0) |
|   2 |   TABLE ACCESS BY INDEX ROWID | 주문       |     38 |      11 (0) |
|*  3 |    INDEX RANGE SCAN           | 주문_X01   |     40 |       3 (0) |
------------------------------------------------------------------------------

Predicate Information (identified by operation id):
---------------------------------------------------
   1 - filter(ROWNUM <= 10)
   3 - access("고객번호" = :CUST_NO)
       filter("주문상태" = :STATUS OR :STATUS IS NULL)
```

일반 고객이 조회했을 때는 큰 지연 없이 수행되었다.

### 실행계획 1-1 (헤비유저, :status = 'COMPLETE' 로 조회 - 동일 쿼리)

```sql
------------------------------------------------------------------------------
| Id  | Operation                     | Name       | E-Rows | Cost (%CPU) |
------------------------------------------------------------------------------
|   0 | SELECT STATEMENT              |            |     10 |    3500 (0) |
|*  1 |  SORT ORDER BY STOPKEY        |            |     10 |    3500 (0) |
|   2 |   TABLE ACCESS BY INDEX ROWID | 주문       |   9500 |    2750 (0) |
|*  3 |    INDEX RANGE SCAN           | 주문_X01   |  10000 |     750 (0) |
------------------------------------------------------------------------------

Predicate Information (identified by operation id):
---------------------------------------------------
   1 - filter(ROWNUM <= 10)
   3 - access("고객번호" = :CUST_NO)
       filter("주문상태" = :STATUS OR :STATUS IS NULL)
```

반면 헤비유저가 동일한 쿼리로 조회했을 때는 체감 성능이 크게 저하되었다.

---

### 1차 조치 - OR 조건을 제거하고 상태값을 필수 파라미터로 변경

```sql
SELECT 주문번호, 주문일자, 주문금액, 주문상태
FROM   주문
WHERE  고객번호 = :cust_no
AND    주문상태 = :status
ORDER BY 주문일자 DESC
FETCH FIRST 10 ROWS ONLY;
```

### 실행계획 2 (일반 고객, OR 제거, :status = 'COMPLETE')

```sql
------------------------------------------------------------------------------
| Id  | Operation                     | Name       | E-Rows | Cost (%CPU) |
------------------------------------------------------------------------------
|   0 | SELECT STATEMENT              |            |     10 |       4 (0) |
|*  1 |  COUNT STOPKEY                |            |        |             |
|   2 |   TABLE ACCESS BY INDEX ROWID | 주문       |     38 |       4 (0) |
|*  3 |    INDEX RANGE SCAN           | 주문_X01   |     38 |       3 (0) |
------------------------------------------------------------------------------

Predicate Information (identified by operation id):
---------------------------------------------------
   1 - filter(ROWNUM <= 10)
   3 - access("고객번호" = :CUST_NO AND "주문상태" = :STATUS)
```

### 실행계획 2-1 (헤비유저, OR 제거, :status = 'COMPLETE')

```sql
------------------------------------------------------------------------------
| Id  | Operation                     | Name       | E-Rows | Cost (%CPU) |
------------------------------------------------------------------------------
|   0 | SELECT STATEMENT              |            |     10 |       4 (0) |
|*  1 |  COUNT STOPKEY                |            |        |             |
|   2 |   TABLE ACCESS BY INDEX ROWID | 주문       |   9500 |       4 (0) |
|*  3 |    INDEX RANGE SCAN           | 주문_X01   |   9500 |       3 (0) |
------------------------------------------------------------------------------

Predicate Information (identified by operation id):
---------------------------------------------------
   1 - filter(ROWNUM <= 10)
   3 - access("고객번호" = :CUST_NO AND "주문상태" = :STATUS)
```

1차 조치 이후에는 일반 고객과 헤비유저 모두 Cost가 4로 동일해졌고, 
실제 체감 성능도 고객 구분 없이 즉시 응답하는 수준으로 균일해졌다.

---

### 문제

1. 실행계획 1에서 `SORT ORDER BY STOPKEY` 가 발생하는 이유를 아래 항목을 포함하여 설명하시오.
   - TABLE ACCESS BY INDEX ROWID 단계 E-Rows(38)의 예측 근거
   - `"주문상태 = :STATUS OR :STATUS IS NULL"` 조건이  access가 아닌 filter로 처리되는 이유와 OR-Expansion으로 처리되지 않는 이유

2. 실행계획 1(일반 고객, Cost 12)과 실행계획 1-1(헤비유저, Cost 3500)을 비교하여, 같은 쿼리인데도 고객에 따라 응답 속도 편차가 발생하는 이유를 `SORT ORDER BY STOPKEY` 의 동작 방식과 연관지어 설명하시오.

3. OR 조건 제거 후 실행계획 2에서 `SORT ORDER BY` 가 사라지고 `COUNT STOPKEY` 만 남는 이유를 `주문_X01` 인덱스 구조와 연관지어 설명하시오.

4. 실행계획 2와 실행계획 2-1을 비교하면, 1차 조치 이후에는 대상 건수가 크게 다름에도 Cost가 동일하게 나타난다. 이 현상을 `COUNT STOPKEY` 의 부분범위 처리 원리로 설명하고, 문제 2번에서 확인한 `SORT ORDER BY STOPKEY` 와의 근본적인 차이를 근거로, SQL 튜닝 시 정렬 컬럼과 인덱스 컬럼 순서를 어떻게 설계해야 하는지 일반적인 원칙을 제시하시오.

5. 아래는 동일 인덱스(주문_X01)를 사용하는 또 다른 쿼리와 그 실행계획이다.
    
    ```sql
    SELECT 주문번호, 주문일자, 주문금액, 주문상태
    FROM   주문
    WHERE  고객번호 = :cust_no
    AND   (주문상태 = 'COMPLETE' OR 주문일자 = DATE '2026-08-01')
    ORDER BY 주문일자 DESC
    FETCH FIRST 10 ROWS ONLY;
    ```
    
    ```sql
    ------------------------------------------------------------------------------
    | Id  | Operation                     | Name       | E-Rows | Cost (%CPU) |
    ------------------------------------------------------------------------------
    |   0 | SELECT STATEMENT              |            |     10 |       6 (0) |
    |*  1 |  SORT ORDER BY STOPKEY        |            |     10 |       6 (0) |
    |   2 |   CONCATENATION               |            |        |             |
    |   3 |    TABLE ACCESS BY INDEX ROWID| 주문       |     38 |       4 (0) |
    |*  4 |     INDEX RANGE SCAN          | 주문_X01   |     38 |       3 (0) |
    |   5 |    TABLE ACCESS BY INDEX ROWID| 주문       |      1 |       2 (0) |
    |*  6 |     INDEX RANGE SCAN          | 주문_X01   |     40 |       3 (0) |
    ------------------------------------------------------------------------------
    
    Predicate Information (identified by operation id):
    ---------------------------------------------------
       1 - filter(ROWNUM <= 10)
       4 - access("고객번호" = :CUST_NO AND "주문상태" = 'COMPLETE')
       6 - access("고객번호" = :CUST_NO)
           filter("주문일자" = DATE '2026-08-01'
                  AND LNNVL("주문상태" = 'COMPLETE'))
    ```
    
    - 이 쿼리에서 OR-Expansion이 발생할 수 있었던 이유를 문제 1의 쿼리와 비교하여 설명하시오.
    - 두 번째 브랜치(Id 5, 6)의 Predicate Information에 LNNVL 함수가 사용된 이유를 설명하시오.

**답변**

- [[SQLP] 제5장&6장(1) 문제 및 풀이](https://app.notion.com/p/SQLP-5-6-1-3af894b3ff3280f8af7cca9a2413c053?source=copy_link)
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
    <summary>Q. 대용량 진료 이력 조회 환경에서의 SQL 옵티마이저 분석 및 소트 튜닝</summary>
  
  ### 업무 요구사항

최근 1년간 완료된 진료를 기준으로 다음 정보를 조회한다.

- 환자번호, 환자명, 환자별 총 진료비
- 가장 최근 진료번호, 가장 최근 진료일시, 가장 최근 진료과명
- 총 진료비가 높은 순으로 상위 100명

정렬 우선순위는 다음과 같다.

1. 총 진료비 내림차순
2. 최근 진료일시 내림차순
3. 환자번호 내림차순

### 주요 테이블

1. 환자 마스터 : `TB_PATIENT`
    - 데이터 규모 : 1,000,000건
    - PATIEND ID : 환자번호 / PATIENT_NM : 환자명
2. 진료 이력 : `TB_TREATMENT`
    - 데이터 규모 : 120,000,000건
    - 최근 1년 완료 진료 : 12,000,000건
    - 최근 1년 진료 환자 : 850,000명
    - TREATMENT_ID : 진료번호 / PATIENT_ID : 환자번호 / TREATMENT_DTM : 진료일시 / TREATMENT_COST : 진료비 / TREATMENT_STAT_CD : 진료상태 / DEPT_CD : 진료과 코드
3. 진료과 : `TB_DEPARTMENT`
    - 데이터 규모 : 300건
    - DEPT_CD : 진료과 코드 / DEPT_NM : 진료과명

### 기존 SQL

```sql
SELECT DISTINCT
       X.PATIENT_ID,
       X.PATIENT_NM,
       X.TOTAL_COST,
       X.TREATMENT_ID,
       X.TREATMENT_DTM,
       D.DEPT_NM
FROM (
    SELECT P.PATIENT_ID,
           P.PATIENT_NM,
           T.TREATMENT_ID,
           T.TREATMENT_DTM,
           T.DEPT_CD,
           SUM(T.TREATMENT_COST)
               OVER (
                   PARTITION BY T.PATIENT_ID
               ) AS TOTAL_COST,
           ROW_NUMBER()
               OVER (
                   PARTITION BY T.PATIENT_ID
                   ORDER BY T.TREATMENT_DTM DESC,
                            T.TREATMENT_ID DESC
               ) AS RN
    FROM TB_PATIENT P
    JOIN TB_TREATMENT T
      ON T.PATIENT_ID = P.PATIENT_ID
    WHERE T.TREATMENT_STAT_CD = 'COMPLETE'
      AND T.TREATMENT_DTM >= ADD_MONTHS(TRUNC(SYSDATE), -12)
) X
JOIN TB_DEPARTMENT D
  ON D.DEPT_CD = X.DEPT_CD
WHERE X.RN = 1
ORDER BY X.TOTAL_COST DESC,
         X.TREATMENT_DTM DESC,
         X.PATIENT_ID DESC
FETCH FIRST 100 ROWS ONLY;
```

### 실행계획 및 실행 통계

```sql
-------------------------------------------------------------------------------------------------------
| Id | Operation                        | Starts | A-Rows | Buffers  | TempSpc | A-Time             |
-------------------------------------------------------------------------------------------------------
|  0 | SELECT STATEMENT                 |      1 |    100 | 1,420,000|         | 00:06:18           |
|  1 |  SORT ORDER BY STOPKEY           |      1 |    100 | 1,420,000|   210M  | 00:06:18           |
|  2 |   HASH UNIQUE                    |      1 | 850,000| 1,420,000|   620M  | 00:06:02           |
|  3 |    HASH JOIN                     |      1 | 850,000| 1,420,000|         | 00:05:41           |
|  4 |     TABLE ACCESS FULL DEPARTMENT |      1 |    300 |       12|         | 00:00:01           |
|  5 |     VIEW                         |      1 | 850,000| 1,419,988|         | 00:05:40           |
|  6 |      WINDOW SORT PUSHED RANK     |      1 |  12.0M| 1,419,988|    18G  | 00:05:32           |
|  7 |       HASH JOIN                  |      1 |  12.0M| 1,419,988|         | 00:01:19           |
|  8 |        TABLE ACCESS FULL PATIENT |      1 |   1.0M|    41,000|         | 00:00:06           |
|  9 |        TABLE ACCESS FULL TREATMENT
|                                        |      1 |  12.0M| 1,378,988|         | 00:01:08           |
-------------------------------------------------------------------------------------------------------
```

---

#### 문제 1.

현재 실행계획에서 전체 수행시간에 가장 큰 영향을 미치는 연산을 선정하고 그 이유를 설명하시오.

또한 실행계획에서 `WINDOW SORT PUSHED RANK`의 출력 건수(A-Rows 약 12,000,000건)와 `VIEW` 연산의 출력 건수(약 850,000건)를 근거로 옵티마이저가 Cardinality를 어떻게 계산하고 이후 조인 방식을 결정하는지 설명하시오.

아울러 `TB_PATIENT`와 `TB_TREATMENT`의 조인에서 옵티마이저가 `HASH JOIN`을 선택한 이유를 처리 건수와 Cost 관점에서 기술하시오.

---

#### 문제 2.

현재 SQL에서 `HASH UNIQUE`가 발생한 원인을 설명하고, 결과를 변경하지 않는 범위 내에서 이를 제거하도록 SQL을 수정하시오.

수정한 SQL을 기준으로 다음 사항을 설명하시오.

- `HASH UNIQUE`가 제거되는 이유
- 분석 함수가 포함된 인라인 뷰에서 View Merging이 제한되는 이유
- DISTINCT 제거가 실행계획과 TEMP 사용량에 미치는 영향

---

#### 문제 3.

현재 SQL은 분석 함수를 이용하여 12,000,000건의 진료 데이터를 유지한 상태에서 환자별 집계를 수행한다.

동일한 결과를 반환하도록 SQL을 재작성하시오.

단,

- 환자별 총 진료비
- 가장 최근 진료
- 가장 최근 진료과

정보는 모두 유지되어야 하며, 동일한 진료일시에서는 진료번호가 가장 큰 건을 최근 진료로 판단한다.

작성한 SQL을 기준으로 기존 방식과 비교하여 Cardinality 감소 시점이 어떻게 달라지는지 설명하고, 옵티마이저가 `HASH GROUP BY`를 선택할 가능성이 높은 이유를 기술하시오.

---

#### 문제 4.

문제 3에서 작성한 SQL을 적용하였다고 가정할 때 실행계획이 어떻게 변경될지 설명하시오.

다음 사항을 중심으로 기술하시오.

- Cardinality 감소 시점
- Join 입력 건수 변화
- Sort 입력 건수 변화
- PGA 및 TEMP 사용량 변화

또한 `TB_TREATMENT`는 여전히 전체 12,000,000건을 읽는데도 전체 수행시간이 단축되는 이유를 설명하시오.

---

#### 문제 5.

현재 SQL은 환자별 집계 결과 약 850,000건을 모두 조인한 후 최종 Top-N을 수행한다.

정렬 기준이 모두 환자별 집계 결과에 존재한다는 점을 이용하여 Top-N을 먼저 수행하도록 SQL을 재작성하시오.

또한 기존 방식과 비교하여 아래 관점에서 성능 향상 효과를 설명하시오.

- 조인 처리량
- `SORT ORDER BY STOPKEY`
- Hard Parse
- Soft Parse
- 바인드 변수 사용에 따른 SQL 공유 및 재사용

단, 진료상태별 데이터 분포가 크게 다른 경우 하나의 실행계획을 계속 재사용할 때 발생할 수 있는 문제도 함께 기술하시오.

**답변**

- [https://app.notion.com/p/leeeden/5-3ac70b7b39f4802c89fefe779ec93d6b?source=copy_link](https://app.notion.com/p/leeeden/5-3ac70b7b39f4802c89fefe779ec93d6b?source=copy_link)
</details>
</dd>
</dl>
</details>

<details>
  <summary>이시향🙋🏻‍♀️</summary>
  
  - [x] 주제 핵심 및 문제풀이 전략
  - [[SQLP 스터디] 6주차 - 제5장 SQL 옵티마이저, 제6장 고급 SQL 튜닝 1 : Ⅰ-Ⅸ](https://blog.naver.com/biyoonx/224367161423)
  - [x] 주제에 대한 서술형 문제 및 풀이 공유

<dl>
<dd>
<details>
  <summary>Top-N 조회와 소트 튜닝</summary>
  
  ### 업무 상황

특정 지역에서 지정한 기간 동안 발생한 정상 주문 중 주문금액이 큰 상위 100건을 조회한다.

최근 조회 시간이 급격히 증가하고 TEMP 사용량이 커져 튜닝이 필요하다.

### 테이블 및 데이터 특성

#### ORDER_TXN

* 전체 3억 건
* 일평균 주문 50만 건
* `STATUS_CD = '01'`인 정상 주문은 전체의 95%
* 지역별 주문 분포의 편차가 큼
* 현재 바인드 조건에 해당하는 실제 주문은 약 800만 건

```sql
CREATE TABLE ORDER_TXN
(
    ORDER_NO      NUMBER       NOT NULL,
    CUST_ID       NUMBER       NOT NULL,
    PRODUCT_ID    NUMBER       NOT NULL,
    REGION_CD     VARCHAR2(2)  NOT NULL,
    STATUS_CD     VARCHAR2(2)  NOT NULL,
    ORDER_DTM     DATE         NOT NULL,
    ORDER_AMT     NUMBER       NOT NULL,
    CONSTRAINT ORDER_TXN_PK PRIMARY KEY (ORDER_NO)
);
```

#### CUSTOMER

* 전체 500만 건
* `ADDRESS` 평균 길이 약 300바이트

```sql
CREATE TABLE CUSTOMER
(
    CUST_ID       NUMBER          NOT NULL,
    CUST_NM       VARCHAR2(100)   NOT NULL,
    ADDRESS       VARCHAR2(1000),
    CONSTRAINT CUSTOMER_PK PRIMARY KEY (CUST_ID)
);
```

#### PRODUCT

* 전체 100만 건
* `PRODUCT_DESC` 평균 길이 약 2,000바이트

```sql
CREATE TABLE PRODUCT
(
    PRODUCT_ID    NUMBER          NOT NULL,
    PRODUCT_NM    VARCHAR2(200)   NOT NULL,
    PRODUCT_DESC  VARCHAR2(4000),
    CONSTRAINT PRODUCT_PK PRIMARY KEY (PRODUCT_ID)
);
```

### 인덱스

```sql
CREATE INDEX ORDER_TXN_X01
    ON ORDER_TXN
       (REGION_CD, STATUS_CD, ORDER_DTM);

CREATE INDEX ORDER_TXN_X02
    ON ORDER_TXN
       (REGION_CD, STATUS_CD, ORDER_AMT DESC, ORDER_DTM);
```

### 현재 SQL

```sql
SELECT ORDER_NO,
       CUST_ID,
       PRODUCT_ID,
       ORDER_DTM,
       ORDER_AMT,
       CUST_NM,
       ADDRESS,
       PRODUCT_NM,
       PRODUCT_DESC
FROM (
    SELECT O.ORDER_NO,
           O.CUST_ID,
           O.PRODUCT_ID,
           O.ORDER_DTM,
           O.ORDER_AMT,
           C.CUST_NM,
           C.ADDRESS,
           P.PRODUCT_NM,
           P.PRODUCT_DESC,
           ROW_NUMBER() OVER (
               ORDER BY O.ORDER_AMT DESC, O.ORDER_NO
           ) AS RN
    FROM ORDER_TXN O
    JOIN CUSTOMER C
      ON C.CUST_ID = O.CUST_ID
    JOIN PRODUCT P
      ON P.PRODUCT_ID = O.PRODUCT_ID
    WHERE O.REGION_CD = :REGION_CD
      AND O.STATUS_CD = '01'
      AND O.ORDER_DTM >= :FROM_DTM
      AND O.ORDER_DTM <  :TO_DTM
)
WHERE RN <= 100
ORDER BY ORDER_AMT DESC, ORDER_NO;
```

### 실행계획 및 수행통계

```text
------------------------------------------------------------------------------------------------
| Id | Operation                         | Name          | E-Rows | A-Rows  | Used-Tmp |
------------------------------------------------------------------------------------------------
|  0 | SELECT STATEMENT                  |               |        |     100 |          |
|  1 |  SORT ORDER BY                    |               |    100 |     100 |          |
|  2 |   VIEW                            |               |    100 |     100 |          |
|  3 |    WINDOW SORT PUSHED RANK        |               | 120000 |     100 |     18GB |
|  4 |     HASH JOIN                     |               | 120000 | 8000000 |          |
|  5 |      HASH JOIN                    |               | 120000 | 8000000 |          |
|  6 |       TABLE ACCESS BY INDEX ROWID | ORDER_TXN     | 120000 | 8000000 |          |
|  7 |        INDEX RANGE SCAN           | ORDER_TXN_X01 | 120000 | 8000000 |          |
|  8 |       TABLE ACCESS FULL           | CUSTOMER      |  5000K |   5000K |          |
|  9 |      TABLE ACCESS FULL            | PRODUCT       |  1000K |   1000K |          |
------------------------------------------------------------------------------------------------
```

```text
Operation                 OMem    1Mem    Used-Mem    Used-Tmp
WINDOW SORT PUSHED RANK   180MB   180MB   160MB       18GB
```

옵티마이저는 조회 대상 주문을 12만 건으로 예상했으나 실제 처리 건수는 800만 건이었다.

### 문제

현재 SQL과 실행통계를 분석하여 성능 저하의 주요 원인을 설명하고 SQL을 개선하시오.

다음 두 가지 실행 전략을 모두 검토하고, 각 전략이 유리한 조건과 불리한 조건을 설명하시오.

1. 기존 인덱스의 정렬 순서를 이용하여 별도의 대량 소트 없이 상위 100건을 조회하는 방안
2. 조건에 해당하는 주문을 정렬해야 하는 경우 Workarea와 TEMP 사용량을 줄이는 방안

필요하면 인덱스 변경안을 함께 제시할 수 있다. 단, 조회 기간과 지역별 데이터 분포가 달라질 때에도 동일한 개선안이 항상 유리한지는 별도로 판단하시오.

**답변**

- [[SQLP 스터디] 6주차 - 제5장 SQL 옵티마이저, 제6장 고급 SQL 튜닝 1 : Ⅹ.문제풀이](https://blog.naver.com/biyoonx/224367161423)
</details>
</dd>
</dl>
</details>

---

### 7주차 : 제6장 고급 SQL 튜닝(2026-08-08)
#### 제2절 DML 튜닝
#### 제3절 데이터베이스 Call 최소화
#### 제4절 파티셔닝
#### 제5절 대용량 배치 프로그램 튜닝
#### 제6절 고급 SQL 활용

<details>
<summary>이지은🙋🏻‍♀️</summary>

- [x] 주제에 대한 서술형 문제 및 풀이 공유

<dl>
<dd>
<details>
  <summary>Q. 대용량 진료이력 기반 월간 통계 적재 배치 분석 및 튜닝</summary>
  
  ### 업무 상황

의료기관에서는 매월 초 전월 완료 진료를 기준으로 성별·연령대·진료과별 월간 통계정보를 생성한다.

현재 배치 프로그램은 대상 환자를 먼저 조회한 후 환자별로 진료이력을 반복 조회하고, 계산한 결과를 통계 테이블에 한 건씩 적재한다.

```
대상 환자 조회
    ↓
환자별 반복 처리
    ├─ 해당 월 진료이력 조회
    ├─ 진료 건수 조회
    ├─ 총진료비 조회
    ├─ 최근 진료 조회
    ├─ 통계 테이블 INSERT 또는 UPDATE
    └─ COMMIT
```

최근 진료이력 데이터가 증가하면서 배치 수행시간이 6시간 이상 소요되고 있으며, 수행 중 log file sync, 높은 Execute Call, TEMP 사용량 증가가 확인되었다.

### 데이터 규모

`TB_TREATMENT`

- 전체 진료이력: 120,000,000건
- 월평균 진료이력: 10,000,000건
- 완료 진료 비율: 약 90%
- 월별 RANGE 파티션 구성

`TB_PATIENT`

- 전체 환자: 1,000,000명

`TB_MONTHLY_TREATMENT_STAT`

- 성별·연령대·진료과별 월간 통계 적재 테이블
- 기준월 데이터를 월 1회 생성

### 테이블 구성

```sql
CREATE TABLE TB_PATIENT
(
    PATIENT_ID  NUMBER        NOT NULL,
    PATIENT_NM  VARCHAR2(100) NOT NULL,
    SEX_CD      VARCHAR2(1)   NOT NULL,
    BIRTH_DT    DATE          NOT NULL,
    CONSTRAINT TB_PATIENT_PK PRIMARY KEY (PATIENT_ID)
);
```

```sql
CREATE TABLE TB_TREATMENT
(
    TREATMENT_ID       NUMBER       NOT NULL,
    PATIENT_ID         NUMBER       NOT NULL,
    TREATMENT_DTM      DATE         NOT NULL,
    TREATMENT_STAT_CD  VARCHAR2(20) NOT NULL,
    DEPT_CD            VARCHAR2(10) NOT NULL,
    TREATMENT_COST     NUMBER       NOT NULL,
    CONSTRAINT TB_TREATMENT_PK PRIMARY KEY (TREATMENT_ID)
)
PARTITION BY RANGE (TREATMENT_DTM)
(
    PARTITION P202606 VALUES LESS THAN (DATE '2026-07-01'),
    PARTITION P202607 VALUES LESS THAN (DATE '2026-08-01'),
    PARTITION P202608 VALUES LESS THAN (DATE '2026-09-01'),
    PARTITION PMAX     VALUES LESS THAN (MAXVALUE)
);
```

```sql
CREATE INDEX TB_TREATMENT_X01
    ON TB_TREATMENT (TREATMENT_DTM, PATIENT_ID)
LOCAL;
```

```sql
CREATE TABLE TB_MONTHLY_TREATMENT_STAT
(
    BASE_YYYYMM        VARCHAR2(6)  NOT NULL,
    SEX_CD             VARCHAR2(1)  NOT NULL,
    AGE_GROUP          VARCHAR2(10) NOT NULL,
    DEPT_CD            VARCHAR2(10) NOT NULL,
    PATIENT_CNT        NUMBER       NOT NULL,
    TREATMENT_CNT      NUMBER       NOT NULL,
    TOTAL_COST         NUMBER       NOT NULL,
    LAST_TREATMENT_ID  NUMBER,
    LAST_TREATMENT_DTM DATE
);
```

### 기존 배치 통계

1. 대상 환자 조회 - 1회
2. 환자별 진료 조회 - 약 1,000,000회
3. 환자별 집계 조회 - 약 1,000,000회
4. 최근 진료 조회 - 약 1,000,000회
5. 통계 테이블 DML - 약 1,000,000회
6. COMMIT - 약 1,000,000회

---

#### 문제 1. 집합 기반 적재 SQL 작성

기존 배치 프로그램은 환자별로 진료내역을 반복 조회하고, 계산한 통계 결과를 한 건씩 적재한다.

이를 하나의 집합 기반 SQL로 개선한 경우 다음과 같은 주요 실행계획이 예상된다.

```sql
-----------------------------------------------------------------------------------
| Id | Operation                       | Name                         |
-----------------------------------------------------------------------------------
|  0 | INSERT STATEMENT                |                              |
|  1 |  LOAD AS SELECT                 | TB_MONTHLY_TREATMENT_STAT    |
|  2 |   HASH GROUP BY                 |                              |
|  3 |    HASH JOIN                    |                              |
|  4 |     TABLE ACCESS FULL           | TB_PATIENT                   |
|  5 |     PARTITION RANGE SINGLE      |                              |
|  6 |      TABLE ACCESS FULL          | TB_TREATMENT                 |
-----------------------------------------------------------------------------------
```

위 실행계획의 주요 처리 흐름이 나타나도록 2026년 7월 완료 진료에 대한 월간 통계 적재 SQL을 작성하시오.

적재 항목은 다음과 같다.

- 기준연월
- 성별
- 진료일 기준 10세 단위 연령대
- 진료과
- 고유 환자 수
- 진료 건수
- 총진료비
- 그룹 내 가장 최근 진료번호
- 그룹 내 가장 최근 진료일시

동일한 진료일시에 여러 건이 존재하면 진료번호가 가장 큰 건을 최근 진료로 판단한다.

다음 조건을 모두 만족해야 한다.

- 환자별 반복 SQL과 건별 DML을 사용하지 않는다.
- 조회와 적재를 하나의 `INSERT SELECT`로 처리한다.
- 2026년 7월 파티션만 읽도록 조건을 작성한다.
- 대량 적재에 적합하도록 Direct Path Insert를 고려한다.
- 최근 진료정보는 별도의 분석 함수용 대량 정렬을 최소화하는 방식으로 산출한다.
- 환자 수는 중복 환자를 제외하여 계산한다.

작성한 SQL에서 `LOAD AS SELECT`, `HASH GROUP BY`, `HASH JOIN`, `PARTITION RANGE SINGLE`, `TABLE ACCESS FULL TB_TREATMENT`가 선택될 수 있는 이유를 설명하시오.

---

#### 문제 2. 파티션 프루닝과 조건식 작성

`TB_TREATMENT`는 `TREATMENT_DTM`을 기준으로 월별 RANGE 파티셔닝되어 있다.

2026년 7월 데이터만 조회할 때 다음 두 조건식의 파티션 접근 방식과 성능 차이를 설명하시오.

```sql
T.TREATMENT_DTM >= DATE '2026-07-01'
AND T.TREATMENT_DTM <  DATE '2026-08-01'
```

```sql
TO_CHAR(T.TREATMENT_DTM, 'YYYYMM') = '202607'
```

또한 다음 조건이 2026년 7월 전체 데이터를 정확히 조회하지 못하는 이유를 설명하시오.

```sql
T.TREATMENT_DTM BETWEEN DATE '2026-07-01'
                    AND DATE '2026-07-31'
```

파티션 키를 가공하지 않은 범위 조건, 정적 파티션 프루닝, 로컬 인덱스 활용 및 대상 월 파티션 Full Scan 관점에서 설명한다.

추가로 `TB_MONTHLY_TREATMENT_STAT`도 `BASE_YYYYMM` 기준 월별 파티셔닝되어 있다고 가정한다.

기준월 통계를 전체 재생성할 때 다음 두 방식의 차이를 설명하고, 대용량 월간 배치에 더 적합한 방식을 판단하시오.

```sql
DELETE FROM TB_MONTHLY_TREATMENT_STAT
WHERE BASE_YYYYMM = '202607';
```

```sql
ALTER TABLE TB_MONTHLY_TREATMENT_STAT
TRUNCATE PARTITION P202607;
```

Undo, Redo, 수행시간, 트랜잭션 제어 및 인덱스 관리 측면에서 비교한다.

---

#### 문제 3. DML 및 대용량 배치 튜닝

문제 1의 적재 SQL에 `INSERT /*+ APPEND */ SELECT`를 적용하는 경우 일반적인 Conventional Insert와 비교하여 설명하시오.

다음 내용을 포함한다.

- Direct Path Insert
- Buffer Cache 사용 차이
- High Water Mark 이후 적재
- Undo와 Redo 발생 특성
- 대상 테이블 인덱스 유지 비용
- Lock 및 동시성 제약
- `NOLOGGING` 사용 시 복구상 주의사항

또한 다음 세 가지 COMMIT 방식의 특징을 비교하고, 월간 통계 배치에 적합한 방식을 제시하시오.

1. 건별 COMMIT
2. 일정 처리 단위별 COMMIT
3. 전체 적재 완료 후 COMMIT

다음 관점에서 설명한다.

- `log file sync`
- Undo 사용량
- 장애 시 재처리 범위
- 데이터 정합성
- 배치 재시작 가능성

---

#### 문제 4. 고급 SQL 방식 비교 및 최종 개선 효과

가장 최근 진료정보를 산출하는 다음 두 방식을 비교하시오.

```sql
ROW_NUMBER() OVER
(
    PARTITION BY ...
    ORDER BY TREATMENT_DTM DESC,
             TREATMENT_ID DESC
)
```

```sql
MAX(TREATMENT_ID)
KEEP
(
    DENSE_RANK LAST
    ORDER BY TREATMENT_DTM,
             TREATMENT_ID
)
```

두 방식의 실행 특성을 `WINDOW SORT`, `HASH GROUP BY`, 중간 결과 건수 및 TEMP 사용 측면에서 비교하고, 대용량 월간 집계 배치에서는 어느 방식이 더 적합한지 그 이유를 설명하시오.

또한 최근 진료번호와 최근 진료일시를 각각 집계할 경우 서로 다른 진료행의 값이 조합되지 않도록 데이터 정합성을 보장하는 방법을 설명하시오.

마지막으로 앞선 문제에서 검토한 집합 처리, 파티션 프루닝, Direct Path Insert 및 COMMIT 전략을 기존 배치 프로그램에 적용했을 때 기대되는 전체적인 성능 개선 효과를 Database Call, 파티션 접근, DML 및 트랜잭션 처리 관점에서 설명하시오.

**답변**

- [https://app.notion.com/p/leeeden/7-6-SQL-3b470b7b39f48079a3acd21c9d52c6c8?source=copy_link](https://app.notion.com/p/leeeden/7-6-SQL-3b470b7b39f48079a3acd21c9d52c6c8?source=copy_link)
</details>
</dd>
</dl>
</details>

<details>
  <summary>이시향🙋🏻‍♀️</summary>
  
  - [x] 주제 핵심 및 문제풀이 전략
  - [[SQLP 스터디] 7주차 - 제6장 고급 SQL 튜닝 2-6 : Ⅰ-Ⅸ](https://blog.naver.com/biyoonx/224374512771)
  - [x] 주제에 대한 서술형 문제 및 풀이 공유

<dl>
<dd>
<details>
  <summary>DML·파티션·배치 튜닝</summary>
  
  ### 문제 1. 대량 월별 이력 데이터 적재

#### 업무 상황

인사 시스템에서는 매월 말 기준으로 재직자 정보를 월별 이력 테이블에 저장한다.

#### `EMP_BIG`

* 전체 데이터 약 3,000만 건
* 현재 재직자는 약 1,200만 명
* `RETIRE_YN = 'N'`인 사원을 월별 이력 대상으로 적재함

#### `EMP_MONTHLY_SNAPSHOT`

* 월별 사원 현황 보관 테이블
* 기존 데이터 약 1억 건
* 매월 약 1,200만 건씩 추가됨
* 비고유 B-Tree 보조 인덱스 4개 존재
* 배치 수행 시간에는 해당 테이블을 조회하거나 변경하는 다른 업무가 없음
* 트리거 및 참조 무결성 제약조건은 없음
* 인덱스 재생성을 위한 추가 작업 공간은 충분함
* 배치 완료 후 데이터베이스 백업을 수행함

현재 다음 SQL을 수행하고 있다.

```sql
INSERT INTO EMP_MONTHLY_SNAPSHOT
(
    SNAPSHOT_YM,
    EMPNO,
    ENAME,
    DEPTNO,
    JOB,
    SAL,
    HIREDATE
)
SELECT
    :SNAPSHOT_YM,
    EMPNO,
    ENAME,
    DEPTNO,
    JOB,
    SAL,
    HIREDATE
FROM EMP_BIG
WHERE RETIRE_YN = 'N';
```

최근 데이터 증가로 배치 수행 시간이 길어지고 있으며 대량의 Redo 로그가 발생하고 있다.

#### 작성 요구사항

1. 현재 INSERT 방식의 성능 부하가 발생하는 원인을 설명하시오.
2. 대량 데이터 적재 시간을 단축하고 Redo 로그 발생량을 줄일 수 있도록 SQL 및 작업 절차를 개선하시오.
3. 보조 인덱스를 유지하면서 적재하는 방법과 적재 전 제거 후 재생성하는 방법을 비교하고, 주어진 조건에서 적절한 처리 방법을 제시하시오.
4. 제시한 방법을 운영 환경에 적용할 때 확인해야 할 사항을 작성하시오.

---

### 문제 2. 월 파티션 데이터 대량 삭제

#### 업무 상황

접속 로그 테이블은 접속 일시를 기준으로 월별 Range Partitioning되어 있다.

#### `LOGIN_ACCESS_LOG`

```sql
CREATE TABLE LOGIN_ACCESS_LOG
(
    LOG_ID          NUMBER        NOT NULL,
    MEMBER_ID       NUMBER        NOT NULL,
    ACCESS_DTM      DATE          NOT NULL,
    ACCESS_IP       VARCHAR2(50)  NOT NULL,
    ACCESS_RESULT   VARCHAR2(2)   NOT NULL,
    DEVICE_TYPE     VARCHAR2(20),
    CONSTRAINT LOGIN_ACCESS_LOG_PK
        PRIMARY KEY (LOG_ID)
)
PARTITION BY RANGE (ACCESS_DTM)
(
    PARTITION P_BEFORE_2026
        VALUES LESS THAN (DATE '2026-01-01'),

    PARTITION P202601
        VALUES LESS THAN (DATE '2026-02-01'),

    PARTITION P202602
        VALUES LESS THAN (DATE '2026-03-01'),

    PARTITION P202603
        VALUES LESS THAN (DATE '2026-04-01'),

    PARTITION P_MAX
        VALUES LESS THAN (MAXVALUE)
);
```

#### 데이터 및 인덱스 특성

* 전체 데이터 약 15억 건
* `P202601` 파티션에 약 1억 건 존재
* `ACCESS_RESULT = '99'`는 테스트 및 비정상 수집 데이터
* `P202601` 데이터 중 약 95%가 `ACCESS_RESULT = '99'`
* 나머지 정상 데이터 약 5%는 계속 보관해야 함
* `ACCESS_DTM, MEMBER_ID` 기준 로컬 파티션 인덱스 존재
* `MEMBER_ID, ACCESS_DTM` 기준 글로벌 비파티션 인덱스 존재
* 기본키 인덱스도 글로벌 인덱스로 구성되어 있음
* 작업 시간에는 `P202601` 데이터에 대한 업무를 중단할 수 있음
* 임시 데이터 저장을 위한 별도 공간은 충분함

현재 다음과 같이 삭제하려고 한다.

```sql
DELETE FROM LOGIN_ACCESS_LOG PARTITION (P202601)
WHERE ACCESS_RESULT = '99';
```

#### 작성 요구사항

1. 현재 DELETE 방식을 그대로 수행할 경우 발생할 수 있는 성능 문제를 설명하시오.
2. 삭제 대상 95%를 직접 제거하는 대신 보관 대상 5%를 기준으로 처리하도록 전체 작업 절차와 필요한 SQL을 작성하시오.
3. 작업 과정에서 Undo·Redo 발생량을 최소화할 수 있는 방법을 함께 적용하시오.
4. 파티션 작업이 로컬 인덱스와 글로벌 인덱스에 미치는 영향을 구분하여 설명하고 필요한 후속 작업을 작성하시오.
5. 반대로 삭제 대상이 파티션 전체 데이터의 약 5%뿐이라면 동일한 방법을 사용할 것인지 판단하고 그 이유를 작성하시오.

---

### 문제 3. 대량 급여 계산 배치

#### 업무 상황

급여 시스템에서는 매월 전체 재직자의 급여를 계산하여 월별 급여 결과 테이블에 저장한다.

#### `EMP_BIG`

* 재직자 약 500만 명
* 배치 시작 시 처리 대상 사원 Cursor를 생성함

#### `EMP_SAL_RESULT`

* 월별 급여 계산 결과 테이블
* 사원별·급여월별 1건 저장
* `(PAY_YM, EMPNO)` 조합의 고유성이 보장됨

급여 금액 계산에는 사원정보뿐 아니라 외부 인사규정 모듈과 애플리케이션 로직이 사용되므로 전체 작업을 하나의 `INSERT ... SELECT` SQL로 변경할 수 없다.

배치 프로그램은 Java/JDBC로 작성되어 있으며 현재 다음 방식으로 수행된다.

```text
JDBC Fetch Size = 1로 사원 1건 Fetch
        ↓
애플리케이션에서 급여 계산
        ↓
EMP_SAL_RESULT에 1건씩 개별 INSERT 실행
        ↓
COMMIT
        ↓
다음 사원 처리
```

500만 명을 처리하면서 배치 수행 시간이 지나치게 길어지고 있다.

한편 모든 데이터를 한 번에 하나의 트랜잭션으로 처리할 경우에는 장애 발생 시 재처리 범위와 트랜잭션 크기가 지나치게 커질 수 있다.

#### 작성 요구사항

1. 현재 프로그램이 느린 원인을 데이터베이스 Call 및 COMMIT 관점에서 설명하시오.
2. 조회 과정의 Fetch 방식과 결과 INSERT 방식을 개선하여 한 번의 데이터베이스 Call로 여러 건을 처리할 수 있도록 배치 구조를 설계하시오.
3. COMMIT 단위를 결정할 때 고려해야 할 사항을 작성하고, 행마다 COMMIT하는 방식과 전체 500만 건을 한 번에 COMMIT하는 방식의 문제점을 각각 설명하시오.
4. 배치 도중 장애가 발생한 경우 이미 처리한 구간부터 안전하게 재개할 수 있도록 재처리 방안을 설계하시오.
5. 변경 전과 변경 후의 전체 처리 흐름을 비교하여 작성하시오.

**답변**

- [[SQLP 스터디] 7주차 - 제6장 고급 SQL 튜닝 2-6 : Ⅹ.문제풀이](https://blog.naver.com/biyoonx/224374512771)
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
  <summary>A 사업 지원금 관리 시스템 - Raw Data 배치 튜닝</summary>
  
  ### 업무 상황

A 사업 지원금 관리 시스템에서는 신청 → 접수 → 지원 → 청구로 이어지는 4단계 업무 데이터를 하나의 Raw Data 테이블로 매일 새벽 배치를 통해 관리한다.

각 테이블은 계층적 PK 구조를 가진다.

```
신청 테이블 : 신청PK
접수 테이블 : 신청PK, 접수PK
지원 테이블 : 신청PK, 접수PK, 지원PK
청구 테이블 : 신청PK, 접수PK, 지원PK, 청구PK
```

데이터가 지속적으로 증가하면서 배치 수행 시간과 트랜잭션 부하가 문제가 되기 시작했다.

### 데이터 특성

```
신청 테이블 : 약 3,000만 건
접수 테이블 : 약 2,000만 건 (신청 대비 약 67% 접수)
지원 테이블 : 약 1,300만 건 (접수 대비 약 65% 지원)
청구 테이블 : 약 700만 건  (지원 대비 약 54% 청구)

각 테이블은 수정일시(UPD_DTM) 컬럼을 보유하며
전일 변경(신규 생성 포함) 건수는 일평균 약 3만 건 수준이다.

RAW_DATA 테이블 : 전체 누적 약 700만 건
(청구 테이블 기준 4단계 조인 결과와 1:1 대응)
현재 비파티션 Heap Table이며
신청일자(APPLY_DT) 컬럼을 보유한다.
```

### 현재 배치 처리 방식

```
1. 4개 테이블에서 각각
   수정일시(UPD_DTM) >= 전일 00:00:00 조건으로
   전일 변경분만 인라인뷰로 먼저 필터링

2. 필터링된 결과를 신청→접수→지원→청구 순으로
   단계적으로 조인하여 변경 대상 RAW_DATA 후보군 생성
   (일평균 약 3만 건)

3. 생성된 결과의 PK(신청PK+접수PK+지원PK+청구PK)를 기준으로
   RAW_DATA 테이블에서 기존 데이터를 DELETE

4. 새로 생성한 결과를 RAW_DATA 테이블에 INSERT

5. 배치는 3만 건 단위 전체를
   하나의 트랜잭션으로 처리 후 COMMIT
```

### 현재 SQL

```sql
-- STEP 1. 전일 변경분 조회 (인라인뷰 조인)
CREATE OR REPLACE VIEW V_CHANGED_RAW AS
SELECT A.신청PK, B.접수PK, C.지원PK, D.청구PK,
       A.신청일자, B.접수일자, C.지원일자, D.청구일자,
       D.청구금액
FROM (SELECT * FROM 신청 WHERE UPD_DTM >= TRUNC(SYSDATE-1)) A,
     (SELECT * FROM 접수 WHERE UPD_DTM >= TRUNC(SYSDATE-1)) B,
     (SELECT * FROM 지원 WHERE UPD_DTM >= TRUNC(SYSDATE-1)) C,
     (SELECT * FROM 청구 WHERE UPD_DTM >= TRUNC(SYSDATE-1)) D
WHERE A.신청PK = B.신청PK
AND   B.신청PK = C.신청PK AND B.접수PK = C.접수PK
AND   C.신청PK = D.신청PK AND C.접수PK = D.접수PK AND C.지원PK = D.지원PK;

-- STEP 2. 기존 데이터 삭제
DELETE FROM RAW_DATA
WHERE (신청PK, 접수PK, 지원PK, 청구PK) IN (
    SELECT 신청PK, 접수PK, 지원PK, 청구PK FROM V_CHANGED_RAW
);

-- STEP 3. 신규 데이터 삽입
INSERT INTO RAW_DATA
SELECT * FROM V_CHANGED_RAW;

COMMIT;
```

---

### 문제 1. [DML 튜닝] DELETE + INSERT vs MERGE 비교

1) 현재 DELETE + INSERT 방식의 성능 부하 요인

2) 위 로직을 MERGE 문 하나로 통합했을 때의 SQL을 작성하고, DELETE+INSERT 방식과 비교

3) 현재 배치는 "변경분 전체 삭제 후 전체 삽입" 방식이다. 만약 실제로는 삭제 대상이 없고 신규 삽입 대상만 있는 경우(순수 신규 신청 건)에도 DELETE 문이 함께 수행된다. 이로 인한 불필요한 비용을 설명하고, 개선 방향을 제시하시오.

---

### 문제 2. [파티셔닝] RAW_DATA 테이블 파티셔닝 도입 검토

RAW_DATA 테이블이 700만 건 규모로 증가하면서, 매일 3만 건씩 DELETE + INSERT를 반복하는 현재 방식의 부하가 누적되고 있다. 담당자는 RAW_DATA 테이블에 파티셔닝 도입을 검토하고 있다.

```sql
-- 파티셔닝 도입 검토안
CREATE TABLE RAW_DATA_NEW
(
    신청PK    NUMBER  NOT NULL,
    접수PK    NUMBER  NOT NULL,
    지원PK    NUMBER  NOT NULL,
    청구PK    NUMBER  NOT NULL,
    신청일자   DATE    NOT NULL,
    접수일자   DATE,
    지원일자   DATE,
    청구일자   DATE,
    청구금액   NUMBER
)
PARTITION BY RANGE (신청일자)
(
    PARTITION P_BEFORE VALUES LESS THAN (DATE '2026-01-01'),
    PARTITION P202601  VALUES LESS THAN (DATE '2026-02-01'),
    PARTITION P202602  VALUES LESS THAN (DATE '2026-03-01'),
    PARTITION P_MAX    VALUES LESS THAN (MAXVALUE)
);
```

1) 신청일자를 파티션 키로 선택하는 것이 적절한지 판단하시오.
2) 신청일자 대신 배치처리일자를 파티션 키로 사용하면 이 문제가 해결되는지 판단하시오.
3) 2)의 분석을 바탕으로, 이 RAW_DATA 배치 구조에서 파티셔닝이 DELETE 성능 개선에 실질적으로 기여하기 어려운 근본적인 이유를 설명하시오.

---

### 문제 3. [대용량 배치 튜닝] Direct Path Insert와 COMMIT 전략

현재 배치는 DELETE와 INSERT를 하나의 트랜잭션으로 묶어 3만 건 단위 전체를 처리한 후 한 번에 COMMIT하고 있다.

1) 현재 INSERT 문에 `/*+ APPEND */` 힌트를 적용할 수 있는지 판단하시오. 같은 트랜잭션 내에서 직전에 DELETE가 수행되었다는 점을 고려하여 Direct Path Insert 적용 가능 여부와 제약사항을 설명하시오.

2) 만약 DELETE와 INSERT를 완전히 분리된 두 트랜잭션(각각 별도 COMMIT)으로 처리한다면, Direct Path Insert 적용 가능 여부가 어떻게 달라지는지 설명하시오. 이때 발생할 수 있는 데이터 정합성 문제(트랜잭션 분리로 인한)도 함께 설명하시오.

3) 현재처럼 3만 건 전체를 하나의 트랜잭션으로 처리하는 방식과, 예를 들어 5천 건 단위로 나누어 여러 번 COMMIT하는 방식 비교

4) 이 배치가 매일 새벽 시간대에 단독으로 수행되며 RAW_DATA 테이블을 조회하는 다른 프로세스가 없다는 조건이 주어진다면, 위 3)의 비교 결과가 어떻게 달라지는지 설명하시오.

**답변**

- [[SQLP] 6장(2) 문제와 풀이](https://app.notion.com/p/SQLP-6-2-3b6894b3ff32807182d1e64bd8a35a7f?source=copy_link)
</details>
</dd>
</dl>
</details>

---

### 8주차 : 제7장 Lock과 트랜잭션 동시성 제어(2026-08-16)
#### 제1절 Lock
#### 제2절 트랜잭션
#### 제3절 동시성 제어

<details>
  <summary>최수연🙋🏻‍♀️</summary>

  - [x] 주제에 대한 서술형 문제 및 풀이 공유

<dl>
<dd>
<details>
  <summary>[동시성 제어] 재고 차감 - Lost Update와 해결 방안 + 기출 응용 2문제</summary>
  
  ### 문제 1. [동시성 제어] 재고 차감 - Lost Update와 해결 방안

#### 테이블 구성

```sql
CREATE TABLE PRODUCT_STOCK
(
    PRODUCT_ID  NUMBER      NOT NULL,
    STOCK_QTY   NUMBER      NOT NULL,
    VERSION_NO  NUMBER      DEFAULT 0 NOT NULL,
    CONSTRAINT PRODUCT_STOCK_PK PRIMARY KEY (PRODUCT_ID)
);

INSERT INTO PRODUCT_STOCK VALUES (1001, 10, 0);
COMMIT;
```

#### 상황

```
특정 인기 상품(PRODUCT_ID=1001)의 재고가 1개 남은 상태에서
세션 A와 세션 B가 거의 동시에 같은 상품을 1개씩 주문하는 상황이 발생했다.
```

#### [방식 1] 단순 UPDATE

```sql
-- 세션 A, 세션 B 모두 동일하게 수행
UPDATE PRODUCT_STOCK
SET STOCK_QTY = STOCK_QTY - 1
WHERE PRODUCT_ID = 1001;

COMMIT;
```

#### [방식 2] 애플리케이션에서 재고 확인 후 처리

```sql
-- STEP 1. 애플리케이션이 현재 재고를 조회
SELECT STOCK_QTY FROM PRODUCT_STOCK WHERE PRODUCT_ID = 1001;

-- STEP 2. 계산된 값으로 UPDATE
UPDATE PRODUCT_STOCK
SET STOCK_QTY = :계산된값
WHERE PRODUCT_ID = 1001;

COMMIT;
```

#### 문제

1. [방식 1]에서는 세션 A와 세션 B가 동시에 실행되더라도 `Lost Update`(갱신 유실)가 발생하지 않는다. 그 이유를 UPDATE 문의 Lock 획득 방식과 연관지어 설명하시오.
2. [방식 2]에서는 `Lost Update`가 발생할 수 있다. 세션 A와 세션 B의 STEP 1, STEP 2 실행 순서를 시간 순서대로 나열하여 최종 재고가 잘못 계산되는 과정을 설명하시오.
3. [방식 2]의 문제를 비관적 동시성 제어로 해결하는 SQL을 작성하고, 이 방식이 Lost Update를 방지할 수 있는 원리를 설명하시오.
4. [방식 2]의 문제를 낙관적 동시성 제어로 해결하는 SQL을 `VERSION_NO` 컬럼을 활용하여 작성하고, 비관적 동시성 제어와 비교했을 때의 장단점을 설명하시오.
5. 동시 주문이 몰려 재고가 0 미만으로 차감되는 초과 판매(Overselling)를 방지하기 위해 UPDATE 문에 추가해야 할 조건을 작성하고, 이 조건이 비관적/낙관적 동시성 제어 각각에서 어떻게 함께 적용되어야 하는지 설명하시오.

---

### 문제 2. [기출 응용] UPDATE + 스칼라서브쿼리 + OR + EXISTS 튜닝

#### 환경구성

```sql
DROP TABLE T1;
CREATE TABLE T1 AS
SELECT 
	10000+ROWNUM C1
	, ROWNUM C2
	, 10000-ROWNUM C3
	, 123 C4
	, 123 C5
FROM DUAL 
CONNECT BY LEVEL <= 10000;

DROP TABLE T2 ;
CREATE TABLE T2 AS
SELECT 
	CASE WHEN MOD(C2, 2) = 0 THEN C2 END C1
	, CASE WHEN MOD(C2, 2) = 1 THEN C3 END C2
	, TRUNC(DBMS_RANDOM.VALUE(1, 100)) C3
	, TRUNC(DBMS_RANDOM.VALUE(101, 200)) C4
FROM T1, (SELECT LEVEL LVL FROM DUAL CONNECT BY LEVEL <= 10) D
;

DROP TABLE T3 ;
CREATE TABLE T3 AS
SELECT 
	ROWNUM C1
	, 124 C2
FROM DUAL 
CONNECT BY LEVEL <= 1000;

DROP INDEX T2_X1;
CREATE INDEX T2_X1 ON T2(C1);

DROP INDEX T2_X2;
CREATE INDEX T2_X2 ON T2(C2);
```

#### 문제

```
T1 컬럼 : C1, C2, C3, C4, C5
T2 컬럼 : C1, C2, C3, C4
T3 컬럼 : C1, C2

-> 인덱스 : T2 : T2_X1(C1), T2_X2(C2)
```

아래 SQL을 튜닝하여 얻은 실행계획이 아래의 실행계획이다.
아래의 실행계획과 같이 튜닝 하세요.

```sql
-----------------------------------------------------------------
| Id | Operation                               | Name           |
-----------------------------------------------------------------
|  0 | UPDATE STATEMENT                        |                |
|  1 |  UPDATE                                 | T1             |
|* 2 |   HASH JOIN RIGHT SEMI                  |                |
|  3 |    TABLE ACCESS FULL                    | T3             |
|  4 |    TABLE ACCESS FULL                    | T1             |
|  5 |   SORT AGGREGATE                        |                |
|  6 |    VIEW                                 | VW_ORE_AE9E49E8|
|  7 |     UNION-ALL                           |                |
|  8 |      TABLE ACCESS BY INDEX ROWID BATCHED| T2             |
|* 9 |       INDEX RANGE SCAN                  | T2_X1          |
|*10 |      TABLE ACCESS BY INDEX ROWID BATCHED| T2             |
|*11 |       INDEX RANGE SCAN                  | T2_X2          |
-----------------------------------------------------------------
```

```sql
UPDATE T1 A
SET A.C4 = (SELECT MAX(C3) FROM T2 x WHERE X.C1 = A.C2 OR X.C2=A.C3)
	, A.C5 = (SELECT MAX(C4) FROM T2 x WHERE X.C1 = A.C2 OR X.C2=A.C3)
WHERE EXISTS (
				SELECT 1
				FROM T3 X
				WHERE X.C1= A.C2
					AND ROWNUM = 1
			);

COMMIT;
```

---

### 문제 3. [기출 응용] INSERT + 병렬 + 인덱스 UNUSABLE 튜닝

#### 환경구성

```sql
DROP TABLE T_SRC;
CREATE TABLE T_SRC
( C1 NUMBER
, C2 VARCHAR2(10)
, C3 NUMBER
);

DROP TABLE T_TGT;
CREATE TABLE T_TGT
( C1 NUMBER
, C2 VARCHAR2(10)
, C3 NUMBER
);

CREATE INDEX TGT_X1 ON T_TGT(C1);

INSERT INTO T_SRC
SELECT ROWNUM C1, NULL C2, 100000-ROWNUM C3
FROM DUAL
CONNECT BY LEVEL <= 100000
;

COMMIT;
```

#### 문제

```
T_SRC 테이블
( C1 NUMBER
, C2 VARCHAR2(10)
, C3 NUMBER
);

T_TGT 테이블
( C1 NUMBER
, C2 VARCHAR2(10)
, C3 NUMBER
);

인덱스 TGT_X1 : C1
```

아래 실행계획은 SQL을 튜닝한 결과의 실행계획입니다.
아래에서 제시된 실행계획과 같이 튜닝하세요.
- NOLOGGING 안해도 됨
- 병렬도 그대로 2 활용

```sql
----------------------------------------------------------------------------------------
| Id | Operation                               | Name   | TQ     | IN-OUT | PQ Distrib |
----------------------------------------------------------------------------------------
|  0 | INSERT STATEMENT                        |        |        |        |            |
|  1 |  PX COORDINATOR                         |        |        |        |            |
|  2 |   PX SEND QC (RANDOM)                   |:TQ10001| Q1,01  | P->S   | QC (RAND)  |
|  3 |    MULTI-TABLE INSERT                   |        | Q1,01  | PCWP   |            |
|  4 |     PX RECEIVE                          |        | Q1,01  | PCWP   |            |
|  5 |      PX SEND ROUND-ROBIN                |:TQ10000| Q1,00  | P->P   | RND-ROBIN  |
|  6 |       PX BLOCK ITERATOR                 |        | Q1,00  | PCWC   |            |
|  7 |        TABLE ACCESS FULL                | T_SRC  | Q1,00  | PCWP   |            |
|  8 |     DIRECT LOAD INTO (HYBRID TSM/HWMB)  | T_TGT  | Q1,01  | PCWP   |            |
|  9 |     DIRECT LOAD INTO (HYBRID TSM/HWMB)  | T_TGT  | Q1,01  | PCWP   |            |
----------------------------------------------------------------------------------------
```

```sql
DELETE FROM T_TGT;
COMMIT;

INSERT /*+ APPEND PARALLEL(T_TGT 2) */ INTO T_TGT
SELECT C1, 'A', C3 FROM T_SRC
UNION ALL
SELECT C1, 'B', C3 FROM T_SRC;

COMMIT;
```

---

문제2 출처 : [SQLP 54회 1번 복기](https://cafe.naver.com/dbstudydapsqlp/10550)
문제3 출처 : [SQLP 54회 2번 복기](https://cafe.naver.com/dbstudydapsqlp/10551)

**답변**

- [[SQLP] 7장 문제와 풀이](https://app.notion.com/p/SQLP-7-3bd894b3ff328029a4a7d201e55765c3?source=copy_link)
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
  <summary>Q. 동시 예약 처리 후 발생한 데이터 불일치 + 장시간 통계 조회 중 발생한 조회 일관성 문제</summary>
  
  ## Q.

병원 검사 예약 시스템에서는 검사 슬롯별 예약 가능 인원을 관리하고 있으며, 예약 완료 후 검사 결과를 외부 시스템으로 전송한다.

```sql
CREATE TABLE TB_EXAM_SLOT
(
    SLOT_ID          NUMBER       NOT NULL,
    EXAM_DT          DATE         NOT NULL,
    CAPACITY         NUMBER       NOT NULL,
    RESERVED_CNT     NUMBER       NOT NULL,
    SLOT_STATUS      VARCHAR2(20) NOT NULL,
    CONSTRAINT TB_EXAM_SLOT_PK PRIMARY KEY (SLOT_ID)
);

CREATE TABLE TB_RESERVATION
(
    RESERVATION_ID      NUMBER       NOT NULL,
    SLOT_ID             NUMBER       NOT NULL,
    PATIENT_ID          NUMBER       NOT NULL,
    RESERVATION_STATUS  VARCHAR2(20) NOT NULL,
    CONSTRAINT TB_RESERVATION_PK PRIMARY KEY (RESERVATION_ID)
);

CREATE TABLE TB_RESULT_QUEUE
(
    QUEUE_ID       NUMBER       NOT NULL,
    RESERVATION_ID NUMBER       NOT NULL,
    STATUS_CD      VARCHAR2(20) NOT NULL,
    CREATED_DTM    DATE         NOT NULL,
    CONSTRAINT TB_RESULT_QUEUE_PK PRIMARY KEY (QUEUE_ID)
);
```

---

#### 문제 1. 동시 예약 처리 후 발생한 데이터 불일치

특정 검사 슬롯의 현재 상태는 다음과 같다.

```
SLOT_ID       = 500
CAPACITY      = 100
RESERVED_CNT  = 98
SLOT_STATUS   = 'OPEN'
```

현재 프로그램은 예약 인원을 조회한 후 애플리케이션에서 값을 증가시킨다.

```sql
SELECT CAPACITY, RESERVED_CNT
FROM   TB_EXAM_SLOT
WHERE  SLOT_ID = :slot_id;

UPDATE TB_EXAM_SLOT
SET    RESERVED_CNT = :new_cnt
WHERE  SLOT_ID = :slot_id;
```

동일 검사 슬롯에 두 건의 예약 요청이 거의 동시에 발생했으며 두 요청은 모두 성공으로 처리되었으나 최종 `RESERVED_CNT`는 99였다.

다음 세 개선안 중 **동시 요청이 많은 예약 업무에 가장 적합한 방식을 선정하여 SQL을 완성하고**, 기존 방식에서 데이터 불일치가 발생한 원인과 다른 두 개선안보다 해당 방식을 선택한 이유를 동시성 및 Lock 범위 관점에서 설명하시오.

**개선안**

```sql
-- A
SELECT ...
FOR UPDATE;

-- B
UPDATE TB_EXAM_SLOT
SET RESERVED_CNT = RESERVED_CNT + 1
WHERE ...;

-- C
UPDATE TB_EXAM_SLOT
SET RESERVED_CNT = :new_cnt
WHERE SLOT_ID = :slot_id
AND   RESERVED_CNT = :old_cnt;
```

---

#### 문제 2. 장시간 통계 조회 중 발생한 조회 일관성 문제

병원 운영팀에서는 실시간 예약 현황을 확인하기 위해 다음 SQL을 실행한다.

```sql
SELECT SLOT_STATUS,
       COUNT(*)          AS SLOT_CNT,
       SUM(RESERVED_CNT) AS RESERVED_CNT
FROM   TB_EXAM_SLOT
GROUP BY SLOT_STATUS;
```

`TB_EXAM_SLOT`은 약 3천만 건이며, 해당 SQL은 전체 테이블을 읽어 약 8분 동안 수행된다.

한편 예약 서비스는 통계 조회와 관계없이 계속 운영되고 있으며, 조회 수행 중 다른 세션에서 `TB_EXAM_SLOT`의 예약 인원을 지속적으로 변경하고 COMMIT한다.

```sql
UPDATE TB_EXAM_SLOT
SET    RESERVED_CNT = RESERVED_CNT + 1
WHERE  SLOT_ID = :slot_id;

COMMIT;
```

특정 시점의 수행 상황은 다음과 같다.

```
시간      통계 조회 Session A                  예약 Session B
--------------------------------------------------------------------
T1        통계 SQL 실행 시작

T2                                             SLOT 100 RESERVED_CNT 변경
T3                                             COMMIT

T4                                             SLOT 200 RESERVED_CNT 변경
T5                                             COMMIT

T6        아직 통계 SQL 수행 중

T7                                             SLOT 300 RESERVED_CNT 변경
T8                                             COMMIT

T9        통계 SQL 종료
```

운영팀에서는 다음과 같은 두 가지 의문을 제기하였다.

- 통계 SQL이 8분 동안 수행되는 사이 여러 예약이 COMMIT되었는데, 최종 집계 결과에 변경 전 값과 변경 후 값이 섞여 들어가는 것은 아닌가?
- 같은 SQL이 평소에는 정상 수행되지만 특정 시간대에는 간헐적으로 `ORA-01555: snapshot too old`가 발생하는 이유는 무엇인가?

**위 현상을 Oracle의 다중 버전 동시성 제어와 읽기 일관성 관점에서 분석하고, 장시간 조회와 빈번한 갱신이 동시에 발생하는 환경에서 `ORA-01555` 발생 가능성을 낮추기 위한 개선 방향을 제시하시오.**

---

#### 문제 3. 간헐적 Deadlock

예약 취소를 수행하는 두 프로그램이 있다.

**온라인 프로그램**

```sql
UPDATE TB_RESERVATION
SET    RESERVATION_STATUS = 'CANCELLED'
WHERE  RESERVATION_ID = :reservation_id;

UPDATE TB_EXAM_SLOT
SET    RESERVED_CNT = RESERVED_CNT - 1
WHERE  SLOT_ID = :slot_id;

COMMIT;
```

**야간 배치**

```sql
UPDATE TB_EXAM_SLOT
SET    RESERVED_CNT = RESERVED_CNT - 1
WHERE  SLOT_ID = :slot_id;

UPDATE TB_RESERVATION
SET    RESERVATION_STATUS = 'CANCELLED'
WHERE  RESERVATION_ID = :reservation_id;

COMMIT;
```

개별 테스트에서는 문제가 없었지만 두 프로그램이 동시에 실행되는 시간대에 간헐적으로 다음 오류가 발생한다.

```
ORA-00060: deadlock detected while waiting for resource
```

운영팀에서는 해결책으로 다음 두 방안을 검토하고 있다.

1. 두 프로그램의 테이블 접근 순서를 동일하게 변경
2. 각 UPDATE 직후 COMMIT하여 Lock을 즉시 해제

**장애 발생 원인을 분석하고 두 개선안의 적절성을 평가한 후, 업무 정합성을 유지하면서 Deadlock 발생 가능성을 낮출 수 있도록 트랜잭션 구조를 개선하시오.**

**답변**

- [https://app.notion.com/p/leeeden/8-7-Lock-3ba70b7b39f48052abd9e40c36bacb42?source=copy_link](https://app.notion.com/p/leeeden/8-7-Lock-3ba70b7b39f48052abd9e40c36bacb42?source=copy_link)
</details>
</dd>
</dl>
</details>

<details>
  <summary>이시향🙋🏻‍♀️</summary>
  
  - [x] 주제 핵심 및 문제풀이 전략
  - 추가 예정
  - [x] 주제에 대한 서술형 문제 및 풀이 공유

<dl>
<dd>
<details>
  <summary>Lock과 트랜잭션 동시성 제어</summary>
  
  문제

**답변**

- 추가 예정
</details>
</dd>
</dl>
</details>
