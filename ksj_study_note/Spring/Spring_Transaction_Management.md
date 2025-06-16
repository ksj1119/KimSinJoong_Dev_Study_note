# 트랜잭션 관리와 선언적 트랜잭션 설정

---

## 🔹 트랜잭션이란?

트랜잭션(Transaction)은 **하나의 논리적 작업 단위**로, 데이터베이스 상태를 변화시키는 일련의 연산 집합을 의미한다.  
트랜잭션은 다음의 ACID 특성을 만족해야 한다:

- **Atomicity (원자성)**: 전부 성공하거나 전부 실패해야 한다.
- **Consistency (일관성)**: 트랜잭션 전후 데이터의 무결성이 유지되어야 한다.
- **Isolation (격리성)**: 동시에 실행되는 트랜잭션은 서로 간섭하지 않아야 한다.
- **Durability (지속성)**: 트랜잭션 완료 후 데이터는 영구적으로 반영되어야 한다.

---

## 🔹 스프링의 트랜잭션 추상화

Spring은 다양한 기술(JDBC, JPA, Hibernate 등)을 일관된 방식으로 관리할 수 있도록 **트랜잭션 추상화 계층**을 제공한다.

| 구성 요소                    | 설명                                  |
|-----------------------------|---------------------------------------|
| `PlatformTransactionManager`| 핵심 인터페이스                        |
| `DataSourceTransactionManager` | JDBC 기반 구현체                    |
| `JpaTransactionManager`     | JPA 환경에서 사용                      |
| `TransactionDefinition`     | 전파 방식, 격리 수준, 타임아웃 등 정의 |
| `TransactionStatus`         | 트랜잭션 실행 상태 정보 제공           |

---

## 🔹 선언적 트랜잭션 관리

`@Transactional` 어노테이션을 통해 **설정만으로 트랜잭션을 적용**할 수 있다.  
서비스 계층에 선언하는 것이 일반적이며, 메서드 단위 또는 클래스 단위로 사용 가능하다.

속성 예시:
- `rollbackFor`, `noRollbackFor`
- `propagation`, `isolation`, `timeout`, `readOnly`

기본적으로 `RuntimeException`이나 `Error` 발생 시 자동 롤백되며, `Checked Exception`은 명시적으로 롤백 지정 필요.

---

## 🔹 트랜잭션 전파 속성 (Propagation)

전파 속성은 **이미 존재하는 트랜잭션이 있을 때의 동작 방식**을 정의한다.

| 속성           | 설명                                                    |
|----------------|---------------------------------------------------------|
| REQUIRED       | (기본값) 기존 트랜잭션이 있으면 참여, 없으면 새로 생성 |
| REQUIRES_NEW   | 항상 새로운 트랜잭션 생성, 기존 트랜잭션 일시 중단     |
| NESTED         | 중첩 트랜잭션 생성, 부모 롤백과는 별도로 커밋/롤백 가능|
| MANDATORY      | 트랜잭션이 반드시 존재해야 하며 없으면 예외 발생        |
| NEVER          | 트랜잭션이 있으면 예외 발생                             |
| NOT_SUPPORTED  | 트랜잭션 없이 실행                                      |
| SUPPORTS       | 트랜잭션이 있으면 참여, 없으면 트랜잭션 없이 실행       |

---

## 🔹 격리 수준 (Isolation Level)

격리 수준은 **동시성 제어와 무결성 보장**을 위해 설정된다.

| 수준              | 설명                                  | 허용 현상           |
|-------------------|---------------------------------------|----------------------|
| READ_UNCOMMITTED  | 커밋되지 않은 데이터도 읽기 가능       | Dirty Read 허용      |
| READ_COMMITTED    | 커밋된 데이터만 읽기                   | Non-repeatable Read  |
| REPEATABLE_READ   | 트랜잭션 동안 같은 값 보장             | Phantom Read 가능    |
| SERIALIZABLE      | 가장 엄격, 모든 동시성 문제 방지        | 성능 저하 우려       |

---

## 🔹 롤백 정책

- 기본: `RuntimeException`, `Error` 발생 시 자동 롤백
- `Checked Exception` 발생 시 자동 롤백되지 않음 → `rollbackFor` 필요

예시 속성:
- `@Transactional(rollbackFor = SQLException.class)`
- `@Transactional(noRollbackFor = IllegalArgumentException.class)`

---

## 🔹 실무 원칙 요약

1. 트랜잭션은 **서비스 계층**에 선언
2. 핵심 로직 단위로 정의하고 **작게 쪼개지 말 것**
3. **롤백 정책은 예외 유형에 맞게 세밀하게 설정**
4. **트랜잭션 범위는 최소화**하여 리소스 낭비 방지
5. 격리 수준과 전파 설정은 **비즈니스 요구에 맞게 조절**

---

## ✅ 정리 요약

- 스프링은 선언적 방식으로 트랜잭션을 관리하며, 핵심 비즈니스 로직에 집중할 수 있도록 지원한다.
- `@Transactional` 어노테이션 하나로 트랜잭션 전파, 롤백 조건, 격리 수준 등을 유연하게 제어 가능하다.
- 트랜잭션 전략은 애플리케이션의 동시성, 안정성, 성능 요구를 종합적으로 고려하여 설계해야 한다.
