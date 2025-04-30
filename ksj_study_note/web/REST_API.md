# REST API

## 1. REST란?

**REST** (Representational State Transfer)는 웹 서비스를 구축하기 위한 아키텍처 스타일입니다. REST는 HTTP를 기반으로 하며, 클라이언트와 서버 간의 데이터 전송 방식을 규정합니다. RESTful API는 REST의 원칙을 따르는 API입니다.

### REST의 주요 원칙
1. **무상태성 (Stateless)**: 서버는 클라이언트의 상태 정보를 저장하지 않습니다. 각 요청은 독립적으로 처리되며, 이전 요청의 상태를 알 필요가 없습니다.
2. **표현 (Representation)**: 리소스는 서버에서 표현된 형태로 클라이언트에게 전달됩니다. 이 표현은 XML, JSON, HTML 등 다양한 형식일 수 있습니다.
3. **클라이언트-서버 구조 (Client-Server Architecture)**: 클라이언트와 서버는 독립적으로 동작하며, 서로 다른 시스템에서 서로 다른 역할을 수행합니다.
4. **캐시 가능 (Cacheable)**: 클라이언트는 서버로부터 받은 데이터를 캐시할 수 있습니다. 이를 통해 불필요한 서버 요청을 줄이고 성능을 향상시킬 수 있습니다.
5. **계층화된 시스템 (Layered System)**: 클라이언트는 서버의 실제 구현을 알지 못합니다. 서버는 여러 계층으로 구성되어 있을 수 있습니다.
6. **일관된 인터페이스 (Uniform Interface)**: RESTful API는 일관된 방식으로 리소스를 접근할 수 있도록 합니다.

## 2. RESTful API의 기본 HTTP 메서드

RESTful API에서는 주로 **HTTP 메서드**를 사용하여 리소스에 대한 CRUD(Create, Read, Update, Delete) 작업을 수행합니다.

### 1. GET
- **목적**: 서버에서 리소스를 조회합니다.
- **사용 예**: 특정 사용자 정보를 조회, 게시글 목록 조회 등.
- **예시**:
  ```http
  GET /users/1
