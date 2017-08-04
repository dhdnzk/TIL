### composer
- php 패키지 의존성 관리 툴
- 프로젝트 홈 디렉토리에composer.json파일을 생성한 뒤, 다음과 같이 의존성 라이브러리들을 설정해준다.
```json
// ex)
{
    "require": {
        "azuyalabs/yasumi": "1.6.1"
    }
}
```
- composer install 명령어로 의존성 파일들을 설치.
- vender라는 폴더가 생성되고, 그 안에 의존성 파일들이 설치됨


