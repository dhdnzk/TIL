## firebase 초기세팅
- 3steps

### 1. Tools checkup
    - API level 9 이상(android 2.3; Gingerbread 이상)
    - Play services 9.0 이상
    - Android SDK Tools... SDK Manager > SDK Tools > Google play services(ver 30+), Google repository(ver 26+)

### 2. Firebase console
    - firebase project 생성
    - Add firebase to your android app...(클라이언트 어플이 firebase에 접근 가능하도록)
        - 1. unique package name 을 입력해준다
        - 2. 내 debug key에 대한 SHA1 hash값을 입력해준다
            ```
            keytool -exportcert -list -v -alias androiddebugkey -keystore ~/.android/debug.keystore
            // 커맨드 입력후에 요구하는 비밀번호는 전체 소문자로

            ```
            2번의 작업을 완료하면 google-services.json파일을 다운로드 받는데, 이를 firebase와 연동할 안드로이드 프로젝트의 app 디렉터리에 위치시킴
            만약 firebase 설정이 바뀐다면, 다시 다운받아서 프로젝트에 입력해주어야함
            이를 통해 프로젝트에서 firebase를 인식하고, 접근하는것이 가능해짐

### 3. Project modification
    - 프로젝트 레벨의 build.gradle 파일에서 다음 내용 추가
        - buildscript > dependencies에 추가해줄 내용
            ```build.gradle
                classpath 'com.google.gms:google-services:3.0.0'
            ```
    - 앱 레벨에서의 build.gradle 파일에서 다음 내용 추가
        - 제일 하단에(파일의 맨 끝에) 
            ```build.gradle
                apply plugin: 'com.google.gms.google-services'
            ```
        - dependencies 안쪽에 사용할 의존성 라이브러리들을 추가(자동으로 해주겠지만, 특정 버전을 사용하고 싶다면 직접 입력해 주어야 한다)
            ```build.gradle
                // 2017_09_14 현재 firebase core 최신버전: 10.2.6
                compile 'com.google.firebase:firebase-core:10.2.6'
            ```
### sync project한번 돌려준 뒤, 세팅이 잘 끝났나 확인하려면 앱을 한번 launch해서 로그를 확인하자


