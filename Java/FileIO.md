## 자바에서 파일입출력을 진행할때

- 파일에 관련된 객체를 생성(파일명 지정)
- 입력/출력에 관한 스트림 객체를 생성.
- 생성된 스트림을 그대로 가져다 사용한다면 속도 저하의 이슈가 발생하므로 버퍼 스트림을 하나 더 생성해서 달아준다.
- 실제 입력/출력코드는 버퍼스트림 객체를 통해서 진행.


## 파일 입력 Example code 

```java
File f = new File("fileName");
if (f.canRead()) {
    Reader reader = new FileReader("filename");
    BufferedReader bReader = new BufferedReader(reader);

    bReader.readLine();
    
    bReader.close();
    reader.close();
}
```

## 파일 출력 Example code

```java
File f = new File("fileName");
if (f.canWrite()) {
    Writer writer = new FileWriter("filename");
    BufferedWriter bWriter = new BufferedWriter(writer);

    bWriter.write("입력할 내용");
    bWriter.append("입력할 내용");
    bWriter.flush();

    bWriter.close();
    writer.close();
}
```
