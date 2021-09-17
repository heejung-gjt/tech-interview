## 웹 서버
인터넷을 기반으로 클라이언트에게 웹 서비스를 제공하는 컴퓨터    
웹서버는 항상 동일한 페이지를 클라이언트에게 반환해준다. 이미지, html, css, javascript등을 예로 들 수 있다   
> web   
> 인터넷을 기반으로 한 정보를 공유/검색 할 수 있게 하는 서비스 (url-주소, http-통신규칙, html-내용)   

> server   
> 클라이언트에게 네트워크를 통해 정보나 서비스를 제공하는 컴퓨터 시스템   

### 웹 서버의 역할
- 정적인 컨텐츠의 요청인 경우 was를 거치지 않고 바로 자원을 제공해준다
- 동적인 컨텐츠의 경우 요청을 was에 보내고 was가 처리한 결과를 클라이언트에게 전달한다   

예 ) nginx, apache, IIS

## WAS(Web Application Server)
웹 애플리케이션과 서버 환경을 만들어 동작시키는 기능을 제공하는 소프트웨어 프레임워크
db조회나 다양한 로직 처리를 요구하는 동적인 컨텐츠를 제공하기 위해 만들어진 application server이다   
was는 웹 서버로 프로그램을 실행시켜 만들어진 결과물을 클라이언트에게 반환해준다   

> web application   
> 웹에서 실행되는 응용 프로그램


### 실행과정
1. client가 was에 데이터를 요청한다
2. was 안에 있는 web server에서 정적요청인지 동적요청인지 파악한다
3. 동적요청일 경우 web container에 요청을 전달한다
4. container안에 servlet이 데이터를 생성하여 web server에게 전달한다
5. web server가 클라이언트에게 데이터를 보낸다    

예 ) IBM, TomCat, WebSphere

<br>

##### reference
[https://www.youtube.com/watch?v=NyhbNtOq0Bc](https://www.youtube.com/watch?v=NyhbNtOq0Bc)