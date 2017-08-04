### 기본적으로 맥에 설치되는 mysql은 my.cnf가 없고 기본설정이 적용된다.
- 기본설정: latin1 문자코드.. utf-8로 변경하기
- /etc/my.cnf 파일을 생성해서 해당 설정변수 입력
```my.cnf
[client]
default-character-set=utf8
[mysql]
default-character-set=utf8
[mysqld]
collation-server = utf8_unicode_ci
init-connect='SET NAMES utf8'
character-set-server = utf8
sql_mode=NO_ENGINE_SUBSTITUTION
```
