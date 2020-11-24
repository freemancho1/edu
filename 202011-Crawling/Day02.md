# Day 2.
<br/>

<br/><br/>

## HTML 문서 수집 모듈
<br/>

### requests
#### encoding: 2가지
> * UTF-8 : 조합형(초성, 중성, 종성을 분리해 코드화) => 현재의 Web에서 지원
> * EUC-KR : 한글 완성형 방식
>   * 확장된 ANSI : Excel
##### web페이지의 encoding 확인
```python
import requests as req
url = 'https://www.naver.com'
result = req.get(url)
print(result.encoding)
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
<br/>

### urllib
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


## Beautiful Soup 수집
<br/>

### 용어 정리
#### Crawling
> * Web page에서 정보를 수집하는것
