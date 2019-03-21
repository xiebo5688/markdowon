---
enable html: true
---
# **java.io.FileNotFoundException(系统找不到指定的路径、拒绝访问)**

## 产生原因：
`File file = new File("D:\dow\20190311")`
`FileOutputStream fos = new FileOutputStream(newFile);`
这里是文件字节输出流直接读取文件，即在d盘下的文件夹dow下的文件20190311，但是实际上是20190311是哥文件夹，这时候会报异常：java.io.FileNotFoundException（拒绝访问）
## 解决方案：
1、先创建一个包含父类文件夹的文件夹
`File file = new File("D:\dow\20190311");`
```
判断目录是否存在，若不存在则直接创建包含父目录的文件夹
if(!file.exists()){
  file.mkdirs(); }     //mkdirs() 表示创建包含父目录在内的所有文件夹  mkdir()表示创建指定文件夹，不包含父类文件夹
```
2、使用第一步创建的文件夹，在其中写入文件
`File newFile = new File(file ,"abc.jpg")`
3、在使用文件字节输出流将文件写入第一步中创建的文件夹
`FileOutputStream fos=new FileOutputStream(newFile);`

