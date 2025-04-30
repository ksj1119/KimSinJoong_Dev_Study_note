# CORS (Cross-Origin Resource Sharing)

## 1. CORS란?

**CORS** (Cross-Origin Resource Sharing)는 웹 브라우저에서 **다른 도메인**의 리소스에 접근할 수 있도록 허용하는 메커니즘입니다. 기본적으로 웹 브라우저는 보안상의 이유로 다른 도메인에서 제공하는 리소스에 접근하는 것을 제한합니다. CORS는 이 제한을 풀고, 클라이언트가 다른 도메인의 리소스를 안전하게 요청할 수 있도록 도와줍니다.

## 2. Same-Origin Policy (SOP)

웹 브라우저는 **Same-Origin Policy (SOP)**라는 보안 정책을 따릅니다. 이 정책은 **"같은 출처에서만"** 리소스를 요청할 수 있도록 제한합니다. "출처"는 프로토콜(HTTP/HTTPS), 도메인, 포트를 포함하는 URI의 조합을 의미합니다.

예를 들어, `https://example.com`에서 `https://api.example.com`의 API를 호출하려고 하면 SOP 정책에 의해 제한됩니다. 이를 해결하기 위해 **CORS**를 사용합니다.

## 3. CORS의 작동 원리

CORS는 **HTTP 헤더**를 통해 클라이언트와 서버 간의 리소스 공유를 제어합니다. CORS 요청은 두 가지 종류로 나뉩니다:

### 1. 단순 요청 (Simple Request)
- **단순 요청**은 `GET`, `POST`, `HEAD` 메서드와 특정한 `Content-Type` 값을 가진 요청을 의미합니다.
- 예시:
  - `Content-Type`이 `application/x-www-form-urlencoded`, `multipart/form-data`, `text/plain`일 때는 단순 요청으로 간주됩니다.

### 2. 사전 요청 (Preflight Request)
- **사전 요청**은 CORS 요청 전에 HTTP `OPTIONS` 메서드를 사용하여 서버에 먼저 허용된 메서드와 헤더를 확인하는 요청입니다.
- 일반적으로 **복잡한 요청**이 있을 때 사용됩니다. 예를 들어, `Content-Type`이 `application/json`인 경우나, 커스텀 헤더를 사용하는 경우입니다.
