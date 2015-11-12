# 常见问题

##服务咨询

- **CDN的概念和作用**

    CDN 的全称是 Content Delivery Network，即内容分发网络。CDN通过在现有的 Internet 中添加一层新的网络架构，将网站的内容缓存到离用户最近的网络“边缘”，使用户可以就近取得所需的内容，从而提供高带宽、低延迟的用户体验。 

- **什么是CNAME？**
    
    CNAME(Canonical Name record)，通常是别名指向。例如，假设用户自定义加速域名为www.abc.com，用户配置完成后网站加速里给出的CDN服务域名为www.abc.com.mschcdn.com。用户需要在 域名托管服务商那里将www.abc.com对应的A记录删除，添加域名的CNAME记录为www.abc.com.mschcdn.com。这样，用户访问www.abc.com时会去获取www.abc.com.mschcdn.com解析出的加速节点的IP地址记录。

- **CDN流量和回原流量关系**
    - CDN流量表示缓存命中部分
    - 回原流量表示MISS部分 

- **域名审核周期是多久？**
   
    审核所提供的自定义域名和ICP编号是否匹配、有效，这个过程需要最多一个工作日的时间来完成。如果ICP审核通过，CDN服务最多需要 60 分钟时间进行注册以便通过 CDN 网络传播。与此同时，您还需要按照界面上的提示信息配置CNAME映射信息，这样才可以最终通过自定义域名访问CDN缓存内容。

- **为什么使用CDN一定要有备案号？**
 
    使用CDN以后解析出来的IP是FC节点IP。如果没有备案工信部发现的话会直接封IP的。为了后续不给您带来更多的麻烦建议没有备案或者备案号被取消的域名申请备案待工信部能查到后再使用加速服务。
- **二级域名需要备案吗？**

    二级域名不需要备案；如果sample.com已经备案，那么images.sample.com则不需要备案。


- **如果域名有跳转是否可以使用CDN？**
     
    可以，不过建议给跳转后的域名加速，跳转前的域名加速没有必要。

- **一个账户内是否对本账户添加的加速域名个数有限制？**

    Windows Azure CDN对每个账户的加速域名个数没有做限制。
    
- **Windows Azure CDN支持哪些类型的加速？**
  
    现阶段提供的CDN主要是静态加速，包含一部分动态加速技术。比如：通过多线路节点回源，TCP优化等。不支持对PHP，ASP.NET，JSP等动态网页的加速，后续会逐步增加更多对动态页面的加速。
    
    Windows Azure CDN支持的加速类型包括：Web加速，下载加速，VOD加速和HTTPS加速。
	
- **CDN加速类型中的“WEB加速”、“下载加速”、“VOD加速”、“HTTPS加速”具体有什么区别？**

    不同的CDN加速类型对应于不同的使用场景：
    1.WEB加速对应于网页等（html，CSS,图片，JS）比较小的静态文件加速
    2.下载加速一般对应于20MB以上的大文件文件分发
    3.VOD加速对应于基于HTTP的视频点播加速
    4.HTTPS加速针对对安全性要求比较高的情况
    对应到后端CDN的不同之处主要在于，不同的加速类型由不同的CDN节点设备来支撑，您无需做额外配置。

- **Windows Azure CDN缓存规则逻辑是什么？**
	
    缓存规则逻辑：
	1. 如果用户配置了不缓存的规则，优先匹配；然后匹配需要缓存的规则；缓存规则自上而下匹配。
	2. 如果某个URL在不缓存、缓存规则里都没有匹配上，那么就遵循CDN默认规则（遵循源站响应Header设置，如果有cookie、no-cache、expires等限制，就不缓存，否则就会缓存）
	   - Set-Cookie，开启允许忽略Cookie时允许缓存，关闭时不允许缓存。Cookie在用于用户登录和身份识别时是不能勾选忽略Set-Cookie选项的，否则可能引起功能性问题。
       - Cache-Control：若Cache-control的值含有no-store/no-cache/private，开启允许忽略Cache-control时允许缓存，关闭后不允许缓存。
       - Expires：指定了缓存内容到期时间点，到期后会自动刷新。
       - Max-age：指定了缓存时间长度，单位为秒，如果太小，如小于两位数，那么很快就会过期，导致无法缓存。
	3. Windows Azure CDN高级管理平台 “域名管理”界面下面的“修改缓存规则”中可以选择“设置为禁止缓存”功能。即：凡是客户未配置需要缓存的内容，都不缓存。	 
	
- **如何设置缓存刷新？**
   
    1. 设置缓存规则：可以到Windows Azure CDN管理平台上针对不同的内容设置不同的缓存刷新规则，对更新频繁的内容，可以设置较短的缓存时间； 对于不经常更新的内容，可以设置较长的缓存时间，从而减小源站压力。
    2. 手动刷新：若设置的CDN缓存内容生存时间未到期，但是有新内容发布或者删除部分内容，可以根据需求使用Windows Azure CDN高级管理平台提供的缓存刷新功能，设置文件刷新和目录刷新，从而进行手动刷新。 

      
- **“源站地址（回源地址）”和“回源域名（回源host header）”的区别是什么？**
	 
	 回源地址表示源站实际可以被访问到的地址，可以是IP也可以是域名。如果是域名，CDN在回源是会对该域 名进行地址解析，然后用解析出来的IP再进行访问。
	 回源域名表示CDN回源时，HTTP请求头（request header）中的Host字段值。这个字段值一般是域名形式的字符串，被源站用来识别是否与源站服务器上配置的域名相同。
	 
	 在azure management portal里创建CDN的时候，在“原点主机标头（origin host header）”中输入您的源站所接受的回源访问host header。当您输入完“自定义域”之后，系统会根据您所选择的“原始域类型”来自动填充一个默认值。具体的规则是，如果您的源站是在Azure上的话，默认值就是相应的源站地址。如果您的源站不在Azure上，默认值是您输入的“自定义域名”，当然您也可以根据自己源站的实际配置情况来修改。
- **CDN标准版和CDN高级版有什么区别？**
     
    首先，价格不同，具体请参考[定价详细信息](http://www.windowsazure.cn/home/features/cdn/#price)。其次，目前CDN高级版仅包含https的加速服务，后续会逐步增加其他的高级加速服务。目前如果您想使用 CDN HTTPS 加速服务，请通过支持页面联系 Windows Azure 的支持团队开通 CDN HTTPS 加速服务。
- **Azure CDN合作的CDN服务厂商都有谁？**

    目前Windows Azure CDN和蓝汛和网宿合作，为用户提供优质的CDN加速服务。后续会有其他国内主流CDN服务厂商合作。
- **如何配置CNAME？**

     到域名托管商找到该域名解析管理—删除该域名的A记录—添加一条cname记录，cname的域名我们已经给出。

- **怎么确认我的CNAME记录生效了？**

     各地DNS的生效时间不一致，取决于域名对应的原有记录的生效时间（TTL时间）。当ping域名，给出的解析不再是您源站IP，说明已经生效了。

##价格咨询

- **在每月传输的数据超过 10TB 后，是否按更高等级的费率对所有数据传输计费？**

    不。属于每个等级的使用量将按照针对该等级的费5费。例如，如果您在区域 1 产生了 50TB 的标准版 CDN 数据传输，前 10TB 将按照每 GB ¥ 0.41 的费率计费，剩下的 40TB 将按照每 GB ¥ 0.41 的费率计费。


##进阶问题
    
- **为什么回原大于CDN流量？**
 
    一般回原流量<=CDN流量，特殊情况也可能出现回原流量大于CDN流量，比如：如果访问者发起一个请求，请求一个比较大的文件。比如100M，如果节点没有缓存的情况，CDN节点就会去源站获取，这么大文件必然需要点时间，然而此时，访问者又不继续等了于是就断开连接。这样，CDN节点还是会去把100M文件全都拿过来。此时发现访问者已经不要它了，它就没法再返回了，于是，回源的流量就有100M，而CDN流量没有。

- **更换原站服务器如何操作？**
    
    需要。首先要确保域名能正常解析，然后在Windows Azure高级管理平台—域名管理中将原站地址变更为新的地址，保存即可。

- **为什么我的URL不能缓存？**

     URL不能被缓存，通常有以下几个原因： 
     1. 源站的该URL响应Header里含有以下信息：
        - Set-Cookie（且缓存规则里并未勾选忽略Set-Cookie选项）。注：Set-Cookie在用于用户登录和身份识别时是不能勾选忽略Set-Cookie选项的，否则可能引起功能性问题。
        - Cache-Control：no-store/no-cache/private（且缓存规则里并未勾选忽略Cache-Control选项）。
        - Expires的时间是过去的某个时间，Expires指定了缓存到期时间点，如果是过去时间，则将导致无法缓存。
        - Max-age的值很小，Max-age指定了缓存时间长度，单位为秒，如果太小，如小于两位数，那么很快就会过期，导致无法缓存。
      2. 缓存规则里没有配置或配置错误，URL无法命中任何一个缓冲规则，例如，有用户不小心录入以下规则:” [任意字符](.gif|.jpg|.bmp) (.gif|.jpg|.bmp)”，那么即使是图片类型也无法命中规则，因为扩展名重复。
      3. 部分节点暂时还没有用户访问该URL，需要有访问之后才会缓存

- **系统提示不能CNAME**

     有可能，虽然我们没有限制加速域名但是有的域名托管商不允许不带有主机名的域名进行cname，对此，没有更好的办法：要么更换加速域名，要么更换域名托管商。

- **用了CDN后打开速度更慢**

    缓存命中率不高，影响缓存命中率的几个原因：
       - 缓存配置的问题
       - Http Header导致无法缓存
       - 刚添加CDN加速节点，缓存的文件还不多
       - 源站类型，可缓存的内容少
       - 网站访问量低，过期时间短，命中的文件少

- **回源比例比较大** 

    1. 缓存规则配置问题
    2. 可缓存资源少
    3. 缓存时间短
    
 - **使用CDN后，网站打不开 ** 

     可能因素：
     1. 原站故障
     2. 原站有设置防火墙，屏蔽FC
     3. 节点屏蔽客户ip 
     4. 新添加域名/域名状态变更，节点配置下发问题
     5. 设备故障
     
 - **使用CDN后，网站登录异常**
 
     很有可能是在缓存规则中设置了不该缓存的资源，需要将用户后台登陆的文件夹设置不缓存（如： /user  或者 /admin等等）；同时在缓存规则配置中一定不要勾选set-cookie。

- **缓存刷新失败**

    手动提交刷新后系统会统计正常服务的设备来下发任务，如果任务下发过程中某一台设备出现异常，系统会自动检测出来并探测关闭（服务状态关闭后客户不会解析到该节点，不影响加速服务），其他正常设备继续下发任务，直至完成，此时界面就会显示“刷新失败”，同时客服和运维会接到邮件，第一时间做处理，即便是刷新失败不影响CDN服务。

- **为什么没有cname到Windows Azure CDN却消耗CDN流量**

    有可能，因为只要加速域名的服务状态是开启的，即便没有cname到Windows Azure CDN， 我们的探测设备都会通过监控url探测原站和加速情况，这个也是为什么我们建议您选择监控url尽可能选择小一些的文件，如果您不想未cname的加速域名消耗流量可以将服务状态关闭。



