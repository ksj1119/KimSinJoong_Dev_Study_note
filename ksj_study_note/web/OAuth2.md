# OAuth2.md

## OAuth 2.0이란?
> 타사 서비스의 리소스를 사용자의 인증을 통해 접근할 수 있도록 해주는 인증 프레임워크

## 구성 요소
- Resource Owner: 사용자
- Client: API 사용 애플리케이션
- Authorization Server: 인증 서버
- Resource Server: 자원 서버

## 흐름 예시 (Authorization Code)
1. 사용자 로그인 및 동의
2. Authorization Code 발급
3. 토큰 요청 후 Access Token 수신