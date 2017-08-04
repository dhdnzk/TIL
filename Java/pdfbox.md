### pdfbox

- 기본 틀 생성
PDDocumet객체가 있고, PDPage 객체가 있다.
페이지를 만들고, 다큐멘트 객체에다 add해주는 형식으로 추가.

```java
PDDocument pdDocument = new PDDocument();

PDPage pdPage = new PDPage();

pdDocument.addPage(pdPage);

pdDocument.save("./test.pdf");

pdDocument.close();
```

- 다큐멘트(한 pdf파일 전체)에 대한 환경설정

```java
PDDocument document = new PDDocument();

// information 객체를 생성한 뒤에 해당 메소드들로 설정
PDDocumentInformation pddDocumentInformation = document.getDocumentInformation();

// Setting the author of the document
pdd.setAuthor("Tutorialspoint");

// Setting the title of the document
pdd.setTitle("Sample document");

// Setting the creator of the document
pdd.setCreator("PDF Examples");

// Setting the subject of the document
pdd.setSubject("Example document");

// Setting the created date of the document
Calendar date = new GregorianCalendar();

date.set(2015, 11, 5);

pdd.setCreationDate(date);

// Setting the modified date of the document
date.set(2016, 6, 5);

pdd.setModificationDate(date);

// Setting keywords for the document
pdd.setKeywords("sample, first example, my pdf");
```

- 페이지에 글씨쓰기
```java

PDDocument pdDocument = new PDDocument();

PDPage pdPage = new PDPage();

pdDocument.addPage(pdPage);

PDPageContentStream contentStream = new PDPageContentStream(document, pdPage);

//Begin the Content stream
contentStream.beginText();

//Setting the font to the Content stream
contentStream.setFont(PDType1Font.HELVETICA_BOLD, 10);

//Setting the position for the line
contentStream.newLineAtOffset(10, 700);

String text = "This is the sample document and we are adding content to it.";

//Adding text in the form of string
contentStream.showText(text);

//Ending the content stream
contentStream.endText();

System.out.println("Content added");

//Closing the content stream
contentStream.close();

```
