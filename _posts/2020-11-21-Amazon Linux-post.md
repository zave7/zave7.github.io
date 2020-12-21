1. 시간대 수정
  1) 인스턴스에서 사용할 표준 시간대를 식별
    $ ls /usr/share/zoneinfo
    - 해당 위치의 디렉토리 구조를 탐색하여 원하는 표준 시간대의 파일을 찾아야함
    - 일부 항목은 디렉토리이며 이러한 디렉토리에는 도시별 표준 시간대 파일이 들어있음
  2) /etc/sysconfig/clock 파일을 새 표준 시간대로 업데이트
    $ sudo vi /etc/sysconfig/clock
    = ZONE="America/Los_Angeles" // 서울은 "Asia=Seoul"
    
    - UTC=true 는 변경 X
  3) 인스턴스가 현지 시간 정보를 참조할 때 표준 시간대 파일을 찾을 수 있도록 /etc/localtime과 표준 시간대 파일사이에 심볼 링크 생성
    $ sudo ln -sf /usr/share/zoneinfo/America/Los_Angeles /etc/localtime
  4) 시스템을 재부팅하여 적용
    $ sudo reboot
  %) 확인
    $ 
