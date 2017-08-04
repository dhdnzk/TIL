## Gradle

### 빌드 자동화 툴

### gradle Build는 Project, Task라는 단위로 이루어져 있음.
- Build는 1개 이상의 Project로,
- Project는 1개 이상의 Task로 나누어짐
- Project는 어플리케이션 배포 or jar컴파일등의 작업으로 볼 수 있음.
- 세부적인 작업의 명세가 Task

#### gradle init을 통해서 초기화
```gradle
gradle init
```

#### gradle의 기본 설정파일: 

##### build.gradle
- settings.gradle파일이 존재한다면, 이도 같이 빌드에 포함시켜서 실행함.(모듈을 여러개로 분리해서 개발하는 경우에 settings.gradle파일이 유용하게 사용됨)

- (./gradlew 명령어를 실행할 때 파일을 지정하지 않으면 default로 동일 디렉토리의 build.gradle파일을 참조)

##### -b 옵션을 통해서 참조할 파일을 바꿀 수 있다. 이때에는 settings.gradle은 무시됨
```gradle
./gradlew tasks
./gradlew -b testFile.gradle task1
gradle -b someTasks.gradle
```

#### gradle task 를 통해서 build.gradle 파일 내의 가능한 작업을 확인할 수 있음

#### plugin, repositories, dependencies

```gradle
apply plugin:'java' //해당 줄이 실행되면 관련 태스크가 추가됨

// 의존성 파일을 찾아올 저장소들을 결정
repositories {
    mavenCentral()
}

// 의존성 파일들 설정
dependencies {
    compile 'mysql:mysql-connector-java:6.0.6'
}
```
