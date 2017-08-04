### 외부 파일을 이용한 설정(8-1)

#### Environment 객체를 이용한 방법
- 디비 정보 등 다양한 외부 정보를 자바 코드상에 직접 갖고있는것이 아니라, 설정 파일을 따로 둠으로써 참조할 수 있게끔 제공된다.
- context -> environment -> propertysources 순으로 객체를 호출해서 프로퍼티를 추가 밑 추출할 수 있다.
- environment 객체 안에 하나의 propertySource만 존재하는것이 아닌, 여러개의 프로퍼티 객체가 존재.
- 데이터를 참조할 때에는 특정 프로퍼티 객체에 직접 접근하는것이 아니라, 매개변수로 원하는 데이터를 설정해주면 environment객체가 전체 프로퍼티를 참조하면서 알아서 찾아줌
    ```java
    ConfigurableApplicationContext ctx = new GenericXmlApplicationContext();    //context 생성

    ConfigurableEnvironment environment = ctx.getEnvironment();     //수정 가능한 environment 타입 객체 생성

    environment.getPropertySources().addLast(new ResourcePropertySource("classpath:admin.properties")); //프로퍼티 소스 객체를 생성하면서 프로퍼티 소스 리스트에 더해줌

    System.out.println(environment.getProperty("admin.id"));    //설정파일에 적어둔 키를 통해서 값을 찾아옴

    System.out.println(environment.getProperty("admin.pw"));
    ```

##### implements EnvironmentAware
- EnvironmentAware 인터페이스를 구현하면, 객체가 생성될때 다음 메소드가 가장 먼저 호출된다.
```java
    @Override
    public void setEnvironment(Environment environment) {

    }
```

- 이 메소드의 호출이 우선이기 때문에 여기서 받아온 환경변수를 가지고 InitializingBean, DisposableBean 구현 등의 초기화 작업에 사용해줄 수 있다.
```java
@Override
public void afterPropertiesSet() {

    this.environment.getProperty("admin.id");

    this.environment.getProperty("admin.pw");

}
```

- Environment 객체는 싱글톤으로 생성됨.


#### Environment 객체를 이용하지 않고 직접 설정파일을 사용하는 방법

##### xml파일을 이용한 방법
- applicationCTX.xml등의 xml파일에 설정파일을 참조하는 태그와 주소를 직접 입력한 뒤, xml파일에서 직접 참조
```xml
/* beans시작태그의 속성 안에 다음 두가지 경로를 추가해주어야 사용 가능 */

//context 추가
xmlns:context="http://www.springframework.org/schema/context

//location추가
xsi:schemaLocation=
    http://www.springframework.org/schema/beans/spring-beans.xsd 
    http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
```

- 추가 하고 나면, 다음과 같은 형식으로 파일에 직접 접근해서 참조 가능
```

<context:property-placeholder location="main/resources/admin.property"/>    //구체적인 파일 경로를 잡아줌. 이 줄을 추가하기 위해서 위에 작업이 필요

<bean id="example1" class="main.java.com.javalec.ex.ExampleClass">
    <property name="id">
        <value>${example.id}</value>
    </property>
    <property name="examplePw">
        <value>${example.pw}</value>
    </property>
</bean>
```

##### Java annotation을 이용한 방법

