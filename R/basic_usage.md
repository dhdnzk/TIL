## txt파일을 읽어서 변수로 할당하기

```R
foo = scan("aaa.txt")
bar = scan("bbb.txt")

summary(foo)
summary(bar)
```

## 할당된 변수 지우기

```R
rm(foo)
remove(bar)

remove(list = ls() )    // 전체 삭제할때
rm(list = ls() )
```

## 스크립트 파일 읽어서 코드 실행하기

### testScript.R
```R
foo = scan("aaa.txt")   // aaa.txt 파일에는 숫자들만 들어있음
mad(foo)                // 중앙값
mean(foo)               // 평균
sd(foo)                 // 표준편차
summary(foo)            // Min, 1st Qu, Median, Mean, 3rd Qu, Max 에 관한 정보 제공
```

- 위와 같은 코드를 R스크립트 파일로 묶어서 실행할 수 있다.
- source("testScript.R")

## 스크립트 파일을 불러오는것이 아니라 콘솔상에서 바로 변수에 할당하고 싶을때는

```R
foo = c(1, 2, 3, 4, 5, 6)   
```
- 변수에 데이터를 할당할때는 "foo =" 가 아니라 "foo <-" 를 사용해도 됨.
- 그래도 R studio를 사용할때는 가급적 변수를 직접 할당하는 흉악한 짓은 하지말자.
