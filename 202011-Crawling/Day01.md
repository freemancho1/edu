# Day 1.
<br/>

> **전체 과정 소개:** <br/>
> * Python Data Type - 기초, 데이터 정체/분석용 위주
> * 중소기업 사례 
> * Web Service - request, response
> * Web Data 수집 - Crawling, 스크레이핑
> * Web Data 구조 - HTML, CSS, Javascript
> * BS4(Beautiful Shup), Selenium  사용법
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
#### Javascript: Web Page의 기능을 넣어주는 역할
<br/>

### HTTP: Web protocol
