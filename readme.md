# 使用场景


如果您在开发微信公众号网页,这里的内容可能会对你有所帮助

阅读官方文档可能会让你了解到更多:


[微信支付JSAPI支付开发步骤](https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_3)

[微信网页授权](https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1421140842)

阅读此文档时默认您已对接好微信登录,若你还没有做好微信登录,请参考上面官方文档:微信网页授权

# 使用步骤


## 1 配置后台

[点击查看配置步骤](https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_3)


## 2 引入文件

    npm install wx-jsbridge-wxpay

或者直接下载index.js,在自己的项目中使用script引入;



## 3 调用

支付参数备注:prepay_id 通过微信支付统一下单接口拿到，paySign 采用统一的微信支付 Sign 签名生成方法，注意这里 appId 也要参与签名，appId 与 config 中传入的 appId 一致，即最后参与签名的参数有appId, timeStamp, nonceStr, package, signType。
具体生成方法参考 [微信内H5调起支付](https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_7&index=6)
```
let payment = {
     "appId":"wx2421b1c4370ec43b",                  //公众号名称，由商户传入     
     "timeStamp":"1395712654",                      //时间戳，自1970年以来的秒数     
     "nonceStr":"e61463f8efa94090b1f366cccfbbb444", //随机串     
     "package":"prepay_id=u802345jgfjsdfgsdg888",   //prepay_id=预支付id 
     "signType":"MD5",                              //微信签名方式：     
     "paySign":"70EA570631E4BB79628FBCA90534C63FF7FADD89" //微信签名 
}

wxJSBridgePay(payment).then(res=>{
    console.log('支付结果',res);
})

```
### 特别提醒:
支付参数中的package中一般使用后端从统一支付接口获取到的prepay_id;

假设prepay_id为a1b2c3; 提交时package的值应为package:'prepay_id=a1b2c3';如果是package:'a1b2c3';会返回失败!!!


