# 🗂️ Serialization (직렬화)

**Serialization (직렬화)**은 객체의 상태를 **바이너리 형식**이나 **문자열 형식**으로 변환하여 저장하거나 네트워크를 통해 전송하는 과정입니다.  
반대로, **Deserialization (역직렬화)**은 이러한 직렬화된 데이터를 원래 객체로 복원하는 과정입니다.

---

## 💡 기본 개념

- **직렬화(Serialization)**: 객체를 **저장**하거나 **전송**할 수 있는 형식으로 변환하는 과정
- **역직렬화(Deserialization)**: 직렬화된 데이터를 **원래 객체**로 복원하는 과정

직렬화는 **파일 저장**, **네트워크 통신**, **데이터베이스 저장** 등에서 자주 사용됩니다.

---

## 🧩 직렬화의 목적

- **객체 저장**: 객체를 파일, 데이터베이스 등에 저장하고 나중에 복원하기 위함
- **네트워크 전송**: 분산 시스템에서 객체를 전송하기 위한 포맷으로 변환
- **데이터 공유**: 다른 시스템이나 애플리케이션 간에 데이터를 전송하는 데 사용

---

## 🔧 직렬화 형식

### 1. **JSON (JavaScript Object Notation)**

- **문자열 기반** 형식
- 사람이 읽을 수 있어 디버깅 용이
- **경량화**된 데이터 전송 형식

### 2. **XML (eXtensible Markup Language)**

- 태그 기반의 **구조적 데이터 포맷**
- JSON보다 **상대적으로 무겁고 읽기 어려움**
- 복잡한 데이터 구조에 적합

### 3. **Binary (이진 포맷)**

- **최소화된 크기**로 데이터를 전송
- **빠른 처리**가 필요할 때 적합
- 사람이 읽을 수 없음

---

## 🧱 직렬화 과정

1. **객체**를 직렬화하려면, 해당 객체는 **직렬화 가능한 클래스**이어야 하며, `Serializable` 인터페이스(혹은 유사한)를 구현해야 합니다.
2. 직렬화된 객체는 **파일**, **메모리**, **네트워크**를 통해 다른 시스템이나 애플리케이션으로 전송됩니다.
3. 수신 측에서 해당 데이터를 **역직렬화**하여 원래 객체 형태로 복원합니다.

---

## 📚 직렬화 사용 예시

| 사용 사례 | 설명 |
|-----------|------|
| **파일 저장** | 객체를 파일에 저장하고, 필요 시 복원 |
| **API 통신** | JSON 형식으로 객체를 API를 통해 전송 |
| **세션 관리** | 웹 애플리케이션에서 객체를 세션에 저장하거나 복원 |

---

## ✅ 직렬화의 장점

- **데이터 전송 효율성**: 네트워크를 통해 객체를 전송하거나 클라우드에 저장하는 데 유용
- **언어 간 호환성**: JSON, XML 등은 다양한 프로그래밍 언어에서 지원되어 **플랫폼 독립성**을 가짐
- **객체 상태 유지**: 객체의 상태를 유지한 채로 다른 시스템으로 전달 가능

---

## ⚠️ 직렬화의 단점

- **성능 문제**: 직렬화/역직렬화 과정에서 **CPU 자원**과 **시간**을 소모
- **보안 위험**: 직렬화된 객체에 **악성 코드**가 삽입될 수 있어, 역직렬화 시 주의가 필요
- **형식 불일치**: 객체 구조가 변경되면 이전 버전의 데이터와 호환되지 않을 수 있음

---

## 🧠 요약

- **Serialization**은 객체를 저장하거나 네트워크를 통해 전송 가능한 형식으로 변환하는 과정입니다.
- JSON, XML, Binary 등의 형식이 사용되며, 주로 **파일 저장**, **API 통신**, **세션 관리**에 활용됩니다.
- **역직렬화**는 직렬화된 데이터를 다시 원래 객체로 복원하는 과정입니다.
- 직렬화는 **성능**, **보안**, **형식 불일치** 등의 문제를 동반할 수 있으므로 주의가 필요합니다.

---
