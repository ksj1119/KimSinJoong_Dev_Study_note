# CORS (Cross-Origin Resource Sharing)

## 개념
> 다른 출처(origin) 간의 자원 공유를 가능하게 해주는 브라우저 보안 정책.

## 주요 헤더
- Access-Control-Allow-Origin
- Access-Control-Allow-Methods
- Access-Control-Allow-Headers

## 동작 방식
1. 브라우저가 Preflight 요청 전송
2. 서버가 허용 여부를 응답
3. 허용 시 실제 요청 수행