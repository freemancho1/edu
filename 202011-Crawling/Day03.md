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
> * group : 매칭된 문자열 반환
> * start : 매칭된 시작 위치 반환
> * end : 매칭된 종료 위치 반환
> * span : 매칭된 문자열의 시작과 끝을 튜플로 반환
<br/>

### 패턴 만들기

##### 주요 문자들
> * . : 개행 문자를 제외한 1문자를 나타냄
> * ^ : 문자열의 시작을 나타냄
> * $ : 문자열의 종료를 나타냄
> * [] : 문자열의 집합을 나타냄 [abcd]는 'a', 'b', 'c', 'd'을 모두 나타냄
> * | : or 연산
> * () : 괄호 안의 정규식을 group으로 만듬?
> * ? : 0 또는 1회 반복
> * + : 1회 이상 반복
> * * : 0회 이상 반복
> * {m} : 문자가 m회 반복
> * {m, n} : 문자가 m회 부터 n회까지 반복
> * {m, } : 문자가 m회 이상 반복
