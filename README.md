# Python SDK for Stocknote API
Official Python SDK for accessing Stocknote API

The official Python library for communicating with the Stocknote APIs.

Stocknote API Python library provides a wrapper over the HTTPs APIs.

The HTTP calls have been converted to methods and JSON responses are wrapped into Python-compatible objects.

Websocket connections are handled automatically with the library

## Installation

This module is installed via pip:

```
pip install StocknotePythonSDK
```


### Prerequisites

Python 2.x or 3.x

Also, you need the following modules:

* `future`
* `requests`
* `websocket`
* `websocket_client`

The modules can also be installed using `pip`

## Getting started with API

### Overview
There is a StocknoteAPIPythonBridge class in the library: create a object for StocknoteAPIPythonBridge with an instance and from this class you can create a Session token using Login function.The StockNote APIs allow the user authentication using the session token from Login API. A valid StockNote Trading Account and subscription to StockNote API Services is a pre-requisite for successful authentication.
 

### REST Documentation
The original REST API that this SDK is based on is available online.
   [Stocknote API REST documentation](https://developers.stocknote.com/api/?python#stocknote-api-documentation)

## Using the API

### Get an session token
1. Import StocknoteAPIPythonBridge
```
from snapi_py_client.snapi_bridge
```

2. Create a StocknoteAPIPythonBridge object
```python
samco=StocknoteAPIPythonBridge()
```
3. Get the login function so you can login with your Stocknote APi by providing below parameters.

## Parameters:
    userId, password, yob
## Login Sample Request:
  ```python
  print(samco.login(body={"userId":'*****','password':'*****','yob':'****'}))
  ##this will return a user details and generated session token
  ```
 ## Login Response:
 ```python
 {
  "serverTime": "16/06/20 12:36:52",
  "msgId": "580d405d-663e-49e4-9a5d-26d439bc8390",
  "status": "Success",
  "statusMessage": "Login session token generated successfully ",
  "sessionToken": "cbcc85c02d057187a4c6512ae0978946",
  "accountID": "client_id",
  "accountName": "client_name",
  "exchangeList": [
    "BSE",
    "NSE"
  ],
  "orderTypeList": [
    "L",
    "MKT",
    "SL"
  ],
  "productList": [
    "CNC",
    "CO",
    "MIS"
  ]
}
```
4. Get the session token form login response and set it to `set_session_token` function.
```python
samco.set_session_token(sessionToken="cbcc85c02d057187a4c6512ae0978946")
## this function will help to reduce to pass session token for other apis. This will automate the session token for other apis
```
### Search Equity & Derivative:
To search equity, derivatives and commodity scrips based on user provided search symbol and exchange name.

#### Parameters:
```python
search_symbol_name,exchange
```
#### sample Search Request:
```python
print(samco.search_equity_derivative(search_symbol_name="BANKNIFTY20JUN",exchange=samco.EXCHANGE_NFO))
```
#### Search Response:
```python
{
 "msgId": "a9080992-71f3-47a9-9b53-b6103f4eb6ba",
  "status": "Success",
  "statusMessage": "Equity Search details retrieved successfully",
  "equityDertivativeValues": [
       {
            "tradingSymbol": "BANKNIFTY20JUN21000CE",
            "instrument": "OPTIDX",
            "exchange": "NFO"
        },
        {
            "tradingSymbol": "BANKNIFTY20JUN22000CE",
            "instrument": "OPTIDX",
            "exchange": "NFO"
        },
        {
            "tradingSymbol": "BANKNIFTY20JUN20500CE",
            "instrument": "OPTIDX",
            "exchange": "NFO"
        },
        {
            "tradingSymbol": "BANKNIFTY20JUN20000CE",
            "instrument": "OPTIDX",
            "exchange": "NFO"
        },
        {
            "tradingSymbol": "BANKNIFTY20JUN19000PE",
            "instrument": "OPTIDX",
            "exchange": "NFO"
        },
        {
            "tradingSymbol": "BANKNIFTY20JUN20000PE",
            "instrument": "OPTIDX",
            "exchange": "NFO"
        },
        {
            "tradingSymbol": "BANKNIFTY20JUN21500CE",
            "instrument": "OPTIDX",
            "exchange": "NFO"
        },
        {
            "tradingSymbol": "BANKNIFTY20JUN19500PE",
            "instrument": "OPTIDX",
            "exchange": "NFO"
        }
    ]
}
```
### Quote:
Get market depth details for a specific equity scrip including but not limited to values like last trade price, previous close price, change value, change percentage, bids/asks, upper and lower circuit limits etc. This helps user with market picture of an equity scrip using which he will be able to place an order.

#### Parameters:
```python
symbol_name,exchange
```
#### Sample Quote request:
```python
print(samco.get_quote(symbol_name='BANKNIFTY18JUN2017900PE',exchange=samco.EXCHANGE_NFO))
```
#### Quote Response:
```python
{
    "serverTime": "16/06/20 14:06:12",
    "msgId": "b6322a42-1e3f-4706-af6d-6e88c32a5ee5",
    "status": "Success",
    "statusMessage": "Quote details retrieved successfully",
    "tradingSymbol": "BANKNIFTY18JUN2017900PE",
    "exchange": "NFO",
    "lastTradedTime": "16/06/2020 14:08:05",
    "lastTradedPrice": "54.25",
    "changeValue": "19.45",
    "changePercentage": "55.89",
    "lastTradedQuantity": "40",
    "lowerCircuitLimit": "0.05",
    "upperCircuitLimit": "138.95",
    "averagePrice": "37.63",
    "totalBuyQuantity": "85520",
    "totalSellQuantity": "17100",
    "totalTradedValue": "1.57858 (Crs)",
    "totalTradedVolume": "419500",
    "yearlyHighPrice": "0.00",
    "yearlyLowPrice": "0.00",
    "tickSize": "0.05",
    "openInterest": "16880",
    "bestBids": [
        {
            "number": "1",
            "quantity": "20",
            "price": "54.00"
        },
        {
            "number": "2",
            "quantity": "40",
            "price": "53.95"
        },
        {
            "number": "3",
            "quantity": "40",
            "price": "53.85"
        },
        {
            "number": "4",
            "quantity": "40",
            "price": "53.75"
        },
        {
            "number": "5",
            "quantity": "120",
            "price": "53.70"
        }
    ],
    "bestAsks": [
        {
            "number": "1",
            "quantity": "20",
            "price": "54.55"
        },
        {
            "number": "2",
            "quantity": "80",
            "price": "54.60"
        },
        {
            "number": "3",
            "quantity": "40",
            "price": "54.65"
        },
        {
            "number": "4",
            "quantity": "40",
            "price": "54.70"
        },
        {
            "number": "5",
            "quantity": "480",
            "price": "54.75"
        }
    ],
    "expiryDate": "18 Jun 20",
    "spotPrice": "19959.35",
    "instrument": "OPTIDX",
    "lotQuantity": "20",
    "listingId": "41870_NFO",
    "openInterestChange": "8800",
    "oIChangePer": "58.05"
}
```
### OptionChain:
To search OptionChain for equity, derivatives and commodity scrips based on user provided search symbol and exchange name.

#### Parameters:
```python
search_symbol_name,exchange,expiry_date,strike_price,option_type
```
#### Sample OptionChain Request:
```python
print(samco.get_option_chain(search_symbol_name='Reliance',exchange=samco.EXCHANGE_NFO,expiry_date='2020-07-30',strike_price='1961.40',option_type='PE'))
```
#### OptionChain Response:
```python
{
  "serverTime": "16/06/20 14:48:53",
  "msgId": "9922deb8-dcdb-402f-a282-9f8df0b2fdee",
  "status": "Success",
  "statusMessage": "OptionChain details retrived successfully. ",
  "optionChainDetails": [
    {
      "tradingSymbol": "RELIANCE20JUL1961.4PE",
      "exchange": "NFO",
      "symbol": "38914_NFO",
      "strikePrice": "1961.40",
      "expiryDate": "2020-07-30",
      "instrument": "OPTSTK",
      "optionType": "PE",
      "underLyingSymbol": "RELIANCE",
      "spotPrice": "1613.45",
      "lastTradedPrice": "0.00",
      "openInterest": "0",
      "openInterestChange": "0",
      "oichangePer": "0",
      "volume": "0"
    }
  ]
}

```


