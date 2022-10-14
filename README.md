1b): login 

<html>
 <head>
 <title>TODO supply a title</title>
 <meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 </head>
 <body>
 <form method="post" action="login">
 Enter name: <input type="text" name="txtid"><br><br>
 Enter password:<input type="password" name="pass"><br><br>
 <input type="reset">
 <input type="submit" value="click to login"> 
 </form>
 </body>
</html>


Code:
protected void doPost(HttpServletRequest request, HttpServletResponse 
response)
 throws ServletException, IOException
 {
 response.setContentType("text/html;charset=UTF-8");
 PrintWriter out = response.getWriter();
 out.println("<html><head><title>Servlet LoginServlet</title></head>");
 String uname = request.getParameter("txtId");
 String upass = request.getParameter("txtPass"); 
 if(uname.equals("admin") && upass.equals("12345"))
 {
 out.println("<body bgcolor=orange >");
 out.println("<h1> Hello !!! "+uname+"</h1>");
 }
 else
 {
 out.println("<body bgcolor=green >");
 out.println("<h1> Login Fail !!! </h1>"); 
 }
 }
}
  
  1c:Registration
<html>
 <head>
 <title>TODO supply a title</title>
 <meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 </head>
 <body>
 <form method="post" action="registration">
 Enter username: <input type="text" name="u"><br><br>
 Enter password: <input type="text" name="p"><br><br>
 Enter Email: <input type="text" name="e"><br><br>
 Enter country: <input type="text" name="c"><br><br>
 <input type="reset">
 <input type="submit" value="REGISTER">
 </form>
 </body>
</html>
Code:
protected void doPost(HttpServletRequest request, HttpServletResponse response)
 throws ServletException, IOException 
 {
 response.setContentType("text/html;charset=UTF-8");
 PrintWriter out = response.getWriter();
 String id = request.getParameter("u");
 String ps = request.getParameter("p");
 String em = request.getParameter("e");
 String co = request.getParameter("c");
 try{
 
 Class.forName("com.mysql.jdbc.Driver");
 Connection con 
=DriverManager.getConnection("jdbc:mysql://localhost:3306/ROOT","root","root");
 PreparedStatement pst = con.prepareStatement("insert into ni values(?,?,?,?)");
 pst.setString(1,id);
 pst.setString(2,ps);
 pst.setString(3,em);
 pst.setString(4,co);
 int row = pst.executeUpdate();
 out.println(+row+ " Row Inserted Succesfullyyyyy.........");
 }
 catch(Exception e)
 {
 e.printStackTrace();
}
}

 
 2b: Cookie
 
<html>
 <head>
 <title>TODO supply a title</title>
 <meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 </head>
 <body>
 <form method="post" action="test">
 <input type="submit" value="Count">
 </form>
 </body>
</html>
 
Code:
 
protected void doPost(HttpServletRequest request, HttpServletResponse 
response)
 throws ServletException, IOException
 {
 response.setContentType("text/html;charset=UTF-8");
 PrintWriter out = response.getWriter();
 String s=Integer.toString(count);
 Cookie ck=new Cookie("visit",s);
 request.addCookie(ck);
 int n=Integer.parseInt(ck.getValue());
 if(n==1)
 {
 out.println("Welcome...You visited first time...");
 }
 else
 {
 out.println("You visited "+n+" times");
 }
 count++;
 out.close();
 }
 }
 
 
 2c: Session
 
<html>
 <head>
 <title>TODO supply a title</title>
 <meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 </head>
 <body>
 <form method="post" action="test">
 <input type="submit" value="Count">
 </form>
 </body>
</html>
 
 
public void doPost(HttpServletRequest request, HttpServletResponse response)
 throws ServletException, IOException
 {
 response.setContentType("text/html;charset=UTF-8");
 PrintWriter out = response.getWriter();
 HttpSession hs=request.getSession(true);
 out.println("<h1>You Logged in at "+new java.util.Date(hs.getCreationTime())+"</h1>"); 
 out.println("<h1>Your Session ID "+hs.getId()+"</h1>");
 out.println("<body bgcolor=pink>");
 if(hs.isNew())
 {
 out.println("<h2>Welcome... You visited first time...</h2>");
 }
 else
 {
 out.println("<h2>You visited "+count+" times</h2>");
 }
 count++;
 out.close();
}
}
 
 
 3a: upload
 
<html>
 <head>
 <title>TODO supply a title</title>
 <meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 </head>
 <body>
 <form method="post" action="UploadServlet" enctype="multipart/form-data">
 <b>Select File:</b>
 <input type="file" name="fname">
 <br>
 <input type="submit" value="upload">
 </form>
 </body>
</html>
 
Code:
 
public void doPost(HttpServletRequest req, HttpServletResponse res)throws
ServletException, IOException
{
res.setContentType("text/html");
PrintWriter pw = res.getWriter();
MultipartRequest m=new MultipartRequest(req,"D:/abcd");
pw.print("successfully uploaded");
pw.close();
}
}
 
Download
 
<html>
 <head>
 <title>TODO supply a title</title>
 <meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 </head>
 <body> 
 <form method="post" action="DownloadServlet" enctype="multipart/form-data">
 <b>Download File:</b>
 <input type="submit" value="Download">
 </form>
</body>
</html>
 
 
Code:
 
protected void doPost(HttpServletRequest request, HttpServletResponse response)
 throws ServletException, IOException {
 response.setContentType("text/html;charset=UTF-8");
 PrintWriter out = response.getWriter();
 String filename = "EJB.txt";
 String filepath = "D:\\";
 response.setContentType("APPLICATION/OCTET-STREAM");
 FileInputStream f1 = new FileInputStream(filepath + filename);
 int i;
 while ((i=f1.read())!= -1)
 {
 out.write(i);
 }
 f1.close();
 out.close();
 }
}
 
 3b) Quiz
 
<html>
 <head>
 <title>TODO supply a title</title>
 <meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 </head>
 <body>
<h1>
Welcome TO Quiz Servlet....
</h1>
<h1>
<a href="newjsp.jsp"> CLICK TO START QUIZ</a>
</h1>
 </body>
</html>
 
new.jsp
<%@page contentType="text/html" pageEncoding="UTF-8"%>
<html>
<body>
<form method="post" action="Question">
<head>
<h1><b> Check Your Knowledge......... </b></h1>
</head>
<br>
<b> What JSP Stands For ? </B><br>
<input type="radio" name="a" value="J1">
Java Server Pages<br>
<input type="radio" name="a" value="J2">
Java Server Programming <br>
<input type="radio" name="a" value="J3">
Java Service Package <br>
<input type="radio" name="a" value="J4">
Java Server Beans <br>
<b> What EJB Stands For ? </b><br>
<input type="radio" name="b" value="E1">
Enter Java Beans <br>
<input type="radio" name="b" value="E2">
EnterPrise Java Beans <br>
<input type="radio" name="b" value="E3">
Enter Java Bean <br>
<input type="radio" name="b" value="E4">
EnterPrise Java Bean <br>
<b> What JPA Stands For ? </b><br>
<input type="radio" name="c" value="P1">
Java Permanent Analysis <br>
<input type="radio" name="c" value="P2">
Java Persistence API <br>
<input type="radio" name="c" value="P3">
Java Programming API <br>
<input type="radio" name="c" value="P4">
Java Paradise Algorithm <br>
<input type="Submit" value="Submit">
</form>
</body>
</html>
 
Question.java
 
protected void doPost(HttpServletRequest request, HttpServletResponse response)
 throws ServletException, IOException
 {
 response.setContentType("text/html;charset=UTF-8");
 PrintWriter out = response.getWriter();
 int Correct = 0;
int Incorrect = 0;
String s1= request.getParameter("a");
String s2= request.getParameter("b");
String s3= request.getParameter("c");
if(s1.equals("J1"))
{
Correct++;
}
else
{
Incorrect++;
}
if(s2.equals("E4"))
{
Correct++;
}
 }
}
 
 
 6a) Currency
 
<html>
 <head>
 <title>TODO supply a title</title>
 <meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 </head>
 <body>
 <form action="Test" method="post">
 Enter amount in rupees:<input type="text" name="a" value="" size="10">
 <input type="submit" value="Convert">
 </form>
 </body>
</html>
 
Code:
 
<%@page contentType="text/html" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
 <title>JSP Page</title>
 </head>
 <body>
 <h1>Hello World!</h1>
 <%@page import="ejb.dollar"%>
 <%
 int rs=Integer.parseInt(request.getParameter("a"));
 dollar d=new dollar();
 double dl=d.Convert(rs);
 out.println("Amount in dollars="+dl);
 %>
 </body>
</html>
  
Dollar.java
  
public class dollar {
 public Double Convert(int rs)
 {
 double d=rs/77.69;
 return d;
 }
}
 
  2(A). Using Request Dispatcher Interface create a Servlet which will validate the password 
entered by the user, if the user has entered "Servlet" as password, then he will be forwarded 
to Welcome Servlet else the user will stay on the index.html page and an error message will 
be displayed.
PROGRAM:-
index.html:
<html>
 <body>
 <form method="get" action="rd11">
 <b>Username</b>
 <input type="text" name="a" value="" size="10">
 <br>
 <b>Password</b>
 <input type="password" name="b" value="" size="10">
 <br>
 <input type="submit" value="Login">
 </form>
 </body>
</html>
newhtm1.html:
<html>
 <head>
 <title>TODO supply a title</title>
 <meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 </head>
 <body>
 Login Fail......
 </body>
</html>
rd11.java:
import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException
  import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
public class rd11 extends HttpServlet {
 protected void processRequest(HttpServletRequest request, HttpServletResponse response)
 throws ServletException, IOException {
 response.setContentType("text/html;charset=UTF-8");
 try (PrintWriter out = response.getWriter()) {
 
 if( request.getParameter("b").equals("servlet"))
 {
 RequestDispatcher rd = request.getRequestDispatcher("wlcm1");
 rd.forward(request, response);
 }
 else{
 RequestDispatcher rd = request.getRequestDispatcher("newhtm1.html");
 rd.forward(request, response);
 
 }
 }
 }
}
wlcm.java:
import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
public class wlcm1 extends HttpServlet {
 protected void processRequest(HttpServletRequest request, HttpServletResponse response)
 throws ServletException, IOException {
 response.setContentType("text/html;charset=UTF-8");
 try (PrintWriter out = response.getWriter()) {
 out.println("<h1>Welcome Servlet </h1>");
 }
 }
}

  
 4(A). Develop a simple JSP application to display values obtained from the use of intrinsic 
objects of various types.
PROGRAM:-
test.jsp:
<%@page contentType="text/html" pageEncoding="UTF-8"%>
<html>
<head>
<title>JSP Page</title>
</head>
<body>
<h1>Use of Intrinsic Objects in JSP</h1>
<h1>Request Object </h1>
Query String <%=request.getQueryString() %><br> Context Path <%=request.getContextPath() 
%><br> Remote Host <%=request.getRemoteHost() %><br>
<h1>Response Object </h1>
Character Encoding Type <%=response.getCharacterEncoding() %><br> Content Type
<%=response.getContentType() %><br>
Locale <%=response.getLocale() %><br>
<h1>Session Object </h1>
ID <%=session.getId() %><br>
Creation Time <%=new java.util.Date(session.getCreationTime()) %><br>
Last Access Time<%=new java.util.Date(session.getLastAccessedTime()) %><br>
</body>
</html>
 
 4(B). Develop a simple JSP application to pass values from one page to another with 
validations. (Name-txt, age-txt, hobbies-checkbox, email-txt, gender-radio button).
PROGRAM:-
index.html:
<html>
<head>
<title>User Information Paage</title>
</head>
<body><form action="Validate.jsp">
Enter Your Name<input type="text" name="name" ><br> Enter Your Age<input type="text" 
name="age" ><br>
Select Hobbies
<input type="checkbox" name="hob" value="Singing">Singing
<input type="checkbox" name="hob" value="Reading">Reading Books
<input type="checkbox" name="hob" value="Football">Playing Football<br> Enter E-mail<input 
type="text" name="email" ><br>
Select Gender <input type="radio" name="gender" value="male">Male
<input type="radio" name="gender" value="female">Female
<input type="radio" name="gender" value="other">Other<br>
<input type="hidden" name="error" value="">
<input type="submit" value="Submit Form">
</form>
</body>
</html>
Validate.jsp:
<%@page contentType="text/html" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html><head><title>JSP Page</title></head>
<body><h1>Validation Page</h1>
<jsp:useBean id="obj" scope="request" class="mypack.CheckerBean">
<jsp:setProperty name="obj" property="*"/>
</jsp:useBean>
<%if(obj.valid())
{%>
<jsp:forward page="successful.jsp"/>
<% }
else{%>
{%><jsp:include page="index.html"/>
<%}%>
<%=obj.getError() %>
</body>

 CheckerBean.java:
package mypack;
public class CheckerBean {
 private String name, age, hob, email, gender, error; public CheckerBean(){ error="";
}
public void setName(String n){ name=n;
}
public void setAge(String a){ age=a;
}
public void setHob(String h){ hob=h;
} public void setEmail(String e){ email=e;
} public void setGender(String g){ gender=g;
} public void setError(String e){ error=e;
} public String getName(){ return name;
} public String getAge(){ return age;
} public String getHob(){ return hob;
} public String getEmail(){ return email;
} public String getGender(){ return gender;
} public String getError(){ return error;
} public booleanvalid(){
boolean res=true; if(name.trim().equals(""))
{error+="<br>Enter First Name";res=false; if(age.length() > 2 ) {error+="<br>Age Invalid";
}res=false;} return res;
}
}
 
 4(C). Create a registration and login JSP application to register and authenticate the user 
based on username and password using JDBC.
PROGRAM:-
Register.html:
<html>
<head><title>New User Registration Page</title>
</head>
<body>
<form action="Register.jsp" >
<h1> New User Registration Page</h1>
Enter User Name <input type="text" name="txtName" ><br> Enter Password <input 
type="password" name="txtPass1" ><br>
Re-Enter Password<input type="password" name="txtPass2" ><br> Enter Email<input 
type="text" name="txtEmail" ><br>
Enter Country Name <input type="text" name="txtCon" ><br>
<input type="reset" ><input type="submit" value="REGISTER" >
</form>
</body>
</html>
 
Register.jsp:
<%@page contentType="text/html" import="java.sql.*"%>
<html><body>
<h1>Registration JSP Page</h1>
<% String uname=request.getParameter("txtName"); String pass1 = 
request.getParameter("txtPass1"); String pass2 = request.getParameter("txtPass2"); String 
email = request.getParameter("txtEmail"); String ctry = request.getParameter("txtCon"); 
if(pass1.equals(pass2)){
try{ Class.forName("com.mysql.jdbc.Driver");
Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/logindb"); 
PreparedStatement stmt = con.prepareStatement("insert into user values (?,?,?,?)"); 
stmt.setString(1, uname); stmt.setString(2, pass1);
stmt.setString(3, email); stmt.setString(4, ctry); int row = stmt.executeUpdate();
if(row==1) { out.println("Registration Successful"); } else {
out.println("Registration FFFFFAAAIIILLLL !!!!");
%><jsp:include page="Register.html" ></jsp:include>
<%
}
}catch(Exception e){out.println(e);}
}
else
{
   out.println("<h1>Password Mismatch</h1>"); %>
<jsp:include page="Register.html" ></jsp:include>
<% }
%>
</body></html>
Login.html:
<html>
<body>
<h1>Login Page</h1>
<form action="Login.jsp" >
Enter User Name <input type="text" name="txtName" ><br> Enter Password <input 
type="password" name="txtPass" ><br>
<input type="reset" ><input type="submit" value="~~~LOGIN~~" >
</form>
</body>
</html>
 
Login.jsp:
<%@page contentType="text/html" import="java.sql.*"%>
<html><body>
<h1>Registration JSP Page</h1>
<%
String uname=request.getParameter("txtName"); String pass = 
request.getParameter("txtPass"); try{
Class.forName("com.mysql.jdbc.Driver");
Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/logindb"); 
PreparedStatement stmt = con.prepareStatement("select password from user where 
username=?"); stmt.setString(1, uname);
ResultSet rs = stmt.executeQuery(); if(rs.next()){ if(pass.equals(rs.getString(1)))
{
out.println("<h1>~~~ LOGIN SUCCESSFULLL ~~~ </h1>");
}
}
else{
out.println("<h1>User Name not exist !!!!!</h1>");
%>
<jsp:include page="Register.html" ></jsp:include>
<%
}
}catch(Exception e){out.println(e);}
%>
</body>
 </html>
 
 5(A). Create an html page with fields, eno, name, age, desg, salary. Now on submit this data 
to a JSP page which will update the employee table of database with matching eno.
 
 index.html:
<html>
<body>
<form action="UpdateEmp.jsp" >
Enter Employee Number<input type="text" name="txtEno" ><br>
Enter Name<input type="text" name="txtName" ><br>
Enter age<input type="text" name="txtAge" ><br>
Enter Salary<input type="text" name="txtSal" ><br>
<input type="reset" ><input type="submit">
</form>
</body>
</html>
 
UpdateEmp.jsp:
<%@page contentType="text/html" import="java.sql.*" %>
<html>
<body>
<h1>Employee Record Update</h1>
 <%
String eno=request.getParameter("txtEno");
String name=request.getParameter("txtName");
String age = request.getParameter("txtAge");
String sal = request.getParameter("txtSal");
try{ Class.forName("com.mysql.jdbc.Driver");
Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/emdb"); 
PreparedStatement stmt = con.prepareStatement("select * from emp where empid=?"); 
stmt.setString(1, eno);
ResultSet rs = stmt.executeQuery(); if(rs.next()){
out.println("<h1>~~~ Employee "+name+" Exist ~~~ </h1>");
PreparedStatement pst1= con.prepareStatement("update emp set salary=? where empid=?"); 
PreparedStatement pst2= con.prepareStatement("update emp set age=? where empid=?"); 
pst1.setString(1, sal); pst1.setString(2, eno);
pst2.setString(1, age); pst2.setString(2, eno); pst1.executeUpdate(); pst2.executeUpdate();
}
else{
out.println("<h1>Employee Record not exist !!!!!</h1>");
}
}catch(Exception e){out.println(e);}
%>
</body>
</html>
 
6(B). Develop a Simple Room Reservation System Application Using EJB.
 
 index.html:
<html>
<head>
<title>Simple Room Reservation System Application</title>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>
<form action="RBServlet" > Select a room Type
<input type="radio" name="txtType" value="Deluxe">Deluxe
<input type="radio" name="txtType" value="Super Deluxe">Super Deluxe
<input type="radio" name="txtType" value="Suit">Suit<br> Enter Your Name<input type="text" 
name="txtCust" ><br> Enter Mobile No.<input type="text" name="txtMob" ><br>
<input type="reset" ><input type="submit" value="Book Room">
</form>
</body>
</html>
 
RBServlet.java:
package mypack;
import java.io.IOException; import java.io.PrintWriter;
import javax.servlet.ServletException; 
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.ejb.EJB;
import mybeans.RRBean;
public class RBServlet extends HttpServlet { @EJB RRBean obj;
protected void processRequest(HttpServletRequest request, HttpServletResponse response) 
throws ServletException, IOException {
response.setContentType("text/html;charset=UTF-8"); PrintWriter out = response.getWriter();
String rt=request.getParameter("txtType"); String cn=request.getParameter("txtCust"); String 
cm=request.getParameter("txtMob"); String msg = obj.roombook(rt, cn, cm); out.println(msg);
}
}
 
RRBean.java:
package mybeans;
import javax.ejb.Stateless; import java.sql.*; @Stateless
public class RRBean { public RRBean(){}
public String roombook(String rt, String cn, String cm){ String msg="";
try{
Class.forName("com.mysql.jdbc.Driver");
 Connection con =
DriverManager.getConnection("jdbc:mysql://localhost:3306/rrdb","root","sk"); String 
query="select * from roombook where RoomType=? and status='Not Booked'"; 
PreparedStatement pst = con.prepareStatement(query);
pst.setString(1,rt);
ResultSet rs= pst.executeQuery(); if(rs.next()){
String rno=rs.getString(1);
PreparedStatement stm1 = con.prepareStatement("update roombook set cust=? where 
RoomId=? ");
PreparedStatement stm2 = con.prepareStatement("update roombook set mob=? where 
RoomId=? ");
PreparedStatement stm3 = con.prepareStatement("update roombook set status=? where 
RoomId=? ");
stm1.setString(1,cn); stm1.setString(2,rno); stm2.setString(1,cm); stm2.setString(2,rno); 
stm3.setString(1, "Booked"); stm3.setString(2,rno); stm1.executeUpdate(); 
stm2.executeUpdate(); stm3.executeUpdate();
msg = "Room "+rno+ " Booked <br> Charges = "+rs.getString(3);
}
else
{
msg = "Room "+rt+ " currently Not available";
}
catch(ClassNotFoundException | SQLException e){msg=""+e;} return msg;
}
}
