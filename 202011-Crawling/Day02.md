# Day 2.
<br/>

<br/><br/>

## HTML 문서 수집 모듈
<br/>

### requests : 서비스 모듈
#### encoding: 2가지
> * UTF-8 : 조합형(초성, 중성, 종성을 분리해 코드화) => 현재의 Web에서 지원
> * EUC-KR : 한글 완성형 방식
>   * 확장된 ANSI : Excel
##### web페이지의 encoding 확인
```python
import requests as req
url = 'https://www.naver.com'
print(req.get(url).encoding)   # 현재 HTML문서의 encoding 방법 확인
```
##### URL 호출
```python
import json
import requests as req

url = 'https://www.naver.com'

# GET Method
params = {'name': 'Tom', 'pwd': '1234'}
result = req.get(url, params=params)

# POST Method
data = json.dumps({'name': 'Jane', 'pwd': '3456'})
result = req.post(url, data=data)
```
##### 내용 확인
```python
    print(result.text)            # encoding = result.encoding
    print(result.content)         # encoding = 없음(binary?)
```
<br/>

### urllib : 내장 모듈
> * 멤버 항목을 보유하고 있음
```python
from urllib.request import urlopen, Request

url = 'https://www.naver.com'

req = Request(url)
html = urlopen(req)

print(html.read())
print(html.headers)
print(html.code)
print(html.url)
print(html.info())
print(html.info().get_content_charset())
```
<br/>

### requests vs urllib : 개발자의 개인취향이긴하나 6:4정도로 활용됨
> * 요청 객체 생성방법이 다름
> * data 전송 시
>   * requests : dict 형태 전송
>   * urllib : 인코딩 후, binary 형태 전송
> * 요청 페이지가 없을 경우
>   * requests : 에러 표현을 않함(내용이 없는 것 등으로 확인)
>   * urllib : 에러를 표현 함

<br/><br/><br/>

## Beautiful Soup 수집
<br/>

### 기본
> * 파싱(Parsing) 모듈
<br/>

### 개념 정리
> * 파서(Parser)
>   * lxml - XML 해석이 가능한 파서
>   * html5lib - 웹브라우저 방식으로 HTML 해석(2.x 버전)
>   * html.parser - HTML 파서, 가장 많이 사용
<br/>

### Tag 찾기: find, find_all
> Tag 위주 찾기, 클래스나 ID로도 찾을 수 있지만 이 경우는 select가 더 편해보임
> find : 같은 조건 중 가장 먼저 찾은 하나만 추출
> find_all : 같은 조건 모두 추출
```python
from bs4 import BeautifulSoup

with open('data/Test05.html', 'r', encoding='utf-8') as html_file:
    html = html_file.read()
    soup = BeautifulSoup(html, 'html.parser')
    
    print(soup)                                               # 전체 출력
    
    print(soup.find('li', {'id': 'c'}).text)                  # Tag와 ID 조합 검색
    print(soup.find('ul', {'class': 'greet'}).string)         # Tag와 class 조합 검색(클래스명 앞에 .을 붙이지 않음)
    print(soup.find('ul', 'greet').get_text())                # 위와 같은 결과(대상을 class에서 'greet'가 있는것을 참조)
    
    print(f'{soup.body.ul["id"]}')                            # 해당 tag의 id값 출력, class도 동일
    
    div_list = soup.findAll('div')                            # findAll도 유사하게 동작
    for div in div_list:                                      # list형식으로 하나를 찾으려면 div_list[0] 이런 식으로 찾아야 함
        for span in div.find_all('span'):
            print(span.text)
            
    span_text = soup.body.div.span.text                       # Tag만으로 추출(head, body는 최상위 tag)
    
    for li in soup.body.ul.li.next_siblings:                  # Tag로 찾아서 다음 형제들 찾기
        print(li)
    for li in soup.find('li', {'id': 'c'}).previous_siblings: # Tag + ID로 이전 형제들 찾기
        print(li)
        
    last_price = soup.find_all('p')[-1].find('span')          # 아래 5개의 last_price는 모두 동일한 값을 찾는다
    last_price = soup.find_all('p')[-1].find_all('span')[0]
    last_price = soup.find_all('p')[-1].find_all('span', 'price')[0]            # price는 class
    last_price = soup.find_all('p')[-1].find_all('span', {'class': 'price'})[0]
    last_price = soup.find_all('span', {'class': 'price'})[-1]
    
    p_text = [p.text.strip() for p in soup.find_all('p')]     # find_all 결과물 처리 방법
    
    p_and_img = soup.find_all(['p','img'])                    # 여러 태그를 검색할 경우에는 리스트 형태로 인자를 제공
```
<br/>

### CSS Selector: select, select_one
> select_one : 같은 조건 중 가장 먼저 찾은 하나만 추출
> select : 같은 조건 모두 추출
