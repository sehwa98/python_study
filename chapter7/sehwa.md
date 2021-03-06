# 7장 데이터 주무르기

## 7.1 텍스트 문자열

### 7.1.1 유니코드

#### 유니코드
 숫자와 글자, 즉 키와 값이 1:1로 매핑된 형태의 코드이다.

 파이썬 3 문자열은 유니코드 문자열이다.

 기본 평면 : \u + 4자리 16진수(평면 번호 + 평면에 있는 문자의 인덱스)

 높은 평면 : \U + 8자리 16진수

> <참고> 유니코드 : https://ko.wikipedia.org/wiki/%EC%9C%A0%EB%8B%88%EC%BD%94%EB%93%9C_0000~0FFF

```python

import unicodedata

def unicode_test(value):
	name = unicodedata.name(value)    # 인자로 유니코드 문자를 취하고, 대문자 이름을 반환한다. 
	value2 = unicodedata.lookup(name) # 대/소문자를 구분하지 않는 인자를 취하고, 유니코드 문자를 반환한다.
	print('입력문자 = {}, name = {}, lookup = {}' .format(value, name, value2))
```
 #### UTF-8 인코딩과 디코딩
 유니코드를 위한 가변 길이 문자 인코딩 방법
 #### 문자열을 바이트로 **인코딩**
 - 1바이트 : 아스키코드
 - 2바이트 : 대부분의 파생된 라틴어
 - 3바이트 : 기본 다국어 평면의 나머지
 - 4바이트 : 아시아 언어 및 기호를 포함한 나머지

 인코딩 방식
```python
'ascii'              7비트의 아스키코드
'utf-8'              8비트 가변 길이 인코딩 형식, 거의 대부분의 문자 지원
'latin-1'            ISO 8859-1로도 알려짐
'cp-1252'            윈도우 인코딩 형식
'unicode-escape'     파이썬 유니코드 리터럴 형식 (\nxxxx 또는 \Uxxxxxxxx)
```

**encode('[인코딩 이름]')**

**encode('[인코딩 이름]', 'ignore')**           : 알 수 없는 문자를 인코딩 하지 않는다.

**encode('[인코딩 이름]', 'replace')**          : 알 수 없는 문자를 ?로 대체한다

**encode('[인코딩 이름]', 'backslashreplace')** : 알 수 없는 문자를 파이썬의 역 슬래시 이스케이프 시퀀스로 대체한다.

**encode('[인코딩 이름]', 'xmlcharrefreplace')**   : 알 수 없는 문자를 적절한 XML 문자 참조 &#nnn; 로 대체한다.

이외 namereplace, strict, surrogateescape 가 있다.

> <참고> 파이썬 내장함수 : https://docs.python.org/ko/3/library/functions.html

#### 바이트를 문자열로 **디코딩**

인코딩 방식과 다른 방식으로 디코딩하면 예외가 나온다.
 


### 7.1.2 포맷

포맷을 사용하여 데이터값을 문자열에 끼워넣는다.

#### #

변환타입
```python
%s              문자열
%d              10진 정수
%x              16진 정수
%o              8진 정수
%f              10진 부동소수점수
%e              지수로 나타낸 부동소수점수
%g              10진 부동소수점수 혹은 지수로 나타낸 부동소수점수
%%              리터럴 %
```

'%☆d' : 각 변수에 최소 ☆자의 필드를 설정하고, 오른쪽으로 정렬한다. 

'%-☆d' : 각 변수에 최소 ☆자의 필드를 설정하고, 왼쪽으로 정렬한다.

'%☆.★d' : 각 변수에 최소 ☆자의 필드를 설정하고, 최대 문자 길이를 ★로 제한하며, 오른쪽으로 정렬한다.


#### {}와 format

**' {} {} ' .format([변수] ,[변수])**

**' {[순서]} {[순서]} ' .format([변수], [변수])**

**' {[변수 이름]} {[변수 이름]} ' .format([변수 이름]=[변수], [변수 이름]=[변수])**

**' {[순서]:[타입]} {[순서]:[타입]} ' .format([변수], [변수])**

**' {[변수 이름]:[타입]} {[변수 이름]:[타입]} ' .format([변수 이름]=[변수], [변수 이름]=[변수])**

소수점 이후의 정밀 값은 정수에 사용할 수 없다.


### 7.1.3 정규표현식

특정한 규칙을 가진 문자열의 집합을 표현하는데 사용하는 형식 언어

**import re**

- match() : 시작부터 일치하는 패턴 찾기

- search() : 첫 번째 일치하는 패턴 찾기

- findall(.) : 일치하는 모든 패턴 찾기

- split() : 패턴으로 나누기

- sub() : 일치하는 패턴 대체하기


#### 패턴

- 특수문자
```python
\d              숫자
\D              비숫자
\w              알파벳 문자
\W              비알파벳 문자
\s              공백 문자
\S              비공백 문자
\b              단어 경계
\B              비단어 경계
```

- 지정자
```python
abc             리터럴 abc
\D              비숫자
\w              알파벳 문자
\W              비알파벳 문자
\s              공백 문자
\S              비공백 문자333333333333333333333333333333333333333
\b              단어 경계
```
 
- 매칭 결과 지정하기
나는 도대체 이게 뭔지 모르겠습니다.ㅠㅠ 다같이 말해보아요

> <참고> 정규표현식 : http://www.nextree.co.kr/p4327/
> <참고> 정규표현식 기본 문법 정리표 : http://blog.daum.net/creazier/15309380

## 7.2 이진 데이터

### 7.2.1 바이트와 바이트 배열

바이트는 불변한다.

바이트 배열은 변경가능하다.

### 7.2.2 이진 데이터 변환하기 : struct

데이터를 처리하는 모듈

C언어의 구조체와 유사하다.

**import struct**

형식 지정자
```python
x              1 바이트 건너뜀             1
b              부호 있는 바이트             1
B              부호 없는 바이트             1
h              부호 있는 짧은 정수          2
H              부호 없는 짧은 정수          2
i              부호 있는 정수              4
I              부호 없는 정수              4
l              부호 있는 긴 정수            4
L              부호 없는 긴 정수            4
Q              부호 없는 아주 긴 정수        8
f              단정도 부동소수점수           4
d              배정도 부동소수점수           8
p              문자수와 문자               1 + count
s              문자                      count
```

### 7.2.3 기타 이진 데이터 도구

- bitstring : 비트 문자열을 읽고 이진 데이터의 스트림으로 해석한다.
- construct : 구성 요소는 비트 및 바이트 세분성 , 쉬운 디버깅 및 테스트, 확장하기 쉬운 하위 클래스 시스템 및 많은 기본 구성을 제공하여 작업을보다 쉽게한다.
- hachoir : 디렉토리와 파일을 탐색하는 것처럼 모든 이진 스트림을 탐색 할 수 있게 한다.
- binio : 구조화 된 바이너리 파일 (또는 파일과 유사한 객체) 읽기 및 쓰기를 단순화해준다.

> <참고> bitstring : https://pypi.org/project/bitstring/
> <참고> construct : https://pypi.org/project/construct/
> <참고> hachoir : https://pypi.org/project/hachoir/
> <참고> binio : http://spika.net/py/binio/

### 7.2.4 바이트/문자열 변환하기 : binascii()

이진 데이터와 다양한 문자열 표현을 서로 변환할 수 있는 함수를 제공한다.

### 7.2.5 비트 연산자

비트단위 연산자
```python
&              AND
|              OR
^              배타적 OR
~              NOT
<<             비트 왼쪽 이동
>>             비트 오른쪽 이동
```

