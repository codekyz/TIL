# OAuth란?

> 인터넷 사용자들이 비밀번호를 제공하지 않고 다른 웹사이트 상의 자신들의 정보에 대해 웹사이트나 애플리케이션의 접근 권한을 부여할 수 있는 공통적인 수단으로서 사용되는, 접근 위임을 위한 개방형 표준이다.
>
> 인증 프로토콜

- Resource Server : 자원을 보유하고 있는 서버(제공자)
- Resource Owner : 자원의 소유자(유저)
- Client : Server에서 정보를 가져오고자 하는 웹 어플리케이션

## OAuth의 동작 과정

1. Client 등록
   - Resource Server를 이용하기 위한 서비스 등록 과정(사전 승인)
   - Client ID, Client Secret(비밀키), Authorized redirect URL(Code를 전달받을 리다이렉트 주소)
2. Resource Owner의 승인
   - 각 제공자는 소셜로그인을 하기위해 url로 GET 요청을 보내도록 명시함
   - Resource Owner는 Client에서 해당 url로 연결되는 소셜 로그인 버튼을 클릭
   - Resource Owner는 로그인을 수행하고 완료되면 Server는 Query String으로 넘어온 파라미터들을 통해 Client를 검사함
     - Client ID 확인, Redirect URL 확인
3. Resource Server의 승인
   - 명시된 Redirect URL로 리다이렉트 시키고 Resource Server는 임시 암호인 Authorization Code를 함께 발급(Query String)
   - Client는 ID와 비밀키 및 Code를 Server에 직접 전달하고 유효한 요청이라면 Access Token을 발급받게 됨
4. API 호출
   - Client는 해당 토큰을 서버에 저장해두고 Server의 자원을 사용하기 위한 API호출시 토큰을 헤더에 담아서 보냄
5. Refresh Token
   - Refresh Token의 발급 여부와 방법 및 갱신 주기는 Server마다 상이함
   - 보통 Access Token을 발급할 때 Refresh Token을 함께 발급
   - Client는 두 Token을 모두 저장해두고 Access Token이 만료되어 401에러가 발생하면 Refresh Token을 보내 새로운 Access Token을 발급받음

### Reference

[OAuth 개념 및 동작 방식 이해하기](https://tecoble.techcourse.co.kr/post/2021-07-10-understanding-oauth/)
