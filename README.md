# Introduction

This article is the official document of the programmatic trading interface API provided by the CHAIN STAR TECHNOLOGY . We hope that through the document, the developers can implement the functions of the platform by themselves such as API application, verification, calling, debugging to realize programmatic trading on the platform of CHAIN STAR TECHNOLOGY.

# Platform Url
* platform Url:https://www.chaoex.info

# Base Url
* baseUrl:https://www.chaoex.info/unique/

* Other platforms need request with an E-mail and open an interface before developing a programmatic interface API.

# Query

Developers can obtain information such as currency transaction pairs, real-time quotes, transaction depth, and transaction history through the query interface. Currently, the query function does not require login authentication and pass the token. If the request pressure of the query increases, you may consider adding the token and limiting the number of daily queries.

## Currency transaction pairs obtainment

* request_url：baseUrl + coin/allCurrencyRelations
* method：GET
* parameter：null
* response_data:

item|description|type
--------|--------|--------
id|number|int
baseCurrencyId|Base currency id|int
baseCurrencyName|Base currency name|string
baseCurrencyNameEn|Base currency English name|string
tradeCurrencyId|Trade currency id|int
tradeCurrencyName|Trade currency name|string
tradeCurrencyNameEn|Trade currency English name |string
amountLowLimit|Minimum purchase limit|decimal
amountHighLimit|Maximum purchase limit|decimal
sellAmountLowLimit|Minimum sell limit|decimal
sellAmountHighLimit|Maximum sell limit|decimal

* response description：When the status interface returns is 200, the attachment contains the following data. If the status parameter is not 200, an abnormity occurs.
* example：

```json
{
    "attachment": [
    {
    "id": 1,
    "baseCurrencyId": "1",
        "tradeCurrencyId": "2",
        "baseCurrencyName": "Bitcoin",
        "baseCurrencyNameEn": "BTC",
        "tradeCurrencyName": "Litecoin",
        "tradeCurrencyNameEn": "LTC",
        "amountLowLimit": 0.0,
        "amountHighLimit": 9999999.0,
        "sellAmountLowLimit": 0.0,
        "sellAmountHighLimit": 9999999.0
    },
    {
    "id": 2,
    "baseCurrencyId": "1",
        "tradeCurrencyId": "3",
        "baseCurrencyName": "Bitcoin",
        "baseCurrencyNameEn": "BTC",
        "tradeCurrencyName": "Ethereum",
        "tradeCurrencyNameEn": "ETH",
        "amountLowLimit": 0.01,
        "amountHighLimit": 999999.0,
        "sellAmountLowLimit": 0.01,
        "sellAmountHighLimit": 999999.0
    },
    {
    "id": 5,
    "baseCurrencyId": "1",
        "tradeCurrencyId": "6",
        "baseCurrencyName": "Bitcoin",
        "baseCurrencyNameEn": "BTC",
        "tradeCurrencyName": "Lisk",
        "tradeCurrencyNameEn": "LSK",
        "amountLowLimit": 1.0E-4,
        "amountHighLimit": 999999.0,
        "sellAmountLowLimit": 1.0E-4,
        "sellAmountHighLimit": 999999.0
    }
],
"status": 200,
"message": null
}
```

## Obtain real-time quotes (First edition to be abandoned)

* request_url：baseUrl + quote/realTime
* method：GET
* parameter：

item|description|type
--------|--------|--------
baseCurrencyId|Base currency id|string
tradeCurrencyId|Trade currency id|string

* response_data:

item|description|type
--------|--------|--------
buy| Price for one buy|int
high|Highest price|decimal
last|Latest transaction price|decimal
low|Lowest price|decimal
sell|Price for one sell|decimal
vol|Trade currency volume|decimal
currencyId|Trade currency id|int
baseCurrencyId|Base currency id|int

* response description：When the status interface returns is 200, the attachment contains the following data. If the status parameter is not 200, an abnormity occurs.
* example：

```json
{
    "attachment": {
    "buy": 0.0174565,
    "high": 0.01805645,
    "last": 0.0174565,
    "low": 0.01646356,
    "sell": 0.0174565,
    "vol": 391.896,
    "currencyId": 2,
    "baseCurrencyId": 1
    },
    "message": "",
    "status": 200
}

```

## Obtain real-time quotes (Second Edition)

- request_url：baseUrl + quote/v2/realTime
- method：GET
- parameter：

|Item      |description  |type   |
| -------- | :-----:|  :-------:  |
|coins|	(base currency English name+ '_' + trading currency English name)，Letters don’t need to be capitalized. example:code_chex|	string|

- response_data:

|Item      |description  |type   |
| -------- | :-----:|  :-------:  |
|buy	|Price for one buy|	decimal|
|high	|Highest price|	decimal|
|last	|Latest transaction price|	decimal|
|low	|Lowest price|	decimal|
|sell	|Price for one sell|	decimal|
|vol	|Trade currency volume|	decimal|
|currencyId|	Trading currency id|	int|
|baseCurrencyId|	Base currency id	|int|
|changeRate|	Ups and downs rate (up to positive, down to negative)|	decimal|
|changeAmount|	Ups and downs amount (up to positive, down to negative)|	decimal|

- response description：When the status interface returns is 200, the attachment contains the following data. If the status parameter is not 200, an abnormity occurs.
- example：

```
{
    "attachment": {
    "buy": 0.2721,
    "high": 0.2815,
    "last": 0.2765,
    "low": 0.2669,
    "sell": 0.2815,
    "vol": 1.2449481758E8,
    "currencyId": 70,
    "baseCurrencyId": 22,
    "changeRate": 0.47,
    "changeAmount": 0.0013,
    },
    "message": null,
    "status": 200
}
```

## Obtain all real-time quotes

- request_url：baseUrl + quote/v2/allRealTime
- method：GET
- parameter：null

- response_data:

|Item      |description  |type   |
| -------- | :-----:|  :-------:  |
|buy	|Price for one buy|	decimal|
|high	|Highest price|	decimal|
|last	|Latest transaction price|	decimal|
|low	|Lowest price|	decimal|
|sell	|Price for one sell|	decimal|
|vol	|Trade currency volume|	decimal|
|currencyId|	Trading currency id|	int|
|baseCurrencyId|	Base currency id	|int|
|tradeCurrencyName|	Trading currency name|	string|
|baseCurrencyName|	Base currency name	|string|
|changeRate|	Ups and downs rate (up to positive, down to negative)|	decimal|
|changeAmount|	Ups and downs amount (up to positive, down to negative)|	decimal|



- response description：当接口返回的status 为200时，则attachment包含以下数据，如果status参数不为200 ，则出现异常。
- example：

```
{
    {
	  "attachment": [
	    {
	      "buy": 0.008025,
	      "high": 0.0,
	      "last": 0.008025,
	      "low": 0.0,
	      "sell": null,
	      "vol": 0.0,
	      "currencyId": 2,
	      "baseCurrencyId": 1,
	      "tradeCurrencyName": "LTC",
	      "baseCurrencyName": "BTC",
	      "changeRate": 0.0,
	      "changeAmount": 0.0,
	      "rmbScale": 0.0
	    },
	    {
	      "buy": 0.0278,
	      "high": 0.0,
	      "last": 0.028,
	      "low": 0.0,
	      "sell": 0.028,
	      "vol": 0.0,
	      "currencyId": 3,
	      "baseCurrencyId": 1,
	      "tradeCurrencyName": "ETH",
	      "baseCurrencyName": "BTC",
	      "changeRate": 0.0,
	      "changeAmount": 0.0,
	      "rmbScale": 0.0
	    }
    ],
    "message": null,
    "status": 200
}
```

## Obtain transaction depth

* request_url：baseUrl + quote/tradeDeepin
* method：GET
* parameter：

item|description|type
--------|--------|--------
baseCurrencyId|Base currency id|string
tradeCurrencyId|Trading currency id|string
limit|obtained depth level|int

* response_data:

item|description|type
--------|--------|--------
asks|Seller delegate order array|Array
bids|Buyer delegate order array|Array

>Note: the first element of each array object is the price, and the second element is the quantity.

* response description：When the status interface returns is 200, the attachment contains the following data. If the status parameter is not 200, an abnormity occurs.
* example：

```json
{
    "attachment": {
    "asks": [
            [
                "0.01751456",
                "0.0071000000000000"
            ]
        ],
    "bids": [
            [
                "0.01745650",
                "0.0109000000000000"
            ]
        ]
    },
    "message": "",
    "status": 200
}
```

## Obtain transaction history

* request_url：baseUrl + quote/tradeHistory
* method：GET
* parameter：

item|description|type
--------|--------|--------
baseCurrencyId|Base currency id|string
tradeCurrencyId|Trade currency id|string
limit|Obtained depth level|int

* response_data:

item|description|type
--------|--------|--------
date|Transaction time|string
price|Transaction price|decimal
amount|Transaction amount|decimal
number|Transaction number|decimal
coinCode|Trade currency id|int
baseCurrencyId|Base currency id|int
tid|Order number|string
type|Transaction type，value is buy，or sell|string
buyOrSellTrade|Transaction type id，1 is to buy，2 is to sell|int

* response description：When the status interface returns is 200, the attachment contains the following data. If the status parameter is not 200, an abnormity occurs.
* example：

```json
{
    "attachment": [
        {
    "date": "1524561232806",
    "price": 0.0174565,
    "amount": 0.00002618,
    "number": 0.0015,
    "coinCode": 2,
    "baseCurrencyId": 1,
    "tid": "15245612328058682391221000295251",
    "type": "sell",
    "buyOrSellTrade": 2
        }
    ],
    "message": "",
    "status": 200
}
```

# Access Request

## Request with E-mail

E-mail request format:

item|description|
--------|--------
Company name/Individual name|Company application, please write the full name of the company, personal application, please write the full name of the individual
TEL|Cell phone number
Company Business License Number/Personal ID Number|Company Business License Number/Personal ID Number
Platform account|Corresponding platform account
public-key|Your public key will be saved on the platform.The following will detail the generation and the use of the public key

>Note: Due to some force majeure factors, the application for API permissions for login, ordering, and withdrawal of orders cannot be provided by a separate page. Therefore, the application of the API call permission is currently supported by the method of mail application.

### Crypto signature

1.Please generate your own KeyPair (public/private key) according to **RSA**
```
openssl
genrsa -out rsa_private_key.pem 1024
rsa -in rsa_private_key.pem -pubout -out rsa_public_key.pem

//generate
rsa_private_key.pem
rsa_public_key.pem
```

2.Then, send your public-key (that is, rsa_public_key.pem), username, and user uid to business-en@chaoex.com.hk to apply.
3.Each time you apply for API permissions such as login, Delegation order, and Delegation withdrawal, please use the sha256 algorithm and sign the parameters with the private key. I give a Javascript implementation here. 
4.timestamp is the latest time

```javascript

//timestamp format：2018-05-02T18:30:00Z

const signature = crypto.createSign('sha256');
signature.write(timestamp.toString());
signature.end();

console.log(signature.sign(APISECRET, 'hex'));

//signature format：
739deeac15a533508d679c6bc7f67d29e92fce7f05359a500abd8fd9844134d97d60e76495850ba392694dd8a50fc6202d8b004f9b9d61422ae698d2e9fc07aeaf29feb02e0019dfa6f30fd2de03be8f2e4cf5c8442d1b56b560427dd1637934750e5c071e8c9928fa81bfb7de83001e0e70b2c774be4bf43fdaa5e932849c9e
```


>When logging in, obtain the token with the user/password/signature. When using the functions of ordering, withdrawing, and orders query, the token is directly used.


# Log in

The developer obtains the platform token through the login interface. Only after obtaining the platform token can the functions such as order placement and order withdrawal be operated.

## Description

* request_url：baseUrl + user/signLogin
* method：POST
* Content-Type:application/x-www-form-urlencoded
* Accept:application/json, text/plain, */*
* parameter：

item|description|type
--------|--------|--------
email|Platform login name|string
pwd|Platform login password|string
timestamp|Timestamp with the timeZone GMT+8 format like this '2018-11-26T22:16:50Z'|string
sign|Signature|string

## Front-end password encryption rules

```javascript
const salt = 'dig?F*ckDang5PaSsWOrd&%(12lian0160630).'
let pwd = md5(pwd + salt)
```

* response_data:

The return value is in data.attachment, where the values required by the developer are:

item|description|type
--------|--------|--------
token|Operate request token|string
uid|User id|int
uname|User name，currently empty.|string
isShow|Whether to show advanced options, 0 is no, 1 is yes|int

* response description：When the status interface returns is 200, the attachment contains the following data. If the status parameter is not 200, an abnormity occurs.

```json
{
    "attachment": {
        "uid": ****,
        "token": "************************",
        "point": null,
        "uname": null,
        "isShow": 0
    },
    "message": null,
    "status": 200
}
```


# Delegation order

By calling this interface, the platform's generate order function can be used, which can generate limit buy orders and limit sell orders.

## Description

* request_url：baseUrl + order/order
* method：POST
* Content-Type:application/x-www-form-urlencoded
* Accept:application/json, text/plain, */*
* parameter：

item|description|type
--------|--------|--------
buyOrSell|Buying and selling direction, 1 is buy, 2 is sell|int
currencyId|Trade currency id|int
baseCurrencyId|Base currency id|int
fdPassword|Transaction password, can be empty.|string
num|number，Keep up to 8 decimal places after the decimal point|decimal
price|Price, Keep up to 8 decimal places after the decimal point|decimal
source|Programmatic transaction docking type, which is currently 5|int
type|transaction docking type, which is currently 1|int
token|Request authentication, if the token expires, re-acquirement is needed.|string
uid|User id|int
local|languages，Chinese traditional, zh_TW、en_US are selectable.|string
timestamp|timestamp|string

* response description：When the status interface returns is 200, the attachment contains the following data. If the status parameter is not 200, an abnormity occurs.

* response_data:

item|description|type
--------|--------|--------
attachment|Order Number|string

```json
{
    "attachment": "15247205636080030010341100261823"
    , "message": ""
    , "status": 200
}
```


# Delegation withdrawal

By calling this interface, the platform's revocation order function can be used.

## Description

* request_url：baseUrl + order/cancel
* method：POST
* Content-Type:application/x-www-form-urlencoded
* Accept:application/json, text/plain, */*
* parameter：

item|description|type
--------|--------|--------
currencyId|Base currency id|int
orderNo|Delegation order number|string
fdPassword|Transaction password|string
source|Programmatic transaction docking type, which is currently 1|int
token|Request authentication, if the token expires, re-acquirement is needed.|string
uid|User id|int
local|languanges，Chinese traditional, zh_TW、en_US are selectable.|string
timestamp|timestamp|string

* response description：When the status interface returns is 200, the attachment contains the following data. If the status parameter is not 200, an abnormity occurs.

* response_data:

```json
{
    "attachment":200
    ,"message":""
    ,"status":200
}
```

# Account assets query

Account assets query provided by the platform.

## Description

* request_url：baseUrl + coin/customerCoinAccount
* method：POST
* Content-Type:application/x-www-form-urlencoded
* Accept:application/json, text/plain, */*
* parameter：

item|description|type
--------|--------|--------
token|Request authentication, if the token expires, re-acquirement is needed.|string
uid|User id|int
local|languanges，Chinese traditional, zh_TW、en_US are selectable.|string
timestamp|timestamp|string

* response description：When the status interface returns is 200, the attachment contains the following data. If the status parameter is not 200, an abnormity occurs.

* response_data:

item|description|type
--------|--------|--------
allMoney|Total amount of assets|decimal
coinList|User personal position details|object

coinList content

item|description|type
--------|--------|--------
amount|Position amount|decimal
baseCurrencyId|Base currency id|int
btc_value|How much BTC|int
cashAmount|Cash value|decimal
currencyId|Trade currency id|int
currencyName|Digital currency full name|string
currencyNameEn|Digital currency abbreviation|string
freezeAmount|Amount of freezes|decimal
icoUrl|Currency thumbnail|string

```json
{
	"attachment": {
		"allMoney": 11.0,
		"takeBtcMax": 2.0,
		"takeBtcNum": 0.0,
		"coinList": [{
			"currencyNameEn": "LTC",
			"amount": "100.00000000",
			"freezeAmount": "0.00000000",
			"currencyName": "Litecoin",
			"cashAmount": "100.00000000",
			"icoUrl": "bestex/ltc.png",
			"baseCurrencyId": 2,
			"currencyId": 2,
			"btc_value": 10.0
		}, {
			"currencyNameEn": "BTC",
			"amount": "1.00000000",
			"freezeAmount": "0.00000000",
			"currencyName": "BitCoin",
			"cashAmount": "1.00000000",
			"icoUrl": "bestex/btc.png",
			"baseCurrencyId": 1,
			"currencyId": 1,
			"btc_value": 1.0
		}, {
			"currencyNameEn": "ETH",
			"amount": "0.00000000",
			"freezeAmount": "0.00000000",
			"currencyName": "Ethereum",
			"cashAmount": "0.00000000",
			"icoUrl": "bestex/eth.png",
			"baseCurrencyId": 3,
			"currencyId": 3,
			"btc_value": 0.0
		}, {
			"currencyNameEn": "BCH",
			"amount": "0.00000000",
			"freezeAmount": "0.00000000",
			"currencyName": "Bitcoin Cash",
			"cashAmount": "0.00000000",
			"icoUrl": "bestex/bch.png",
			"baseCurrencyId": 14,
			"currencyId": 14,
			"btc_value": 0.0
		}, {
			"currencyNameEn": "ETC",
			"amount": "0.00000000",
			"freezeAmount": "0.00000000",
			"currencyName": "Ethereum Classic",
			"cashAmount": "0.00000000",
			"icoUrl": "coinimg/etc.png",
			"baseCurrencyId": 15,
			"currencyId": 15,
			"btc_value": 0.0
		}, {
			"currencyNameEn": "BEB",
			"amount": "0.00000000",
			"freezeAmount": "0.00000000",
			"currencyName": "Be best",
			"cashAmount": "0.00000000",
			"icoUrl": "bestex/beb.png",
			"baseCurrencyId": 23,
			"currencyId": 23,
			"btc_value": 0.0
		}]
	},
	"message": null,
	"status": 200
}
```

# User delegation order query

Through this interface, you can query the user's historical delegation information.

## Description

* request_url：baseUrl + user/trOrderListByCustomer
* method：POST
* Content-Type:application/x-www-form-urlencoded
* Accept:application/json, text/plain, */*
* parameter：

item|description|type
--------|--------|--------
beginTime|Query start date，format：2018-04-25|string
endTime|Query end date，format：2018-04-26|string
start|The starting point of the query, the default is 1, the maximum is 999|int
size|Query amount|int
status|Order status, created and not dealed = 0, partial dealed = 1, all dealed = 2, withdrawal(including orders all cancled and cancled after partial dealed) = 4, all status = 10, active orders(including order status 0 and status 1) = 11, deafault value is 10|int
buyOrSell|Buying and selling direction, 0 is all directions, 1 is to buy, 2 is to sell|int
currencyId|Trade currency id|int
baseCurrencyId|Base currency id|int
priceType|Price type, default is 0, indicating that 0 decimal places are reserved|
token|Request authentication, if the token expires, re-acquirement is needed.|string
uid|User id|int
local|languanges，Chinese traditional, zh_TW、en_US are selectable.|string
timestamp|timestamp|string

* response description：When the status interface returns is 200, the attachment contains the following data. If the status parameter is not 200, an abnormity occurs.

* response_data:

item|description|type
--------|--------|--------
total|Query item number|int
list|Query content|object

list content

item|description|type
--------|--------|--------
averagePrice|average delegation amount|decimal
baseCurrencyId|Base currency id|int
baseCurrencyName|Base currency name|string
baseCurrencyNameEn|Base currency abbrievation|string
buyOrSell|Buying and selling direction, 0 is all directions, 1 is to buy, 2 is to sell|int
currencyName|Digital currency full name|string
currencyNameEn|Digital currency abbreviation|string
dealAmount|Dealed transaction amount|decimal
fee|Trading fee|decimal
num|Delegation number|decimal
orderNo|Delegation order number|string
orderTime|Delegation time|string
price|Delegation price|decimal
remainNum|Remaining number|decimal
status|Order status, unfilled = 0, partial transaction = 1, all transactions = 2, withdrawal = 4, All states = 10|int
tradeNum|Transaction number|decimal

```json
{
    "attachment": {
        "total": 5,
        "list": [
            {
                "currencyNameEn": "LTC",
                "remainNum": "0.00000000",
                "orderNo": "15247224350040050010351100223505",
                "dealAmount": "0.00000000",
                "fee": "0.00000000",
                "num": "0.01000000",
                "tradeNum": "0.00000000",
                "baseCurrencyId": 1,
                "baseCurrencyName": "BitCoin",
                "baseCurrencyNameEn": "BTC",
                "buyOrSell": 1,
                "orderTime": "2018-04-26 14:00:35",
                "currencyName": "Litecoin",
                "price": "10.00000000",
                "averagePrice": "0.00000000",
                "status": 4
            },
            {
                "currencyNameEn": "LTC",
                "remainNum": "0.00000000",
                "orderNo": "15247207813130040010351100299823",
                "dealAmount": "0.00000000",
                "fee": "0.00000000",
                "num": "0.01000000",
                "tradeNum": "0.00000000",
                "baseCurrencyId": 1,
                "baseCurrencyName": "BitCoin",
                "baseCurrencyNameEn": "BTC",
                "buyOrSell": 1,
                "orderTime": "2018-04-26 13:33:01",
                "currencyName": "Litecoin",
                "price": "10.00000000",
                "averagePrice": "0.00000000",
                "status": 4
            },
            {
                "currencyNameEn": "LTC",
                "remainNum": "0.00000000",
                "orderNo": "15247205636080030010341100261823",
                "dealAmount": "0.00000000",
                "fee": "0.00000000",
                "num": "0.01000000",
                "tradeNum": "0.00000000",
                "baseCurrencyId": 1,
                "baseCurrencyName": "BitCoin",
                "baseCurrencyNameEn": "BTC",
                "buyOrSell": 1,
                "orderTime": "2018-04-26 13:29:23",
                "currencyName": "Litecoin",
                "price": "1.00000000",
                "averagePrice": "0.00000000",
                "status": 4
            },
            {
                "currencyNameEn": "LTC",
                "remainNum": "0.00000000",
                "orderNo": "15247205330170020010341100292977",
                "dealAmount": "0.00000000",
                "fee": "0.00000000",
                "num": "0.01000000",
                "tradeNum": "0.00000000",
                "baseCurrencyId": 1,
                "baseCurrencyName": "BitCoin",
                "baseCurrencyNameEn": "BTC",
                "buyOrSell": 1,
                "orderTime": "2018-04-26 13:28:53",
                "currencyName": "Litecoin",
                "price": "1.00000000",
                "averagePrice": "0.00000000",
                "status": 4
            },
            {
                "currencyNameEn": "LTC",
                "remainNum": "0.00000000",
                "orderNo": "15247205167340010010381100231945",
                "dealAmount": "0.00000000",
                "fee": "0.00000000",
                "num": "1.00000000",
                "tradeNum": "0.00000000",
                "baseCurrencyId": 1,
                "baseCurrencyName": "BitCoin",
                "baseCurrencyNameEn": "BTC",
                "buyOrSell": 2,
                "orderTime": "2018-04-26 13:28:36",
                "currencyName": "Litecoin",
                "price": "1.00000000",
                "averagePrice": "0.00000000",
                "status": 4
            }
        ]
    },
    "message": null,
    "status": 200
}
```
