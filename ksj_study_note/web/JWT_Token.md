# JWT_Token.md

## JWT란?
> JSON Web Token: 사용자 인증 정보를 JSON 객체로 안전하게 전달하는 방식

## 구조
- Header: 타입, 해시 알고리즘
- Payload: 사용자 정보, 클레임
- Signature: 서명 (비밀 키로 생성)

## 사용 예시
1. 로그인 성공 시 JWT 발급
2. 클라이언트가 JWT를 저장 후 요청 시 포함
3. 서버는 JWT를 검증하여 인증 수행