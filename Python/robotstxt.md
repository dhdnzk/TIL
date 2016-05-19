### robots.txt
#### robot exclusion protocol

- 웹사이트 관리자가 자신의 사이트에 검색 로봇이 자료를 수집해도 좋으며, 어느 디렉터리에 접근해도 좋은지 등에 대한 정보를 적어놓는 규정

- [http://www.robotstxt.org/](http://www.robottxt.org/)

#### python에서 robot.txt에 접근하기, 특정 페이지를 수집해도 되는지 여부 확인하기(3단계)
-  robotparser 모듈이 제공되므로, 객체를 생성해서 해당 홈페이지의 robots.txt파일을 읽고, 페이지를 읽을 수 있는지 여부를 하나씩 물어보면 됨.

- RobotFileParser: url을 매개변수로 해서 객체를 생성
- read(): 메소드를 호출해서 파일을 읽어옴
- can_fetch(): 읽어온 페이지에서 크롤러 이름과 url을 매개변수로 하는 메소드를 호출해서 가능여부 확인

```python
import robotparser

robot_parser = robotparser.RobotFileParser("http://blog.daum.net/robots.txt")

robot_parser.read()

robot_parser.can_fetch('mycrawler', 'http://blog.daum.net') # True
```
- http://blog.daum.net에서 mycrawler라는 수집기가 http://blog.daum.net에서 수집할 수 있는지 여부를 물어보는 코드

#### 웹 페이지 읽어들이기

```python
import urllib2

urllib2.urlopen("http://www.google.com").read()
```
