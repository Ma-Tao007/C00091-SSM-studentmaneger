# 	基于SSM（非maven）的学生信息管理系统

@[TOC](	基于SSM（非maven）的学生信息管理系统)
# 项目简介
基于SSM（非maven）的学生信息管理系统；
功能简单，适合学习以及大作业等，jsp页面，form表单提交数据，拦截器处理用户未登录状态
管理员功能：登录注册，管理员管理，学生管理（增删改查）
使用MVC设计模式开发

 # 项目获取
> [源码获取地址](http://www.manoncode.cn/details?id=91)

 
# 开发环境

运行环境：推荐jdk1.8；
开发工具：eclipse以及idea（推荐）；
操作系统：windows 10 8G内存以上（其他windows以及macOS支持，但不推荐）；
浏览器：Firefox(推荐)、Google Chrome(推荐)、Edge;
数据库：MySQL8.0(推荐)及其他版本（支持，但容易异常尤其MySQL5.7（不含）以下版本）；
数据库可视化工具：Navicat Premium 15（推荐）以及其他Navicat版本
是否maven项目：否


 # 项目技术
 
后端：mysql、Spring、SpringMVC、Mybatis
前端：jsp

# 相关代码

 - TestInterceptor.java（拦截器）
 

```java
package ssm.interceptor;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;
import ssm.entity.Sysuser;

public class TestInterceptor implements HandlerInterceptor{
	@Override
	public boolean preHandle(HttpServletRequest request, 
			HttpServletResponse response, Object handler)
			throws Exception {
		response.setContentType("text/html;charset=utf-8");
		request.setCharacterEncoding("utf-8");
		String url = request.getRequestURI();
		if(url.equals("/sysuser/login")){
			return true;
		}
		if(url.equals("/sysuser/topPage")){
			return true;
		}
		if(url.equals("/sysuser/insert")){
			return true;
		}
		if(url.indexOf("/success")>0){
			return true;
		}HttpSession session=request.getSession();
		Sysuser user = (Sysuser) session.getAttribute("USER_SESSION");
		if(user!=null){
			return true;
		}
		
		request.setAttribute("msg","NO LOGIN");
		request.getRequestDispatcher("/WEB-INF/testSSM/login.jsp").forward(request, response);
		System.out.println("preHandle");
		return false;
	}
	
	@Override
	public void postHandle(HttpServletRequest request, 
			HttpServletResponse response, Object handler,
			ModelAndView modelAndView) throws Exception {
		System.out.println("postHandle");
	}
	@Override
	public void afterCompletion(HttpServletRequest request, 
			HttpServletResponse response, Object handler, Exception ex)
			throws Exception {
		System.out.println("afterHandle");
	}
}

```

 - login.jsp
 

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
欢迎使用学生信息管理系统
${msg}
	<form action="/sysuser/login" method="post">
		<table>
			<tr>
				<td>用户名</td>
				<td><input name="username" type="text" ></td>
			</tr>
			<tr>
				<td>密码</td>
				<td><input name="password" type="text" ></td>
			</tr>
		</table>
		<td>
		<input type="submit" value="登录">
		</td>	
	</form>

<button onClick="location.href='/sysuser/topPage?page=sysuser/add'">注册</button>
</body>

</html>
```

 # 运行截图
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/e9befab704994cdb99d7fe6ef06eed4d.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/5e55a2e181894d7a9d73905e04643891.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/d0aa395d57d74d80ab8b4f4db07e290b.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/cf92c820ed0042658e16ed38af77ccba.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/daab0a2ac8f14a4cbb728f2fe4228e7d.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/1ef9d613d32f4ccb94356c6466f5749b.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/0ca1f6ca46cb495bb990629eba0352ed.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/c8bb10a717b84206817a61f5cbf7b52d.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/5d1f68f19825417ca94ae00f5f98d545.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/02cbba02aa52481183df9a67e3d0e3bf.png#pic_center)
# 运行视频


[video(video-Tf2YRssx-1668042338699)(type-bilibili)(url-https://player.bilibili.com/player.html?aid=987431244)(image-https://img-blog.csdnimg.cn/img_convert/ab820ee5ab2a226489c38a1eb9dfd41d.jpeg)(title-【运行视频】（C00091）基于SSM（非maven）的学生信息管理系统)]

