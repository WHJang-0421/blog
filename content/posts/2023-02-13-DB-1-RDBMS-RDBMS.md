---
title:  "오라클 DB 1: RDBMS의 개념과 오라클 RDBMS"
author: "Woohyuk Jang"
draft: false

date: "2023-02-13"
description: ""
categories:
  - cs/db
tags:
  - Blog
---
### 오라클 DB #1: RDBMS의 개념과 오라클 RDBMS



이 글은 책 [오라클로 배우는 데이터베이스 입문](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=171630125)을 읽고 정리했다.



1. 데이터베이스란?



* 데이터(data)는 특정 목적으로 사용하기 위해 기록된 자료이다. 이 데이터를 분석/가공하면 정보(information)을 얻을 수 있다.

* 과거에는 파일 시스템을 이용하여 데이터를 관리했다. 파일 시스템은 각 프로그램별로 자기가 사용할 데이터를 관리하는 방식이다. 이때 데이터의 누락/중복이 발생하고, 데이터의 관리 방식 역시 일관되지 않다.

* 교훈: 데이터의 누락/중복을 피하고 일관된 방법으로 데이터를 관리하기 위해서는 데이터를 통합하여 관리해야 한다. (이때 여러 사용자의 공동 실시간 이용을 지원해야 한다)

* 이런 이유로 통합되어 관리되는 데이터의 집합체를 데이터베이스(database)라고 한다. DBMS (database management system)은 데이터베이스의 접근, 관리를 담당하는 소프트웨어이다.



2\. 데이터 모델



* 데이터 모델은 컴퓨터에 데이터를 저장하는 방식에 대한 개념 모형이다.

* 계층형 데이터 모델 (hierarichical data model): 트리 형태. 1:N 구조를 표현하기에 적합하다.

* 네트워크형 데이터 모델 (network data model): 그래프 형태. 다대다 구조를 표현하기에 적합하다.

* 객체 지향형 데이터 모델 (object-oriented data model): 객체 지향. 데이터를 독립된 객체로 생각한다.

* 관계형 데이터 모델 (relational data model): 관계(relationship)에 집중. 관계형 데이터베이스에서 더 자세히 설명한다.



3\. 관계형 데이터베이스



* RDBMS (relational database management system)이 관리한다.

* RDBMS는 SQL (structured query language)라는 데이터베이스 질의 언어를 사용하여 다룬다.

* SQL은 data query, data manipulation, data definition, transaction control, data control 등을 할 수 있다.



4\. 관계형 데이터베이스의 구성 요소



* 테이블: 2차원 표.

* 행 (row): record라고도 한다.

* 열 (column)

* 키 (key)



키에 주목해야 한다. 키는 다음과 같이 나뉜다.



* 기본키 (PK; primary key): 테이블에서 특정 행을 식별하기 위한 열이다. 식별하기 위해서는 값의 중복이 없어야 하고, NULL이면 안된다. 기본키는 한개만 만들 수 있다.

* 복합키 (composite key): 여러 열을 묶어서 기본키로 쓰는 것이다. 가능하면 피하자.

* 후보키 (candidate key): 기본키가 될 수 있는 모든 키. 기본키도 후보키다.

* 대체키 (alternate key): 기본키가 아닌 후보키.

* 외래키 (FK; foriegn key): 다른 테이블의 기본키인 열. 외래키를 통해 이 테이블이 다른 테이블을 참조할 수 있다.



5\. 오라클



* 오라클 데이터베이스는 가장 널리 쓰이는 RDBMS이며, 특히 legacy 기업에서 많이 쓰인다.

* 오라클은 관계형에 객체 지향의 개념을 추가한 객체 관계형 (object-relational) DBMS이다.

* 오라클은 PL/SQL (Procedural Language extension to SQL)을 제공한다.



6\. 오라클의 자료형



* VARCHAR2(길이): 가변 길이 문자열. (1byte-400byte)

* NUMBER(전체 자리수, 소수점 이하 자리수): 숫자 (\~38자리)

* DATE: 날짜.

* 그 외 CHAR (고정 길이 문자열), NVARCHAR2 (National VARCHAR2), BLOB (Binary Large Objects), CLOB (Character Large Objects), BFILE (Binary File) 등이 있다.



7\. 관련 프로그램의 설치



* 인터넷을 보니 WSL2 + Docker + 오라클 환경설정을 할 수 있는 것 같다. 하지만 나는 Docker에 대해 아무것도 모르므로 그냥 책에 나와있는대로 하기로 했다.

* 오라클 데이터베이스 Express 11g와 Toad for Oracle을 설치했다.



8\. 참고 자료/더 깊이 파보고 싶다면!



[**\[DB개념\] :: The Relational Data Model (관계형 데이터 모델)**\

*The Relational Data ModelData modelingWhat is data modeling?컴퓨터에 저장할 데이터의 구조를 논리적으로 표현하기 위한 행위.주어진 개념으로부터 논리적인 데이터 모델을…*&#x63;hartworld.tistory.com](https://chartworld.tistory.com/6 "https://chartworld.tistory.com/6")[](https://chartworld.tistory.com/6)



[**\[데이터베이스\]릴레이션 키 개념& 종류(기본키, 슈퍼키, 대체키, 복합키, 후보키)&특징, 유일성 최소성이란?**\

*데이터베이스\] 데이터베이스 완벽 정리 목차 오늘은 데이터베이스 릴레이션 키에 대해서 알아볼거예요. 키의 개념은 영어를 하기 위해서는 알파벳을 알아야 하는 것처럼 기본 중의 기본에 해당합니다. 키란? Key…*&#x6A;hnyang.tistory.com](https://jhnyang.tistory.com/71 "https://jhnyang.tistory.com/71")[](https://jhnyang.tistory.com/71)



[**Do it! 오라클로 배우는 데이터베이스 입문**\

*현업 프로그래머이자 강사인 저자가 수많은 프로젝트 경험을 살려 실무에서 진짜 필요한 기본기를 중심으로 내용을 구성했다. 본문 내용은 비전공자도 알기 쉽게 도해와 비유로 풀어 썼고 427개의 예제는 실무에서 ...*&#x77;ww.aladin.co.kr](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=171630125 "https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=171630125")[](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=171630125)



By [Woohyuk Jang](https://medium.com/@morrranii) on [February 13, 2023](https://medium.com/p/d0026a78c607).

Exported from [Medium](https://medium.com) on August 26, 2025.
