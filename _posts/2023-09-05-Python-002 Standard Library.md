---
title: 파이썬 표준 라이브러리
categories: Python
---
파이썬 표준 라이브러리에 대해 정리합니다.

## File

- shutil
    
    파일을 복사하거나 이동할 때 사용하는 모듈
    
    ```python
    import shutil
    
    ## copy : 파일 복사
    shutil.copy("./file/test1.txt", "./file/test2.txt")
    
    ## move : 이동
    shutil.move("./file/test1.txt", "./file/test3.txt")
    ```
    
- glob
    
    디렉토리에 있는 파일 이름을 모두 조회할 때 사용하는 모듈
    
    ```python
    import glob
    file_path_list: list[str] = glob.glob("./file/*") # ['./file/test2.txt', './file/test3.txt']
    ```
    
- pickle
    
    직렬화
    
    ```python
    import pickle
    
    data = {
        "key": "value"
    }
    
    with open("./file/test1.txt", "wb") as file_pickle:
        pickle.dump(data, file_pickle)
    
    with open("./file/test1.txt", "rb") as file_pickle_read:
        data = pickle.load(file_pickle_read) # {'key': 'value'}
    ```
    
- os
    
    운영체제 시스템 모듈
    
    ```python
    import os
    
    ## environ : 시스템 환경 변수 반환
    os.environ # dictionary
    os.environ["PATH"]
    
    ## path.expanduser('~) 홈디렉토리
    home_path = os.path.expanduser('~')
    
    ## chdir : 디렉토리 위치 변경하기
    os.chdir(f"{home_path}/Private/dev/learning/python/")
    
    ## getcwd : 현재 디렉토리 위치 반환
    print(os.getcwd())
    
    ## system : 시스템 명령어 호출하기
    ## 시스템 자체의 프로그램이나 기타 명령어를 파이썬에서 호출할 수 있다.
    ## `os.system("명령어")`
    os.system("ls")
    os.system("ls -al")
    
    ## popen : 시스템 명령어를 실행한 결과값을 읽기 모드 형태의 파일 객체로 반환
    file_ls = os.popen("ls")
    
    ## mkdir : 디렉토리 생성
    os.mkdir("디렉토리경로")
    
    ## rmdir : 디렉토리 삭제
    os.rmdir("디렉토리경로")
    
    ## remove : 파일 삭제
    os.remove("파일경로")
    
    ## rename : 파일명 변경
    os.rename("소스 파일", "타겟 파일")
    ```
    
- zipfile
    
    여러개의 파일을 zip 형식으로 합치거나 해제할 때 사용하는 모듈
    
    ```python
    import zipfile
    
    ## 묶기
    with zipfile.ZipFile("./file/filename.zip", 'w') as zip:
        zip.write('./file/test1.txt')
        zip.write('./file/test2.txt')
        zip.write('./file/test3.txt')
    
    ## 해제
    with zipfile.ZipFile("./file/filename.zip") as zip:
        zip.extractall("./file/compact/")
    
    ## 특정 파일만 해제
    # with zipfile.ZipFile("./file/filename.zip") as zip:
    #     zip.extract("test1.txt")
    
    ## 압축 묶기
    with zipfile.ZipFile("./file/filename.zip", 'w', compression=zipfile.ZIP_LZMA, compresslevel=9) as zip:
        pass
    ### ZIP_STORED : 압축하지 않고 파일을 zip으로만 묶는다. 속도가 빠르다.
    ### ZIP_DEFLATED : 일반적인 zip 압축ㅇ로 속도가 빠르고 압축률은 낮다(호환성이 좋음).
    ### ZIP_BZIP2 : bzip2 압축으로 압축률이 높고 속도가 느리다.
    ### ZIP_LZMA : lzma 압축으로 압축률이 높고 속도가 느리다(7zip과 동일한 알고리즘으로 알려져있다).
    
    ### compressionlevel 은 압축 수준을 의미하는 숫자값으로, 1~9를 사용한다. 1은 속도가 가장 빠르지만 압축률이 낮고, 9는 속도가 가장 느리지만 압축률이 높다.
    ```
    
- tempfile
    
    파일을 임시로 만들어서 사용할 수 있는 모듈
    
    ```python
    import tempfile
    
    ## mkstemp : 중복되지 않는 임시 파일의 이름을 무작위로 만들어서 반환
    filename = tempfile.mkstemp()
    
    # TemporaryFile : 임시 저장 공간으로 사용할 파일 객체를 반환
    ## 이 파일은 기본적으로 바이너리 쓰기 모드를 갖는다.
    ## close 가 호출되면 이 파일은 자동으로 삭제된다.
    with tempfile.TemporaryFile('r+b') as file_temp:
        pickle.dump({"a": 1}, file_temp) # 바이너리를 저장하면서 커서가 파일의 맨 뒤로 이동
        file_temp.seek(0) # EOFError: Ran out of input, 끝에 있기 때문에 커서를 파일의 맨 앞으로 이동
        pickle.load(file_temp)
    ```
    

---

## Iterable

- itertools
    
    반복 가능한 데이터 함수 모듈
    
    ```python
    import itertools
    
    ## zip_longest : 같은 갯수의 자료형을 묶는 파이썬 내장 함수인 zip 함수와 동일하게 동작한다.
    ## 하지만 반복 가능한 객체의 길이가 다를 경우 긴 객체의 길이에 맞춰 fillvalue에 설정한 값을 짧은 객체에 채울 수 있다.
    students = ['권영찬', '이진혁', '박찬혁', '한예진']
    drink = ['사이다', '콜라']
    zip_result = zip(students, drink) # [ ('권영찬', '사이다'), ('이진혁', '콜라') ]
    zip_longest_result = itertools.zip_longest(students, drink, fillvalue='fill') # [ ('권영찬', '사이다'), ('이진혁', '콜라'), ('박찬혁', 'fill'), ('한예진', 'fill') ]
    
    ## permutation : 반복 가능한 객체 중에서 r개를 선택한 순열을 iterator로 반환하는 함수
    permutation = itertools.permutations([1, 2, 3], 2) # [ (1, 2), (1, 3), (2, 1), (2, 3), (3, 1), (3, 2) ]
    
    ## combinations : 반복 가능한 객체 중에서 순서에 상관없이 r개의 조합을 반환하는 함수
    combination = itertools.combinations([1, 2, 3], 2) # [ (1, 2), (1, 3), (2, 3) ]
    
    ## combinations_with_replacement : combinations에서 데이터의 중복을 허용하는 조합을 반환하는 함수
    combinations_with_replacement = itertools.combinations_with_replacement([1, 2, 3], 2) # [ (1, 1), (1, 2), (1, 3), (2, 2), (2, 3), (3, 3) ]
    ```
    
- functools
    
    고차 함수를 위한 모듈
    
    ```python
    import functools
    
    ## reduce : iterable 요소 값들을 누적 계산하여 최종 계산된 1개의 값을 반환
    reduce = functools.reduce(lambda a, b: a + b, [1, 2, 3]) # 6
    ```
    
- operator
    
    수행 가능한 연산을 효율적으로 처리할 수 있는 함수 모듈
    
    ```python
    from operator import itemgetter, attrgetter
    
    ## itemgetter : 정렬 함수 key 매개변수에 적용하여 정렬할 수 있도록 도와주는 모듈(클래스)
    students_tuple = [
        ("a", 1), ("b", 3), ("c", 2),
    ]
    sorted_student_tuple = sorted(students_tuple, key=itemgetter(1)) # [('a', 1), ('c', 2), ('b', 3)]
    
    students_dic = [
        { "name": "a", "age": 1 },
        { "name": "b", "age": 3 },
        { "name": "c", "age": 2 }
    ]
    
    sorted_students_dic = sorted(students_dic, key=itemgetter("age")) # [{'name': 'a', 'age': 1}, {'name': 'c', 'age': 2}, {'name': 'b', 'age': 3}]
    
    ## attrgetter : 정렬 함수 key 매개변수에 적용하여 정렬할 수 있도록 도와주는 모듈(클래스)
    class Student:
        def __init__(self, name, age) -> None:
            self.name = name
            self.age = age
    students_class = [
        Student('a', 1),
        Student('b', 3),
        Student('c', 2)
    ]
    sorted_students_class = sorted(students_class, key=attrgetter('age')) # a, b, c 순 정렬
    ```
    

---

## Time

- time
    
    시간과 지역화를 다루기 위한 모듈
    
    ```python
    import time
    
    ## time : UTC를 사용하여 현재 시간을 실수 형태로 반환
    print(time.time()) # 1693876905.844053
    
    ## localtime : time이 반환한 실수값을 사용해서 연,월,일,시,분,초의 형태로 변환
    ## 인수 없이 호출 시 현재 시각을 기준으로 반환
    struct_time = time.localtime(time.time()) # struct_time
    # (tm_year=2023, tm_mon=9, tm_mday=5, tm_hour=10, tm_min=30, tm_sec=51, tm_wday=1, tm_yday=248, tm_isdst=0)
    
    ## asctime : localtime가 반환된 튜플 형태의 값을 인수로 받아서 날짜와 시간을 알아보기 쉬운 형태로 반환
    ## 인수 없이 호출 시 현재 시각을 기준으로 반환
    asc_time: str = time.asctime(struct_time) # Tue Sep  5 10:34:08 2023
    
    ## ctime : time.asctime(time.localtime(time.time())) 을 간단하게 현재시간만을 반환
    ctime: str = time.ctime() # Tue Sep  5 10:35:58 2023
    
    ## strftime : 시간게 관계된 것을 세밀하게 표현하는 여러 가지 포맷 코드를 제공하는 함수
    ## 인수 없이 호출 시 현재 시각을 기준으로 반환
    ## format code : https://wikidocs.net/33#timestrftime
    strf_day: str = time.strftime('%d', time.localtime(time.time()))
    
    ## sleep : 일정한 시간 간격을 지연시키는 함수
    ## 초단위로 실수 형태로 입력값을 받는다
    for i in range(10):
        print(i)
        time.sleep(1)
    ```
    

---

## Date

- datetime
    
    날짜와 시간을 다루기 위한 모듈
    
    ```python
    import datetime
    
    ## date : 연, 월, 일로 날짜를 표현할 때 사용하는 함수
    
    day1 = datetime.date(2023, 3, 3) # date 타입
    day2 = datetime.date(2023, 3, 4)
    
    ## timedelta
    diff = day2 - day1 # timedelta 객체가 반환
    diff.days # 1
    
    ## weekday : 0-월요일 ~ 6-일요일
    week_day = datetime.date(2023, 9, 5).weekday() # 화요일 1
    
    ## isweekday : 1-월요일 ~ 7-일요일
    iso_week_day = datetime.date(2023, 9, 5).isoweekday() # 화요일 2
    ```
    

---

## Math

- math
    
    C 표준에서 정의된 수학 함수에 대한 액세스를 제공하는 모듈
    
    ```python
    import math
    
    ## gcd : 최대공약수를 구하는 함수 (python 3.5 버전부터 존재)
    gcd_val = math.gcd(77, 99, 11) # 11
    
    ## lcm : 최소 공배수를 구하는 함수 (python 3.9 버전부터 존재)
    lcm_val = math.lcm(3, 9, 18) # 18
    ```

- fractions

    유리수를 표현할 때 사용하는 표준 라이브러리
    ```python
    from fractions import Fraction

    ## Fraction
    Fraction(1, 5) # 5분의 1
    Fraction('1/3') # 3분의 1
    ```
    

---

## Random

- random
    
    난수를 발생시키는 모듈
    
    ```python
    import random
    
    ## random
    random_val_1 = random.random() # 0.0 ~ 1.0 사이의 실수 중 난수 값을 반환, 0.023461997948057034
    rand_int = random.randint(1, 2) # a 이상 b 이하 값 중 난수 값을 반환
    choice = random.choice((1,2,3)) # iterable 타입 값을 입력받아 그 값들 중 임의의 값을 반환
    sample = random.sample([1,2,3,4,5], 3) # iterable 타입 값과 길이 값을 입력받아 섞어서 길이에 맞춰 반환
    ```
    

---

## Thread

- threading
    
    스레드를 다루는 모듈
    
    ```python
    import threading
    import time
    
    def long_task(): 
        for i in range(5):
            print(f"working {i}")
            time.sleep(1)
    
    print("Start")
    
    threads = []
    for i in range(5): 
        thread = threading.Thread(target=long_task)
        threads.append(thread)
    
    for t in threads:
        t.start()
    
    for t in threads:
        t.join()
    
    print("End")
    ```

---

## Data

- json

    json 데이터 처리 모듈
    ```python
    import json

    ## load : json 파일을 읽고 dictionary 로 변환하여 반환
    import tempfile

    with tempfile.TemporaryFile("r+") as file_json:
        file_json.write('{ "test": 1 }')
        file_json.seek(0)
        json_data = json.load(file_json)
        type(json_data) # <class 'dict'>

    ## dumps : dictionary 자료형을 json 문자열로 변환
    dict = { "a": 1 }
    json_str = json.dumps(dict)
    print(json_str)

    ## dump : dictionary 자료형을 json 파일로 생성
    with tempfile.TemporaryFile("r+") as file_json:
        dict = { "한글": "ㄱㄴㄷㄹ" }
        json.dump(dict, file_json) # 유니코드로 변환
        file_json.seek(0)
        file_json.read() # {"\ud55c\uae00": "\u3131\u3134\u3137\u3139"}
        
        file_json.truncate(0) # 파일 크기를 0byte로 조정, 파일 크기를 지정하지 않으면 현재 위치의 크기로 지정된다.
        json.dump(dict, file_json, ensure_ascii=False) # 유니코드(아스키) 변환 X
        file_json.seek(0)
        file_json.read() # {"한글": "ㄱㄴㄷㄹ"}

    list_json = json.dumps([1, 2, 3]) # '[1, 2, 3]'
    tuple_json = json.dumps((1, 2, 3)) # '[1, 2, 3]'
    ```

---

## Exception

- traceback

    프로그램 실행 중 발생한 오류 추적 모듈
    ```python
    import traceback

    def a():
        a = 1 / 0
    def b():
        a()
    def c():
        b()

    try:
        c()
    except:
        print(traceback.format_exc())

    # Traceback (most recent call last):
    #   File "/Users/zave/Private/dev/learning/python/standard_library/exception.py", line 12, in <module>
    #     c()
    #   File "/Users/zave/Private/dev/learning/python/standard_library/exception.py", line 9, in c
    #     b()
    #   File "/Users/zave/Private/dev/learning/python/standard_library/exception.py", line 7, in b
    #     a()
    #   File "/Users/zave/Private/dev/learning/python/standard_library/exception.py", line 5, in a
    #     a = 1 / 0
    #         ~~^~~
    # ZeroDivisionError: division by zero
    ```

---

## Web

- urllib

    URL을 가져오기 위한 파이썬 모듈
    ```python
    import urllib.request

    ## request.urlopen : http 요청
    resource = "https://wikidocs.net/33"
    with urllib.request.urlopen(resource) as html:
        with open("wikidocs_33.html", "wb") as file:
            file.write(html.read())
    ```

- webbrowser

    시스템 브라우져를 호출할 때 사용하는 모듈
    ```python
    import webbrowser

    ## open_new : 시스템 브라우져 새 창으로 열기
    webbrowser.open_new('https://www.naver.com')
    ```