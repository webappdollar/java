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
  
  
  
