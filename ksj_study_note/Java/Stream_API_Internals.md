# Stream API 내부 동작과 최적화 전략

---

## 🔹 Stream API의 철학

Stream은 Java 8부터 도입된 **데이터 중심 프로그래밍 모델**로,  
컬렉션 데이터를 **선언적(what)**으로 다루고 **지연 연산(lazy evaluation)**을 통해 최적화된 처리 흐름을 제공합니다.

Stream의 핵심 목표는 다음과 같습니다:

- 컬렉션 데이터의 함수형 처리
- 중간 연산과 최종 연산 분리
- 외부 반복(external iteration)을 내부 반복(internal iteration)으로 대체
- 병렬 처리 지원 (`parallelStream()`)

---

## 🔹 Stream의 실행 흐름

Stream은 다음 3단계로 구성됩니다:

1. **데이터 소스 생성**: `Collection`, `Array`, `Files`, `Optional`, `IntStream.range()` 등  
2. **중간 연산 연결**: `filter`, `map`, `sorted`, `distinct` 등 → **지연 실행**
3. **최종 연산 트리거**: `forEach`, `collect`, `reduce`, `count` 등 → **실제 실행**

중간 연산은 **Lazy**하게 실행되며, 최종 연산이 호출되기 전까지는 아무 작업도 수행되지 않습니다.

---

## 🔹 중간 연산과 최종 연산 구분

| 중간 연산        | 설명                             | 반환 타입     |
|------------------|----------------------------------|---------------|
| `filter(Predicate)` | 조건 필터링                    | Stream        |
| `map(Function)`     | 요소 변환                       | Stream        |
| `flatMap()`         | 중첩 구조 평탄화                | Stream        |
| `distinct()`        | 중복 제거                       | Stream        |
| `sorted()`          | 정렬                           | Stream        |
| `peek()`            | 디버깅용 중간 확인              | Stream        |

| 최종 연산        | 설명                             | 반환 타입     |
|------------------|----------------------------------|---------------|
| `forEach()`       | 각 요소에 대해 소비              | void          |
| `collect()`       | 리스트, 셋 등으로 수집           | Collection    |
| `reduce()`        | 누적 처리                        | Optional 또는 값 |
| `count()`         | 요소 수 계산                     | long          |
| `anyMatch()` 등   | 조건 검사                        | boolean       |

---

## 🔹 내부 반복과 외부 반복의 차이

- 외부 반복: `for` 또는 `Iterator`를 통해 사용자가 명시적으로 순회
- 내부 반복: Stream이 순회를 자체적으로 처리 → 병렬성 확보, 코드 간결성 증가

Stream의 내부 반복은 **Pipeline 구조**로 연결되며, 연산은 요소 단위로 하나씩 통과 처리된다.

---

## 🔹 지연 평가(Lazy Evaluation)와 단말 평가(Eager Evaluation)

- 중간 연산은 **lazy**하다: 여러 개를 연결하더라도 실제 계산은 수행되지 않음
- 최종 연산이 호출되는 순간, 중간 연산들이 조합된 pipeline이 **한 번에 실행됨**
- 이를 통해 불필요한 계산을 줄이고, 조건에 따라 연산을 조기에 종료할 수 있음

---

## 🔹 Stream의 병렬 처리

- `.parallelStream()` 또는 `.parallel()`을 사용하면 내부적으로 **ForkJoinPool**을 통해 병렬 실행됨
- CPU 코어 수에 따라 병렬로 분산 처리
- 다만, 병렬 Stream은 다음 조건에서만 성능 향상이 보장됨:
  - 요소 수가 많음 (수천 개 이상)
  - 각 요소 연산의 부하가 큼
  - 순서가 중요하지 않음
  - 공유 자원 접근 없음 (병목 방지)

---

## 🔹 Stream 처리 시 주의할 점

- **상태가 있는 중간 연산** (`sorted`, `distinct`)은 병렬 처리 시 성능 저하 유발 가능
- **side effect 있는 lambda** (`peek`, `forEach` 안에서 외부 변수 수정 등)는 지양
- Stream은 1회용이며, 재사용 불가 → 재사용하려면 Supplier 또는 새로 생성

---

## 🔹 성능 최적화 전략

1. **필터링 연산은 앞에 배치**  
   - `filter → map` 순서가 `map → filter`보다 성능 우수

2. **병렬 처리 여부는 실험적으로 결정**  
   - Stream 성능은 하드웨어, 데이터 크기, 연산 비용에 따라 달라짐

3. **Collect vs Reduce 명확히 구분**  
   - `reduce`는 누산/집계, `collect`는 변환 및 그룹화 목적

4. **기본형 Stream 사용 권장**  
   - `IntStream`, `LongStream`, `DoubleStream`을 사용하면 boxing/unboxing 오버헤드 방지

---

## ✅ 정리 요약

- Stream API는 선언형 데이터 처리와 지연 평가를 통해 간결하고 최적화된 데이터 처리를 가능하게 한다.
- 모든 중간 연산은 lazy하게 연결되며, 최종 연산이 호출될 때 실제로 실행된다.
- 병렬 스트림은 조건에 따라 성능을 향상시킬 수 있으나, 모든 경우에 적합하지는 않으며 검토가 필요하다.
- 스트림은 함수형 사고를 기반으로 설계되어 있으며, side effect를 최소화하고 순수 함수 중심으로 구성하는 것이 핵심이다.
