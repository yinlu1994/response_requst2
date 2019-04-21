# response_requst2
request 用户注册
# 案例二-完成用户注册操作
* 需求：在一个表单页面上填写用户数据，点击提交，将所有的数据提交到服务器上，通过java代码最终保存到数据库中
* 技术分析：
  * 表单
  * request
## request：请求
  * 作用：获取浏览器发送过来的数据
  * 组成部分：
    * 请求行 请求头 请求体
    * 请求行
    ```(java)
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// 获取请求方式
		String m = request.getMethod();
		System.out.println("方式："+m);
		//获取请求参数的字符串
		String uri = request.getRequestURI();
		String url = request.getRequestURL().toString();
		System.out.println("uri:"+uri);
		System.out.println("url:"+url);
		//获取请求参数的字符串
		String s = request.getQueryString();
		System.out.println("get请求参数："+s);
		//获取协议版本
		String p = request.getProtocol();
		System.out.println("协议："+p);
		//获取请求的IP（重要）
		String ip = request.getRemoteAddr();
		System.out.println("ip:"+ip);
		//获取项目名称（重要）
		String path = request.getContextPath();
		System.out.println("项目路径："+path);
	}
    ```
  * request获取请求参数
  ```（html）
  <a href = "/rr/Param?username=tom&password=123&hobby=drink&hobby=sleep">f_请求参数</a><br>
  ``` 
  ```(java)
  protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		//获取爱好，多个值
		String[] hobby = request.getParameterValues("hobby");
		System.out.println("hobby:"+Arrays.toString(hobby));
		//获取所有
		Map<String,String[]> map = request.getParameterMap();
		for(String key:map.keySet()) {
			System.out.println(key+"::"+Arrays.toString(map.get(key)));
		}
	}
  ```
  * request获取客户信息（解决乱码问题）
    * index.html
    ```(html)
    <a href = "/rr/form.html">提交表单</a><br>
    ```
    * (servlet)param2.java
    ```(java)
    	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		/*
		String name = request.getParameter("username");
		name=new String(name.getBytes("iso8859-1"),"utf-8");
		System.out.println("用户名："+name);
		String psw = request.getParameter("password");
		System.out.println("密码："+psw);*/
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		//doGet(request,response);
		//*
		request.setCharacterEncoding("utf-8");
		String name = request.getParameter("username");
		System.out.println("用户名："+name);
		String psw = request.getParameter("password");
		System.out.println("密码："+psw);
		// */
		
	}
    ```
    * (form提交用户信息)form.html
    ```(html)
    <body>
	<form action="/rr/param" method="post">
		用户名：<input name="username"><br>
		密码：<input name="password"><br>
		<input type="submit">
	</form>
    </body>
    ```
