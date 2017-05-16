## 제네릭
- 클래스 내부에서 사용할 자료형을 클래스 외부에서 지정하는 기법.

### 사용법

- SampleClass.java
```java
public class SampleClass<T> {

    public T var;

    public SampleClass (T var) {
        this.var = var;
    }

    public SampleClass () {
    }

    ...
}
```

- Main.java
```java {

    SampleClass sampleClass1 = new SampleClass<>( "hello, world!" );   // sampleClass1.var 의 자료형은 String형이 되고, "hello, world!"로 할당
    SampleClass sampleClass2 = new SampleClass( "hello, world!" );     // sampleClass2.var 의 자료형은 String형이 되고, "hello, world!"로 할당
    SampleClass sampleClass3 = new SampleClass( 10 );                  // sampleClass3.var 의 자료형은 int형이 되고, 값은 10으로 할당
    SampleClass sampleClass4 = new SampleClass();                      /* sampleClass4.var 의 자료형은 결정되지 않고, null 상태. 
                                                                        * set 메소드등을 사용해서 값을 할당해주면, 그때 자료형이 결정됨*/

    sampleClass4.getVar.getClass();                                    // 아무것도 들어있지 않은 상테에서 접근해 자료형을 물어보면 널포인터 예외가 나옴

}
```
- 클래스 정의부에서는 클래스명 뒤에 <T>, <E>등 <>로 감싼 알파벳이 들어가고, 클래스 내부에 그 알파벳을 사용한 멤버변수가 들어간다.
- 자바에서 제네릭을 사용할때 주의할점 네가지 
- 1. 클래스를 정의할때 class명 바로 뒤에 써줌 
- 2. class 내부의 제네릭으로 선언할 멤버변수의 자료형 자리에 써줌
- 3. 인스턴스를 생성할때는 제네릭 표시를 따로 써주지 않아도 매개변수의 자료형에 따라서 결정됨
- 4. 생성자 정의부분에는 써주지 않음!
- 5. 오버로드 메소드가 다수 있을때.. instance of 문법 참고.
