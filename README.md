# Oracle

# MYSQL
●가장 널리 사용되고 있는 관계형 데이터베이스 관리 시스템(RDBMS)

●MYSQL은 오픈소스이며, 다중 사용자와 다중 스레드를 지원

●유닉스,리눅스,윈도우 등 다양한 운영체제에서 사용할 수 있으며, 특히 PHP와 함께 웹 개발에 자주 사용

# SQL의 기본
# SQL의 분류

# DML

	-데이터 조작 언어
  
	-데이터를 조작(선택,삽입,수정,삭제)하는데 사용하는 언어
  
	-DML 구문이 사용되는 대상은 테이블의 행
  
	-DML 사용하기 위해서는 꼭 그 이전에 테이블이 정의되어 있어야 함
  
	-SQL문 중 SELECT, INSERT, UPDATE, DELETE가 이 구문에 해당
  
	-트랜잭션이 발생하는 SQL도 이 DML에 속함
  
# DDL

	-데이터 정의 언어 
  
	-데이터베이스, 테이블, 뷰, 인덱스 등의 데이터베이스 개체를 생성/삭제/변경하는 역할
  
	-CREATE,DROP,ALTER 구문
  
	-DDL은 트랜잭션 발생시키지 않음
  
	-ROLLBACK이나 COMMIT사용 불가
  
	-DDL문은 실행 즉시 MYSQL에 적용
  
# DCL

	-데이터 제어 언어
  
	-사용자에게 어떤 권한을 부여하거나 뺴앗을때 주로 사용하는 구문
  
	-GRANT/REVOKE
  
  아래 작업은 DBA역할이 있는 최고 관리자(SYSTEM/SYS)로 접속해야 한다.
  
1] 사용자 생성 및 암호 설정
  
  -사용자는 DB에 엑세스하기 위해 시스템 권한이 필요하고 DB 개체의 내용을 조작하기 위해 개체 권한이 필요하다

  -시스템 권한의 종류는 200개 이상 개체권한은 28개

  -시스템 권한은 주로 DBA가 부여한다.(SYS/SYSTEM)

  -DBA는 상급의 시스템권한을 부여한다.

●역할

DBA : 최고 권한

connect : DB에 엑세스 할 수 있는 권한

resource : 개체를 생성 할 수 있는 권한

    //시스템 권한 확인
     SELECT * FROM SYSTEM_PRIVILEGE_MAP
    //개체 권한 확인
    SELECT * FROM TABLE_PRIVILEGE_MAP          
    //사용자 목록 확인
    SELECT username from dba_users             // system 계정에서 해야함
    //사용자 구조
    desc DBA_USERS

    //생성
    CREATE USER 아이디 IDENTIFIED BY 암호            // 사용자는 생성된 후 어떠한 권한도 가지지 못한다.
    create user user03 identified by user03; //아이디 user03 비밀번호 user03


    //권한 부여
    Grant 시스템 권한1,[시스템 권한2...] | 역할1, [역할2...]
    to 사용자1,[사용자2...] | 역할1, [역할2...]
    [With admin option]                            // 받은 시스템 권한을 다른 사용자에게 부여 할 수 있는 권한

    grant connect, resource to user03; //테이블을 만들 수 있는 권한
    grant create view to user03;                  // 뷰를 만들 수 있는 권한


    //수정 
    alter user user03 identified by 1234; //비밀번호 1234 로 변경

    //계정 lock 걸고 풀기
    alter user user03 account lock;                   //lock
    alter user user03 account unlock identified by user03     // lock 풀자마자 비밀번호 변경


    //다른 계정에서 테이블 DCL 사용할 수 있는 권한 
    grant select, delete On scott.emp To user03;    //user03은 scott.emp 테이블 select,delete 할 수 있다.

    //삭제
    drop user user04 cascade
  
  
# CMD 기초

●계정 만들기

	 create user 아이디 identified by 비번;

●권한 주기

	grant connect, resource to 아이디;

●테이블 만들기

	CREATE TABLE MEMBER(

	username varchar2(10) primary key,

	password varchar2(10) not null,

	name nvarchar2(10),

	postdate date);

●시퀀스 만들기

	CREATE SEQUENCE SEQ_MEMBER

	NOCACHE

	NOCYCLE;

# PL/SQL

●프로그래밍 언어의 특성을 수용한 SQL의 확장

●SQL의 데이터 조작(DML)과 질의문 블락 구조에 절차적 단위(IF, FOR, WHILE, LOOP등)로 된 커맨드를 포함 할 수 있음

●PL/SQL블락내에서 한 문장이 종료할때마나 세미콜론(;)을 붙인다.

●END뒤에 세미콜론(;)을 붙여 하나의 BLOCK이 끝났다는 것을 명시

●마지막에 반드시 / 를 붙여야 한다.

●-- 한줄 주석

●/* 여러줄 주석

# 1] PL/SQL 구조
    변수명 [CONSTANT] 자료형 [NOT NULLL] [ := 초기값 | DEFAULT 초기값 ];
    한 라인에 하나의 식별자만 가능
    상수선언에서 CONSTANT는 자료형보다 먼저 기술
    대소문자를 구분하지 않는다.
    
# 명령어

# SHOW DATABASES

●현재 서버에 어떤 DB가 있는지 보기


# USER

●사용할 데이터베이스 지정

●지정해 놓은 후 특별히 다시 USE문 사용하거나 다른 DB를 사용하겠다고 명시하지 않는 이상 모든 SQL문은 지정 DB에서 수행

●Workbench에서 직접 선택해 사용 가능


# SHOW TABLE

●데이터베이스의 테이블 이름 보기


# SHOW TABLE STATUS

●데이터베이스의 테이블 정보 조회

# DESCRIVE(DESC)

●테이블에 무슨 열이 있는지 확인

-DESCRIBE ***;
  
-DESC ***;

# SELECT

●<SELECT... FROM>

●요구하는 데이터를 가져오는 구문

●일반적으로 가장 많이 사용되는 구문

●데이터베이스 내 테이블에서 원하는 정보를 추출

●SELECT 열 이름

    -테이블에서 필요로 하는 열만 가져오기 기능

    -여러개의 열을 가져오고 싶을 떄는 콤마로 구분

    -열 이름의 순서는 출력하고 싶은 순서대로 배열 가능

# SELECT FROM WHERE

●기본적인 WHERE절

	-조회하는 결과를 특정한 조건으로 원하는 데이터만 보고 싶을때 사용
  
	-SELECT 필드이름 FROM 테이블이름 WHERE 조건식;
  
	-조건이 없을 경우 테이블의 크기가 클수록 찾는 시간과 노력이 증가
  

●관계 연산자의 사용

	-OR 연산자
  
	-AND 연산자
  
	-조건 연산자(=, <, >, <=, >=, <>, !=등)
  
	-관계 연산자(NOT, AND, OR 등)
  
	-연산자의 조합으로 데이터를 효율적으로 추출
  
  
  # Sub Query	
  
●쿼리문 안에 또 쿼리문이 들어 있는 것

●서브 쿼리의 결과가 둘 이상이 되면 에러 발생

	-(where절 고른것을 다시 select해서 정보검색)
  
●서브쿼리는 다른 하나의 SQL문장에 기술된 SELECT문장을 말한다

●서브쿼리는 괄호로 묶어야 한다.

●서브쿼리만을 단독 실행시 실행이 된다.

●서브쿼리는 연산자의 오른쪽에 기술 되어야 한다.

●단일행 서브 쿼리에는 단일행 연산자를 다중행 서브쿼리에는 복수행 연산자를 사용한다

●서브쿼리는 SELECT, FROM, WHERE절 등에 위치할 수 있다

●FROM절 서브쿼리를 쓸 때 SELECT이랑 칼럼이 같거나 더 커야함


# TOP Query	

●반드시 정렬되어야 한다

●얻어진 질의 결과에서 위에서부터 순서대로 몇 개만 가져오는 경우에 사용함

●데이터가 입력된 순서대로 혹은 서브쿼리에 의해 생성된 테이블에 레코드가 생성된 순서대로 내부적으로 번호가 순차적으로 부여되고 그 부여된 번호는 ROWNUM이라는 컬럼에 내부적으로 저장되어 있다.


# ANY

●서브쿼리의 여러 개의 결과 중 한가지만 만족해도 사용 가능

●SOME은 ANY와 동일한 의미로 사용

●=ANY 구문은 IN과 동일한 의미


# ALL

●서브쿼리의 여러 개의 결과를 모두 만족 시켜야함



# BETWEEN

●데이터가 숫자로 구성되어 있어 연속적인 값은 BETWEEN... AND 사용 가능

# IN

●이산적인 값의 조건에서는 IN()사용 가능

	(정한 값만 보고 싶을떄, ex WHERE Name IN('SEOUL', NEW YORK'))

# LIKE

●문자열의 내용 검색하기 위해 LIKE 연산자 사용

●문자 뒤에 % -무엇이든(%)허용

●한 글자와 매치하기 위해서는 '_' 사용


# ORDER BY

●결과가 출력되는 순서를 조절하는 구문

●기본적으로 오름차순 정렬

●내림차순으로 정렬

	-열 이름 뒤에 DESC적어줄 것
  
●ASC(오름차순)는 default이므로 생략 가능

●ORDER BY 구문을 혼합해 사용하는 구문도 가능


# DISTINCT

●중복된 것은 1개씩만 보여주면서 출력

●테이블의 크기가 클수록 효율적


# LIMIT

●출력 개수를 제한

●상위의 N개만 출력하는 'LIMIT N'구문

●서버의 처리량을 많이 사용해 서버의 전반적인 성능을 나쁘게 하는 악성 쿼리문 개선할 떄 사용


# GROUP BY

●그룹으로 묶어주는 역할

●집계 함수를 함께 사용

      -AVG(): 평균값
      -MIN(): 최소값
      -MAX(): 최대값
      -COUNT(): 행의 개수
      -COUNT(DISTINCT): 중복 제외된 행의 개수
      -STDEC(): 표준 편차
      -CARIANCE(): 분산
      
●효율적인 데이터 그룹화

●입기 좋게 하기 위해 별칭 사용 SELECT절 묶은 것 뒤에 사용( AS ****) 



# HAVING

●WHERE과 비슷한 개념으로 조건 제한

●집계 함수에 대해서 조건 제한하는 편리한 개념

●HAVING절은 반드시 GROUP BY절 다음에 나와야 함



# ROLLUP

●총합 또는 중간합계가 필요할 경우 사용

●GROUP BY절과 함께 WITH TOLLUP문 사용

(ex GROUP BY ****, *** WITH ROLLUP)


# JOIN

●JOIN은 데이터베이스 내의 여러 테이블에서 가져온 레코드를 조합하여 하나의 테이블이나 결과 집합으로 표현

# 1] inner join

2개 이상의 테이블로부터 자료를 검색하기 위해서 Join을 사용한다.

일반적으로 pk와 fk을 사용하여 join하는 경우가 대부분

가장 많이 사용되는 조인문으로 테이블 간에 연결 조건을 모두 만족하는 행을 검색하는데 사용한다

검색시 검색되는 컬럼이 조인하는 테이블 모두에 존재한다면 반드시 컬럼명에 테이블 이름을 "테이블명.컬럼명'의 형태로 기술

자식테이블 레코드 10개, 부모테이블 레코드 100개 inner join하면 레코드 수는 10개 PK : 중복 X, Null X

테이블 칭을 명부여하여 긴 테이블 명을 간단하게 사용 (as 사용 불가)

    [정규 표현]
    SELECT 칼럼명
    FROM 테이블1 join 테이블2 On 테이블1.pk = 테이블2.fk
    join 테이블3 on 테이블2.pk = 테이블3.fk

    SELECT ename,sal,job,dname
    FROM emp e JOIN dept d ON e.deptno = d.deptno;


# 2] outer join

어느 한쪽 테이블에서 결과값을 모두 가져오는 join문이다.

어느 쪽 테이블에서 가져올지 즉 왼쪽인지 오른쪽인지 아니면 양쪽 테이블인지 반드시 기술해야 한다.

자식테이블 left outer join 부모테이블은 ineer join과 같다

RDMS는 full outer join 의미가 없다.

자식에 없는 부모 튜플도 outer join으로 알 수 있다.

    SELECT 부모테이블 칼럼
    FROM 부모테이블 부 left outer join 자식테이블 자 on 부.pk = 자.fk;
    WHERE 자.pk is null
    
 # MYSQL 내장함수
 
 ●사용자의 편의를 위해 다양한 기능의 내장함수
 
●대표적인 내장 함수의 종류

	-문자열 함수
	-수학 함수
	-날짜와 시간 함수
  
  # 문자열 함수
  
# LENGTH()

●전달받은 문자열의 길이를 반환

# LENGTHB()

●LENGTHB('문자열') : 문자열 비트 길이


 # LPAD()
 
●LPAD('문자열',전체 자리수,'채울 문자열') : 좌측을 지정한 값으로 채운다

# RPAD()

●RPAD('문자열',전체 자리수,'채울 문자열') : 우측을 지정한 값으로 채운다


# INSTR()

●INSTR('문자열','찾을 문자열') : 찾은 문자열의 인덱스 변환, 인덱스는 1부터 시작

●like 사용하는것보다 속도면에서 우수하다.

●없으면 0 반환

# SUBSTR()

●SUBSTR('문자열',시작인덱스,길이) : 문자열에서 시작인덱스부터 길이만큼 가져옴, 인덱스는 1부터


# TO_CHAR

●TO_CHAR(숫자 혹은 날짜) : CHAR형으로 바꿔준다.

●TO_CHAR(숫자, '숫자형식 포맷 문자열')

    -9는 값이 있으면 표시, 없으면 표시 안함
    -0은 값이 있으면 표시, 없으면 0으로 표시
    -단, 소수점은 9든 0이든 값이 없으면 모두 0으로 표시됨
    -소수점은 실제값의 자리수가 많으면 나머지는 짤림
    -정수인 경우는 실제값의 자리수가 많으면 값이 #으로 표시됨




# CONCAT()

●전달받은 문자열을 모두 결합하여 하나의 문자열로 반환

●전달받은 문자열 중 하나라도 NULL이 존재하면 NULL을 반환

# LOCATE()

●문자열 내에서 찾는 문자열이 처음으로 나타나는 위치를 찾아서 해당 위치를 반환

●찾는 문자열이 문자열 내에 존재하지 않으면 0을 반환

●MYSQL에서는 문자열의 시작 인덱스를 1부터 계산


# LEFT(), RIGHT()

●LEFT(): 문자열의 왼쪽부터 지정한 개수만큼의 문자를 반환

●RIGHT(): 문자열의 오른쪽부터 지정한 개수만큼의 문자를 반환


# LOWER(), UPPER()

●LOWER(): 문자열의 문자를 모두 소문자로 변경

●UPPER(): 문자열의 문자를 모두 대문자로 변경

# initcap()

●initcap('문자열') : 첫 글자만 대글자로 변경

# REPLACE()

●문자열에서 특정 문자열을 대체 문자열로 교체



# TRIM()

●문자열의 앞이나 뒤, 또는 양쪽 모두에 있는 특정 문자를 제거 

	-BOTH:전달받은 문자열의 양 끝에 존재하는 특정 문자를 제거(기본설정)
  
	-LEADING:전달받은 문자열 앞에 존재하는 특정 문자를 제거
  
	-TRAILING:전달받은 문자열 뒤에 존재하는 특정 문자를 제거
  
●만약 지정자를 명시하지 않으면 자동으로 BOTH로 설정

●제거할 문자를 명시하지 않으면, 자동으로 공백을 제거

# 수학 함수

# FORMAT()

●숫자 타입의 데이터를 세 자리마다 쉼표(,)를 사용하는'#,###,###.##'형식으로 변환

●반환되는 데이터의 형식은 문자열 타입

●두번쨰 인수는 반올림할 소수 부분의 자릿수

# FLOOR(),CEIL(),ROUNT()

●FLOOR(): 내림

●CEIL(): 올림

●ROUND(): 반올림


# SQRT(),POW(),EXP(),LOG()

●SQRT():양의 제곱근

●POW(): 첫 번째 인수로는 밑수를 전달하고, 두번째 인수로는 지수를 전달하여 거듭제곱 계산

●EXP(): 인수로 지수를 전달받아, E의 거듭제곱을 계산

●LOG(): 자연로그 값을 계산


# SIN(),COS(),TAN()

●SIN(): 사인값 반환

●COS():코사인값 반환

●TAN():탄젠트값 반환


# ABS(),RAND()

●AVS(X): 절대값을 반환

●RAND(): 0.0보다 크거나 같고 1.0보다 작은 하나의 실수를 무작위로 생성

# 날짜와 시간 함수

# NOW(),CRUDATE(),CURTIME()

●NOW(): 현재 날짜와 시간을 반환, 반환되는 값은 'YYYY-MM-DD HH:MM:SS'또는 YYYYMMDDHHMMSS 형태로 반환

●CRUDATE(): 현재 날짜를 반환, 이때 반환되는 값은 'YYYY-MM-DD'또는 YYYYMMDD 형태로 반환

●CRUTIME(): 현재 시각을 반환, 이때 반환되는 값은 'HH:MM:SS'또는 HHMMSS형태로 반환


# DATE(),MONTH(),DAY(),HOUR(),MINUTE(),SECOND()

●DATE(): 전달받은 값에 해당하는 날짜 정보를 반환

●MONTH(): 월에 해당하는 값을 반환하며, 0부터 12사이의 값을 가짐

●DAY(): 일에 해당하는 값을 반환하며, 0부터 31사이의 값을 가짐

●HOUR(): 시간에 해당하는 값을 반환하며, 0부터 23사이의 값을 가짐

●MINUTE(): 분에 해당하는 값을 반환하며, 0부터 59사이의 값을 가짐

●SECOND(): 초에 해당하는 값을 반환하며, 0부터 59사이의 값을 가짐

# MONTHNAME(), DAYNAME()

●MONTHNAME(): 월에 해당하는 이름을 반환

●DAYBANE(): 요일에 핻아하는 이름을 반환


# DAYOFWEEK(),DAYOFMONTH(),DAYOFYEAR()

●DAYOFWEEK(): 일자가 해당 주에서 몇번째 날인지를 반환, 1부터 7사이의 값을 반환(일요일=1, 토요일=7)

●DAYOFMONTH(): 일자가 해당 월에서 몇번째 날인지를 반환, 0부터 31사이의 값을 반환

●DAYOFYEAR(): 일자가 해당 연도에서 몇번째 날인지를 반환, 1부터 366사이의 값을 반환



# DATE_FORMAT()

●전달받은 형식에 맞춰 날짜와 시간 정보를 문자열로 반환

# TABLE

# CREATE TABLE AS SELECT

●지정한 테이블과 똑같은 테이블2 생성 (CREATE TABLE AA SELECT * FROM AA;)


# CREATE DATABASE

●CREATE DATABASE문은 새로운 데이터베이스를 생성

●USE문으로 새 데이터베이스를 사용 (USE AA)

# 1] CREATE

    Create tabel 테이블명{
     컬러명1 자료형1 [not null],
     컬러명2 자료형2 [not null]

# 2] 테이블 이름 미 컬러 명명규칙

●문자로 시작한다

●30자 이내로 지정 한다

●대소문자를 구별하지 않는다

●동일한 이름으 사용할 수 없다. 또한 예약어도 사용할 수 없다

# 3] 테이블 제약 조건

[1] 기본키(pk) (Not Null + Unique)

	●참조무결성을 유지하기 위해 제약조건이다
  
	●하나의 테이블에느 하나의 키만 존재한다.
  
	●PK로 설정되면 그 칼럼은 값이 중복되거나 NULL을 허용하지 않는다.
  
[2] NOT NULL

	●NULL값을 절대로 허용하지 않는 컬럼
  
[3] UINQUE

	●중복을 허용하지 않는다. NULL은 허용한다(여러번)
  
[4] DEFAULT

[5] FK

	●컬럼 옆에
  
	●creat문 마지막에


# 4] Check

●WHERE절 이라고 생각하면 된다.

    create table chktbl(
    col1 number primary key,
    col2 Char(1) constraint chk_chktbl_col2 check(col2 IN ('F','M')),
    col3 number check(col3 >= 100 and col3 <= 200),
    col4 date check(col4 >= To_DATE('2021-02-24' and col4 <= TO_DATE('2021-08-23)),
    col5 char(14) check(regexp_like(col5,'^[0-9]{6}-[1-4]{7}$');


# 5] 테이블 변경

●안하는게 낫다

●테이블 구조와 데이터는 그대로 복사되지만, 제약조건(pk,fk,unique등)은 복사가 안된다.


# 6] Alter

●새로운 칼럼, 제약조건 추가

    Alter Table 테이블명 Add 컬럼명 자료형 Not Null    //가장 위험하다 칼럼 not null 하려면 그 행 다 지워야 한다,,
    alter table emp_copy add comm number(6,2)
    alter table emp_copy add constraint PK_emp_copy primary key(empno)
    alter table emp_copy drop constraint PK_emp_copy;
    alter table emp_copy drop column comm;
    alter table emp_copy modify empno NUMBER(2)  // 컬럼 자료형 바꿀때 반드시 더 큰 자료형으로 바꿔야 한다. 
    원본 데이터는 number(4) 2로바꾸면 오류 6을 바꾸면 성공
    alter table emp_copy rename column sal to salary // sal -> salar로 칼럼 명 변경
    rename emp_copy to EMP2    // 테이블 명 변경


# 7] DROP

●부모 테이블은 삭제가 안된다 (삭제하려면 함수 다름)

    Drop table emp2 // emp2 삭제
    Flashback table emp2 to before drop // 삭제한 테이블 복원
    Drop table emp2 pudge // 복원 불가능 완전 삭제

    Drop table 부모테이블 Cascade constraint // 부모 테이블 삭제

# SEQUENCE

●테이블의 필드에 일련번호 부여

●테이블 생성 후 시퀀스(일련번호)를 따로 만들어야 한다.

●테이블 하나 당 시퀀스 하나를 만들자

●DUAL : 출력을 위한 임시 테이블로 모든 사용자 계정이 가질 수 있다.

     [increment by 증가값]
     [start with seed값]
     [maxvalues n / minvalues n] 
     [cycle / nocycle] // 무조건 1보다 커야함
     // 최대 최소값을 도달한 후 계속 값을 생성할 지 여부 지정 (디폴트 노사이클)
     [cache / nocache] // CACHE메모리에 오라클 서버가 SEQUENCE값을 할당하는가 여부 지정 (디폴트로 CACHE) 
     // 캐쉬 기본 값이 20이라 maxvalues가 20보다 낮으면 오류다,
     // 그래서 노캐쉬 하던가 사이클을 maxvalues보다 낮게 지정하면 된다.


# 데이타 값 입
력
# 1] INSERT 문
●테이블 이름 다음에 나오는 열 생략 가능

●생략할 경우에 VALUE 다음에 나오는 값들의 순서 및 개수가 테이블이 정의된 열 순서 및 개수와 동일해야함

     Insert into 테이블명 (컬럼1, 컬럼2, 컬럼n)
        values(값1,값2,값n)

        insert into dmltbl 
        values(seq_dmltbl.NEXTVAL,'ID'||seq_dmltbl.NEXTVAL,20,default);


# 2]Update문

●기존에 입력되어 있는 값 변경하는 구문

●WHERE절 생략 가능하나 없으면 테이블의 전체 행의 내용이 변경됨

     update 테이블명
     set 컬러명 = 바꿀 값

     update dmltbl
     set age = 40, id = 'kosmo';

     update dmltbl 
     set id='KIM', age = 20
     where no=1;


# 3]Delete문

●행 단위로 데이터 삭제하는 구문

●DELECT FROM 테이블이름 WHERE 조건;

●데이터는 지워지지만 테이블 용량은 줄어들지 않음

●원하는 데이터만 지울 수 있음

●삭제 후 잘못 삭제한 것을 되돌릴 수 있음


     delete 
        from dmltbl
        where no=5;

        delete dmltbl
        where no >=2;


        TRUNCATE table 테이블명 : 즉 테이블안에 있는 모든 데이터를 삭제한다.
        (delete from 테이블 명과 같다, 속도는 빠르지만 복원 불가,,)

    
# VIEW 

●물리적인 공간을 차지하지 않는다.

●하나 또는 그 이상의 테이블로부터 생성된 가상의 테이블이다.

●실제 테이블처럼 행과 열을 가지고 있지만, 실제로 데이터를 저장하지는 않는다.

●DB의 선택적인 내용을 보여줄 수 있기 때문에 DB에 대한 엑세스 제한 기능 (보안 기능)

●복작한 질의어를 통해 얻을 수 있는 결과를 간단한 질의어를 써 구할 수 있다.

●하나의 테이블로 만든 VIEW에서는 DML문장을 수행 할 수 있지만 여러 테이블로 만든 VIEW에서는 DML문을 수행 할 수 없다. 단, UPDATE와 DELETE는 가능

●뷰의 목적은 SELECT다.

●뷰의 장점

    -특정 사용자에게 테이블 전체가 아닌 필요한 컬럼만 보여줄 수 있음

    -복잡한 쿼리를 단순화해서 사용

    -쿼리 재사용 가능
  
●뷰의 단점

    -한 번 정의된 뷰는 변경할 수 없음

    -삽입, 삭제, 갱신 작업에 많은 제한 사항을 가짐

    -자신만의 인덱스를 가질 수 없음
.
  
     create [or replace] view view명 // 별칭 하려면 ""로 감싸줘야한다.  [or replace] 같은 뷰 있으면 대체하겠다라는 뜻 
     as
     select 구문
     [with read only] // 뷰를 읽기 전용으로

     //생성
     create or replace view vw_emp("사원번호","이름","직무","입사일","부서코드")
     as
     select empno,ename,job, hiredate,deptno
     from emp
     order by sal;

    //삭제
     drop view VW_EMP;

     drop view vw_emp_dept;


# INDEX

●행의 검색 속도를 향상 시킬 수 있는 개체

●테이블에서 원하는 데이터를 빠르게 찾기 위해 사용

●인덱스를 명시적 (Create index) 또는 자동적으로 (primary key, unique key)로 생성 할 수 있다.

●컬럼에 대한 인덱스가 없으면 한 테이블 전체를 검색, 즉 인덱스는 쿼리의 성능을 향상 시키는 것이 목적

●Insert/update/delete가 많은 컬럼에 대해서 index를 되도록이면 설정하지 말아라

●인덱스가 많은 것이 항상 좋은것은 아니다, 왜냐하면 인덱스를 가진 테이블에 대한 DML작업은 인덱스도 갱신되여 함을 의미하기 때문

●인덱스는 수정 불가 수정시에는 삭제후 다시 생성

●어느 컬럼에 인덱스를 설정하는가?!

	-WHERE조건이나 조인 조건에서 자주 사용되는 컬럼
	-광범위한 값을 포함하는 컬럼
	-많은 null값을 포함하는 칼럼
	-테이블에 자료의 양이 적거나 자주 갱신되는 테이블은 오히려 인덱스를 걸지 말아라

    //생성
    Create index idx_emp on emp(deptno,sal,comm)  //조인이 많아서, 범위 넓어서, null이 많아서

    //삭제
    drop index idx_emp;
    
    
 # CURSOR
 
 ●select 문장에 의해 여러행이 RETURN되는 경우 각 행에 접근하기 위한 것

    CURSOR 커서명 IS
            SELECT문장 ----- DECLARE부에서 한다
            (INTO절이 없는 SELECT문)
            OPEN 커서명
            FETCH 커서명 
            INTO{variable1[,variable2,...]};
        
        CLOSE 커서명
        
        
        
        accept deptno prompt '부서코드 입력'
        declare
            --커서 정의
            CURSOR mycursor is
            select ename,trim(to_char(sal,'$99,999')) sal, dname,loc
            from emp e join dept d on e.deptno= d.deptno
            where e.deptno = &deptno;
            --변수 정의
            ename_ emp.ename%type;
            sal_ varchar2(10);
            dname_ dept.dname%type;
            loc_ dept.loc%type;
        begin
            --커서 오픈
            open mycursor;

            --FETCH하기
            fetch mycursor 
            into ename_,sal_,dname_,loc_;

            while mycursor%found loop
                --출력
                dbms_output.put_line(ename_ || ' : ' || sal_ || ' : ' || dname_ || ' : ' || loc_);
                --FETCH하기
                 fetch mycursor 
                 into ename_,sal_,dname_,loc_;
            end loop;
            --커서 닫기
            close mycursor;
        end;
        /
        
 # FUNTION
 ●다른 계정에 함수 실행권한 주기
 
-grant execute on 소유계정.함수명 to 부여받는 계정;
  
-grant execute on scott.get to hr;

    create or replace function getsum(num1 number, num2 in number)
      --반환타입 정의
      return number  --자리수 지정, 세미콜론 X
      --함수 시작
      is
      --변수 선언
          hap number :=0;
      begin
          for i  in num1 .. num2 loop
              hap := hap + i;
          end loop;
       return hap;
      end;
      /

      --호출 2가지 방법
      select getsum(1,10)
      from dual;

      var hap number;
      exec :hap := getsum(1,10)
      print hap;



      create or replace function get(en_ varchar2)
      return varchar2
      IS
      begin
         return  RPAD(substr(en_,1,1),length(en_),'*');
      end;
      /

      var ename_ varchar2;
      exec :ename_ := get('abcde')
      print ename_;

      select ename,get(ename)
      from emp;





      create or replace function getday(en_ date)
      return varchar2
      IS
      begin
         return  to_char(en_,'yyyy-mm-dd');
      end;

      select getday('21-08-13')
      from dual;

      select hiredate,getday(hiredate)
      from emp;
      
      
   # 저장 프로시져
  
  ●프로시저는 RETURN문이 없다. OUT 매개변수로 값을 RETURN한다.
  
●저장 프로시져의 장점

	-매우 좋은 성능 (여러명이 사용할 때 SQL문은 할때마다 parsing, 프로시져는 처음에 한번 만)
	-보안성을 높일 수 있음
	-다양한 처리가 가능
	-네트웍의 부하를 줄일 수 있음
  
●무조건 EXECUTE해야한다.

       //입력값 받는 프로스져
        create or replace procedure SP_INS_MEMBER(
        id_ member.id%type,
        pwd_ member.pwd%type,
        name_ member.name%type,
        RTVAL out NVARCHAR2
        )
        IS
        begin
            insert into member(id,pwd,name)
            values(id_,pwd_,name_);

            if SQL%FOUND then 
                RTVAL := '입력 성공';
                COMMIT;
            end if;

            exception
                when others then
                    ROLLBACK;
                    RTVAL := '입력실패 - 중복키거나 입력 값이 크다';
        end;
        /

       VAR RTVAL NVARCHAR2(50)
       EXEC SP_INS_MEMBER('KIM','1234','김길동',:RTVAL)       
       PRINT RTVAL
       SELECT * FROM MEMBER


       // 수정하는 프로시져
       create or replace procedure SP_UP_MEMBER(
       ID_ IN MEMBER.ID%TYPE,
       PWD_ MEMBER.PWD%TYPE,
       NAME_ MEMBER.NAME%TYPE,
       RTVAL OUT  Char
       )
       IS
       BEGIN
           update member
           set pwd = pwd_, name = name_
           where id = id_;

        IF SQL%FOUND THEN
           RTVAL :='SUCCESS';
           COMMIT;
       else 
           RTVAL := 'FAIL : NOT FOUND ID : ' || id_;
       END IF;

       EXCEPTION
           WHEN OTHERS THEN
               ROLLBACK;
               RTVAL :='FAIL : TOO MUCH VALUE';
       END;
       /

       var RT_VAR CHAR(50);
       exec SP_UP_MEMBER('KIM1','9999','가길동',:RT_VAR);
       print rt_var;

       select *
       from member;


       create or replace procedure SP_DEL_MEMBER(
       ID_ IN MEMBER.ID%TYPE,
       AFFECTED OUT  NUMBER
       )
       is
       begin
           delete member
           where id =id_;

       if SQL%FOUND then
           DBMS_OUTPUT.put_LINE(ID_||'가 삭제되었어요');
           AFFECTED := SQL%ROWCOUNT;
           commit;
       else 
            DBMS_OUTPUT.put_LINE(ID_||'가 존재하지 않아요');
            AFFECTED := -1;
          end if;

        EXCEPTION
           WHEN OTHERS THEN
               ROLLBACK;
              DBMS_OUTPUT.put_LINE('자식이 참조하고 있어요');
               AFFECTED := -2;
       end;
       /

       create table bbs(
       No number primary key,
       ID varchar2(10) references member(id),
       title nvarchar2(50) not null,
       postdate date default sysdate
       )

       create sequence seq_bbs
       nocache
       nocycle;

       insert into bbs 
       values(SEQ_BBS.NEXTVAL,'KIM','가길동입니다',SYSDATE);

       COMMIT;

       var return_var number;
       exec SP_DEL_MEMBER('KOSMO',:return_var);
       print return_var;


       //회원아이디와 비밀번호를 받아 회원인지 판단하는 프로시져
       create or replace procedure sp_ismember(
       id_ member.id%type,
       pwd_ member.pwd%type,
       RTVAL out number)
       is
           FLAG number(1);
       begin
           select count(*)
           into FLAG
           from member
           where id=id_;

           if FLAG = 0 then
               RTVAL := -1;
           else -- 아이디 일치
               select count(*)
               into FLAG
               from member
               where id=id_ and pwd = pwd_;

               if flag = 0 then -- 비밀번호 불 일치
                   RTVAL := 0;
               else 
                   RTVAL := 1;
               end if;
           end if;
       end;
       /

       --회원인 경우
       exec SP_ismember('KIM','9999',:return_var);
       print return_var;

       --아이디는 일치하는데 비밀번호 틀린경우
       exec SP_ismember('KIM','99',:return_var);
       print return_var;

       -- 아이디 불 일치
       exec SP_ismember('KIM1','9999',:return_var);
       print return_var;
   
   
   # 트리거
   
●자동으로 실행되는 프로시저의 한 종류, 직접 (exec) 실행 불가

●하나의 테이블에 최대 3개까지 트리거 적용 가능 단, 트리거 많을 수록 성능 저하 초래

●트리거 몸체(PL/SQL)안에는 COMMIT;,ROLLBACK불가

●:NEW(변경 후), :OLD(변경 전) 임시테이블을 행 단위 트리거에서만 사용 가능

      //트리거 생성
      Create Trigger 트리거명
      타이밍 [Before/after] 이벤트[insert [or] | update [or] | delete]
      on 트리거를 걸 테이블 명
      [for each row] --- 생략시 문자단위 트리거
      [when 트리거 조건]
      declare
      begin
      end;
      /


      // after 테이블
      create table before_RAISE(
           EVENT_STRING nvarchar2(10),
           postdate date default sysdate
       );

       create table target_trigger_table(
           no number primary key,
           title nvarchar2(10)
       );

       Create trigger trg_sample
       after insert or delete or update
       on target_trigger_table
       for each row
       declare
       begin
           if inserting then
               insert into before_raise values('insert',sysdate);
           elsif deleting then
               insert into before_raise values('delete',sysdate);
           elsif updating then
               insert into before_raise values('update',sysdate);

           end if;
       end;
       /

       select *
       from before_raise;

       select *
       from target_trigger_table;

       insert into target_trigger_table
       values(3,'3번');

       delete target_trigger_table
       where no >=2;

       update target_trigger_table
       set title = '일번'
       where no ='1';

       // before 트리거
       Create trigger trg_sample1
       before insert
       on target_trigger_table
       for each row
       declare
       begin
           if to_char(sysdate,'dy') = '수' or to_char(sysdate,'hh24') >= 17 then
               raise_application_error(-20001,'수요일 혹은 오후 5시에는 입력 불가');
           else
                insert into before_raise values('입력성공',sysdate);
           end if;
       end;
       /

       insert into target_trigger_table
       values(6,'6번');

       select *
       from before_raise;

       select *
       from target_trigger_table;



       // 상품 트리거


       --상품
       create table product(
           p_code char(4) primary key,
           p_name nvarchar2(10) not null,
           p_price number,
           p_qty number default 0
       )

       --입고
       create table ipgo(
           i_no number primary key,
           p_code char(4) references product(p_code),
           i_date date default sysdate,
           i_qty number,
           i_price number
       )

       -- 판매
       create table sales(
           s_no number primary key,
           p_code char(4) references product(p_code),
           s_date date default sysdate,
           s_qty number,
           s_price number
       )

       select * from product;
       select * from ipgo;
       select * from sales;

       insert into product(p_code,p_name,p_price)
       values('p001','노트북',2000);

       create trigger trg_ipgo1
       after insert 
       on ipgo
       for each row
       declare
       begin
           update product set p_qty = p_qty + :new.i_qty
           where p_code = :new.p_code;
       end;
       /

       insert into ipgo(i_no,p_code,i_qty,i_price)
       values(2,'p001',100,1500);

       create trigger trg_ipgo2
       after update 
       on ipgo
       for each row
       declare
       begin
           update product set p_qty = p_qty - :old.i_qty + :new.i_qty
           where p_code = :new.p_code;
       end;
       /

       update ipgo
       set i_qty = 50
       where i_no=2;


       create trigger trg_sales1
       before insert
       on sales
       for each row
       declare
           qty number; -- 재고 수량
       begin
           select p_qty
           into qty 
           from product
           where p_code = :new.p_code;
           if qty < :new.s_qty then
               raise_application_error(-20020,'재고가 없어요');
           else
               update product 
               set p_qty =p_qty - :new.s_qty
               where p_code = :new.p_code;
           end if;
       end;
       /

       insert into sales(s_no,p_code,s_qty,s_price)
       values(1,'p001',149,3000);


 
