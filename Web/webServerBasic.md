### 웹 서버의 작동원리를 기억해 두고자 하여 만든 문서입니다.

#### 웹 서버 컨테이너의 기본적인 동작방식

- 클라이언트가 특정 웹페이지를 요청

- 서버에서 받은 페이지에 정보를 담아서 전송
    ```html5
    <form action="/serveletFile" method="post"(or get)>

        // 화면상에서 텍스트 에딧, 버튼같은 뷰. 서브렛에서 request.getParameter("NAME") 을 통해서 값에 접근할 수 있게 해준다.
        <input name="NAME" value="VALUE"> </input>

    </form>
    ```
    
- form 에서 지정한 서브렛으로 정보들을 넘겨준다.

- 서브렛에서 데이터를 처리한 뒤에, 리퀘스트 객체를 이용해서 html파일을 넘겨주는 파일로 정보를 전달한다(jsp 등의 파일로)
```java
request.setAttribute("key", value);
```

- request 객체에 정보들을 담았으므로, html 페이지 생성을 담당하는 파일로 전달해준다.
```java
RequestDispatcher requestDispatcher = request.getRequestDispatcher("/file");
requestDispatcher.forward(request, response);
```

- JSP 파일에서, 받은 리퀘스트 오브젝트의 내용을 활용해 html파일을 생성한다.

- 만들어진 웹 페이지를 클라이언트로 반환

#### 세션 오브젝트

- 초기 : 클라이언트가 리퀘스트를 날릴때에는 세션 정보가 없음.
- 서버에서 세션을 만들고, 응답할때 세션아이디를 같이 날림
- 그 다음부터는 클라이언트에서도 세션 정보를 같이 보내면서 주고받음
- 클라이언트쪽에 쿠키를 이용해서 세션 아이디 등을 저장할 수 있다. 서버에서 이를 참조할 수 있음

```java
HttpSession httpSession = request.getSession();   // 리퀘스트로부터 세션에 관련된 정보를 얻을 수 있다.
```
