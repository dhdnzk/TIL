## mysql 계정 추가 및 특정 테이블에 대한 권한 부여하기, 로컬, 특정 IP에서 계정으로 접속하기

- CREATE USER 'id'@'localhost' IDENTIFIED BY '암호';
- localhost 대신에 특정 ip나, 아무곳에서나 접속하게 하려면 깡으로'%' 입력
- '192.168.0.%' 등등..
- 계정 이름을 쓸때 'username'과 같은 식으로 따옴표를 붙여줘야함

### 모든 IP에서 접속 가능한 계정 만들기
```
INSERT INTO mysql.user (host,user,password) VALUES ('%','root',password('비밀번호'));
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' with grant option;  
FLUSH PRIVILEGES;
```
- GRANT ALL PRIVILEGES ON은 뒤에 나오는 계정에 어떤 데이터베이스와 어떤 테이블에 접근할 권한을 줄 것인가를 설정하는 명령어
- \*.\*은 각각 <데이터베이스명>.<해당 데이터베이스의 테이블명을 의미>
- grant option은 해당 권한을 부여받은 유저가 또다시 다른 유저에게 권한을 부여할 수 있는 권한을 주는 옵션
- 따라서 위의 명령문을 실행하고 나면 모든 IP대역에서 접속 가능하고, 전체 디비와 테이블들에 접근 가능하고 남들에게 권한도 줄 수 있는 root 계정을 만들게 됨

### 특정 대역 IP에서 접속 가능한 계정 만들기
```
INSERT INTO mysql.user (host,user,password) VALUES ('192.168.8.%','root',password('비밀번호'));
GRANT ALL PRIVILEGES ON *.* TO 'root'@'192.168.8.%';
FLUSH PRIVILEGES;
```

### 특정 IP에서만 접속 가능한 계정 만들기
```
INSERT INTO mysql.user (host,user,password) VALUES ('192.168.8.123','root',password('비밀번호'));
GRANT ALL PRIVILEGES ON *.* TO 'root'@'192.168.8.123';
FLUSH PRIVILEGES;
```

### my.cnf 파일 수정하기

- 위의 과정을 거친 뒤 /etc/mysql/my.cnf 파일을 수정하면 끝.
- 파일을 오픈 후 bind-address 를 주석처리 혹은 * 하거나 특정 ip를 써주면 된다.
```
# Instead of skip-networking the default is now to listen only on
# localhost which is more compatible and is not less secure.
bind-address = *
```


## 원격 접속 권한 삭제
###아래와 같이 파일을 /etc/mysql/my.cnf 파일을 수정

```
# Instead of skip-networking the default is now to listen only on
# localhost which is more compatible and is not less secure.
bind-address = 127.0.0.1
```
### my.cnf파일 수정 후에 mysql 에 다시 접속 후 삭제하고자 하는 계정의 원격 권한 설정을 삭제하여 준다.

```
DELETE FROM mysql.user WHERE Host='%' AND User='root';
FLUSH PRIVILEGES;
sudo service mysql restart  // mysql을 재시작해준다.
```
