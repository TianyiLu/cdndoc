# Azure CDN HTTPS加速服务-自由证书

Azure CDN提供HTTPS安全加速服务，支持用户上传自有证书，也支持Azure CDN代为申请证书，均只开放给付费用户。本文档针对用户自己上传证书自动化部署的情况，Azure CDN代为申请证书请参考[Azure CDN HTTPS加速服务-Azure代为申请证书](https://www.azure.cn/documentation/articles/cdn-https-how-to/)。

##证书说明

- 用户自有证书的HTTPS加速是基于SNI技术实现的，SNI证书可以多个HTTPS 客户共享同一个IP 地址。
    >**注意** SNI技术不支持Windwos XP系统下所有的IE版本，浏览器会提示不受信任。

- 开启HTTPS加速后，需要上传加速域名的证书和私钥，证书和私钥需要匹配，否则会校验出错。

- 上传的证书和私钥需要匹配，且证书格式为PEM格式，不支持其他格式的证书，需将其他格式的证书转换成PEM格式，可以通过openssl工具进行转换。
    >**注意** 
    >秘钥编码格式目前支持RSA PCKS 1到PKCS8编码格式，可以使用openssl工具将秘钥编码格式转为支持的编码格式，以PKCS8为例：
    >
    >.\openssl.exe pkcs8 -topk8 -inform PEM -outform PEM -in .\keyfile.key -out converted.key -nocrypt

- 支持看证书信息，但不支持证书下载，也不支持秘钥查看，请保管好证书相关信息。
- 目前不支持证书链。

##配置说明

- HTTPS加速只发放给付费用户。
- 支持泛域名的HTTPS加速。
- 支持的加速类型为网页加速，下载加速，点播加速和直播加速。
     >**注意** 图片处理加速类型暂不支持HTTPS加速。
- 用户需先创建好所需加速类型的HTTP加速，之后点击配置界面的“管理”按钮，跳转到CDN节点管理界面启用HTTPS服务，并上传PEM格式的证书和秘钥。
- 开启HTTPS加速后，默认同时支持HTTP和HTTPS方式的请求。如需强制将HTTP请求跳转成HTTPS请求，请联系世纪互联进行配置。我们后续会在管理界面实现自动化选择。
- 回源协议默认跟随用户发起的请求协议，即HTTP请求通过HTTP协议回源，HTTPS请求通过HTTPS协议回源。如需指定只有HTTP回源或者只有HTTPS回源，请联系世纪互联尽心配置。我们后续会在管理界面实现自动化选择。


##价格说明

自有证书的HTTPS加速价格是标准版服务价格，具体计费方式请参见[Azure官方网站](https://www.azure.cn/pricing/details/cdn/)。

### 启用HTTPS加速配置步骤

