### aspect oriented programming (관점 지향 프로그래밍)

#### 용어정리
- Aspect: 공통 기능
- Advice: Aspect의 기능 자체
- JoinPoint: 핵심 기능 중에서, Advice를 적용할 부분이 존재하는 핵심 기능(ex: method, field, ETC..)
- Pointcut: JoinPoint의 일부분으로, 실제로 Advice가 적용된 부분
- Weaving: Advice를 핵심 기능에 적용하는 행위

#### 스프링에서 AOP를 구현하는 방법: proxy
- Client -> Proxy -> Target
- 스프링에서 AOP를 구현하는 방식: XML schema, @Aspect

#### XML schema 방식
- 핵심 기능은 그대로 두고, xml 설정파일만 수정함으로써 
1. 의존성 설정
```xml
<dependency>
    <..>
    <..>
</dependency>
```
2. 공통 기능의 클래스 제작(Advice 역할 클래스)
```java

/* 핵심기능을 실행하면서, 해당 기능을 실행하는데 걸린 시간을 계산해서 출력하는 프록시 */
public class LogAop {

    public Object loggerAop(ProceedingJoinPoint joinPoint) {

        String signitureStr = joinPoint.getSignature();

        long startTime = System.currentTimeMillis();

        try {

            Object obj = signitureStr.proceed();    // 핵심 기능을 실행하는 부분

            return obj;

        } finally {

            long endTime = System.currentTimeMillis();


            System.out.println(signitureStr + "is finished.");
            System.out.println(signitureStr + "경과된 시간: " + (endTime - startTime));

        }

    }

}

```
3. XML파일에 Aspect 설정
```xml
<!-- AOP -->
<Beans xmlns:aop="http://www.springframework.org/schema/aop"/>              // aop를 사용하겠다고 임포트

<aop:config>
    <aop:aspect id="logger" ref="logAop">                                   // 밑에 logAop를 id로 해서 작성해둔 bean객체를 참조*
        <aop:pointcut id="publicM" expression="within(com.javalec.ex)"/>    // expression으로 공통기능을 적용할 범위를 지정
        <aop:around method="loggerAop" pointcut-ref="publicM"/>             // 프록시 메소드: loggerAop, 참조할 포인트컷의 id: publicM
    </aop:aspect>
</aop:config>

<bean id="logAop" class="main.java.com.javalec.ex.LogAop"/>     //여기*
```

- advice 종류
```xml
<aop:before>            // 메소드 실행 전에 advice실행
<aop:after-returning>   // 정상적으로 메소드 실행 후에 advice 실행
<aop:after-throwing>    // 메소드 실행중 exception 발생시 advice 실행
<aop:after>             // 메소드 실행중 exception이 발생하여도 advice 실행
<aop:around>            // 메소드 전/후 및 excpetion이 발생하여도 advice 실행
```
- 이중, around와 before를 제일 많이 사용함

#### Java code 방식
```java
@Aspect
public class AopClass {
    
    @pointcut("within(com.javalec.ex.*)")           // 필수
    private void pointcutMethod() {}

    @Around             // 다음 다섯가지 방법으로 advice 실행법을 구현할 수 있다.
    @before
    @AfterReturning
    @AfterThrowing
    @After

}
```
