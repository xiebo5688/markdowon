---
enable html: true
---
# ftps服务器连接发生错误（证书过期）

报错信息：
`javax.net.ssl.SSLHandshakeException`
报错原因：
`由于ftps服务器传输数据的过程中需要进行加密证书进行认证，由于证书有加密期限，刚好在当天上午证书过期，所以连接服务器的时候一直报错`

分析
`1、由于客户公司（广州燃气公司）搭建的ftps服务器是通过 SSLHandshakeException 来进行证书认证的，通过查询网络资料得知 https的加密证书也是通过SSLHandshakeException 进行加密的，通过查找 https加密证书不通过 搜索对应的帖子，得知重写 TrustManager 可以解决改问题 `
`2、查找对应的api（http://commons.apache.org/proper/commons-net/apidocs/org/apache/commons/net/ftp/FTPSClient.html#setTrustManager(javax.net.ssl.TrustManager)）得知 有对应的  setTrustManager() 这个方法`

![setTrustManager]($resource/QQ%E6%B5%8F%E8%A7%88%E5%99%A8%E6%88%AA%E5%9B%BE20190225194117.png)
 `重写 jvm的 TrustManager 这个类即可解决问题，如下图所示`
![重写TrustManager ]($resource/QQ%E6%B5%8F%E8%A7%88%E5%99%A8%E6%88%AA%E5%9B%BE20190225204157.png)
