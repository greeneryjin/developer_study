
#### forward

```java

@WebServlet("/one")
public class ServletOne extends HttpServlet {
	
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println("ServletOne doGet()");
		process(request, response);
	}
	
	
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println("ServletOne doPost()");
		process(request, response);
	}
	
	protected void process(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		//요청 객체에 새로운 데이터 서버단에서 저장
		//forward 방식 
		request.setAttribute("eduName", "우리 FISA");
		//request.getRequestDispatcher("two").forward(request, response);
	}
}

@WebServlet("/two")
public class ServletTwo extends HttpServlet {
	private static final long serialVersionUID = 1L;

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println("servlet two do get");
		process(request, response);
	}


	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println("servlet two do post");
		process(request, response);
	}
	
	protected void process(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html;charset=utf-8");
	 	PrintWriter out = response.getWriter();
	 	out.println("안녕");
	 	out.println("<font color='red'>");
	 	out.println(request.getAttribute("eduName"));
	 	out.println("</font>");
	}
}
```

요청 url 프로세스

client -> html -> /one -> /one

내부적으로 페이지를 이동해주고 client에게 보여줌 


#### redirect 

```java

@WebServlet("/one")
public class ServletOne extends HttpServlet {
	
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println("ServletOne doGet()");
		process(request, response);
	}
	
	
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println("ServletOne doPost()");
		process(request, response);
	}
	
	protected void process(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    //redirect
		request.setAttribute("eduName", "우리 FISA");
		response.sendRedirect("two");
	}
}

@WebServlet("/two")
public class ServletTwo extends HttpServlet {
	private static final long serialVersionUID = 1L;

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println("servlet two do get");
		process(request, response);
	}


	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println("servlet two do post");
		process(request, response);
	}
	
	protected void process(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html;charset=utf-8");
	 	PrintWriter out = response.getWriter();
	 	out.println("안녕");
	 	out.println("<font color='red'>");
	 	out.println(request.getAttribute("eduName"));
	 	out.println("</font>");
	}
}
```

요청 url 프로세스

client -> html -> /one -> /two

내부적으로 페이지를 생성해주고 client에게 다시 전송 
