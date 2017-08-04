### spring framework 학습 내용 정리

#### XML을 통해서 DI 설정을 구현

- property 태그로 초기화 해주려면 setter함수가 구현되어 있어야 한다.
```xml
<bean id="calculator" class="com.aaa.bbb.ccc.Calculator"
    <property name="aList">
        <list>
            <value>aa</value> <value>bb</value>
            <value>cc</value>
        </list>
    </property>
</bean>

<bean id="myCalculator" class="con.aaa.bbb.ccc.MyCalculator">

    <properity name="calculator">
        <ref bean="calculator"/>
    </properity>

    <properity name="firstNum" value="10"/>

    <properity name="secondNum" value="2"></properity>

</bean>
```

- setter와 xml파일상에서의 이름 규칙을 맞춰야함
xml에서 이름이"firstName"일 경우: java코드에서 setter 메소드명 : setFirstName
- xml파일의 작성이 끝났다면, 자바 코드상에서 xml파일을 참조할 경로를 설정
- xml파일 경로를 매개변수로 알려주면서 컨테이너 객체를 생성
- 컨테이너에서 어떤 클래스를 원하는지 매개변수로 알려주면서 객체를 조립해서 받아옴
- 사용

```java
String configFilePath = "classpath:applicationCTX.xml";

AbstractApplicationContext ctx = new GenericXmlApplicationContext(configFilePath);

MyInfo myInfo = ctx.getBean("myInfo", MyInfo.class);

myInfo.getInfo();

ctx.close();
```

- constructor-arg: property 태그로 필드값을 설정하는것이 아니라, 생성자를 통해서 매개변수로 받아온 값을 필드값으로 설정하고 싶을때
```xml
<bean id='..' class='....'>
    <constructor-arg>
        <value>홍길동</value>
    </constructor-arg>
    <constructor-arg>
        <value>10살</value>
    </constructor-arg>
    <constructor-arg>
        <value>300키로</value>
    </constructor-arg>
</bean>
```
```xml
<bean id='..' class='....'>
    <constructor-arg value='홍길동'/>
    <constructor-arg value='10살'/>
    <constructor-arg value='300키로'/>
</bean>
```

- xml파일로 constructor-arg 혹은 property를 설정하는 다른방법
```xml
<bean id="id1" class="main.java.com.javalec.ex.Class" c:memberVariableName="vlaue" p:memberVariableName="value">
```

#### java 코드로 DI설정을 구현

- 어노테이션을 달아준다.
```java
@ImportResource("classpath:main/resources/applicationCTX.xml")  // 자바설정파일에 xml 추가할때

@Configuration
class ApplicationConfig {

@Bean
public Student student1() {
    new 로 생성해서 초기화작업
}

@Bean

...

}
```

- java코드로 컨테이너 생성할때

```java
AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(ApplicationConfig.class);
```

#### 스프링 컨테이너의 생명주기

- 생성
```java
GenericXmlApplicationContext ctx = new GenericXmlApplicationContext();  //매개변수로 설정파일 경로를 알려주면 바로 설정까지 완료된다
```

- 설정
```java
ctx.load("classpath:aaa/bbb/ccc/applicationCTX.xml");

ctx.refresh();
```

- 사용
```java
Object object = ctx.getBean("idName", Aaa.class);
```

- 종료
```java
ctx.close();
```

#### Bean의 생성/소멸시 처리

##### implements InitializingBean, DisposableBean
- Bean이 생성, 초기화될때 호출되는 메소드
```java
class Student implements InitializingBean {

    @Override
    public void destroy() throws Exception {

    }

}
```

- Bean이 삭제, 소멸될때 호출되는 메소드
```java
class Student implements DisposableBean {

    @Override
    public void afterPropertiesSet() throws Exception {

    }

}
```
- 위의 인터페이스를 구현하고 나면 해당 bean객체가 생성/소멸될때 각각의 메소드가 실행됨 

##### @PostConstruct, @PreDestroy
- Bean 내부에 임의의 메소드를 정의하고 위의 어노테이션을 달아주면, 해당 Bean이 생성/소멸될 때 각각의 메소드가 호출된다. 
```java
@PostConstruct
public void initMethod() {

}

@PreDestroy
public void destroyMethod() {

}
```

#### scope
- scope
```java
<bean id="" class="" scope="singleton">     // default: singleton
```
