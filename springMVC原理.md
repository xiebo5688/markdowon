---
enable html: true
---
# **springMVC原理**

![springMVC执行过程]($resource/springMVC.jpg)

1、用户发送请求到前端控制器DispatcherServlet

2、DispatcherServlet收到请求调用HandlerMapping处理映射器（map键值对）

3、处理映射器根据请求url找到具体的处理器，生成处理器对象及处理器拦截器（如有 则生成）一并返回给DispatcherServlet

4、DispatcherServlet通过HandlerAdapter 处理器适配器调用处理器Contorller

5、执行处理器Controller，也叫后端处理器

6、Controller执行完返回ModelAndView

7、HandlerAdapter将Controller执行结果ModelAndView返回给DispatcherServlet

8、DispatcherServlet将ModelAndView传给ViewReslover视图解析器

9、ViewReslover解析后返回具体View

10、DispatcherServlet对View进行渲染视图（即将模型数据填充至视图中）

11、DispatcherServlet响应用户

# springMVC九大组件
![springMVC九大组件]($resource/springMVC%E4%B9%9D%E5%A4%A7%E7%BB%84%E4%BB%B6.jpg)

