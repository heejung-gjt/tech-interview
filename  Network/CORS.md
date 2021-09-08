## SOP(Same Origin Policy/동일 출처 정책)란
```한 origin으로부터 로드된 document또는 script가 다른 origin의 리소스와 상호작용 할 수 있는 방법을 제한하는 중요한 보안 메커니즘이다. (mozilla.org)```      
다른 출처의 리소스를 사용하는 것에 제한하는 보안방식으로 같은 출처인지 아닌지 url을 통해 판단한다         
__document내에서 외부리소스들과 상호작용 할 때__ 리소스의 origin이 document의 origin과 다른 경우에 제한을 두는 방식이다       

쉽게 말해 데이터를 요청하는 url이 같은 출처인 경우 데이터를 주고받을 수 있게하는 웹 브라우저 정책이다    

<br>

## 같은 출처(origin)란

```https://www.naver.com:443/path/page.html``` 에서 브라우저가 이 origin을 따질 때에는 __scheme(https)__, __host(www.naver.com)__, __port(443)__ 로 따지게 된다

여기서 잠깐 이런 url을 살펴보자. http://localhost 와 http://127.0.0.1은 다른 출처이다. 같은 url이긴하지만 브라우저 입장에서는 다른 출처라고 판단한다. 브라우저는 url을 string value로 비교하여 판단하기 때문이다.    

<br>

## SOP의 필요성
SOP가 없다면 다른 origin의 문서와 마음대로 상호작용이 가능해진다. 그렇게 된다면 보안상 큰 문제가 발생한다   

예를 들어 nenen.com이라는 웹 사이트가 있을때 나쁜 의도를 가진 사람이 dead.com이라는 자신의 웹 서버로 유저를 유도하는 스크립트를 작성한다. 유저가 nenen.com에서 해당 기능을 작동되버리면 유저의 개인 정보는 dead.com으로 넘어가게 되는 보안적인 문제가 발생한다   

<br>

## CORS(cross resource sharing)

SOP의 정책을 따르게 되면 nenen.com의 웹 사이트는 정상적인 다른 사이트와도 통신할 수 없게 된다. (예를 들어 nnn.com에서 만든 api 서버와 통신이 불가능해진다) 그렇기 때문에 등장한 정책이 바로 CORS정책이다   

> CORS가 나오게 된 배경    

초창기에 웹은 단순히 문서를 제공해주는 용도였기 때문에 웹 사이트에서 다른 서버로 요청을 날리면 개인정보 유출등의 보안상 악의적인 행동을 하는것으로 의심하였다.     

많은 어플리케이션이 개발되면서 필요한 리소스를 서버에서 가져오기 위해 스크립트를 불러오는 기능인 script를 이용해 데이터를 받아오는 용도로 사용하여 우회적으로 사용하였다.   

이로인해 보안에 문제가 발생, 공식적인 루트로 다른 서버에서 리소스를 가져올 수 있도록 __CORS__ 가 등장했다    

<br>

## CORS란 
서로 다른 도메인을 가지고 있는 서버(서로 다른 origin)에서 리소스를 공유할 수 있도록 하기위해 내놓은 정책이다.    

서로다른 origin이라는 것은 도메인 혹은 포트가 다르다는 것을 의미한다

## CORS 동작방식
nene.com 사이트에서 nnn.com 사이트가 만든 api서버를 사용하고 싶을때 
먼저 nene.com 사이트에서 nnn.com 사이트에 요청을 보내도 되는지 물어본다.(pre-flight) nene.com에서 nnn.com에 요청을 보낼때는 http header에 {Origin : nene.com} 으로 요청하는 출처를 명시해주어야 한다    

이후 nnn.com의 서버가 다시 응답을 보낼때는 http header에 {Access-Control-Allow-Origin : 허용하는 주소}로 CORS를 허용할 URI를 명시해서 보낸다    

nene.com의 브라우저에서는 http header를 해석한 후 요청을 승인/거부 할지를 결정한다   

nene.com의 브라우저가 요청을 승인하면 nene.com 사이트에서는 이후 하려던 요청을 nnn.com의 서버에 보낸다      

<br>

## CORS 동작 원리
- 단순 요청 방법
- 예비 요청 방법

### Simple request
단순 요청 방법은 서버에게 바로 요청을 보내는 방법이다. 
- 서버에 API를 바로 요청한다      
- 서버는 Access-Control-Allow-Origin 헤더를 포함한 응답을 브라우저에 보낸다    
- 브라우저는 Access-COntrol-Allow-Origin헤더를 확인해서 cors 동작을 수행하지 확인한다       

#### simple request은 3가지의 조건을 만족해야 한다     
1. 요청 메서드는 GET, HEAD, POST 중 하나여야 한다

2. Accept, Accept-Language, Content-Language, Content-Type, DRP, Downlink, Save-Data, Viewport-Width, Width를 제외한 헤더를 사용하면 안된다   

3. Content-Type헤더는 application/x-www-form-urlencoded, multipart/form-data, text/plain 중 하나를 사용해야 한다    


### Preflight request
예비 요청 방법은 서버에 예비 요청을 보낸 후 안전한 사이트인지 판단한 후 요청을 보내는 방법이다. preflight요청은 실제 리소스를 요청하기 전에 OPTIONS라는 메서드를 통해 실제 요청을 전송할지 판단한다     

OPTIONS 메서드로 서버에 예비 요청을 먼저 보낸 후 서버에서 해당 요청에 대한 응답으로 Access-Control-Allow-Origin헤더를 포함한 응답을 브라우저에 보낸다.        

브라우저는 단순 요청과 동일하게 Access-COntrol-Allow-Origin헤더를 확인해서 cors동작을 수행할지 판단한다

(장고 rest api을 사용해보며 cors에 대한 에러를 정리할 예정 !)