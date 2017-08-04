### 아파치, php 연동하기(mac에서)

#### 아파치 실행
```shell
sudo apachectl start
```

#### 아파치 디폴트 설정을 바꾸고 싶으면
```shell
/private/etc/apache2/httpd.conf 
```
파일의 내용 중,
```shell

DocumentRoot "/Library/WebServer/Documents" 
<Directory "/Library/WebServer/Documents">
```
부분을 수정해줌

#### 아파치 디폴트는 건들지 말고, userdir 을 활성화 해서 사용하려면
```shell
/private/etc/apache2/extra/httpd-userdir.conf
```

```shell
/private/etc/apache2/httpd.conf
```

파일을 수정해야되고, 
```shell
/private/etc/apache2/users/
```
경로에 자신의 계정명으로 된 conf파일을 생성해야된다.

##### /private/etc/apache2/extra/httpd-userdir.conf 파일 수정내용

- 3번째줄을 보면,
```shell
# Required module: mod_authz_core, mod_authz_host, mod_userdir
```
이 세개의 모듈이 필요함을 알 수 있다(위 주석은 건들지말것)
- 16번째줄 
```shell
Include /private/etc/apache2/users/*.conf 
```
의 주석을 제거


##### /private/etc/apache2/httpd.conf 파일 수정내용
```shell
/private/etc/apache2/extra/httpd-userdir.conf 
```
파일의 3번째 줄에 있던 의존성 파일들을 호출하는 코드의 주석을 제거했기 때문에, 
```shell
/private/etc/apache2/httpd.conf 
```
파일에서 
- 해당 의존성을 이어주는 작업을 해야됨(72, 78, 166 번째 줄인듯)

- 파일을 Include하는 코드도 주석 제거(503번째 줄)

```shell
//다음 라인의 주석을 제거
# LoadModule authz_core_module libexec/apache2/mod_authz_core.so

# LoadModule authz_host_module libexec/apache2/mod_authz_host.so

# LoadModule userdir_module libexec/apache2/mod_userdir.so

# Include /private/etc/apache2/extra/httpd-userdir.conf
```
- 보통 mod_authz_host.so 모듈과 mod_authz_core.so 모듈을 LoadModule하는 코드는 이미 주석이 제거되어 있는 상태이다(요세미티 기준)

##### /private/etc/apache2/users/에 자신의 계정명으로 된 conf파일을 생성

- 마지막으로 
```shell
/private/etc/apache2/users (/etc/apache2/users) 
```
- 폴더에 계정명으로 된 conf파일 (username.conf) 를 생성해 준다. 
- 경로: "/Users/id/Sites"
- Guest.conf 파일을 복사해서 수정하는 경우 Guest 부분을 자신의 계정명으로 변경하고 권한 설정 부분을 사용할Apache 버전에 맞도록 변경. (기존의 Guest.conf파일의 권한설정은 Apache 2.2 기준으로 되어 있어 동작하지 않는다 - 4, 5번째 줄 삭제 후 Require all granted 추가) 모든 변경이 완료되었으면 아파치를 재시작 한다.

#### 아파치에 php 연동
- 다음 파일을 수정
```shell
/private/etc/apache2/httpd.conf
```
- 다음에 해당하는 주석을 풀어준다
```shell
#LoadModule php5_module libexec/apache2/libphp5.so
```

#### 추가로 php의 설정을 변경하려면
```shell
/private/etc/php.ini.default
```
파일을 php.ini 파일로 파일명을 변경하고 설정 내용을 변경하면 된다.
