---
enable html: true
---
# spring的xml配置文件实现数据库用户名和密码加密

    很多项目的数据库配置信息都放在了xml配置文件中，当容器加载项目的时候就会将配置信息加载内存中，但很多时候需要将数据库的用户名和密码进行加密处理

1、编写EncrypPropertyPlaceholderConfigurer使其继承PropertyPlaceholderConfigurer类

```
public class EncrypPropertyPlaceholderConfigurer extends PropertyPlaceholderConfigurer {    private Logger log= LoggerFactory.getLogger(EncrypPropertyPlaceholderConfigurer.class);    @Override
  protected void processProperties(
  ConfigurableListableBeanFactory beanFactoryToProcess, Properties props) throws BeansException {
  String username = props.getProperty("jdbc.username");
  //用户名加密
  if (username != null) {
  props.setProperty("jdbc.username", AESUtil.decAes(username));//解密
  }
  //密码加密
  String password = props.getProperty("jdbc.password");
 if (password != null) {
  props.setProperty("jdbc.password", AESUtil.decAes(password));//解密
  }
  super.processProperties(beanFactoryToProcess, props);
  }     
  }
```

    上面代码的大致思路就是获取配置文件中的jdbc.username和jdbc.password对应的信息，因为用户名和密码都是经过加密后处理的，所以将其解密后将其放入Properties 对应的对象中，类似一将信息放入一个modle对象的属性中

2、修改对应的xml配置
     将之前xml配置文件中的用户名和密码对应的value如下

     <property name="username" value="${jdbc.username}"/>
     <property name="password" value="${jdbc.password}"/>

然后在配置数据库连接的bean的挨着的上面加上另外一个bean，代码如下：

     <bean id="propertyConfigurer"
      class="com.heji.util.EncrypPropertyPlaceholderConfigurer">
     <property name="locations">
     <list>
     <value>classpath:jdbc.properties</value>
     </list>
     </property> </bean>

上面bean中的class就是第一步中编写的类，classpath:jdbc.properties 是在resource目录下存放数据库连接的配置文件jdbc.properties，其大致思路就是在加载xml配置文件过程中首先获取bean ： propertyConfigurer 然后该bean加载jdbc.properties配置文件中的配置并调用类EncrypPropertyPlaceholderConfigurer 将用户名和密码解密然后放入Properties 对象中，紧接着调用下一个bean，将之前获取的到的用户名和密码的明文塞入到对应的username和password对应的value中

该方法大致实现思路：
1、在resource目录下建立配置文件jdbc.properties 并将其数据库的配置信息写入其中。
2、编写数据库用户名和密码解密的类并实现PropertyPlaceholderConfigurer类，在该类中读取jdbc.properties配置中的信息，并将其解密后的明文信息放入Properties 对应的对象中（如第一步代码所示）
3、编写xml文件（具体如第二步所示）

