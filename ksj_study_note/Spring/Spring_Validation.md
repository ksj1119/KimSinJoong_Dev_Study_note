# 스프링에서의 입력 검증 (Validation)

---

## 🔹 입력 검증이란?

입력 검증(Validation)은 **클라이언트로부터 받은 데이터가 유효한지 검사하는 과정**이다.  
스프링에서는 폼 데이터, API 요청, 바인딩 객체 등을 검증할 수 있는 다양한 방법을 제공하며,  
이를 통해 **데이터 무결성 확보, 보안 강화, 예외 방지** 등이 가능하다.

---

## 🔹 검증 방식 분류

1. **명시적 검증 (수동 검사)**  
   - 컨트롤러에서 직접 조건을 검사하고 에러 처리 수행

2. **Bean Validation (표준 방식)**  
   - `javax.validation` 기반의 어노테이션 사용
   - `@Valid`, `@NotNull`, `@Size` 등의 제약 조건 선언

3. **스프링 Validator 인터페이스 활용**  
   - 복잡하거나 커스텀 검증이 필요한 경우 유용

---

## 🔹 Bean Validation의 주요 어노테이션

| 어노테이션         | 설명                                      |
|--------------------|-------------------------------------------|
| `@NotNull`         | null 값 불허                               |
| `@NotEmpty`        | null 또는 빈 문자열 불허                   |
| `@NotBlank`        | null, 빈 문자열, 공백만 있는 문자열 불허    |
| `@Size(min, max)`  | 문자열, 컬렉션 등의 크기 제약               |
| `@Email`           | 이메일 형식 검사                           |
| `@Pattern`         | 정규식 기반 검증                           |
| `@Min`, `@Max`     | 숫자 범위 지정                             |
| `@Positive`        | 양수만 허용                                |
| `@Past`, `@Future` | 과거/미래 날짜 여부                        |

---

## 🔹 검증 적용 흐름 (Annotation 기반)

1. DTO에 제약 조건 어노테이션을 추가  
2. 컨트롤러에서 `@Valid` 또는 `@Validated` 적용  
3. `BindingResult` 파라미터를 통해 검증 실패 여부 확인  
4. 에러가 있다면 사용자에게 적절한 응답 또는 뷰 반환

---

## 🔹 `@Valid` vs `@Validated`

| 어노테이션     | 설명                                      |
|----------------|-------------------------------------------|
| `@Valid`       | JSR-303 표준 검증 (javax.validation)       |
| `@Validated`   | 스프링 자체의 검증, 그룹 검증 지원 가능    |

※ 그룹 검증이 필요 없는 일반적인 경우에는 `@Valid`를 사용해도 무방

---

## 🔹 BindingResult란?

스프링 MVC에서 `@Valid` 또는 `@Validated`로 검증 시,  
**바로 다음 파라미터에 `BindingResult`를 선언하면** 검증 오류 발생 시 예외가 아닌 결과 객체로 반환된다.

이 객체는 다음 정보를 포함함:

- 필드별 에러 메시지
- 전체 유효성 결과
- 사용자에게 반환할 오류 정보

---

## 🔹 Validator 인터페이스 구현

복잡한 로직이 필요한 경우, Spring의 `org.springframework.validation.Validator` 인터페이스를 구현할 수 있다.  
커스텀 객체에 대해 수동 검증이 가능하며, `supports()` 및 `validate()` 메서드를 통해 적용 범위와 검증 로직을 정의한다.

Controller에서는 `WebDataBinder`를 통해 해당 Validator를 등록하거나, 전역 Validator 설정 가능

---

## 🔹 검증 실패 처리 전략

- Form 기반: 모델에 에러 메시지를 담아 뷰로 되돌림
- REST API 기반: `@RestControllerAdvice` 또는 `@ExceptionHandler`를 활용한 JSON 에러 응답 제공
- 글로벌 메시지 처리: `message.properties`에 에러 메시지 키 정의하여 국제화 대응 가능

---

## ✅ 정리 요약

- 스프링은 Bean Validation을 통해 어노테이션 기반 검증 기능을 제공하며, 복잡한 로직은 Validator 인터페이스로 확장 가능하다.
- 검증은 주로 DTO에 선언되며, 컨트롤러에서 `@Valid` 또는 `@Validated`를 통해 활성화된다.
- 검증 실패 시 `BindingResult`를 활용하면 예외 없이 유연한 오류 처리가 가능하다.
- REST와 Form 기반 응답 모두에 맞게 유연하게 대응할 수 있는 설계가 중요하다.
