---
enable html: true
---
# **SpringMVC设计思路**

## 1、读取配置文件

SpringMVC本质上还是一个servlet，这个servlet继承自HttpServlet。


## 2、初始化阶段
在前面我们提到DispatcherServlet的initStrategies方法会初始化9大组件，但是这里将实现一些SpringMVC的最基本的组件而不是全部，按顺序包括：

加载配置文件
扫描用户配置下面所有的类
拿到扫描的类，通过反射机制，实例化，并且放到 ioc 容器中（Map的键值对beanName-bean）beanName默认是是字母小写
初始化HandlerMapping，这里其实就是把 url 和method对应起来放在一个k-v的map中，在运行阶段取出

## 3、运行阶段
每一次请求将会调用doGet或者doPost方法，所以统一运行阶段都放在doDispatch（）方法处理，他会根据 url 请求去HandlerMapping中匹配 到对应的Method，然后利用反射机制调用Controller中的url对应的方法，并得到结果返回。
1、异常拦截
2、获取请求传入的参数并处理参数
3、通过初始化好的HandlerMapping中拿出url对应的方法名，反射调用


