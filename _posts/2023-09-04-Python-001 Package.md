---
title: 파이썬 Package
categories: Python
---
파이썬 패키지에 대해 학습한 내용을 간략히 정리합니다. `(위키독스 점프 투 파이썬 참조)`

### 패키지 생성

파이썬에서 패키지란 관련 있는 모듈의 집합을 말한다.

패키지는 파이썬 모듈을 계층적으로 관리할 수 있게 해준다. `(파이썬에서 모듈은 하나의 .py 파일)`

- 가상의 game 패키지 예
    
    ```
    game/
    	__init__.py
    	sound/
    		__init__.py
    		echo.py
    	graphic/
    		__init__.py
    		render.py
    ```
    
    game, sound, graphic은 디렉토리, 확장자가 .py 인 파일은 파이썬 모듈이다.
    game 디렉토리가 이 패키지의 루트 디렉토리, sound, graphic은 서브 디렉토리이다.
    

### 패키지 안의 함수 실행

- echo 모듈을 import 하여 실행
    
    ```python
    import game.sound.echo
    game.sound.echo.echo_test()
    # >>> 'echo'
    ```
    
- echo 모듈이 있는 디렉토리까지 import
    
    ```python
    import game.sound import echo
    echo.echo_test()
    # >>> 'echo'
    ```
    
- echo_test 함수를 직접 import
    
    ```python
    from game.sound.echo import echo_test
    echo_test()
    # >>> 'echo'
    ```
    

### __init__.py

__init__.py 파일은 해당 디렉토리가 패키지의 일부임을 알려주는 역할을 한다. `python 3.3 버전부터는 __init__.py 파일이 없어도 패키지로 인식한다. ([PEP 420](https://peps.python.org/pep-0420/))`

또한 처음 불러올 때 실행되어야할 초기화 코드를 작성할 수 있다.

다만, 하위 버전 호환을 위해 __init__.py 파일을 생성하는 것이 안전한 방법이다.

- game/__init__.py
    
    ```python
    # game/__init__.py
    VERSION = 1.0.0
    print(f"Game Version {VERSION}")
    ```
    
- terminal
    
    ```python
    >>> import game
    >>> print(game.VERSION)
    # >>> '1.0.0'
    ```
    

### Relative 패키지

모듈 import 를 상대경로로 지정할 수 있다.

- game/graphic/render.py
    
    ```python
    # game/graphic/render.py
    from game.sound.echo import echo_test
    def render_test():
        print("render")
        echo_test()
    ```
    
- terminal
    
    ```python
    >>> from game.graphic.render import render_test
    >>> render_test()
    # >>> 'render'
    # >>> 'echo'
    ```
    
- render.py 상대경로 수정
    
    ```python
    from ..sound.echo import echo_test
    def render_test():
        print("render")
        echo_test()
    ```
    
- render.py 파일을 메인으로 terminal에서 실행 시 다음과 같이 실패한다
    
    ```python
    >>> from ..sound.echo import echo_test
    # ImportError: attempted relative import with no known parent package
    ```
    
- 메인 실행 파일에는 상대 경로로 import 할 수 없기 때문이다.
    - 파이썬의 모듈은 메인으로 실행될 경우 `__name__` 변수에 `__main__` 값이 할당된다.
    - `__main__` 모듈의 경우 패키지의 구조가 실제 파일 시스템에 있는 위치에 관계없이 최상위 모듈인 것 처럼 된다.
    - 따라서 상대경로 import 는 할 수 없고 절대경로로 지정해줘야한다.
        - 참조 : 
        [https://velog.io/@anjaekk/python절대경로상대경로-상대경로-import-에러이유와-해결](https://velog.io/@anjaekk/python%EC%A0%88%EB%8C%80%EA%B2%BD%EB%A1%9C%EC%83%81%EB%8C%80%EA%B2%BD%EB%A1%9C-%EC%83%81%EB%8C%80%EA%B2%BD%EB%A1%9C-import-%EC%97%90%EB%9F%AC%EC%9D%B4%EC%9C%A0%EC%99%80-%ED%95%B4%EA%B2%B0)
        [https://docs.python.org/3/tutorial/modules.html#intra-package-references](https://docs.python.org/3/tutorial/modules.html#intra-package-references)
        [https://peps.python.org/pep-0328/](https://peps.python.org/pep-0328/)