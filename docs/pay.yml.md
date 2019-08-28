### Configure

###### src/main/resource/pay.yml
```yaml
##########
## 微信支付
##########
wechat:
    # key为商户平台设置的密钥key
    # 自己要保管好的私有Key了（切记只能放在自己的后台代码里，不能放在任何可能被看到源代码的客户端程序中）
    # 每次自己Post数据给API的时候都要用这个key来对所有字段进行签名，生成的签名会放在Sign这个字段，API收到Post数据的时候也会用同样的签名算法对Post过来的数据进行签名和验证
    # 收到API的返回的时候也要用这个key来对返回的数据算下签名，跟API的Sign数据进行比较，如果值不一致，有可能数据被第三方给篡改
    key: XXXXXXXXXXXXXXXX
    # 微信分配的公众号ID（开通公众号之后可以获取到）
    appid: XXXXXXXXXXXXXXXX
    # 微信支付分配的商户号ID（开通公众号的微信支付功能之后可以获取到）
    mchid: 10000100
    # 受理模式下给子商户分配的子商户号
    submchid:
    # HTTPS证书的本地路径 https://pay.weixin.qq.com/index.php/core/cert/api_cert
    certLocalPath:
    # HTTPS证书密码，默认密码等于商户号MCHID
    certPassword:
    # 是否使用异步线程的方式来上报API测速，默认为异步模式
    useThreadToDoReport: true
    # 填写为本机的IP地址
    ip: 123.12.12.123
    # 支付结果通用通知URL https://pay.weixin.qq.com/wiki/doc/api/native.php?chapter=9_7
    notifyUrl: https://pay.weixin.qq.com/wiki/doc/api/native.php?chapter=9_7

##########
## 支付宝
##########
ali:
    # 合作身份者ID，签约账号，以2088开头由16位纯数字组成的字符串，查看地址：https://b.alipay.com/order/pidAndKey.htm
    partner: 2088121145819891
    # 收款支付宝账号，以2088开头由16位纯数字组成的字符串，一般情况下收款账号就是签约账号
    sellerId: 2088121145819891
    # 商户的私钥,需要PKCS8格式
    # RSA公私钥生成：https://doc.open.alipay.com/doc2/detail.htm?spm=a219a.7629140.0.0.nBDxfy&treeId=58&articleId=103242&docType=1
    privateKey:
    # 支付宝的公钥,查看地址：https://b.alipay.com/order/pidAndKey.htm
    publicKey:
    # 服务器异步通知页面路径  需http://格式的完整路径，不能加?id=123这类自定义参数，必须外网可以正常访问
    notifyUrl: http://商户地址/api/alipay/aync_notify
    # 页面跳转同步通知页面路径 需http://格式的完整路径，不能加?id=123这类自定义参数，必须外网可以正常访问
    returnUrl: http://商户地址/api/alipay/sync_return
    # 签名方式
    signType: RSA
    # 调试用，创建TXT日志文件夹路径，见AlipayCore.java类中的logResult(String sWord)打印方法。
    logPath:
    # 字符编码格式 目前支持 gbk 或 utf-8
    inputCharset: utf-8
    # ⬇️请在这里配置防钓鱼信息，如果没开通防钓鱼功能，为空即可
    # 防钓鱼时间戳  若要使用请调用类文件submit中的query_timestamp函数
    antiPhishingKey:
    # 客户端的IP地址 非局域网的外网IP地址，如：221.0.0.1
    exterInvokeIp:

##########
## 银联
##########
unionpay:
    # 商户号
    merId: 777290058134993
    # 测试环境trId固定值62000000001，生产环境的trId值请咨询银联业务
    trId: 62000000001
    # 前台通知地址 （需设置为外网能访问 http https均可），支付成功后的页面 点击“返回商户”的时候将异步通知报文post到该地址
    # 如果想要实现过几秒中自动跳转回商户页面权限，需联系银联业务申请开通自动返回商户权限
    # 注：如果开通失败的“返回商户”按钮也是触发frontUrl地址，点击时是按照get方法返回的，没有通知数据返回商户
    frontUrl: http://127.0.0.1:8080/ACPSample_WuTiaoZhuan_Token/frontRcvResponse
    # 后台通知地址（需设置为【外网】能访问 http https均可），支付成功后银联会自动将异步通知报文post到商户上送的该地址，失败的交易银联不会发送后台通知
    # 后台通知参数详见open.unionpay.com帮助中心 下载  产品接口规范  网关支付产品接口规范 消费交易 商户通知
    # 注意:1.需设置为外网能访问，否则收不到通知    2.http https均可  3.收单后台通知后需要10秒内返回http200或302状态码
    #     4.如果银联通知服务器发送通知后10秒内未收到返回状态码或者应答码非http200，那么银联会间隔一段时间再次发送。总共发送5次，每次的间隔时间为0,1,2,4分钟。
    #     5.后台通知地址如果上送了带有？的参数，例如：http://abc/web?a=b&c=d 在后台通知处理程序验证签名之前需要编写逻辑将这些字段去掉再验签，否则将会验签失败
    backUrl: http://222.222.222.222:8080/ACPSample_WuTiaoZhuan_Token/BackRcvResponse

    ########################## 入网测试环境交易发送地址（线上测试需要使用生产环境交易请求地址）#############################

    # 交易请求地址
    frontTransUrl: https://101.231.204.80:5000/gateway/api/frontTransReq.do
    backTransUrl: https://101.231.204.80:5000/gateway/api/backTransReq.do
    singleQueryUrl: https://101.231.204.80:5000/gateway/api/queryTrans.do
    batchTransUrl: https://101.231.204.80:5000/gateway/api/batchTrans.do
    fileTransUrl: https://101.231.204.80:9080/
    appTransUrl: https://101.231.204.80:5000/gateway/api/appTransReq.do
    cardTransUrl: https://101.231.204.80:5000/gateway/api/cardTransReq.do

    ######################### 入网测试环境签名证书配置 ################################

    ## 签名证书路径，必须使用绝对路径，如果不想使用绝对路径，可以自行实现相对路径获取证书的方法；测试证书所有商户共用开发包中的测试签名证书，生产环境请从cfca下载得到
    signCertPath: /Users/zhanghua/certs/acp_test_sign.pfx
    ## 签名证书密码，测试环境固定000000，生产环境请修改为从cfca下载的正式证书的密码，正式环境证书密码位数需小于等于6位，否则上传到商户服务网站会失败
    signCertPwd: 000000
    ## 签名证书类型，固定不需要修改
    signCertType: PKCS12

    ########################## 验签证书配置 ################################
    # 验证签名证书目录，只配置到目录即可，必须使用绝对路径，如果不想使用绝对路径，可以自行实现相对路径获取证书的方法；测试证书所有商户共用开发包中的测试验证证书，生产环境所有商户共用开发包中的生产验签证书
    validateCertDir:

    ##########################加密证书配置################################
    ##敏感信息加密证书路径(商户号开通了商户对敏感信息加密的权限，需要对 卡号accNo，pin和phoneNo，cvn2，expired加密（如果这些上送的话），对敏感信息加密使用)
    encryptCertPath:
    ## 是否启用多证书模式(true:单证书|false:多证书---没有配置此项时,默认为单证书模式)
    singleMode: true
```
