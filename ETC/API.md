> 참고
[API란? 개념 정리와 포트폴리오에 유용한 대박 사이트 공유 🙌](https://youtu.be/ogT267HvNuQ)  
[REST API가 뭔가요?](https://youtu.be/iOueE9AXDQQ)  

# API란?
- Application Programming Interface
- 소프트웨어가 다른 소프트웨어로부터 지정된 형식으로 요청, 명령을 받을 수 있는 수단
- ex) 다양한 기기에서 서버에 있는 데이터를 읽고 쓰기 위해서 Web APIs를 이용해서 처리
- ex) Windows APIs
- `HTTP(s)` : 네트워크에서 기기들간에 의사소통을 해나가는 규격사항
- Web APIs를 어떻게 디자인해서 만들건지 정의하는 것
    - 예전에는 `SOAP` 이라는 형식으로 모든 네트워크 요청과 반응을 XML데이터 포맷에 주고 받음
    - 요즘에는 `REST` 형식을 사용
- 이제는 이런 Web API뿐만아니라 라이브러리나 프레임워크에서 이용할수 있는 클래스나 함수들도 `API`라고 부름


## Open/Public API란?
- 회사 내부에서 사용하는 Web API를 외부의 다른 개발자가 이용할 수 있도록 공개적으로 오픈한 것


# REST API란?
- `HTTP` 요청을 보낼 때 어떤 URI에 어떤 메소드를 사용할지 개발자들 사이에 널리 지켜지는 약속(형식)
1. Post(Create)
2. Get(Read)
3. Put(Update)
4. Delete(Delete)
5. Patch(일부 Update)
- get으로 데이터를 요청하면 JSON이라는 포맷에 받아올 수 있음