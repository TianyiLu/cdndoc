# Azure China CDN Restful API正式上线

对于电商，在线社交等图片为主的网站，需要定期批量刷新图片，上千万图片手动刷新简直是运维的噩梦；很多市场活动定时上新，运维人员需要蹲点操作；跨平台资源需要整合到统一的展示平台给老板看等。使用Azure China CDN的开发者和运维朋友的福音来啦！除了现有图形化管理界面对CDN节点进行创建、删除、缓存刷新、设置缓存规则，预加载等功能进行管理外，Azure China CDN团队正式上线CDN API接口供用户对CDN资源进行管理。

用户只需按照接口说明在请求中加入相应请求参数即可获得相应结果，通过Azure China CDN API管理Azure China CDN资源，实现自动化操作。API支持通过HTTPS协议进行请求通信，验证和授权方式基于接口密钥，密钥申请需要到[Azure CDN新版管理门户](https://www.azure.cn/documentation/articles/cdn-management-v2-portal-how-to-use/)申请。

目前Azure China CDN可以实现如下功能：

- 节点管理- 在指定Azure订阅下创建、删除、启用、禁用CDN节点；查询、更新CDN节点信息，比如修改CDN源站等；设定缓存规则
- 流量查询-  按月、天、小时、分钟，根据订阅或者单个域名查看流量信息
- 内容管理- 缓存刷新、预加载

想要使用API实现CDN资源管理的用户，快去Azure China CDN Restful API文档了解更多吧。

Azure China CDN团队正紧锣密鼓的开发其他基于API的功能，比如日志分析查看用户请求的地域、终端分布、热门URL、请求状态码分布等，HTTPS自定义证书上传等功能。敬请期待。

