# Day 2.
<br/>

<br/><br/>

## 정규표현식(Reqular Expression)
<br/>

### 개요
> * 소스 데이터에서 특정 패턴의 데이터가 있는가 확인하거나,
> * 특정 패턴의 데이터를 추출하기 위해 사용
> * 하나의 독립적인 컴퓨터 언어 형태로, 다양한 분야에서 활용됨(그러다 보니 서로 약간씩 다름)
<br/>

### 실행 단계
> * 1단계: 패턴 만들기
> * 2단계: 함수 적용(search, match, findall, sub)
> * 3단계: 적용결과 확인(group, groups, start, end, span)
<br/>

### 함수 확인
> * 실행 단계는 패턴을 만들고 원하는 함수를 적용해야 하지만,
> * 적용할 함수를 알아야 정확한 패턴을 작성할 수 있으니, 학습은 함수부터 진행

##### 주요 객체
> * search : 문자열 전체에서 매칭되는 부분 검색, 가장 많이 사용
> * match : 문자열의 처음에서 매칭되는 부분 검색
> * findall : 문자열 전체에서 매칭되는 모든 문자열을 리스트로 반환
> * finditer : findall과 같은데 iterator 객체로 반환

##### 메서드 함수
> * group() : 매칭된 문자열 반환
> * start() : 매칭된 시작 위치 반환
> * end() : 매칭된 종료 위치 반환
> * span() : 매칭된 문자열의 시작과 끝을 튜플로 반환
> * string : 매칭되면 대상 소스 문자열 전체를 리턴함
<br/>

### 패턴 만들기

##### 주요 문자들
> * . : 개행 문자를 제외한 1문자를 나타냄
> * ^ : 문자열의 시작을 나타냄
> * $ : 문자열의 종료를 나타냄
> * [] : 문자열의 집합을 나타냄 [abcd]는 'a', 'b', 'c', 'd'을 모두 나타냄
> * | : or 연산
> * () : 괄호 안의 정규식을 group으로 만듬
> * ? : 0 또는 1회 반복
> * '+' : 1회 이상 반복
> * '*' : 0회 이상 반복
> * {m} : 문자가 m회 반복
> * {m, n} : 문자가 m회 부터 n회까지 반복
> * {m, } : 문자가 m회 이상 반복
> * '\\' : 특수문자 표시
<br/><br/>

##### 실습
```python
soc_data = 'pizza Pizza test text Apple pizza apple APPLE Test Text'

# [ ]은 각각의 단어에 대해 개별 비교함
re.search('[az]', soc_data)                               # 'a'나 'z'가 하나라도 있으면, <class 're.Match'> <re.Match object; span=(2, 3), match='z'>
re.search('[az]', soc_data).group()                       # 'a'나 'z'가 하나라도 있으면, 첫번째 'z' 리턴
re.search('[az]', soc_data).string                        # 'a'나 'z'가 하나라도 있으면, soc_data 전체 리턴 

re.match('[pi]', soc_data)                                # 'p'나 'z'로 시작하면, 클래스 리턴 
re.match('[pi]', soc_data).group()                        # 'p'나 'z'로 시작하면, 첫번째 글자 리턴
re.match('[pi]', soc_data).string                         # 'p'나 'z'로 시작하면, soc_data 전체 리턴

re.search('test', soc_data)                               # 'test'문자가 있으면 매칭
re.search('te.t', soc_data)                               # 'test', 'text' 매칭
re.search('te.t', soc_data).group()                       # 'test' 리턴
re.search('te.t', soc_data).group(0)                      # 'test' 리턴
re.search('te.t', soc_data).group(1)                      # ()로 그룹을 만들지 않았기 때문에 (1)부터는 IndexError 발생

# ? : 앞 문자의 0 또는 1회 반복
re_pattern = 't?xt'                                       # 'xt', 'txt' 검색
# * : 앞 문자의 0회 이상 반복
re_pattern = 't*xt'                                       # 'xt', 'txt', 'ttxt', 'tttxt', ... 검색
# + : 앞 문자의 1회 이상 반복
re_pattern = 't+xt'                                       # 'txt', 'ttxt', 'tttxt', ... 검색

# ^ : 단일 문자열 내에서는 시작 문자열에서의 검색을 의미(match와 동일해짐)
re.search('^pi', soc_data)                                # 아래와 동일하게 매칭
re.match('pi', soc_data)
# $ : 단일 문자열 내에서 종료되는 부분 검사
re.search('ext$', soc_data)                               # 문자열이 'ext'로 종료되면 매칭

# [^abcd] : 'a', 'b', 'c', 'd'를 제외한 첫번째 글자 매칭
re.search('[^pizaPte ]', soc_data)                        # 공백까지 포함했기 때문에 첫번째 's'가 매칭
test = 'adcbcadxcbzdadcabdacbdacb'
print(''.join([s for s in test if re.search('[^abcd]', s)]))  # xz 출력
print(''.join([s for s in test if s not in 'abcd']))      # 위와 동일하게 출력

# []는 한 글자에 대한 영역임을 항상 기억
re_pattern = '[A-z]'                                      # 영문 대소문자가 하나라도 있으면 매칭
re_pattern = '[A-z0-9]'                                   # 영숫자가 하나라도 있으면 매칭

# \ 특수문자(여기에서 모든 문자라고 할 때 공백은 제외됨)
# \d : 모든 숫자
# \D : 숫자를 제외한 모든 문자
# \w : 모든 문자
# \W : 모든 문자 제외 문자
test = '감자는 6700원입니다.'
print(re.search('\d', test).group())                      # '6' 출력
print(re.search('\d+', test).group())                     # '6700' 출력
print(re.search('\D+', test).group())                     # '감자는'
print(re.search('\w+', test).group())                     # '감자는'
print(re.search('\W+', test).group())                     # ' ' (공백 1개)

# search와 양대산맥 findall (리스트 리턴)
test = '홍길동은 2001년 4월 27일에 태어남'
print(re.findall('\d', test))                             # ['2','0','0',...]
print(re.findall('\d+', test))                            # ['2001', '4', '27']



```

## Python으로 스크레이핑 하는 단계
> * 1단계: fetch(url)
> * 2단계: scrape(html)
> * 3단계: save(db_path, books)
