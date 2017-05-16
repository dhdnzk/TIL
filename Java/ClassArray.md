### 특정한 클래스의 2차원 이상 배열을 생성할때
#### 문제가 발생한부분
```java

// 다음과 같은 형식으로 끝내버리면, 내부가 전부null로 처리된다.
TmpClass array[][] = new TmpClass[9][9];

```
#### 이렇게 바꾸자

```java

// 따라서 다음과 같은 방식으로 인스턴스를 하나씩 생성해준다.
TmpClass array[][] = new TmpCass[9][9];
for(int i = 0; i < array.length(); i ++) {
    for(int j = 0; j < array[i].length(); j ++) {
        array[i][j] = new TmpClass();
    }
}

```
