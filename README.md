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

