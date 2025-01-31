# GoogleCSAgent_cdf
CSAgent 与 GoogleAuth 的缝合体，cobalt strike4.4版本的破解+otp动态口令的agent

编译：`mvn clean package -DskipTests`

使用方法：

## 先，生成otp的密钥：

命令：`java -jar GoogleCSAgent.jar`

![image-20211208114532203](README/image-20211208114532203.png)

data:image是二维码，复制到浏览器中用app扫即可；Secret是密钥，添加到teamserver中即可。

## 再，启动teamserver：

```
java -XX:ParallelGCThreads=4 -Dcobaltstrike.server_port=50050 -Djavax.net.ssl.keyStore=./cobaltstrike.store -Djavax.net.ssl.keyStorePassword=123456 -server -XX:+AggressiveHeap -XX:+UseParallelGC -javaagent:GoogleCSAgent.jar=5BDANTCIUEGDH76PBLZJTCBNJBTKNRXB -classpath ./cobaltstrike.jar server.TeamServer $*
```

未破解原版的cobaltstrike.jar用javaagent启动后就变成了个破解版带有GoogleAuth二次认证的小可爱了。

**PS：想修改成其他版本cs，需要修改GoogleCSAgent.java中76行“5e98194a01c6b48fa582a6a9fcbb92d6”为对应版本的key即可。**

## 参考

https://github.com/HKirito/GoogleAuth.git

https://github.com/Twi1ight/CSAgent.git
