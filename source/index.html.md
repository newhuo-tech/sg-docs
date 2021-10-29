title: 火币新加坡 API 文档

language_tabs: # must be one of https://git.io/vQNgJ

  - json

toc_footers:

  - <a href='https://www.huobi.sg/zh-cn/login/?backUrl=%2Fzh-cn%2Fapikey%2F'>创建 API Key </a>
    includes:

search: true

# 更新日志

<style>
table {
    max-width:100%
}
table th {
    white-space: nowrap; /*表头内容强制在一行显示*/
}
</style>





| 生效时间<br>(UTC +8) | 接口                    | 变化 | 摘要                       |
| -------------------- | ----------------------- | ---- | -------------------------- |
| 2021.8.24            | `market.$symbol.ticker` | 新增 | 增加聚合行情（Ticker）数据 |
|                      |                         |      |                            |

# 简介

欢迎使用火币新加坡 API！  

此文档是火币新加坡API的唯一官方文档，火币新加坡API提供的功能和服务会在此文档持续更新，并会发布公告进行通知，建议您关注和订阅我们的公告，及时获取相关信息。

您可以点击 <a href='https://huobisg.zendesk.com/hc/en-us/sections/4407023586585-API-Announcements'>这里</a> 查看公告。如果想订阅公告，请在“API公告”页右上角点击“关注”按钮，会弹出登录窗口，用账号登录成功后，再次点击“关注”按钮，并选择需要关注的内容类型，按钮变为“正在关注”，即表示订阅成功。若无账号，可以点击登录窗口中的“注册”按钮，进行注册。

**如何阅读本文档**

文档上方导航栏是不同业务的API；右上方的语言按钮可以切换文档语言，目前支持中文和英文。
文档下方是某个业务的API文档，其中左侧是目录，中间是正文，右侧是请求参数和响应结果的示例。

以下是现货API文档各章节主要内容

第一部分是概要介绍：

- **快速入门**：该章节对火币新加坡API做了简单且全方位的介绍，适合第一次使用火币API的用户。
- **在线演示**：该章节介绍了现货API在线演示工具，方便用户直接调用和观察线上API环境。
- **常见问题**：该章节列举了使用火币新加坡API时常见的、和具体API无关的通用问题。
- **联系我们**：该章节介绍了针对不同问题，如何联系我们。

第二部分是每个接口类的详细介绍，每个接口类一个章节，每个章节分为如下内容：

- **简介**：对该接口类进行简单介绍，包括一些注意事项和说明。
- ***具体接口***：介绍每个接口的用途、限频、请求、参数、返回等详细信息。
- **常见错误码**：介绍该接口类下常见的错误码及其说明。
- **常见问题**：介绍该接口类下常见问题和解答。

# 快速入门

## 接入准备

如需使用API ，请先登录网页端，完成API key的申请和权限配置，再据此文档详情进行开发和交易。  

您可以点击 <a href='https://www.huobi.sg/zh-cn/login/?backUrl=%2Fzh-cn%2Fapikey%2F'>这里 </a> 创建 API Key。

每个母用户可创建20组Api Key，每个Api Key可对应设置读取、交易、提币三种权限。  

权限说明如下：

- 读取权限：读取权限用于对数据的查询接口，例如：订单查询、成交查询等。
- 交易权限：交易权限用于下单、撤单、划转类接口。
- 提币权限：提币权限用于创建提币订单、取消提币订单操作。

创建成功后请务必记住以下信息：

- `Access Key`  API 访问密钥

- `Secret Key`  签名认证加密所使用的密钥（仅申请时可见）

<aside class="notice">
每个 API Key 最多可绑定 5个IP 地址(主机地址或网络地址)，未绑定 IP 地址的 API Key 有效期为90天。出于安全考虑，强烈建议您绑定 IP 地址。
</aside>
<aside class="warning">
<red><b>风险提示</b></red>：这两个密钥与账号安全紧密相关，无论何时都请勿将二者<b>同时</b>向其它人透露。API Key的泄露可能会造成您的资产损失（即使未开通提币权限），若发现API Key泄露请尽快删除该API Key。
</aside> 




## SDK与代码示例

**SDK（推荐）**

[Java](https://github.com/huobiapi/huobi_Java) | [Python3](https://github.com/huobiapi/huobi_Python) | [C++](https://github.com/huobiapi/huobi_Cpp) | [C#](https://github.com/HuobiRDCenter/huobi_CSharp) | [Go](https://github.com/huobirdcenter/huobi_golang)

**其它代码示例**

[https://github.com/huobiapi?tab=repositories](https://github.com/huobiapi?tab=repositories)

## 测试环境（已停止）

测试环境运行了一段时间后，因用户访问量很少，而维护成本很高，我们慎重决定后将其停止。

线上环境更稳定，流动性更好，建议您直接使用线上环境。 

## 接口类型

火币新加坡为用户提供两种接口，您可根据自己的使用场景和偏好来选择适合的方式进行查询行情、交易或提币。  

### REST API

REST，即Representational State Transfer的缩写，是目前较为流行的基于HTTP的一种通信机制，每一个URL代表一种资源。

交易或资产提币等一次性操作，建议开发者使用REST API进行操作。

### WebSocket API

WebSocket是HTML5一种新的协议（Protocol）。它实现了客户端与服务器全双工通信，通过一次简单的握手就可以建立客户端和服务器连接，服务器可以根据业务规则主动推送信息给客户端。

市场行情和买卖深度等信息，建议开发者使用WebSocket API进行获取。

**接口鉴权**

以上两种接口均包含公共接口和私有接口两种类型。

公共接口可用于获取基础信息和行情数据。公共接口无需认证即可调用。

私有接口可用于交易管理和账户管理。每个私有请求必须使用您的API Key进行签名验证。

## 接入URLs

您可以自行比较使用api.huobi.sg和api-aws.huobi.sg两个域名的延迟情况，选择延迟低的进行使用。

其中，api-aws.huobi.sg域名对使用aws云服务的用户做了一定的链路延迟优化。   （永庆确认是否删除）

**REST API**

https://api.huobi.sg

Websocket Feed（行情，不包含MBP增量行情）

wss://api.huobi.sg/ws

Websocket Feed（资产和订单）

wss://api.huobi.sg/ws/v  

<aside class="notice">
请使用中国大陆以外的 IP 访问火币新加坡 API。
</aside>
<aside class="notice">
鉴于延迟高和稳定性差等原因，不建议通过代理的方式访问火币新加坡API。
</aside>
<aside class="notice">
为保证API服务的稳定性，建议使用日本AWS云服务器进行访问。如使用中国大陆境内的客户端服务器，连接的稳定性将难以保证。 
</aside> 



## 签名认证

### 签名说明

API 请求在通过 internet 传输的过程中极有可能被篡改，为了确保请求未被更改，除公共接口（基础信息，行情数据）外的私有接口均必须使用您的 API Key 做签名认证，以校验参数或参数值在传输途中是否发生了更改。  
每一个API Key需要有适当的权限才能访问相应的接口，每个新创建的API Key都需要分配权限。在使用接口前，请查看每个接口的权限类型，并确认你的API Key有相应的权限。

一个合法的请求由以下几部分组成：

- 方法请求地址：即访问服务器地址 api.huobi.sg，比如 api.huobi.sg/v1/order/orders。
- API 访问Id（AccessKeyId）：您申请的 API Key 中的 Access Key。
- 签名方法（SignatureMethod）：用户计算签名的基于哈希的协议，此处使用 HmacSHA256。
- 签名版本（SignatureVersion）：签名协议的版本，此处使用2。
- 时间戳（Timestamp）：您发出请求的时间 (UTC 时间)  。如：2017-05-11T16:22:06。在查询请求中包含此值有助于防止第三方截取您的请求。
- 必选和可选参数：每个方法都有一组用于定义 API 调用的必需参数和可选参数。可以在每个方法的说明中查看这些参数及其含义。 
  - 对于 GET 请求，每个方法自带的参数都需要进行签名运算。
  - 对于 POST 请求，每个方法自带的参数不进行签名认证，并且需要放在 body 中。
- 签名：签名计算得出的值，用于确保签名有效和未被篡改。

### 签名步骤

规范要计算签名的请求 因为使用 HMAC 进行签名计算时，使用不同内容计算得到的结果会完全不同。所以在进行签名计算前，请先对请求进行规范化处理。下面以查询某订单详情请求为例进行说明：

查询某订单详情时完整的请求URL

`https://api.huobi.sg/v1/order/orders?`

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`&SignatureMethod=HmacSHA256`

`&SignatureVersion=2`

`&Timestamp=2017-05-11T15:19:30`

`&order-id=1234567890`

**1. 请求方法（GET 或 POST，WebSocket用GET），后面添加换行符 “\n”**

例如：
`GET\n`

**2. 添加小写的访问域名，后面添加换行符 “\n”**

例如：
`
api.huobi.sg\n
`

**3. 访问方法的路径，后面添加换行符 “\n”**

例如查询订单：<br>
`
/v1/order/orders\n
`

例如WebSocket v2<br>
`
/ws/v2
`

**4. 对参数进行URL编码，并且按照ASCII码顺序进行排序**

例如，下面是请求参数的原始顺序，且进行URL编码后


`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`order-id=1234567890`

`SignatureMethod=HmacSHA256`

`SignatureVersion=2`

`Timestamp=2017-05-11T15%3A19%3A30`

<aside class="notice">
使用 UTF-8 编码，且进行了 URL 编码，十六进制字符必须大写，如 “:” 会被编码为 “%3A” ，空格被编码为 “%20”。
</aside>
<aside class="notice">
时间戳（Timestamp）需要以YYYY-MM-DDThh:mm:ss格式添加并且进行 URL 编码。时间戳有效时间5分钟。
</aside>



经过排序之后

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`SignatureMethod=HmacSHA256`

`SignatureVersion=2`

`Timestamp=2017-05-11T15%3A19%3A30`

`order-id=1234567890`

**5. 按照以上顺序，将各参数使用字符 “&” 连接**


`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30&order-id=1234567890`

**6. 组成最终的要进行签名计算的字符串如下**

`GET\n`

`api.huobi.sg\n`

`/v1/order/orders\n`

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30&order-id=1234567890`


**7. 用上一步里生成的 “请求字符串” 和你的密钥 (Secret Key) 生成一个数字签名**


1. 将上一步得到的请求字符串和 API 私钥作为两个参数，调用HmacSHA256哈希函数来获得哈希值。
2. 将此哈希值用base-64编码，得到的值作为此次接口调用的数字签名。

`4F65x5A2bLyMWVQj3Aqp+B4w+ivaA7n5Oi2SuYtCJ9o=`

**8. 将生成的数字签名加入到请求里**

对于Rest接口：

1. 把所有必须的认证参数添加到接口调用的路径参数里
2. 把数字签名在URL编码后加入到路径参数里，参数名为“Signature”。

最终，发送到服务器的 API 请求应该为

`https://api.huobi.sg/v1/order/orders?AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&order-id=1234567890&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30&Signature=4F65x5A2bLyMWVQj3Aqp%2BB4w%2BivaA7n5Oi2SuYtCJ9o%3D`

对于WebSocket接口：

1. 按照要求的JSON格式，填入参数和签名。
2. JSON请求中的参数不需要URL编码

例如：

`
{
    "action": "req", 
    "ch": "auth",
    "params": { 
        "authType":"api",
        "accessKey": "e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx",
        "signatureMethod": "HmacSHA256",
        "signatureVersion": "2.1",
        "timestamp": "2019-09-01T18:16:16",
        "signature": "4F65x5A2bLyMWVQj3Aqp+B4w+ivaA7n5Oi2SuYtCJ9o="
    }
}
`


## 业务字典

### 交易对

交易对由基础币种和报价币种组成。以交易对 ETH/BTC 为例，ETH 为基础币种，BTC 为报价币种。  

基础币种对应字段为 base-currency 。  

报价币种对应字段为 quote-currency 。 

### 账户

不同业务对应需要不同的账户，account-id为不同业务账户的唯一标识ID。  

account-id可通过/v1/account/accounts接口获取，并根据account-type区分具体账户。  

账户类型包括：   

* spot：现货账户 

# 接入说明

## 接口概览

| 接口分类 | 分类链接                     | 概述                                             |
| -------- | ---------------------------- | ------------------------------------------------ |
| 基础类   | /v1/common/*                 | 基础类接口，包括币种、币种对、时间戳等接口       |
| 行情类   | /market/*                    | 公共行情类接口，包括成交、深度、行情等           |
| 账户类   | /v1/account/*  /v1/subuser/* | 账户类接口，包括账户信息，子用户等               |
| 订单类   | /v1/order/*                  | 订单类接口，包括下单、撤单、订单查询、成交查询等 |

该分类为大类整理，部分接口未遵循此规则，请根据需求查看有关接口文档。

## 新限频规则

- 当前，新限频规则正在逐步上线中，已单独标注限频值的接口且该限频值被标注为NEW的接口适用新限频规则。

- 新限频规则采用基于UID的限频机制，即，同一UID下各API Key同时对某单个节点请求的频率不能超出单位时间内该节点最大允许访问次数的限制。

- 用户可根据Http Header中的"X-HB-RateLimit-Requests-Remain"（限频剩余次数）及"X-HB-RateLimit-Requests-Expire"（窗口过期时间）查看当前限频使用情况，以及所在时间窗口的过期时间，根据该数值动态调整您的请求频率。

## 限频规则

除已单独标注限频值为NEW的接口外 -<br>

* 每个API Key 在1秒之内限制10次<br>
* 若接口不需要API Key，则每个IP在1秒内限制10次<br>

比如：

* 资产订单类接口调用根据API Key进行限频：1秒10次
* 行情类接口调用根据IP进行限频：1秒10次

## 请求格式

所有的API请求都是restful，目前只有两种方法：GET和POST

* GET请求：所有的参数都在路径参数里
* POST请求，所有参数以JSON格式发送在请求主体（body）里

## 返回格式

所有的接口都是JSON格式。其中v1和v2接口的JSON定义略有区别。

**v1接口返回格式**：最上层有四个字段：`status`, `ch`,  `ts` 和 `data`。前三个字段表示请求状态和属性，实际的业务数据在`data`字段里。

以下是一个返回格式的样例：

```json
{
  "status": "ok",
  "ch": "market.ethbtc.kline.1day",
  "ts": 1499223904680,
  "data": // per API response data in nested JSON object
}
```

| 参数名称 | 数据类型 | 描述                                                         |
| -------- | -------- | ------------------------------------------------------------ |
| status   | string   | API接口返回状态                                              |
| ch       | string   | 接口数据对应的数据流。部分接口没有对应数据流因此不返回此字段 |
| ts       | long     | 接口返回的UTC时间的时间戳，单位毫秒                          |
| data     | object   | 接口返回数据主体                                             |

**v2接口返回格式**：最上层有三个字段：`code`, `message` 和 `data`。前两个字段表示返回码和错误消息，实际的业务数据在`data`字段里。

以下是一个返回格式的样例：

```json
{
  "code": 200,
  "message": "",
  "data": // per API response data in nested JSON object
}
```

| 参数名称 | 数据类型 | 描述               |
| -------- | -------- | ------------------ |
| code     | int      | API接口返回码      |
| message  | string   | 错误消息（如果有） |
| data     | object   | 接口返回数据主体   |

## 数据类型

本文档对JSON格式中数据类型的描述做如下约定：

- `string`: 字符串类型，用双引号（"）引用
- `int`: 32位整数，主要涉及到状态码、大小、次数等
- `long`: 64位整数，主要涉及到Id和时间戳
- `float`: 浮点数，主要涉及到金额和价格，建议程序中使用高精度浮点型
- `object`: 对象，包含一个子对象{}
- `array`: 数组，包含多个对象

## 最佳实践

###安全类

- 强烈建议：在申请API Key时，请绑定您的IP地址，以此来保证您的API Key仅能在您自己的IP上使用。另外，在API Key未绑定IP时，有效期为90天，绑定IP后，则永远不会过期。
- 强烈建议：不要将API Key暴露给任何人（包括第三方软件或机构），API Key代表了您的账户权限，API Key的暴露可能会对您的信息、资金造成损失，若API Key泄露，请尽快删除并重新创建。

###公共类
**API访问建议**

- 不建议在中国大陆境内使用临时域名以及代理的方式访问Huobi API，此类方式访问API连接的稳定性很难保证。
- 建议使用日本AWS云服务器进行访问。
- 官方域名api.huobi.sg, api-aws.huobi.sg，若您使用了AWS云服务，建议使用api-aws.huobi.sg域名，该域名为AWS用户做了链路上的优化，链路延迟相对更低。

**新限频规则**

- 当前最新限频规则正在逐步上线中，已单独标注限频值的接口适用新限频规则。

- 用户可根据Http Header中“X-HB-RateLimit-Requests-Remain（限频剩余次数）”，“X-HB-RateLimit-Requests-Expire（窗口过期时间）”查看当前限频使用情况，以及所在时间窗口的过期时间，根据该数值动态调整您的请求频率。

- 同一UID下各API Key同时对某单个节点请求的频率不能超出单位时间内该节点最大允许访问次数的限制。

###行情类
**行情类数据的获取**

- 行情类数据推荐使用WebSocket方式实时接收数据变化的推送，并在程序中进行数据的缓存，WebSocket方式实时性更高，且不受限频的影响。
- 建议用户不要在同一条WebSocket连接中订阅过多的主题和币种对，否则可能会因为上游数据量过大，导致网络阻塞，以至于连接断连。

**最新成交价格的获取**

- 推荐使用WebSocket的方式订阅`market.$symbol.trade.detail`主题，该主题为逐笔成交信息推送，该数据中成交的Price即为最新成交价格，且实时性更高。

**盘口深度的获取**

- 若对盘口数据的要求仅为买一卖一，可使用WebSocket订阅`market.$symbol.bbo`主题，该主题会在买一卖一变更时进行推送。
- 若需要多档数据，且对数据的实时性要求不高的情况下，可使用WebSocket订阅`market.$symbol.depth.$type`主题，该主题推送周期为1秒。
- 若需要多档数据，且对数据的实时性要求较高的情况下，可使用WebSocket订阅`market.$symbol.mbp.$levels`主题，并使用该主题发送req请求，构建本地深度，并增量跟新，该主题增量消息推送最快周期为100ms。
- 建议使用Rest（`/market/depth`）、WebSocket全量推送（`market.$symbol.depth.$type`）获取深度时，根据version字段对数据进行去重（舍弃较小的version）；使用WebSocket增量推送（`market.$symbol.mbp.$levels`）时，根据seqNum字段进行去重（舍弃较小的seqNum）。

**最新成交的获取**

- 建议订阅WebSocket成交明细（`market.$symbol.trade.detail`）主题时，可根据tradeId字段对数据进行去重。

###订单类
**下单接口（/v1/order/orders/place）**

- 建议用户下单前根据`/v1/common/symbols`接口中返回的币种对参数数据对下单价格、下单数量等参进行校验，避免产生无效的下单请求。
- 推荐下单时携带`client-order-id`参数，且建议用户保证该参数的唯一性（每次发送请求时都不同，且唯一），该参数能够防止在发起下单请求时由于网络或其他原因造成接口超时或没有返回的情况，在此情况下，可根据`client-order-id`对WebSocket中推送过来的数据进行验证，或使用`/v1/order/orders/getClientOrder`接口查询该订单信息。 （对于用户下单时传入的clientOrderId 的唯一性不进行校验，若发生多笔订单使用同一clientOrderId的情况，查询/撤单时将返回该clientOrderId对映的最近一笔订单。）

**搜索历史订单（/v1/order/orders）**

- 推荐使用`start-time`、`end-time`参数进行查询，该参数传入值为13位时间戳（精确至毫秒），使用该参数查询时最大查询窗口为48小时（2天），推荐按照小时进行查询，您搜索的时间范围越小，时间戳准确性越高，查询的效率会更高，可以根据上次查询的时间戳进行迭代查询。

**订单状态变化的通知**

- 建议使用WebSocket订阅`orders.$symbol.update`主题，该主题拥有更低的数据延迟以及更准确的消息顺序。
- 不建议使用WebSocket订阅`orders.$symbol`主题，该主题已由`orders.$symbol.update`取代，会在后续停止服务，请尽早更换使用。

###账户类
**资产变更**

- 使用WebSocket的方式，同时订阅`orders.$symbol.update`、`accounts.update#${mode}`主题，`orders.$symbol.update`用于接收订单的状态变化（创建、成交、撤销以及相关成交价格、数量信息），由于该主题在推送数据时，未经过清算，所以时效性更快，可根据`accounts.update#${mode}`主题接收相关资产的变更信息，以此来维护账户内的资金情况。
- 不建议WebSocket订阅`accounts`主题，该主题已由`accounts.update#${mode}`取代，会在后续停止服务，请尽早更换使用。

# 联系我们

## 做市商项目

欢迎有优秀 maker 策略且交易量大的用户参与长期做市商项目。如果您的火币新加坡现货账户有折合大于10BTC资产，请提供以下信息发送邮件至：

- customersupport@huobi.sg （现货 ）做市商申请；

1. 提供 UID （需不存在返佣关系的 UID）；
2. 提供其他交易平台 maker 交易量截图证明（比如30天内成交量，或者 VIP 等级等）；
3. 请简要阐述做市方法，不需要细节。 

<aside class="notice">
做市商项目不支持点卡抵扣、VIP、交易量相关活动以及任何形式的返佣活动。
</aside>

联系

## 技术支持

使用过程中如有问题或者建议，您可选择以下任一方式联系我们：

- 通过官网的“帮助中心”或者发送邮件至customersupport@huobi.sg联系客服。

如您遇到API错误，请按照如下模板向我们反馈问题。

`1. 问题描述`  
`2. 问题发生的用户Id(UID)，账户Id和订单Id(如果和账户、订单有关系)`  
`3. 完整的URL请求`  
`4. 完整的JSON格式的请求参数（如果有）`  
`5. 完整的JSON格式的返回结果`  
`6. 问题出现时间和频率（如何时开始出现，是否可以重现）`  
`7. 签名前字符串（如果是签名认证错误）`  

下方是一个应用了模版的例子：

`1. 问题简要说明：签名错误`   
`2. UID：123456`  
`3. 完整的URL请求：GET https://api.huobi.sg/v1/account/accounts?&SignatureVersion=2&SignatureMethod=HmacSHA256&Timestamp=2019-11-06T03%3A25%3A39&AccessKeyId=rfhxxxxx-950000847-boooooo3-432c0&Signature=HhJwApXKpaLPewiYLczwfLkoTPnFPHgyF61iq0iTFF8%3D`  
`4. 完整的JSON格式的参数：无`     
`5. 完整的JSON格式的返回：{"status":"error","err-code":"api-signature-not-valid","err-msg":"Signature not valid: Incorrect Access key [Access key错误]","data":null}`  
`6. 问题出现频率：每次都会出现`  
`7. 签名前字符串`    
`GET\n`  
`api.huobi.sg\n`  
`/v1/account/accounts\n`   
`AccessKeyId=rfhxxxxx-950000847-boooooo3-432c0&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2019-11-06T03%3A26%3A13`   

注意：Access Key仅能证明您的身份，不会影响您账户的安全。切记**不**要将Secret Key信息分享给任何人，若您不小心将Secret Key暴露，请尽快[删除](https://www.huobi.sg/zh-cn/login/?backUrl=%2Fzh-cn%2Fapikey%2F)其对应的API Key，以免造成您的账户损失。

# 行情数据

## 简介

行情数据接口提供了多种K线、深度以及最新成交记录等行情数据。

行情接口提供的数据每1分钟更新一次


## K 线数据（蜡烛图）

此接口返回历史K线数据。K线周期以新加坡时间为基准开始计算，例如日K线的起始周期为新加坡时间0时至新加坡时间次日0时。

<aside class="notice">当前 REST API 不支持自定义时间区间，如需要历史固定时间范围的数据，请参考 Websocket API 中的 K 线接口。</aside>
<aside class="notice">获取 btc 净值时， symbol 请填写 “btc”。</aside>

```shell
curl "https://api.huobi.sg/market/history/kline?period=1day&size=200&symbol=ethbtc"
```

### HTTP 请求

- GET `/market/history/kline`

### 请求参数

| 参数   | 数据类型 | 是否必须 | 默认值 | 描述                                       | 取值范围                                                     |
| ------ | -------- | -------- | ------ | ------------------------------------------ | ------------------------------------------------------------ |
| symbol | string   | true     | NA     | 交易对                                     | ethbtc                                                       |
| period | string   | true     | NA     | 返回数据时间粒度，也就是每根蜡烛的时间区间 | 1min, 5min, 15min, 30min, 60min, 4hour, 1day, 1mon, 1week, 1year |
| size   | integer  | false    | 150    | 返回 K 线数据条数                          | [1, 2000]                                                    |

> Response:

```json
[  {    "id": 1499184000,    "amount": 37593.0266,    "count": 0,    "open": 1935.2000,    "close": 1879.0000,    "low": 1856.0000,    "high": 1940.0000,    "vol": 71031537.97866500  }]
```

### 响应数据

| 字段名称 | 数据类型 | 描述                                                    |
| -------- | -------- | ------------------------------------------------------- |
| id       | long     | 调整为新加坡时间的时间戳，单位秒，并以此作为此K线柱的id |
| amount   | float    | 以基础币种计量的交易量                                  |
| count    | integer  | 交易次数                                                |
| open     | float    | 本阶段开盘价                                            |
| close    | float    | 本阶段收盘价                                            |
| low      | float    | 本阶段最低价                                            |
| high     | float    | 本阶段最高价                                            |
| vol      | float    | 以报价币种计量的交易量                                  |



## 聚合行情（Ticker）

此接口获取ticker信息同时提供最近24小时的交易聚合信息。

```shell
curl "https://api.huobi.sg/market/detail/merged?symbol=ethbtc"
```

### HTTP 请求

- GET `/market/detail/merged`

### 请求参数

| 参数   | 数据类型 | 是否必须 | 默认值 | 描述   | 取值范围                                              |
| ------ | -------- | -------- | ------ | ------ | ----------------------------------------------------- |
| symbol | string   | true     | NA     | 交易对 | ltcbtc, ethbtc...（取值参考`GET /v1/common/symbols`） |

> Response:

```json
{  "id":1499225271,  "ts":1499225271000,  "close":1885.0000,  "open":1960.0000,  "high":1985.0000,  "low":1856.0000,  "amount":81486.2926,  "count":42122,  "vol":157052744.85708200,  "ask":[1885.0000,21.8804],  "bid":[1884.0000,1.6702]}
```

### 响应数据

| 字段名称 | 数据类型 | 描述                                     |
| -------- | -------- | ---------------------------------------- |
| id       | long     | NA                                       |
| amount   | float    | 以基础币种计量的交易量（以滚动24小时计） |
| count    | integer  | 交易次数（以滚动24小时计）               |
| open     | float    | 本阶段开盘价（以滚动24小时计）           |
| close    | float    | 本阶段最新价（以滚动24小时计）           |
| low      | float    | 本阶段最低价（以滚动24小时计）           |
| high     | float    | 本阶段最高价（以滚动24小时计）           |
| vol      | float    | 以报价币种计量的交易量（以滚动24小时计） |
| bid      | object   | 当前的最高买价 [price, size]             |
| ask      | object   | 当前的最低卖价 [price, size]             |

## 所有交易对的最新 Tickers

获得所有交易对的 tickers。

```shell
curl "https://api.huobi.sg/market/tickers"
```

<aside class="notice">此接口返回所有交易对的 ticker，因此数据量较大。</aside>

### HTTP 请求

- GET `/market/tickers`

### 请求参数

此接口不接受任何参数。

> Response:

```json
[      {          "open":0.044297,      // 开盘价        "close":0.042178,     // 收盘价        "low":0.040110,       // 最低价        "high":0.045255,      // 最高价        "amount":12880.8510,          "count":12838,        "vol":563.0388715740,        "symbol":"ethbtc",        "bid":0.007545,        "bidSize":0.008,        "ask":0.008088,        "askSize":0.009    },    {          "open":0.008545,        "close":0.008656,        "low":0.008088,        "high":0.009388,        "amount":88056.1860,        "count":16077,        "vol":771.7975953754,        "symbol":"ltcbtc",        "bid":0.007545,        "bidSize":0.008,        "ask":0.008088,        "askSize":0.009    }]
```

### 响应数据

核心响应数据为一个对象列，每个对象包含下面的字段

| 字段名称 | 数据类型 | 描述                                     |
| -------- | -------- | ---------------------------------------- |
| amount   | float    | 以基础币种计量的交易量（以滚动24小时计） |
| count    | integer  | 交易笔数（以滚动24小时计）               |
| open     | float    | 开盘价（以新加坡时间自然日计）           |
| close    | float    | 最新价（以新加坡时间自然日计）           |
| low      | float    | 最低价（以新加坡时间自然日计）           |
| high     | float    | 最高价（以新加坡时间自然日计）           |
| vol      | float    | 以报价币种计量的交易量（以滚动24小时计） |
| symbol   | string   | 交易对，例如ltcbtc, ethbtc               |
| bid      | float    | 买一价                                   |
| bidSize  | float    | 买一量                                   |
| ask      | float    | 卖一价                                   |
| askSize  | float    | 卖一量                                   |

## 市场深度数据

此接口返回指定交易对的当前市场深度数据。

```shell
curl "https://api.huobi.sg/market/depth?symbol=ethbtc&type=step2"
```

### HTTP 请求

- GET `/market/depth`

### 请求参数

| 参数   | 数据类型 | 必须  | 默认值 | 描述                             | 取值范围                                              |      |
| ------ | -------- | ----- | ------ | -------------------------------- | ----------------------------------------------------- | ---- |
| symbol | string   | true  | NA     | 交易对                           | Ltcbtc, ethbtc...（取值参考`GET /v1/common/symbols`） |      |
| depth  | integer  | false | 20     | 返回深度的数量                   | 5，10，20                                             |      |
| type   | string   | true  | step0  | 深度的价格聚合度，具体说明见下方 | step0，step1，step2，step3，step4，step5              |      |

<aside class="notice">当type值为‘step0’时，‘depth’的默认值为150而非20。 </aside>

**参数type的各值说明**

| 取值  | 说明                    |
| ----- | ----------------------- |
| step0 | 无聚合                  |
| step1 | 聚合度为报价精度*10     |
| step2 | 聚合度为报价精度*100    |
| step3 | 聚合度为报价精度*1000   |
| step4 | 聚合度为报价精度*10000  |
| step5 | 聚合度为报价精度*100000 |

> Response:

```json
{    "version": 31615842081,    "ts": 1489464585407,    "bids": [      [7964, 0.0678], // [price, size]      [7963, 0.9162],      [7961, 0.1],      [7960, 12.8898],      [7958, 1.2],      ...    ],    "asks": [      [7979, 0.0736],      [7980, 1.0292],      [7981, 5.5652],      [7986, 0.2416],      [7990, 1.9970],      ...    ]  }
```

### 响应数据

<aside class="notice">返回的JSON顶级数据对象名为'tick'而不是通常的'data'。</aside>

| 字段名称 | 数据类型 | 描述                               |
| -------- | -------- | ---------------------------------- |
| ts       | integer  | 调整为新加坡时间的时间戳，单位毫秒 |
| version  | integer  | 内部字段                           |
| bids     | object   | 当前的所有买单 [price, size]       |
| asks     | object   | 当前的所有卖单 [price, size]       |

## 最近市场成交记录

此接口返回指定交易对最新的一个交易记录。

```shell
curl "https://api.huobi.sg/market/trade?symbol=ethbtc"
```

### HTTP 请求

- GET `/market/trade`

### 请求参数

| 参数   | 数据类型 | 是否必须 | 默认值 | 描述                                                  |
| ------ | -------- | -------- | ------ | ----------------------------------------------------- |
| symbol | string   | true     | NA     | ltcbtc, ethbtc...（取值参考`GET /v1/common/symbols`） |

> Response:

```json
{    "id": 600848670,    "ts": 1489464451000,    "data": [      {        "id": 600848670,        "trade-id": 102043494568,        "price": 7962.62,        "amount": 0.0122,        "direction": "buy",        "ts": 1489464451000      }    ]}
```

### 响应数据

<aside class="notice">返回的JSON顶级数据对象名为'tick'而不是通常的'data'。</aside>

| 字段名称  | 数据类型 | 描述                                               |
| --------- | -------- | -------------------------------------------------- |
| id        | integer  | 唯一交易id（将被废弃）                             |
| trade-id  | integer  | 唯一成交ID（NEW）                                  |
| amount    | float    | 以基础币种为单位的交易量                           |
| price     | float    | 以报价币种为单位的成交价格                         |
| ts        | integer  | 调整为新加坡时间的时间戳，单位毫秒                 |
| direction | string   | 交易方向：“buy” 或 “sell”, “buy” 即买，“sell” 即卖 |

## 获得近期交易记录

此接口返回指定交易对近期的所有交易记录。

```shell
curl "https://api.huobi.sg/market/history/trade?symbol=ethbtc&size=2"
```

### HTTP 请求

- GET `/market/history/trade`

### 请求参数

| 参数   | 数据类型 | 是否必须 | 默认值 | 描述                                                  |
| ------ | -------- | -------- | ------ | ----------------------------------------------------- |
| symbol | string   | true     | NA     | ltcbtc, ethbtc...（取值参考`GET /v1/common/symbols`） |
| size   | integer  | false    | 1      | 返回的交易记录数量，最大值2000                        |

> Response:

```json
[     {        "id":31618787514,      "ts":1544390317905,      "data":[           {              "amount":9.000000000000000000,            "ts":1544390317905,            "trade-id": 102043483472,            "id":3161878751418918529341,            "price":94.690000000000000000,            "direction":"sell"         },         {              "amount":73.771000000000000000,            "ts":1544390317905,            "trade-id": 102043483473            "id":3161878751418918532514,            "price":94.660000000000000000,            "direction":"sell"         }      ]   },   {        "id":31618776989,      "ts":1544390311353,      "data":[           {              "amount":1.000000000000000000,            "ts":1544390311353,            "trade-id": 102043494568,            "id":3161877698918918522622,            "price":94.710000000000000000,            "direction":"buy"         }      ]   }]
```

### 响应数据

<aside class="notice">返回的数据对象是一个对象数组，每个数组元素为一个调整为新加坡时间的时间戳（单位毫秒）下的所有交易记录，这些交易记录以数组形式呈现。</aside>

| 参数      | 数据类型 | 描述                                               |
| --------- | -------- | -------------------------------------------------- |
| id        | integer  | 唯一交易id（将被废弃）                             |
| trade-id  | integer  | 唯一成交ID（NEW）                                  |
| amount    | float    | 以基础币种为单位的交易量                           |
| price     | float    | 以报价币种为单位的成交价格                         |
| ts        | integer  | 调整为新加坡时间的时间戳，单位毫秒                 |
| direction | string   | 交易方向：“buy” 或 “sell”, “buy” 即买，“sell” 即卖 |

## 最近24小时行情数据

此接口返回最近24小时的行情数据汇总。

<aside class="notice">此接口返回的成交量、成交金额为24小时滚动数据（平移窗口大小24小时），有可能会出现后一个窗口内的累计成交量、累计成交额小于前一窗口的情况。</aside>

```shell
curl "https://api.huobi.sg/market/detail?symbol=ethbtc"
```

### HTTP 请求

- GET `/market/detail`

### 请求参数

| 参数   | 数据类型 | 是否必须 | 默认值 | 描述                                                  |
| ------ | -------- | -------- | ------ | ----------------------------------------------------- |
| symbol | string   | true     | NA     | ltcbtc, ethbtc...（取值参考`GET /v1/common/symbols`） |

> Response:

```json
{     "amount":613071.438479561,   "open":86.21,   "close":94.35,   "high":98.7,   "id":31619471534,   "count":138909,   "low":84.63,   "version":31619471534,   "vol":5.6617373443873316E7}
```

### 响应数据

<aside class="notice">返回的JSON顶级数据对象名为'tick'而不是通常的'data'。</aside>

| 字段名称 | 数据类型 | 描述                                     |
| -------- | -------- | ---------------------------------------- |
| id       | integer  | 响应id                                   |
| amount   | float    | 以基础币种计量的交易量（以滚动24小时计） |
| count    | integer  | 交易次数（以滚动24小时计）               |
| open     | float    | 本阶段开盘价（以滚动24小时计）           |
| close    | float    | 本阶段收盘价（以滚动24小时计）           |
| low      | float    | 本阶段最低价（以滚动24小时计）           |
| high     | float    | 本阶段最高价（以滚动24小时计）           |
| vol      | float    | 以报价币种计量的交易量（以滚动24小时计） |
| version  | integer  | 内部数据                                 |

### HTTP 请求

- GET `/market/etp`

## 常见错误码

以下是行情数据接口返回的错误码、错误消息以及说明。

| 错误码            | 错误消息                            | 说明                    |
| ----------------- | ----------------------------------- | ----------------------- |
| invalid-parameter | invalid symbol                      | 无效的交易对            |
| invalid-parameter | invalid period                      | 请求K线，period参数错误 |
| invalid-parameter | invalid depth                       | 深度depth参数错误       |
| invalid-parameter | invalid type                        | 深度type 参数错误       |
| invalid-parameter | invalid size                        | size参数错误            |
| invalid-parameter | invalid size,valid range: [1, 2000] | size参数错误            |
| invalid-parameter | request timeout                     | 请求超时                |

# 账户相关

## 简介

账户相关接口提供了账户、余额、历史、点卡等查询以及资产划转等功能。

<aside class="notice">访问账户相关的接口需要进行签名认证。</aside>

## 账户信息 

API Key 权限：读取<br>
限频值（NEW）：100次/2s

查询当前用户的所有账户 ID `account-id` 及其相关信息

### HTTP 请求

- GET `/v1/account/accounts`

### 请求参数

无

> Response:

```json
{  "data": [    {      "id": 100001,      "type": "spot",      "subtype": "",      "state": "working"    }  ]}
```

### 响应数据

| 参数名称 | 是否必须 | 数据类型 | 描述       | 取值范围                        |
| -------- | -------- | -------- | ---------- | ------------------------------- |
| id       | true     | long     | account-id |                                 |
| state    | true     | string   | 账户状态   | working：正常, lock：账户被锁定 |
| type     | true     | string   | 账户类型   | spot：现货账户                  |


## 账户余额

API Key 权限：读取<br>
限频值（NEW）：100次/2s

查询指定账户的余额，支持以下账户：

spot：现货账户

### HTTP 请求

- GET `/v1/account/accounts/{account-id}/balance`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 描述                                                         | 默认值 | 取值范围 |
| ---------- | -------- | ------ | ------------------------------------------------------------ | ------ | -------- |
| account-id | true     | string | account-id，填在 path 中，取值参考 `GET /v1/account/accounts` |        |          |

> Response:

```json
{  "data": {    "id": 100009,    "type": "spot",    "state": "working",    "list": [      {        "currency": "btc",        "type": "trade",        "balance": "5007.4362872650"      },      {        "currency": "btc",        "type": "frozen",        "balance": "348.1199920000"      }    ]  }}
```

### 响应数据

| 参数名称 | 是否必须 | 数据类型 | 描述     | 取值范围                        |
| -------- | -------- | -------- | -------- | ------------------------------- |
| id       | true     | long     | 账户 ID  |                                 |
| state    | true     | string   | 账户状态 | working：正常  lock：账户被锁定 |
| type     | true     | string   | 账户类型 | spot：现货账户                  |
| list     | false    | Array    |          |                                 |

list字段说明

| 参数名称 | 是否必须 | 数据类型 | 描述 | 取值范围                                      |
| -------- | -------- | -------- | ---- | --------------------------------------------- |
| balance  | true     | string   | 余额 |                                               |
| currency | true     | string   | 币种 |                                               |
| type     | true     | string   | 类型 | trade: 交易余额，frozen: 冻结余额, lock: 锁仓 |

## 获取平台资产总估值

API Key 权限：读取

限频值（NEW）：100次/2s

按照BTC或法币计价单位，获取平台账户的总资产估值。

### HTTP 请求

- GET `/v2/account/valuation`

### 请求参数

| 参数              | 是否必填 | 数据类型 | 描述                                                   | 默认值 | 取值范围 |
| ----------------- | -------- | -------- | ------------------------------------------------------ | ------ | -------- |
| accountType       | false    | string   | 账户类型，详见账户类型数据字典                         |        |          |
| valuationCurrency | false    | string   | 不填默认为btc估值（目前暂只支持BTC估值，参数值需大写） |        |          |

> Responds:

```lang=json
{    "message": null,    "success": true,    "code":200,    "data":"{        "todayProfit": null,        "updated": null,        "totalBalance": "68232.925885978428351309",        "todayProfitRate": null,        "profitAccountBalanceList": [            {                "distributionType": "1",                "success": true,                "accountBalance": "68232.925885978428351309"            },            {                "distributionType": "2",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "3",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "4",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "5",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "6",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "7",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "8",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "9",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "10",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "11",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "12",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "13",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "14",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "15",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "16",                "success": false,                "accountBalance": "0"            }        ]        }"}
```

### 响应数据

| 参数名称       | 数据类型             | 描述                                              |
| -------------- | -------------------- | ------------------------------------------------- |
| accountList    | List<AccountBalance> | 账户资产列表                                      |
| {accountType   | String               | 账户类型                                          |
| accountBalance | String               | 账户资产                                          |
| success}       | Boolean              | 账户资产是否成功获取,为false时accountBalance返回0 |
| timestamp      | long                 | 数据返回时间，为unix time in millisecond          |

### 账户类型数据字典

| code | 说明     |
| ---- | -------- |
| 1    | 币币账户 |



## 获取指定账户资产估值（现货）

API Key 权限：读取

限频值（NEW）：100次/2s

按照BTC或法币计价单位，获取指定账户的总资产估值。

### HTTP 请求

- GET `/v2/account/asset-valuation`

### 请求参数

| 参数              | 是否必填 | 数据类型 | 描述                                           | 默认值 | 取值范围                            |
| ----------------- | -------- | -------- | ---------------------------------------------- | ------ | ----------------------------------- |
| accountType       | true     | string   | 账户类型                                       | NA     | spot：现货账户                      |
| valuationCurrency | false    | string   | 资产估值法币，即资产按哪个法币为单位进行估值。 | BTC    | 可选法币有：USD、SGD （大小写敏感） |

> Responds:

```json
{    "code": 200,    "data": {        "balance": "34.75",        "timestamp": 1594901254363    },    "ok": true}
```

### 返回字段

| 参数      | 是否必须 | 数据类型 | 说明                                     |
| --------- | -------- | -------- | ---------------------------------------- |
| balance   | true     | string   | 按照某一个法币为单位的总资产估值         |
| timestamp | true     | long     | 数据返回时间，为unix time in millisecond |


## 资产划转

API Key 权限：交易<br>

其他划转功能将逐步上线，敬请期待。<br>

### HTTP 请求

- POST `/v1/account/transfer`

### 请求参数

| 参数         | 是否必填 | 数据类型 | 说明                                | 取值范围                         |
| ------------ | -------- | -------- | ----------------------------------- | -------------------------------- |
| from-account | true     | long     | 转出账户id                          |                                  |
| to-account   | true     | long     | 转入账户id                          |                                  |
| currency     | true     | string   | 币种，即btc, ltc, bch, eth, etc ... | 取值参考GET /v1/common/currencys |
| amount       | true     | string   | 划转金额                            |                                  |


> Response:

```json
{    "status": "ok",    "data": {        "transact-id": 220521190,        "transact-time": 1590662591832    }}
```

### 响应数据

| 参数            | 是否必须 | 数据类型 | 说明       | 取值范围        |
| --------------- | -------- | -------- | ---------- | --------------- |
| status          | true     | string   | 状态       | "ok" or "error" |
| data            | true     | list     |            |                 |
| { transact-id   | true     | int      | 交易流水号 |                 |
| transact-time } | true     | long     | 交易时间   |                 |
| </data>         |          |          |            |                 |


## 账户流水

API Key 权限：读取<br>
限频值（NEW）：5次/2s

该节点基于用户账户ID返回账户流水。

### HTTP Request

- GET `/v1/account/history`

### 请求参数

| 参数名称       | 是否必需 | 数据类型 | 描述                                                         | 缺省值               | 取值范围                                                     |
| -------------- | -------- | -------- | ------------------------------------------------------------ | -------------------- | ------------------------------------------------------------ |
| account-id     | true     | string   | 账户编号,取值参考 `GET /v1/account/accounts`                 |                      |                                                              |
| currency       | false    | string   | 币种,即btc, ltc, bch, eth, etc ...(取值参考`GET /v1/common/currencys`) |                      |                                                              |
| transact-types | false    | string   | 变动类型，可多选，以逗号分隔，包含动账类型列表详见注3        | all                  | trade (交易), transact-fee（交易手续费）, transfer（划转）, deposit（充币），withdraw（提币）, withdraw-fee（提币手续费）, exchange（兑换）, other-types（其他） |
| start-time     | false    | long     | 远点时间 unix time in millisecond. 以transact-time为key进行检索. 查询窗口最大为1小时. 窗口平移范围为最近30天. | ((end-time) – 1hour) | [((end-time) – 1hour), (end-time)]                           |
| end-time       | false    | long     | 近点时间unix time in millisecond. 以transact-time为key进行检索. 查询窗口最大为1小时. 窗口平移范围为最近30天. | current-time         | [(current-time) – 29days,(current-time)]                     |
| sort           | false    | string   | 检索方向                                                     | asc                  | asc or desc                                                  |
| size           | false    | int      | 最大条目数量                                                 | 100                  | [1,500]                                                      |
| from-id        | false    | long     | 起始编号（仅在下页查询时有效，见注2）                        |                      |                                                              |

> Response:

```json
{    "status": "ok",    "data": [        {            "account-id": 5260185,            "currency": "btc",            "transact-amt": "0.002393000000000000",            "transact-type": "transfer",            "record-id": 89373333576,            "avail-balance": "0.002393000000000000",            "acct-balance": "0.002393000000000000",            "transact-time": 1571393524526        },        {            "account-id": 5260185,            "currency": "btc",            "transact-amt": "-0.002393000000000000",            "transact-type": "transfer",            "record-id": 89373382631,            "avail-balance": "0E-18",            "acct-balance": "0E-18",            "transact-time": 1571393578496        }    ]}
```

### 响应数据

| 字段名称      | 数据类型 | 描述                                                        | 取值范围     |
| ------------- | -------- | ----------------------------------------------------------- | ------------ |
| status        | string   | 状态码                                                      | "ok","error" |
| data          | object   |                                                             |              |
| { account-id  | long     | 账户编号                                                    |              |
| currency      | string   | 币种                                                        |              |
| transact-amt  | string   | 变动金额（入账为正 or 出账为负）                            |              |
| transact-type | string   | 变动类型                                                    |              |
| avail-balance | string   | 可用余额                                                    |              |
| acct-balance  | string   | 账户余额                                                    |              |
| transact-time | long     | 交易时间（数据库记录时间）                                  |              |
| record-id }   | long     | 数据库记录编号（全局唯一）                                  |              |
| next-id       | long     | 下页起始编号（仅在查询结果需要分页返回时包含此字段，见注2） |              |

注1：<br>
账户流水中返回的交易返佣为到账金额，多笔成交产生的多笔返佣可能会合并到帐，成为一笔流水。<br>

注2：<br>
仅当用户请求查询的时间范围内的数据条目超出单页限制（由“size“字段设定）时，服务器才返回”next-id“字段。用户收到服务器返
回的”next-id“后 –<br>
1） 须知晓后续仍有数据未能在本页返回；<br>
2） 如需继续查询下页数据，应再次请求查询并将服务器返回的“next-id”作为“from-id“，其它请求参数不变。<br>
3） 作为数据库记录ID，“next-id”和“from-id”除了用来翻页查询外，无其它业务含义。<br>

注3：<br>
变动类型包含动账类型明细列表：

| 变动类型             | 动账类型                      | 描述                  |
| -------------------- | ----------------------------- | --------------------- |
| trade                | match-income                  | 撮合成交收入          |
| transfer             | spot-generic-transfer-in      | 币币账户 通用划转划入 |
| transfer{ account-id | spot-generic-transfer-outlong | 币币账户 通用划转转出 |
| deposit              | user-account-deposit          | 用户账户充值转账      |
| withdraw             | user-account-withdraw         | 用户账户提现转账      |


## 财务流水

API Key 权限：读取

该节点基于用户账户ID返回财务流水。<br>
一期上线暂时仅支持划转流水的查询（“transactType” = “transfer”）。<br>
通过“startTime”/“endTime”框定的查询窗口最大为10天，意即，通过单次查询可检索的范围最大为10天。<br>
该查询窗口可在最近180天范围内平移，意即，通过多次平移窗口查询，最多可检索到过往180天的记录。<br>

### HTTP Request

- GET `/v2/account/ledger`

### 请求参数

| 参数名称      | 数据类型 | 是否必需 | 描述                                                |
| ------------- | -------- | -------- | --------------------------------------------------- |
| accountId     | string   | TRUE     | 账户编号                                            |
| currency      | string   | FALSE    | 币种 （缺省值所有币种）                             |
| transactTypes | string   | FALSE    | 变动类型，可多填 （缺省值all） 枚举值： transfer    |
| startTime     | long     | FALSE    | 远点时间（取值范围及缺省值见注1）                   |
| endTime       | long     | FALSE    | 近点时间（取值范围及缺省值见注2）                   |
| sort          | string   | FALSE    | 检索方向（asc 由远及近, desc 由近及远，缺省值desc） |
| limit         | int      | FALSE    | 单页最大返回条目数量 [1,500] （缺省值100）          |
| fromId        | long     | FALSE    | 起始编号（仅在下页查询时有效，见注3）               |

注1：<br>
startTime取值范围：[(endTime - 10天), endTime], unix time in millisecond<br>
startTime缺省值：(endTime - 10天)

注2：<br>
endTime取值范围：[(当前时间 - 180天), 当前时间], unix time in millisecond<br>
endTime缺省值：当前时间

> Response:

```json
{"code": 200,"message": "success","data": [    {        "accountId": 5260185,        "currency": "btc",        "transactAmt": 1.000000000000000000,        "transactType": "transfer",        "transferType": "margin-transfer-out",        "transactId": 0,        "transactTime": 1585573286913,        "transferer": 5463409,        "transferee": 5260185    },    {        "accountId": 5260185,        "currency": "btc",        "transactAmt": -1.000000000000000000,        "transactType": "transfer",        "transferType": "margin-transfer-in",        "transactId": 0,        "transactTime": 1585573281160,        "transferer": 5260185,        "transferee": 5463409    }]}
```

### 响应数据

| 字段名称     | 数据类型 | 是否必需 | 描述                                                         | 取值范围         |
| ------------ | -------- | -------- | ------------------------------------------------------------ | ---------------- |
| code         | integer  | TRUE     | 状态码                                                       |                  |
| message      | string   | FALSE    | 错误描述（如有）                                             |                  |
| data         | object   | TRUE     | 按用户请求参数sort中定义的顺序排列                           |                  |
| { accountId  | integer  | TRUE     | 账户编号                                                     |                  |
| currency     | string   | TRUE     | 币种                                                         |                  |
| transactAmt  | number   | TRUE     | 变动金额（入账为正 or 出账为负）                             |                  |
| transactType | string   | TRUE     | 变动类型                                                     | transfer（划转） |
| transferType | string   | FALSE    | 划转类型（仅对transactType=transfer有效）                    |                  |
| transactId   | integer  | TRUE     | 交易流水号                                                   |                  |
| transactTime | integer  | TRUE     | 交易时间                                                     |                  |
| transferer   | integer  | FALSE    | 付款方账户ID                                                 |                  |
| transferee } | integer  | FALSE    | 收款方账户ID                                                 |                  |
| nextId       | integer  | FALSE    | 下页起始编号（仅在查询结果需要分页返回时包含此字段，见注3。） |                  |

注3：<br>
仅当用户请求查询的时间范围内的数据条目超出单页限制（由“limit“字段设定）时，服务器才返回”nextId“字段。用户收到服务器返回的”nextId“后 –<br>
1）	须知晓后续仍有数据未能在本页返回；<br>
2）	如需继续查询下页数据，应再次请求查询并将服务器返回的“nextId”作为“fromId“，其它请求参数不变。<br>
3）	作为数据库记录ID，“nextId”和“fromId”除了用来翻页查询外，无其它业务含义。<br>

# 钱包（充提相关）

## 简介

充提相关接口提供了充提记录等查询功能。

<aside class="notice">访问充提相关的接口需要进行签名认证。</aside>

## 充提记录

此节点用于查询充提记录

API Key 权限：读取<br>
限频值（NEW）：20次/2s

### HTTP 请求

- GET `/v1/query/deposit-withdraw`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 描述             | 默认值                                                       | 取值范围                                                     |
| -------- | -------- | ------ | ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| currency | false    | string | 币种             |                                                              | btc, ltc, bch, eth, etc ...(取值参考`GET /v1/common/currencys`) |
| type     | true     | string | 充值或提币       |                                                              | deposit 或 withdraw,子用户仅可用deposit                      |
| from     | false    | string | 查询起始 ID      | 缺省时，默认值direct相关。当direct为‘prev’时，from 为1 ，从旧到新升序返回；当direct为’next‘时，from为最新的一条记录的ID，从新到旧降序返回 |                                                              |
| size     | false    | string | 查询记录大小     | 100                                                          | 1-500                                                        |
| direct   | false    | string | 返回记录排序方向 | 缺省时，默认为“prev” （升序）                                | “prev” （升序）or “next” （降序）                            |

> Response:

```json
{  "data":    [      {        "id": 1171,        "type": "deposit",        "currency": "xrp",        "tx-hash": "ed03094b84eafbe4bc16e7ef766ee959885ee5bcb265872baaa9c64e1cf86c2b",        "amount": 7.457467,        "address": "rae93V8d2mdoUQHwBDBdM4NHCMehRJAsbm",        "address-tag": "100040",        "fee": 0,        "state": "safe",        "created-at": 1510912472199,        "updated-at": 1511145876575      },      ...    ]}
```

### 响应数据

| 参数名称    | 是否必须 | 数据类型 | 描述                                                         | 取值范围                                 |
| ----------- | -------- | -------- | ------------------------------------------------------------ | ---------------------------------------- |
| id          | true     | long     | 充币或者提币订单id，翻页查询时from参数取自此值               |                                          |
| type        | true     | string   | 类型                                                         | 'deposit', 'withdraw', 子用户仅有deposit |
| currency    | true     | string   | 币种                                                         |                                          |
| tx-hash     | true     | string   | 交易哈希。                                                   |                                          |
| chain       | true     | string   | 链名称                                                       |                                          |
| amount      | true     | float    | 个数                                                         |                                          |
| address     | true     | string   | 目的地址                                                     |                                          |
| address-tag | true     | string   | 地址标签                                                     |                                          |
| fee         | true     | float    | 手续费                                                       |                                          |
| state       | true     | string   | 状态                                                         | 状态参见下表                             |
| error-code  | false    | string   | 提币失败错误码，仅type为”withdraw“，且state为”reject“、”wallet-reject“和”failed“时有。 |                                          |
| error-msg   | false    | string   | 提币失败错误描述，仅type为”withdraw“，且state为”reject“、”wallet-reject“和”failed“时有。 |                                          |
| created-at  | true     | long     | 发起时间                                                     |                                          |
| updated-at  | true     | long     | 最后更新时间                                                 |                                          |


- 虚拟币充值状态定义：

| 状态       | 描述                                 |
| ---------- | ------------------------------------ |
| unknown    | 状态未知                             |
| confirming | 区块确认中                           |
| confirmed  | 区块已完成，已经上账，可以划转和交易 |
| safe       | 区块已确认，可以提币                 |
| orphan     | 区块已被孤立                         |

- 虚拟币提币状态定义：

| 状态            | 描述         |
| --------------- | ------------ |
| verifying       | 待验证       |
| failed          | 验证失败     |
| submitted       | 已提交       |
| reexamine       | 审核中       |
| canceled        | 已撤销       |
| pass            | 审批通过     |
| reject          | 审批拒绝     |
| pre-transfer    | 处理中       |
| wallet-transfer | 已汇出       |
| wallet-reject   | 钱包拒绝     |
| confirmed       | 区块已确认   |
| confirm-error   | 区块确认错误 |
| repealed        | 已撤销       |

## 常见错误码

以下是充提相关接口返回的返回码、返回消息以及说明。

| 返回码 | 返回消息                             | 说明         |
| ------ | ------------------------------------ | ------------ |
| 200    | success                              | 请求成功     |
| 500    | error                                | 系统错误     |
| 1002   | unauthorized                         | 未授权       |
| 1003   | invalid signature                    | 验签失败     |
| 2002   | invalid field value in "field name"  | 非法字段取值 |
| 2003   | missing mandatory field "field name" | 强制字段缺失 |



# 现货 

## 简介

现货交易接口提供了下单、撤单、订单查询、成交明细查询、手续费率查询等功能。

<aside class="notice">访问交易相关的接口需要进行签名认证。</aside>

以下是订单业务相关的字段说明

**订单类型 (type)**：订单类型由方向和行为类型组合而成，[方向]-[行为类型]

方向：

- buy: 买
- sell: 卖

行为类型：

- market：市价单，该类型订单仅需指定下单金额或下单数量，不需要指定价格，订单在进入撮合时，会直接与对手方进行成交，直至金额或数量低于最小成交金额或成交数量为止。
- limit：限价单，该类型订单需指定下单价格，下单数量。

**订单来源 (source)**：

- spot-api：现货API交易

  

**订单状态 (state)**:

- created：已创建，该状态订单尚未进入撮合队列。
- submitted : 已挂单等待成交，该状态订单已进入撮合队列当中。
- partial-filled : 部分成交，该状态订单在撮合队列当中，订单的部分数量已经被市场成交，等待剩余部分成交。
- filled : 已成交。该状态订单不在撮合队列中，订单的全部数量已经被市场成交。
- partial-canceled : 部分成交撤销。该状态订单不在撮合队列中，此状态由partial-filled转化而来，订单数量有部分被成交，但是被撤销。
- canceling : 撤销中。该状态订单正在被撤销的过程中，因订单最终需在撮合队列中剔除才会被真正撤销，所以此状态为中间过渡态。
- canceled : 已撤销。该状态订单不在撮合订单中，此状态订单没有任何成交数量，且被成功撤销。

**相关ID**

- order-id : 订单的唯一编号

- client-order-id : 客户自定义ID，该ID在下单时传入，与下单成功后返回的order-id对应。

  client-order-id 时效：对于已完结状态订单，2小时内有效。（其他状态订单有效时间仍为8小时有效）即订单创建超过2h，将无法使用clientOrderId查询已完结状态订单，建议用户通过orderid进行查询。其中，已完结订单状态包括部分成交已撤销、已撤销和完全成交。

- 。 允许的字符包括字母(大小写敏感)、数字、下划线 (_)和横线(-)，最长64位

- match-id : 订单在撮合中的顺序编号

- trade-id : 成交的唯一编号

## 下单

API Key 权限：交易
限频值；100次/2s

发送一个新订单到火币新加坡以进行撮合。

### HTTP 请求

- POST ` /v1/order/orders/place`

> Request:

```json
{  "account-id": "100009",  "amount": "10.1",  "price": "100.1",  "source": "api",  "symbol": "ethbtc",  "type": "buy-limit",  "client-order-id": "a0001"}
```

### 请求参数

| 参数名称        | 数据类型 | 是否必需 | 默认值   | 描述                                                         |
| --------------- | -------- | -------- | -------- | ------------------------------------------------------------ |
| account-id      | string   | true     | NA       | 账户 ID，取值参考 `GET /v1/account/accounts`。现货交易使用 ‘spot’ 账户的 account-id |
| symbol          | string   | true     | NA       | 交易对,即ltcbtc, ethbtc...（取值参考`GET /v1/common/symbols`） |
| type            | string   | true     | NA       | 订单类型，包括buy-market, sell-market, buy-limit, sell-limit,（说明见下文） |
| amount          | string   | true     | NA       | 订单交易量（市价买单为订单交易额）                           |
| price           | string   | false    | NA       | 订单价格（对市价单无效）                                     |
| source          | string   | false    | spot-api | 现货交易填写“spot-api”                                       |
| client-order-id | string   | false    | NA       | 用户自编订单号（最大长度64个字符，须在8小时内保持唯一性）    |


**buy-limit-maker**

当“下单价格”>=“市场最低卖出价”，订单提交后，系统将拒绝接受此订单；

当“下单价格”<“市场最低卖出价”，提交成功后，此订单将被系统接受。

**sell-limit-maker**

当“下单价格”<=“市场最高买入价”，订单提交后，系统将拒绝接受此订单；

当“下单价格”>“市场最高买入价”，提交成功后，此订单将被系统接受。

> Response:

```json
{    "data": "59378"}
```

### 响应数据

返回的主数据对象是一个对应下单单号的字符串。

如client order ID（在8小时内）被复用，节点将返回错误消息invalid.client.order.id。

## 批量下单

API Key 权限：交易<br>
限频值（NEW）：50次/2s<br>

一个批量最多10张订单

### HTTP 请求

- POST ` /v1/order/batch-orders`

> Request:

```json
[	{    "account-id": "123456",    "price": "7801",    "amount": "0.001",    "symbol": "ethbtc",    "type": "sell-limit",    "client-order-id": "c1"	},	{    "account-id": "123456",    "price": "7802",    "amount": "0.001",    "symbol": "ethbtc",    "type": "sell-limit",    "client-order-id": "d2"	}]
```

### 请求参数

| 参数名称        | 数据类型 | 是否必需 | 默认值   | 描述                                                         |
| --------------- | -------- | -------- | -------- | ------------------------------------------------------------ |
| [{ account-id   | string   | true     | NA       | 账户 ID，取值参考 `GET /v1/account/accounts`。现货交易使用 ‘spot’ 账户的 account-id |
| symbol          | string   | true     | NA       | 交易对,即ltcbtc, ethbtc...（取值参考`GET /v1/common/symbols`） |
| type            | string   | true     | NA       | 订单类型，包括buy-market, sell-market, buy-limit, sell-limit（说明见下文） |
| amount          | string   | true     | NA       | 订单交易量（市价买单为订单交易额）                           |
| price           | string   | false    | NA       | 订单价格（对市价单无效）                                     |
| source          | string   | false    | spot-api | 现货交易填写“spot-api”                                       |
| client-order-id | string   | false    | NA       | 用户自编订单号（最大长度64个字符，须在8小时内保持唯一性）    |

**buy-limit-maker**

当“下单价格”>=“市场最低卖出价”，订单提交后，系统将拒绝接受此订单；

当“下单价格”<“市场最低卖出价”，提交成功后，此订单将被系统接受。

**sell-limit-maker**

当“下单价格”<=“市场最高买入价”，订单提交后，系统将拒绝接受此订单；

当“下单价格”>“市场最高买入价”，提交成功后，此订单将被系统接受。

> Response:

```json
{    "status": "ok",    "data": [        {            "order-id": 61713400772,            "client-order-id": "c1"        },        {            "order-id": 61713400940,            "client-order-id": "d2"        }    ]}
```

### 响应数据

| 字段名称        | 数据类型 | 描述                                 |
| --------------- | -------- | ------------------------------------ |
| [{ order-id     | integer  | 订单编号                             |
| client-order-id | string   | 用户自编订单号（如有）               |
| err-code        | string   | 订单被拒错误码（仅对被拒订单有效）   |
| err-msg }]      | string   | 订单被拒错误信息（仅对被拒订单有效） |

如client order ID（在8小时内）被复用，节点返回先前订单的order ID及client order ID。

## 撤销订单

API Key 权限：交易<br>
限频值（NEW）：100次/2s

此接口发送一个撤销订单的请求。

<aside class="warning">此接口只提交取消请求，实际取消结果需要通过订单状态，撮合状态等接口来确认。</aside>

### HTTP 请求

- POST ` /v1/order/orders/{order-id}/submitcancel`


### 请求参数

| 参数名称 | 是否必须 | 类型   | 描述                      | 默认值 | 取值范围 |
| -------- | -------- | ------ | ------------------------- | ------ | -------- |
| order-id | true     | string | 订单ID，填在path中        |        |          |
| symbol   | false    | string | 交易对，填在URL请求参数中 |        |          |

> Success response:

```json
{    "data": "59378"}
```

### 响应数据

返回的主数据对象是一个对应下单单号的字符串。

### 错误码

> Failure response:

```json
{  "status": "error",  "err-code": "order-orderstate-error",  "err-msg": "订单状态错误",  "order-state":-1 // 当前订单状态}
```

返回字段列表中，order-state的可能取值包括 -

| order-state | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| -1          | order was already closed in the long past (order state = canceled, partial-canceled, filled, partial-filled) |
| 1           | created                                                      |
| 3           | submitted                                                    |
| 4           | partial-filled                                               |
| 5           | partial-canceled                                             |
| 6           | filled                                                       |
| 7           | canceled                                                     |
| 10          | cancelling                                                   |

## 撤销订单（基于client order ID）

API Key 权限：交易<br>
限频值（NEW）：100次/2s

此接口基于client-order-id（8小时内有效）发送一个撤销订单的请求。

<aside class="notice">撤单个订单建议通过接口/v1/order/orders/{order-id}/submitcancel，会更快更稳定</aside>
<aside class="warning">此接口只提交取消请求，实际取消结果需要通过订单状态，撮合状态等接口来确认。</aside>



### HTTP 请求

- POST ` /v1/order/orders/submitCancelClientOrder`

> Request:

```json
{  "client-order-id": "a0001"}
```

### 请求参数

| 参数名称        | 是否必须 | 类型   | 描述                                                         | 默认值 | 取值范围 |
| --------------- | -------- | ------ | ------------------------------------------------------------ | ------ | -------- |
| client-order-id | true     | string | 用户自编订单号，必须8小时内已有该订单存在，否则下次下单时不允许用此值 |        |          |


> Response:

```json
{    "data": "10"}
```

### 响应数据

| 字段名称 | 数据类型 | 描述       |
| -------- | -------- | ---------- |
| data     | integer  | 撤单状态码 |

| Status Code | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| -1          | order was already closed in the long past (order state = canceled, partial-canceled, filled, partial-filled) |
| 0           | client-order-id not found                                    |
| 1           | created                                                      |
| 3           | submitted                                                    |
| 4           | partial-filled                                               |
| 5           | partial-canceled                                             |
| 6           | filled                                                       |
| 7           | canceled                                                     |
| 10          | cancelling                                                   |



## 自动撤销订单

API Key 权限：交易<br>

为了防止API用户在发生网络故障或用户端系统故障与火币新加坡系统失去联系时，给用户造成意外损失，火币新加坡新增自动撤单接口，当用户与火币新加坡发生意外断连时，能自动帮用户取消全部委托单，以避免损失，即提供Dead man's switch功能。若开启，在设定的时间数完前，接口没有被再次调用，则用户所有现货委托单将被取消（最大支持撤500单）。

### HTTP 请求

- POST `/v2/algo-orders/cancel-all-after`

> Request:

```json
{  "timeout": "10"}
```

### 请求参数

| 参数名称 | 是否必须 | 类型 | 描述                                 | 默认值 | 取值范围         |
| -------- | -------- | ---- | ------------------------------------ | ------ | ---------------- |
| timeout  | true     | int  | 超时时间（单位：秒），设置建议见附注 | NA     | 0或者大于等于5秒 |


> 响应示例-开启成功 
> Response:

```json
{"code": 200,"data": [    {       "currentTime":"1587971400",       "triggerTime":"1587971460"  }]}
```


> 响应示例-关闭成功 
> Response:

```json
{"code": 200,"data": [    {       "currentTime":"1587971400",       "triggerTime":"0"  }]}
```


> 响应示例-开启/关闭失败
> Response:

```json
{"code": 2003,"message": "missing mandatory field"}
```

### 响应数据

| **参数名称**  | **是否必须** | **数据类型** | **描述**         |
| ------------- | ------------ | ------------ | ---------------- |
| code          | true         | int          | 状态码           |
| message       | false        | string       | 错误描述（如有） |
| data          | true         | object       |                  |
| { currentTime | true         | long         | 当前时间         |
| triggerTime } | true         | long         | 触发时间         |


## 查询当前未成交订单

API Key 权限：读取<br>
限频值（NEW）：50次/2s

查询已提交但是仍未完全成交或未被撤销的订单。

### HTTP 请求

- GET `/v1/order/openOrders`

> Request:

```json
{   "account-id": "100009",   "symbol": "ethbtc",   "side": "buy"}
```

### 请求参数

| 参数名称   | 数据类型 | 是否必需                                         | 默认值 | 描述                                                         |
| ---------- | -------- | ------------------------------------------------ | ------ | ------------------------------------------------------------ |
| account-id | string   | true                                             | NA     | 账户 ID，取值参考 `GET /v1/account/accounts`。               |
| symbol     | string   | ture                                             | NA     | 交易对,即ltcbtc, ethbtc...（取值参考`GET /v1/common/symbols`） |
| side       | string   | false                                            | both   | 指定只返回某一个方向的订单，可能的值有: buy, sell. 默认两个方向都返回。 |
| types      | string   | false                                            |        | 查询的订单类型组合，使用逗号分割                             |
| from       | string   | false                                            |        | 查询起始 ID，如果是向后查询，则赋值为上一次查询结果中得到的最后一条id ；如果是向前查询，则赋值为上一次查询结果中得到的第一条id |
| direct     | string   | false (如字段'from'已设定，此字段'direct'为必填) |        | 查询方向，prev 向前；next 向后                               |
| size       | int      | false                                            | 100    | 返回订单的数量，最大值500。                                  |

> Response:

```json
{    "data": [    {      "id": 5454937,      "symbol": "ethbtc",      "account-id": 30925,      "amount": "1.000000000000000000",      "price": "0.453000000000000000",      "created-at": 1530604762277,      "type": "sell-limit",      "filled-amount": "0.0",      "filled-cash-amount": "0.0",      "filled-fees": "0.0",      "source": "web",      "state": "submitted"    }  ]}
```

### 响应数据

| 字段名称           | 数据类型 | 描述                                                   |
| ------------------ | -------- | ------------------------------------------------------ |
| id                 | integer  | 订单id，无大小顺序，可作为下一次翻页查询请求的from字段 |
| client-order-id    | string   | 用户自编订单号（所有open订单可返回client-order-id）    |
| symbol             | string   | 交易对, 例如ltcbtc, ethbtc                             |
| price              | string   | limit order的交易价格                                  |
| created-at         | int      | 订单创建的调整为新加坡时间的时间戳，单位毫秒           |
| type               | string   | 订单类型                                               |
| filled-amount      | string   | 订单中已成交部分的数量                                 |
| filled-cash-amount | string   | 订单中已成交部分的总价格                               |
| filled-fees        | string   | 已交交易手续费总额（准确数值请参考matchresults接口）   |
| source             | string   | 订单来源                                               |
| state              | string   | 订单状态，包括created, submitted, partial-filled       |

## 批量撤销所有订单

API Key 权限：交易<br>
限频值（NEW）：50次/2s

此接口发送批量撤销所有（单次最大100个）订单的请求。

<aside class="warning">此接口只提交取消请求，实际取消结果需要通过订单状态，撮合状态等接口来确认。</aside>

### HTTP 请求

- POST ` /v1/order/orders/batchCancelOpenOrders`


### 请求参数

| 参数名称   | 是否必须 | 类型   | 描述                                                         | 默认值 | 取值范围                                          |
| ---------- | -------- | ------ | ------------------------------------------------------------ | ------ | ------------------------------------------------- |
| account-id | false    | string | 账户ID，取值参考 `GET /v1/account/accounts`                  |        |                                                   |
| symbol     | false    | string | 交易代码列表（最多10 个symbols，多个交易代码间以逗号分隔），ltcbtc, ethbtc...（取值参考`/v1/common/symbols`） | all    |                                                   |
| types      | false    | string | 订单类型组合，使用逗号分割                                   |        | 所有可能的订单类型（见本章节简介）                |
| side       | false    | string | 主动交易方向                                                 |        | “buy”或“sell”，缺省将返回所有符合条件尚未成交订单 |
| size       | false    | int    | 撤销订单的数量                                               | 100    | [0,100]                                           |


> Response:

```json
{  "status": "ok",  "data": {    "success-count": 2,    "failed-count": 0,    "next-id": 5454600  }}
```


### 响应数据


| 参数名称      | 是否必须 | 数据类型 | 描述                                                 |
| ------------- | -------- | -------- | ---------------------------------------------------- |
| success-count | true     | int      | 成功取消的订单数                                     |
| failed-count  | true     | int      | 取消失败的订单数                                     |
| next-id       | true     | long     | 下一个可以撤销的订单号，返回-1表示没有可以撤销的订单 |

## 批量撤销指定订单

API Key 权限：交易<br>
限频值（NEW）：50次/2s

此接口同时为多个订单（基于id）发送取消请求，建议通过order-ids来撤单，比client-order-ids更快更稳定。

### HTTP 请求

- POST ` /v1/order/orders/batchcancel`

> Request:

```json
{  "client-order-ids": [   "5983466", "5722939", "5721027", "5719487"  ]}
```

### 请求参数

| 参数名称         | 是否必须 | 类型     | 描述                                                         | 默认值 | 取值范围           |
| ---------------- | -------- | -------- | ------------------------------------------------------------ | ------ | ------------------ |
| order-ids        | false    | string[] | 订单编号列表（order-ids和client-order-ids必须且只能选一个填写，不超过50张订单），建议通过order-ids来撤单，比client-order-ids更快更稳定 |        | 单次不超过50个订单 |
| client-order-ids | false    | string[] | 用户自编订单号列表（order-ids和client-order-ids必须且只能选一个填写，不超过50张订单），必须已有该订单存在，否则下次下单时不允许用此值 |        | 单次不超过50个订单 |

> Response:

```json
{    "status": "ok",    "data": {        "success": [            "5983466"                    ],        "failed": [            {              "err-msg": "Incorrect order state",              "order-state": 7,              "order-id": "",              "err-code": "order-orderstate-error",              "client-order-id": "first"            },            {              "err-msg": "Incorrect order state",              "order-state": 7,              "order-id": "",              "err-code": "order-orderstate-error",              "client-order-id": "second"            },            {              "err-msg": "The record is not found.",              "order-id": "",              "err-code": "base-not-found",              "client-order-id": "third"            }          ]    }}
```

### 响应数据

| 字段名称  | 数据类型 | 描述                                                         |
| --------- | -------- | ------------------------------------------------------------ |
| { success | string[] | 撤单成功订单列表（可为order-id列表或client-order-id列表，以用户请求为准） |
| failed }  | string[] | 撤单失败订单列表（可为order-id列表或client-order-id列表，以用户请求为准） |

撤单失败订单列表 -

| 字段名称        | 数据类型 | 描述                                                         |
| --------------- | -------- | ------------------------------------------------------------ |
| [{ order-id     | string   | 订单编号（如用户创建订单时包含order-id，返回中也须包含此字段） |
| client-order-id | string   | 用户自编订单号（如用户创建订单时包含client-order-id，返回中也须包含此字段） |
| err-code        | string   | 订单被拒错误码（仅对被拒订单有效）                           |
| err-msg         | string   | 订单被拒错误信息（仅对被拒订单有效）                         |
| order-state }]  | string   | 当前订单状态（若有）                                         |

返回字段列表中，order-state的可能取值包括 -

| order-state | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| -1          | order was already closed in the long past (order state = canceled, partial-canceled, filled, partial-filled) |
| 1           | created                                                      |
| 3           | submitted                                                    |
| 4           | partial-filled                                               |
| 5           | partial-canceled                                             |
| 6           | filled                                                       |
| 7           | canceled                                                     |
| 10          | cancelling                                                   |

## 查询订单详情

API Key 权限：读取<br>
限频值（NEW）：50次/2s

此接口返回指定订单的最新状态和详情。通过API创建的订单，撤销超过2小时后无法查询。通过API创建的订单返回order-id，按此order-id查询订单还是返回base-record-invalid是因为系统内部处理有延迟，但是不影响成交。建议您后续重试查询或者通过订阅订单推送WebSocket消息查询。

### HTTP 请求

- GET `/v1/order/orders/{order-id}`


### 请求参数

| 参数名称 | 是否必须 | 类型   | 描述               | 默认值 | 取值范围 |
| -------- | -------- | ------ | ------------------ | ------ | -------- |
| order-id | true     | string | 订单ID，填在path中 |        |          |


> Response:

```json
{    "data":   {    "id": 59378,    "symbol": "ethbtc",    "account-id": 100009,    "amount": "10.1000000000",    "price": "100.1000000000",    "created-at": 1494901162595,    "type": "buy-limit",    "field-amount": "10.1000000000",    "field-cash-amount": "1011.0100000000",    "field-fees": "0.0202000000",    "finished-at": 1494901400468,    "user-id": 1000,    "source": "api",    "state": "filled",    "canceled-at": 0  }}
```

### 响应数据

| 字段名称          | 是否必须 | 数据类型 | 描述                                                         | 取值范围                           |
| ----------------- | -------- | -------- | ------------------------------------------------------------ | ---------------------------------- |
| account-id        | true     | long     | 账户 ID                                                      |                                    |
| amount            | true     | string   | 订单数量                                                     |                                    |
| canceled-at       | false    | long     | 订单撤销时间                                                 |                                    |
| created-at        | true     | long     | 订单创建时间                                                 |                                    |
| field-amount      | true     | string   | 已成交数量                                                   |                                    |
| field-cash-amount | true     | string   | 已成交总金额                                                 |                                    |
| field-fees        | true     | string   | 已成交手续费（准确数值请参考matchresults接口）               |                                    |
| finished-at       | false    | long     | 订单变为终结态的时间，不是成交时间，包含“已撤单”状态         |                                    |
| id                | true     | long     | 订单ID                                                       |                                    |
| client-order-id   | false    | string   | 用户自编订单号（所有open订单可返回client-order-id（如有）；仅7天内（基于订单创建时间）的closed订单（state <> canceled）可返回client-order-id（如有）；仅8小时内（基于订单创建时间）的closed订单（state = canceled）可返回client-order-id（如有）） |                                    |
| price             | true     | string   | 订单价格                                                     |                                    |
| source            | true     | string   | 订单来源                                                     | api                                |
| state             | true     | string   | 订单状态                                                     | 所有可能的订单状态（见本章节简介） |
| symbol            | true     | string   | 交易对                                                       | ltcbtc, ethbtc ...                 |
| type              | true     | string   | 订单类型                                                     | 所有可能的订单类型（见本章节简介） |


## 查询订单详情（基于client order ID）

API Key 权限：读取<br>
限频值（NEW）：50次/2s

此接口返回指定用户自编订单号（8小时内）的订单最新状态和详情。通过API创建的订单，撤销超过2小时后无法查询。建议通过GET `/v1/order/orders/{order-id}`来撤单，比使用clientOrderId更快更稳定

### HTTP 请求

- GET `/v1/order/orders/getClientOrder`

### 请求参数

| 参数名称      | 是否必须 | 类型   | 描述           | 默认值 | 取值范围 |
| ------------- | -------- | ------ | -------------- | ------ | -------- |
| clientOrderId | true     | string | 用户自编订单号 |        |          |

> Response:

```json
{    "data":   {    "id": 59378,    "symbol": "ethbtc",    "account-id": 100009,    "amount": "10.1000000000",    "price": "100.1000000000",    "created-at": 1494901162595,    "type": "buy-limit",    "field-amount": "10.1000000000",    "field-cash-amount": "1011.0100000000",    "field-fees": "0.0202000000",    "finished-at": 1494901400468,    "user-id": 1000,    "source": "api",    "state": "filled",    "canceled-at": 0  }}
```

### 响应数据

| 字段名称          | 是否必须 | 数据类型 | 描述                                                         | 取值范围                           |
| ----------------- | -------- | -------- | ------------------------------------------------------------ | ---------------------------------- |
| account-id        | true     | long     | 账户 ID                                                      |                                    |
| amount            | true     | string   | 订单数量                                                     |                                    |
| canceled-at       | false    | long     | 订单撤销时间                                                 |                                    |
| created-at        | true     | long     | 订单创建时间                                                 |                                    |
| field-amount      | true     | string   | 已成交数量                                                   |                                    |
| field-cash-amount | true     | string   | 已成交总金额                                                 |                                    |
| field-fees        | true     | string   | 已成交手续费（准确数值请参考matchresults接口）               |                                    |
| finished-at       | false    | long     | 订单变为终结态的时间，不是成交时间，包含“已撤单”状态         |                                    |
| id                | true     | long     | 订单ID                                                       |                                    |
| client-order-id   | false    | string   | 用户自编订单号（仅8小时内（基于订单创建时间）的订单可被查询，订单状态是终态的2小时内可查询） |                                    |
| price             | true     | string   | 订单价格                                                     |                                    |
| source            | true     | string   | 订单来源                                                     | api                                |
| state             | true     | string   | 订单状态                                                     | 所有可能的订单状态（见本章节简介） |
| symbol            | true     | string   | 交易对                                                       | ltcbtc, ethbtc...                  |
| type              | true     | string   | 订单类型                                                     | 所有可能的订单类型（见本章节简介） |

如client order ID不存在，返回如下错误信息 
{
    "status": "error",
    "err-code": "base-record-invalid",
    "err-msg": "record invalid",
    "data": null
}

## 成交明细

API Key 权限：读取<br>
限频值（NEW）：50次/2s

此接口返回指定订单的成交明细。

### HTTP 请求

- GET `/v1/order/orders/{order-id}/matchresults`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 描述               | 默认值 | 取值范围 |
| -------- | -------- | ------ | ------------------ | ------ | -------- |
| order-id | true     | string | 订单ID，填在path中 |        |          |


> Response:

```json
{    "status": "ok",    "data": [        {            "symbol": "polyusdt",            "fee-currency": "poly",            "source": "spot-web",            "order-id": 345487249132375,            "price": "0.338",            "created-at": 1629443051839,            "role": "taker",            "match-id": 5014,            "filled-amount": "147.928994082840236",            "filled-fees": "0",            "filled-points": "0.1",            "fee-deduct-currency": "hbpoint",            "fee-deduct-state": "done",            "trade-id": 1085,            "id": 313288753120940,            "type": "buy-market"        }    ]}
```

### 响应数据

<aside class="notice">返回的主数据对象为一个对象数组，其中每一个元件代表一个交易结果。</aside>

|               |          |          |                                                              |                                    |
| :------------ | :------- | :------- | :----------------------------------------------------------- | :--------------------------------- |
| 字段名称      | 是否必须 | 数据类型 | 描述                                                         | 取值范围                           |
| status        | true     | string   | 状态                                                         |                                    |
| <data>        | true     | object   |                                                              |                                    |
| created-at    | true     | long     | 该成交记录创建的时间戳（略晚于成交时间）                     |                                    |
| filled-amount | true     | string   | 成交数量                                                     |                                    |
| filled-fees   | true     | string   | 交易手续费（正值）或交易返佣金（负值）                       |                                    |
| fee-currency  | true     | string   | 交易手续费或交易返佣币种（买单的交易手续费币种为基础币种，卖单的交易手续费币种为计价币种；买单的交易返佣币种为计价币种，卖单的交易返佣币种为基础币种） |                                    |
| id            | true     | long     | 订单成交记录ID                                               |                                    |
| match-id      | true     | long     | 撮合ID，订单在撮合中执行的顺序ID                             |                                    |
| order-id      | true     | long     | 订单ID，成交所属订单的ID                                     |                                    |
| trade-id      | false    | integer  | Unique trade ID (NEW)唯一成交编号，成交时产生的唯一编号ID    |                                    |
| price         | true     | string   | 成交价格                                                     |                                    |
| source        | true     | string   | 订单来源                                                     | api                                |
| symbol        | true     | string   | 交易对                                                       | btcusdt, ethbtc, rcneth ...        |
| type          | true     | string   | 订单类型                                                     | 所有可能的订单类型（见本章节简介） |
| role          | true     | string   | 成交角色                                                     | maker,taker                        |
| </data>       |          |          |                                                              |                                    |

注：<br>

- filled-fees中的交易返佣金额可能不会实时到账。<br>

## 搜索历史订单

API Key 权限：读取<br>
限频值（NEW）：50次/2s

此接口基于搜索条件查询历史订单。通过API创建的订单，撤销超过2小时后无法查询。

用户可选择以“时间范围”查询历史订单，以替代原先的以“日期范围“查询方式。

-	如用户填写start-time AND/OR end-time查询历史订单，服务器将按照用户指定的“时间范围“查询并返回，并忽略start-date/end-date参数。此方式的查询窗口大小限定为最大48小时，窗口平移范围为最近180天。

-	如用户不填写start-time/end-time参数，而填写start-date AND/OR end-date查询历史订单，服务器将按照用户指定的“日期范围“查询并返回。此方式的查询窗口大小限定为最大2天，窗口平移范围为最近180天。

-	如用户既不填写start-time/end-time参数，也不填写start-date/end-date参数，服务器将缺省以当前时间为end-time，返回最近48小时内的历史订单。

火币新加坡建议用户以“时间范围“查询历史订单。未来，火币新加坡将下线以”日期范围“查询历史订单的方式，并另行通知。


### HTTP 请求

- GET `/v1/order/orders`

> Request:

```json
{   "account-id": "100009",   "amount": "10.1",   "price": "100.1",   "source": "api",   "symbol": "ethbtc",   "type": "buy-limit"}
```


### 请求参数

| 参数名称   | 是否必须 | 类型   | 描述                                                         | 默认值                      | 取值范围                                                     |
| ---------- | -------- | ------ | ------------------------------------------------------------ | --------------------------- | ------------------------------------------------------------ |
| symbol     | true     | string | 交易对                                                       |                             | ltcbtc, ethbtc...（取值参考`GET /v1/common/symbols`）        |
| types      | false    | string | 查询的订单类型组合，使用逗号分割                             |                             | 所有可能的订单类型（见本章节简介）                           |
| start-time | false    | long   | 查询开始时间, 时间格式UTC time in millisecond。 以订单生成时间进行查询 | -48h 查询结束时间的前48小时 | 取值范围 [((end-time) – 48h), (end-time)] ，查询窗口最大为48小时，窗口平移范围为最近180天，已完全撤销的历史订单的查询窗口平移范围只有最近2小时(state="canceled") |
| end-time   | false    | long   | 查询结束时间, 时间格式UTC time in millisecond。 以订单生成时间进行查询 | present                     | 取值范围 [(present-179d), present] ，查询窗口最大为48小时，窗口平移范围为最近180天，已完全撤销的历史订单的查询窗口平移范围只有最近2小时(state="canceled") |
| states     | true     | string | 查询的订单状态组合，使用','分割                              |                             | 所有可能的订单状态（见本章节简介）                           |
| from       | false    | string | 查询起始 ID                                                  |                             | 如果是向后查询，则赋值为上一次查询结果中得到的最后一条id ；如果是向前查询，则赋值为上一次查询结果中得到的第一条id |
| direct     | false    | string | 查询方向                                                     |                             | prev 向前；next 向后                                         |
| size       | false    | string | 查询记录大小                                                 | 100                         | [1, 100]                                                     |


> Response:

```json
  "data": [    {      "id": 59378,      "symbol": "ethbtc",      "account-id": 100009,      "amount": "10.1000000000",      "price": "100.1000000000",      "created-at": 1494901162595,      "type": "buy-limit",      "field-amount": "10.1000000000",      "field-cash-amount": "1011.0100000000",      "field-fees": "0.0202000000",      "finished-at": 1494901400468,      "user-id": 1000,      "source": "api",      "state": "filled",      "canceled-at": 0    }  ]
```

### 响应数据

| 参数名称          | 是否必须 | 数据类型 | 描述                                                         | 取值范围                           |
| ----------------- | -------- | -------- | ------------------------------------------------------------ | ---------------------------------- |
| account-id        | true     | long     | 账户 ID                                                      |                                    |
| amount            | true     | string   | 订单数量                                                     |                                    |
| canceled-at       | false    | long     | 接到撤单申请的时间                                           |                                    |
| created-at        | true     | long     | 订单创建时间                                                 |                                    |
| field-amount      | true     | string   | 已成交数量                                                   |                                    |
| field-cash-amount | true     | string   | 已成交总金额                                                 |                                    |
| field-fees        | true     | string   | 已成交手续费（准确数值请参考matchresults接口）               |                                    |
| finished-at       | false    | long     | 最后成交时间                                                 |                                    |
| id                | true     | long     | 订单ID，无大小顺序，可作为下一次翻页查询请求的from字段       |                                    |
| client-order-id   | false    | string   | 用户自编订单号（所有open订单可返回client-order-id（如有）；仅7天内（基于订单创建时间）的closed订单（state <> canceled）可返回client-order-id（如有）；仅8小时内（基于订单创建时间）的closed订单（state = canceled）可被查询） |                                    |
| price             | true     | string   | 订单价格                                                     |                                    |
| source            | true     | string   | 订单来源                                                     | 所有可能的订单来源（见本章节简介） |
| state             | true     | string   | 订单状态                                                     | 所有可能的订单状态（见本章节简介） |
| symbol            | true     | string   | 交易对                                                       | ltcbtc, ethbtc ...                 |
| type              | true     | string   | 订单类型                                                     | 所有可能的订单类型（见本章节简介） |

### start-date, end-date相关错误码

| 错误码             | 对应错误场景                                                 |
| ------------------ | ------------------------------------------------------------ |
| invalid_interval   | start date小于end date; 或者 start date 与end date之间的时间间隔大于2天 |
| invalid_start_date | start date是一个180天之前的日期；或者start date是一个未来的日期 |
| invalid_end_date   | end date 是一个180天之前的日期；或者end date是一个未来的日期 |

## 搜索最近48小时内历史订单

API Key 权限：读取<br>
限频值（NEW）：20次/2s

此接口基于搜索条件查询最近48小时内历史订单。通过API创建的订单，撤销超过2小时后无法查询。

### HTTP 请求

- GET `/v1/order/history`

> Request:

```json
{   "symbol": "ethbtc",   "start-time": "1556417645419",   "end-time": "1556533539282",   "direct": "prev",   "size": "10"}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 描述                                                         | 默认值         | 取值范围                                              |
| ---------- | -------- | ------ | ------------------------------------------------------------ | -------------- | ----------------------------------------------------- |
| symbol     | false    | string | 交易对                                                       | all            | ltcbtc, ethbtc...（取值参考`GET /v1/common/symbols`） |
| start-time | false    | long   | 查询起始时间（含）                                           | 48小时前的时刻 | UTC time in millisecond                               |
| end-time   | false    | long   | 查询结束时间（含）                                           | 查询时刻       | UTC time in millisecond                               |
| direct     | false    | string | 订单查询方向（注：仅在检索出的总条目数量超出size字段限定时起作用；如果检索出的总条目数量在size 字段限定内，direct 字段不起作用。） | next           | prev 向前, next 向后                                  |
| size       | false    | int    | 每次返回条目数量                                             | 100            | [10,1000]                                             |

> Response:

```json
{    "status": "ok",    "data": [        {            "id": 31215214553,            "symbol": "ethbtc",            "account-id": 4717043,            "amount": "1.000000000000000000",            "price": "1.000000000000000000",            "created-at": 1556533539282,            "type": "buy-limit",            "field-amount": "0.0",            "field-cash-amount": "0.0",            "field-fees": "0.0",            "finished-at": 1556533568953,            "source": "web",            "state": "canceled",            "canceled-at": 1556533568911        }    ]}
```

### 响应数据

| 参数名称          | 是否必须 | 数据类型 | 描述                                                         | 取值范围                                                     |
| ----------------- | -------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| {account-id       | true     | long     | 账户 ID                                                      |                                                              |
| amount            | true     | string   | 订单数量                                                     |                                                              |
| canceled-at       | false    | long     | 接到撤单申请的时间                                           |                                                              |
| created-at        | true     | long     | 订单创建时间                                                 |                                                              |
| field-amount      | true     | string   | 已成交数量                                                   |                                                              |
| field-cash-amount | true     | string   | 已成交总金额                                                 |                                                              |
| field-fees        | true     | string   | 已成交手续费（准确数值请参考matchresults接口）               |                                                              |
| finished-at       | false    | long     | 最后成交时间                                                 |                                                              |
| id                | true     | long     | 订单ID，无大小顺序                                           |                                                              |
| client-order-id   | false    | string   | 用户自编订单号（仅48小时内（基于订单创建时间）的closed订单（state <> canceled）可返回client-order-id（如有）；仅8小时内（基于订单创建时间）的closed订单（state = canceled）可被查询） |                                                              |
| price             | true     | string   | 订单价格                                                     |                                                              |
| source            | true     | string   | 订单来源                                                     | 所有可能的订单来源（见本章节简介）                           |
| state             | true     | string   | 订单状态                                                     | partial-canceled 部分成交撤销, filled 完全成交, canceled 已撤销 |
| symbol            | true     | string   | 交易对                                                       | ltcbtc, ethbtc ...                                           |
| type}             | true     | string   | 订单类型                                                     | 所有可能的订单类型（见本章节简介）                           |
| next-time         | false    | long     | 下一查询起始时间（当请求字段”direct”为”prev”时有效）, 下一查询结束时间（当请求字段”direct”为”next”时有效）。注：仅在检索出的总条目数量超出size字段限定时，此返回字段存在。 | UTC time in millisecond                                      |


## 当前和历史成交

API Key 权限：读取<br>
限频值（NEW）：20次/2s

此接口基于搜索条件查询当前和历史成交记录。

### HTTP 请求

- GET `/v1/order/matchresults`


### 请求参数

| 参数名称   | 是否必须 | 类型   | 描述                                                         | 默认值                      | 取值范围                                                     |
| ---------- | -------- | ------ | ------------------------------------------------------------ | --------------------------- | ------------------------------------------------------------ |
| symbol     | true     | string | 交易对                                                       | N/A                         | ltcbtc, ethbtc...（取值参考`GET /v1/common/symbols`）        |
| types      | false    | string | 查询的订单类型组合，使用','分割                              | all                         | 所有可能的订单类型（见本章节简介）                           |
| start-time | false    | long   | 查询开始时间, 时间格式UTC time in millisecond。 以订单生成时间进行查询 | -48h 查询结束时间的前48小时 | 取值范围 [((end-time) – 48h), (end-time)] ，查询窗口最大为48小时，窗口平移范围为最近120天。 |
| end-time   | false    | long   | 查询结束时间, 时间格式UTC time in millisecond。 以订单生成时间进行查询 | present                     | 取值范围 [(present-120d), present] ，查询窗口最大为48小时，窗口平移范围为最近120天。 |
| from       | false    | string | 查询起始 ID                                                  | N/A                         | 如果是向后查询，则赋值为上一次查询结果中得到的最后一条id（不是trade-id） ；如果是向前查询，则赋值为上一次查询结果中得到的第一条id（不是trade-id） |
| direct     | false    | string | 查询方向                                                     | next                        | prev 向前；next 向后                                         |
| size       | false    | string | 查询记录大小                                                 | 100                         | [1，500]                                                     |

> Response:

```json
{    "status": "ok",    "data": [        {            "symbol": "polyusdt",            "fee-currency": "poly",            "source": "spot-web",            "price": "0.338",            "created-at": 1629443051839,            "role": "taker",            "order-id": 345487249132375,            "match-id": 5014,            "trade-id": 1085,            "filled-amount": "147.928994082840236",            "filled-fees": "0",            "filled-points": "0.1",            "fee-deduct-currency": "hbpoint",            "fee-deduct-state": "done",            "id": 313288753120940,            "type": "buy-market"        }    ]}
```

### 响应数据

<aside class="notice">返回的主数据对象为一个对象数组，其中每一个元件代表一个交易结果。</aside>

|               |          |          |                                                              |                                    |
| :------------ | :------- | :------- | :----------------------------------------------------------- | :--------------------------------: |
| 参数名称      | 是否必须 | 数据类型 | 描述                                                         |              取值范围              |
| status        | true     | string   | 状态                                                         |                                    |
| <data>        | true     | object   |                                                              |                                    |
| created-at    | true     | long     | 该成交记录创建的时间戳（略晚于成交时间）                     |                                    |
| filled-amount | true     | string   | 成交数量                                                     |                                    |
| filled-fees   | true     | string   | 交易手续费（正值）或交易返佣（负值）                         |                                    |
| fee-currency  | true     | string   | 交易手续费或交易返佣币种（买单的交易手续费币种为基础币种，卖单的交易手续费币种为计价币种；买单的交易返佣币种为计价币种，卖单的交易返佣币种为基础币种） |                                    |
| id            | true     | long     | 订单成交记录 ID，无大小顺序，可作为下一次翻页查询请求的from字段 |                                    |
| match-id      | true     | long     | 撮合 ID                                                      |                                    |
| order-id      | true     | long     | 订单 ID                                                      |                                    |
| trade-id      | false    | integer  | 唯一成交编号                                                 |                                    |
| price         | true     | string   | 成交价格                                                     |                                    |
| source        | true     | string   | 订单来源                                                     |                api                 |
| symbol        | true     | string   | 交易对                                                       |    btcusdt, ethbtc, rcneth ...     |
| type          | true     | string   | 订单类型                                                     | 所有可能的订单类型（见本章节简介） |
| role          | true     | string   | 成交角色                                                     |            maker,taker             |
| </data>       |          |          |                                                              |                                    |

注：<br>

- filled-fees中的交易返佣金额可能不会实时到账；<br>

### start-date, end-date相关错误码 

| 错误码             | 对应错误场景                                                 |
| ------------------ | ------------------------------------------------------------ |
| invalid_interval   | start date小于end date; 或者 start date 与end date之间的时间间隔大于2天 |
| invalid_start_date | start date是一个61天之前的日期；或者start date是一个未来的日期 |
| invalid_end_date   | end date 是一个61天之前的日期；或者end date是一个未来的日期  |


## 获取用户当前手续费率

Api用户查询交易对费率，一次限制最多查10个交易对，子用户的费率和母用户保持一致

API Key 权限：读取

```shell
curl "https://api.huobi.sg/v2/reference/transact-fee-rate?symbols=,ethbtc,ltcbtc"
```

### HTTP 请求

- GET `/v2/reference/transact-fee-rate`

### 请求参数

| 参数    | 数据类型 | 是否必须 | 默认值 | 描述                     | 取值范围                                               |
| ------- | -------- | -------- | ------ | ------------------------ | ------------------------------------------------------ |
| symbols | string   | true     | NA     | 交易对，可多填，逗号分隔 | ltcbtc, ethbtc...（取值参考`GET /v1/common/symbols`）> |

> Response:

```json
{  "code": "200",  "data": [     {        "symbol": "ethbtc",        "makerFeeRate":"0.002",        "takerFeeRate":"0.002",        "actualMakerRate": "0.002",        "actualTakerRate":"0.002     },     {        "symbol": "ethbtc",        "makerFeeRate":"0.002",        "takerFeeRate":"0.002",        "actualMakerRate": "0.002",        "actualTakerRate":"0.002    },     {        "symbol": "ltcbtc",        "makerFeeRate":"0.002",        "takerFeeRate":"0.002",        "actualMakerRate": "0.002",        "actualTakerRate":"0.002    }  ]}
```

### 响应数据

|      | 字段名称          | 数据类型 | 描述                                                         |      |
| ---- | ----------------- | -------- | ------------------------------------------------------------ | ---- |
|      | code              | integer  | 状态码                                                       |      |
|      | message           | string   | 错误描述（如有）                                             |      |
|      | data              | object   |                                                              |      |
|      | { symbol          | string   | 交易代码                                                     |      |
|      | makerFeeRate      | string   | 基础费率 - 被动方，如适用交易手续费返佣，返回返佣费率（负值） |      |
|      | takerFeeRate      | string   | 基础费率 - 主动方                                            |      |
|      | actualMakerRate   | string   | 抵扣后费率 - 被动方，如不适用抵扣或未启用抵扣，返回基础费率；如适用交易手续费返佣，返回返佣费率（负值） |      |
|      | actualTakerRate } | string   | 抵扣后费率 – 主动方，如不适用抵扣或未启用抵扣，返回基础费率  |      |

注：<br>

- 如makerFeeRate/actualMakerRate为正值，该字段意为交易手续费率；<br>
- 如makerFeeRate/actualMakerRate为负值，该字段意为交易返佣费率。<br>

## 常见错误码

以下是交易相关接口返回的返回码以及说明。

| 返回码                                                       | 说明                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| base-argument-unsupported                                    | 某参数不支持，请检查参数                                     |
| base-system-error                                            | 系统错误，如果是撤单：缓存中查不到订单状态，该订单无法撤单；如果是下单：订单入缓存失败，请再次尝试 |
| login-required                                               | url中没有Signature参数或找不到此用户（key与账户id不对应等情况） |
| base-record-invalid                                          | 暂时未找到数据，请稍后重试                                   |
| order-amount-over-limit                                      | 订单数量超出限额                                             |
| base-symbol-trade-disabled                                   | 该交易对被禁止交易                                           |
| base-operation-forbidden                                     | 用户不在白名单内或该币种不允许OTC交易等禁止行为              |
| account-get-accounts-inexistent-error                        | 该账户在该用户下不存在                                       |
| account-account-id-inexistent                                | 该账户不存在                                                 |
| order-disabled                                               | 交易对暂停，无法下单                                         |
| cancel-disabled                                              | 交易对暂停，无法撤单                                         |
| order-invalid-price                                          | 下单价格非法（如市价单不能有价格，或限价单价格超过市场价10%） |
| order-accountbalance-error                                   | 账户余额不足                                                 |
| order-limitorder-price-min-error                             | 卖出价格不能低于指定价格                                     |
| order-limitorder-price-max-error                             | 买入价格不能高于指定价格                                     |
| order-limitorder-amount-min-error                            | 下单数量不能低于指定数量                                     |
| order-limitorder-amount-max-error                            | 下单数量不能高于指定数量                                     |
| order-etp-nav-price-min-error                                | 下单价格不能低于净值的指定比率                               |
| order-etp-nav-price-max-error                                | 下单价格不能高于净值等指定比率                               |
| order-orderprice-precision-error                             | 交易价格精度错误                                             |
| order-orderamount-precision-error                            | 交易数额精度错误                                             |
| order-value-min-error                                        | 订单交易额不能低于指定额度                                   |
| order-marketorder-amount-min-error                           | 卖出数量不能低于指定数量                                     |
| order-marketorder-amount-buy-max-error                       | 市价单买入额度不能高于指定额度                               |
| order-marketorder-amount-sell-max-error                      | 市价单卖出数量不能高于指定数量                               |
| order-holding-limit-failed                                   | 下单超出该币种的持仓限额                                     |
| order-type-invalid                                           | 订单类型非法                                                 |
| order-orderstate-error                                       | 订单状态错误                                                 |
| order-date-limit-error                                       | 查询时间不能超过系统限制                                     |
| order-source-invalid                                         | 订单来源非法                                                 |
| order-update-error                                           | 更新数据错误                                                 |
| order-user-cancel-forbidden                                  | 订单类型为IOC或FOK 不允许撤单                                |
| order-price-greater-than-limit                               | 下单价格高于开盘前下单限制价格，请重新下单                   |
| order-price-less-than-limit                                  | 下单价格低于开盘前下单限制价格，请重新下单                   |
| market-orders-not-support-during-limit-price-trading         | 限时下单不支持市价单                                         |
| price-exceeds-the-protective-price-during-limit-price-trading | 限价时间内价格超出保护价                                     |
| invalid-client-order-id                                      | client order id 在最近的下单或撤单参数中已被使用             |
| invalid-interval                                             | 查询起止窗口设置错误                                         |
| invalid-start-date                                           | 查询起始日期含非法取值                                       |
| invalid-end-date                                             | 查询起始日期含非法取值                                       |
| invalid-start-time                                           | 查询起始时间含非法取值                                       |
| invalid-end-time                                             | 查询起始时间含非法取值                                       |
| validation-constraints-required                              | 指定的必填参数缺失                                           |
| symbol-not-support                                           | 交易对不支持，全仓杠杆或c2c                                  |
| not-found                                                    | 撤单时订单不存在                                             |
| base-not-found                                               | 未找到记录                                                   |
| base_record_invalid                                          | 订单不存在 （传错订单ID）                                    |
| dw_cancel_withdraw_failed                                    | 取消失败，订单状态错误                                       |
| base_update_error                                            | 内部系统错误                                                 |

## 常见问题

### Q1：client-order-id是什么？

A： client-order-id作为下单请求标识的一个参数，类型为字符串，长度为64。 此id为用户自己生成，8小时内有效。如果是终态订单仅2小时有效。

### Q2：如何获取下单数量、金额、小数限制、精度的信息？

A： 可使用 Rest API `GET /v1/common/symbols` 获取相关币对信息， 下单时注意最小下单数量和最小下单金额的区别。 

常见返回错误如下：  

- order-value-min-error: 下单金额小于最小交易额  
- order-orderprice-precision-error : 限价单价格精度错误  
- order-orderamount-precision-error : 下单数量精度错误  
- order-limitorder-price-max-error : 限价单价格高于限价阈值  
- order-limitorder-price-min-error : 限价单价格低于限价阈值  
- order-limitorder-amount-max-error : 限价单数量高于限价阈值  
- order-limitorder-amount-min-error : 限价单数量低于限价阈值  

### Q3： 为什么收到订单成功成交的消息后再次进行下单，返回余额不足？

A：为保证订单的及时送达以及低延时， 订单推送的结果是在撮合后直接推送，此时订单可能并未完成资产的清算。  

建议使用以下方式保证资金可以正确下单：

1. 结合资产推送主题`accounts`同步接收资产变更的消息，确保资金已经完成清算。

2. 收到订单推送消息时，使用Rest接口调用账户余额，验证账户资金是否足够。

3. 账户中保留相对充足的资金余额。

### Q4: 成交明细里的filled-fees和filled-points有什么区别？

A: 成交中的成交手续费分为普通手续费以及抵扣手续费两种类型，两种类型不会同时存在。

1. 普通手续费表示，在成交时，使用原币进行手续费扣除。例如：在ETHBTC币种对下购买ETH，filled-fees字段不为空，表示扣除了普通手续费，单位是ETH。


### Q5: 成交明细中match-id和trade-id有什么区别？

A: match-id表示订单在撮合中的顺序号，trade-id表示成交时的序号， 一个match-id可能有多个trade-id（成交时），也可能没有trade-id(创建订单、撤销订单)

### Q6: 为什么基于当前盘口买一或者卖一价格进行下单触发了下单限价错误？

A: 当前火币新加坡有基于最新成交价上下一定幅度的限价保护，对流动性不好的币，基于盘口数据下单可能会触发限价保护。建议基于ws推送的成交价+盘口数据信息进行下单



# Websocket行情数据

## 简介

### 接入URL

**Global站行情请求地址（除MBP增量推送及MBP全量REQ以外Websocket行情频道）**

**`wss://api.huobi.sg/ws`**  

**`wss://api-aws.huobi.sg/ws`**  

**MBP增量推送及MBP全量REQ请求地址**

**`wss://api.huobi.sg/feed`**  

**`wss://api-aws.huobi.sg/feed`** 

### 数据压缩

WebSocket 行情接口返回的所有数据都进行了 GZIP 压缩，需要 client 在收到数据之后解压。

### 心跳消息

```json
{"ping": 1492420473027} 
```

当用户的Websocket客户端连接到火币新加坡Websocket服务器后，服务器会定期（当前设为5秒）向其发送`ping`消息并包含一整数值。

```json
{"pong": 1492420473027} 
```

当用户的Websocket客户端接收到此心跳消息后，应返回`pong`消息并包含同一整数值。

<aside class="warning">当Websocket服务器连续两次发送了`ping`消息却没有收到任何一次`pong`消息返回后，服务器将主动断开与此客户端的连接。</aside>

### 订阅主题

> Sub request:

```json
{  "sub": "market.ethbtc.kline.1min",  "id": "id1"}
```

成功建立与Websocket服务器的连接后，Websocket客户端发送请求以订阅特定主题：

{
  "sub": "topic to sub",
  "id": "id generate by client"
}

> Sub response:

```json
{  "id": "id1",  "status": "ok",  "subbed": "market.ethbtc.kline.1min",  "ts": 1489474081631}
```

成功订阅后，Websocket客户端将收到确认。

之后, 一旦所订阅的主题有更新，Websocket客户端将收到服务器推送的更新消息（push）。

### 取消订阅

> UnSub request:

```json
{  "unsub": "market.ethbtc.trade.detail",  "id": "id4"}
```

取消订阅的格式如下：

{
  "unsub": "topic to unsub",
  "id": "id generate by client"
}

> UnSub response:

```json
{  "id": "id4",  "status": "ok",  "unsubbed": "market.ethbtc.trade.detail",  "ts": 1494326028889}
```

取消订阅成功确认。

### 请求数据

Websocket服务器同时支持一次性请求数据（pull）。

一次性请求的格式如下：

{
  "req": "topic to req",
  "id": "id generate by client"
}

一次性返回数据的具体格式参见各个主题。

### 限频

数据请求（req）限频规则

单个连接每两次请求不能小于100ms。

## K线数据

### 主题订阅

一旦K线数据产生，Websocket服务器将通过此订阅主题接口推送至客户端：

`market.$symbol$.kline.$period$`

> 订阅请求

```json
{  "sub": "market.ethbtc.kline.1min",  "id": "id1"}
```

### 参数

| 参数   | 数据类型 | 是否必需 | 描述     | 取值范围                                                     |
| ------ | -------- | -------- | -------- | ------------------------------------------------------------ |
| symbol | string   | true     | 交易代码 | ltcbtc, ethbtc...                                            |
| period | string   | true     | K线周期  | 1min, 5min, 15min, 30min, 60min, 4hour, 1day, 1mon, 1week, 1year |

> Response

```json
{  "id": "id1",  "status": "ok",  "subbed": "market.ethbtc.kline.1min",  "ts": 1489474081631 //system response time}
```

> Update example

```json
{  "ch": "market.ethbtc.kline.1min",  "ts": 1489474082831, //system update time  "tick": {    "id": 1489464480,    "amount": 0.0,    "count": 0,    "open": 7962.62,    "close": 7962.62,    "low": 7962.62,    "high": 7962.62,    "vol": 0.0  }}
```

### 数据更新字段列表

| 字段   | 数据类型 | 描述                                        |
| ------ | -------- | ------------------------------------------- |
| id     | integer  | unix时间，同时作为K线ID                     |
| amount | float    | 成交量                                      |
| count  | integer  | 成交笔数                                    |
| open   | float    | 开盘价                                      |
| close  | float    | 收盘价（当K线为最晚的一根时，是最新成交价） |
| low    | float    | 最低价                                      |
| high   | float    | 最高价                                      |
| vol    | float    | 成交额, 即 sum(每一笔成交价 * 该笔的成交量) |

### 数据请求

用请求方式一次性获取K线数据需要额外提供以下参数：
（每次最多返回300条）

```json
{  "req": "market.$symbol.kline.$period",  "id": "id generated by client",  "from": "from time in epoch seconds",  "to": "to time in epoch seconds"}
```

| 参数 | 数据类型 | 是否必需 | 缺省值                                | 描述                            | 取值范围                                                     |
| ---- | -------- | -------- | ------------------------------------- | ------------------------------- | ------------------------------------------------------------ |
| from | integer  | false    | 1501174800(2017-07-28T00:00:00+08:00) | 起始时间 (epoch time in second) | [1501174800, 2556115200]                                     |
| to   | integer  | false    | 2556115200(2050-01-01T00:00:00+08:00) | 结束时间 (epoch time in second) | [1501174800, 2556115200] or ($from, 2556115200] if "from" is set |



## 聚合行情(Ticker)数据

### 主题订阅

获取市场聚合行情数据，每100ms推送一次。

`market.$symbol.ticker`

> 订阅请求

```json
{  "sub": "market.ethbtc.ticker"}
```

### 请求参数

| 参数   | 数据类型 | 是否必须 | 默认值 | 描述   | 取值范围                                              |
| ------ | -------- | -------- | ------ | ------ | ----------------------------------------------------- |
| symbol | string   | true     | NA     | 交易对 | ltcbtc, ethbtc...（取值参考`GET /v1/common/symbols`） |

> Response:

```json
{"ch": "market.ethbtc.ticker", "ts": 1628587397308, "tick": {"open": 44718.5, "high": 46711, "low": 44480.81, "close": 45868.99, "amount": 22527.427922989766, "vol": 1030630905.0136755, "count": 676424, "bid": 45868.98, "bidSize": 0.016782, "ask": 45868.99, "askSize": 3.1279664455029423, "lastPrice": 45868.99, "lastSize": 0.007444}}
```

### 响应数据

| 字段名称  | 数据类型 | 描述                                     |
| --------- | -------- | ---------------------------------------- |
| id        | long     | NA                                       |
| amount    | float    | 以基础币种计量的交易量（以滚动24小时计） |
| count     | integer  | 交易次数（以滚动24小时计）               |
| open      | float    | 本阶段开盘价（以滚动24小时计）           |
| close     | float    | 本阶段最新价（以滚动24小时计）           |
| low       | float    | 本阶段最低价（以滚动24小时计）           |
| high      | float    | 本阶段最高价（以滚动24小时计）           |
| vol       | float    | 以报价币种计量的交易量（以滚动24小时计） |
| bid       | float    | 当前的最高买价                           |
| bidSize   | float    | 最高买价对应的量                         |
| ask       | float    | 当前的最低卖价                           |
| askSize   | float    | 最低卖价对应的量                         |
| lastPrice | float    | 最新成交价                               |
| lastSize  | float    | 最新成交价对应的量                       |

## 

## 市场深度行情数据

此主题发送最新市场深度快照。快照频率为每秒1次。

### 主题订阅

`market.$symbol.depth.$type`

> Subscribe request

```json
{  "sub": "market.ethbtc.depth.step0",  "id": "id1"}
```

### 参数

| 参数   | 数据类型 | 是否必需 | 缺省值 | 描述         | 取值范围                                              |
| ------ | -------- | -------- | ------ | ------------ | ----------------------------------------------------- |
| symbol | string   | true     | NA     | 交易代码     | ltcbtc, ethbtc...（取值参考`GET /v1/common/symbols`） |
| type   | string   | true     | step0  | 合并深度类型 | step0, step1, step2, step3, step4, step5              |

**"type" 合并深度类型**

| Value | Description                          |
| ----- | ------------------------------------ |
| step0 | 不合并深度                           |
| step1 | Aggregation level = precision*10     |
| step2 | Aggregation level = precision*100    |
| step3 | Aggregation level = precision*1000   |
| step4 | Aggregation level = precision*10000  |
| step5 | Aggregation level = precision*100000 |

当type值为‘step0’时，默认深度为150档;
当type值为‘step1’,‘step2’,‘step3’,‘step4’,‘step5’时，默认深度为20档。

> Response

```json
{  "id": "id1",  "status": "ok",  "subbed": "market.ethbtc.depth.step0",  "ts": 1489474081631 //system response time}
```

> Update example

```json
{  "ch": "market.htbtc.depth.step0",  "ts": 1572362902027, //system update time  "tick": {    "bids": [      [3.7721, 344.86],// [price, size]      [3.7709, 46.66]     ],    "asks": [      [3.7745, 15.44],      [3.7746, 70.52]    ],    "version": 100434317651,    "ts": 1572362902012 //quote time  }}
```

### 数据更新字段列表

<aside class="notice">在'tick'object下方呈现买盘卖盘深度列表</aside>

| 字段    | 数据类型 | 描述                         |
| ------- | -------- | ---------------------------- |
| bids    | object   | 当前的所有买单 [price, size] |
| asks    | object   | 当前的所有卖单 [price, size] |
| version | integer  | 内部字段                     |
| ts      | integer  | 新加坡时间的时间戳，单位毫秒 |

### 数据请求

支持数据请求方式一次性获取市场深度数据：

```json
{  "req": "market.ethbtc.depth.step0",  "id": "id10"}
```

## 市场深度MBP行情数据（增量推送）

用户可订阅此频道以接收最新深度行情Market By Price (MBP) 的增量数据推送；同时，该频道支持用户以req方式请求获取全量数据。

**MBP增量推送及MBP全量REQ请求地址**

**`wss://api.huobi.sg/feed`**  

**`wss://api-aws.huobi.sg/feed`** 

建议下游数据处理方式：<br>
1）	订阅增量数据并开始缓存；<br>
2）	请求全量数据（同等档位数）并根据该全量消息的seqNum与缓存增量数据中的prevSeqNum对齐；<br>
3）	开始连续增量数据接收与计算，构建并持续更新MBP订单簿；<br>
4）	每条增量数据的prevSeqNum须与前一条增量数据的seqNum一致，否则意味着存在增量数据丢失，须重新获取全量数据并对齐；<br>
5）	如果收到增量数据包含新增price档位，须将该price档位插入MBP订单簿中适当位置；<br>
6）	如果收到增量数据包含已有price档位，但size不同，须替换MBP订单簿中该price档位的size；<br>
7）	如果收到增量数据某price档位的size为0值，须将该price档位从MBP订单簿中删除；<br>
8）	如果收到单条增量数据中包含两个及以上price档位的更新，这些price档位须在MBP订单簿中被同时更新。<br>

当前仅支持5档/20档MBP逐笔增量以及150档MBP快照增量的推送，二者的区别为 -<br>
1） 深度不同；<br>
2） 5档/20档为逐笔增量MBP行情，150档为100毫秒定时快照增量MBP行情；<br>
3） 当5档/20档订单簿仅发生单边行情变化时，增量推送仅包含单边行情更新，比如，推送消息中包含数组asks，但不含数组bids；<br>

```json
{    "ch": "market.ethbtc.mbp.5",    "ts": 1573199608679,    "tick": {        "seqNum": 100020146795,        "prevSeqNum": 100020146794,        "asks": [            [645.140000000000000000, 26.755973959140651643]        ]    }}
```

当150档订单簿仅发生单边行情变化时，增量推送包含双边行情更新，但其中一边行情为空，比如，推送消息中包含数组asks更新的同时，也包含bids空数组；<br>

```json
{    "ch":"market.ethbtc.mbp.150",    "ts":1573199608679,    "tick":{        "seqNum":100020146795,        "prevSeqNum":100020146794,        "bids":[ ],        "asks":[            [645.14,26.75597395914065]        ]    }}
```

未来，150档增量推送的数据行为将与5档/20档增量保持一致，即，单边深度行情变更时，推送消息中将不包含另一边行情深度行情；<br>
4） 当150档订单簿在100毫秒时间间隔内未发生变化时，增量推送包含bids和asks空数组；<br>

```json
{    "ch":"market.ethbtc.mbp.150",    "ts":1585074391470,    "tick":{        "seqNum":100772868478,        "prevSeqNum":100772868476,        "bids":[  ],        "asks":[  ]    }}
```

而5档/20档MBP逐笔增量，在订单簿未发生变化时，不推送数据；<br>
未来，150档增量推送的数据行为将与5档增量保持一致，即，在订单簿未发生变化时，不再推送空消息；<br>
5）5档/20档逐笔增量行情仅支持部分交易对（ethbtc,ltcbtc,bchbtc），150档快照增量支持全部交易对。<br>

REQ频道支持5档/20档/150档全量数据的获取。<br>

### 订阅增量推送

`market.$symbol.mbp.$levels`

> Sub request

```json
{  "sub": "market.ethbtc.mbp.5",  "id": "id1"}
```

### 请求全量数据

`market.$symbol.mbp.$levels`

> Req request

```json
{  "req": "market.ethbtc.mbp.5",  "id": "id2"}
```

### 参数

| 参数   | 数据类型 | 是否必需 | 缺省值 | 描述                                | 取值范围                            |
| ------ | -------- | -------- | ------ | ----------------------------------- | ----------------------------------- |
| symbol | string   | true     | NA     | 交易代码（不支持通配符）            |                                     |
| levels | integer  | true     | NA     | 深度档位（取值：5， 20， 150，400） | 当前仅支持5档，20档，150或400档深度 |

> Response (增量订阅)

```json
{  "id": "id1",  "status": "ok",  "subbed": "market.ethbtc.mbp.5",  "ts": 1489474081631 //system response time}
```

> Incremental Update (增量订阅)

```json
{	"ch": "market.ethbtc.mbp.5",	"ts": 1573199608679, //system update time  "tick": {           "seqNum": 100020146795,            "prevSeqNum": 100020146794,           "asks": [                 [645.140000000000000000, 26.755973959140651643] // [price, size]           ]      }}
```

> Response (全量请求)

```json
{	"id": "id2",	"rep": "market.ethbtc.mbp.150",	"status": "ok",	"data": {		"seqNum": 100020142010,		"bids": [			[618.37, 71.594], // [price, size]			[423.33, 77.726],			[223.18, 47.997],			[219.34, 24.82],			[210.34, 94.463]    ],		"asks": [			[650.59, 14.909733438479636],			[650.63, 97.996],			[650.77, 97.465],			[651.23, 83.973],			[651.42, 34.465]		]	}}
```

### 数据更新字段列表

| 字段       | 数据类型 | 描述                                    |
| ---------- | -------- | --------------------------------------- |
| seqNum     | integer  | 消息序列号                              |
| prevSeqNum | integer  | 上一消息序列号                          |
| bids       | object   | 买盘，按price降序排列，["price","size"] |
| asks       | object   | 卖盘，按price升序排列，["price","size"] |

## 市场深度MBP行情数据（全量推送）

用户可订阅此频道以接收最新深度行情Market By Price (MBP) 的全量数据推送。推送频率为大约100毫秒一次。

### 订阅增量推送

`market.$symbol.mbp.refresh.$levels`

> Sub request

```json
{"sub": "market.ltcbtc.mbp.refresh.20","id": "id1"}
```

### 参数

| 参数   | 数据类型 | 是否必需 | 缺省值 | 描述                     | 取值范围 |
| ------ | -------- | -------- | ------ | ------------------------ | -------- |
| symbol | string   | true     | NA     | 交易代码（不支持通配符） |          |
| levels | integer  | true     | NA     | 深度档位                 | 5,10,20  |

> Response

```json
{"id": "id1","status": "ok","subbed": "market.ethbtc.mbp.refresh.20","ts": 1489474081631 //system response time}
```

> Refresh Update

```json
{"ch": "market.ethbtc.mbp.refresh.20","ts": 1573199608679, //system update time"tick": {		"seqNum": 100020142010,		"bids": [			[618.37, 71.594], // [price, size]			[423.33, 77.726],			[223.18, 47.997],			[219.34, 24.82],			[210.34, 94.463], ... // 省略余下15档   		],		"asks": [			[650.59, 14.909733438479636],			[650.63, 97.996],			[650.77, 97.465],			[651.23, 83.973],			[651.42, 34.465], ... // 省略余下15档		]}}
```

### 数据更新字段列表

| 字段   | 数据类型 | 描述                                    |
| ------ | -------- | --------------------------------------- |
| seqNum | integer  | 消息序列号                              |
| bids   | object   | 买盘，按price降序排列，["price","size"] |
| asks   | object   | 卖盘，按price升序排列，["price","size"] |


## 买一卖一逐笔行情

当买一价、买一量、卖一价、卖一量，其中任一数据发生变化时，此主题推送逐笔更新。

### 主题订阅

`market.$symbol.bbo`

> Subscribe request

```json
{  "sub": "market.ethbtc.bbo",  "id": "id1"}
```

### 参数

| 参数   | 数据类型 | 是否必需 | 缺省值 | 描述     | 取值范围                                              |
| ------ | -------- | -------- | ------ | -------- | ----------------------------------------------------- |
| symbol | string   | true     | NA     | 交易代码 | ltcbtc, ethbtc...（取值参考`GET /v1/common/symbols`） |

> Response

```json
{  "id": "id1",  "status": "ok",  "subbed": "market.ethbtc.bbo",  "ts": 1489474081631 //system response time}
```

> Update example

```json
{  "ch": "market.ethbtc.bbo",  "ts": 1489474082831, //system update time  "tick": {    "symbol": "ltcbtc",    "quoteTime": "1489474082811",    "bid": "10008.31",    "bidSize": "0.01",    "ask": "10009.54",    "askSize": "0.3",    "seqId":"10242474683"  }}
```

### 数据更新字段列表

| 字段      | 数据类型 | 描述         |
| --------- | -------- | ------------ |
| symbol    | string   | 交易代码     |
| quoteTime | long     | 盘口更新时间 |
| bid       | float    | 买一价       |
| bidSize   | float    | 买一量       |
| ask       | float    | 卖一价       |
| askSize   | float    | 卖一量       |
| seqId     | int      | 消息序号     |


## 成交明细

### 主题订阅

此主题提供市场最新成交逐笔明细。

`market.$symbol.trade.detail`

> Subscribe request

```json
{  "sub": "market.ethbtc.trade.detail",  "id": "id1"}
```

### 参数

| 参数   | 数据类型 | 是否必需 | 缺省值 | 描述     | 取值范围                                              |
| ------ | -------- | -------- | ------ | -------- | ----------------------------------------------------- |
| symbol | string   | true     | NA     | 交易代码 | ltcbtc, ethbtc...（取值参考`GET /v1/common/symbols`） |

> Response

```json
{  "id": "id1",  "status": "ok",  "subbed": "market.ethbtc.trade.detail",  "ts": 1489474081631 //system response time}
```

> Update example

```json
{  "ch": "market.ethbtc.trade.detail",  "ts": 1489474082831, //system update time  "tick": {        "id": 14650745135,        "ts": 1533265950234, //trade time        "data": [            {                "amount": 0.0099,                "ts": 1533265950234, //trade time                "id": 146507451359183894799,                "tradeId": 102043494568,                "price": 401.74,                "direction": "buy"            }            // more Trade Detail data here        ]  }}
```

### 数据更新字段列表

| 字段      | 数据类型 | 描述                                           |
| --------- | -------- | ---------------------------------------------- |
| id        | integer  | 唯一成交ID（将被废弃）                         |
| tradeId   | integer  | 唯一成交ID（NEW）                              |
| amount    | float    | 成交量（买或卖一方）                           |
| price     | float    | 成交价                                         |
| ts        | integer  | 成交时间 (UNIX epoch time in millisecond)      |
| direction | string   | 成交主动方 (taker的订单方向) : 'buy' or 'sell' |

### 数据请求

支持数据请求方式一次性获取成交明细数据（仅能获取最多最近300个成交记录）：

```json
{  "req": "market.ethbtc.trade.detail",  "id": "id11"}
```

## 市场概要

### 主题订阅

此主题提供24小时内最新市场概要快照。快照频率不超过每秒10次。

`market.$symbol.detail`

> Subscribe request

```json
{  "sub": "market.ethbtc.detail",  "id": "id1"}
```

### 参数

| 参数   | 数据类型 | 是否必需 | 缺省值 | 描述     | 取值范围            |
| ------ | -------- | -------- | ------ | -------- | ------------------- |
| symbol | string   | true     | NA     | 交易代码 | ltcbtc, ethbtc...等 |

> Response

```json
{  "id": "id1",  "status": "ok",  "subbed": "market.ethbtc.detail",  "ts": 1489474081631 //system response time}
```

> Update example

```json
{  "ch": "market.ethbtc.detail",  "ts": 1494496390001, //system update time  "tick": {    "amount": 12224.2922,    "open":   9790.52,    "close":  10195.00,    "high":   10300.00,    "id":     1494496390,    "count":  15195,    "low":    9657.00,    "vol":    121906001.754751  }}
```

### 数据更新字段列表

| 字段   | 数据类型 | 描述                     |
| ------ | -------- | ------------------------ |
| id     | integer  | unix时间，同时作为消息ID |
| amount | float    | 24小时成交量             |
| count  | integer  | 24小时成交笔数           |
| open   | float    | 24小时开盘价             |
| close  | float    | 最新价                   |
| low    | float    | 24小时最低价             |
| high   | float    | 24小时最高价             |
| vol    | float    | 24小时成交额             |

### 数据请求

支持数据请求方式一次性获取市场概要数据：

```json
{  "req": "market.ethbtc.detail",  "id": "id11"}
```

# Websocket资产及订单

## 简介

### 接入URL

**Websocket资产及订单**

**`wss://api.huobi.sg/ws/v2`**  

**`wss://api-aws.huobi.sg/ws/v2`**   

注：api-aws.huobi.sg域名对使用aws云服务的用户做了一定的链路延迟优化。  

请使用中国大陆以外的服务器访问火币新加坡 API。

### 数据压缩

与行情WebSocket不同，资产和订单返回的数据未进行 GZIP 压缩。

### 心跳消息

当用户的Websocket客户端连接到火币新加坡WebSocket服务器后，服务器会定期（当前设为20秒）向其发送`Ping`消息并包含一整数值如下：

```json
{	"action": "ping",	"data": {		"ts": 1575537778295	}}
```

当用户的Websocket客户端接收到此心跳信息后，应返回`Pong`消息并包含同一整数值：

```json
{    "action": "pong",    "data": {          "ts": 1575537778295 // 使用Ping消息中的ts值    }}
```

### `action`的有效取值

| 有效取值   | 取值说明                             |
| ---------- | ------------------------------------ |
| sub        | 订阅数据                             |
| req        | 数据请求                             |
| ping、pong | 心跳数据                             |
| push       | 推送数据，服务端发送至客户端数据类型 |

### 限频

此版本对用户采取了多维度的限频策略，具体策略如下：

- 限制单连接**有效**的请求（包括req，sub，unsub，不包括ping/pong和其他无效请求)为**50次/秒**（此处秒限制为滑动窗口）。当超过此限制时，会返回"too many request"错误消息。
- 限制单API Key建连总数为**10**。当超过此限制时，会返回"too many connection"错误消息。
- 限制单IP建立连接数为**100次/秒**。当超过次限制时，会返回"too many request"错误消息。

### 鉴权

鉴权请求格式如下：

```json
{    "action": "req",     "ch": "auth",    "params": {         "authType":"api",        "accessKey": "e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx",        "signatureMethod": "HmacSHA256",        "signatureVersion": "2.1",        "timestamp": "2019-09-01T18:16:16",        "signature": "4F65x5A2bLyMWVQj3Aqp+B4w+ivaA7n5Oi2SuYtCJ9o="    }}
```

鉴权成功后返回数据格式如下：

```json
{	"action": "req",	"code": 200,	"ch": "auth",	"data": {}}
```

参数说明

| 字段             | 是否必需 | 数据类型 | 描述                                                         |
| ---------------- | -------- | -------- | ------------------------------------------------------------ |
| action           | true     | string   | Websocket数据操作类型，鉴权固定值为req                       |
| ch               | true     | string   | 请求主题，鉴权固定值为auth                                   |
| authType         | true     | string   | 鉴权类型，鉴权固定值为api。注意，该参数不在签名计算中。      |
| accessKey        | true     | string   | 您申请的API Key中的AccessKey                                 |
| signatureMethod  | true     | string   | 签名方法，用户计算签名寄语哈希的协议，固定值为HmacSHA256     |
| signatureVersion | true     | string   | 签名协议版本，固定值为2.1                                    |
| timestamp        | true     | string   | 时间戳，您发出请求的时间（UTC时间）在查询请求中包含此值有助于防止第三方截取您的请求。如：2017-05-11T16:22:06。再次强调是 (UTC 时区) |
| signature        | true     | string   | 签名, 计算得出的值，用于确保签名有效和未被篡改               |

### 签名步骤

资产和订单WebSocket签名与Rest接口签名步骤相似，具体区别如下：

1. 生成参与签名的字符串时，请求方法固定使用GET，请求地址固定为/ws/v2

2. 生成参与签名的固定参数名替换为：accessKey，signatureMethod，signatureVersion，timestamp

3. signatureVersion版本升级为2.1

Rest接口签名步骤,您可以点击 <a href='https://huobi-sg.github.io/docs/spot/v1/cn/#c64cd15fdc'>这里</a> 获取。

签名前最后生成的字符串如下：

```
GET\napi.huobi.sg\n/ws/v2\naccessKey=0664b695-rfhfg2mkl3-abbf6c5d-49810&signatureMethod=HmacSHA256&signatureVersion=2.1&timestamp=2019-12-05T11%3A53%3A03
```

注：JSON请求中的数据不需要URL编码。

### 订阅主题

成功建立与Websocket服务器的连接后，Websocket客户端发送如下请求以订阅特定主题：

```json
{	"action": "sub",	"ch": "accounts.update"}
```

订阅成功Websocket客户端会接收到如下消息：

```json
{	"action": "sub",	"code": 200,	"ch": "accounts.update#0",	"data": {}}
```

### 请求数据

成功建立Websocket服务器的连接后，Websocket客户端发送如下请求用以获取一次性数据：


```json
{    "action": "req",     "ch": "topic",}
```

请求成功后Websocket客户端会收到如下消息：

```json
{    "action": "req",    "ch": "topic",    "code": 200,    "data": {} // 请求数据体}
```

## 订阅订单更新

API Key 权限：读取

订单的更新推送由任一以下事件触发：<br>

-	计划委托或追踪委托触发失败事件（eventType=trigger）<br>
-	计划委托或追踪委托触发前撤单事件（eventType=deletion）<br>
-	订单创建（eventType=creation）<br>
-	订单成交（eventType=trade）<br>
-	订单撤销（eventType=cancellation）<br>

不同事件类型所推送的消息中，字段列表略有不同。开发者可以采取以下两种方式设计返回的数据结构：<br>

- 定义一个包含所有字段的数据结构，并允许某些字段为空<br>
- 定义不同的数据结构，分别包含各自的字段，并继承自一个包含公共数据字段的数据结构

### 订阅主题

` orders#${symbol}`

### 订阅参数

> Subscribe request

```json
{	"action": "sub",	"ch": "orders#ethbtc"}
```

> Response

```json
{	"action": "sub",	"code": 200,	"ch": "orders#ethbtc",	"data": {}}
```

| 参数   | 数据类型 | 描述                      |
| ------ | -------- | ------------------------- |
| symbol | string   | 交易代码（支持通配符 * ） |


### 数据更新字段列表

> Update example

```json
{	"action":"push",	"ch":"orders#ethbtc",	"data":	{		"orderSide":"buy",		"lastActTime":1583853365586,		"clientOrderId":"abc123",		"orderStatus":"rejected",		"symbol":"ltcbtc",		"eventType":"trigger",		"errCode": 2002,		"errMessage":"invalid.client.order.id (NT)"	}}
```

当计划委托/追踪委托触发失败后 –

| 字段          | 数据类型 | 描述                                                         |
| ------------- | -------- | ------------------------------------------------------------ |
| eventType     | string   | 事件类型，有效值：trigger（本事件仅对计划委托/追踪委托有效） |
| symbol        | string   | 交易代码                                                     |
| clientOrderId | string   | 用户自编订单号                                               |
| orderSide     | string   | 订单方向，有效值：buy,sell                                   |
| orderStatus   | string   | 订单状态，有效值：rejected                                   |
| errCode       | int      | 订单触发失败错误码                                           |
| errMessage    | string   | 订单触发失败错误消息                                         |
| lastActTime   | long     | 订单触发失败时间                                             |

> Update example

```json
{	"action":"push",	"ch":"orders#ethbtc",	"data":	{		"orderSide":"buy",		"lastActTime":1583853365586,		"clientOrderId":"abc123",		"orderStatus":"canceled",		"symbol":"ltcbtc",		"eventType":"deletion"	}}
```

当计划委托/追踪委托在触发前被撤销后 –

| 字段          | 数据类型 | 描述                                                         |
| ------------- | -------- | ------------------------------------------------------------ |
| eventType     | string   | 事件类型，有效值：deletion（本事件仅对计划委托/追踪委托有效） |
| symbol        | string   | 交易代码                                                     |
| clientOrderId | string   | 用户自编订单号                                               |
| orderSide     | string   | 订单方向，有效值：buy,sell                                   |
| orderStatus   | string   | 订单状态，有效值：canceled                                   |
| lastActTime   | long     | 订单撤销时间                                                 |

> Update example

```json
{	"action":"push",	"ch":"orders#ethbtc",	"data":	{		"orderSize":"2.000000000000000000",		"orderCreateTime":1583853365586,		"accountId":992701,		"orderPrice":"77.000000000000000000",		"type":"sell-limit",		"orderId":27163533,		"clientOrderId":"abc123",		"orderSource":"spot-api",		"orderStatus":"submitted",		"symbol":"ethbtc",		"eventType":"creation"	}}
```

当订单挂单后 –

| 字段            | 数据类型 | 描述                                                         |
| --------------- | -------- | ------------------------------------------------------------ |
| eventType       | string   | 事件类型，有效值：creation                                   |
| symbol          | string   | 交易代码                                                     |
| accountId       | long     | 账户ID                                                       |
| orderId         | long     | 订单ID                                                       |
| clientOrderId   | string   | 用户自编订单号（如有）                                       |
| orderSource     | string   | 订单来源                                                     |
| orderPrice      | string   | 订单价格                                                     |
| orderSize       | string   | 订单数量（对市价买单无效）                                   |
| orderValue      | string   | 订单金额（仅对市价买单有效）                                 |
| type            | string   | 订单类型，有效值：buy-market, sell-market, buy-limit, sell-limit, |
| orderStatus     | string   | 订单状态，有效值：submitted                                  |
| orderCreateTime | long     | 订单创建时间                                                 |

注：<br>

- Taker订单在成交前，接口首先推送其创建事件。<br>

> Update example

```json
{	"action":"push",	"ch":"orders#ethbtc",	"data":	{		"tradePrice":"76.000000000000000000",		"tradeVolume":"1.013157894736842100",		"tradeId":301,		"tradeTime":1583854188883,		"aggressor":true,		"remainAmt":"0.000000000000000400000000000000000000",		"execAmt":"2",		"orderId":27163536,		"type":"sell-limit",		"clientOrderId":"abc123",		"orderSource":"spot-api",		"orderPrice":"15000",		"orderSize":"0.01",		"orderStatus":"filled",		"symbol":"ethbtc",		"eventType":"trade"	}}
```

当订单成交后 –

| 字段          | 数据类型 | 描述                                                         |
| ------------- | -------- | ------------------------------------------------------------ |
| eventType     | string   | 事件类型，有效值：trade                                      |
| symbol        | string   | 交易代码                                                     |
| tradePrice    | string   | 成交价                                                       |
| tradeVolume   | string   | 成交量                                                       |
| orderId       | long     | 订单ID                                                       |
| type          | string   | 订单类型，有效值：buy-market, sell-market, buy-limit, sell-limit |
| clientOrderId | string   | 用户自编订单号（如有）                                       |
| orderSource   | string   | 订单来源                                                     |
| orderPrice    | string   | 原始订单价（市价单无效）                                     |
| orderSize     | string   | 原始订单数量（市价买单无效）                                 |
| orderValue    | string   | 原始订单金额（仅对市价买单有效）                             |
| tradeId       | long     | 成交ID                                                       |
| tradeTime     | long     | 成交时间                                                     |
| aggressor     | bool     | 是否交易主动方，有效值： true (taker), false (maker)         |
| orderStatus   | string   | 订单状态，有效值：partial-filled, filled                     |
| remainAmt     | string   | 该订单未成交数量（市价买单为未成交金额）                     |
| execAmt       | string   | 该订单累计成交量（市价买单为成交金额）                       |

注：<br>

- 当一张taker订单同时与对手方多张订单成交后，所产生的每笔成交（tradePrice, tradeVolume, tradeTime, tradeId, aggressor）将被分别推送（而不是合并推送一笔）。<br>

> Update example

```json
{	"action":"push",	"ch":"orders#ethbtc",	"data":	{		"lastActTime":1583853475406,		"remainAmt":"2.000000000000000000",		"execAmt":"2",		"orderId":27163533,		"type":"sell-limit",		"clientOrderId":"abc123",		"orderSource":"spot-api",		"orderPrice":"15000",		"orderSize":"0.01",		"orderStatus":"canceled",		"symbol":"ethbtc",		"eventType":"cancellation"	}}
```

当订单被撤销后 –

| 字段          | 数据类型 | 描述                                                         |
| ------------- | -------- | ------------------------------------------------------------ |
| eventType     | string   | 事件类型，有效值：cancellation                               |
| symbol        | string   | 交易代码                                                     |
| orderId       | long     | 订单ID                                                       |
| type          | string   | 订单类型，有效值：buy-market, sell-market, buy-limit, sell-limit |
| clientOrderId | string   | 用户自编订单号（如有）                                       |
| orderSource   | string   | 订单来源                                                     |
| orderPrice    | string   | 原始订单价（市价单无效）                                     |
| orderSize     | string   | 原始订单数量（市价买单无效）                                 |
| orderValue    | string   | 原始订单金额（仅对市价买单有效）                             |
| orderStatus   | string   | 订单状态，有效值：partial-canceled, canceled                 |
| remainAmt     | string   | 该订单未成交数量（市价买单为未成交金额）                     |
| execAmt       | string   | 该订单累计成交量（市价买单为成交金额）                       |
| lastActTime   | long     | 订单最近更新时间                                             |
| 注：<br>      |          |                                                              |
|               |          |                                                              |

## 订阅清算后成交及撤单更新

API Key 权限：读取

仅当用户订单成交或撤销时推送。其中，订单成交为逐笔推送，如一张 taker 订单同时与多张 maker 订单成交，该接口将推送逐笔更新。但用户收到的这几笔成交消息的次序，有可能与实际的成交次序不完全一致。另外，如果一张订单的成交及撤销几乎同时发生，例如 IOC 订单成交后剩余部分被自动撤销，用户可能会先收到撤单推送，再收到成交推送。<br>

如用户需要获取依次更新的订单推送，建议订阅另一频道 orders#${symbol}。<br>

### 订阅主题

`trade.clearing#${symbol}#${mode}`

### 订阅参数

| 参数   | 数据类型 | 是否必需 | 描述                                                         |
| ------ | -------- | -------- | ------------------------------------------------------------ |
| symbol | string   | TRUE     | 交易代码（支持通配符 * ）                                    |
| mode   | int      | FALSE    | 推送模式（0 - 仅在订单成交时推送；1 - 在订单成交、撤销时均推送；缺省值：0） |

注：<br>
可选订阅参数 mode，如不填或填0，仅推送成交事件；如填1，推送成交及撤销事件。<br>

> Subscribe request

```json
{	"action": "sub",	"ch": "trade.clearing#ltcbtc#0"}
```

> Response

```json
{	"action": "sub",	"code": 200,	"ch": "trade.clearing#ltcbtc#0",	"data": {}}
```

> Update example

```json
{    "ch": "trade.clearing#ltcbtc#0",    "data": {         "eventType": "trade",         "symbol": "ethbtc",         "orderId": 99998888,         "tradePrice": "9999.99",         "tradeVolume": "0.96",         "orderSide": "buy",         "aggressor": true,         "tradeId": 919219323232,         "tradeTime": 998787897878,         "transactFee": "19.88",         "feeDeduct ": "0",         "feeDeductType": "",         "feeCurrency": "btc",         "accountId": 9912791,         "source": "spot-api",         "orderPrice": "10000",         "orderSize": "1",         "clientOrderId": "a001",         "orderCreateTime": 998787897878,         "orderStatus": "partial-filled"    }}
```

### 数据更新字段列表（当订单成交后）

| 字段            | 数据类型 | 描述                                                         |
| --------------- | -------- | ------------------------------------------------------------ |
| eventType       | string   | 事件类型（trade）                                            |
| symbol          | string   | 交易代码                                                     |
| orderId         | long     | 订单ID                                                       |
| tradePrice      | string   | 成交价                                                       |
| tradeVolume     | string   | 成交量                                                       |
| orderSide       | string   | 订单方向，有效值： buy, sell                                 |
| orderType       | string   | 订单类型，有效值： buy-market, sell-market,buy-limit         |
| aggressor       | bool     | 是否交易主动方，有效值： true, false                         |
| tradeId         | long     | 交易ID                                                       |
| tradeTime       | long     | 成交时间，unix time in millisecond                           |
| transactFee     | string   | 交易手续费（正值）或交易手续费返佣（负值）                   |
| feeCurrency     | string   | 交易手续费或交易手续费返佣币种（买单的交易手续费币种为基础币种，卖单的交易手续费币种为计价币种；买单的交易手续费返佣币种为计价币种，卖单的交易手续费返佣币种为基础币种） |
| feeDeduct       | string   | 交易手续费抵扣                                               |
| feeDeductType   | string   | 交易手续费抵扣类型，有效值： ht, point                       |
| accountId       | long     | 账户编号                                                     |
| source          | string   | 订单来源                                                     |
| orderPrice      | string   | 订单价格 （市价单无此字段）                                  |
| orderSize       | string   | 订单数量（市价买单无此字段）                                 |
| orderValue      | string   | 订单金额（仅市价买单有此字段）                               |
| clientOrderId   | string   | 用户自编订单号                                               |
| orderCreateTime | long     | 订单创建时间                                                 |
| orderStatus     | string   | 订单状态，有效值：filled, partial-filled                     |

注：<br>

- transactFee中的交易返佣金额可能不会实时到账；<br>

### 数据更新字段列表（当订单撤销后）

| 字段            | 数据类型 | 描述                                                         |
| --------------- | -------- | ------------------------------------------------------------ |
| eventType       | string   | 事件类型（cancellation）                                     |
| symbol          | string   | 交易代码                                                     |
| orderId         | long     | 订单ID                                                       |
| orderSide       | string   | 订单方向，有效值： buy, sell                                 |
| orderType       | string   | 订单类型，有效值： buy-market, sell-market,buy-limit,sell-limit |
| accountId       | long     | 账户编号                                                     |
| source          | string   | 订单来源                                                     |
| orderPrice      | string   | 订单价格 （市价单无此字段）                                  |
| orderSize       | string   | 订单数量（市价买单无此字段）                                 |
| orderValue      | string   | 订单金额（仅市价买单有此字段）                               |
| clientOrderId   | string   | 用户自编订单号                                               |
| orderCreateTime | long     | 订单创建时间                                                 |
| remainAmt       | string   | 未成交量（对于市价买单，该字段定义为未成交额）               |
| orderStatus     | string   | 订单状态，有效值：canceled, partial-canceled                 |


## 订阅账户变更

API Key 权限：读取

订阅账户的余额更新。

### 订阅主题

`accounts.update#${mode}`

用户可选择以下任一账户变更推送的触发方式

1、仅在账户余额发生变动时推送；

2、在账户余额发生变动或可用余额发生变动时均推送，且分别推送。

3、在账户余额发生变动或可用余额发生变动时均推送，且一起推送。

注意：现货和合约之间的账户划转引起的账户余额变动，暂时没有消息推送。

### 订阅参数

| 参数 | 数据类型 | 描述                                 |
| ---- | -------- | ------------------------------------ |
| mode | integer  | 推送方式，有效值：0，1，2  默认值：0 |

订阅示例  

1、不填mode：  

accounts.update  

仅当账户余额变动时推送；  

2、填写mode=0：  

accounts.update#0  

仅当账户余额变动时推送；  

3、填写mode=1： 

accounts.update#1  

在账户余额发生变动或可用余额发生变动时均推送且分别推送。

4、填写mode=2：  

accounts.update#2

 在账户余额发生变动或可用余额发生变动时均推送且一起推送。

注：无论用户采用哪种模式订阅，在订阅成功后，服务器将首先推送当前各账户的账户余额与可用余额，然后再推送后续的账户更新。在首推各账户初始值时，消息中的changeType和changeTime的值为null。

> Subscribe request

```json
{	"action": "sub",	"ch": "accounts.update"}
```

> Response

```json
{	"action": "sub",	"code": 200,	"ch": "accounts.update#0",	"data": {}}
```

> Update example

```json
accounts.update#0：{	"action": "push",	"ch": "accounts.update#0",	"data": {		"currency": "btc",		"accountId": 123456,		"balance": "23.111",		"changeType": "transfer",           	"accountType":"trade",		"changeTime": 1568601800000	}}accounts.update#1：{	"action": "push",	"ch": "accounts.update#1",	"data": {		"currency": "btc",		"accountId": 33385,		"available": "2028.699426619837209087",		"changeType": "order.match",         		"accountType":"trade",		"changeTime": 1574393385167	}}{	"action": "push",	"ch": "accounts.update#1",	"data": {		"currency": "btc",		"accountId": 33385,		"balance": "2065.100267619837209301",		"changeType": "order.match",           	"accountType":"trade",		"changeTime": 1574393385122	}}
```

### 数据更新字段列表

| 字段        | 数据类型 | 描述                                                         |
| ----------- | -------- | ------------------------------------------------------------ |
| currency    | string   | 币种                                                         |
| accountId   | long     | 账户ID                                                       |
| balance     | string   | 账户余额（仅当账户余额发生变动时推送）                       |
| available   | string   | 可用余额（仅当可用余额发生变动时推送）                       |
| changeType  | string   | 余额变动类型，有效值：order-place(订单创建)，order-match(订单成交)，order-refund(订单成交退款)，order-cancel(订单撤销)，deposit (充币）, withdraw (提币)，other(其他资产变化) |
| accountType | string   | 账户类型，有效值：trade, loan, interest                      |
| changeTime  | long     | 余额变动时间，unix time in millisecond                       |

注：<br>
账户更新推送的是到账金额，多笔成交产生的多笔交易返佣可能会合并到帐。<br>

## 常见错误码

以下是WebSocket资产和订单接口的错误码、错误消息和说明。

| 错误码 | 错误消息                 | 说明                                                         |
| ------ | ------------------------ | ------------------------------------------------------------ |
| 200    | 正确                     | 正确返回                                                     |
| 100    | 超时关闭                 | 超时关闭                                                     |
| 400    | Bad Request              | 请求错误                                                     |
| 404    | Not Found                | 找不到服务                                                   |
| 429    | Too Many Requests        | 超过单机服务最大连接数或者超过单IP最大连接数                 |
| 500    | 系统异常                 | 系统错误                                                     |
| 2000   | invalid.ip               | 无效的ip                                                     |
| 2001   | nvalid.json              | 无效的请求json                                               |
| 2001   | invalid.authType         | 验签方式错误                                                 |
| 2001   | invalid.action           | 无效的订阅事件                                               |
| 2001   | invalid.symbol           | 无效的交易对                                                 |
| 2001   | invalid.ch               | 无效的订阅                                                   |
| 2001   | invalid.exchange         | 无效的交易所code                                             |
| 2001   | missing.param.auth       | 缺少验签参数                                                 |
| 2002   | invalid.auth.state       | 认证未通过                                                   |
| 2002   | auth.fail                | 验签失败，包括API Key绑定的IP错误                            |
| 2003   | query.account.list.error | 查询账户列表失败                                             |
| 4000   | too.many.request         | 客户端上行请求限频（单个实例50次/秒）                        |
| 4000   | too.many.connection      | 同一个API Key的建联数量超过服务器单个实例限制（单个实例最多连接10个） |


