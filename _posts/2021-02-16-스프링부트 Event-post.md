---
title: 스프링부트 트랜잭션 분리
categories: springboot
---

# Event

## 스프링 4.2 이상
  - 스프링 4.2 이상 버전에서는 ApplicationEvent, ApplicationListener 를 구현할 필요가 없다.(이전 버전에서는 구현해야함)
  - ApplicationEventPublisher 에서 이벤트를 발행한다.
  
### ApplicationEvent
  - 이벤트 클래스를 생성한다. (ApplicationEvent 을 상속받지 않아도 된다.)
  - 이벤트 리스너가 수행할 이벤트 대상 클래스이다.
  - 보통 getter 만으로 충분하다.
      ```
        @Getter
        public class CredentialRequestEvent {

          private String mailAddress;
          private String sendData;

          public CredentialRequestEvent(String mailAddress, String sendData) {
              this.mailAddress = mailAddress;
              this.sendData = sendData;
          }
        }
      ```

### ApplicationListener
  - 이벤트 객체를 받아 이벤트를 실행하는 주체이다. (ApplicationListener<E> 를 구현하지 않아도 된다.)
  - 이벤트 리스너는 실행해야할 service 객체에 의존한다.
  - 이벤트 리스너 메서드에 @EventListener 어노테이션을 선언하고 파라미터로 해당 이벤트 객체를 받도록 작성해놓으면 된다.
  - @Order 어노테이션으로 이벤트 큐의 실행 순서를 지정할 수 있다.
  - @Async 어노테이션으로 비동기 실행을 설정할 수 있다.
      ```
        @Component
        @RequiredArgsConstructor
        public class CredentialRequestHandler {

          private final MailService mailService;

          @Order(1)
          @Async
          @EventListener
          public void sendMail(CredentialRequestEvent event) {
              mailService.sendCredentials(event.getMailAddress(), event.getSendData());
          }
          
          @Order(2)
          @Async
          @EventListener
          public void postSendMail(CredentialRequestEvent event) {
              mailService.postSendCredentials(event.getMailAddress(), event.getSendData());
          }
        }
      ```
  
### @TransactionalEventListener
  - 이벤트를 발행하는 메서드에 선언하는 어노테이션이다.
  - 설정 value로 phase, fallbackExecution 등이 있다.
    1. phase 는 AFTER_COMMIT, AFTER_COMPLETION, AFTER_ROLLBACK, BEFORE_COMMIT 이 있다. 필요한 상황에 따라서 설정해주면 된다.
    2. fallbackExecution 은 true, false 값을 가진다. 기본값은 false 이다. true 이면 만약 트랜잭션이 존재하지 않는 곳에서 이벤트를 발행했을 경우, 예외를 던진다.
        ```
          @Autowired
          private ApplicationEventPublisher publisher;

          @TransactionalEventListener(phase = TransactionPhase.AFTER_COMMIT, fallbackExecution = true)
            public CommonResult sendEmail(RequestDto requestDto) { 

            ...
            publisher.publishEvent(new CredentialRequestEvent(requestDto.getEmailAddress(), data));
          }
        ```

### @EnableAsync
  - 스프링부트 Application 클래스에 @EnableAsync 어노테이션을 선언하면 비동기 기능을 활성화 시킨다.
  - 이벤트 리스너 메서드에 선언 할 경우 비동기로 실행된다. (별개의 스레드에서 동작)

### 참조
  - https://brunch.co.kr/@springboot/422
  - https://velog.io/@ljinsk3/Spring-Events
