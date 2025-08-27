---
title:  "SQL vs NoSQL: DBMS 개괄"
author: "Woohyuk Jang"
draft: false

date: "2023-02-23"
description: ""
categories:
  - cs/db
tags:
  - Blog
---
### SQL vs NoSQL: DBMS 개괄



1. NoSQL의 뜻



* NoSQL은 “Not only SQL”, 즉 SQL만을 사용하지 않는 DBMS을 의미한다.

* NoSQL은 관계형만을 사용하지 않는 데이터베이스를 포괄하는 개념이다.



2\. SQL vs NoSQL



* 구조 (structure)



​ ​ ​​​ ​ ​​​ ​ ​​​- SQL은 관계형 데이터베이스를 위한 것이다. 이는 잘 정의된 테이블, 제약 ​ ​ ​​​ ​ ​​​ ​ ​​​​ ​​​​(constraints), 관계 (relations) 등을 포함한다.



​ ​ ​​​ ​ ​​​ ​ ​​​- NoSQL은 key-value pair을 기반으로, 테이블, 문서 (JSON documents), ​ ​ ​​​ ​ ​​​ ​ ​​​ ​ ​​​ ​ ​​​ ​ ​​​​그래프 등의 여러 구조를 제공한다.



​ ​ ​​​ ​ ​​​ ​ ​​​- NoSQL은 스키마가 없다 (schemaless): 애자일 방법론에 어울린다.



* 저장 (storage)과 확장 (scale)



​ ​ ​​​ ​ ​​​ ​ ​​​- SQL은 전통적으로 모든 데이터를 한 노드(서버)에 저장했다. 이는 ​ ​ ​​​ ​ ​​​ ​ ​​​​ ​ ​​​ ​ ​​​ ​ ​​​​ ​ ​​​ ​ ​​​ ​ ​​​vertical scaling (서버 기기 성능 향상)만을 허용하고, 이는 한계가 있다.



​ ​ ​​​ ​ ​​​ ​ ​​​- 읽기의 경우 read replica로 horizontal scaling이 가능하다.



​ ​ ​​​ ​ ​​​ ​ ​​​- 최근에는 SQL로도 horizontal scaling (여러 서버에 데이터 분산 저장)을 ​ ​ ​​​ ​ ​​​ ​ ​​​허용한다: sharding



​ ​ ​​​ ​ ​​​ ​ ​​​- NoSQL은 해시 값을 기반으로 파티션을 나눠서 horizontal scaling이 가​ ​ ​​​ ​ ​​​ ​ ​​​​ ​ ​​​ ​ ​​​ ​ ​​​능하다.



* 접근 (access)



​ ​ ​​​ ​ ​​​ ​ ​​​- 관계형 데이터베이스는 SQL이나 ORM (Object Relational Mapping)으로 ​ ​ ​​​ ​ ​​​ ​ ​​​주요 사용한다. 이는 데이터베이스 엔드포인트에 연결을 요구한다.



​ ​ ​​​ ​ ​​​ ​ ​​​- NoSQL은 REST API나 벤더 제공 언어로 접근할 수 있다고 한다.



By [Woohyuk Jang](https://medium.com/@morrranii) on [February 23, 2023](https://medium.com/p/c34c8b988750).

Exported from [Medium](https://medium.com) on August 26, 2025.
