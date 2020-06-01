---
layout: post
title: Hierarchical and Network Database Model 계층형 & 네트워크 데이터베이스 모델
comments: true
categories: [Database]
---

# Hierarchical DB Model

## Hierarchical DB, 계층형 데이터베이스의 특징

---

![DB1](/public/images/db1.PNG)

- 뒤집힌 트리 구조 (Reversed Tree-like structure)

  - 데이터베이스에 있는 하나의 테이블이 뿌리 역할을 한다.
  - 다른 테이블은 뿌리에서 파생된 가지가 된다.
  - 부모/자식 관계로 표현된다.
  - 각각의 부모는 여러 자식을 가질 수 있지만 자식은 오직 하나의 부모만을 가질 수 있다.
  - one-to-one, one-to-many relationships

- 왜 Hierarchical DB 을 사용할까?
  - 테이블 구조 사이에 명시적 링크(Explicit Link)가 있어서 사용자가 데이터를 매우 빠르게 검색할 수 있다.
  - 참조 무결성(Referential integrity)이 내장되어 있으며 자동적으로 시행된다.

### What is a Referential integrity? 참조 무결성이란?

---

참조 무결성(Referential integrity)은 관계 내에서 데이터의 정확성과 일관성을 가리킨다.

참조 무결성이 보장하는것은 ?

- 하위 테이블의 레코드는 상위 테이블의 기존 레코드와 연결된다
- 상위 테이블에서 삭제된 레코드로 인하여 하위 테이블의 모든 관련 레코드도 삭제가 된다.

### The problem of the Hierarchical DB, 계층형 DB의 문제

---

계층형 DB를 사용한다면 어떨 때 문제가 발생할까?

사용자가 부모 테이블의 레코드와 관련이 없는 자식 테이블에 리코드를 저장할때 문제가 발생하게 된다.

사용자는 새로운 엔터테이너가 Agents 테이블에 있는 한 에이전트에 할당되지 않는한 새로운 엔터테이너를 Entertainers 테이블에 넣을 수 없다. 자식 테이블(Entertainers)에 있는 레코드는 부모 테이블(Agents)에 있는 레코드와 반드시 관련되어야 하기 때문이다.

하지만 실생활에서는 엔터테이너들은 특정한 에이전트에 할당되기 전에 에이전시와 계약한다.

따라서 계층형 데이터베이스는

- 복잡한 관계(Complext Relationship) 표현이 어렵다.
- 중복 데이터(Redundant data) 와 관련된 문제가 발생한다.

# Network DB Model
---
Network DB는 Hierarchical DB의 문제를 해결하기 위해서 개발되었다.

![DB2](/public/images/db2.PNG)

## Network DB, 네트워크 데이터베이스의 특징
---
- 노드(Node) 와 집합구조(Set Structure) 로 표현된다.
  - 노드는 레코드의 모음, 집합 구조는 테이터베이스 간의 관계를 표현한다.
  - 한 쌍의 노드에서 하나를 owner, 또 하나는 member로 표현한다.
  - one-to-many 관계
  - member 노드의 레코드는 onwer 노드의 레코드와 반드시 연결되어야 한다.
  - owner 노드에 있는 레코드는 하나 또는 여러개의 member 노드에 있는 레코드와 연결될 수 있다.
  - member 노드에 있는 레코드는 owner 노드에 있는 레코드와 관련되지 않으면 존재할 수 없다.

* 왜 Network DB 를 사용할까?

  - 데이터를 빠르게 찾을 수 있다.
  - 복잡한 쿼리를 만들고 사용할 수 있다.

* Problems 문제점
  - 데이터베이스의 구조를 바꾸기 어렵다.
    - 집합 구조를 통해 작업해야 하기 때문에 데이터베이스 구조에 대해서 잘 알아야 한다는 단점이 있다.
  - 네트워크 데이터베이스와 연동되어 있는 어플리케이션에 영향을 주지 않고 집합 구조를 변경할 수 없다.
    - 집합 구조를 변경하기 위해서 모든 어플리케이션을 수정해야 한다.

## Conclusion 결론
---
대규모 데이터를 다루기 위해서는 계층형 & 네트워크 데이터베이스 모두 알맞지 않다. 그래서 등장한것이 관계형 데이터베이스 모델 (Relational Database Model) 이다.

참고 서적: 파워 오브 데이터베이스, 송현호,황규용 Database Design for Mere Mortals: A Hands-On Guide to Relational Database Design, 3rd Edition, 마이클 J. 헤르난데즈
