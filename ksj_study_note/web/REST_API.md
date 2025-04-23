# REST_API.md

## REST란?
> Representational State Transfer의 약자로, 자원을 URI로 표현하고, HTTP 메서드를 통해 해당 자원에 대한 행위를 정의하는 방식의 API 디자인 아키텍처다.

## 구성 원칙
- 자원의 URI는 명사로 표현
- 메서드로 행위를 정의 (GET, POST, PUT, DELETE 등)
- 무상태성
- 계층화 구조
- 캐시 가능성

## 예시
```
GET /users           # 사용자 목록 조회
POST /users          # 사용자 생성
GET /users/1         # 특정 사용자 조회
PUT /users/1         # 사용자 전체 수정
DELETE /users/1      # 사용자 삭제
```