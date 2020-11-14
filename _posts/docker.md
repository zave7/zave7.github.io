1. AWS EC2 인스턴스 생성 ( ubuntu )
  1) 접속 : https://ap-northeast-2.console.aws.amazon.com/console/home?nc2=h_ct&region=ap-northeast-2&src=header-signin
  2) EC2 검색
  3) 인스턴스 시작 클릭
  4) 운영체제 선택 > 검토 및 시작 > 시작하기
  5) 키페어 생성
    ※ 서버 접속을 위한 보안용 키
      - 유츌 되지 않도록 중요하게 관리
    (1) 새 키페어 생성 선택 > 키 페어 이름 작성 후 키페어 다운로드 > 인스턴스 시작
    (2) 키 보안설정(권한) - 일반 유저는 사용할 수 없도록
      - 리눅스 : chmod 400 권한 설정
      - 윈도우 : 속성에서 관리자 권한만 설정
  6) 인스턴스 보기
  7) cmd에서 ssh로 접속해보기
    (1) 관리자 권한으로 cmd 실행
    (2) 인스턴스 연결 버튼 누른 후 ssh 명령 복사
    (3) cmd에서 명령 실행
    (4) aws 인스턴스 접속 성공
2. GUI 환경 구축 ( jupiter notebook )
  1) apt-get 명령어로 주피터 노트북 설치
    - sudo apt-get update
    ※ 우분투 18.04 버전에는 기본적으로 파이썬3가 설치되어있음
  2) 파이썬 관련 패키지를 설치할 수 있도록 도와주는 pip 파이프 설치
    - sudo apt-get install python3-pip
  3) 주피터 노트북 설치
    - sudo pip3 install notebook
    ※ 이제 서버 외부에서 웹브라우져를 통해 접속 가능
  4) 주피터 노트북 암호 설정
    - 기본적으로 주피터 노트북은 sha-1 해시 패스워드 관리
    (1) 파이썬으로 패스워드 설정
      - from notebook.auth import passwd
      - passwd()
      - 비밀번호 해시 값 저장
      - exit() 로 나가기
  5) 외부에서 접속 했을때 패스워드 입력 후 접속가능하게 하기위해 주피터 노트북 환경 설정
    (1) 환경 설정 파일 생성
      $ jupyter notebook --generate-config 
      $ sudo vi /home/ubuntu/.jupyter/jupyter_notebook_config.py
      - 최하단 이동
      $ c = get_config()
      $ c.NotebookApp.password = u'argon2:$argon2id$v=19$m=10240,t=10,p=8$c0UEVzkUKxl6s3l0Eaa6Uw$bWeeL1TDa/Nul0pp+AVuow'
      $ c.NotebookApp.ip = '172.31.38.47' # 서버 내부 아이피 설정
      $ c.NotebookApp.notebook_dir = '/'
      $ wq!
    (2) 주피터 노트북 실행
      - sudo jupyter-notebook --allow-root
      ※ 기본적으로 8888 포트로 열림
      - EC2 인스턴스에서 보안 > 보안그룹 > 인바운드 규칙 편집 0.0.0.0/0 으로 설정
    (3) 인스턴스 ip로 8888 포트 접속
      - 주피터 노트북 접속
    (4) 주피터 노트북 항상 실행 설정
      $ ctrl + z 로 주피터 노트북 종료
      $ bg # 백그라운드 상태에서 돌아가도록 실행
      $ disown -h # 주피터 노트북에대한 소유권 포기
      - 항상 실행중인 상태
      - 현재 주피터 노트북은 ssl이 적용되어있지 않아 보안 위협에 노출
      - 실행중인 포트로 찾아 주피터노트북 종료
      $ sudo netstat -nap | grep 8888
      $ sudo kill -9 [pid]
    (5) SSL 적용
      $ cd /home/ubuntu
      $ mkdir ssl
      $ cd ssl
      $ sudo openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout "cert.key" -out "cert.pem" -batch
      # 공개키 기반 구조의 기반에 입각함
      # keyout 은 개인키, out은 공개키
      # 주피터 노트북 설정파일에 ssl 설정 추가
      $ sudo vi /home/ubuntu/.jupyter/jupyter_notebook_config.py
      c.NotebookApp.certfile = u'/home/ubuntu/ssl/cert.pem'
      c.NotebookApp.keyfile = u'/home/ubuntu/ssl/cert.key'
      $ sudo jupyter-notebook --allow-root # 다시실행하면 https 로 적용되어 실행되는것을 확인할 수 있다.
      # 사설 인증서이기 때문에 웹브라우져에서 신뢰하지 못하기 때문에 경고 표시를 함
    (6) 주피터 노트북을 시스템 서비스에 등록
      $ ctrl + c 주피터 노트북 종료
      $ which jupyter-notebook 실행 파일 경로 찾기
      $ sudo vi /etc/systemd/system/jupyter.service 파일 작성
      [Unit]
      Description=Jupyter Notebook Server
      
      [Service]
      Type=simple
      User=ubuntu # ssh명령을 이용해서 접속할 때는 기본적으로 ubuntu 계정으로 접속함
      ExecStart=/usr/bin/sudo /usr/local/bin/jupyter-notebook --allow-root --config=/home/ubuntu/.jupyter/jupyter_notebook_config.py
      
      [Install]
      WantedBy=multi-user.target
      $ sudo systemctl daemon-reload
      $ sudo systemctl enable jupyter
      $ sudo systemctl start jupyter
      $ sudo systemctl status jupyter
      ※ 재부팅 후 한 30초 정도면 올라옴
      
      
      
      
      
      
      
      
