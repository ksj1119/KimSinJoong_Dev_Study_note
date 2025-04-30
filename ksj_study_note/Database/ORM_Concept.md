# 🧩 ORM (Object-Relational Mapping) 개념

**ORM(Object-Relational Mapping)**은 객체 지향 프로그래밍 언어에서 객체를 데이터베이스의 테이블과 자동으로 매핑해주는 기술입니다. 즉, **코드의 객체와 DB의 데이터를 연결해주는 중간 계층** 역할을 합니다.

---

## 📘 핵심 개념

- **객체(Object)** ↔ **테이블(Table)**
- **속성(Property)** ↔ **컬럼(Column)**
- **인스턴스(Instance)** ↔ **레코드(Row)**

ORM을 사용하면 SQL문을 직접 작성하지 않고, 객체를 통해 DB 작업(CRUD)을 수행할 수 있습니다.

---

## 🛠️ 주요 특징

- **SQL 추상화**: SQL문 없이 메서드 호출로 데이터 조작 가능
- **자동 매핑**: 클래스와 테이블 간의 매핑 자동 처리
- **생산성 향상**: 반복되는 SQL 작성 부담 감소
- **유지보수 편의**: 코드 중심으로 DB 접근 가능

---

## 📚 ORM의 장점

- 코드 중심의 개발 → 직관적이고 생산성 높음
- 데이터베이스 독립성 확보 (다른 DB로의 전환이 쉬움)
- 보안 향상 (SQL Injection 방지에 유리)
- 재사용성 및 테스트 용이

---

## ⚠️ ORM의 단점

- 복잡한 쿼리 처리에는 한계 (성능 저하 가능성)
- 내부 동작 이해 부족 시 디버깅 어려움
- 자동화된 쿼리가 비효율적일 수 있음
- 대규모 시스템에서는 세밀한 SQL 튜닝이 필요함

---

## 🔍 주요 ORM 프레임워크

| 언어 | ORM 도구 |
|------|-----------|
| Java | Hibernate, JPA (EclipseLink, Spring Data JPA 등) |
| Python | SQLAlchemy, Django ORM |
| JavaScript | Sequelize, TypeORM, Prisma |
| PHP | Doctrine, Eloquent (Laravel) |
| Ruby | ActiveRecord (Rails) |

---

## ✅ ORM 사용이 적합한 경우

- 애플리케이션 로직 중심으로 데이터 모델링할 때
- SQL보다 객체 중심 코드 유지보수가 중요한 경우
- 반복적인 CRUD 작업이 많은 경우

---

## 🚫 ORM보다 SQL이 유리한 경우

- 매우 복잡한 쿼리, 조인, 최적화가 필요한 경우
- 성능 튜닝이 중요한 실시간 데이터 처리 시스템
- 트랜잭션 처리와 쿼리 제어가 중요한 경우

---
