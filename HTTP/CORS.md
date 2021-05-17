## CORS(cross resource sharing)
서로 다른 Origin에서 리소스를 공유할 수 있도록 하기 위해 내놓은 정책이다. 서로 다른 도메인 주소 사이에서 데이터(api 요청)를 주고받을 수 있도록 하기 위한 정책이다

어떤 출처에서 불러운 문서나 스크립트가 다른 출처에서 가져온 리소스와 상호작용하는 것을 제한하는 보안 방식을 의미한다. 

추가 HTTP 헤더를 사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제이다


오픈 API에 요청을 보내고 응답받는 일을 많이 하게 된다
이때 자주 발생하는 에러로 CORS에러가 있다 

프론트 레이어와 API서버레이어를 따로 구성하는 경우가 많다
웹프론트엔드 사이트 따로 서버따로 둔다
웹프론트엔드에서 다른 도메인에 위치한 API서버로 요청을 넣어야 하는 상황이 생긴다

