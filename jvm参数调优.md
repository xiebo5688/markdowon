---
enable html: true
---
#  JVM调优
jvm调优基本上是进行垃圾回收
1、java内存结构
java执行过程：
.class文件 --> classLoad(类加载器，专门加载class文件分配到内存空间中)  -------> 内存（方法区     java堆     java栈   本地方法栈）

### 什么是方法区
```
static修饰、常量信息当class文件被加载的时候，就会初始化，所有线程共享方法区，所有注意线程安全问题
```

#### 调优问题：web开发过程中定义过多的static 变量 好不好
```
答案： 不好，因为 static 存放在 方法区（永久区）垃圾回收期根本就不会回收变量，非常占内存，可能出现内存溢出
方法区是所有线程共享的，这里会出现一个问题：线程安全问题：
```

### 什么是堆
```
创建对象、new创建 数组 存放在堆内存 --- 调优策略：堆
堆 是所有线程共享的
```

判断一个对象存放的位置：
```
看创建该对象是否有static关键字修饰
```

### 什么是栈
```
定义局部变量，栈代码运行完毕，自动释放内存，每个线程私有，互不共享，栈不会产生线程安全问题，类的方法存放在栈中
```

### 本地方法栈
```
主要是调用c语言
```

### PC寄存器
```
私有的，计算机组成原理的概览
```

### PC执行引擎
```
执行字节码文件
```

### 垃圾回收机制
```
不定时的回收堆内存空间资源
```
