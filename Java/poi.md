### Poor Obfuscation Implementation
- 마이크로소프트 오피스 파일 포맷 조작 기능 지원 라이브러리

#### iPOIFS(Poor Obfuscation Implementation File System)

- 마이크로소프트 오피스의 OLE 2 Compound document 파일 포맷을 읽고 쓰는 컴포넌트. 모든 오피스 파일 포맷은 OLE2 방식이므로 하위 모든 컴포넌트의 기반이 된다.

#### HSSF(Horrible SpreadSheet Format)

- 마이크로소프트 엑셀 파일포맷을 읽고 쓰는 컴포넌트로서 엑셀 97버전부터 현재까지 지원한다.

#### XSSF(XML SpreadSheet Format)

- 마이크로소프트 엑셀 2007부터 지원하는 오피스 오픈 XML 파일 포맷인 *.xlsx 파일을 읽고 쓰는 컴포넌트이다.

#### HPSF(Horrible Property Set Format)

- 오피스 파일의 문서요약 정보를 읽는데 사용되는 컴포넌트이다.

#### HWPF(Horrible Word Processor Format) 

- 마이크로소프트 워드 97(*.doc) 파일을 읽고 쓰는데 사용되는 컴포넌트이다. 아직까지는 개발 초기단계이다.

#### HSLF(Horrible Slid Layout Format) 

- 마이크로소프트 파워포인트 파일을 읽고 쓰는데 사용되는 컴포넌트이다.

#### HDGF(Horrible DiaGram Format) 

- 마이크로소프트 비지오 파일을 읽는데 사용하는 컴포넌트이다.

#### HPBF(Horrible PuBlisher Format)

- 마이크로소프트 퍼블리셔 파일을 다루는데 사용되는 컴포넌트이다.

#### HSMF(Horrible PuBlisher Format)

- 마이크로소프트 아웃룩에서 사용되는 *.msg 파일을 다루는데 사용되는 컴포넌트이다.

#### DDF(Dreadful Drawing Format)

- 마이크로소프트 오피스에서 사용되는 이미지 파일을 읽어오는데 사용하는 컴포넌트이다.

#### HSSF 컴포넌트가 가장 안정적이고 많은 기능을 지원하며 다른 컴포넌트들은 사용은 가능하나 아직까지는 개발 단계이다.

### example code

- Workbook을 상속받은 워크북의 종류가 있고(마이크로 소프트 오피스 종류에 따라서 종류가 나뉨), 해당 워크북마다 쉘, 시트, 로우, 셀이라는 객체가 존재
해당 객체와 인덱스를 설정함으로써 각각의 셀을 만들거나 참조할 수 있음
파일 인풋스트림, 아웃풋 스트림으로 읽고 쓰기가 가능

```java
    //읽기
    FileInputStream fileInputStream = new FileInputStream("test.xls");

    Workbook workbook = new HSSFWorkbook(fileInputStream);
    
    fileInputStream.close();

    Sheet sheet = workbook.getSheetAt(0);

    Row row = sheet.getRow(0);

    Cell cell = row.getCell(0)

    String readValue = cell.getStringCellValue();

```

```java
    //쓰기
    Workbook workbook = new HSSFWorkbook();
    
    Sheet sheet1 = workbook.getSheetAt(0);
    
    Row row = sheet1.createRow(0);
    
    Cell cell = row.createCell(0);
    
    cell.setCellValue("Hello world!");
    
    FileOutputStream fileOutputStream = new FileOutputStream("test.xls");
    
    workbook.write(f);
    
    workbook.close();
```
