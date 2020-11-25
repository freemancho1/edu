# Day 2.
<br/>

<img src="https://user-images.githubusercontent.com/31339365/100090897-3ccded00-2e97-11eb-8393-8979599c8f49.png" width="100%"></img>

<br/><br/>

## HTML 문서 수집 모듈
<br/>

### requests : 서비스 모듈
#### encoding: 2가지
> * UTF-8 : 조합형(초성, 중성, 종성을 분리해 코드화) => 현재의 Web에서 지원
> * EUC-KR : 한글 완성형 방식
>   * 확장된 ANSI : Excel  encoding='CP949'
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

### 파일 읽기
```python
# 파일에서 읽기
from bs4 import BeautifulSoup

with open('data/Test05.html', 'r', encoding='utf-8') as html_file:
    html = html_file.read()
    soup = BeautifulSoup(html, 'html.parser')
    
    print(soup)                            # 전체 출력
    
# Web에서 직접 읽기
from urllib.request import urlopen
from bs4 import BeautifulSoup

web_url = 'https://www.naver.com'
with urlopen(web_url) as response:
    html = response.read()
    soup = BeautifulSoup(html, 'html.parser')
```
<br/>

### Tag 찾기: find, find_all
> * Tag 위주 찾기, 클래스나 ID로도 찾을 수 있지만 이 경우는 select가 더 편해보임
> * find : 같은 조건 중 가장 먼저 찾은 하나만 추출
> * find_all : 같은 조건 모두 추출
> * find 계열에서 class를 지칭할 때 .을 사용하지 않음.
```python
# find 계열에서 class를 지칭할 때 .을 사용하지 않음.

# 데이터 추출
soup.find('li', {'id': 'c'}).text                           # Tag와 ID 조합 검색
soup.find('ul', {'class': 'greet'}).string                  # Tag와 class 조합 검색(클래스명 앞에 .을 붙이지 않음)
soup.find('ul', 'greet').get_text()                         # 위와 같은 결과(대상을 class에서 'greet'가 있는것을 참조)

soup.body.h1.div.p['id']                                    # 해당 tag의 ID값 추출(문자열, ID는 고유하기 때문)
soup.find_all('p')[0]['id']                                 # 가장 먼저 나오는 p tag의 id값 추출
soup.find_all('p')[-1].find('span')['class']                # 해당 tag의 class값 추출(리스트, 클래스는 여러개 올 수 있음)

soup.body.div.span.text                                     # Tag만으로 추출(head, body는 최상위 tag)

soup.find_all('p')[-1].find('span')                         # 아래 5개의 last_price는 모두 동일한 값을 찾는다
soup.find_all('p')[-1].find_all('span')[0]
soup.find_all('p')[-1].find_all('span', 'price')[0]         # price는 class
soup.find_all('p')[-1].find_all('span', {'class': 'price'})[0]
soup.find_all('span', {'class': 'price'})[-1]

# find_all(tag_name, attr, recursive, string, limit, **kwargs)
soup.find_all(['p', 'img'])                                 # 여러 태그를 검색할 경우에는 리스트 형태로 하나의 인자를 제공
soup.find_all('p', 'price')                                 # 위와 차이점은 리스트가 아닌 각각의 인자다. 따라서 두번째 'price'는 attr임
soup.find_all('p', {'id': 'fruits3'})                       # 바로 위와 같은 경우인데, 속성이 class만 'class'를 생략할 수 있음

# 데이터 조작
div_list = soup.findAll('div')                              # findAll도 유사하게 동작
for div in div_list:                                        # 모든 div 아래 있는 모든 span을 대상으로 
    for span in div.find_all('span'):                       # 작업하는 방법
        print(span.text)

for li in soup.body.ul.li.next_siblings:                    # Tag로 찾아서 다음 형제들 찾기
    print(li)
for li in soup.find('li', {'id': 'c'}).previous_siblings:   # Tag + ID로 이전 형제들 찾기
    print(li)

# 번외
p_text = [p.text.strip() for p in soup.find_all('p')]       # find_all 결과물 처리 방법
```
<br/>

### CSS Selector를 이용한 찾기: select, select_one
> * select_one : 같은 조건 중 가장 먼저 찾은 하나만 추출
> * select : 같은 조건 모두 추출
```python
 soup.select('p')                          # tag가 p인 모든 항목 추출
 soup.select_one('p')                      # tag가 p인 첫번째 항목 추출

 soup.find_all('p', {'class': 'name1'})    # find_all을 이용한 p tag중 class가 'name1'인 모든 항목 추출
 soup.select('p.name1')                    # select를 이용한 위와 동일한 처리

 soup.select('.price')                     # class가 'price'인 모든 항목
 soup.select('#fruits2')                   # id가 'fruits2'인 모든 항목

 soup.select('p > span')                   # p tag 아래에 있는 모든 span tag(p가 span의 부모일때만 가능 할아버지 이상의 조상이면 안됨)
 soup.select('#fruits2 > .store')          # 특정 조건의 태그 아래 특정 class 대상 추출

 soup.select('#fruits2 > .store')[0].text  # select의 모든 결과는 리스트이기 때문에 [x] 배열로 처리해야 함

 soup.select('span[class]')                # class가 있는 모든 span 추출
 soup.select('span[class="count"]')        # class가 'count'인 모든 span 추출

 soup.select('a[href]')[0].text            # href가 있는 a tag 중 첫번째 tag의 text 추출
 soup.select('a[href]')[0]["href"]         # href가 있는 a tag 중 첫번째 tag의 속성 href의 값 추출(주소값 추출)
```
<br/>

### 불필요한 부분 제거: extract()
> * tag path나 find()를 이용해 해당 태그를 찾은 후 삭제함
> * find_all(), select()를 이용한 경우 for문에서 각각 처리해줌
```python
a = soup.body.extract()                     # soup에서 body 부분을 삭제해 soup에 저장하고 삭제된 body부분은 a에 저장함
a = soup.find('p', 'price').extract()       # 조건에 맞는 p tag 삭제

for tag in soup.select('p'):                # 조건의 결과가 리스트면, for문으로 처리
    tag.extract()                           # 리스트 일괄처리는 없는듯;;
del_tag = [tag.extract() for tag in soup.select('p')] # 결과도 받을 수 있음    
```  
