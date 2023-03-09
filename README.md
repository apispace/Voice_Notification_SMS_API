# APISpace 介绍
**本 API 服务由 [APISpace（apispace.com）](https://www.apispace.com/?utm_source=github&utm_term=yuyintongzhi) 提供。**

APISpace 是 Eolink 旗下专业的 API 开放与交易平台，为广大企业以及个人开发者提供多维度、全方位的API接口，覆盖短信验证、天气查询、快递物流、OCR文字识别等海量 API 服务，帮助用户快速获取数据，降低获取数据的成本和难度，提升开发效率。

APISpace 提供15种开发语言的代码示例，分别是：
- Java(OK HTTP)
- HTTP
- cURL
- 微信小程序
- PHP(pecl_http)、PHP(cURL)
- Python(http.client)、Python(Requests)
- JavaScript(Jquery AJAX)、JavaScript(XHR)
- NodeJS(Native)、NodeJS(Request)
- Ruby(Net:Http)
- Shell(Httpie)、Shell(cUrl)

# 语音通知短信
语音通知服务，通过系统发起电话直呼并播放通知内容；可自定义通知内容，支持变量。

**使用该产品前，您需要通过 [https://www.apispace.com/eolink/api/notify-vocie/introduction](https://www.apispace.com/eolink/api/notify-vocie/introduction?utm_source=github&utm_term=yuyintongzhi) 申请API服务**

本文档末尾提供了 Python(Requests) 的调用代码示例，可以前往文档末尾查看。

更多代码示例：[https://www.apispace.com/eolink/api/notify-vocie/guidence/](https://www.apispace.com/eolink/api/notify-vocie/guidence/?utm_source=github&utm_term=yuyintongzhi)

**该产品拥有以下APIs：**
1. 语音通知
2. 批量语音通知

### 应用场景

1.  会议通知会议临近，通知与会人员按时参会，避免遗漏重要会议。
1.  快递群发快递员可一键向多个用户发起快递送达通知，大大缩短等待时间，提高送件效率。
1.  还款提醒最迟还款期前，以语音通知方式及时通知到借款人，避免用户遗忘、逾期造成损失。
1.  订单通知用户下单后，以语音通知的方式拨打到商家指定的手机或者固话上。
1.  事件提醒紧急安全事件预警，确保市民群众第一时间获取重要信息。


### 使用须知

接听成功扣费，接听不成功不扣费。

### 扣费计算

1.  语音通知，按请求次数扣费；
1.  批量语音通知，按 **号码个数** 扣费。

### 查询发送报告

如果想知道短信的发送情况，可以通过以下API来进行短信发送报告的获取。

注意：数据拉取成功后服务器会删除当前拉取成功的数据，不再保存！请妥善处理接口返回的数据。此状态报告保存时间为72小时，上限存储100万条。

**请求地址**

```
GET  https://cb.o.apispace.com/api/voice/report
```

**请求参数**

| 字段                 | 参数位置   | 说明                  |
| ------------------ | ------ | ------------------- |
| X-APISpace-Token   | Header | apispace的token私钥    |
| Authorization-Type | Header | 鉴权类型，值为：apikey      |
| count              | Query  | 单次调用接口得到的报告数量，默认为10 |

**返回参数**

![image](https://user-images.githubusercontent.com/36323798/223947711-3161c233-bba1-4385-a264-86b17e474e96.png)

**返回示例**

```
{
    “code”:”0”,
    “data”:[
        {
            “callId”:”YYTZ1014203626049417217”,
            “code”:”000”,
            “desc”:”成功”,
            “result”:{
                “timeLength”:5,
                “answerTime”:”1661846594000”,
                “invokeTime”:”1661846587533”,
                “mobile”:”xxxxxx”,
                “callTime”:”1661846591000”,
                “callType”:”0”,
                “byeTime”:”1661846599000”
            },
            “voiceCode”:”1000”,
            “voiceCodeDesc”:”语音播放成功”
        }
    ]
}
```
**状态码文档**

| code状态码 | 参数说明    |
| ------- | ------- |
| 000     | 成功      |
| 001     | 参数校验错误  |
| 002     | 余额不足    |
| 003     | 不在IP白名单 |
| 500     | 未知异常

### Python(Requests) 调用代码示例
这里以 语音通知API 为例
```
import requests

url = "https://eolink.o.apispace.com/notify-vocie/voice-notify"

payload = {"mobile":"","templateId":1011340330258440200,"param":"","allowedCallTime":"","transData":"","isNotifyFileId":""}

headers = {
    "X-APISpace-Token":"",
    "Authorization-Type":"apikey",
    "Content-Type":"application/x-www-form-urlencoded"
}

response=requests.request("POST", url, data=payload, headers=headers)

print(response.text)

```
