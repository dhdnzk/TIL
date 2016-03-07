## intellij에서 Junit을 통해서 테스트 주도 개발하기

- 2015년 2학기 오픈소스 소프트웨어 수업때 들었던 내용 정리

### 디렉토리 경로 설정하기, 패키지 만들기, 클래스 만들기

- 프로젝트 Import 할때 Import Maven Projects automatically 체크박스 표시해주기
- 외부 라이브러리에 JDK처럼 Junit4 추가해주기
- 디렉터리 구조를 설정할때 intellij에서 제공하는 "Mark Directory As" 기능때문에 헷갈리는 부분이 있었는데, src 디렉터리를 "Unmark As Sources Root"로 설정하고, 구조를 다시 잡아주자.
- src 디렉터리 안에 main, test 디렉터리를 만들고, 그 안에 각각 java와 resource 디렉터리를 만든 후에, 끝단에 있는 이 4개의 디렉터리에 "Mark Directory As"기능으로 적절히 표시. 각각의 java 디렉터리에 패키지를 만들고 여기서 작업한다. (디렉토리 구조를 만드는법은 사람마다 설명이 다른데, 표준이 없는건지 아니면 나만 모르고 있는건지는 더 찾아봐야 알듯)
- java 디렉터리 : .java 파일들
- resource 디렉터리 : 기타 설정파일 등등..
- 어떤 방식이 되었든, 소스코드와 테스트 코드를 작성할 틀을 적절히 만들어주자.
- 메인, 테스트 디렉토리에 각각 같은 이름의 패키지 만들기 (도메인을 거꾸로, 전부 소문자 (.하나하나를 디렉토리로 구분하기 때문에 전부 소문자로))
- 클래스 만들기 (클래스명은 무조건 명사, Camel 표기법으로, 언더바, 한글 넣으면 안됨(은행, 보험사같은곳만 내부에서 쓰는 특수용어 사용 ex : 청구심사))
- 메인 패키지에 클래스명이 "Class" 라면, 테스트패키지의 클래스명은 "ClassTest" 와 같은식으로 지어준다.

### 테스트 주도 개발방법

- 테스트코드 짜기 ( @Test)
- 테스트 ( 리턴값 상수로 해서 파란불 들어오도록)
- 그담에 변수 사용해서 테스트
- 코드 왼쪽에 파란불 : 사용되는 코드인지 확인해서 보여줌(사용중일때 초록색)
- 예외가 뜨던 뜨지 않던지간에 의도한대로 코딩을 했다면 파란불이 나오게 해야함
- 밑에껄 고쳤을때 위에 앞서 테스했던 메소드들이 작동하지 않을 수 있다. 따라서 테스트 메소드를 하나 만들때마다 회기 테스트를 다시 해줘야함.
- unit test의 최소 단위는 메소드
- unit test를 해야할 책임은 개발자에게 있음(테스터에게 책임을 전가할 생각말것)
- 단위테스트 할때에는 메인메소드가 없음
- 메이븐을 설치해서 프로젝트를 통째로 갖고있으면 IDE가 없어도 커맨드라인에서 명령어 한번으로 테스트를 해줄 수 있다.
- TDD를 할때에는 테스트를 작성할 생각부터.
- 프로젝트가 커지면 메소드 크기가 점점 커지는데, 테스트를 이어나가기 위해서 메소드를 분리해서 크기를 줄일것. 크기가 큰 메소드를 잘뜯는법 > 리펙토링( 책의 챕터이름 > 리펙토링 메뉴의 항목들 )

### 테스트 주도 개발 예시 코드

- 메인 소스코드
```java
package test.co.kr;

public class Source {

    public static boolean returnTrue() {
        return true;
    }

}
```
- 테스트 소스코드
```java
pckage test.co.kr;

import org.junit.Test;
import junit.framework.TestCase;

public class SourceTest {

    @Test
    public void returnTrue() {
        TestCase.assertEquals( true, test.co.kr.Source.returnTrue() );
        TestCase.assertTrue( Source.returnTrue() );
    }

}
```
- 위와 같은 형식으로 테스트코드를 먼저 작성한 뒤에 메소드를 만들고, 여러가지 테스트코드를 계속 만들어가면서 단위테스트를 실행해서 빨간불이 나오는것을 고쳐가는 과정으로 진행한다. TestCase.assert* 메소드를 하나씩 추가해주자.
