---
title: httpMessageNotReadableException 에러
categories: springboot
---

# httpMessageNotReadableException 에러

## 원인
  1. 로그를 남기기 위해 HttpServletRequest 클래스를 감싼 커스텀 래퍼클래스를 작성
  2. HttpServletRequest 의 InputStream 을 읽어 올 때의 조건을 만족하지 않아 발생
    ```
    public ReReadableHttpServletRequestWrapper(HttpServletRequest request) throws IOException {

        //So that other request method behave just like before
        super(request);
        StringBuilder stringBuilder = new StringBuilder();
        BufferedReader bufferedReader = null;
        try {
            InputStream inputStream = request.getInputStream();
            // stream 이 Null 이 이나거나 사용 가능 할때만 read
            if (inputStream != null && inputStream.available()) { // <- 문제가 되는 부분
                bufferedReader = new BufferedReader(new InputStreamReader(inputStream));
                char[] charBuffer = new char[128];
                int bytesRead = -1;
                while ((bytesRead = bufferedReader.read(charBuffer)) > 0) {
                    stringBuilder.append(charBuffer, 0, bytesRead);
                }
            }
        } catch (IOException ex) {
            throw ex;
        } finally {
            if (bufferedReader != null) {
                try {
                    bufferedReader.close();
                } catch (IOException ex) {
                    throw ex;
                }
            }
        } //Store request pody content in 'body' variable
        body = stringBuilder.toString();
    }
    ```
    - 문제가 발생하는 부분 : && inputStream.available()
    - body가 있을때는 1을 반환하고 없을 때는 0을 반환하는데 확실하지는 않다.
    - body가 있을 때에도 0을 반환하는 경우가 발생한다.
    - 그래서 HttpServletRequest 의 InputStream 값이 없어 스프링 컨버터에서 httpMessageNotReadableException 을 발생시킨다.
    
## 해결
  - inputStream.available() 을 조건문에서 제거
    
    
    
