# 리눅스 날짜 포맷 지정 출력

## 표기
- 24 시간: %H
- 12시간: %I
- 분: %M
- 초: %S
- 오전/오후: %p
- unix time stamp: %s(소문자)

### 특정 날짜 구하기
```
# 1일 전
$ date -d "-1 days"
```
- 출력 : Thu Jan  7 12:35:20 KST 2021
```
# 1주 전
$ date -d "-1 weeks"
```
- 출력 : Thu Jan  7 12:35:20 KST 2021

### YYYY-MM-DD 형식 출력
```
$ date "+%Y-%m-%d" 
```
- 출력 : 2020-12-31

### 한달 3일 후를 YYYY-MM-DD 형식으로 출력
```
$ date -d "+1 months +3 days" "+%Y-%m-%d"
```
