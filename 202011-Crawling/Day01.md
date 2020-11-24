# Day 1.
<br/>

> **전체 과정 소개:** <br/>
> * Python Data Type - 기초, 데이터 정체/분석용 위주
> * 중소기업 사례 
> * Web Service - request, response
> * Web Data 수집 - Crawling, 스크레이핑
> * Web Data 구조 - HTML, CSS, Javascript
> * BS4(Beautiful Soup), Selenium  사용법
> * Web Data 파일 내용 추출
> * Web Data 수집
> * (Web) Data 정제
> * Web Browser Driver(Chrome Driver)
> * Portal API => Data 추출

<br/><br/>

## Web Data 수집
<br/>

### 용어 정리
#### Crawling
> * Web page에서 정보를 수집하는것
>   * Web에서 하이퍼링크를 순회하면서 Web page의 내용을 수집 및 추출 하는것
#### 스크레이핑
> * Web page에서 수집한 데이터에서 필요한 정보를 추출 하는것
<br/>

### 기타
#### Web Data 수집 절차
> * 수집 - 분석 - 추출 - 가공 - 저장 - 시각화
#### 크롤링을 하는 도구 : 크롤러
> * 빅데이터 시대에 3V중 실시간성의 중요성에 의해 Web Data가 주목받으면서 수집 도구로서 급성장함
#### 자주 사용하는 도구들
##### wget
<pre>wget 'https://www.hanbit.co.kr/store/books/full_book_list.html' -outfile 'full_book_list.txt'</pre>

<br/><br/>

## Web Service
<br/>

### 기본 작동 원리
> * Client 요청(request)에 Server가 응답(response)하는 방식으로 작동
> * Client와 Server간에는 HyperLink문서를 HTTP protocol을 이용해 요청 및 제공
<br/>

### Web Page(Hypertext) 구조
#### HTML: Web page의 레이아웃과 내용을 채워주는 역할
> **HTML vs XML(Extensible Markup Language)**
> * 공통점: 인터넷을 통해 데이터를 주고 받을 수 있고 브라우저에서 볼 수 있음
> * 차이점: HTML은 공통 규약으로 정의된 Tag를 사용하고, XML은 사용자 정의 형태로 생각하면 됨
#### CSS: Web page를 꾸미는 역할
> * Cascading Style Sheets 
> * <style> ~ </style>
> * #: ID, .: class
> **xpath(XML path language):**
>   * xpath는 xml문서의 특정 부분의 위치를 찾을 때 사용하는 언어
>   * xpath는 xml문서 안의 요소와 속성들을 탐색함
#### Javascript: Web Page의 기능을 넣어주는 역할
> * **DOM(Document Object Model)을 이용함(중요)**
> * DOM: HTML문서 객체
>   * document.getElementById/Class('값') : 함수 이용
> * BOM(Browser Object Model)
#### Web 렌더링(Javascript+HTML+CSS Mix)
> * Javascript가 먼저 해석되고, DOM으로 해석된 HTML에 붙여가는 것
<br/>

### HTTP: Web protocol
#### 요청(request) Method
> * 조회:
>   * GET: URL에 Query String(가져올 정보를 특정할 수 있는 정보)을 넣어서 처리 - 주로 SELECT 처리
> * 수정:
>   * POST: 서버에 저장될 값(DATA)을 문서에 넣어서 전송, 전송이 올때마다 처리 - 주로 CREATE, UPDATE 처리
>   * PUT: POST와 유사하지만 자체 식별자를 가지고 동일 전송이 여러번 요청되도 한번만 처리됨
>   * PATCH: 자원을 업데이트하기 위해 사용하며, PUT은 자원 전체를 한번에, PATCH는 원하는 부분만 업데이트 가능
> * 삭제: DELETE
#### 응답(response) Code
> * 1xx: 조건부 응답(Query를 분리해서 처리해야 함)
> * 2xx: 성공
> * 3xx: Redirection(새로고침) 완료
> * 4xx: Request(요청)에 대한 오류(클라이언트에서 올라온 데이터에 의한 오류)
> * 5xx: Response(응답)에 대한 오류(서버에서 클라이언트로 보낼 데이터를 만들면서 생기는 오류)

### Web Page Header
#### Request Header
> * Accept-Charset(사용할 문자집합)
> * Accept-Encoding(인코딩 방법)
> * Cookie 정보
> * Refered(예전 접속 정보, 직전 주소 정보)
> * Method
##### Response Header
> * Status-Code
> * WWW-Authenticate(사용자 인증 요청 정보)
##### General Header
> * 날짜와 시간
> * Connection(연결 지속 정보)
##### Entity Header
> * Message 설명(Content-Encoding, Content-Length, Content-Type...

