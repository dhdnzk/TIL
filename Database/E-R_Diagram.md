## E-R Diagram을 이용한 DB모델링 (2016.4.30)

- UML, ERD

- UML은 program측면에서 software를 바라보는 관점

- ERD는 data측면에서 software를 바라보는 관점

- UML 중요!

### 모델링

#### 소프트웨어 모델링이란

- 만들고자 하는, 머리 속에 있는 생각을 누구나 볼 수 있게 본을 뜨는것

- 객체나 DB를 그림으로 표현하는것
  
#### 모델링을 하면 좋은점

- 만들고자 하는 바를 더 명확하게 알 수 있음.

- 좀 더 잘 만들 수 있음.

- 이해하고 소통하기 편하다!

#### 모델링을 하면 더 좋은점

- 면접 볼 떄 좋음ㅋㅋ

- 보여줄 때 좋음ㅋㅋ

- 만들고나면 뿌듯ㅋㅋ

#### 소프트웨어를 해부하면

- 크게 "동작"과 "데이터"로 나눌 수 있음

- 인간을 위한 소프트웨어중에 데이터가 없는 소프트웨어는 없다!

### ERD

- Entity-Relationship Diagram

- UML은 sequence diagram, class diagram정도만 그리는 반면

- ERD는 실무에서 자주 그리게 됨!

- 대기업에서는 ERD를 그리는 업무 프로세스가 존재함... 어차피 해야되는거

#### ERD 도구

- ER-win (유명... but유료)

- MySQL Workbench (mysql의 전체 기능을 다 다룰 수 있음)

- ERD Tool, DB Design tool 등 검색

- 손으로 짜도 되지만.. ERD tool을 통해서 효율을 높이자

#### ERD 식별자

- | : 전체참여

- O : 부분참여

- < : n

- - : 1

#### ERD 표기법

#### 데이터베이스

- 모델링에서는 데이터베이스를 스키마(scheme)라고도 함

#### 선

- 실선 : primary key로 연결됨

- 점선 : foreign key로 연결됨

#### 관계

- 1  <Xenonix> 이용자
- 10 <안녕하세요> 글

#### RDBMS무결성

- 실체 무결성

- 참조 무결성

- 영역 무결

#### 알아야 할 용어

- Identifying Relationship : 식별 관계

- foreign key가 Primary key로 지정되어 있는가

#### Foreign key options

- RESTRICT : 참고 테이블의 값과 변경을 거부

- CASCADE : 같이 삭제 또는 수정

- SET NULL : null로 변경

- NO ACTION : restrict와 같은 결과... (but 후불의 개념.. mysql에서는 둘의 차이가 무의미)

### 실습

#### (질문) log성 데이터를 어떻게 처리할것인가?

- db partioning : log성 데이터들을 일정 기간별로 잘라서 따로 보관(mysql은 partioning기능 지원함)

- sharding 

#### 정규화, 역정규화

- 정답이 없다!

#### foreign key option

- 아주 자주쓰이진 않지만, 적절하게 알고쓰면 매우 유용함!

#####  RESTRICT 

- 참고 테이블의 값과 변경을 거부 

- 학생의 정보중에 전공학과의 번호가 들어있을텐데, 이 전공부서에서 특정 부서의 번호를 바꿔버리면 거절함

##### CASCADE 

- 같이 삭제 또는 수정

- 전공부서에서 특정 부서의 번호를 바꿀떄 학생들의 각각의 레코드에 들어있는 전공학과 번호도 같이 바뀜

- 전공부서에서 학과를 삭제할때 castcase를 적용해버리면, 해당 학과의 학생들이 없어져버리는 문제 발생

##### SET NULL 

- null로 변경

- set null으로 설정해놓고 학부 번호를 바꾸면, 해당 학부가 전공인 학생들의 값은 전부 null로 설정됨

##### NO ACTION

- restrict와 같은 결과... (but 후불의 개념.. mysql에서는 둘의 차이가 무의미)

### DB를 소프트웨어로 담아내기

- db에 있는대로(비슷하게) 모델링하면 됨

### NOSQL

#### log성 데이터들을 RDBMS에 저장했을때의 장점

- 추가로 필요한 학습이 적다

- 현재 인프라로 사용할 수 있음

- RDBMS의 무결성을 보장해줌

#### NOSQL의 장점

- Insert 속도가 빠름(insert 하지도 않아놓고 값 리턴... 하고나서 뒤에서 처리, 무결성이 보장되지 않음)

- 통계자료를 뽑아내기 위한 API 구성이 잘 되어있음(RDBMS에 비해서)

### 수업 끝나고나서 나온 이야기

- 초당 100만개의 요청이 들어오고, DB에서는 초당 100개의 응답밖에 처리를 못단다고 하면

- RDBMS가 초당 처리할 수 있는 Query문의 개수가 제한되어있음

- 서버와 DB 사이에 memory queue를 만들어서 비동기 처리

- apache activemq (실시간으로 읽기를 하고싶을때 : activemq를 쓰면안됨)

