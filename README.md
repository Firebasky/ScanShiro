# ScanShiro

>把去年写的ShiroScan 给重构了一下

## Update
1.扫描的判断逻辑,通过返回的rememberMe个数进行判断

2.添加了bypass功能,可以发送随机的请求方法


## 学习

[原理](http://www.lmxspace.com/2020/08/24/%E4%B8%80%E7%A7%8D%E5%8F%A6%E7%B1%BB%E7%9A%84shiro%E6%A3%80%E6%B5%8B%E6%96%B9%E5%BC%8F/)

```java
<1.2.4   shiro550
<1.4.2   shiro721 https://cloud.tencent.com/developer/article/1944738 需要成功登录(目前还没有添加
>1.4.2   换加密方法 aes cmg
```

## 使用

```java
暴力破解key
java -jar ScanShiro.jar -u http://0.0.0.0 -k key.txt
        
批量暴力破解key
java -jar ScanShiro.jar -f url.txt -k key.txt
        
根据正确的key生成payload 适合在有key无gadgets的情况下
java -jar ScanShiro.jar -p payload.ser -c kPH+bIxk5D2deZiIxcaaaA==

-n 参数是值修改shiro中cookie的名字少部分环境存在,默认是rememberMe
        
-proxy 参数是代理 目前只支持socks5代理并且没有用户名密码

支持 -bypass 1 
发送数据的请求方法
```

**说明:默认是先跑常规的模式如果没有跑出key就自动跑AES/GCM,并且生成payload的时候生成这两种的payload。怎么说呢工具肯定是存在误报的！！！**


## 问题

  1. 少部分环境存在shiro rememberMe参数为于post请求中 等待解决
  2. 经过大量测试,发现当跑批量的时候小几率出现连接异常的问题.所以为了保证工具准确性建议提前测试目标连接情况

