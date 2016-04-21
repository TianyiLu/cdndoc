# 服务检查

用户在创建CDN服务终节点后，可以在“服务检查”视图做一些基本的检查。我们强烈建议用户在CNAME操作之前，做一下服务检查。

![][1]

如上视图，用户选择需要检查的域名后，提供一个源站可以访问的资源，然后点击“检查”。

1. 源站正常 - 表明提供的资源可以访问；
2. CDN部署完成 - 表明该域名对应的CDN服务已经部署；
3. CDN缓存正常 - 表明通过源站访问的内容和通过CDN访问的内容一致（通过比较HTTP头：HTTP Status Code，Last Modified Time，Content Length）。

>**注意**
>服务检查功能不能保证该域名所处的所有CDN边缘服务器都没有异常。

 [1]: images/service-check.png