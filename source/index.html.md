---

---

title: New Huo Singapore API Doc

language_tabs: # must be one of https://git.io/vQNgJ

  - json

toc_footers:

  - <a href='https://www.huobi.sg/en-us/login/?backUrl=%2Fen-us%2Fapikey%2F'>Create API Key </a>
    includes:

search: true

# Change Log



<style>
table {
    max-width:100%
}
table th {
    white-space: nowrap; /*表头内容强制在一行显示*/
}
</style>


| Release Date<br>(UTC +8) | API                     | Update | Description              |
| ------------------------ | ----------------------- | ------ | ------------------------ |
| 2021.8.24                | `market.$symbol.ticker` | New    | Add Market（Ticker) data |
|                          |                         |        |                          |

# 

# Introduction

Welcome to New Huo Singapore API！  

This is the official New Huo Singapore API document, and will be continue updating. New Huo will also publish API announcement in advance for any API change. Please subscribe to our announcements so that you can get the latest updates.

You can click <a href='https://huobisg.zendesk.com/hc/en-us/sections/4407023586585-API-Announcements'>Here</a> to view the announcements. If you want to subscribe, please click "Follow" button in the top right of the page. After login and click "Follow" again, then choose the type you want to follow. After you subscribe, the button will be changed to "Following". If you don't have any account, you need to register first in the login dialog.

**How to read this document**

The top of the document is the navigation menu for different API business; The language button in the top right is for different languages, it supports Chinese and English right now.
The main content of each API document has three parts, the left hand side is the contents, the middle part is the document body, and the right hand side is the request and response sameple.

Below is the content for Spot API document

The first part is the overview:

- **Quick Start**: It introduces the overall knowledge of New Huo Singapore API, and suitability for new New Huo Singapore API user
- **API Explorer**: It introduces the API Explorer online tool, which is convenient for user to invoke and observe the API
- **FAQ**: It lists the frequently asked questions regardless the specific API
- **Contact Us**: It introduces how to contact us according to different subjects

The second part is detail for each API. Each API category is listed in one section, and each each section has below contents:

- **Introduction**: It introduces notes and description for this API category
- ***Specific API***: It introduces the usage, rate limit, request, parameters and response for each API
- **Error Code**: It lists the common error code and the description for this API category
- **FAQ**: It lists the frequently asked questions for this API category

# Quick Start

## Preparation

Before you use API, you need to login the website to create API Key with proper permissions. The API key is shared for all instruments in New Huo including spot, futures, swap, options.

You can manage your API Keys <a href='https://www.huobi.sg/en-us/login/?backUrl=%2Fzh-cn%2Fapikey%2F'>here</a>.

Every user can create at most 20 API Keys, each can be applied with either permission below:

- Read permission: It is used to query the data, such as order query, trade query.
- Trade permission: It is used to create order, cancel order and transfer, etc.
- Withdraw permission: It is used to create withdraw order, cancel withdraw order, etc.

Please remember below information after creation:

- `Access Key`  It is used in API request

- `Secret Key`  It is used to generate the signature (only visible once after creation)

<aside class="notice">
The API Key can bind maximum 20 IP addresses (either host IP or network IP), we strongly suggest you bind IP address for security purpose. The API Key without IP binding will be expired after 90 days.
</aside>
<aside class="warning">
<red><b>Warning</b></red>: These two keys are important to your account safety, please don't share <b>both</b> of them together to anyone else (including any product or person from New Huo). If you find your API Key is disposed, please remove it immediately.
</aside> 




## SDK and Demo

**SDK (Suggested)**

[Java](https://github.com/New HuoRDCenter/huobi_Java) | [Python3](https://github.com/New HuoRDCenter/huobi_Python) | [C++](https://github.com/New HuoRDCenter/huobi_Cpp) | [C#](https://github.com/New HuoRDCenter/huobi_CSharp) | [Go](https://github.com/huobirdcenter/huobi_golang)

**Other Demos**

[https://github.com/huobi-sg?tab=repositories](https://github.com/huobi-sg?tab=repositories)

## Testnet (Stopped)

The testnet has been alive for months, however the active user count is rather low and the cost is high, after considering carefully we decide to shutdown the testnet environment.

It is suggest you use live environment, which is more stable and has more liquidity.

## Interface Type

There are two types of interface, you can choose the proper one according to your scenario and preferences.

### REST API

REST (Representational State Transfer) is one of the most popular communication mechanism under HTTP, each URL represents a type of resource.

It is suggested to use Rest API for one-off operation, like trading and withdraw.

### WebSocket API

WebSocket is a new protocol in HTML5. It is full-duplex between client and server. The connection can be established by a single handshake, and then server can push the notification to client actively.

It is suggest to use WebSocket API to get data update, like market data and order update.

**Authentication**

Both API has two levels of authentication:

Public API: It is for basic information and market data. It doesn't need authentication.

Private API: It is for account related operation like trading and account management. Each private API must be authenticated with API Key.

## Access URLs

You can compare the network latency between two domain <u>api.huobi.sg</u> and <u>api-aws.huobi.sg</u>, and then choose the better one for you.

In general, the domain <u>api-aws.huobi.sg</u> is optimized for AWS client, the latency will be lower.

**REST API**

**`https://api.huobi.sg`**  

**Websocket Feed (market data except MBP incremental)**

**`wss://api.huobi.sg/ws`**  



**Websocket Feed (account and order)**

**`wss://api.huobi.sg/ws/v`**  


<aside class="notice">
Please initiate API calls with non-China IP.
</aside>
<aside class="notice">
It is not recommended to use proxy to access New Huo Singapore API because it will introduce high latency and low stability.
</aside>
<aside class="notice">
It is recommended to access New Huo Singapore API from AWS Japan for better stability. If your server is in China mainland, it may be not stable.
</aside> 



## Authentication

### Overview

The API request may be tampered during internet, therefore all private API must be signed by your API Key (Secrete Key).

Each API Key has permission property, please check the API permission, and make sure your API key has proper permission.

A valid request consists of below parts:

- API Path: Server Access address api.huobi.sg，for example <u>api.huobi.sg/v1/order/orders</u>
- API Access Key: The 'Access Key' in your API Key
- Signature Method: The Hash method that is used to sign, it uses **HmacSHA256**
- Signature Version: The version for the signature protocol, it uses **2**
- Timestamp: The UTC time when the request is sent, e.g. 2017-05-11T16:22:06. It is useful to prevent the request to be intercepted by third-party.
- Parameters: Each API Method has a group of parameters, you can refer to detailed document for each of them. 
  - For GET request, all the parameters must be signed.
  - For POST request, the parameters needn't be signed and they should be put in request body.
- Signature: The value after signed, it is guarantee the signature is valid and the request is not be tempered.

### Signature Method

The signature may be different if the request text is different, therefore the request should be normalized before signing. Below signing steps take the order query as an example:

This is a full URL to query one order:

`https://api.huobi.sg/v1/order/orders?`

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`&SignatureMethod=HmacSHA256`

`&SignatureVersion=2`

`&Timestamp=2017-05-11T15:19:30`

`&order-id=1234567890`

**1. The request Method (GET or POST, WebSocket use GET), append line break “\n”**

`GET\n`

**2. The host with lower case, append line break “\n”**

Example:
`
api.huobi.sg\n
`

**3. The path, append line break “\n”**

For example, query orders:

`
/v1/order/orders\n
`



For example, WebSocket v2

`/ws/v2`

**4. The parameters are URL encoded, and ordered based on ASCII**

For example below is the original parameters:

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`order-id=1234567890`

`SignatureMethod=HmacSHA256`

`SignatureVersion=2`

`Timestamp=2017-05-11T15%3A19%3A30`

<aside class="notice">
Use UTF-8 encoding and URL encoded, the hex must be upper case. For example, The semicolon ':' should be encoded as '%3A', The space should be encoded as '%20'.
</aside>
<aside class="notice">
The 'timestamp' should be formated as 'YYYY-MM-DDThh:mm:ss' and URL encoded. The value is valid within 5 minutes.
</aside>



Then above parameter should be ordered like below:


`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`SignatureMethod=HmacSHA256`

`SignatureVersion=2`

`Timestamp=2017-05-11T15%3A19%3A30`

`order-id=1234567890`

**5. Use char  “&” to concatenate all parameters**


`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30&order-id=1234567890`

**6. Assemble the pre-signed text**

`GET\n`

`api.huobi.sg\n`

`/v1/order/orders\n`

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30&order-id=1234567890`


**7. Use the pre-signed text and your Secret Key to generate a signature**

- Use the pre-signed text in step 6 and your API Secret Key to generate hash code by HmacSHA256 hash function.
- Encode the hash code with base-64 to generate the signature.

`4F65x5A2bLyMWVQj3Aqp+B4w+ivaA7n5Oi2SuYtCJ9o=`

**8. Put the signature into request URL**

For Rest interface:

1. Put all the parameters in the URL
2. Encode signature by URL encoding and append in the URL with parameter name “Signature”.

Finally, the request sent to API should be:

`https://api.huobi.sg/v1/order/orders?AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&order-id=1234567890&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30&Signature=4F65x5A2bLyMWVQj3Aqp%2BB4w%2BivaA7n5Oi2SuYtCJ9o%3D`



For WebSocket interface:

1. Fill the value according to required JSON schema
2. The value in JSON doesn't require URL encode

For example:

`{
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
}`

## 




## Glossary

### Trading symbols

The trading symbols are consist of base currency and quote currency. Take the symbol `ETH/BTC` as an example, `ETH` is the base currency, and `BTC` is the quote currency.  

The **base-currency** refers to the denominator token.

The **quote-currency** refers to the numerator token being priced.   

### Account

The `account-id` defines the Identity for different business type, it can be retrieved from API `/v1/account/accounts` , where the `account-type` is the business types.
The types include:

* spot: Spot account

# API Access

## Overview

| Category    | URL Path                     | Description                                                  |
| ----------- | ---------------------------- | ------------------------------------------------------------ |
| Common      | /v1/common/*                 | Common interface, including currency, currency pair, timestamp, etc |
| Market Data | /market/*                    | Market data interface, including trading, depth, quotation, etc |
| Account     | /v1/account/*  /v1/subuser/* | Account interface, including account information, sub-user ,etc |
| Order       | /v1/order/*                  | Order interface, including order creation, cancellation, query, etc |

Above is a general category, it doesn't cover all API, you can refer to detailed API document according to your requirement.

## New Version Rate limit Rule

- Only those endpoints marked with rate limit value and a bracketed 'NEW' are applied with new rate limit rule.<br>

- The new version rate limit is applied on UID basis, which means, the overall access rate, from all API keys under same UID, to single endpoint, shouldn’t exceed the rate limit applied on that endpoint.<br>

- It is suggested to read HTTP Header `X-HB-RateLimit-Requests-Remain` and `X-HB-RateLimit-Requests-Expire` to get the remaining count of request and the expire time for current rate limit time window, then you can adjust the API access rate dynamically.<br>


## Rate Limiting Rule

Except those endpoints which are marked with new rate limit value separately, following rate limit rules are applicable -

* Each API Key is limited to 10 times per second
* If API Key is empty in request, then each IP is limited to 10 times per second

Endpoints marked with rate limit value separately are applied with new rate limit rule. See "new version rate limit rule" sector of this document.

For example

* Order interface is limited by API Key: no more than 10 times within 1 sec
* Market data interface is limited by IP: no more than 10 times within 1 sec

## Request Format

The API is restful and there are two method: GET and POST.

* GET request: All parameters are included in URL
* POST request: All parameters are formatted as JSON and put int the request body

## Response Format

**v1Response Format**：The response is JSON format.There are four fields in the top level: `status`, `ch`, `ts` and `data`. The first three fields indicate the general status, the business data is is under `data` field.

Below is an example of response:

```json
{
  "status": "ok",
  "ch": "market.ethbtc.kline.1day",
  "ts": 1499223904680,
  "data": // per API response data in nested JSON object
}
```

| Field  | Data Type | Description                                                  |
| ------ | --------- | ------------------------------------------------------------ |
| status | string    | Status of API response                                       |
| ch     | string    | The data stream. It may be empty as some API doesn't have data stream |
| ts     | int       | The UTC timestamp when API respond, the unit is millisecond  |
| data   | object    | The body data in response                                    |

**v2Response Format**：There are three fields at the top layer: `code`, `message` and `data`. The first two fields represent the return code and error message. The actual business data is in the `data` field.

The following is a sample of the return response：

```json
{
  "code": 200,
  "message": "",
  "data": // per API response data in nested JSON object
}
```

| Parameter Name | Data type | Description            |
| -------------- | --------- | ---------------------- |
| code           | int       | API return code        |
| message        | string    | error message (if any) |
| data           | object    | returns data subject   |

## 

##  Data Type

The JSON data type described in this document is defined as below:

- `string`: a sequence of characters that are quoted
- `int`: a 32-bit integer, mainly used for status code, size and count
- `long`: a 64-bit integer, mainly used for Id and timestamp
- `float`: a fraction represented in decimal format, mainly used for volume and price, recommend to use high precision decimal data types in program
- `object`: object, contains a child object{}
- `array`: array containing multiple objects

## Best Practice

### Security

- It is strongly suggested to bind your IP with your API Key to ensure that your API Key can only be used in your machine. Furthermore, your API Key will be expired after 90 days if it is not binded with any IP.
- It is strongly suggested not to share your API Key with any body or third-party software, otherwise your personal information and asset may be stolen. If your expose your API Key by accident, please do delete the API Key and create a new one.

### General

**API Access**

- It is suggested not to use temporary domain or proxy, which may be not stable.
- It is suggested to use AWS Japan to access API for lower latency
- It is suggested to connect to domain `api.huobi.sg, api-aws.huobi.sg，` if your server is based on AWS, because this domain is optimized for AWS client, the latency will be lower.

**New Version Rate limit Rule**

- Only those endpoints marked with rate limit value separately are applied with new rate limit rule.

- It is suggested to read HTTP Header `X-HB-RateLimit-Requests-Remain` and `X-HB-RateLimit-Requests-Expire` to get the remaining count of request and the expire time for current rate limit time window, then you can adjust the API access rate dynamically.

- The overall access rate, from all API keys under same UID, to single endpoint, shouldn’t exceed the rate limit applied on that endpoint.

### Market

**Market data**

- It is suggested to use WebSocket interface to subscribe the market update and then cache the data locally, because WebSocket notification has lower latency and not have rate limit.
- It is suggested not to subscribe too many topics in a single websocket connection, it may generate more notifications and cause network latency and disconnection.

**Latest trade**

- It is suggested to subscribe WebSocket topic `market.$symbol.trade.detail`, the response field `price` represents the latest price, and it has lower latency.
- It is suggested to use `tradeId` to de-duplicate if you subscribe WebSocket topic `market.$symbol.trade.detail`.

**Depth**

- It is suggested to subscribe WebSocket topic `market.$symbol.bbo` if you only need the best bid and best offer.
- It is suggested to subscribe WebSocket topic `market.$symbol.depth.$type` if you need multiple bid and offer with normal latency.
- It is suggested to subscribe WebSocket topic `market.$symbol.mbp.$level` if you need multiple bid and offer with lower latency
- It is suggested to use `version` field to de-duplicate and discard the smaller data if you use Rest interface `/market/depth` and WebSocket topic `market.$symbol.depth.$type`. It is suggest to use `seqNum` to de-duplicate and discard the smaller data if yo subscribe WebSocket topic `market.$symbol.mbp.$levels`.

**Get the latest transaction**

- It is recommended that when subscribing to WebSocket transaction details (`market.$symbol.trade.detail`), to eliminate duplicate data as per the tradeId field. 

###Order

**Place an order (/v1/order/orders/place)**

- It is suggested to follow the symbol reference (`/v1/common/symbols`) to validate the amount and value before placing the older, otherwise you may place an invalid order and waste your time.
- It is suggested to provide an unique `client-order-id` field when placing the order, it is useful to track your orders status if you fail to get the order id response. Later you can use the `client-order-id` to match the WebSocket order notification or query order detail by interface `/v1/order/orders/getClientOrder`.The uniqueness of the clientOrderId passed in when you place an order will no longer be verified. We recommend you to manage clientOrderId by yourself to ensure its uniqueness. If multiple orders use the same clientOrderId, the latest order corresponding to the clientOrderId will be returned when querying/canceling an order.

**Search history olders (/v1/order/orders)**

- It is recommended to use `start-time` and `end-time` to query, that are two timestamps with 13 digits (millisecond). The maximum query time window is 48 hours (2 days), the more precision you provide, the better performance you will get. You can query for multiple iterations. 

**Order update**

- It is suggested to subscribe WebSocket topic `orders.$symbol.update`, which has lower latency and more accurate sequence.
- It is suggested not to subscribe WebSocket topic `orders.$symbol`,which is replaced by `orders.$symbol.update`, and will be retired later.

###Account

**Asset update**

- It is suggested to subscribe both WebSocket topic `orders.$symbol.update` and `account.update#${mode}`. The former one tells the order status update and arrives earlier than the latter one, and the latter one confirms the final asset balance.
- It is suggested not to subscribe WebSocket topic `accounts`, which is replaced by `accounts.update#${mode}`, and will be retired later.



# Contact Us

## Market Maker Program

It is very welcome for market maker who has good market making strategy and large trading volume. If your New Huo Spot account or Contract account has at least 10 BTC, you can send your email to:

- Contact customer support from Help Center or send email to [customersupport@huobi.sg](mailto:customersupport@huobi.sg).

And provide below details:

1. UID (not linked to any rebate program in any accounts)
2. Screenshot of trading volume in other transaction platform (such as trading volume within 30 days, or VIP status)
3. A brief description of your market-making strategy 

<aside class="notice">
Market makers will not be able to use point cards, VIP rate, rebate or any other fee promotion.
</aside>



## Technical Support

If you have any other questions on API, you can contact us by below ways:

- Contact customer support from Help Center or send email to [customersupport@huobi.sg](mailto:customersupport@huobi.sg).

If you encounter API errors, please use below template in your feedback:

`1. Problem description`  
`2. UID, Account Id and Order Id (if related with account and order)`  
`3. Raw URL request`  
`4. Raw JSON request (if any)`  
`5. Raw JSON response`  
`6. Problem time and frequency (such as, when this problem occurs, whether it is reproducible)`  
`7. Pre-signed text (mandatory for authentication issue)`  

Below is an example：

`1. Problem description: API authentication error`  
`2. UID：123456`  
`3. Raw URL request: https://api.huobi.sg/v1/account/accounts?&SignatureVersion=2&SignatureMethod=HmacSHA256&Timestamp=2019-11-06T03%3A25%3A39&AccessKeyId=rfhxxxxx-950000847-boooooo3-432c0&Signature=HhJwApXKpaLPewiYLczwfLkoTPnFPHgyF61iq0iTFF8%3D`  
`4. Raw JSON request: N/A`  
`5. Raw JSON response：{"status":"error","err-code":"api-signature-not-valid","err-msg":"Signature not valid: Incorrect Access key [Access key错误]","data":null}`  
`6. Problem time and frequency: It occurs every time`  
`7. Pre-signed text:`  
`GET\n`  
`api.huobi.sg\n`  
`/v1/account/accounts\n`    
`AccessKeyId=rfhxxxxx-950000847-boooooo3-432c0&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2019-11-06T03%3A26%3A13`

Note：It is safe to share your Access Key, which is to prove your identity, and it will not affect your account safety. Remember do **not** share your `Secret Key` to any one. If you expose your `Secret Key` by accident, please [remove](https://www.hbg.com/en-us/apikey/) the related API Key immediately.



# Market Data

## Introduction

Market data APIs provide public market information such as varies of candlestick, depth and trade information.

The market data is updated **once per second**. 

## Get Klines(Candles)

This interface returns historical K-line data. The K-line cycle is calculated based on SGT time. For example, the starting cycle of the daily K-line is 0:00 SGT time to 0:00 SGT the next day.

<aside class="notice">The current REST API does not support custom time intervals. If you need historical data in a fixed time range, please refer to the K-line interface in the Websocket API.</aside>
<aside class="notice">To obtain the net value of btc, please fill in the token symbol "btc".</aside>

```shell
curl "https://api.huobi.sg/market/history/kline?period=1day&size=200&symbol=ethbtc"
```

### 

### HTTP Request

- GET `/market/history/kline`

Query Parameters

| Parameter | Data Type | Required | Default | Description                 | Value Range                                                  |
| --------- | --------- | -------- | ------- | --------------------------- | ------------------------------------------------------------ |
| symbol    | string    | true     | NA      | The trading symbol to query | ethbtc                                                       |
| period    | string    | true     | NA      | The period of each candle   | 1min, 5min, 15min, 30min, 60min, 4hour, 1day, 1mon, 1week, 1year |
| size      | integer   | false    | 150     | The number of data returns  | [1, 2000]                                                    |



> Response:

```json
"data": [
  {
    "id": 1499184000,
    "amount": 37593.0266,
    "count": 0,
    "open": 1935.2000,
    "close": 1879.0000,
    "low": 1856.0000,
    "high": 1940.0000,
    "vol": 71031537.97866500
  }
]
```

### Response Content

| Field  | Data Type | Description                                  |
| ------ | --------- | -------------------------------------------- |
| id     | long      | The UNIX timestamp in seconds as response id |
| amount | float     | Accumulated trading volume, in base currency |
| count  | integer   | The number of completed trades               |
| open   | float     | The opening price                            |
| close  | float     | The closing price                            |
| low    | float     | The low price                                |
| high   | float     | The high price                               |
| vol    | float     | Accumulated trading value, in quote currency |

## Get Latest Aggregated Ticker

This endpoint retrieves the latest ticker with some important 24h aggregated market data.

```shell
curl "https://api.huobi.sg/market/detail/merged?symbol=ethbtc"
```



### HTTP Request

- GET `/market/detail/merged`



### Request Parameters

| Parameter | Data Type | Required | Default | Description                 | Value Range                                                  |
| --------- | --------- | -------- | ------- | --------------------------- | ------------------------------------------------------------ |
| symbol    | string    | true     | NA      | The trading symbol to query | All supported trading symbol, e.g. ltcbtc, ethbtc...Refer to `GET /v1/common/symbols` |

> The above command returns JSON structured like this:

```json
{  "id":1499225271,  "ts":1499225271000,  "close":1885.0000,  "open":1960.0000,  "high":1985.0000,  "low":1856.0000,  "amount":81486.2926,  "count":42122,  "vol":157052744.85708200,  "ask":[1885.0000,21.8804],  "bid":[1884.0000,1.6702]}
```

### Response Content

| Field  | Data Type | Description                                                  |
| ------ | --------- | ------------------------------------------------------------ |
| id     | long      | The internal identity                                        |
| amount | float     | Accumulated trading volume of last 24 hours (rotating 24h), in base currency |
| count  | integer   | The number of completed trades (rotating 24h)                |
| open   | float     | The opening price of last 24 hours (rotating 24h)            |
| close  | float     | The last price of last 24 hours (rotating 24h)               |
| low    | float     | The lowest price of last 24 hours (rotating 24h)             |
| high   | float     | The highest price of last 24 hours (rotating 24h)            |
| vol    | float     | Accumulated trading value of last 24 hours (rotating 24h), in quote currency |
| bid    | object    | The current best bid in format [price, size]                 |
| ask    | object    | The current best ask in format [price, size]                 |

## Get Latest Tickers for All Pairs

This endpoint retrieves the latest tickers for all supported pairs.

```shell
curl "https://api.huobi.sg/market/tickers"
```

<aside class="notice">The returned data object can contain large amount of tickers.</aside>

### HTTP Request

GET `/market/tickers`

### Request Parameters

No parameters are needed for this endpoint.

> Response:

```json
"data": [  
    {  
        "open":0.044297,
        "close":0.042178,
        "low":0.040110,
        "high":0.045255,
        "amount":12880.8510,  
        "count":12838,
        "vol":563.0388715740,
        "symbol":"ethbtc",
        "bid":0.007545,
        "bidSize":0.008,
        "ask":0.008088,
        "askSize":0.009
    },
    {  
        "open":0.008545,
        "close":0.008656,
        "low":0.008088,
        "high":0.009388,
        "amount":88056.1860,
        "count":16077,
        "vol":771.7975953754,
        "symbol":"ltcbtc",
        "bid":0.007545,
        "bidSize":0.008,
        "ask":0.008088,
        "askSize":0.009
    }
]
```

### Response Content

Response content is an array of object, each object has below fields.

| Field   | Data Type | Description                                                  |
| ------- | --------- | ------------------------------------------------------------ |
| amount  | float     | The aggregated trading volume in last 24 hours (rotating 24h) |
| count   | integer   | The number of completed trades of last 24 hours (rotating 24h) |
| open    | float     | The opening price of a nature day (Singapore time)           |
| close   | float     | The closing price of a nature day (Singapore time)           |
| low     | float     | The lowest price of a nature day (Singapore time)            |
| high    | float     | The highest price of a nature day (Singapore time)           |
| vol     | float     | The aggregated trading value in last 24 hours (rotating 24h) |
| symbol  | string    | The trading symbol of this object, e.g. ltcbtc, ethbtc       |
| bid     | float     | Best bid price                                               |
| bidSize | float     | Best bid size                                                |
| ask     | float     | Best ask price                                               |
| askSize | float     | Best ask size                                                |

## Get Market Depth

This endpoint retrieves the current order book of a specific pair.

```shell
curl "https://api.huobi.sg/market/depth?symbol=ethbtc&type=step2"
```

### HTTP Reques

GET `/market/depth`

### Request Parameters

| Parameter | Data Type | Required | Default Value | Description                                       | Value Range                                        |
| --------- | --------- | -------- | ------------- | ------------------------------------------------- | -------------------------------------------------- |
| symbol    | string    | true     | NA            | The trading symbol to query                       | Ltcbtc, ethbtc...Refer to `GET /v1/common/symbols` |
| depth     | integer   | false    | 20            | The number of market depth to return on each side | 5, 10, 20                                          |
| type      | string    | true     | step0         | Market depth aggregation level, details below     | step0, step1, step2, step3, step4, step5           |

<aside class="notice">when type is set to "step0", the default value of "depth" is 150 instead of 20.</aside>

**"type" Details**

| Value | Description                          |
| ----- | ------------------------------------ |
| step0 | No market depth aggregation          |
| step1 | Aggregation level = precision*10     |
| step2 | Aggregation level = precision*100    |
| step3 | Aggregation level = precision*1000   |
| step4 | Aggregation level = precision*10000  |
| step5 | Aggregation level = precision*100000 |

> Response:

```json
{    "version": 31615842081,    "ts": 1489464585407,    "bids": [      [7964, 0.0678], // [price, size]      [7963, 0.9162],      [7961, 0.1],      [7960, 12.8898],      [7958, 1.2],      ...    ],    "asks": [      [7979, 0.0736],      [7980, 1.0292],      [7981, 5.5652],      [7986, 0.2416],      [7990, 1.9970],      ...    ]  }
```

### Response Content

<aside class="notice">The returned data object is under 'tick' object instead of 'data' object in the top level JSON</aside>

| Field   | Data Type | Description                                                  |
| ------- | --------- | ------------------------------------------------------------ |
| ts      | integer   | The UNIX timestamp in milliseconds is adjusted to Singapore time |
| version | integer   | Internal data                                                |
| bids    | object    | The current all bids in format [price, size]                 |
| asks    | object    | The current all asks in format [price, size]                 |


## Get the Last Trade

This endpoint retrieves the latest trade with its price, volume, and direction.

```shell
curl "https://api.huobi.sg/market/trade?symbol=ethbtc"
```



### HTTP Request

- GET `/market/trade`

### Request Parameters

| Parameter | Data Type | Required | Default Value | Description                 | Value Range                                        |
| --------- | --------- | -------- | ------------- | --------------------------- | -------------------------------------------------- |
| symbol    | string    | true     | NA            | The trading symbol to query | ltcbtc, ethbtc...Refer to `GET /v1/common/symbols` |

> Response:

```json
"tick": {    "id": 600848670,    "ts": 1489464451000,    "data": [      {        "id": 600848670,        "trade-id": 102043494568,        "price": 7962.62,        "amount": 0.0122,        "direction": "buy",        "ts": 1489464451000      }    ]}
```

### Response Content

<aside class="notice">The returned data object is under 'tick' object instead of 'data' object in the top level JSON</aside>

| Parameter | Data Type | Description                                                  |
| --------- | --------- | ------------------------------------------------------------ |
| id        | integer   | The unique trade id of this trade (to be obsoleted)          |
| trade-id  | integer   | The unique trade id (NEW)                                    |
| amount    | float     | The trading volume in base currency                          |
| price     | float     | The trading price in quote currency                          |
| ts        | integer   | The UNIX timestamp in milliseconds adjusted to Singapore time |
| direction | string    | The direction of the taker trade: 'buy' or 'sell'            |

## Get the Most Recent Trades

This endpoint retrieves the most recent trades with their price, volume, and direction.

```shell
curl "https://api.huobi.sg/market/history/trade?symbol=ethbtc&size=2"
```



### HTTP Request

GET `/market/history/trade`



### Request Parameters

| Parameter | Data Type | Required | Default Value | Description                 | Value Range                                         |
| --------- | --------- | -------- | ------------- | --------------------------- | --------------------------------------------------- |
| symbol    | string    | true     | NA            | The trading symbol to query | ltcbtc, ethbtc....Refer to `GET /v1/common/symbols` |
| size      | integer   | false    | 1             | The number of data returns  | [1, 2000]                                           |

> Response:

```json
"data": [     {        "id":31618787514,      "ts":1544390317905,      "data":[           {              "amount":9.000000000000000000,            "ts":1544390317905,            "id":3161878751418918529341,            "trade-id": 102043495672,            "price":94.690000000000000000,            "direction":"sell"         },         {              "amount":73.771000000000000000,            "ts":1544390317905,            "id":3161878751418918532514,            "trade-id": 102043495673,            "price":94.660000000000000000,            "direction":"sell"         }      ]   },   {        "id":31618776989,      "ts":1544390311353,      "data":[           {              "amount":1.000000000000000000,            "ts":1544390311353,            "id":3161877698918918522622,            "trade-id": 102043495674,            "price":94.710000000000000000,            "direction":"buy"         }      ]   }}
```

### Response Content

<aside class="notice">The returned data object is an array which represents one recent timestamp; each timestamp object again is an array which represents all trades occurred at this timestamp.</aside>

| Field     | Data Type | Description                                                  |
| --------- | --------- | ------------------------------------------------------------ |
| id        | integer   | The unique trade id of this trade (to be obsoleted)          |
| trade-id  | integer   | The unique trade id (NEW)                                    |
| amount    | float     | The trading volume in base currency                          |
| price     | float     | The trading price in quote currency                          |
| ts        | integer   | The UNIX timestamp in milliseconds adjusted to Singapore time |
| direction | string    | The direction of the taker trade: 'buy' or 'sell'            |

## Get the Last 24h Market Summary

This endpoint retrieves the summary of trading in the market for the last 24 hours.

<aside class="notice">It is possible that the accumulated volume and the accumulated value counted for current 24h window is smaller than the previous ones.</aside>

```shell
curl "https://api.huobi.sg/market/detail?symbol=ethbtc"
```

### HTTP Request

- GET `/market/detail`



### Request Parameters

| Parameter | Data Type | Required | Default Value | Description                                           |
| --------- | --------- | -------- | ------------- | ----------------------------------------------------- |
| symbol    | string    | true     | NA            | ltcbtc, ethbtc...（Refer to`GET /v1/common/symbols`） |

> Response:Response:

```json
"tick": {     "amount":613071.438479561,   "open":86.21,   "close":94.35,   "high":98.7,   "id":31619471534,   "count":138909,   "low":84.63,   "version":31619471534,   "vol":5.6617373443873316E7}
```

### Response Content

<aside class="notice">The returned data object is under 'tick' object instead of 'data' object in the top level JSON</aside>

| Field   | Data Type | Description                                                  |
| ------- | --------- | ------------------------------------------------------------ |
| id      | integer   | The internal identity                                        |
| amount  | float     | The aggregated trading volume in btc of last 24 hours (rotating 24h) |
| count   | integer   | The number of completed trades of last 24 hours (rotating 24h) |
| open    | float     | The opening price of last 24 hours (rotating 24h)            |
| close   | float     | The closing price of last 24 hours (rotating 24h)            |
| low     | float     | The lowest price of last 24 hours (rotating 24h)             |
| high    | float     | The highest price of last 24 hours (rotating 24h)            |
| vol     | float     | The trading volume in base currency of last 24 hours (rotating 24h) |
| version | integer   | Internal data                                                |



### HTTP Request

- GET `/market/etp`



## Error Code

Below is the error code, error message and description returned by Market data APIs.

| Error Code        | Error Message                       | Description                                      |
| ----------------- | ----------------------------------- | ------------------------------------------------ |
| invalid-parameter | invalid symbol                      | Parameter symbol is invalid                      |
| invalid-parameter | invalid period                      | Parameter period is invalid for candlestick data |
| invalid-parameter | invalid depth                       | Parameter depth is invalid for depth data        |
| invalid-parameter | invalid type                        | Parameter type is invalid                        |
| invalid-parameter | invalid size                        | Parameter size is invalid                        |
| invalid-parameter | invalid size,valid range: [1, 2000] | Parameter size range is invalid                  |
| invalid-parameter | request timeout                     | Request timeout please try again                 |

# Account

## Introduction

Account APIs provide account related (such as basic info, balance, history, point) query and transfer functionality.

<aside class="notice">All endpoints in this section require authentication</aside>

## Get all Accounts of the Current User

API Key Permission：Read<br>
Rate Limit (NEW): 100times/2s

This endpoint returns a list of accounts owned by this API user.

### HTTP Request

GET `/v1/account/accounts`



### Request Parameters

<aside class="notice">No parameter is available for this endpoint</aside>

> Response:

```json
{  "data": [    {      "id": 100001,      "type": "spot",      "subtype": "",      "state": "working"    }  ]}
```

### Response Content

| Field | Data Type | Description              | Value Range   |
| ----- | --------- | ------------------------ | ------------- |
| id    | integer   | Unique account id        |               |
| state | string    | Account state            | working, lock |
| type  | string    | The type of this account | spot          |



## Get Account Balance of a Specific Account

API Key Permission：Read<br>
Rate Limit (NEW): 100times/2s

Query account balance of a specified account. Supports the following account types:

spot：spot account

### HTTP Request

GET `/v1/account/accounts/{account-id}/balance`

### Request Parameters

| Field      | Required | Type   | Description                                                  | Default Value | Range |
| ---------- | -------- | ------ | ------------------------------------------------------------ | ------------- | ----- |
| account-id | true     | string | account-id, obtain value reference during path input  `GET /v1/account/accounts` |               |       |

> 

> Response:

```json
{  "data": {    "id": 100009,    "type": "spot",    "state": "working",    "list": [      {        "currency": "btc",        "type": "trade",        "balance": "5007.4362872650"      },      {        "currency": "btc",        "type": "frozen",        "balance": "348.1199920000"      }    ]  }}
```

### Response Content

| Field | Data Type | Description                          | Value Range   |
| ----- | --------- | ------------------------------------ | ------------- |
| id    | integer   | Unique account id                    | NA            |
| state | string    | Account state                        | working, lock |
| type  | string    | The type of this account             | spot          |
| list  | object    | The balance details of each currency |               |

**Per list item content**

| Field    | Data Type | Description                           | Value Range          |
| -------- | --------- | ------------------------------------- | -------------------- |
| currency | string    | The currency of this balance          | NA                   |
| type     | string    | The balance type                      | trade, frozen , lock |
| balance  | string    | The balance in the main currency unit | NA                   |

## Get Asset Valuation

API Key Permission：Read

Rate Limit (NEW): 100times/2s

This endpoint returns the valuation of the total assets of the account in btc or fiat currency.

### HTTP Request

- GET `/v2/account/valuation`

### Request Parameters

| Parameter         | Required | Data Type | Description                                          | Default Value | Value Range          |
| ----------------- | -------- | --------- | ---------------------------------------------------- | ------------- | -------------------- |
| accountType       | true     | string    | The type of this account                             | NA            |                      |
| valuationCurrency | false    | string    | The valuation according to the certain fiat currency | BTC           | BTC (case sensitive) |


> Responds:

```json
{    "message": null,    "success": true,    "code":200,    "data":"{        "todayProfit": null,        "updated": null,        "totalBalance": "68232.925885978428351309",        "todayProfitRate": null,        "profitAccountBalanceList": [            {                "distributionType": "1",                "success": true,                "accountBalance": "68232.925885978428351309"            },            {                "distributionType": "2",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "3",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "4",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "5",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "6",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "7",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "8",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "9",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "10",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "11",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "12",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "13",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "14",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "15",                "success": true,                "accountBalance": "0"            },            {                "distributionType": "16",                "success": false,                "accountBalance": "0"            }        ]        }"}
```

### Response Content

| todayProfit    | String               | Description                                         |
| -------------- | -------------------- | --------------------------------------------------- |
| accountList    | List<AccountBalance> | Account asset list                                  |
| {accountType   | String               | Account type                                        |
| accountBalance | String               | Account asset balance                               |
| success}       | Boolean              | Account asset retrieval status. Returns 0 if false. |
| timestamp      | long                 | Response time - unix time in millisecond            |

### Account Type Data Definition

| code | detail       |
| ---- | ------------ |
| 1    | spot account |

## Get Asset Valuation

API Key Permission：Read

Rate Limit (NEW): 100times/2s

This endpoint returns the valuation of the total assets of the account in btc or fiat currency.

### HTTP Request

- GET `/v2/account/asset-valuation`

### Request Parameters

| Parameter         | Required | Data Type | Description                                          | Default Value | Value Range              |
| ----------------- | -------- | --------- | ---------------------------------------------------- | ------------- | ------------------------ |
| accountType       | true     | string    | The type of this account                             | NA            | spot                     |
| valuationCurrency | false    | string    | The valuation according to the certain fiat currency | BTC           | USD,SGD (case sensitive) |


> The above command returns JSON structured like this:

```json
{    "code": 200,    "data": {        "balance": "34.75",        "timestamp": 1594901254363    },    "ok": true}
```

### Response Content

| Parameter | Required | Data Type | Description                                          |
| --------- | -------- | --------- | ---------------------------------------------------- |
| balance   | true     | string    | The valuation according to the certain fiat currency |
| timestamp | true     | long      | Return time                                          |

## 

## Asset Transfer

API Key Permission：Trade<br>

Other transfer features will be added in due time.<br>

### HTTP Request

- POST `/v1/account/transfer`

### Request Parameters

| Parameter    | Required | Data Type | Description                                    | Values                            |
| ------------ | -------- | --------- | ---------------------------------------------- | --------------------------------- |
| from-account | true     | long      | transfer out account ID                        |                                   |
| to-account   | true     | long      | transfer in account ID                         |                                   |
| currency     | true     | string    | token symbol，e.g. btc, ltc, bch, eth, etc ... | Refer to GET /v1/common/currencys |
| amount       | true     | string    | transfer amount                                |                                   |


> Response:

```json
{    "status": "ok",    "data": {        "transact-id": 220521190,        "transact-time": 1590662591832    }}
```

### Response Content

| Field          | Required | Data Type | Description    | Values          |
| -------------- | -------- | --------- | -------------- | --------------- |
| status         | true     | string    | Request status | "ok" or "error" |
| data           | true     | list      |                |                 |
| {transact-id   | true     | int       | Transfer id    |                 |
| transact-time} | true     | long      | Transfer time  |                 |


## Get Account History

API Key Permission：Read<br>
Rate Limit (NEW): 5times/2s

This endpoint returns the amount changes of a specified user's account.

### HTTP Request

GET `/v1/account/history`

### Request Parameters

| Parameter      | Required | Data Type | Description                                                  | Default Value        | Value Range                                                  |
| -------------- | -------- | --------- | ------------------------------------------------------------ | -------------------- | ------------------------------------------------------------ |
| account-id     | true     | string    | Account Id, refer to `GET /v1/account/accounts`              |                      |                                                              |
| currency       | false    | string    | Currency name                                                |                      | Refer to /v1/common/currencys                                |
| transact-types | false    | string    | Amount change types (multiple selection allowed, separated by comma) | all                  | trade, transact-fee, transfer, deposit，withdraw, withdraw-fee, exchange, other-types |
| start-time     | false    | long      | The start time of the query window (unix time in millisecond). Searching based on transact-time. The maximum size of the query window is 1 hour. The query window can be shifted within 30 days. | ((end-time) – 1hour) | [((end-time) – 1hour), (end-time)]                           |
| end-time       | false    | long      | The end time of the query window (unix time in millisecond). Searching based on transact-time. The maximum size of the query window is 1 hour. The query window can be shifted within 30 days. | current-time         | [(current-time) – 29days,(current-time)]                     |
| sort           | false    | string    | Sorting order                                                | asc                  | asc or desc                                                  |
| size           | false    | int       | Maximum number of items in each response                     | 100                  | [1,500]                                                      |
| from-id        | false    | long      | First record ID in this query (only valid for next page querying, see Note 2) |                      |                                                              |

> Response:

```json
{    "status": "ok",    "data": [        {            "account-id": 5260185,            "currency": "btc",            "transact-amt": "0.002393000000000000",            "transact-type": "transfer",            "record-id": 89373333576,            "avail-balance": "0.002393000000000000",            "acct-balance": "0.002393000000000000",            "transact-time": 1571393524526        },        {            "account-id": 5260185,            "currency": "btc",            "transact-amt": "-0.002393000000000000",            "transact-type": "transfer",            "record-id": 89373382631,            "avail-balance": "0E-18",            "acct-balance": "0E-18",            "transact-time": 1571393578496        }    ]}
```

### Response Content

| Field         | Data Type | Description                                                  | Value Range  |
| ------------- | --------- | ------------------------------------------------------------ | ------------ |
| status        | string    | Status code                                                  | "ok","error" |
| data          | object    |                                                              |              |
| { account-id  | long      | Account ID                                                   |              |
| currency      | string    | Currency                                                     |              |
| transact-amt  | string    | Amount change (positive value if income, negative value if outcome) |              |
| transact-type | string    | Amount change types                                          |              |
| avail-balance | string    | Available balance                                            |              |
| acct-balance  | string    | Account balance                                              |              |
| transact-time | long      | Transaction time (database time)                             |              |
| record-id }   | long      | Unique record ID in the database                             |              |
| next-id       | long      | First record ID in next page (only valid if exceeded page size, see Note 2) |              |

Note 1:<br>

- If ‘transact-type’ is shown as ‘rebate’, it implicates a paid maker rebate.<br>
- A paid maker rebate could possibly include rebate from multiple trades.<br>

Note 2:<br>
Only when the number of items within the query window (between “start-time” and ”end-time”) exceeded the page limitation (defined by “size”), New Huo server returns “next-id”. Once received “next-id”, API user should –<br>

1) Be aware of that, some items within the query window were not returned due to the page size limitation.<br>
2) In order to get these items from New Huo server, adopt the “next-id” as “from-id” and submit another request, with other request parameters no change.<br>
3) As database record ID, “next-id” and “from-id” are for recurring query purpose and the ID itself does not have any business implication.<br>

Note 3:<br>

Change type contains a detailed list of account types：

| trade                | match-income                  | Matched Trade In                  |
| -------------------- | ----------------------------- | --------------------------------- |
| trade                | match-income                  | Matched Trade In                  |
| transfer             | spot-generic-transfer-in      | Spot Account General Transfer In  |
| transfer{ account-id | spot-generic-transfer-outlong | Spot Account General Transfer Out |
| deposit              | user-account-deposit          | User Account Deposit Transfer     |
| withdraw             | user-account-withdraw         | User Account Withdrawal Transfer  |

## 

## Get Account Ledger

API Key Permission：Read

This endpoint returns the amount changes of specified user's account.<br>

Phase 1 release only supports historical assets transfer querying (“transactType” = “transfer”).<br>

The maximum query window size set by “startTime” & “endTime” is 10-day, which mean a maximum of 10-day records are queriable per request.
The query window can be within the last 180 days, which means, by adjusting “startTime” & “endTime” accordingly, the records in last 180 days are queriable.<br>

### HTTP Request

GET `/v2/account/ledger`



### Request Parameters

| Field Name    | Data Type | Mandatory | Description                                                  |
| ------------- | --------- | --------- | ------------------------------------------------------------ |
| accountId     | string    | TRUE      | Account ID                                                   |
| currency      | string    | FALSE     | Cryptocurrency (default value: all)                          |
| transactTypes | string    | FALSE     | Transaction types (multiple inputs are allowed; default value: all; enumerated values: transfer) |
| startTime     | long      | FALSE     | Farthest time (please refer to note 1 for valid range and default value) |
| endTime       | long      | FALSE     | Nearest time (please refer to note 2 for valid range and default value) |
| sort          | string    | FALSE     | Sorting order (enumerated values: asc, desc)                 |
| limit         | int       | FALSE     | Maximum number of items in one page (valid range:[1,500]; default value:100) |
| fromId        | long      | FALSE     | First record ID in this query (only valid for next page querying. please refer to note 3) |

Note 1:<br>
startTime valid range: [(endTime – 10days), endTime], unix time in millisecond<br>
startTime default value: (endTime – 10days)

Note 2:<br>
endTime valid range: [(current time – 180days), current time], unix time in millisecond<br>
endTime default value: current time

> Response:

```json
{"code": 200,"message": "success","data": [    {        "accountId": 5260185,        "currency": "btc",        "transactAmt": 1.000000000000000000,        "transactType": "transfer",        "transferType": "margin-transfer-out",        "transactId": 0,        "transactTime": 1585573286913,        "transferer": 5463409,        "transferee": 5260185    },    {        "accountId": 5260185,        "currency": "btc",        "transactAmt": -1.000000000000000000,        "transactType": "transfer",        "transferType": "margin-transfer-in",        "transactId": 0,        "transactTime": 1585573281160,        "transferer": 5260185,        "transferee": 5463409    }]}
```

### Response Content

| Field Name   | Data Type | Mandatory | Description                                                  | Value Rage |
| ------------ | --------- | --------- | ------------------------------------------------------------ | ---------- |
| code         | integer   | TRUE      | Status code                                                  |            |
| message      | string    | FALSE     | Error message (if any)                                       |            |
| data         | object    | TRUE      | Sorting as user defined (in request parameter “sort”	)    |            |
| { accountId  | integer   | TRUE      | Account ID                                                   |            |
| currency     | string    | TRUE      | Cryptocurrency                                               |            |
| transactAmt  | number    | TRUE      | Transaction amount (income positive, expenditure negative)   |            |
| transactType | string    | TRUE      | Transaction type                                             | transfer   |
| transferType | string    | FALSE     | Transfer type	(only valid for transactType=transfer)      |            |
| transactId   | integer   | TRUE      | Transaction ID                                               |            |
| transactTime | integer   | TRUE      | Transaction time                                             |            |
| transferer   | integer   | FALSE     | Transferer’s account ID                                      |            |
| transferee } | integer   | FALSE     | Transferee’s account ID                                      |            |
| nextId       | integer   | FALSE     | First record ID in next page (only valid if exceeded page size. please refer to note 3.) |            |

Note 3:<br>
Only when the number of items within the query window (between “startTime” and ”endTime”) exceeded the page limitation (defined by “limit”), New Huo server returns “nextId”. Once received “nextId”, API user should –<br>

1)	Be aware of that, some items within the query window were not returned due to the page size limitation.<br>
2)	In order to get these items from New Huo server, adopt the “nextId” as “fromId” and submit another request, with other request parameters no change.<br>
3)	As database record ID, “nextId” and “fromId” are for recurring query purpose and the ID itself does not have any business implication.<br>



# Wallet (Deposit and Withdraw)

## Introduction

Wallet APIs provide query functionality for deposit address, withdraw address, withdraw quota, deposit and withdraw history, and also provide withdraw and cancel-withdraw functionality.

<aside class="notice">All endpoints in this section require authentication</aside>

## Query Deposit Address

Parent user could query deposit address of corresponding chain, for a specific crypto currency (except IOTA).

API Key Permission：Read<br>
Rate Limit (NEW): 20times/2s



### HTTP Request

GET `/v1/query/deposit-withdraw`

### Request Parameters

| Parameter | Required | Type   | Description                  | Default Vault                                                | Value Range                                                  |
| --------- | -------- | ------ | ---------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| currency  | false    | string | Token Symbol                 |                                                              | btc, ltc, bch, eth, etc ...(Refer to GET /v1/common/currencys`) |
| type      | true     | string | Deposit or Withdrawal        |                                                              | Deposit or Withdraw, child account can only use deposit      |
| from      | false    | string | Query start ID               | By default, the default value is direct. When direct is ‘prev’, from is 1, and returns from old to new in ascending order; when direct is ‘next’, from is the ID of the latest record, and returns from new to old in descending order |                                                              |
| size      | false    | string | Query record size            | 100                                                          | 1-500                                                        |
| direct    | false    | string | Return record sort direction | By default, the default is "prev" (ascending order)          | "Prev" (ascending order) or "next" (descending order)        |



> Response:

```json
{  "data":    [      {        "id": 1171,        "type": "deposit",        "currency": "xrp",        "tx-hash": "ed03094b84eafbe4bc16e7ef766ee959885ee5bcb265872baaa9c64e1cf86c2b",        "amount": 7.457467,        "address": "rae93V8d2mdoUQHwBDBdM4NHCMehRJAsbm",        "address-tag": "100040",        "fee": 0,        "state": "safe",        "created-at": 1510912472199,        "updated-at": 1511145876575      },      ...    ]}
```



### Response Content

| Parameter   | Required | Data Type | Description                                                  | Value Range                                               |
| ----------- | -------- | --------- | ------------------------------------------------------------ | --------------------------------------------------------- |
| id          | true     | long      | Deposit or withdrawal order ID, the from parameter is taken from this value when performing page query |                                                           |
| type        | true     | string    | data Type                                                    | 'deposit', 'withdraw', child account can only use deposit |
| currency    | true     | string    | token symbol                                                 |                                                           |
| tx-hash     | true     | string    | transaction hash                                             |                                                           |
| chain       | true     | string    | blockchain name                                              |                                                           |
| amount      | true     | float     | quantity                                                     |                                                           |
| address     | true     | string    | destination address                                          |                                                           |
| address-tag | true     | string    | address tag                                                  |                                                           |
| fee         | true     | float     | fee                                                          |                                                           |
| state       | true     | string    | state                                                        | refer to table below for applicable states                |
| error-code  | false    | string    | Error code for withdrawal failure, only when the type is "withdraw" and the state is "reject", "wallet-reject" and "failed". |                                                           |
| error-msg   | false    | string    | Error message for withdrawal failure, only when the type is "withdraw" and the state is "reject", "wallet-reject" and "failed". |                                                           |
| created-at  | true     | long      | initiation start time                                        |                                                           |
| updated-at  | true     | long      | last update time                                             |                                                           |



**List of possible deposit state**

| State      | Description                                                  |
| ---------- | ------------------------------------------------------------ |
| unknown    | On-chain transfer has not been received                      |
| confirming | On-chain transfer waits for first confirmation               |
| confirmed  | On-chain transfer confirmed for at least one block, user is able to transfer and trade |
| safe       | Multiple on-chain confirmed, user is able to withdraw        |
| orphan     | On-chain transfer confirmed but currently in an orphan branch |

**List of possible withdraw state**

| State           | Description                                       |
| --------------- | ------------------------------------------------- |
| verifying       | Awaiting verification                             |
| failed          | verification failed                               |
| submitted       | Withdraw request submitted successfully           |
| reexamine       | Under examination for withdraw validation         |
| canceled        | Withdraw canceled by user                         |
| pass            | Withdraw validation passed                        |
| reject          | Withdraw validation rejected                      |
| pre-transfer    | Withdraw is about to be released                  |
| wallet-transfer | On-chain transfer initiated                       |
| wallet-reject   | Transfer rejected by chain                        |
| confirmed       | On-chain transfer completed with one confirmation |
| confirm-error   | On-chain transfer faied to get confirmation       |
| repealed        | Withdraw terminated by system                     |

## Error Code

Below is the response code, message and description returned by Wallet APIs.

| Response Code | Message                              | Description            |
| ------------- | ------------------------------------ | ---------------------- |
| 200           | success                              | Successful             |
| 500           | error                                | Server internal error  |
| 1002          | unauthorized                         | User is unautherized   |
| 1003          | invalid signature                    | API signature is wrong |
| 2002          | invalid field value in "field name"  | Parameter is invalid   |
| 2003          | missing mandatory field "field name" | Parameter is missing   |





# Trading

## Introduction

Trading APIs provide trading related functionality, including placing order, canceling order, order history query, trading history query, transaction fee query.

<aside class="notice">All endpoints in this section require authentication</aside>
<aside class="warning">The parameter "account-id" and "source" should be set properly, refer to details in Request Parameters description below.</aside>

Below is the glossary of trading related field:

**order type**: The order type is consist of trade direction and behavior type: [direction]-[type]

direction:

- buy
- sell

type:

- market : The price is not required in order creation request, you only need to specify either volume or amount. The matching and trade will happen automatically according to the request.

- limit: Both of the price and amount should be specified in order creation request.

  

**order source**: the origin of the order

- spot-api: API order from spot account

  

**order state**:

- created: The order is created, and not in the matching queue yet.
- submitted: The order is submitted, and already in the matching queue, waiting for deal.
- partial-filled: The order is already in the matching queue and partially traded, and is waiting for further matching and trade.
- filled: The order is already traded and not in the matching queue any more.
- partial-canceled: The order is not in the matching queue any more. The status is transferred from 'partial-filled', the order is partially trade, but remaining is canceled.
- canceling: The order is under canceling, but haven't been removed from matching queue yet.
- canceled: The order is not in the matching queue any more, and completely canceled. There is no trade associated with this order.

**IDs**: The frequently used identities are listed below:

- order-id: The unique identity for order.
- client-order-id: The identity defined by the client. This id is included in order creation request, and will be returned as order-id. For completed orders, clientOrderId will be valid for 2 hours since the order creation (it is still valid for 8 hours concerning other orders). That is to say, if an order has been created for more than 2 hours, clientOrderId can’t be used to query the completed order (It is recommended to check it with orderid). Among them, the status of the completed order includes partially canceled, canceled, and fully executed. The allowed characters are letters (case sensitive), digit, underscore (_) and hyphen (-), no more than 64 chars.
- match-id : The identity for order matching.
- trade-id : The unique identity for the trade.

## Place a New Order

API Key Permission：Trade<br>
Rate Limit (NEW): 100times/2s

This endpoint places a new order and sends to the exchange to be matched.

### HTTP Request

POST ` /v1/order/orders/place`

Request:

```shell
{  "account-id": "100009",  "amount": "10.1",  "price": "100.1",  "source": "api",  "symbol": "ethbtc",  "type": "buy-limit",  "client-order-id": "a0001"}
```

### Request Parameters

| Parameter       | Data Type | Required | Default  | Description                                                  | Value Range                                        |
| --------------- | --------- | -------- | -------- | ------------------------------------------------------------ | -------------------------------------------------- |
| account-id      | string    | true     | NA       | The account id used for this trade                           | Refer to `GET /v1/account/accounts`                |
| symbol          | string    | true     | NA       | The trading symbol to trade                                  | ltcbtc, ethbtc...Refer to `GET /v1/common/symbols` |
| type            | string    | true     | NA       | The order type                                               | buy-market, sell-market, buy-limit, sell-limit     |
| amount          | string    | true     | NA       | order size (for buy market order, it's order value)          | NA                                                 |
| price           | string    | false    | NA       | The order price (not available for market order)             | NA                                                 |
| source          | string    | false    | spot-api | When trade with spot use 'spot-api'                          |                                                    |
| client-order-id | string    | false    | NA       | Client order ID (maximum 64-character length, to be unique within 8 hours) |                                                    |



**buy-limit-maker**

If the order price is greater than or equal to the lowest selling price in the market, the order will be rejected.

If the order price is less than the lowest selling price in the market, the order will be accepted.

**sell-limit-maker**

If the order price is less than or equal to the highest buy price in the market, the order will be rejected.

If the order price is greater than the highest buy price in the market, the order will be accepted.

> Response:

```json
{    "data": "59378"}
```

### Response Content

<aside class="notice">The returned data object is a single string which represents the order id</aside>

If client order ID duplicates with a previous order (within 8 hours), the endpoint reverts error message `invalid.client.order.id`.


## Place a Batch of Orders

API Key Permission：Trade<br>
Rate Limit (NEW): 50times/2s

A batch contains at most 10 orders.

### HTTP Request

- POST ` /v1/order/batch-orders`

```json
[	{    "account-id": "123456",    "price": "7801",    "amount": "0.001",    "symbol": "ethbtc",    "type": "sell-limit",    "client-order-id": "c1"	},	{    "account-id": "123456",    "price": "7802",    "amount": "0.001",    "symbol": "ethbtc",    "type": "sell-limit",    "client-order-id": "d2"	}]
```

### Request Parameters

| Parameter       | Data Type | Required | Default  | Description                                                  |
| --------------- | --------- | -------- | -------- | ------------------------------------------------------------ |
| [{ account-id   | string    | true     | NA       | The account id, refer to `GET /v1/account/accounts`. Use 'spot' `account-id` for spot trading |
| symbol          | string    | true     | NA       | The trading symbol, i.e. ltcbtc, ethbtc...(Refer to `GET /v1/common/symbols`) |
| type            | string    | true     | NA       | The type of order, including “buy-market, sell-market, buy-limit, sell-limit” |
| amount          | string    | true     | NA       | The order size (for buy market order, it's order value)      |
| price           | string    | false    | NA       | The order price (not available for market order)             |
| source          | string    | false    | spot-api | When trade with spot use 'spot-api'                          |
| client-order-id | string    | false    | NA       | Client order ID (maximum 64-character length)                |

**buy-limit-maker**

If the order price is greater than or equal to the lowest selling price in the market, the order will be rejected.

If the order price is less than the lowest selling price in the market, the order will be accepted.

**sell-limit-maker**

If the order price is less than or equal to the highest buy price in the market, the order will be rejected.

If the order price is greater than the highest buy price in the market, the order will be accepted.

> Response:

```json
{    "status": "ok",    "data": [        {            "order-id": 61713400772,            "client-order-id": "c1"        },        {            "order-id": 61713400940,            "client-order-id": "d2"        }    ]}
```

### Response Content

| Field           | Data Type | Description                                 |
| --------------- | --------- | ------------------------------------------- |
| [{order-id      | integer   | The order id                                |
| client-order-id | string    | The client order id (if available)          |
| err-code        | string    | The error code (only for rejected order)    |
| err-msg}]       | string    | The error message (only for rejected order) |

If client order ID duplicates with a previous order , the endpoint responds that previous order's Id and client order ID.

## Submit Cancel for an Order

API Key Permission：Trade<br>
Rate Limit (NEW): 100times/2s

This endpoint submits a request to cancel an order.

<aside class="warning">The actual result of the cancellation request needs to be checked by order status or match result endpoints after submitting the request.</aside>

### HTTP Request

POST ` /v1/order/orders/{order-id}/submitcancel`

### Request Parameters

| Parameter | Data Type | Required | Default | Description                                   |
| --------- | --------- | -------- | ------- | --------------------------------------------- |
| order-id  | string    | true     | NA      | order id which needs to be filled in the path |
| symbol    | string    | false    | NA      | symbol which needs to be filled in the URL    |

> Success response:

```json
  "data": "59378"
```

### Response Content

<aside class="notice">The returned data object is a single string which represents the order id</aside>

### Error Code

> Failure response:

```json
{  "status": "error",  "err-code": "order-orderstate-error",  "err-msg": "Incorrect order state",  "order-state":-1 // current order state}
```

The possible values of "order-state" includes -

| order-state | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| -1          | order was already closed in the long past (order state = cancelled, partially-cancelled, filled, partially-filled) |
| 1           | created                                                      |
| 3           | submitted                                                    |
| 4           | partial-filled                                               |
| 5           | partially-cancelled                                          |
| 6           | filled                                                       |
| 7           | cancelled                                                    |
| 10          | cancelling                                                   |

## Submit Cancel for an Order (based on client order ID)

API Key Permission：Trade<br>
Rate Limit (NEW): 100times/2s

This endpoint submit a request to cancel an order based on client-order-id .

<aside class="notice">It is suggested to use /v1/order/orders/{order-id}/submitcancel to cancel a single order, which is faster and more stable</aside>
<aside class="warning">This only submits the cancel request, the actual result of the canel request needs to be checked by order status or match result endpoints</aside>

### HTTP Request

- POST ` /v1/order/orders/submitCancelClientOrder`

> Request:

```json
{  "client-order-id": "a0001"}
```

### 

### Request Parameters

| Parameter       | Data Type | Required | Default | Description                                                  |
| --------------- | --------- | -------- | ------- | ------------------------------------------------------------ |
| client-order-id | string    | true     | NA      | Client order ID, it must exist within 8 hours, otherwise it is not allowed to use when placing a new order |

> Response:

```json
 {    "data": "10"}
```

### Response Content

| Field | Data Type | Description              |
| ----- | --------- | ------------------------ |
| data  | integer   | Cancellation status code |

| Status Code | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| -1          | order was already closed in the long past (order state = cancelled, partially-cancelled, filled, partially-filled) |
| 0           | client-order-id not found                                    |
| 1           | created                                                      |
| 3           | submitted                                                    |
| 4           | partial-filled                                               |
| 5           | partially-cancelled                                          |
| 6           | filled                                                       |
| 7           | cancelled                                                    |
| 10          | cancelling                                                   |

## Automated Cancel Order

API Key Permission：Trade<br>

In order to protect API users from unexpected losses resulting from lost network connection due to system failure on the part of the client or the New Huo Singapore system, New Huo Singapore has added an automatic order withdrawal interface. When users accidentally disconnect from New Huo Singapore, the system automatically cancels all orders for users to avoid loss, that is, provide Dead man's switch function. When enabled, if the interface is not called again before the set time expires, all the user's spot orders will be cancelled (maximum support for cancellation of 500 orders).

### HTTP Request

- POST `/v2/algo-orders/cancel-all-after`

> Request:

```json
{  "timeout": "10"}
```

### Request Parameter

| Parameter | Mandatory | Type | Description                                                  | Default Value | Value Range                        |
| --------- | --------- | ---- | ------------------------------------------------------------ | ------------- | ---------------------------------- |
| timeout   | true      | int  | timeout value (in seconds), refer to notes for proposed setup | NA            | 0 or greater or equal to 5 seconds |


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

### Response Content

| Parameter     | **Mandatory** | **Data Type** | **Description**            |
| ------------- | ------------- | ------------- | -------------------------- |
| code          | true          | int           | Status code                |
| message       | false         | string        | Error description (if any) |
| data          | true          | object        |                            |
| { currentTime | true          | long          | Current time               |
| triggerTime } | true          | long          | Trigger time               |




## ## 


## Get All Open Orders

API Key Permission：Read<br>
Rate Limit (NEW): 50times/2s

This endpoint returns all open orders which have not been filled completely.

### HTTP Request

- GET `/v1/order/openOrders`

> Request:

```json
{   "account-id": "100009",   "symbol": "ethbtc",   "side": "buy"}
```

### 

### Request Parameters

| Parameter  | Data Type | Required                                                     | Default | Description                                | Value Range                                                  |
| ---------- | --------- | ------------------------------------------------------------ | ------- | ------------------------------------------ | ------------------------------------------------------------ |
| account-id | string    | true                                                         | NA      | The account id used for this trade         | Refer to `GET /v1/account/accounts`                          |
| symbol     | string    | true                                                         | NA      | The trading symbol to trade                | ltcbtc, ethbtc...Refer to `GET /v1/common/symbols`           |
| side       | string    | false                                                        | NA      | Filter on the direction of the trade       | buy, sell                                                    |
| from       | string    | false                                                        | NA      | start order ID the searching to begin with |                                                              |
| direct     | string    | false (if field "from" is defined, this field "direct" becomes mandatory) | NA      | searching direction                        | prev - in ascending order from the start order ID; next - in descending order from the start order ID |
| size       | int       | false                                                        | 100     | The number of orders to return             | [1, 500]                                                     |

> Response:

```json
{    "data": [    {      "id": 5454937,      "symbol": "ethbtc",      "account-id": 30925,      "amount": "1.000000000000000000",      "price": "0.453000000000000000",      "created-at": 1530604762277,      "type": "sell-limit",      "filled-amount": "0.0",      "filled-cash-amount": "0.0",      "filled-fees": "0.0",      "source": "web",      "state": "submitted"    }  ]}
```

### Response Content

| Field              | Data Type | Description                                                  |
| ------------------ | --------- | ------------------------------------------------------------ |
| id                 | integer   | Order id                                                     |
| client-order-id    | string    | Client order id, can be returned from all open orders (if specified). |
| symbol             | string    | The trading symbol to trade, e.g. ltcbtc, ethbtc             |
| price              | string    | The limit price of limit order                               |
| created-at         | int       | The timestamp in milliseconds when the order was created     |
| type               | string    | All possible order type (refer to introduction in this section) |
| filled-amount      | string    | The amount which has been filled                             |
| filled-cash-amount | string    | The filled total in quote currency                           |
| filled-fees        | string    | Transaction fee (Accurate fees refer to matchresults endpoint) |
| source             | string    | The source where the order was triggered, possible values: sys, web, api, app |
| state              | string    | Order status, valid values: created, submitted, partial-filled |

## Submit Cancel for Multiple Orders by Criteria

API Key Permission：Trade<br>
Rate Limit (NEW): 50times/2s

This endpoint submit cancellation for multiple orders (not exceeding 100 orders per request) at once with given criteria.

This endpoint only submit the cancellation request, the actual cancellation result will need to be confirmed by other endpoints 
like order status, matchresult, etc.

### HTTP Request

POST ` /v1/order/orders/batchCancelOpenOrders`

| Parameter  | Data Type | Required | Default | Description                                                  | Value Range                                                  |
| ---------- | --------- | -------- | ------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| account-id | string    | false    | NA      | The account id used for this cancel                          | Refer to `GET /v1/account/accounts`                          |
| symbol     | string    | false    | all     | The trading symbol list (maximum 10 symbols, separated by comma, default value all symbols) | All supported trading symbol, e.g. ltcbtc, ethbtc...Refer to `GET /v1/common/symbols` |
| types      | string    | false    | NA      | One or more types of order to include in the search, use comma to separate. |                                                              |
| side       | string    | false    | NA      | Filter on the direction of the trade                         | buy, sell                                                    |
| size       | int       | false    | 100     | The number of orders to cancel                               | [1, 100]                                                     |

> Response:

```json
  {  "status": "ok",  "data": {    "success-count": 2,    "failed-count": 0,    "next-id": 5454600  }}
```

### Response Content

| Field         | Required | Data Type | Description                                                  |
| ------------- | -------- | --------- | ------------------------------------------------------------ |
| success-count | true     | int       | The number of cancel request sent successfully               |
| failed-count  | true     | int       | The number of cancel request failed                          |
| next-id       | true     | long      | the next order id that can be cancelled, -1 indicates no open orders |

## Submit Cancel for Multiple Orders by IDs

API Key Permission：Trade<br>
Rate Limit (NEW): 50times/2s

This endpoint submit cancellation for multiple orders at once with given ids. It is suggested to use order-ids instead of 
client-order-ids, so that the cancellation is faster, more accurate and more stable. 

### HTTP Request

- POST ` /v1/order/orders/batchcancel`

> Request:

```json
{  "client-order-ids": [   "5983466", "5722939", "5721027", "5719487"  ]}
```

### 

### Request Parameters

| Parameter        | Data Type | Required | Description                                                  | Value Range                        |
| ---------------- | --------- | -------- | ------------------------------------------------------------ | ---------------------------------- |
| order-ids        | string[]  | false    | The order ids to cancel (Either order-ids or client-order-ids can be filled in one batch request). It is suggest to use order-ids rather than client-order-ids, the former is faster and more stable | No more than 50 orders per request |
| client-order-ids | string[]  | false    | The client order ids to cancel (Either order-ids or client-order-ids can be filled in one batch request), it must exist already, otherwise it is not allowed to use when placing a new order | No more than 50 orders per request |

> Response:

```json
{    "status": "ok",    "data": {        "success": [            "5983466"                    ],        "failed": [            {              "err-msg": "Incorrect order state",              "order-state": 7,              "order-id": "",              "err-code": "order-orderstate-error",              "client-order-id": "first"            },            {              "err-msg": "Incorrect order state",              "order-state": 7,              "order-id": "",              "err-code": "order-orderstate-error",              "client-order-id": "second"            },            {              "err-msg": "The record is not found.",              "order-id": "",              "err-code": "base-not-found",              "client-order-id": "third"            }          ]    }}
```

### Response Content

| Field    | Data Type | Description                                                  |
| -------- | --------- | ------------------------------------------------------------ |
| {success | string[]  | Cancelled order list (Can be order ID list or client order list, based on the request) |
| failed}  | string[]  | Failed order list (Can be order ID list or client order list, based on the request) |

The failed id list has below fields

| Fields          | Data Type | Description                                                  |
| --------------- | --------- | ------------------------------------------------------------ |
| [{ order-id     | string    | The order id (if the request is based on order-ids)          |
| client-order-id | string    | The client order id (if the request is based on client-order-ids) |
| err-code        | string    | The error code (only applicable for rejected order)          |
| err-msg         | string    | The error message (only applicable for rejected order)       |
| order-state }]  | string    | Current order state (if available)                           |

The possible values of "order-state" includes -

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






## Get the Order Detail of an Order

API Key Permission：Read<br>
Rate Limit (NEW): 50times/2s

This endpoint returns the detail of a specific order. If an order is created via API, then it's no longer queryable after being cancelled for 2 hours.

### HTTP Request

`GET /v1/order/orders/{order-id}`

### Request Parameters

| **Name** | **Mandatory** | **Type** | **Description**                                       | 默认值 | 取值范围 |
| -------- | ------------- | -------- | ----------------------------------------------------- | ------ | -------- |
| order-id | true          | string   | order id when order was created. Place it within path |        |          |

> Response:

```json
{    "data":   {    "id": 59378,    "symbol": "ethbtc",    "account-id": 100009,    "amount": "10.1000000000",    "price": "100.1000000000",    "created-at": 1494901162595,    "type": "buy-limit",    "field-amount": "10.1000000000",    "field-cash-amount": "1011.0100000000",    "field-fees": "0.0202000000",    "finished-at": 1494901400468,    "user-id": 1000,    "source": "api",    "state": "filled",    "canceled-at": 0  }}
```

### 

### Response Content

| Field              | Data Type | Description                                                  |
| ------------------ | --------- | ------------------------------------------------------------ |
| id                 | integer   | order id                                                     |
| client-order-id    | string    | Client order id ("client-order-id" (if specified) can be returned from all open orders.	"client-order-id"  (if specified) can be returned only from closed orders (state <> canceled) created within 7 days.	"client-order-id"  (if specified) can be returned only from closed orders (state = canceled) created within 8 hours.) |
| symbol             | string    | The trading symbol to trade, e.g. ltcbtc, ethbtc             |
| account-id         | string    | The account id which this order belongs to                   |
| amount             | string    | The amount of base currency in this order                    |
| price              | string    | The limit price of limit order                               |
| created-at         | int       | The timestamp in milliseconds when the order was created     |
| finished-at        | int       | The timestamp in milliseconds when the order was changed to a final state. This is not the time the order is matched. |
| canceled-at        | int       | The timestamp in milliseconds when the order was canceled, if not canceled then has value of 0 |
| type               | string    | All possible order type (refer to introduction in this section) |
| filled-amount      | string    | The amount which has been filled                             |
| filled-cash-amount | string    | The filled total in quote currency                           |
| filled-fees        | string    | Transaction fee (Accurate fees refer to matchresults endpoint) |
| source             | string    | All possible order source (refer to introduction in this section) |
| state              | string    | All possible order state (refer to introduction in this section) |






## Get the Order Detail of an Order (based on client order ID)

API Key Permission：Read<br>
Rate Limit (NEW):50times/2s

This endpoint returns the detail of one order by specified client order id (within 8 hours). The order created via API will no longer be queryable after being cancelled for more than 2 hours. It is suggested to cancel orders via `GET /v1/order/orders/{order-id}`, which is faster and more stable.

### HTTP Request

`GET /v1/order/orders/getClientOrder`



### Request Parameters

| Parameter | Data Type | Required | Default | Description     |
| --------- | --------- | -------- | ------- | --------------- |
| order-id  | string    | true     | NA      | Client order ID |

> Response:

```json
{    "data": {    "id": 59378,    "symbol": "ethbtc",    "account-id": 100009,    "amount": "10.1000000000",    "price": "100.1000000000",    "created-at": 1494901162595,    "type": "buy-limit",    "field-amount": "10.1000000000",    "field-cash-amount": "1011.0100000000",    "field-fees": "0.0202000000",    "finished-at": 1494901400468,    "user-id": 1000,    "source": "api",    "state": "filled",    "canceled-at": 0  }}
```

### Response Content

| client-order-id    | string | Client order id (only those orders created within 8 hours can be returned.) |
| ------------------ | ------ | ------------------------------------------------------------ |
| symbol             | string | The trading symbol to trade, e.g. ltcbtc, ethbtc             |
| account-id         | string | The account id which this order belongs to                   |
| amount             | string | The amount of base currency in this order                    |
| price              | string | The limit price of limit order                               |
| created-at         | int    | The timestamp in milliseconds when the order was created     |
| finished-at        | int    | The timestamp in milliseconds when the order was changed to a final state. This is not the time the order is matched. |
| canceled-at        | int    | The timestamp in milliseconds when the order was canceled, if not canceled then has value of 0 |
| type               | string | All possible order type (refer to introduction in this section) |
| filled-amount      | string | The amount which has been filled                             |
| filled-cash-amount | string | The filled total in quote currency                           |
| filled-fees        | string | Transaction fee (Accurate fees refer to matchresults endpoint) |
| source             | string | All possible order source (refer to introduction in this section) |
| state              | string | All possible order state (refer to introduction in this section) |
| stop-price         | string | trigger price of stop limit order                            |
| operator           | string | operation character of stop price                            |



If the client order ID is not found, following error message will be returned:
{
    "status": "error",
    "err-code": "base-record-invalid",
    "err-msg": "record invalid",
    "data": null
}



## Get the Match Result of an Order

API Key Permission：Read<br>
Rate Limit (NEW): 50times/2s

This endpoint returns the match result of an order.

### HTTP Request

`GET /v1/order/orders/{order-id}/matchresults`



### Request Parameters

| Parameter | Data Type | Required | Default | Description                  |
| --------- | --------- | -------- | ------- | ---------------------------- |
| order-id  | string    | true     | NA      | Order ID, place it into path |


> The above command returns JSON structured like this:

```json
 {    "data": [    {      "id": 29553,      "order-id": 59378,      "match-id": 59335,      "trade-id": 100282808529,      "symbol": "ethbtc",      "type": "buy-limit",      "source": "api",      "price": "100.1000000000",      "filled-amount": "9.1155000000",      "filled-fees": "0.0182310000",      "created-at": 1494901400435,      "role": "maker",      "filled-points": "0.0",      “fee-deduct-state”:"done",      "fee-deduct-currency": ""    }    ...  ]}
```

### Response Content

<aside class="notice">The return data contains a list and each item in the list represents a match result</aside>

| Parameter     | Data Type | Description                                                  |
| ------------- | --------- | ------------------------------------------------------------ |
| id            | long      | Internal id                                                  |
| symbol        | string    | The trading symbol to trade, e.g. ltcbtc, ethbtc ...         |
| order-id      | long      | The order id of this order                                   |
| match-id      | long      | The match id of this match                                   |
| trade-id      | integer   | Unique trade ID (NEW)                                        |
| price         | string    | The limit price of limit order                               |
| created-at    | int       | The timestamp in milliseconds when this record is created (slightly later than trade time) |
| type          | string    | All possible order type (refer to introduction in this section) |
| filled-amount | string    | The amount which has been filled                             |
| filled-fees   | string    | Transaction fee (positive value). If maker rebate applicable, revert maker rebate value per trade (negative value). |
| fee-currency  | string    | Currency of transaction fee or transaction fee rebate (transaction fee of buy order is based on base currency, transaction fee of sell order is based on quote currency; transaction fee rebate of buy order is based on quote currency, transaction fee rebate of sell order is based on base currency) |
| source        | string    | All possible order source (refer to introduction in this section) |
| role          | string    | the role in the transaction: taker or maker                  |
| status        | string    | state                                                        |
| <data>        | object    |                                                              |



Notes:<br>

- The calculated maker rebate value inside ‘filled-fees’ would not be paid immediately.<br>


## Search Past Orders

API Key Permission：Read<br>
Rate Limit (NEW): 50times/2s

This endpoint returns orders based on a specific searching criteria. The order created via API will no longer be queryable after being cancelled for more than 2 hours.


- Upon user defined “start-time” AND/OR “end-time”, New Huo server will return historical orders whose order creation time falling into the period. The maximum query window between “start-time” and “end-time” is 48-hour. Oldest order searchable should be within recent 180 days. If either “start-time” or “end-time” is defined, New Huo server will ignore “start-date” and “end-date” regardless they were filled or not.

- If user does neither define “start-time” nor “end-time”, but “start-date”/”end-date”, the order searching will be based on defined “date range”, as usual. The maximum query window is 2 days, and oldest order searchable should be within recent 180 days.

- If user does not define any of “start-time”/”end-time”/”start-date”/”end-date”, by default New Huo server will treat current time as “end-time”, and then return historical orders within recent 48 hours.

New Huo Singapore suggests API users to search historical orders based on “time” filter instead of “date”. In the near future, New Huo Singapore would remove “start-date”/”end-date” fields from the endpoint, through another notification.


### HTTP Request

`GET /v1/order/orders`

> Request

```json
{   "account-id": "100009",   "amount": "10.1",   "price": "100.1",   "source": "api",   "symbol": "ethbtc",   "type": "buy-limit"}
```


### Request Parameters

| Parameter  | Data Type | Required | Default | Description                                                  | Value Range                                                  |
| ---------- | --------- | -------- | ------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| symbol     | string    | true     | NA      | The trading symbol                                           | All supported trading symbols, e.g. ltcbtc, ethbtc ...       |
| types      | string    | false    | NA      | One or more types of order to include in the search, use comma to separate. | buy-market, sell-market, buy-limit, sell-limit, buy-ioc, sell-ioc, buy-stop-limit, sell-stop-limit, buy-limit-fok, sell-limit-fok, buy-stop-limit-fok, sell-stop-limit-fok |
| start-time | long      | false    | -48h    | Search starts time, UTC time in millisecond                  | Value range [((end-time) – 48h), (end-time)], maximum query window size is 48 hours, query window shift should be within past 180 days, query window shift should be within past 2 hours for cancelled order (state = "canceled") |
| end-time   | long      | false    | present | Search ends time, UTC time in millisecond                    | Value range [(present-179d), present], maximum query window size is 48 hours, query window shift should be within past 180 days, queriable range should be within past 2 hours for cancelled order (state = "canceled") |
| states     | string    | true     | NA      | One or more  states of order to include in the search, use comma to separate. | All possible order state (refer to introduction in this section) |
| from       | string    | false    | NA      | Search order id to begin with                                | NA                                                           |
| direct     | string    | false    | both    | Search direction when 'from' is used                         | next, prev                                                   |
| size       | integer   | false    | 100     | The number of orders to return                               | [1, 100]                                                     |

> The above command returns JSON structured like this:

```json
  "data": [    {      "id": 59378,      "symbol": "ethbtc",      "account-id": 100009,      "amount": "10.1000000000",      "price": "100.1000000000",      "created-at": 1494901162595,      "type": "buy-limit",      "field-amount": "10.1000000000",      "field-cash-amount": "1011.0100000000",      "field-fees": "0.0202000000",      "finished-at": 1494901400468,      "user-id": 1000,      "source": "api",      "state": "filled",      "canceled-at": 0    }  ]
```

### Response Content

| Field              | Data Type | Description                                                  |
| ------------------ | --------- | ------------------------------------------------------------ |
| id                 | long      | Order id                                                     |
| client-order-id    | string    | Client order id ("client-order-id" (if specified) can be returned from all open orders.	"client-order-id" (if specified) can be returned only from closed orders (state <> canceled) created within 7 days.	only those closed orders (state = canceled) created within 8 hours can be returned.) |
| account-id         | long      | Account id                                                   |
| user-id            | integer   | User id                                                      |
| amount             | string    | The amount of base currency in this order                    |
| symbol             | string    | The trading symbol to trade, e.g. ltcbtc, ethbtc ...         |
| price              | string    | The limit price of limit order                               |
| created-at         | long      | The timestamp in milliseconds when the order was created     |
| canceled-at        | long      | The timestamp in milliseconds when the order was canceled, or 0 if not canceled |
| finished-at        | long      | The timestamp in milliseconds when the order was finished, or 0 if not finished |
| type               | string    | All possible order type (refer to introduction in this section) |
| filled-amount      | string    | The amount which has been filled                             |
| filled-cash-amount | string    | The filled total in quote currency                           |
| filled-fees        | string    | Transaction fee (Accurate fees refer to matchresults endpoint) |
| source             | string    | All possible order source (refer to introduction in this section) |
| state              | string    | All possible order state (refer to introduction in this section) |
| exchange           | string    | Internal data                                                |
| batch              | string    | Internal data                                                |
| stop-price         | string    | trigger price of stop limit order                            |
| operator           | string    | operation character of stop price                            |

### Error code for invalid start-date/end-date

| err-code           | scenarios                                                    |
| ------------------ | ------------------------------------------------------------ |
| invalid_interval   | Start date is later than end date; the date between start date and end date is greater than 2 days |
| invalid_start_date | Start date is a future date; or start date is earlier than 180 days ago. |
| invalid_end_date   | end date is a future date; or end date is earlier than 180 days ago. |



## Search Historical Orders within 48 Hours

API Key Permission：Read<br>
Rate Limit (NEW): 20times/2s

This endpoint returns orders based on a specific searching criteria.
The orders created via API will no longer be queryable after being cancelled for more than 2 hours. 

### HTTP Request

`GET /v1/order/history`

>Request

```json
{   "symbol": "ethbtc",   "start-time": "1556417645419",   "end-time": "1556533539282",   "direct": "prev",   "size": "10"}
```

### Request Parameters

| Parameter  | Required | Data Type | Description                                                  | Default Value         | Value Range                                                  |
| ---------- | -------- | --------- | ------------------------------------------------------------ | --------------------- | ------------------------------------------------------------ |
| symbol     | false    | string    | The trading symbol to trade                                  | all                   | All supported trading symbol, e.g. ltcbtc, ethbtc ....Refer to `GET /v1/common/symbols` |
| start-time | false    | long      | Start time (included)                                        | The time 48 hours ago | UTC time in millisecond                                      |
| end-time   | false    | long      | End time (included)                                          | The query time        | UTC time in millisecond                                      |
| direct     | false    | string    | Direction of the query. (Note: If the total number of items in the search result is within the limitation defined in “size”, this field does not take effect.) | next                  | prev, next                                                   |
| size       | false    | int       | Number of items in each response                             | 100                   | [10,1000]                                                    |



> The above command returns JSON structured like this:

```json
{    "status": "ok",    "data": [        {            "id": 31215214553,            "symbol": "ethbtc",            "account-id": 4717043,            "amount": "1.000000000000000000",            "price": "1.000000000000000000",            "created-at": 1556533539282,            "type": "buy-limit",            "field-amount": "0.0",            "field-cash-amount": "0.0",            "field-fees": "0.0",            "finished-at": 1556533568953,            "source": "web",            "state": "canceled",            "canceled-at": 1556533568911        }    ]}
```

### Response Content

| Field             | Data Type | Description                                                  |
| ----------------- | --------- | ------------------------------------------------------------ |
| {account-id       | long      | Account ID                                                   |
| amount            | string    | Order size                                                   |
| canceled-at       | long      | Order cancellation time                                      |
| created-at        | long      | Order creation time                                          |
| field-amount      | string    | Executed order amount                                        |
| field-cash-amount | string    | Executed cash amount                                         |
| field-fees        | string    | Transaction fee (Accurate fees refer to matchresults endpoint) |
| finished-at       | long      | Last trade time                                              |
| id                | long      | Order ID                                                     |
| client-order-id   | string    | Client order id ("client-order-id" (if specified) can be returned only from closed orders (state <> canceled) created within 48 hours, upon order creation time.	only those closed orders (state = canceled) created within 8 hours can be returned.) |
| price             | string    | Order price                                                  |
| source            | string    | All possible order source (refer to introduction in this section) |
| state             | string    | Order status ( filled, partial-canceled, canceled )          |
| symbol            | string    | Trading symbol.e.g. ltcbtc, ethbtc ...                       |
| stop-price        | string    | trigger price of stop limit order                            |
| operator          | string    | operation character of stop price. e.g. get, lte             |
| type}             | string    | All possible order type (refer to introduction in this section) |
| next-time         | long      | Next query “start-time” (in response of “direct” = prev), Next query “end-time” (in response of “direct” = next). Note: Only when the total number of items in the search result exceeded the limitation defined in “size”, this field exists. UTC time in millisecond. |


## Search Match Results

API Key Permission：Read<br>
Rate Limit (NEW): 20times/2s

This endpoint returns the match results of past and current filled, or partially filled orders based on specific search criteria.

### HTTP Request

GET `/v1/order/matchresults`

### Request Parameters

| Parameter  | Data Type | Required | Default                                                      | Description                                 | Value Range                                                  |
| ---------- | --------- | -------- | ------------------------------------------------------------ | ------------------------------------------- | ------------------------------------------------------------ |
| symbol     | string    | true     | N/A                                                          | The trading symbol to trade                 | All supported trading symbol, e.g. ltcbtc, ethbtc.Refer to `GET /v1/common/symbols` |
| types      | string    | false    | all                                                          | The types of order to include in the search |                                                              |
| start-time | false     | long     | Far point of time of the query window (unix time in millisecond). Searching based on transact-time. The maximum size of the query window is 48 hour. The query window can be shifted within 120 days. | ((end-time) – 48hour)                       | [((end-time) – 48hour), (end-time)]                          |
| end-time   | false     | long     | Near point of time of the query window (unix time in millisecond). Searching based on transact-time. The maximum size of the query window is 48 hour. The query window can be shifted within 120 days. | current-time                                | [(current-time) – 120days,(current-time)]                    |
| from       | string    | false    | N/A                                                          | Search internal id to begin with            | if search next page, then this should be the last id (not trade-id) of last page; if search previous page, then this should be the first id (not trade-id) of last page |
| direct     | string    | false    | next                                                         | Search direction when 'from' is used        | next, prev                                                   |
| size       | int       | false    | 100                                                          | The number of orders to return              | [1, 500]                                                     |

> The above command returns JSON structured like this:

```json
  "data": [    {      "id": 29553,      "order-id": 59378,      "match-id": 59335,      "symbol": "ethbtc",      "type": "buy-limit",      "source": "api",      "price": "100.1000000000",      "filled-amount": "9.1155000000",      "filled-fees": "0.0182310000",      "created-at": 1494901400435,      "trade-id": 100282808529,      "role": "taker",      "filled-points": "0.0",      "fee-deduct-currency": "",      "fee-deduct-state": "done"    }  ]
```

### Response Content

<aside class="notice">The return data contains a list and each item in the list represents a match result</aside>

| Field         | Data Type | Description                                                  |
| ------------- | --------- | ------------------------------------------------------------ |
| id            | long      | Record id, non sequential, it can be used in "from" field for next request |
| symbol        | string    | The trading symbol to trade, e.g. ltcbtc, ethbtc             |
| order-id      | long      | The order id of this order                                   |
| match-id      | long      | The match id of this match                                   |
| trade-id      | long      | Unique trade ID                                              |
| price         | string    | The limit price of limit order                               |
| created-at    | long      | The timestamp in milliseconds when this record is created    |
| type          | string    | All possible order type (refer to introduction in this section) |
| filled-amount | string    | The amount which has been filled                             |
| filled-fees   | string    | Transaction fee (positive value). If maker rebate applicable, revert maker rebate value per trade (negative value). |
| fee-currency  | string    | Currency of transaction fee or transaction fee rebate (transaction fee of buy order is based on base currency, transaction fee of sell order is based on quote currency; transaction fee rebate of buy order is based on quote currency, transaction fee rebate of sell order is based on base currency) |
| source        | string    | All possible order source (refer to introduction in this section) |
| role          | string    | The role in the transaction: taker or maker.                 |
| status        | string    | state                                                        |
| <data>        | object    |                                                              |

Notes:<br>

- The calculated maker rebate value inside ‘filled-fees’ would not be paid immediately.<br>


### Error code for invalid start-date/end-date

| err-code           | scenarios                                                    |
| ------------------ | ------------------------------------------------------------ |
| invalid_interval   | Start date is later than end date; the date between start date and end date is greater than 2 days |
| invalid_start_date | Start date is a future date; or start date is earlier than 61 days ago. |
| invalid_end_date   | end date is a future date; or end date is earlier than 61 days ago. |

## Get Current Fee Rate Applied to The User

This endpoint returns the current transaction fee rate applied to the user.

API Key Permission：Read

```shell
curl "https://api.huobi.sg/v2/reference/transact-fee-rate?symbols=,ethbtc,ltcbtc"
```

### HTTP Request

`GET /v2/reference/transact-fee-rate`

### Request Parameters

| Parameter | Data Type | Required | Default | Description                                      | Value Range                                        |
| --------- | --------- | -------- | ------- | ------------------------------------------------ | -------------------------------------------------- |
| symbols   | string    | true     | NA      | The trading symbols to query, separated by comma | ltcbtc, ethbtc...Refer to `GET /v1/common/symbols` |

> Response:

```json
{  "code": "200",  "data": [     {        "symbol": "ethbtc",        "makerFeeRate":"0.002",        "takerFeeRate":"0.002",        "actualMakerRate": "0.002",        "actualTakerRate":"0.002     },     {        "symbol": "ethbtc",        "makerFeeRate":"0.002",        "takerFeeRate":"0.002",        "actualMakerRate": "0.002",        "actualTakerRate":"0.002    },     {        "symbol": "ltcbtc",        "makerFeeRate":"0.002",        "takerFeeRate":"0.002",        "actualMakerRate": "0.002",        "actualTakerRate":"0.002    }  ]}
```

### Response Content

|      | Field Name        | Data Type | Description                                                  |      |
| ---- | ----------------- | --------- | ------------------------------------------------------------ | ---- |
|      | code              | integer   | Status code                                                  |      |
|      | message           | string    | Error message (if any)                                       |      |
|      | data              | object    |                                                              |      |
|      | { symbol          | string    | Trading symbol                                               |      |
|      | makerFeeRate      | string    | Basic fee rate – passive side (positive value);If maker rebate applicable, revert maker rebate rate (negative value). |      |
|      | takerFeeRate      | string    | Basic fee rate – aggressive side                             |      |
|      | actualMakerRate   | string    | Deducted fee rate – passive side (positive value). If deduction is inapplicable or disabled, return basic fee rate.If maker rebate applicable, revert maker rebate rate (negative value). |      |
|      | actualTakerRate } | string    | Deducted fee rate – aggressive side. If deduction is inapplicable or disabled, return basic fee rate. |      |

Note：

- If makerFeeRate/actualMakerRate is positive，this field means the transaction fee rate.
- If makerFeeRate/actualMakerRate is negative, this field means the rebate fee rate.

## Error Code

Below is the error code and description returned by Trading APIs

| Error Code                                                   | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| base-argument-unsupported                                    | The specified parameter is not supported                     |
| base-system-error                                            | System internel error. For placing or canceling order, it is mostly due to cache issue, please try again later. |
| login-required                                               | Signature is missing, or user not find (key and uid not match). |
| base-record-invalid                                          | Failed to get data, please try again later                   |
| order-amount-over-limit                                      | The amount of order exceeds the limitation                   |
| base-symbol-trade-disabled                                   | The symbol is disabled for trading                           |
| base-operation-forbidden                                     | The operation is forbidden for current user or the symbol is not allowed to trade over OTC |
| account-get-accounts-inexistent-error                        | The account doesn't exist in current user                    |
| account-account-id-inexistent                                | The account id doesn't exist                                 |
| order-disabled                                               | The symbol is pending and not allowed to place order         |
| cancel-disabled                                              | The symbol is pending and not allowed to cancel order        |
| order-invalid-price                                          | The order price is invalid, usually exceeds the 10% of latest trade price |
| order-accountbalance-error                                   | The account balance is insufficient                          |
| order-limitorder-price-min-error                             | Sell price cannot be lower than specific price               |
| order-limitorder-price-max-error                             | Buy price cannot be higher than specific price               |
| order-limitorder-amount-min-error                            | Limit order amount can not be less than specific number      |
| order-limitorder-amount-max-error                            | Limit order amount can not be more than specific number      |
| order-etp-nav-price-min-error                                | Order price cannot be lower than specific percentage         |
| order-etp-nav-price-max-error                                | Order price cannot be higher than specific percentage        |
| order-orderprice-precision-error                             | Order price precision error                                  |
| order-orderamount-precision-error                            | Order amount precision error                                 |
| order-value-min-error                                        | Order value cannot be lower than specific value              |
| order-marketorder-amount-min-error                           | Market order sell amount cannot be less than specific amount |
| order-marketorder-amount-buy-max-error                       | Market order buy amount(value) cannot be more than specific amount(value) |
| order-marketorder-amount-sell-max-error                      | Market order sell amount cannot be more than specific amount |
| order-holding-limit-failed                                   | Exceed the holding limit of the currency                     |
| order-type-invalid                                           | Order type is invalid                                        |
| order-orderstate-error                                       | Order state is invalid                                       |
| order-date-limit-error                                       | Order query date exceed the limit                            |
| order-source-invalid                                         | Order source is invalid                                      |
| order-update-error                                           | Order update error                                           |
| order-user-cancel-forbidden                                  | IOC or FOK order is not allowed to cancel                    |
| order-price-greater-than-limit                               | Order price is higher than the limitation before market opens |
| order-price-less-than-limit                                  | Order price is lower than the limitation before market opens |
| market-orders-not-support-during-limit-price-trading         | Market orders are not supported during limit-price trading   |
| price-exceeds-the-protective-price-during-limit-price-trading | The price exceeds the protective price during limit-price trading |
| invalid-client-order-id                                      | The parameter client order id is duplicated (within last 24h) in place or cancel order request |
| invalid-interval                                             | Query window is zero, negative or greater than limitation    |
| invalid-start-date                                           | The start date is invalid                                    |
| invalid-end-date                                             | The end date is invalid                                      |
| invalid-start-time                                           | The start time is invalid                                    |
| invalid-end-time                                             | The end time is invalid                                      |
| validation-constraints-required                              | The specified parameters is missing                          |
| symbol-not-support                                           | The symbol is not support for cross margin or C2C            |
| not-found                                                    | The order id is not found                                    |
| base-not-found                                               | The record is not found                                      |

## FAQ

### Q1：What is client-order-id?

A： The `client-order-id` is an optional request parameter while placing order. It's string type which maximum length is 64. The client order id is generated by client, and is only valid within 8 hours (It’s only valid within 2 hours for the final state).

### Q2：How to get the order size, price and decimal precision?

A： You can call API `GET /v1/common/symbols` to get the currency pair information, pay attention to the difference between the minimum amount and the minimum price.   

Below are common errors:

- order-value-min-error: The order price is less than minimum price
- order-orderprice-precision-error : The precision for limited order price is wrong 
- order-orderamount-precision-error : The precision for limited order amount is wrong
- order-limitorder-price-max-error : The limited order price is higher than the threshold
- order-limitorder-price-min-error : The limited order price is lower than the threshold
- order-limitorder-amount-max-error : The limited order amount is larger than the threshold
- order-limitorder-amount-min-error : The limited order amount is smaller than the threshold  

### Q3：Why I got insufficient balance error while placing an order just after a successful order matching?

A：To ensure the low latency of order update, Order update push is made directly after order matching. Meanwhile, the clearing service of that order may be still in progress at backend. It is suggested to follow either of below to ensure a successful order submission:

1、Subscribe to WebSocket topic `accounts` for getting account balance moves to ensure the completion of asset clearing.

2、After receiving WebSocket push message, check account balance from REST endpoint to ensure sufficient available balance for the next order submission.

3、Leave sufficient balance in your account.

### Q4: What is the difference between 'filled-fees' and 'filled-points' in match result?

A: Transaction fee can be paid from either of below. They won't exist at the same time.

1、filled-fees: Filled-fee is also called transaction fee. It's charged from your income currency from the transaction. For example, if your purchase order of BTC/btc got matched，the transaction fee will be based on BTC.

2、filled-points: If user enabled transaction fee deduction, the fee should be charged from either HT or Point. When there's sufficient fund in HT/Point, filled-fees is empty while filled-points has value. That means the deduction is made via HT/Point. User could refer to field `fee-deduct-currency` to get the exact deduction type of the transaction. 

### Q5: What is the difference between 'match-id' and 'trade-id' in matching result?

A: The `match-id` is the identity for order matching, while the `trade-id` is the unique identifier for each trade. One `match-id` may be correlated with multiple `trade-id`, or no `trade-id`(if the order is cancelled). For example, if a taker's order got matched with 3 maker's orders at the same time, it generates 3 trade IDs but only one match ID.

### Q6: Why the order submission could be rejected even though the order price is set as same as current best bid (or best ask)?

A: For some extreme illiquid trading symbols, the best quote price at particular time might be far away from last trade price. But the price limit is actually based on last trade price which could possibly exclude best quote price from valid range for any new order. It is suggested to place orders based on the WebSocket pushed Bid and market data.



# Websocket Market Data

## Introduction

### Websocket URL

**Websocket Market Feed (excluding MBP incremental channel & its REQ channel)**

**`wss://api.huobi.sg/ws`**
or
**`wss://api-aws.huobi.sg/ws`**

**MBP incremental channel & its REQ channel)**

**`wss://api.huobi.sg/feed`**
or
**`wss://api-aws.huobi.sg/feed`**

### Data Format

All return data of websocket Market APIs are compressed with GZIP so they need to be unzipped.

### Heartbeat and Connection

```json
{"ping": 1492420473027} 
```

After connected to New Huo's Websocket server, the server will send heartbeat periodically (currently at 5s interval). The heartbeat message will have an integer in it, e.g.

```json
{"pong": 1492420473027} 
```

When client receives this heartbeat message, it should respond with a matching "pong" message which has the same integer in it, e.g.

<aside class="warning">After the server sent two consecutive heartbeat messages without receiving at least one matching "pong" response from a client, then right before server sends the next "ping" heartbeat, the server will be disconnected with the client server.</aside>

### Subscribe to Topic

> Sub request:

```json
{  "sub": "market.ethbtc.kline.1min",  "id": "id1"}
```

To receive data you have to send a "sub" message first.

{
  "sub": "topic to sub",
  "id": "id generate by client"
}

> Sub response:

```json
{  "id": "id1",  "status": "ok",  "subbed": "market.ethbtc.kline.1min",  "ts": 1489474081631}
```

After successfully subscribed, you will receive a response to confirm subscription

Then, you will received messages when there is any update in the subcribed topics.

### Unsubscribe

> UnSub request:

```json
{  "unsub": "market.ethbtc.trade.detail",  "id": "id4"}
```

To unsubscribe, you need to send below message

{
  "unsub": "topic to unsub",
  "id": "id generate by client"
}

> UnSub response:

```json
{  "id": "id4",  "status": "ok",  "unsubbed": "market.ethbtc.trade.detail",  "ts": 1494326028889}
```

And you will receive a message to confirm the action.

### Pull Data

While connected to websocket, you can also use it in pull style by sending message to the server.

To request pull style data, you send below message

{
  "req": "topic to req",
  "id": "id generate by client"
}

You will receive a response accordingly and immediately

### Rate Limit

**Rate limt of pull style query (req)**

The limitation of single connection is 100 ms.

## Market Candlestick

This topic sends a new candlestick whenever it is available.

### Topic

`market.$symbol$.kline.$period$`

> Subscribe request

```json
{  "sub": "market.ethbtc.kline.1min",  "id": "id1"}
```

### Topic Parameter

| Parameter | Data Type | Required | Description          | Value Range                                                  |
| --------- | --------- | -------- | -------------------- | ------------------------------------------------------------ |
| symbol    | string    | true     | Trading symbol       | ltcbtc, ethbtc...                                            |
| period    | string    | true     | Candlestick interval | 1min, 5min, 15min, 30min, 60min, 4hour, 1day, 1mon, 1week, 1year |

> Response

```json
{  "id": "id1",  "status": "ok",  "subbed": "market.ethbtc.kline.1min",  "ts": 1489474081631 //system response time}
```

> Update example

```json
{  "ch": "market.ethbtc.kline.1min",  "ts": 1489474082831, //system update time  "tick": {    "id": 1489464480,    "amount": 0.0,    "count": 0,    "open": 7962.62,    "close": 7962.62,    "low": 7962.62,    "high": 7962.62,    "vol": 0.0  }}
```

### Update Content

| Field  | Data Type | Description                                                  |
| ------ | --------- | ------------------------------------------------------------ |
| id     | integer   | UNIX epoch timestamp in second as response id                |
| amount | float     | Aggregated trading volume during the interval (in base currency) |
| count  | integer   | Number of trades during the interval                         |
| open   | float     | Opening price during the interval                            |
| close  | float     | Closing price during the interval                            |
| low    | float     | Low price during the interval                                |
| high   | float     | High price during the interval                               |
| vol    | float     | Aggregated trading value during the interval (in quote currency) |



### Pull Request

Pull request is supported with extra parameters to define the range. The maximum number of ticks in each response is 300.

```json
{  "req": "market.$symbol.kline.$period",  "id": "id generated by client",  "from": "from time in epoch seconds",  "to": "to time in epoch seconds"}
```

| Parameter | Data Type | Required | Default Value                         | Description                        | Value Range                                                  |
| --------- | --------- | -------- | ------------------------------------- | ---------------------------------- | ------------------------------------------------------------ |
| from      | integer   | false    | 1501174800(2017-07-28T00:00:00+08:00) | "From" time (epoch time in second) | [1501174800, 2556115200]                                     |
| to        | integer   | false    | 2556115200(2050-01-01T00:00:00+08:00) | "To" time (epoch time in second)   | [1501174800, 2556115200] or ($from, 2556115200] if "from" is set |

## Market Ticker

Retrieve the market ticker,data is pushed every 100ms.

### Topic

`market.$symbol.ticker`

> Subscribe request

```json
{  "sub": "market.ethbtc.ticker"}
```

### Request Parameters

| Parameter | Data Type | Required | Default | Description                 | Value Range                                                  |
| --------- | --------- | -------- | ------- | --------------------------- | ------------------------------------------------------------ |
| symbol    | string    | true     | NA      | The trading symbol to query | All supported trading symbol, e.g. ltcbtc, ethbtc...Refer to `/v1/common/symbols` |

> The above command returns JSON structured like this:

```json
{"ch": "market.ethbtc.ticker", "ts": 1628587397308, "tick": {"open": 44718.5, "high": 46711, "low": 44480.81, "close": 45868.99, "amount": 22527.427922989766, "vol": 1030630905.0136755, "count": 676424, "bid": 45868.98, "bidSize": 0.016782, "ask": 45868.99, "askSize": 3.1279664455029423, "lastPrice": 45868.99, "lastSize": 0.007444}}
```

### Response Content

| Field     | Data Type | Description                                                  |
| --------- | --------- | ------------------------------------------------------------ |
| id        | long      | The internal identity                                        |
| amount    | float     | Accumulated trading volume of last 24 hours (rotating 24h), in base currency |
| count     | integer   | The number of completed trades (rotating 24h)                |
| open      | float     | The opening price of last 24 hours (rotating 24h)            |
| close     | float     | The last price of last 24 hours (rotating 24h)               |
| low       | float     | The lowest price of last 24 hours (rotating 24h)             |
| high      | float     | The highest price of last 24 hours (rotating 24h)            |
| vol       | float     | Accumulated trading value of last 24 hours (rotating 24h), in quote currency |
| bid       | float     | Best bid price                                               |
| bidSize   | float     | Best bid size                                                |
| ask       | float     | Best ask price                                               |
| askSize   | float     | Best ask size                                                |
| lastPrice | float     | Last traded price                                            |
| lastSize  | float     | Last traded size                                             |

## 

## Market Depth

This topic sends the latest market by price order book in snapshot mode at 1-second interval.

### Topic

`market.$symbol.depth.$type`

> Subscribe request

```json
{  "sub": "market.ethbtc.depth.step0",  "id": "id1"}
```

### Topic Parameter

| Parameter | Data Type | Required | Default Value | Description                                   | Value Range                                        |
| --------- | --------- | -------- | ------------- | --------------------------------------------- | -------------------------------------------------- |
| symbol    | string    | true     | NA            | Trading symbol                                | ltcbtc, ethbtc...Refer to `GET /v1/common/symbols` |
| type      | string    | true     | step0         | Market depth aggregation level, details below | step0, step1, step2, step3, step4, step5           |

**"type" Details**

| Value | Description                          |
| ----- | ------------------------------------ |
| step0 | No market depth aggregation          |
| step1 | Aggregation level = precision*10     |
| step2 | Aggregation level = precision*100    |
| step3 | Aggregation level = precision*1000   |
| step4 | Aggregation level = precision*10000  |
| step5 | Aggregation level = precision*100000 |

While type is set as ‘step0’, the market depth data supports up to 150 levels.
While type is set as ‘step1’, ‘step2’, ‘step3’, ‘step4’, or ‘step5’, the market depth data supports up to 20 levels.

> Response

```json
{  "id": "id1",  "status": "ok",  "subbed": "market.ethbtc.depth.step0",  "ts": 1489474081631 //system response time}
```

> Update example

```json
{  "ch": "market.htbtc.depth.step0",  "ts": 1572362902027, //system update time  "tick": {    "bids": [      [3.7721, 344.86],// [price, size]      [3.7709, 46.66]    ],    "asks": [      [3.7745, 15.44],      [3.7746, 70.52]    ],    "version": 100434317651,    "ts": 1572362902012 //quote time  }}
```

### Update Content

<aside class="notice">Under 'tick' object there is a list of bids and a list of asks</aside>

| Field   | Data Type | Description                                                  |
| ------- | --------- | ------------------------------------------------------------ |
| bids    | object    | The current all bids in format [price, size]                 |
| asks    | object    | The current all asks in format [price, size]                 |
| version | integer   | Internal data                                                |
| ts      | integer   | The UNIX timestamp in milliseconds adjusted to Singapore time |

<aside class="notice">When symbol is set to "hb10" amount, count, and vol will always have the value of 0</aside>

### Pull Request

Pull request is supported.

```json
{  "req": "market.ethbtc.depth.step0",  "id": "id10"}
```

## Market By Price (incremental update)

User could subscribe to this channel to receive incremental update of Market By Price order book. Refresh message, the full image of the order book, are acquirable from the same channel, upon "req" request.

**MBP incremental channel & its REQ channel)**

**`wss://api.huobi.sg/feed`**
or
**`wss://api-aws.huobi.sg/feed`**

Suggested downstream data processing:<br>

1)	Subscribe to incremental updates and start to cache them;<br>
2)	Request refresh message (with same number of levels), and base on its “seqNum” to align it with the cached incremental message which has the same “prevSeqNum”;<br>
3)	Start to continuously process incremental messages to build up MBP book;<br>
4)	The “prevSeqNum” of the current incremental message must be the same with “seqNum” of the previous message, otherwise it implicates message loss which should require another round of refresh message retrieval and alignment;<br>
5)	Once received a new price level from incremental message, that price level should be inserted into appropriate position of existing MBP book;<br>
6)	Once received an updated “size” at the existing price level from incremental message, the size should be replaced directly by the new value;<br>
7)	Once received a “size=0” at existing price level from incremental message, that price level should be removed from MBP book;<br>
8)	If one incremental message includes updates of multiple price levels, all of those levels should be updated simultaneously in MBP book.<br>

Currently New Huo Singapore only supports 5-level/20-level MBP incremental channel and 150-level incremental channel, the differences between them are -<br>

1) Different depth of market.<br>
2) 5-level/20-level incremental MBP is a tick by tick feed, which means whenever there is an order book change at that level, it pushes an update; 150 levels incremental MBP feed is based on the gap between two snapshots at 100ms interval.<br>
3) While there is single side order book update, either bid or ask, the incremental message sent from 5-level/20-level MBP feed only contains that side update. <br>

```json
{    "ch": "market.ethbtc.mbp.5",    "ts": 1573199608679,    "tick": {        "seqNum": 100020146795,        "prevSeqNum": 100020146794,        "asks": [            [645.140000000000000000, 26.755973959140651643]        ]    }}
```

But the incremental message from 150 levels MBP feed contains not only that side update and also a blank object for another side.

```json
{    "ch":"market.ethbtc.mbp.150",    "ts":1573199608679,    "tick":{        "seqNum":100020146795,        "prevSeqNum":100020146794,        "bids":[ ],        "asks":[            [645.14,26.75597395914065]        ]    }}
```

In the near future, New Huo Singapore will align the update behavior of 150-level incremental channel with 5-level/20-level, which means while single side order book changed (either bid or ask), the update message will be no longer including a blank object for another side.<br>

4) While there is nothing change between two snapshots in past 100ms, the 150 levels incremental MBP feed still sends out a message which contains two blank objects – bids & asks. <br>

```json
{    "ch":"market.ethbtc.mbp.150",    "ts":1585074391470,    "tick":{        "seqNum":100772868478,        "prevSeqNum":100772868476,        "bids":[  ],        "asks":[  ]    }}
```

But 5-level/20-level incremental channel won’t disseminate any update in such a case.<br>
In the future, New Huo Singapore will align the update behavior of 150-level incremental channel with 5-level/20-level, which means while there is no order book change at all, the channel will be no longer disseminating messages of blank object any more.<br>

5) 5-level/20-level incremental channel only supports the following symbols at this stage - ethbtc,ltcbtc,bchbtc, while 150-level incremental channel supports all symbols.<br>

REQ channel supports refreshing message for 5-level, 20-level, and 150-level.

### Subscribe incremntal updates

`market.$symbol.mbp.$levels`

> Sub request

```json
{  "sub": "market.ethbtc.mbp.5",  "id": "id1"}
```

### Request refresh update

`market.$symbol.mbp.$levels`

> Req request

```json
{  "req": "market.ethbtc.mbp.5",  "id": "id2"}
```

### Parameters

| Field Name | Data Type | Mandatory | Default Value | Description                                        | Value Range                                                  |
| ---------- | --------- | --------- | ------------- | -------------------------------------------------- | ------------------------------------------------------------ |
| symbol     | string    | true      | NA            | Trading symbol (wildcard inacceptable)             |                                                              |
| levels     | integer   | true      | NA            | Number of price levels (Valid value: 5,20,150,400) | Only support the number of price levels at 5, 20,150 or 400 at this point of time. |

> Response (Incremental update subscription)

```json
{  "id": "id1",  "status": "ok",  "subbed": "market.ethbtc.mbp.5",  "ts": 1489474081631 //system response time}
```

> Incremental Update (Incremental update subscription)

```json
{	"ch": "market.ethbtc.mbp.5",	"ts": 1573199608679, //system update time  "tick": {           "seqNum": 100020146795,            "prevSeqNum": 100020146794,           "asks": [                 [645.140000000000000000, 26.755973959140651643] // [price, size]           ]      }}
```

> Response (Refresh update acquisition)

```json
{	"id": "id2",	"rep": "market.ethbtc.mbp.150",	"status": "ok",	"data": {		"seqNum": 100020142010,		"bids": [			[618.37, 71.594], // [price, size]			[423.33, 77.726],			[223.18, 47.997],			[219.34, 24.82],			[210.34, 94.463]    ],		"asks": [			[650.59, 14.909733438479636],			[650.63, 97.996],			[650.77, 97.465],			[651.23, 83.973],			[651.42, 34.465]		]	}}
```

### Update Content

| Field Name | Data Type | Description                                                  |
| ---------- | --------- | ------------------------------------------------------------ |
| seqNum     | integer   | Sequence number of the message                               |
| prevSeqNum | integer   | Sequence number of previous message                          |
| bids       | object    | Bid side, (in descending order of “price”), ["price","size"] |
| asks       | object    | Ask side, (in ascending order of “price”), ["price","size"]  |

## Market By Price (refresh update)

User could subscribe to this channel to receive refresh update of Market By Price order book. The update interval is around 100ms.

### Subscription

`market.$symbol.mbp.refresh.$levels`

```json
{"sub": "market.ltcbtc.mbp.refresh.20","id": "id1"}
```

### Parameters

| Field Name | Data Type | Mandatory | Default Value | Description                            | Value Range |
| ---------- | --------- | --------- | ------------- | -------------------------------------- | ----------- |
| symbol     | string    | true      | NA            | Trading symbol (wildcard inacceptable) |             |
| levels     | integer   | true      | NA            | Number of price levels                 | 5,10,20     |

> Response

```json
{"id": "id1","status": "ok","subbed": "market.ethbtc.mbp.refresh.20","ts": 1489474081631 //system response time}
```

> Response

```json
{"ch": "market.btcusdt.mbp.refresh.20","ts": 1573199608679, //system update time"tick": {		"seqNum": 100020142010,		"bids": [			[618.37, 71.594], // [price, size]			[423.33, 77.726],			[223.18, 47.997],			[219.34, 24.82],			[210.34, 94.463], ... // rest levels omitted   		],		"asks": [			[650.59, 14.909733438479636],			[650.63, 97.996],			[650.77, 97.465],			[651.23, 83.973],			[651.42, 34.465], ... // rest levels omitted		]}}
```

### Update Content

| Field Name | Data Type | Description                                                  |
| ---------- | --------- | ------------------------------------------------------------ |
| seqNum     | integer   | Sequence number of the message                               |
| bids       | object    | Bid side, (in descending order of “price”), ["price","size"] |
| asks       | object    | Ask side, (in ascending order of “price”), ["price","size"]  |

## Best Bid/Offer

User can receive BBO (Best Bid/Offer) update in tick by tick mode.

### Topic

`market.$symbol.bbo`

> Subscribe request

```json
{  "sub": "market.ethbtc.bbo",  "id": "id1"}
```

### Topic parameter

| Parameter | Data Type | Required | Default Value | Description    | Value Range                                        |
| --------- | --------- | -------- | ------------- | -------------- | -------------------------------------------------- |
| symbol    | string    | true     | NA            | Trading symbol | ltcbtc, ethbtc...Refer to `GET /v1/common/symbols` |

> Response

```json
{  "id": "id1",  "status": "ok",  "subbed": "market.ethbtc.bbo",  "ts": 1489474081631 //system response time}
```

> Update example

```json
{  "ch": "market.ethbtc.bbo",  "ts": 1489474082831, //system update time  "tick": {    "symbol": "ltcbtc",    "quoteTime": "1489474082811",    "bid": "10008.31",    "bidSize": "0.01",    "ask": "10009.54",    "askSize": "0.3",    "seqId":"10242474683"  }}
```

### Update Content

| Field     | Data Type | Description     |
| --------- | --------- | --------------- |
| symbol    | string    | Trading symbol  |
| quoteTime | long      | Quote time      |
| bid       | float     | Best bid        |
| bidSize   | float     | Best bid size   |
| ask       | float     | Best ask        |
| askSize   | float     | Best ask size   |
| seqId     | int       | Sequence number |


## Trade Detail

This topic sends the latest completed trades. It updates in tick by tick mode.

### Topic

`market.$symbol.trade.detail`

> Subscribe request

```json
{  "sub": "market.ethbtc.trade.detail",  "id": "id1"}
```

### Topic Parameter

| Parameter | Data Type | Required | Default Value | Description    | Value Range                                        |
| --------- | --------- | -------- | ------------- | -------------- | -------------------------------------------------- |
| symbol    | string    | true     | NA            | Trading symbol | ltcbtc, ethbtc...Refer to `GET /v1/common/symbols` |

> Response

```json
{  "id": "id1",  "status": "ok",  "subbed": "market.ethbtc.trade.detail",  "ts": 1489474081631 //system response time}
```

> Update example

```json
{  "ch": "market.ethbtc.trade.detail",  "ts": 1489474082831, //system update time  "tick": {        "id": 14650745135,        "ts": 1533265950234, //trade time        "data": [            {                "amount": 0.0099,                "ts": 1533265950234, //trade time                "id": 146507451359183894799,                "tradeId": 102043494568,                "price": 401.74,                "direction": "buy"            }            // more Trade Detail data here        ]  }}
```

### Update Content

| Field     | Data Type | Description                                     |
| --------- | --------- | ----------------------------------------------- |
| id        | integer   | Unique trade id (to be obsoleted)               |
| tradeId   | integer   | Unique trade id (NEW)                           |
| amount    | float     | The volume of the trade (buy side or sell side) |
| price     | float     | The price of the trade                          |
| ts        | integer   | timestamp (UNIX epoch time in millisecond)      |
| direction | string    | direction of the trade (taker): 'buy' or 'sell' |

### Pull Request

Pull request (of maximum latest 300 trade records) is supported.

```json
{  "req": "market.ethbtc.trade.detail",  "id": "id11"}
```

## Market Details

This topic sends the latest market stats with 24h summary. It updates in snapshot mode, in frequency of no more than 10 times per second.

### Topic

`market.$symbol.detail`

> Subscribe request

```json
{  "sub": "market.ethbtc.detail",  "id": "id1"}
```

### Topic Parameter

| Parameter | Data Type | Required | Default Value | Description    | Value Range                                        |
| --------- | --------- | -------- | ------------- | -------------- | -------------------------------------------------- |
| symbol    | string    | true     | NA            | Trading symbol | ltcbtc, ethbtc...Refer to `GET /v1/common/symbols` |

> Response

```json
{  "id": "id1",  "status": "ok",  "subbed": "market.ethbtc.detail",  "ts": 1489474081631 //system response time}
```

> Update example

```json
{  "ch": "market.ethbtc.detail",  "ts": 1494496390001, //system update time  "tick": {    "amount": 12224.2922,    "open":   9790.52,    "close":  10195.00,    "high":   10300.00,    "id":     1494496390,    "count":  15195,    "low":    9657.00,    "vol":    121906001.754751  }}
```

### Update Content

| Field  | Data Type | Description                                              |
| ------ | --------- | -------------------------------------------------------- |
| id     | integer   | UNIX epoch timestamp in second as response id            |
| amount | float     | Aggregated trading volume in past 24H (in base currency) |
| count  | integer   | Number of trades in past 24H                             |
| open   | float     | Opening price in past 24H                                |
| close  | float     | Last price                                               |
| low    | float     | Low price in past 24H                                    |
| high   | float     | High price in past 24H                                   |
| vol    | float     | Aggregated trading value in past 24H (in quote currency) |

### Pull Request

Pull request is supported.

```json
{  "req": "market.ethbtc.detail",  "id": "id11"}
```

# Websocket Account and Order

## Introduction

### Access URL

**Websocket Asset and Order**

**`wss://api.huobi.sg/ws/v2`**  

**`wss://api-aws.huobi.sg/ws/v2`**   

Note: 
By comparing to api-aws.huobi.sg, the network latency to api-aws.huobi.sg is lower, for those client's servers locating at AWS.

### Message Compression

Unlike Market WebSocket, the return data of Account and Order Websocket are not compressed by GZIP.

### Heartbeat

```json
{	"action": "ping",	"data": {		"ts": 1575537778295	}}
```

Once the Websocket connection is established, New Huo server will periodically send "ping" message at 20s interval, with an integer inside.

```json
{    "action": "pong",    "data": {          "ts": 1575537778295 // the same with "ping" message    }}
```

Once client receives "ping", it should respond "pong" message back with the same integer.

### Valid Values of `action`

| Valid Values | Description                                 |
| ------------ | ------------------------------------------- |
| sub          | Subscribe                                   |
| req          | Request                                     |
| ping,pong    | Heartbeat                                   |
| push         | Push (from New Huo server to client's server) |

### Rate Limit

There are multiple limitations for this version:

- The limitation of single connection for **valid** request (including req, sub, unsub, excluding ping/pong or other invalid request) is **50 per second**. It will return "too many request" when the limit is exceeded.
- A single API Key can establish **10** connections. It will return "too many connection" when the limit is exceeded.
- The limitation of requests from single IP is **100 per second**. It will return "too many request" when the limitation is exceeded.

### Authentication

Authentication request field list

| Field            | Mandatory | Data Type | Description                                                  |
| ---------------- | --------- | --------- | ------------------------------------------------------------ |
| action           | true      | string    | Action type, valid value: "req"                              |
| ch               | true      | string    | Channel, valid value: "auth"                                 |
| authType         | true      | string    | Authentication type, valid value: "api". Note: this is not part of signature calculation |
| accessKey        | true      | string    | Access key                                                   |
| signatureMethod  | true      | string    | Signature method, valid value: "HmacSHA256"                  |
| signatureVersion | true      | string    | Signature version, valid value: "2.1"                        |
| timestamp        | true      | string    | Timestamp in UTC in format like 2017-05-11T16:22:06          |
| signature        | true      | string    | Signature                                                    |

```json
{    "action": "req",     "ch": "auth",    "params": {         "authType":"api",        "accessKey": "e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx",        "signatureMethod": "HmacSHA256",        "signatureVersion": "2.1",        "timestamp": "2019-09-01T18:16:16",        "signature": "4F65x5A2bLyMWVQj3Aqp+B4w+ivaA7n5Oi2SuYtCJ9o="    }}
```

This is an exmaple of authentication request:

```json
{	"action": "req",	"code": 200,	"ch": "auth",	"data": {}}
```

The response of success:

### Generating Signature 

The signature generation method of Account and Order WebSocket is similar with Rest API , with only following differences:

1. The request method should be "GET", to URL "/ws/v2".
2. The involved field names in signature generation are: accessKey，signatureMethod，signatureVersion，timestamp
3. The valid value of signatureVersion is 2.1.

Please refer to detailed signature generation steps from: [https://huobi-sg.github.io/docs/spot/v1/cn/#c64cd15fdc]

```
GET\napi.huobi.sg\n/ws/v2\naccessKey=0664b695-rfhfg2mkl3-abbf6c5d-49810&signatureMethod=HmacSHA256&signatureVersion=2.1&timestamp=2019-12-05T11%3A53%3A03
```

The final string involved in signature generation should be like below:

Note: The data in JSON request doesn't require URL encode

### Subscribe a Topic to Continuously Receive Updates

> Sub request:

```json
{	"action": "sub",	"ch": "accounts.update"}
```

Once the Websocket connection is established, Websocket client could send following request to subscribe a topic:

> Sub respose:

```json
{	"action": "sub",	"code": 200,	"ch": "accounts.update#0",	"data": {}}
```

Upon success, Websocket client should receive a response below:

## Subscribe Order Updates

API Key Permission: Read

An order update can be triggered by any of following:<br>

-	Conditional order triggering failure (eventType=trigger)<br>
-	Conditional order cancellation before trigger (eventType=deletion)<br>
-	Order creation (eventType=creation)<br>
-	Order matching (eventType=trade)<br>
-	Order cancellation (eventType=cancellation)<br>

The field list in order update message can be various per event type, developers can design the data structure in either of two ways:<br>

- Define a data structure including fields for all event types, allowing a few of them are null<br>
- Define different data structure for each event type to include specific fields, inheriting from a common data structure which has common fields

### Topic

` orders#${symbol}`

> Subscribe request

```json
{	"action": "sub",	"ch": "orders#ethbtc"}
```

> Response

```json
{	"action": "sub",	"code": 200,	"ch": "orders#ethbtc",	"data": {}}
```

### Subscription Field

| Field  | Data Type | Description                            |
| ------ | --------- | -------------------------------------- |
| symbol | string    | Trading symbol (wildcard * is allowed) |

### Update Content

```json
{	"action":"push",	"ch":"orders#ethbtc",	"data":	{		"orderSide":"buy",		"lastActTime":1583853365586,		"clientOrderId":"abc123",		"orderStatus":"rejected",		"symbol":"ltcbtc",		"eventType":"trigger",		"errCode": 2002,		"errMessage":"invalid.client.order.id (NT)"	}}
```

After conditional order triggering failure –

| Field         | Data Type | Description                                                  |
| ------------- | --------- | ------------------------------------------------------------ |
| eventType     | string    | Event type, valid value: trigger (only applicable for conditional order) |
| symbol        | string    | Trading symbol                                               |
| clientOrderId | string    | Client order ID                                              |
| orderSide     | string    | Order side, valid value: buy, sell                           |
| orderStatus   | string    | Order status, valid value: rejected                          |
| errCode       | int       | Error code for triggering failure                            |
| errMessage    | string    | Error message for triggering failure                         |
| lastActTime   | long      | Order triggering failure time                                |

```json
{	"action":"push",	"ch":"orders#ethbtc",	"data":	{		"orderSide":"buy",		"lastActTime":1583853365586,		"clientOrderId":"abc123",		"orderStatus":"canceled",		"symbol":"ltcbtc",		"eventType":"deletion"	}}
```

After conditional order being cancelled before triggering –

| Field         | Data Type | Description                                                  |
| ------------- | --------- | ------------------------------------------------------------ |
| eventType     | string    | Event type, valid value: deletion (only applicable for conditional order) |
| symbol        | string    | Trading symbol                                               |
| clientOrderId | string    | Client order ID                                              |
| orderSide     | string    | Order side, valid value: buy, sell                           |
| orderStatus   | string    | Order status, valid value: canceled                          |
| lastActTime   | long      | Order trigger time                                           |

```json
{	"action":"push",	"ch":"orders#ethbtc",	"data":	{		"orderSize":"2.000000000000000000",		"orderCreateTime":1583853365586,		"accountId":992701,		"orderPrice":"77.000000000000000000",		"type":"sell-limit",		"orderId":27163533,		"clientOrderId":"abc123",		"orderSource":"spot-api",		"orderStatus":"submitted",		"symbol":"ethbtc",		"eventType":"creation"	}}
```

After order is submitted –

| Field           | Data Type | Description                                                  |
| --------------- | --------- | ------------------------------------------------------------ |
| eventType       | string    | Event type, valid value: creation                            |
| symbol          | string    | Trading symbol                                               |
| accountId       | long      | account ID                                                   |
| orderId         | long      | Order ID                                                     |
| clientOrderId   | string    | Client order ID (if any)                                     |
| orderSource     | string    | Order source                                                 |
| orderPrice      | string    | Order price                                                  |
| orderSize       | string    | Order size (inapplicable for market buy order)               |
| orderValue      | string    | Order value (only applicable for market buy order)           |
| type            | string    | Order type, valid value: buy-market, sell-market, buy-limit, sell-limit |
| orderStatus     | string    | Order status, valid value: submitted                         |
| orderCreateTime | long      | Order creation time                                          |

Note:<br>

- The topic will send creation update for taker's order before it being filled.<br>

```json
{	"action":"push",	"ch":"orders#ethbtc",	"data":	{		"tradePrice":"76.000000000000000000",		"tradeVolume":"1.013157894736842100",		"tradeId":301,		"tradeTime":1583854188883,		"aggressor":true,		"remainAmt":"0.000000000000000400000000000000000000",		"execAmt":"2",		"orderId":27163536,		"type":"sell-limit",		"clientOrderId":"abc123",		"orderSource":"spot-api",		"orderPrice":"15000",		"orderSize":"0.01",		"orderStatus":"filled",		"symbol":"ethbtc",		"eventType":"trade"	}}
```

After order matching –

| Field         | Data Type | Description                                                  |
| ------------- | --------- | ------------------------------------------------------------ |
| eventType     | string    | Event type, valid value: trade                               |
| symbol        | string    | Trading symbol                                               |
| tradePrice    | string    | Trade price                                                  |
| tradeVolume   | string    | Trade volume                                                 |
| orderId       | long      | Order ID                                                     |
| type          | string    | Order type, valid value: buy-market, sell-market, buy-limit, sell-limit |
| clientOrderId | string    | Client order ID (if any)                                     |
| orderSource   | string    | Order source                                                 |
| orderPrice    | string    | Original order price (not available for market order)        |
| orderSize     | string    | Original order amount (not available for buy-market order)   |
| orderValue    | string    | Original order value (only available for buy-market order)   |
| tradeId       | long      | Trade ID                                                     |
| tradeTime     | long      | Trade time                                                   |
| aggressor     | bool      | Aggressor or not, valid value: true (taker), false (maker)   |
| orderStatus   | string    | Order status, valid value: partial-filled, filled            |
| remainAmt     | string    | Remaining amount (for buy-market order it's remaining value) |
| execAmt       | string    | Accumulative amount (for buy-market order it is accumulative value) |

Note:<br>

- If a taker’s order matching with multiple orders at opposite side simultaneously, the multiple trades will be disseminated over separately instead of merging into one trade.<br>

```json
{	"action":"push",	"ch":"orders#ethbtc",	"data":	{		"lastActTime":1583853475406,		"remainAmt":"2.000000000000000000",		"execAmt":"2",		"orderId":27163533,		"type":"sell-limit",		"clientOrderId":"abc123",		"orderSource":"spot-api",		"orderPrice":"15000",		"orderSize":"0.01",		"orderStatus":"canceled",		"symbol":"ethbtc",		"eventType":"cancellation"	}}
```

After order cancellation –

| Field         | Data Type | Description                                                  |
| ------------- | --------- | ------------------------------------------------------------ |
| eventType     | string    | Event type, valid value: cancellation                        |
| symbol        | string    | Trading symbol                                               |
| orderId       | long      | Order ID                                                     |
| type          | string    | Order type, valid value: buy-market, sell-market, buy-limit, sell-limit |
| clientOrderId | string    | Client order ID (if any)                                     |
| orderSource   | string    | Order source                                                 |
| orderPrice    | string    | Original order price (not available for market order)        |
| orderSize     | string    | Original order amount (not available for buy-market order)   |
| orderValue    | string    | Original order value (only available for buy-market order)   |
| orderStatus   | string    | Order status, valid value: partial-canceled, canceled        |
| remainAmt     | string    | Remaining amount	(for buy-market order it's remaining value) |
| execAmt       | string    | Accumulative amount (for buy-market order it is accumulative value) |
| lastActTime   | long      | Last activity time                                           |



## Subscribe Trade Details & Order Cancellation post Clearing

API Key Permission: Read

Only update when order is in transaction or cancellation. Order transaction update is in tick by tick mode, which means, if a taker’s order matches with multiple maker’s orders, the simultaneous multiple trades will be disseminated one by one. But the update sequence of the multiple trades, may not be exactly the same as the sequence of the transactions made. Also, if an order is auto cancelled immediately just after its partial fills, for example a typical IOC order, this channel would possibly disseminate the cancellation update first prior to the trade. <br>

If user willing to receive order updates in exact same sequence with the original happening, it is recommended to subscribe order update channel orders#${symbol}.<br>

### Topic

`trade.clearing#${symbol}#${mode}`

### Subscription Field

| Field  | Data Type | Description                                                  |
| ------ | --------- | ------------------------------------------------------------ |
| symbol | string    | Trading symbol (wildcard * is allowed)                       |
| mode   | int       | Subscription mode (0 – subscribe only trade event; 1 – subscribe both trade and cancellation events; default value: 0) |

Note:<br>
About optional field ‘mode’: If not filled, or filled with 0, it implicates to subscribe trade event only. If filled with 1, it implicates to subscribe both trade and cancellation events.<br>


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
{    "ch": "trade.clearing#ltcbtc#0",    "data": {         "eventType": "trade",         "symbol": "ltcbtc",         "orderId": 99998888,         "tradePrice": "9999.99",         "tradeVolume": "0.96",         "orderSide": "buy",         "aggressor": true,         "tradeId": 919219323232,         "tradeTime": 998787897878,         "transactFee": "19.88",         "feeDeduct ": "0",         "feeDeductType": "",         "feeCurrency": "btc",         "accountId": 9912791,         "source": "spot-api",         "orderPrice": "10000",         "orderSize": "1",         "clientOrderId": "a001",         "orderCreateTime": 998787897878,         "orderStatus": "partial-filled"    }}
```

### Update Contents (after order matching)

| Field           | Data Type | Description                                                  |
| --------------- | --------- | ------------------------------------------------------------ |
| eventType       | string    | Event type (trade)                                           |
| symbol          | string    | Trading symbol                                               |
| orderId         | long      | Order ID                                                     |
| tradePrice      | string    | Trade price                                                  |
| tradeVolume     | string    | Trade volume                                                 |
| orderSide       | string    | Order side, valid value: buy, sell                           |
| orderType       | string    | Order type, valid value:  buy-market, sell-market,buy-limit  |
| aggressor       | bool      | Aggressor or not, valid value: true, false                   |
| tradeId         | long      | Trade ID                                                     |
| tradeTime       | long      | Trade time, unix time in millisecond                         |
| transactFee     | string    | Transaction fee (positive value) or Transaction rebate (negative value) |
| feeCurrency     | string    | Currency of transaction fee or transaction fee rebate (transaction fee of buy order is based on base currency, transaction fee of sell order is based on quote currency; transaction fee rebate of buy order is based on quote currency, transaction fee rebate of sell order is based on base currency) |
| feeDeduct       | string    | Transaction fee deduction                                    |
| feeDeductType   | string    | Transaction fee deduction type, valid value: ht, point       |
| accountId       | long      | Account ID                                                   |
| source          | string    | Order source                                                 |
| orderPrice      | string    | Order price (invalid for market order)                       |
| orderSize       | string    | Order size (invalid for market buy order)                    |
| orderValue      | string    | Order value (only valid for market buy order)                |
| clientOrderId   | string    | Client order ID                                              |
| stopPrice       | string    | Stop price (only valid for stop limit order)                 |
| operator        | string    | Operation character (only valid for stop limit order)        |
| orderCreateTime | long      | Order creation time                                          |
| orderStatus     | string    | Order status, valid value: filled, partial-filled            |

Notes:<br>

- The calculated maker rebate value inside ‘transactFee’ may not be paid immediately.<br>

### Update Contents (after order cancellation)

| Field           | Data Type | Description                                                  |
| --------------- | --------- | ------------------------------------------------------------ |
| eventType       | string    | Event type (cancellation)                                    |
| symbol          | string    | Trading symbol                                               |
| orderId         | long      | Order ID                                                     |
| orderSide       | string    | Order side, valid value: buy, sell                           |
| orderType       | string    | Order type, valid value: buy-market, sell-market,buy-limit,sell-limit |
| accountId       | long      | Account ID                                                   |
| source          | string    | Order source                                                 |
| orderPrice      | string    | Order price (invalid for market order)                       |
| orderSize       | string    | Order size (invalid for market buy order)                    |
| orderValue      | string    | Order value (only valid for market buy order)                |
| clientOrderId   | string    | Client order ID                                              |
| stopPrice       | string    | Stop price (only valid for stop limit order)                 |
| operator        | string    | Operation character (only valid for stop limit order)        |
| orderCreateTime | long      | Order creation time                                          |
| remainAmt       | string    | Remaining order amount (if market buy order, it implicates remaining order value) |
| orderStatus     | string    | Order status, valid value: canceled, partial-canceled        |

## Subscribe Account Change

API Key Permission: Read

The topic updates account change details.

### Topic

`accounts.update#${mode}`

Upon subscription field value specified, the update can be triggered by either of following events:

1、Whenever account balance is changed.

2、Whenever account balance or available balance is changed. (Update separately.)

3、Whenever  account balance or available balance changed, it will be updated together.

Note that right now there is no account update when transferring between spot account and other accounts.

### Subscription Field

| Field | Data Type | Description                                       |
| ----- | --------- | ------------------------------------------------- |
| mode  | integer   | Trigger mode, valid value: 0, 1, default value: 0 |

Samples 

1、Not specifying "mode":  
accounts.update  
Only update when account balance changed;  

2、Specify "mode" as 0:  
accounts.update#0  
Only update when account balance changed;  

3、Specify "mode" as 1:  
accounts.update#1  
Update when either account balance changed or available balance changed.  

4、Specify "mode" as 2:  
accounts.update#2  
Whenever account balance or available balance changed, it will be updated together.

Note:
The topic disseminates the current static value of individual accounts first, at the beginning of subscription, followed by account change updates. While disseminating the current static value of individual accounts, inside the message, field value of "changeType" and "changeTime" is null.

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

### Update Contents

| Field       | Data Type | Description                                                  |
| ----------- | --------- | ------------------------------------------------------------ |
| currency    | string    | Currency                                                     |
| accountId   | long      | Account ID                                                   |
| balance     | string    | Account balance (only exists when account balance changed)   |
| available   | string    | Available balance (only exists when available balance changed) |
| changeType  | string    | Change type, valid value: order-place，order-match，order-refund，order-cancel，deposit , withdraw，other |
| accountType | string    | account type, valid value: trade, loan, interest             |
| changeTime  | long      | Change time, unix time in millisecond                        |

Note:<br>

- A maker rebate would be paid in batch mode for multiple trades.<br>


## Error Code

Below is the return code, return message and the description returend from Asset and Order WebSocket

| Return Code | Return Message           | Description                                                  |
| ----------- | ------------------------ | ------------------------------------------------------------ |
| 200         | Success                  | Successful                                                   |
| 100         | time out close           | The connection is timeout and closed                         |
| 400         | Bad Request              | The request is invalid                                       |
| 404         | Not Found                | The service is not found                                     |
| 429         | Too Many Requests        | Connection number exceed limit                               |
| 500         | system error             | System internal error                                        |
| 2000        | invalid.ip               | The IP is invalid                                            |
| 2001        | nvalid.json              | The JSON request is invalid                                  |
| 2001        | invalid.action           | Parameter action is invalid                                  |
| 2001        | invalid.symbol           | Parameter symbol is invalid                                  |
| 2001        | invalid.ch               | Parameter channel is invalid                                 |
| 2001        | missing.param.auth       | Parameter auth is missing                                    |
| 2002        | invalid.auth.state       | Authentication state is invalid                              |
| 2002        | auth.fail                | Authentication failed, including wrong IP address binding in API Key |
| 2003        | query.account.list.error | Account query error                                          |
| 4000        | too.many.request         | Request exceed limit (a single instance limit to 50 per second) |
| 4000        | too.many.connection      | Connection number exceed limit for single API Key (a single instance limit to 10 connections) |

