## HTTP 요청/응답 헤더

### 요청(request)
요청을 보낼때 요청에 대한 정보를 담아 서버로 보낸다
브라우저에 url을 친 후 요청을 보내면 GET/http://url.com HTTP/1.1 요청을 보내는것과 같다. 이때 주소와 함께 HTTP 메서드를 같이 보낼 수 있다
#### HTTP 메서드
__GET__ : 지정된 리소스(URL)을 요청    
__POST__ : 서버가 클라이언트의 폼 입력 필드 데이터의 수락을 요청, 클라이언트는 서버로 HTTP Body에 Data를 전송한다    
__HEAD__ : 문서의 헤더 정보만 요청하며, 응답데이터(BODY)를 받지 않는다   
__PUT__ : 클라이언트가 전송한 데이터를 지정한 URI로 대체한다. 클라이언트는 서버로 HTTP Body에 data를 전송한다    
__DELETE__ : 클라이언트가 지정한 URI를 서버에서 삭제한다    


### 요청/응답 공통헤더
요청과 응답에 모두 사용되는 헤더이다. 

__Date__ : HTTP 메시지가 만들어진 시각이다. 자동으로 생성된다 ```Date: Fri, 03 Jul 2021 03:12:27 GMT```   

__Connection__ : Connection은 기본적으로 keep-alive로 되어있는데 사실 아무 의미가 없다. HTTP/2에서는 아예 사라졌다    

__Cache-Control__ : 매우 중요한 부분이다. 
  - 아무것도 캐싱하지 않으려면 ```Cache-Control: no-store```을 하면된다. 
  - Cache-Control: no-cache는 no-cache이지만 캐시하지 말라는 뜻이 아니라 모든 캐시를 쓰기 전에 서버에 이 캐시를 진짜 써도 되냐고 물어보라는 뜻이다   
  - Cache-Control: must-revalidate는 만료된 캐시만 서버에 확인을 받도록 한다. ```Cache-Control: public 또는 private``` public이면 공유개시에 저장해도 된다는 뜻이고 private이면 브라우저 같은 특정 사용자 환경에만 저장하라는 뜻이다   

__Content-Length__ : 요청과 응답 메시지의 본문 크기를 바이트 단위로 표시해주며 메시지 크기에 따라 자동으로 만들어진다 ```Content-Length: 30```   

__Content-Type__ : 컨텐츠의 타입과 문자열 인코딩을 명시할 수 있다. ```Content-Type: text/html; charset=utf-8```    

__Content-Encoding__ : 컨텐츠가 압축된 방식으로 응답 컨텐츠를 압축하여 보내면 브라우저가 알아서 해제해 사용한다. 컨텐츠 용량이 줄기 때문에 압축하여 보내는 것을 권장한다(요청이나 응답 전송 속도가 빨라진다)   

<br>

### 요청 헤더

__Host__ : 서버의 도메인 네임이 나타나는 부분이다(포트도 포함이다) ```Host: www.url.com```   

__User-Agent__ : 현재 사용자가 어떤 클라이언트를 이용해 보냈는지 나온다 ```User-Agent: Chrome/67.0.3396.99 Safari/537.36```   

__Accept__ : 요청을 보낼때 서버에 원하는 타입의 데이터를 보냈으면 좋겠다고 명시할 때 사용한다 ```Accept: text/html``` (HTML형식인 응답을 처리하겠다는 뜻이다)    
Accept-encoding등 원하는 형식을 Accept를 통해 서버에 보내면 서버는 이에 맞춰 데이터를 보내준다   

__Authorization__ : 인증 토큰(JWT, Bearer token)을 서버로 보낼때 사용하는 헤더이다. api 요청등을 할때 토큰이 없으면 거절당하기 때문에 Authorization을 사용한다 ```Authorization: Bearer xxxxxx```    

__Origin__ : post요청등을 보낼때 요청이 어느 주소에서 시작되었는지를 나타낸다. 이곳에서 요청을 보낸 주소와 받는 주소가 다르면 __CORS문제__ 가 발생한다   

__Referer__ : 해당 페이지 이전의 페이지 주소가 담겨있다. 이 헤더를 이용해 어떤 페이지에서 지금 페이지로 들어왔는지 알 수 있다 (애널리틱스등에 사용)

<br>


### 응답 헤더

__Access-Control-Allow-Origin__ : 요청을 보내는 프론트 주소와 받는 백엔드 주소가 다르면 __CORS문제__ 가 발생한다. 이때 서버에서 응답 메시지 Access-Control-Allow-Origin 헤더에 프론트 주소를 적어주어야 에러가 발생하지 않는다 ```Access-Control-Allow-Origin: www.url.com```   
만약 응답을 보내는 주소를 일일이 지정하기 싫다면 * 을 사용하여 모든 주소에 CORS요청을 허용하면 된다(보안에 취약해지는 단점이 존재)   

__Allow__ : allow 헤더는 CORS요청 외에도 적용이 된다. ```Allow: GET```  GET요청만을 허용한다는 뜻이다.    

__Content-Disposition__ :  응답 본문을 브라우저가 어떻게 표시해야 할지 알려주는 헤더이다. inline인 경우 웹 페이지 화면에 표시되고 attachment인 경우 다운로드된다   

__Location__ : 어느 페이지로 이동할지를 알려주는 헤더이다  ```Location: /``` 인 경우는 브라우저는 /주소로 리다이렉트 한다    

__Content-Security-Policy__ : 다른 외부 파일들을 불러오는 경우, 차단할 소스와 불러올 소스를 이곳에 명시할 수 있다. ```Content-Security-Policy: default-src https:``` 인 경우는 https를 통해서만 파일을 가져올 수 있게 한다는 뜻이다. 