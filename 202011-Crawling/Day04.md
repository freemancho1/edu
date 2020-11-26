# Day 4.
<br/>

<br/><br/>

## selenium 사용
<br/>

### 개요
> * 드라이브 브라우져를 사용해 직접 사용자가 클릭하듯 진행 가능
> * 브라우져를 숨겨 처리할 수 있음(인터넷 참조)

```python
from selenium import webdriver
from bs4 import BeautifulSoup
from html import unescape

target_url = 'https://www.naver.com/'
driver_path = 'C:\\Users\\freeman\\PycharmProjects\\Crawling\\chrome-d87.0.4280\\chromedriver.exe'

driver = webdriver.Chrome(driver_path)

driver.get(target_url)

query_text = '봄여행'
target_tag = driver.find_element_by_css_selector('#query')
target_tag.send_keys(query_text)

driver.find_element_by_css_selector('#search_btn').click()
driver.find_element_by_css_selector('#lnb > div.lnb_group > div > ul > li:nth-child(2) > a').click()

html = driver.page_source
soup = BeautifulSoup(html, 'html.parser')

for idx, tag in enumerate(soup.find_all('a', 'api_txt_lines total_tit')[:4]):
    print(f'{idx}: {unescape(tag.text).strip()}')
```
> * 이 부분을 활용하면 다양한 분야에서 활용 가능
