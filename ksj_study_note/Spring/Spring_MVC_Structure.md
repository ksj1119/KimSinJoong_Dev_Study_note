# Spring MVC 구조와 DispatcherServlet 흐름

---

## 🔹 Spring MVC란?

Spring MVC는 Model-View-Controller 디자인 패턴을 기반으로 하는 웹 프레임워크이다.  
**요청 처리 흐름의 명확한 분리**를 통해 유지보수성과 확장성을 높이며, HTTP 요청을 일관성 있게 처리한다.  
핵심 컴포넌트는 DispatcherServlet을 중심으로 구성된다.

---

## 🔹 MVC 구성 요소

| 구성 요소  | 설명                                                         |
|-------------|--------------------------------------------------------------|
| Model       | 데이터와 비즈니스 로직을 담당하는 부분 (VO, DTO, Entity 등) |
| View        | 사용자에게 보여지는 화면 (JSP, Thymeleaf 등 사용)            |
| Controller  | 요청을 받아 처리하고, 적절한 응답 또는 뷰를 반환함           |

---

## 🔹 DispatcherServlet의 역할

DispatcherServlet은 **프론트 컨트롤러(Front Controller)**로서 모든 HTTP 요청을 수신하고 적절한 컴포넌트에 위임한다.  
Spring MVC의 요청 처리 흐름의 중심에 위치한다.

---

## 🔹 요청 처리 흐름 요약

1. **클라이언트 요청**
   - 브라우저가 특정 URL로 HTTP 요청을 보냄

2. **DispatcherServlet**
   - 웹.xml 또는 Spring Boot 설정에 의해 등록된 중앙 진입점
   - 요청을 받아 적절한 핸들러(컨트롤러)를 찾음

3. **HandlerMapping**
   - 요청 URL에 맞는 컨트롤러를 탐색
   - 애노테이션 기반(`@RequestMapping`) 또는 XML 기반 매핑

4. **HandlerAdapter**
   - 컨트롤러 호출을 위한 어댑터
   - 다양한 컨트롤러 구현체를 일관되게 처리

5. **Controller**
   - 요청 로직 수행
   - Model 객체에 데이터 저장, View 이름 반환

6. **ViewResolver**
   - 반환된 View 이름을 실제 View로 매핑
   - JSP, Thymeleaf 등 템플릿 처리

7. **View**
   - 사용자에게 최종 HTML 응답을 렌더링하여 반환

---

## 🔹 주요 컴포넌트 역할 정리

| 컴포넌트            | 역할                                                     |
|---------------------|----------------------------------------------------------|
| DispatcherServlet   | 모든 요청 수신 및 흐름 제어                               |
| HandlerMapping      | 어떤 컨트롤러가 요청을 처리할지 결정                      |
| HandlerAdapter      | 컨트롤러를 실행할 수 있도록 돕는 어댑터                   |
| Controller          | 요청 로직 및 모델 처리                                    |
| ModelAndView        | 뷰 이름 + 데이터 모델을 함께 반환                         |
| ViewResolver        | 뷰 이름을 실제 뷰 구현체로 변환 (예: JSP 파일 경로 매핑)  |
| View                | 최종 렌더링 대상, 사용자에게 HTML 응답 생성               |

---

## 🔹 어노테이션 기반 컨트롤러 구성 요소

| 어노테이션            | 설명                                                |
|------------------------|-----------------------------------------------------|
| `@Controller`         | 컨트롤러 클래스 정의                                |
| `@RequestMapping`     | 요청 URL, HTTP 메서드, 파라미터 등을 매핑           |
| `@GetMapping`         | GET 요청 처리 (`@RequestMapping(method = GET)`)    |
| `@PostMapping`        | POST 요청 처리                                      |
| `@ModelAttribute`     | 폼 데이터를 모델 객체로 바인딩                      |
| `@RequestParam`       | 요청 파라미터 단일 값 바인딩                        |
| `@ResponseBody`       | 반환값을 JSON 등 응답 본문으로 직접 전달            |

---

## 🔹 Spring Boot에서 DispatcherServlet 설정

- Spring Boot에서는 `DispatcherServlet`이 자동으로 등록되며 `/` 경로를 기본 매핑으로 사용
- 커스터마이징이 필요할 경우 application.properties 또는 Java 설정으로 변경 가능

---

## ✅ 정리 요약

- Spring MVC는 요청과 응답을 효과적으로 분리하기 위한 구조이며, DispatcherServlet이 흐름을 총괄한다.
- 요청은 HandlerMapping, Controller, ViewResolver 등을 거쳐 최종 뷰로 응답된다.
- 애노테이션 기반의 간결한 설정을 통해 복잡한 웹 요청 처리 로직을 효과적으로 구현할 수 있다.
