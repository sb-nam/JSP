# JSP

## jsp doget방식
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style type="text/css">
#loginFormArea {
   text-align: center;
   width: 250px;
   margin: auto;
   border: 1px solid red;
}

h1 {
	text-align: center;
}
</style>
</head>
<body>
	<h1>로그인</h1>
	<section id="loginFormArea">
		<form action="login" method="get">
			<label id="id">아이디:</label><input type="text" name="id" id="id"><br>
			<label id="passwd">비밀번호:</label><input type="password" name="passwd" id="passwd"><br>
			<br> <input type="submit" value="로그인" />
		</form>
	</section>
</body>
</html>
```
## 로그인 서블릿
```java

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class LoginServlet
 */
@WebServlet("/login")
public class LoginServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    /**
     * @see HttpServlet#HttpServlet()
     */
    public LoginServlet() {
        super();
        // TODO Auto-generated constructor stub
    }

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		String id = request.getParameter("id");
		String passwd = request.getParameter("passwd");
		response.setContentType("text/html; charset=euc-kr");
		PrintWriter out = response.getWriter();
		out.println("아이디"+id+"<br>");
		out.println("비밀번호"+passwd+"<br>");
	}

}
```

## a테그를 이용하여 doget사용하기
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h2>2페이지 목록 요청하기</h2>
<a href="boardList?page=2">2page</a>
</body>
</html>
```
## boardList 서블릿
```java
import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class boardListServlet
 */
@WebServlet("/boardList")
public class boardListServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    /**
     * @see HttpServlet#HttpServlet()
     */
    public boardListServlet() {
        super();
        // TODO Auto-generated constructor stub
    }

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		String  page=request.getParameter("page");
		response.setContentType("text/html; charset=euc-kr");
		PrintWriter out = response.getWriter();
		out.println(page+"페이지 게시판 목록 출력");
	}

}
```
## dopost방식
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h1>회원가입</h1>
	<form action="memReg" method="post">
		회원명: <input type="text" name="name"><br> 
		주소: <input type="text" name="addr"><br> 
		전화번호: <input type="text" name="tel"><br> 
		취미: <input type="text" name="hobby"><br>
		<input type="submit" value="회원가입" />
	</form>
</body>
</html>
```
## memReg 서블릿

```java


import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class MemRegServlet
 */
@WebServlet("/memReg")
public class MemRegServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    /**
     * @see HttpServlet#HttpServlet()
     */
    public MemRegServlet() {
        super();
        // TODO Auto-generated constructor stub
    }

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		request.setCharacterEncoding("UTF-8");
		response.setContentType("text/html;charset=euc-kr");
		PrintWriter out = response.getWriter();
		String name = request.getParameter("name");
		String addr = request.getParameter("addr");
		String tel = request.getParameter("tel");
		String hobby = request.getParameter("hobby");
		out.println("이름 = "+name+"<br>");
		out.println("주소 = "+addr+"<br>");
		out.println("전화번호 = "+tel+"<br>");
		out.println("취미 = "+hobby+"<br>");
	}

}
```

## include 지시어
```java

<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<%@ include file="header.jsp" %>
<html>
<head>
<meta charset="UTF-8">
<title>include 테스트</title>
</head>
<body>
<h1>includeTest.jsp 파일 입니다.</h1>
<%@ include file="footer.jsp" %>

</body>
</html>
```
## header.jsp
```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<h3>header.jsp 파일의 내용이 들어가는 곳 입니다.</h3>
<hr>
```

## footer.jsp
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<hr>    
<h3>footer.jsp 파일의 내용이 들어가는 곳 입니다.</h3>
```

## Declaration(선언문)
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h1><%=getStr()%></h1>
	<%!private String getStr() {
		str += "테스트 입니다.";
		return str;
	}
	
	private String str="선언문 ";
	%>

</body>
</html>
```

## scriptlet(명령 단위)
```
<%@page import="java.util.Calendar"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<%
Calendar c = Calendar.getInstance();
int hour=c.get(Calendar.HOUR_OF_DAY);
int minute=c.get(Calendar.MINUTE);
int second=c.get(Calendar.SECOND);
%>
<html>
<head>
<meta charset="UTF-8">
<title>scriptlet Test</title>
</head>
<body>
<h1>현재 시간은<%=hour %>시 <%=minute %>분 <%=second %>초 입니다.</h1>
</body>
</html>
```

## Expression(표현식)
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<%!public int sum() {
		int total = 0;
		for (int i=1; i<=100; i++) {
			total += i;
		}
		return total;
	}
%>
<%
String str="1부터 100까지의 합";
%>
<html>
<head>
<meta charset="UTF-8">
<title>Expression Test</title>
</head>
<body>
<h2><%=str %>은<b><%=sum() %></b>입니다.</h2>
<br>
<h2><%=str %>에 3을 곱하면<b><%=sum()*3 %></b>이 됩니다.</h2>
<br>
<h2><%=str %>을 1000으로 나누면<b><%=sum() / 1000. %></b>이 됩니다.</h2>
</body>
</html>
```

## request 클릭
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Request Test</title>
<style>
h1 , #commandCell {
     text-align: center;
}

table {
	margin: auto;
	width: 400px;
	border: 1px solid black;
	
}
</style>
</head>
<body>
	<h1>Request EX</h1>
	<form action="request1.jsp" method="post">
		<table>
			<tr>
				<td><label for="name">이름: </label></td>
				<td><input type="text" name="name" id="name"></td>
			</tr>
			<tr>
				<td><label for="gender">성별: </label></td>
				<td>남<input type="radio" name="gender" value="male" id="gender">여<input
					type="radio" name="gender" value="female" id="gender"></td>
			</tr>
			<tr>
				<td><label for="hobby">취미: </label></td>
				<td>독서<input type="checkbox" name="hobby" value="독서" id="hobby">
					게임<input type="checkbox" name="hobby" value="게임" id="hobby">
					tv시청<input type="checkbox" name="hobby" value="tv시청" id="hobby">
					축구<input type="checkbox" name="hobby" value="축구" id="hobby">
					기타<input type="checkbox" name="hobby" value="기타" id="hobby">
				</td>
			</tr>
			<tr>
				<td colspan="2" id="commandCell"><input type="submit"
					value="전송"></td>
			</tr>
		</table>
	</form>
</body>
</html>
```
## request 결과
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<%request.setCharacterEncoding("UTF-8"); %>
<html>
<head>
<meta charset="UTF-8">
<title>Request Test</title>
<style>
h1 , #commandCell {
     text-align: center;
}

table {
	margin: auto;
	width: 400px;
	border: 1px solid red;
	
}
</style>
</head>
<body>
	<h1>Request EX</h1>
	
		<table>
			<tr>
				<td>이름: </td>
				<td><%=request.getParameter("name") %></td>
			</tr>
			<tr>
				<td>성별: </td>
				<td><%if(request.getParameter("gender").equals("male")) {
					%>남자
				<%} else {%>여자<%} %>
				</td>
			</tr>
			<tr>
				<td>취미: </td>
				<td>
				<%String[] hobby = request.getParameterValues("hobby");
				for(int i=0; i<hobby.length; i++) {
				%>
				<%=hobby[i] %>&nbsp;&nbsp;
				<%} %>
				</td>
			</tr>
			
		</table>
	
</body>
</html>
```
