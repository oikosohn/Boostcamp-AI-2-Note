코드 발췌 : 프리코스 강의

# Function and Console I/O
```python3
# PEP 함수 사이 2줄씩 비운다.
def addition(x, y):
  return x+y


def multiplication(x, y):
  return x*y


def divided_by_2(x):
  return x/2


# __name__ 코드 부분은 python Shell에서 호출 할 경우 실행되지 않음
if __name__ == '__main__':
  print(addition(10,5))
  print(multiplication(10,5))
  print(divided_by_2(50))
```

# String and advanced function concept
```python3
a = 'Team x boost'
print(a.capitalize())
print(a.title())
print(a.count(a))
print(a.find('a')) # 앞에서부터 탐색
print(a.rfind('a')) # 뒤에서부터 탐색
print(a.startswith('T'))
print(a.endswith('t'))
print(a.isdigit())
print('123456'.isdigit())
print("  Hello   ".strip())
```

- raw string
```python3
raw_string = r'이제 파이썬 공부 \n 레알'
print(raw_string)
```

- File IO

```python3
!wget https://raw.githubusercontent.com/TeamLab/introduction_to_python_TEAMLAB_MOOC/master/code/6/yesterday.txt

f = open("yesterday.txt",'r') 
yesterday_lyric = ""

while True:
  line = f.readline() # 라인 한 줄 씩 읽어오기
  if not line:
    break
  yesterday_lyric = yesterday_lyric + line.strip() + "\n"
f.close() # with open을 사용하지 않으면 필수
n_of_yesterday = yesterday_lyric.upper().count("YESTERDAY")
print(n_of_yesterday)
```

- 함수 호출 방식 
1. call by value : 값만 넘김
2. call by reference : 메모리 주소 넘김
3. call by object reference : 파이썬은 객체의 주소가 함수로 전달

```python3
def spam(eggs):
  eggs.append(1) # 기존 객체의 주소값에 1 추가
  eggs = [2,3] # 새로운 객체 생성

ham = [0]
spam(ham)
print(ham)
```

- function type hints
```python3
# (변수명: 변수형) -> 반환형
def type_hint_example(name: str) -> str:
  return f"Hello, {name}"
```

# Python Data Structure

namedtuple
- Tuple 형태로 Data 구조체를 저장하는 방법
- 저장되는 data의 variable을 사전에 지정해서 저장함


# Pythonic code

iterable objects
- 내부적 구현으로 __iter__ 와 __next__ 가 사용됨
- iter() 와 next() 함수로 iterable 객체를 iterator object로 사용

generator
- iterable object를 특수한 형태로 사용해주는 함수
- element가 사용되는 시점에 값을 메모리에 반환
  - yield를 사용해 한번에 하나의 element만 반환함
  
generator comprehension
- list comprehension과 유사한 형태로 generator형태의 list 생성
- generator expression 이라는 이름으로도 부름
- `[ ]` 대신 `( )` 를 사용하여 표현

가변인자 (variable-length)
- 개수가 정해지지 않은 변수를 함수의 parameter로 사용하는 법
- Keyword arguments와 함께, argument 추가가 가능
- Asterisk(*) 기호를 사용하여 함수의 parameter를 표시함
- 입력된 값은 tuple type으로 사용할 수 있음
- 가변인자는 오직 한 개만 맨 마지막 parameter 위치에 사용가능
- 가변인자는 일반적으로 *args를 변수명으로 사용
- 기존 parameter 이후에 나오는 값을 tuple로 저장함

키워드 가변인자 (Keyword variable-length )

- Parameter 이름을 따로 지정하지 않고 입력하는 방법
- asterisk(*) 두개를 사용하여 함수의 parameter를 표시함
- 입력된 값은 dict type으로 사용할 수 있음
- 가변인자는 오직 한 개만 기존 가변인자 다음에 사용


# Python Object Oriented Programming

  - class 예약어 class 이름(상속받는 개체명)
  - self는 생성된 인스턴스
  - 상속 : object 생략 가능
  - 다형성 : 이름은 같지만 내부 구현은 다르다.
  - 가시성(정보 은닉, 캡슐화) : Private 변수로 선언되면 타 객체가 접근하지 못한다.
  - decorate
  ``` python3
  class Student:
  def __init__(self, name, marks):
    self.name = name
    self.marks = marks
    # self.gotmarks = self.name + ' obtained ' + self.marks + ' marks'

  @property # property decorator : 숨겨진 변수를 반환하게 해줌
  def gotmarks(self):
    return self.name + ' obtained ' + self.marks + ' marks'
  ```
  - 일급 함수
    - 일등함수 또는 일급 객체
    - 변수나 데이터 구조에 할당이 가능한 객체
    - 파라메터로 전달이 가능 + 리턴 값으로 사용
    - 파이썬의 함수는 일급함수
    ```python3
    def square(x):
      return x * x

    f = square # square 함수를 변수로 사용
    f(5)

    def square(x):
      return x * x

    def cube(x):
      return x*x*x

    # 함수를 파라메터로 사용
    def formula(method, argument_list):
      return [method(value) for value in argument_list]    
    ```

  - 내부 함수 : 함수 내에 또 다른 함수가 존재
  ```python3
  def print_msg(msg):
    def printer():
      print(msg)
    printer()

  print_msg("Hello, Python")
  ```
  
   - closures : inner function을 return값으로 반환
  ```python3
  def print_msg(msg):
    def printer():
      print(msg)
    return printer

  another = print_msg("Hello, Python")
  another()    
  ```
    
   - decorator function : 복잡한 클로져 함수를 간단하게 만들어준다.


# Module and Project

모듈 : Built-in Module인 Random을 사용, 난수를 쉽게 생성할 수 있음

패키지 : 모듈을 모아놓은 단위, 하나의 프로그램

- 네임스페이스 예제

  1. Alias 설정하기 – 모듈명을 별칭으로 써서
  ```python3
  import fah_converter as fah # fah_converter를 fah라는 이름으로
  print(fah.covert_c_to_f(41.6)) # 그 안에 covert_c_to_f 함수를 쓴다
  ```

  2. 모듈에서 특정 함수 또는 클래스만 호출하기
  ```python3
  from fah_converter import covert_c_to_f
  print(covert_c_to_f(41.6)) # covert_c_to_f 함수만 호출함
  ```

  3. 모듈에서 모든 함수 또는 클래스를 호출하기
  ```python3
  from fah_converter import *
  print(covert_c_to_f(41.6)) # 전체 호출
  ```

- 패키지
  - 하나의대형프로젝트를만드는코드의묶음
  - 다양한모듈들의합, 폴더로연결됨
  - \_\_init\_\_ , \_\_main\_\_ 등키워드파일명이사용됨
  - 다양한오픈소스들이모두패키지로관리됨

- tqdm : 실행 진행도를 보여주는 패키지
  ```python3
  from tqdm import tqdm
  import time
  for i in tqdm(range(1000)):
    if i % 1000 == 0:
      time.sleep(1)
  ```

# File / Exception / Log Handling

## Exception
1. 예상 가능한 예외
- 발생 여부를 사전에 인지할 수 있는 예외
- 사용자의 잘못된 입력, 파일 호출 시 파일 없음
- 개발자가 반드시 명시적으로 정의 해야함

2. 예상이 불가능한 예외
- 인터프리터 과정에서 발생하는 예외, 개발자 실수
- 리스트의 범위를 넘어가는 값 호출, 정수 0으로 나눔
- 수행 불가시 인터프리터가 자동 호출

예외 처리 (Exception Handling)
- 예외가 발생할 경우 후속조치 등 대처 필요
1. 없는 파일 호출→ 파일없음을 알림
2. 게임 이상 종료→ 게임 정보 저장
- 프로그램 = 제품, 모든 잘못된상황에 대처가 필요

Built-in Exception : 이름 내용
- IndexError : List의 Index 범위를 넘어갈 때
- NameError : 존재하지 않은 변수를 호출 할 때
- ZeroDivisionError : 0으로 숫자를 나눌 때
- ValueError : 변환할 수 없는 문자/숫자를 변환할 때
- FileNotFoundError : 존재하지 않는 파일을 호출할 때

raise 구문
- 필요에 따라 강제로 Exception을 발생
```python3
raise \<Exception Type>(예외정보)
```
assert 구문
- 특정 조건에 만족하지 않을 경우 예외 발생

## File handling

Binary 파일 
- 컴퓨터만 이해할 수 있는 형태인
이진(법)형식으로 저장된 파일
- 일반적으로 메모장으로 열면
내용이 깨져 보임 (메모장 해설 불가)
- 엑셀파일, 워드 파일 등등

Text 파일
- 인간도 이해할 수 있는 형태인
문자열 형식으로 저장된 파일
- 메모장으로 열면 내용 확인 가능
- 메모장에 저장된 파일, HTML 파일,
파이썬 코드 파일 등

파일열기모드 설명
- r 읽기모드 : 파일을 읽기만 할 때 사용
- w 쓰기모드 : 파일에 내용을 쓸 때 사용
- a 추가모드 : 파일의 마지막에 새로운 내용을 추가 시킬 때 사용

Pickle
- 파이썬의 객체를 영속화(persistence)하는 built-in 객체
- 데이터, object 등 실행중 정보를 저장 -> 불러와서 사용
- 저장해야하는 정보, 계산 결과(모델) 등 활용이 많음


## Log handling
로그 남기기 - Logging

- 프로그램이 실행되는 동안 일어나는 정보를 기록을 남기기
- 유저의 접근, 프로그램의 Exception, 특정 함수의 사용
- Console 화면에 출력, 파일에 남기기, DB에 남기기 등등
- 기록된 로그를 분석하여 의미있는 결과를 도출 할 수 있음
- 실행시점에서 남겨야 하는 기록, 개발시점에서 남겨야하는 기록

print vs logging
- 기록을 print로 남기는 것도 가능함
- 그러나 Console 창에만 남기는 기록은 분석시 사용불가
- 때로는 레벨별(개발, 운영)로 기록을 남길 필요도 있음
- 모듈별로 별도의 logging을 남길필요도 있음
- 이러한 기능을 체계적으로 지원하는 모듈이 필요함

logging level
- 프로그램 진행 상황에 따라 다른 Level의 Log를 출력함
- 개발 시점, 운영 시점 마다 다른 Log가 남을 수 있도록 지원함
- DEBUG > INFO > WARNING > ERROR > Critical == 개발  > 운영 > 운영 > 사용자 > 사용자
- Log 관리시 가장 기본이 되는 설정 정보
- 파이썬 기본 logging level : warning

configparser
- 프로그램의 실행 설정을 file에 저장함
- Section, Key, Value 값의 형태로 설정된 설정 파일을 사용
- 설정파일을 Dict Type으로 호출후 사용

argparser
- Console 창에서 프로그램 실행시 Setting 정보를 저장함
- 거의 모든 Console 기반 Python 프로그램 기본으로 제공
- 특수 모듈도 많이 존재하지만(TF), 일반적으로 argparse를 사용
- Command-Line Option 이라고 부름

Logging formmater
- Log의 결과값의 format을 지정해줄 수 있음


# Python data handling
Comma Separate Value
- CSV, 필드를 쉼표(,)로 구분한 텍스트 파일
- 엑셀 양식의 데이터를 프로그램에 상관없이 쓰기 위한
데이터 형식이라고 생각하면 쉬움
- 탭(TSV), 빈칸(SSV) 등으로 구분해서 만들기도 함
- 통칭하여 character-separated values (CSV) 부름
- 엑셀에서는 “다름 이름 저장” 기능으로 사용 가능

정규식 (regular expression)
- 관련자료: http://www.nextree.co.kr/p4327/

XML이란

- 데이터의 구조와 의미를 설명하는
TAG(MarkUp)를 사용하여 표시하는 언어
- TAG와 TAG사이에 값이 표시되고, 
구조적인 정보를 표현할 수 있음
- HTML과 문법이 비슷, 대표적인 데이터 저장 방식
- 정보의 구조에 대한 정보인 스키마와 DTD 등으로
정보에 대한 정보(메타정보)가 표현되며, 용도에 따라
다양한 형태로 변경가능
- XML은 컴퓨터(예: PC ↔ 스마트폰)간에 정보를
주고받기 매우 유용한 저장 방식으로 쓰이고 있음


XML 예제
```
<?xml version="1.0"?>
<고양이>
 <이름>나비</이름>
 <품종>샴</품종>
 <나이>6</나이>
 <중성화>예</중성화>
 <발톱 제거>아니요</발톱 제거>
 <등록 번호>Izz138bod</등록 번호>
 <소유자>이강주</소유자>
</고양이>
```

XML Parsing in Python

- XML도 HTML과 같이 구조적 markup 언어
- 정규표현식으로 Parsing이 가능함
- 그러나 좀 더 손쉬운 도구들이 개발되어 있음
- 가장 많이 쓰이는 parser인 beautifulsoup으로 파싱
- HTML, XML등 Markup 언어 Scraping을 위한 대표적인 도구
- https://www.crummy.com/software/BeautifulSoup/
- lxml 과 html5lib 과 같은 Parser를 사용함
- 속도는 상대적으로 느리나 간편히 사용할 수 있음

JSON Overview

- JavaScript Object Notation
- 원래 웹 언어인 Java Script의 데이터 객체 표현 방식
- 간결성으로 기계/인간이 모두 이해하기 편함
- 데이터 용량이 적고, Code로의 전환이 쉬움
- 이로 인해 XML의 대체제로 많이 활용되고 있음

JSON in Python

- json 모듈을 사용하여 손 쉽게 파싱 및 저장 가능
- 데이터 저장 및 읽기는 dict type과 상호 호환 가능
- 웹에서 제공하는 API는 대부분 정보 교환 시 JSON 활용
- 페이스북, 트위터, Github 등 거의 모든 사이트
- 각 사이트 마다 Developer API의 활용법을 찾아 사용

JSON Read
- JSON 파일의 구조를 확인 -> 읽어온 후 -> Dict Type처럼 처리
