# 스프링 시큐리티 핵심 개념과 인증/인가 구조

---

## 🔹 Spring Security란?

Spring Security는 스프링 기반 애플리케이션에서 **인증(Authentication)**과 **인가(Authorization)**를 담당하는 보안 프레임워크이다.  
보안 관련 기능(로그인, 권한 확인, 세션 관리 등)을 표준화된 방식으로 제공하며, 필터 기반 구조로 동작한다.

---

## 🔹 핵심 개념: 인증과 인가

| 구분       | 설명                                                   |
|------------|--------------------------------------------------------|
| 인증       | 사용자가 누구인지 확인 (로그인, 세션 인증 등)          |
| 인가       | 인증된 사용자가 어떤 자원에 접근 가능한지 판단         |

스프링 시큐리티는 이 두 개념을 기반으로 요청 흐름을 제어한다.

---

## 🔹 Spring Security 처리 흐름 요약

1. 사용자가 로그인 요청 (`/login`) 전송
2. `UsernamePasswordAuthenticationFilter`가 요청 가로채기
3. `AuthenticationManager`가 인증 시도
4. `UserDetailsService`를 통해 사용자 정보 조회
5. 인증 성공 시 `SecurityContextHolder`에 사용자 정보 저장
6. 인가 과정에서는 권한(ROLE)에 따라 접근 허용/거부 판단

---

## 🔹 주요 구성 요소 설명

| 컴포넌트                 | 설명                                                          |
|--------------------------|---------------------------------------------------------------|
| `AuthenticationManager`  | 인증을 총괄하는 인터페이스                                   |
| `UserDetailsService`     | 사용자 정보를 로딩하는 인터페이스 (`loadUserByUsername`)     |
| `UserDetails`            | 사용자 계정 도메인 객체 (username, password, authorities 등) |
| `GrantedAuthority`       | 사용자의 권한 정보 표현 (`ROLE_USER`, `ROLE_ADMIN` 등)       |
| `SecurityContextHolder`  | 현재 인증된 사용자 정보 저장소                                |
| `Authentication`         | 인증 객체 (사용자 정보 + 권한 정보 포함)                     |

---

## 🔹 인증 vs 인가의 분리 구조

- **인증(Authentication)**: `UsernamePasswordAuthenticationToken`, `AuthenticationManager`, `UserDetailsService`
- **인가(Authorization)**: `AccessDecisionManager`, `SecurityContextHolder`, URL 접근 제어

---

## 🔹 필터 기반 아키텍처

스프링 시큐리티는 `FilterChainProxy` 아래 수많은 보안 필터가 등록되어 있다.  
중요한 필터:

| 필터명                              | 역할                                 |
|-------------------------------------|--------------------------------------|
| `SecurityContextPersistenceFilter` | SecurityContext를 HTTP 세션과 연결   |
| `UsernamePasswordAuthenticationFilter` | 로그인 요청 처리 (기본: /login)  |
| `ExceptionTranslationFilter`       | 접근 거부/예외 상황 처리              |
| `FilterSecurityInterceptor`        | 인가(Authorization) 수행              |

---

## 🔹 권한 부여 방식

- 역할 기반 (`ROLE_USER`, `ROLE_ADMIN` 등)
- URL 기반 접근 제어 (`hasRole()`, `hasAuthority()` 등)
- 메서드 수준 제어 (`@PreAuthorize`, `@Secured`)

권한 설정은 `HttpSecurity` 설정 또는 애노테이션 방식으로 가능하다.

---

## 🔹 실무 보안 고려 사항

1. 모든 요청은 인증 필터를 거치도록 구성
2. 인증 토큰(JWT 등)을 사용한 Stateless 방식 설계 시 `SecurityContext` 수동 설정 필요
3. 세션 고정 공격 방지, CSRF, CORS, HTTPS 설정 등 종합적 고려 필요
4. 보안 이벤트 로깅 필수 (접속, 실패, 차단 등)

---

## ✅ 정리 요약

- Spring Security는 인증/인가를 명확히 구분하며, 필터 체인을 기반으로 보안 흐름을 제어한다.
- 구성요소 간 역할 분리가 명확하며, 인증 성공 시 SecurityContext에 사용자 정보가 저장된다.
- 실무에서는 보안 정책(로그인 방식, 인가 방식, 토큰 사용 등)을 아키텍처 설계 초기에 결정하고 적용해야 한다.
