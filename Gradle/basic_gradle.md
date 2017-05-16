### Gradle
#### 빌드 자동화 툴
##### groovy언어를 사용
##### gradle init을 통해서 초기화
```gradle
gradle init
```
##### ./gradlew tasks를 통해서 gradle파일내의 가능한 작업을 확인할 수 있음
#####(./gradlew 명령어를 실행할 때 파일을 지정하지 않으면 default로 동일 디렉토리의 build.gradle파일을 참조)
##### ./gradlew -b 옵션을 통해서 참조할 파일을 바꿀 수 있음
```gradle
예)
./gradlew tasks
./gradlew -b testFile.gradle task1
```



