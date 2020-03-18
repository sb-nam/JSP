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
## 속성과 관련된 메소드
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Attribute Test Form</title>
</head>
<body>
	<h2>영역과 속성 테스트</h2>
	<form action="attributeTest.1jsp" method="post">
		<table border="1">
			<tr>
				<td colspan="2">Application 영역에 저장할 내용들</td>
			</tr>
			<tr>
				<td>이름</td>
				<td><input type="text" name="name"></td>
			</tr>
			<tr>
				<td>아이디</td>
				<td><input type="text" name="id"></td>
			</tr>
			<tr>
				<td colspan="2"><input type="submit" value="전송"></td>
			</tr>
		</table>
	</form>
</body>
</html>
```

## 속성 정의하고 사용하기1
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Attribute Test Form</title>
</head>
<body>
	<h2>영역과 속성 테스트</h2>
	<form action="attributeTest1.jsp" method="post">
		<table border="1">
			<tr>
				<td colspan="2">Application 영역에 저장할 내용들</td>
			</tr>
			<tr>
				<td>이름</td>
				<td><input type="text" name="name"></td>
			</tr>
			<tr>
				<td>아이디</td>
				<td><input type="text" name="id"></td>
			</tr>
			<tr>
				<td colspan="2"><input type="submit" value="전송"></td>
			</tr>
		</table>
	</form>
</body>
</html>
```

## 2
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>attribute Test</title>
</head>
<body>
	<h2>영역과 속성 테그</h2>
	<%
		request.setCharacterEncoding("UTF-8");
		String name = request.getParameter("name");
		String id = request.getParameter("id");
		if (name != null && id != null) {
			application.setAttribute("name", name);
			application.setAttribute("id", id);

		}
	%>
	<h3><%=name%>님 반갑습니다.<br><%=name%>님의 아이디는
		<%=id%>입니다.
	</h3>
	<form action="attributeTest2.jsp" method="post">
		<table border="1">
			<tr>
				<td colspan="2">Session 영역에 저장할 내용들</td>
			</tr>
			<tr>
				<td>e-mail 주소</td>
				<td><input type="text" name="email"></td>
			</tr>
			<tr>
				<td>집 주소</td>
				<td><input type="text" name="address"></td>
			</tr>
			<tr>
				<td>전화번호</td>
				<td><input type="text" name="tel"></td>
			</tr>
			<tr>
				<td colspan="2"><input type="submit" value="전송"></td>
		</table>
	</form>
</body>
</html>
```

## 3
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Attribute Test</title>
</head>
<body>
	<h2>영역과 속성 테스트</h2>
	<%
		request.setCharacterEncoding("UTF-8");
		String email = request.getParameter("email");
		String address = request.getParameter("address");
		String tel = request.getParameter("tel");
		session.setAttribute("email", email);
		session.setAttribute("address", address);
		session.setAttribute("tel", tel);

		String name = (String) application.getAttribute("name");
	%>
	<h3><%=name%>님의 정보가 모두 저장되었습니다.
	</h3>
	<a href="attributeTest3.jsp">확인하러 가기</a>
</body>
</html>
```
## 4
```
<%@page import="java.util.Enumeration"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Attribute Test</title>
</head>
<body>
	<h2>영역과 속성 테스트</h2>
	<table border="1">
		<tr>
			<td colspan="2">Application 영역에 저장된 내용들</td>
		</tr>
		<tr>
			<td>이름</td>
			<td><%=application.getAttribute("name")%></td>
		</tr>
		<tr>
			<td>아이디</td>
			<td><%=application.getAttribute("id")%></td>
		</tr>
	</table>
	<br>
	<table border="1">
		<tr>
			<td>Session 영역에 저장된 내용들</td>
		</tr>

		<%
			Enumeration e = session.getAttributeNames();
			while (e.hasMoreElements()) {
				String attributeName = (String) e.nextElement();
				String attributeValue = (String) session.getAttribute(attributeName);
		%>
		<tr>
			<td><%=attributeName%></td>
			<td><%=attributeValue%></td>
		</tr>
		<%
			}
		%>
	</table>
</body>
</html>
```
## 자바빈 사용법1
```
package test;

public class BeanTest2 {

	private String name;
	private String addr;
	private String email;
	private String birthday;
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getAddr() {
		return addr;
	}
	public void setAddr(String addr) {
		this.addr = addr;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public String getBirthday() {
		return birthday;
	}
	public void setBirthday(String birthday) {
		this.birthday = birthday;
	}
	
}
```
##  자바빈 사용법2
```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style type="text/css">
</style>
</head>
<body>
	<section id="formArea">
		<h1>property="*"테스트</h1>
		<form action="beanTest4.jsp" method="post">
			<fieldset>
				<label for="name">이름 : </label><input type="text" name="name"
					id="name" /><br> <label for="addr">주소 : </label><input
					type="text" name="addr" id="addr" /><br> <label for="email">이메일
					: </label><input type="text" name="email" id="email" /><br> <label
					for="birthday">생년월일 : </label><input type="text" name="birthday"
					id="birthday" /><br> <input type="submit" value="전송">
			</fieldset>
		</form>
	</section>
</body>
</html>
```
## 자바빈 사용법3
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
    request.setCharacterEncoding("UTF-8");
%>
<jsp:useBean id="beantest" class="test.BeanTest2" scope="page"/>
<jsp:setProperty property="*" name="beantest"/>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>JavaBean Test</title>
</head>
<body>
<h1>자바빈 속성 값 출력</h1>
<b>이름 : </b><%=beantest.getName() %><br>
<b>주소 : </b><%=beantest.getAddr() %><br>
<b>이메일 : </b><%=beantest.getEmail() %><br>
<b>생년월일 : </b><%=beantest.getBirthday() %><br>
</body>
</html>
```

## 자바빈 회원 가입 페이지1
```
package join;

public class JoinBean {

	private String id;
	private String pass;
	private String name;
	private int sex;
	private int age;
	private String email;
	public String getId() {
		return id;
	}
	public void setId(String id) {
		this.id = id;
	}
	public String getPass() {
		return pass;
	}
	public void setPass(String pass) {
		this.pass = pass;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getSex() {
		return sex;
	}
	public void setSex(int sex) {
		this.sex = sex;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	
	
}
```
## 자바빈 회원 가입 페이지2
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>회원 가입 폼</title>
<style type="text/css">
#formArea {
	margin: auto;
	width: 400px;
	border: 1px solid black;
	text-align: center;
}

h1 {
	text-align: center;
}

table {
	width: 300px;
	margin: auto;
	text-align: center;
}
</style>
</head>
<body>
	<section id="formArea">
		<form action="join.jsp" method="post">
			<table>
				<tr>
					<td><label for="id">아이디 : </label></td>
					<td><input type="text" name="id" id="id"></td>
				</tr>
				<tr>
					<td><label for="pass">비밀번호 : </label></td>
					<td><input type="text" name="pass" id="pass"></td>
				</tr>
				<tr>
					<td><label for="name">이름 : </label></td>
					<td><input type="text" name="name" id="name"></td>
				</tr>
				<tr>
					<td><label for="sex">성별 : </label></td>
					<td><input type="radio" name="sex" value="1" id="sex" checked>남</td>
					<td><input type="radio" name="sex" value="2" id="sex" checked>여</td>
				</tr>
				<tr>
					<td><label for="age">나이 : </label></td>
					<td><input type="text" name="age" id="age"></td>
				</tr>
				<tr>
					<td><label for="email">이메일 : </label></td>
					<td><input type="email" name="email" id="email"></td>
				</tr>
				<tr>
					<td colspan="2"><input type="submit" value="가입"> <input
						type="submit" value="다시 작성"></td>
				</tr>
			</table>
		</form>
	</section>
</body>
</html>
```

## 자바빈 회원가입 페이지3
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<%
	request.setCharacterEncoding("UTF-8");
%>
<jsp:useBean id="join" class="join.JoinBean" />
<jsp:setProperty property="*" name="join" />
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>회원가입 입력 정보 확인 페이지</title>
<style type="text/css">
table {
	width: 400px;
}

h1 {
	text-align: center;
}
</style>
</head>
<body>
	<table>
		<tr>
			<td><b>아이디 : </b></td>
			<td><jsp:getProperty property="id" name="join" /></td>
		</tr>
		<tr>
			<td><b>비밀번호 : </b></td>
			<td><jsp:getProperty property="pass" name="join" /></td>
		</tr>
		<tr>
			<td><b>이름 : </b></td>
			<td><jsp:getProperty property="name" name="join" /></td>
		</tr>
		<tr>
			<td><b>성별 : </b></td>
			<td><jsp:getProperty property="sex" name="join" /></td>
		</tr>
		<tr>
			<td><b>나이 : </b></td>
			<td><jsp:getProperty property="age" name="join" /></td>
		</tr>
		<tr>
			<td><b>이메일 : </b></td>
			<td><jsp:getProperty property="email" name="join" /></td>
		</tr>
	</table>
</body>
</html>
```
## session
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<%
	String name;
	if (session.getAttribute("name") != null) {
		name = (String) session.getAttribute("name");
	} else {
		name = "세션값 없음";
	}
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h2>세션 테스트</h2>
	<input type="button" onclick="location.href='sessionSet.jsp'"
		value="세션 값 저장">
	<input type="button" onclick="location.href='sessionDel.jsp'"
		value="세션 값 삭제">
	<input type="button" onclick="location.href='sessionReset.jsp'"
		value="세션 초기화">
	<h4><%=name%></h4>
</body>
</html>
```
## sessionSet
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<%
	session.setAttribute("name", "Session Test!");
%>
<script>
	location.href = "sessionTest.jsp";
</script>
```
## sessionDel
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<%
	session.removeAttribute("name");
%>
<script type="text/javascript">
	location.href = "sessionTest.jsp";
</script>
```
## sesstionInvalidate
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<%
	session.invalidate();
%>
<script>
	location.href = "sessionTest.jsp";
</script>
```
## session로그인
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style type="text/css">
#loginArea {
	width: 400px;
	margin: auto;
	border: 1px solid black;
}

table {
	margin: auto;
}

td {
	text-align: center;
}
</style>
</head>
<body>
	<section id="loginArea">
		<form action="sessionLogin2.jsp" method="post">
			<table>
				<tr>
					<td><label for="id">아이디: </label></td>
					<td><input type="text" name="id" id="id"></td>
				</tr>
				<tr>
					<td><label for="pw">비밀번호: </label></td>
					<td><input type="password" name="pw" id="pw"></td>
				</tr>
				<tr>
					<td colspan="2"><input type="submit" value="로그인"> <input
						type="reset" value="다시 작성"></td>
				</tr>
			</table>
		</form>
	</section>
</body>
</html>
```
## session로그인2
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<%
	session.setAttribute("id", request.getParameter("id"));
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h3>로그인 되었습니다.</h3>
	<h3>
		로그인 아이디:
		<%=(String) session.getAttribute("id")%></h3>
	<a href="sessionLogout.jsp">로그아웃</a>
</body>
</html>
```
## session로그아웃
```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<%
	session.removeAttribute("id");
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h3>로그아웃 되었습니다.</h3>
	<a href="sessionLogin1.jsp">로그인 페이지로 이동</a>
</body>
</html>
```
## JSP 와 DB연동
```
servers-톰캣-context.xml에 작성

<?xml version="1.0" encoding="UTF-8"?>
  
    <WatchedResource>WEB-INF/web.xml</WatchedResource>
    <WatchedResource>WEB-INF/tomcat-web.xml</WatchedResource>
    <WatchedResource>${catalina.base}/conf/web.xml</WatchedResource>

   
    	<Resource name="jdbc/OracleDB" auth="Container"
		type="javax.sql.DataSource" username="scott" password="tiger"
		driverClassName="oracle.jdbc.driver.OracleDriver"
		factory="org.apache.tomcat.dbcp.dbcp2.BasicDataSourceFactory"
		url="jdbc:oracle:thin:@localhost:1521:xe" maxActive="500"
		maxIdle="1000"
</Context>
```
## JSP 와 DB연동2
```
<%@page import="javax.sql.*"%>
<%@page import="javax.naming.*"%>
<%@page import="java.sql.*"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
Connection conn = null;
String sql = "INSERT INTO student(num,name) VALUES(7,'홍길동')";
Statement stmt = null;
try{
	Context init = new InitialContext();
	DataSource ds = (DataSource)init.lookup("java:comp/env/jdbc/OracleDB");
	conn = ds.getConnection();
	stmt = conn.createStatement();
	
	int result = stmt.executeUpdate(sql);
	if(result!=0) {
		out.println("<h3>레코드가 등록되었습니다.</h3>");
	}
}catch (Exception e) {
	out.println("<h3>레코드 등록에 실패 하였습니다.</h3>");
	e.printStackTrace();
}
finally {
	try{
		stmt.close();
		conn.close();
		
	} catch(Exception e) {
		e.printStackTrace();
	}
}
%>    
```
