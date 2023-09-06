---
title: 파이썬 외부 라이브러리
categories: Python
---
파이썬 외부 라이브러리에 대해 정리합니다.

## 모듈 및 패키지 관리 도구

- pip
    
    파이썬 모듈 및 패키지를 쉽게 설치할 수 있도록 도와주는 도구 ( [https://pypi.org/](https://pypi.org/) )
    
    ```bash
    # pip install
    pip install {package_name}
    
    # pip uninstall
    pip uninstall {package_name}
    
    # 특정 버전으로 설치하기
    pip install {package_name}==1.0.4 # 생략하면 최신 버전 설치
    
    # 최신 버전으로 업그레이드하기
    pip install --upgrade {package_name}
    
    # 설치된 패키지 확인하기
    pip list
    ```
    

## 더미데이터 생성 라이브러리

- Faker
    
    테스트용 더미 데이터를 생성할 때 사용하는 라이브러리
    
    ```python
    ## Faker 설치
    # $ pip install Faker
    
    from faker import Faker
    
    ## current_country : 현재 설정된 나라 반환
    Faker().current_country() # United States, 기본값
    
    ## name : 이름 더미 데이터 반환
    Faker().name() # Mary Flynn, 영어 이름 반환
    Faker("ko-KR").name() # 최지우, 한글 이름 반환
    
    ## address : 주소 더미 데이터 반환
    Faker("ko-KR").address() # 제주특별자치도 음성군 영동대225거리 (윤서이이동)
    
    ## postcode : 우편번호 반환
    ## country : 국가명 반환
    ## company : 회사명 반환
    ## job : 직업명 반환
    ## phone_number : 휴대폰 번호 반환
    ## email : 이메일 주소 반환
    ## user_name : 사용자명 반환
    ## pyint : 임의의 숫자 반환
    ## ipv4_private : IP 주소 반환
    ## text : 임의의 문장 (한글 임의의 문장은 catch_phrase)
    ## color_name : 색상명 반환
    ```
    

## 기호 기반 수학 라이브러리

- sympy
    
    ```python
    ## sympy 설치
    # $ pip install sympy
    
    import sympy
    from fractions import Fraction
    
    ## symbols : 'x'처럼 방정식에 사용하는 미지수를 나타내는 기호를 생성하여 반환
    x = sympy.symbols("x")
    y, z = sympy.symbols("y, z")
    
    ## Eq : a와 b가 같다는 방정식
    f_1 = sympy.Eq(1, 2)
    f_2 = sympy.Eq(x * Fraction(2, 5), 1760)
    
    ## solve : 방정식에서 미지수의 해를 구하여 반환, 방정식의 해는 여러개일 수 있으므로 리스트로 반환
    result_one = sympy.solve(f_2) # [4400]
    result_two = sympy.solve(sympy.Eq(x*x, 4)) # [-2, 2]
    
    ### 미지수가 2개 이상이면 딕셔너리로 반환
    # 연립 방정식 예시 (simultaneous equations)
    _x, _y = sympy.symbols('_x _y')
    se_f1 = sympy.Eq(_x + _y, 4)
    se_f2 = sympy.Eq(_x * _y, 3)
    result = sympy.solve([se_f1, se_f2]) # 연립 방정식의 경우 list 타입으로 전달
    result # [{_x: 1, _y: 3}, {_x: 3, _y: 1}]
    ```