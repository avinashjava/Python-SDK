# StockNoteBridge - Python SDK for Stocknote API
Official Python SDK for accessing and integrating Stocknote API

This documentation covers details of the Python bridge / SDK provided by SAMCO, for accessing the [SAMCO Stocknote APIs](https://developers.stocknote.com/api/?python#stocknote-api-documentation).

The primary purpose of this Python Bridge is to help our customers quickly create python based client scripts using our SDK and integrate with StockNote APIs. Our Python Bridge provides a wrapper over the RESTful StockNote APIs where the HTTP calls have been converted to method calls with JSON responses. Websocket connections are handled automatically with the library.

Please refer the below documentation for details on installation, set up and API specific sample code/request-responses to create your own Python client code.

## Installation

This module is installed via pip:

```
pip install stocknotebridge
```
Once done, you can verify if package is appropriately installed using  below command.

```
pip list
```

### Prerequisites

Python 2.x or 3.x setup. You can verify the version installed using

```
python --version
```

You can verify the Pip version installed using
```
pip --version
```
Also, you need the following modules:

* `future`
* `requests`
* `websocket`
* `websocket_client`

These modules can also be installed using `pip`

## Getting started with API

### Overview
Stocknote python SDK is a python client library for easily accessing the stocknote API. It exposes the individual APIs as python method calls and provides an easy-to-use interface for implementing your strategies in Python language. 

For specific details on parameters passed on the request, and details about API response, please refer our [Stocknote API documentation](https://developers.stocknote.com/api/?python#stocknote-api-documentation).

## List of API
* [Login](#login)
* [SearchEquityDerivative](#searchequityderivative)
* [Quote](#quote)
* [OptionChain](#OptionChain)
* [UserLimits](#userLimits)
* [PlaceOrder](#placeOrder)
* [PlaceOrderBO](#placeOrderBO)
* [PlaceOrderCO](#placeOrderCO)
* [ModifyOrder](#modifyOrder)
* [OrderBook](#orderBook)
* [TriggerOrders](#triggerOrders)
* [OrderStatus](#orderStatus)
* [CancelOrder](#cancelOrder)
* [CancelOrderCO](#cancelOrderCO)
* [CancelOrderBO](#cancelOrderBO)
* [TradeBook](#tradeBook)
* [Positons](#positions)
* [PositionConversion](#positionConversion)
* [PositionSquareOff](#positionSquareOff)
* [Holdings](#holdings)
* [IntraDayCandleData](#intraDayCandleData)
* [IndexIntraDayCandleData](#indexIntraDayCandleData)
* [HistoricalCandleData](#historicalCandleData)
* [IndexHistoricalCandleData](#indexHistoricalCandleData)
* [StreamingData](#streamingData)
* [Logout](#logout)


## Using the API

As a first step to access StockNote APIs, you need to import our SDK in your client code and then login to get valid session token.

### Import the Python SDK and get a session token
1. Import StocknoteAPIPythonBridge
```
from snapi_py_client.snapi_bridge import StocknoteAPIPythonBridge
```

2. Create a StocknoteAPIPythonBridge object
```python
samco=StocknoteAPIPythonBridge()
```
3. Login to access Stocknote API by providing below parameters.

<a name="login"/>

## Login

## Parameters:
```
userId,password,yob
```
<details>
  <summary>Login Sample Request</summary>

    login=samco.login(body={"userId":'*****','password':'*****','yob':'****'})
    print("Login details",login)
    ##this will return a user details and generated session token
 </details>

 <details>
  <summary>Login Sample Response</summary>
  
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
</details>

4. Get the session token form login response and set it to `set_session_token()` function.
```python
samco.set_session_token(sessionToken="cbcc85c02d057187a4c6512ae0978946")
## this function will help to reduce to pass session token for other apis. This will automate the session token for other apis
```

<a name="searchequityderivative"/>

## SearchEquityDerivative:

The search function `search_equity_derivative()` should be used to search equity, derivatives and commodity scrips based on user provided search symbol and exchange name. 

#### Parameters:
```python

search_symbol_name,exchange
```
<details>
  <summary>Sample Search Request/Response  for Cash segment</summary>
  
  Request :
  ```python
  samco.search_equity_derivative(search_symbol_name="TC",exchange=samco.EXCHANGE_NSE)
  ```
  Response :  
  ```python
  Search: {
  "msgId": "de6c1332-3d4b-4371-a9d1-b52787c039a9",
  "status": "Success",
  "statusMessage": "Equity Search details retrieved successfully",
  "equityDertivativeValues":[
    {
      "exchange": "NSE",
      "scripDescription": "TATA CONSULTANCY SERV LT",
      "tradingSymbol": "TCS-EQ",
      "isin": "INE467B01029",
      "tickSize": "0.05",
      "bodLotQuantity": "1"
    },
    {
      "exchange": "NSE",
      "scripDescription": "TCI DEVELOPERS LIMITED",
      "tradingSymbol": "TCIDEVELOP-EQ",
      "isin": "INE662L01016",
      "tickSize": "0.05",
      "bodLotQuantity": "1"
    },
    {
      "exchange": "NSE",
      "scripDescription": "TCI EXPRESS LIMITED",
      "tradingSymbol": "TCIEXP-EQ",
      "isin": "INE586V01016",
      "tickSize": "0.05",
      "bodLotQuantity": "1"
    },
    {
      "exchange": "NSE",
      "scripDescription": "TCI FINANCE LTD",
      "tradingSymbol": "TCIFINANCE-EQ",
      "isin": "INE911B01018",
      "tickSize": "0.05",
      "bodLotQuantity": "1"
    },
    {
      "exchange": "NSE",
      "scripDescription": "TCNS CLOTHING CO. LIMITED",
      "tradingSymbol": "TCNSBRANDS-EQ",
      "isin": "INE778U01029",
      "tickSize": "0.05",
      "bodLotQuantity": "1"
    },
    {
      "exchange": "NSE",
      "scripDescription": "TCPL PACKAGING LIMITED",
      "tradingSymbol": "TCPLPACK-EQ",
      "isin": "INE822C01015",
      "tickSize": "0.05",
      "bodLotQuantity": "1"
    },
    {
      "exchange": "NSE",
      "scripDescription": "TRANSPORT CORPN OF INDIA",
      "tradingSymbol": "TCI-EQ",
      "isin": "INE688A01022",
      "tickSize": "0.05",
      "bodLotQuantity": "1"
    }
  ]
}
  ```
</details>

<details>
  <summary>Sample Search Request/Response  for Future & Options segment</summary>

#### Sample Search Request:
```python
    samco.search_equity_derivative(search_symbol_name="BANKNIFTY",exchange=samco.EXCHANGE_NFO)
```
#### Sample Search Response:
```python
   Search: {
  "msgId": "dd84e6ba-29d1-4eb8-a021-c9b896eed795",
  "status": "Success",
  "statusMessage": "Equity Search details retrieved successfully",
  "equityDertivativeValues": [
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY20NOVFUT",
      "instrument": "FUTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY19NOV2029000CE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY19NOV2030000CE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY19NOV2028500CE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY19NOV2028000PE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY19NOV2029500CE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY19NOV2027000PE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY19NOV2027500PE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY19NOV2030500CE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY19NOV2028500PE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY20NOV30000CE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY20NOV28000PE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY20NOV29000CE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY19NOV2031000CE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY19NOV2026000PE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY20NOV27000PE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY19NOV2026500PE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY20NOV30500CE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY19NOV2031500CE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY20NOV29500CE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    }
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY31DEC2024500CE",
      "instrument": "OPTIDX"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY20NOV25900CE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY19NOV2022000CE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY19NOV2026700CE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY19NOV2026400CE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY20NOV22700PE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY20NOV29300PE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY20NOV22800PE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY31DEC2028300PE",
      "instrument": "OPTIDX"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY31DEC2028300CE",
      "instrument": "OPTIDX"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY31DEC2026800CE",
      "instrument": "OPTIDX"
    },
    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY20NOV21000CE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },    {
      "exchange": "NFO",
      "tradingSymbol": "BANKNIFTY21JUN19000PE",
      "instrument": "OPTIDX",
      "bodLotQuantity": "25"
    },

  ]
}
```
</details>

<details>
  <summary>Sample Search Request/Response  for Currency segment</summary>
  
  Request :
  ```python
 samco.search_equity_derivative(search_symbol_name="USDINR20DEC",exchange=samco.EXCHANGE_CDS)
  ```
  Response :  
  ```python
  Search:{
 "msgId": "14de6691-8493-464d-99c1-8eabb5a9d4e9",
 "status": "Success",
 "statusMessage": "Equity Search details retrieved successfully",
 "equityDertivativeValues": [
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC75PE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC75.5CE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC76CE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC74.5PE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC74.5CE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC74PE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC76PE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC72CE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC73.5PE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC74CE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC73PE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC76.5CE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC73CE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC73.5CE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC73.75PE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC75.5PE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC77CE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC72.5PE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC72.5CE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC72PE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC70.75PE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC72.5CE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC74.25PE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DEC78.5CE",
   "instrument": "OPTCUR",
   "bodLotQuantity": "1"
  },
  {
   "exchange": "CDS",
   "tradingSymbol": "USDINR20DECFUT",
   "instrument": "FUTCUR",
   "bodLotQuantity": "1"
  }
 ]
}
  ```
</details>

<details>
  <summary>Sample Search Request/Response  for Commodity segment</summary>
  
  Request :
  ```python
  samco.search_equity_derivative(search_symbol_name="SILVER20NOV68",exchange=samco.EXCHANGE_MCX)
  ```
  Response :  
  ```python
  Search:{
 "msgId": "44e00c5e-362a-48ad-a07b-6da0d9ab2c2a",
 "status": "Success",
 "statusMessage": "Equity Search details retrieved successfully",
 "equityDertivativeValues": [
  {
   "exchange": "MFO",
   "tradingSymbol": "SILVER20NOV68000CE",
   "instrument": "OPTFUT",
   "quantityInLots": "9"
  },
  {
   "exchange": "MFO",
   "tradingSymbol": "SILVER20NOV68250CE",
   "instrument": "OPTFUT",
   "quantityInLots": "0"
  },
  {
   "exchange": "MFO",
   "tradingSymbol": "SILVER20NOV68250PE",
   "instrument": "OPTFUT",
   "quantityInLots": "0"
  },
  {
   "exchange": "MFO",
   "tradingSymbol": "SILVER20NOV68500CE",
   "instrument": "OPTFUT",
   "quantityInLots": "0"
  },
  {
   "exchange": "MFO",
   "tradingSymbol": "SILVER20NOV68500PE",
   "instrument": "OPTFUT",
   "quantityInLots": "0"
  },
  {
   "exchange": "MFO",
   "tradingSymbol": "SILVER20NOV68750CE",
   "instrument": "OPTFUT",
   "quantityInLots": "0"
  },
  {
   "exchange": "MFO",
   "tradingSymbol": "SILVER20NOV68750PE",
   "instrument": "OPTFUT",
   "quantityInLots": "0"
  },
  {
   "exchange": "MFO",
   "tradingSymbol": "SILVER20NOV68000PE",
   "instrument": "OPTFUT",
   "quantityInLots": "0"
  }
 ]
}
  ```
</details>




<a name="quote"/>

## Quote

Get market depth details for a specific equity scrip including but not limited to values like last trade price, previous close price, change value, change percentage, bids/asks, upper and lower circuit limits etc. This helps user with market picture of an equity scrip using which he will be able to place an order.
The Quote function name in python is `get_quote()`

#### Parameters:
```python
`symbol_name`,exchange
```
<details>
  <summary>Sample Quote Request/Response  for Cash segment</summary>

Request:  
  ```python
  samco.get_quote(symbol_name="INFY",exchange=samco.EXCHANGE_NSE)
  ```

 Response:  
  ```python
  {
  "serverTime": "19/11/20 17:28:04",
  "msgId": "ba01c95a-3f07-46ad-9a09-efc42f4772ad",
  "status": "Success",
  "statusMessage": "Quote details retrieved successfully",
  "symbolName": "INFY",
  "tradingSymbol": "INFY-EQ",
  "exchange": "NSE",
  "companyName": "INFOSYS LIMITED",
  "lastTradedTime": "19/11/2020 16:10:13",
  "lastTradedPrice": "1100.00",
  "previousClose": "1157.80",
  "changeValue": "-57.80",
  "changePercentage": "-4.99",
  "lastTradedQuantity": "227",
  "lowerCircuitLimit": "999.50",
  "upperCircuitLimit": "1221.60",
  "averagePrice": "1098.93",
  "openValue": "1157.80",
  "highValue": "1200.00",
  "lowValue": "1055.50",
  "closeValue": "1157.80",
  "totalBuyQuantity": "87",
  "totalSellQuantity": "0",
  "totalTradedValue": "16.2861426 (Lacs)",
  "totalTradedVolume": "1482",
  "yearlyHighPrice": "0.00",
  "yearlyLowPrice": "0.00",
  "tickSize": "0.05",
  "bestBids": [
    {
    "number": "1",
    "quantity": "87",
    "price": "1055.50"
    },
    {
    "number": "2",
    "quantity": "0",
    "price": "0.00"
    },
    {
    "number": "3",
    "quantity": "0",
    "price": "0.00"
    },
    {
    "number": "4",
    "quantity": "0",
    "price": "0.00"
    },
    {
    "number": "5",
    "quantity": "0",
    "price": "0.00"
    }
  ],
  "bestAsks": [
    {
    "number": "1",
    "quantity": "0",
    "price": "0.00"
    },
    {
    "number": "2",
    "quantity": "0",
    "price": "0.00"
    },
    {
    "number": "3",
    "quantity": "0",
    "price": "0.00"
    },
    {
    "number": "4",
    "quantity": "0",
    "price": "0.00"
    },
    {
    "number": "5",
    "quantity": "0",
    "price": "0.00"
    }
  ],
  "listingId": "1594_NSE"
  }
  ```
</details>

<details>
  <summary>Sample Quote Request/Response for Future & Options segment</summary>

Request:  
  ```python
 samco.get_quote(symbol_name="INFY20NOVFUT",exchange=samco.EXCHANGE_NFO)
  ```
Response:
```python
{
   "serverTime": "29/10/20 13:31:29",
   "msgId": "688287cf-3818-4620-b5bc-b9c152c1de17",
   "status": "Success",
   "statusMessage": "Quote details retrieved successfully",
   "tradingSymbol": "INFY20NOVFUT",
   "exchange": "NFO",
   "lastTradedTime": "NA",
   "lastTradedPrice": "975.55",
   "changeValue": "-130.80",
   "changePercentage": "-11.82",
   "lastTradedQuantity": "1200",
   "lowerCircuitLimit": "973.20",
   "upperCircuitLimit": "1189.45",
   "averagePrice": "0.00",
   "totalBuyQuantity": "0",
   "totalSellQuantity": "0",
   "totalTradedValue": "NA",
   "totalTradedVolume": "0",
   "yearlyHighPrice": "0.00",
   "yearlyLowPrice": "0.00",
   "tickSize": "0.05",
   "openInterest": "23355600",
   "bestBids": [
    {
     "_number": "1",
     "quantity": "0",
     "price": "0.00"
    },
    {
     "_number": "2",
     "quantity": "0",
     "price": "0.00"
    },
    {
     "_number": "3",
     "quantity": "0",
     "price": "0.00"
    },
    {
     "_number": "4",
     "quantity": "0",
     "price": "0.00"
    },
    {
     "_number": "5",
     "quantity": "0",
     "price": "0.00"
    }
   ],
   "bestAsks": [
    {
     "_number": "1",
     "quantity": "0",
     "price": "0.00"
    },
    {
     "_number": "2",
     "quantity": "0",
     "price": "0.00"
    },
    {
     "_number": "3",
     "quantity": "0",
     "price": "0.00"
    },
    {
     "_number": "4",
     "quantity": "0",
     "price": "0.00"
    },
    {
     "_number": "5",
     "quantity": "0",
     "price": "0.00"
    }
   ],
   "expiryDate": "26 Nov 20",
   "spotPrice": "1072.80",
   "instrument": "FUTSTK",
   "lotQuantity": "1200",
   "listingId": "47312_NFO",
   "openInterestChange": "8505600"
  }
```
</details>
<details>
  <summary>Sample Quote Request/Response for Currency segment</summary>

Request :  
  ```python
	samco.get_quote(symbol_name="USDINR20DEC75PE",exchange=samco.EXCHANGE_CDS)
  ```
Response :
  ```python
    {
      "serverTime": "19/11/20 17:44:33",
      "msgId": "2f65bcc2-8c06-4db1-8147-97f5f6301414",
      "status": "Success",
      "statusMessage": "Quote details retrieved successfully",
      "tradingSymbol": "USDINR20DEC75PE",
      "exchange": "NSE-CDS",
      "lastTradedTime": "19/11/2020 05:00:00",
      "lastTradedPrice": "0.8050",
      "previousClose": "0.8375",
      "changeValue": "-0.0325",
      "changePercentage": "-3.88",
      "lastTradedQuantity": "1",
      "lowerCircuitLimit": "0.5150",
      "upperCircuitLimit": "1.1600",
      "averagePrice": "0.8078",
      "openValue": "0.84",
      "highValue": "0.84",
      "lowValue": "0.78",
      "closeValue": "0.8375",
      "totalBuyQuantity": "115",
      "totalSellQuantity": "1009",
      "totalTradedValue": "1961.35",
      "totalTradedVolume": "2428",
      "yearlyHighPrice": "0.0000",
      "yearlyLowPrice": "0.0000",
      "tickSize": "0.0025",
      "openInterest": "29937",
      "bestBids": [
        {
        "number": "1",
        "quantity": "2",
        "price": "0.7975"
        },
        {
        "number": "2",
        "quantity": "4",
        "price": "0.7725"
        },
        {
        "number": "3",
        "quantity": "1",
        "price": "0.7500"
        },
        {
        "number": "4",
        "quantity": "15",
        "price": "0.7025"
        },
        {
        "number": "5",
        "quantity": "1",
        "price": "0.7000"
        }
      ],
      "bestAsks": [
        {
        "number": "1",
        "quantity": "35",
        "price": "0.8225"
        },
        {
        "number": "2",
        "quantity": "10",
        "price": "0.8350"
        },
        {
        "number": "3",
        "quantity": "9",
        "price": "0.8400"
        },
        {
        "number": "4",
        "quantity": "1",
        "price": "0.8500"
        },
        {
        "number": "5",
        "quantity": "500",
        "price": "0.8900"
        }
      ],
      "expiryDate": "29 Dec 20",
      "instrument": "OPTCUR",
      "lotQuantity": "1",
      "listingId": "9192_CDS",
      "openInterestChange": "351",
      "oIChangePer": "1.19"
      }
  ```
</details>

<details>
  <summary>Sample Quote Request/Response for Commodity segment</summary>
	
Request :  
  ```python
	samco.get_quote(symbol_name="GOLDM21JANFUT",exchange=samco.EXCHANGE_MCX)
  ```

Response :  
  ```python
    {
      "serverTime": "19/11/20 17:53:08",
      "msgId": "4aa3c562-0464-4e31-b382-b7f9dbd1832a",
      "status": "Success",
      "statusMessage": "Quote details retrieved successfully",
      "tradingSymbol": "GOLDM21JAN57200PE",
      "exchange": "MCX",
      "companyName": "GOLDMINI995",
      "lastTradedTime": "19/11/2020 01:22:51",
      "lastTradedPrice": "0.00",
      "previousClose": "6278.0",
      "changeValue": "0.00",
      "changePercentage": "0.0",
      "lastTradedQuantity": "0",
      "lowerCircuitLimit": "0.00",
      "upperCircuitLimit": "0.00",
      "averagePrice": "0.00",
      "openValue": "0.0",
      "highValue": "0.0",
      "lowValue": "0.0",
      "closeValue": "6278.0",
      "totalBuyQuantity": "0",
      "totalSellQuantity": "0",
      "totalTradedValue": "0.00",
      "totalTradedVolume": "0",
      "yearlyHighPrice": "0.00",
      "yearlyLowPrice": "0.00",
      "tickSize": "0.5",
      "openInterest": "0",
      "bestBids": [
        {
        "number": "1",
        "quantity": "0",
        "price": "0.00"
        },
        {
        "number": "2",
        "quantity": "0",
        "price": "0.00"
        },
        {
        "number": "3",
        "quantity": "0",
        "price": "0.00"
        },
        {
        "number": "4",
        "quantity": "0",
        "price": "0.00"
        },
        {
        "number": "5",
        "quantity": "0",
        "price": "0.00"
        }
      ],
      "bestAsks": [
        {
        "number": "1",
        "quantity": "0",
        "price": "0.00"
        },
        {
        "number": "2",
        "quantity": "0",
        "price": "0.00"
        },
        {
        "number": "3",
        "quantity": "0",
        "price": "0.00"
        },
        {
        "number": "4",
        "quantity": "0",
        "price": "0.00"
        },
        {
        "number": "5",
        "quantity": "0",
        "price": "0.00"
        }
      ],
      "expiryDate": "05 Jan 21",
      "instrument": "OPTCOM",
      "lotQuantity": "100",
      "listingId": "225816_MFO",
      "openInterestChange": "0",
      "oIChangePer": "0"
      }
  ```
</details>

<a name="optionChain"/>

## OptionChain:

The OptionChain function `get_option_chain()` can be used to search OptionChain for equity, derivatives and commodity scrips based on user provided search symbol and exchange name.

#### Parameters:
```python
search_symbol_name,exchange,expiry_date,strike_price,option_type
```
<details>
  <summary>Sample OptionChain Request/Response  for Future & Options segment</summary>

  Request:
  ```python
	samco.get_option_chain(search_symbol_name="TCS",exchange=samco.EXCHANGE_NFO,expiry_date="2020-12-31",strike_price="1500",option_type='PE')
  ```
  Response:
  ```python
	{
	 "serverTime": "29/10/20 13:53:32",
	 "msgId": "35bd9041-0aab-49e4-8365-e784c2d1f43c",
	 "status": "Success",
	 "statusMessage": "OptionChain details retrived successfully. ",
	 "optionChainDetails": [
	  {
	   "tradingSymbol": "TCS20DEC1500PE",
	   "exchange": "NFO",
	   "symbol": "85010_NFO",
	   "strikePrice": "1500.00",
	   "expiryDate": "2020-12-31",
	   "instrument": "OPTSTK",
	   "optionType": "PE",
	   "underLyingSymbol": "TCS",
	   "spotPrice": "2645.50",
	   "lastTradedPrice": "0.00",
	   "openInterest": "0",
	   "openInterestChange": "0",
	   "oichangePer": "0",
	   "volume": "0"
	  }
	 ]
	}	
  ```
</details>


<details>
  <summary>Sample OptionChain Request/Response  for Currency segment</summary>
  
  Request:
  ```python
    samco.get_option_chain(search_symbol_name="USDINR",exchange=samco.EXCHANGE_CDS,expiry_date="2020-12-29",strike_price="83")
  ```
  Response:
  ```python
    {
      "serverTime": "20/11/20 11:15:15",
      "msgId": "55515231-8b5d-40bc-ba6f-64005d51eb44",
      "status": "Success",
      "statusMessage": "OptionChain details retrived successfully. ",
      "optionChainDetails": [
        {
        "tradingSymbol": "USDINR20DEC83CE",
        "exchange": "CDS",
        "symbol": "3033_CDS",
        "strikePrice": "83.00",
        "expiryDate": "2020-12-29",
        "instrument": "OPTCUR",
        "optionType": "CE",
        "underLyingSymbol": "USDINR",
        "lastTradedPrice": "0.0000",
        "openInterest": "0",
        "openInterestChange": "0",
        "oichangePer": "0",
        "volume": "0"
        },
        {
        "tradingSymbol": "USDINR20DEC83PE",
        "exchange": "CDS",
        "symbol": "3034_CDS",
        "strikePrice": "83.00",
        "expiryDate": "2020-12-29",
        "instrument": "OPTCUR",
        "optionType": "PE",
        "underLyingSymbol": "USDINR",
        "lastTradedPrice": "0.0000",
        "openInterest": "0",
        "openInterestChange": "0",
        "oichangePer": "0",
        "volume": "0"
        }
      ]
      }	  
  ```
</details>

<details>
  <summary>Sample OptionChain Request/Response  for Commodity segment</summary>
  
  Request:
  ```python
samco.get_option_chain(search_symbol_name="GOLD",exchange=samco.EXCHANGE_MCX,expiry_date="2021-01-27",strike_price="58600",option_type='CE')
  ```
  Response:
  ```python
  {
    "serverTime": "20/11/20 11:08:27",
    "msgId": "e2421d4a-3755-4f6a-92a4-38c7aa540c4b",
    "status": "Success",
    "statusMessage": "OptionChain details retrived successfully. ",
    "optionChainDetails": [
      {
      "tradingSymbol": "GOLD21JAN58600CE",
      "exchange": "MCX",
      "symbol": "223993_MFO",
      "strikePrice": "58600.00",
      "expiryDate": "2021-01-27",
      "instrument": "OPTCOM",
      "optionType": "CE",
      "underLyingSymbol": "GOLD",
      "lastTradedPrice": "0.00",
      "openInterest": "0",
      "openInterestChange": "0",
      "oichangePer": "0",
      "volume": "0",
      "bestBids": [
        {
        "number": "1",
        "quantity": "0",
        "price": "0.00"
        },
        {
        "number": "2",
        "quantity": "0",
        "price": "0.00"
        },
        {
        "number": "3",
        "quantity": "0",
        "price": "0.00"
        },
        {
        "number": "4",
        "quantity": "0",
        "price": "0.00"
        },
        {
        "number": "5",
        "quantity": "0",
        "price": "0.00"
        }
      ],
      "bestAsks": [
        {
        "number": "1",
        "quantity": "0",
        "price": "0.00"
        },
        {
        "number": "2",
        "quantity": "0",
        "price": "0.00"
        },
        {
        "number": "3",
        "quantity": "0",
        "price": "0.00"
        },
        {
        "number": "4",
        "quantity": "0",
        "price": "0.00"
        },
        {
        "number": "5",
        "quantity": "0",
        "price": "0.00"
        }
      ]
      }
    ]
    }	  
  ```
</details>


<a name="userLimits"/>

## UserLimits

The UserLimits function `get_limits()` can be used  to gets the user cash balances, available margin for trading in equity and commodity segments.

<details>
  <summary>Sample UserLimit Request</summary>

  ```python
	samco.get_limits()
  ```
</details>

<details>
  <summary>Sample UserLimit Response</summary>
  
  ```python
	{
  "serverTime": "18/06/20 12:27:44",
  "msgId": "095bd777-34f3-40b8-81fd-6bf25d3f3c3c",
  "status": "Success",
  "statusMessage": "User Limit details retrieved successfully",
  "equityLimit": {
    "grossAvailableMargin": "50000000000",
    "payInToday": "0",
    "notionalCash": "0",
    "marginUsed": "0",
    "netAvailableMargin": "50000000000"
  },
  "commodityLimit": {
    "grossAvailableMargin": "0",
    "payInToday": "0",
    "notionalCash": "0",
    "marginUsed": "0",
    "netAvailableMargin": "0"
  }
}
  ```
</details>

<a name="placeOrder"/>

## PlaceOrder

The PlaceOrder function `place_order()` can be used to place an equity/derivative order to the exchange i.e the place order request typically registers the order with OMS and when it happens successfully, a success response is returned. Successful placement of an order via the API does not imply its successful execution. When an order is successfully placed the PlaceOrder API returns an OrderNumber in response, and the actual order status can be checked separately using the OrderStatus API call .This is for Placing CNC, MIS and NRML Orders.


#### Parameters:
```python
symbol_name,exchange,transactionType,orderType,price,quantity,disclosedQuantity,orderValidity,productType,marketProtection
```
<details>
  <summary>Sample PlaceOrder Request/Response  for Cash segment</summary>

Request:
  ```python
samco.place_order(body={
"symbolName":"TCS",
"exchange":samco.EXCHANGE_NSE,
"transactionType":samco.TRANSACTION_TYPE_BUY,
"orderType":samco.ORDER_TYPE_LIMIT,
"price":"2374",
"quantity": "200",
"disclosedQuantity":"",
"orderValidity":samco.VALIDITY_DAY,
"productType":samco.PRODUCT_CNC,
"afterMarketOrderFlag":"NO"
})

  ```

Response:  
  ```python
	{
      "serverTime": "20/11/20 14:43:54",
      "msgId": "211b8163-e443-4a2f-89a2-e6c8df468de9",
      "orderNumber": "201120000000023",
      "status": "Success",
      "statusMessage": "CNC Order request placed successfully",
      "exchangeOrderStatus": "PENDING",
      "orderDetails": {
        "pendingQuantity": "200",
        "avgExecutionPrice": "0.00",
        "tradingSymbol": "TCS-EQ",
        "triggerPrice": "0.00",
        "exchange": "NSE",
        "totalQuantity": "200",
        "transactionType": "BUY",
        "productType": "CNC",
        "orderType": "L",
        "quantity": "200",
        "filledQuantity": "0",
        "orderPrice": "2374.0",
        "filledPrice": "0.00",
        "orderValidity": "DAY",
        "orderTime": "20/11/2020 14:43:55"
      }
    }
  ```
</details>

<details>
  <summary>Sample PlaceOrder Request/Response  for Future & Options segment</summary>

Request:
  ```python
	samco.place_order(body={
        "symbolName": "BANKNIFTY20NOVFUT",
        "exchange": sn.constants.EXCHANGE_NFO,
        "transactionType": sn.constants.TRANSACTION_TYPE_BUY,
        "orderType": sn.constants.ORDER_TYPE_MARKET,
        "quantity": "500",
        "disclosedQuantity": "",
        "orderValidity": sn.constants.VALIDITY_DAY,
        "productType": sn.constants.PRODUCT_MIS,
        "afterMarketOrderFlag": "NO"
      })
  ```

Response:  
  ```python
 {
    "serverTime": "23/11/20 15:14:11",
    "msgId": "28837fc5-23e3-4a39-9da8-9d0ffdd36f31",
    "orderNumber": "201123000152416",
    "status": "Success",
    "statusMessage": "MIS Order request placed successfully",
    "exchangeOrderStatus": "PENDING",
    "orderDetails": {
        "pendingQuantity": "50",
        "avgExecutionPrice": "0.00",
        "orderPlacedBy": "--",
        "tradingSymbol": "BANKNIFTY20NOVFUT",
        "triggerPrice": "0.00",
        "exchange": "NFO",
        "totalQuantity": "50",
        "transactionType": "BUY",
        "productType": "MIS",
        "orderType": "L",
        "quantity": "50",
        "filledQuantity": "0",
        "orderPrice": "29891.05",
        "filledPrice": "0.00",
        "orderValidity": "DAY",
        "orderTime": "23/11/2020 15:14:11"
    }
}
  ```
</details>

<details>
  <summary>Sample PlaceOrder Request/Response  for Currency segment</summary>

Request:
  ```python
	samco.place_order(body= {
        "symbolName": "USDINR20NOVFUT",
        "exchange": sn.constants.EXCHANGE_CDS,
        "transactionType": sn.constants.TRANSACTION_TYPE_BUY,
        "orderType": sn.constants.ORDER_TYPE_MARKET,
        "quantity": "10",
        "disclosedQuantity": "",
        "orderValidity": sn.constants.VALIDITY_DAY,
        "productType": sn.constants.PRODUCT_MIS,
        "afterMarketOrderFlag": "NO"
      })
  ```

Response:  
  ```python
	{
    "serverTime": "23/11/20 14:25:15",
    "msgId": "bfe30991-22a1-4814-9b36-c654cf96c21a",
    "orderNumber": "201123000134794",
    "status": "Success",
    "statusMessage": "MIS Order request placed successfully",
    "exchangeOrderStatus": "PENDING",
    "orderDetails": {
        "pendingQuantity": "10",
        "avgExecutionPrice": "0.0000",
        "orderPlacedBy": "--",
        "tradingSymbol": "USDINR20NOVFUT",
        "triggerPrice": "72.0000",
        "exchange": "CDS",
        "totalQuantity": "10",
        "transactionType": "BUY",
        "productType": "MIS",
        "orderType": "L",
        "quantity": "10",
        "filledQuantity": "0",
        "orderPrice": "76.3325",
        "filledPrice": "0.0000",
        "orderValidity": "DAY",
        "orderTime": "23/11/2020 14:25:19"
    }
}
  ```
</details>

<details>
  <summary>Sample PlaceOrder Request/Response  for Commodity segment</summary>

Request:
  ```python
	samco.place_order(body={
      "symbolName": "GOLDPETAL20NOVFUT",
      "exchange": sn.constants.EXCHANGE_MCX,
      "transactionType": sn.constants.TRANSACTION_TYPE_BUY,
      "orderType": sn.constants.ORDER_TYPE_LIMIT,
      "price": "5027",
      "quantity": "20",
      "disclosedQuantity": "",
      "orderValidity": sn.constants.VALIDITY_DAY,
      "productType": sn.constants.PRODUCT_NRML,
      "afterMarketOrderFlag": "NO"
    })
  ```

Response:  
  ```python
  {
      "serverTime": "23/11/20 12:51:39",
      "msgId": "b7d6acfe-a147-4421-8fd4-60551a8f3c72",
      "orderNumber": "201123000000008",
      "status": "Success",
      "statusMessage": "NRML Order request placed successfully",
      "exchangeOrderStatus": "PENDING",
      "orderDetails": {
        "pendingQuantity": "20",
        "avgExecutionPrice": "0.00",
        "tradingSymbol": "GOLDPETAL20NOVFUT",
        "triggerPrice": "0.00",
        "exchange": "MCX",
        "totalQuantity": "20",
        "transactionType": "BUY",
        "productType": "NRML",
        "orderType": "L",
        "quantity": "20",
        "filledQuantity": "0",
        "orderPrice": "5027.0",
        "filledPrice": "0.00",
        "orderValidity": "DAY",
        "orderTime": "23/11/2020 12:51:39"
      }
    }
  ```
</details>



<a name="placeOrderBO"/>

## PlaceOrderBO

The PlaceOrderBO function `place_order_bo()` can be used to place an equity/derivative bracket orders to the exchange i.e the place order BO request typically registers the order with OMS and when it happens successfully, a success response is returned. Successful placement of an order via the API does not imply its successful execution. So when an order is successfully placed the placeOrderBO returns an orderNumber in response, and the actual order status can be checked separately using the orderStatus API call. 

#### Parameters:
```python
symbol_name,exchange,transactionT
ype,orderType,price,quantity,disclosedQuantity,orderValidity,productType,trailingStopLoss,stopLossValue,squareOffValue,valueType,priceType,
```
<details>
  <summary>Sample PlaceOrderBO Request/Response  for Cash segment</summary>
  
Request:
  ```python
	samco.place_order_bo(body= {
        "symbolName": "TCS",
        "exchange": sn.constants.EXCHANGE_NSE,
        "transactionType": sn.constants.TRANSACTION_TYPE_BUY,
        "orderType": sn.constants.ORDER_TYPE_LIMIT,
        "quantity": "100",
        "disclosedQuantity": "",
        "price": "2660.10",
        "priceType": "LTP",
        "valueType": "Absolute",
        "orderValidity": sn.constants.VALIDITY_DAY,
        "productType": sn.constants.PRODUCT_BO,
        "squareOffValue": "50.00",
        "stopLossValue": "18.00",
        "trailingStopLoss": "5"
    })
  ```

Response:
  ```python
	{
    "serverTime": "20/11/20 15:51:56",
    "msgId": "03c0c1d0-04f7-42aa-8d4b-b5ca3bfff3c5",
    "orderNumber": "201120000000030",
    "status": "Success",
    "exchangeOrderStatus": "PENDING",
    "statusMessage": "Bracket Order request placed successfully",
    "orderDetails": {
      "pendingQuantity": "100",
      "avgExecutionPrice": "0.00",
      "tradingSymbol": "TCS-EQ",
      "triggerPrice": "0.00",
      "exchange": "NSE",
      "totalQuantity": "100",
      "transactionType": "BUY",
      "productType": "BO",
      "orderType": "L",
      "quantity": "100",
      "filledQuantity": "0",
      "orderPrice": "2660.1",
      "filledPrice": "0.00",
      "orderValidity": "DAY",
      "orderTime": "20/11/2020 15:51:58"
    }
  }

  ```
</details>

<details>
  <summary>Sample PlaceOrderBO Request/Response  for Future & Options segment</summary>

Request:
  ```python
  samco.place_order_bo(body={
        "symbolName": "BANKNIFTY20NOVFUT",
        "exchange": sn.constants.EXCHANGE_NFO,
        "transactionType": sn.constants.TRANSACTION_TYPE_BUY,
        "orderType": sn.constants.ORDER_TYPE_LIMIT,
        "quantity": "25",
        "disclosedQuantity": "",
        "price": "28976.95",
        "priceType": "LTP",
        "valueType": "Absolute",
        "orderValidity": sn.constants.VALIDITY_DAY,
        "productType": sn.constants.PRODUCT_BO,
        "squareOffValue": "50.00",
        "stopLossValue": "10.00",
        "trailingStopLoss": "5"
    })
  ```

Response:  
  ```python
 {
    "serverTime": "23/11/20 15:11:30",
    "msgId": "1e77f2f7-4951-4e5a-8df1-071ff184e863",
    "orderNumber": "201123000151445",
    "status": "Success",
    "statusMessage": "Bracket Order request placed successfully",
    "exchangeOrderStatus": "PENDING",
    "orderDetails": {
        "pendingQuantity": "25",
        "avgExecutionPrice": "0.00",
        "orderPlacedBy": "--",
        "tradingSymbol": "BANKNIFTY20NOVFUT",
        "triggerPrice": "0.00",
        "exchange": "NFO",
        "totalQuantity": "25",
        "transactionType": "BUY",
        "productType": "BO",
        "orderType": "L",
        "quantity": "25",
        "filledQuantity": "0",
        "orderPrice": "28976.95",
        "filledPrice": "0.00",
        "orderValidity": "DAY",
        "orderTime": "23/11/2020 15:11:30"
    }
}
  ```
</details>

<details>
  <summary>Sample PlaceOrderBO Request/Response  for Currency segment</summary>

Request:
  ```python
  samco.place_order_bo(body={
        "symbolName": "USDINR20NOVFUT",
        "exchange": sn.constants.EXCHANGE_CDS,
        "transactionType": sn.constants.TRANSACTION_TYPE_BUY,
        "orderType": sn.constants.ORDER_TYPE_LIMIT,
        "quantity": "10",
        "disclosedQuantity": "",
        "price": "74.11",
        "priceType": "LTP",
        "valueType": "Absolute",
        "orderValidity": sn.constants.VALIDITY_DAY,
        "productType": sn.constants.PRODUCT_BO,
        "squareOffValue": "10.00",
        "stopLossValue": "5.00",
        "trailingStopLoss": "5"
    })
  ```

Response:  
  ```python
  {
    "serverTime": "23/11/20 14:33:58",
    "msgId": "e704b5b8-9f93-42c2-b27e-bb347ad6cb45",
    "orderNumber": "201123000137902",
    "status": "Success",
    "statusMessage": "Bracket Order request placed successfully",
    "exchangeOrderStatus": "PENDING",
    "orderDetails": {
        "pendingQuantity": "1",
        "avgExecutionPrice": "0.0000",
        "orderPlacedBy": "--",
        "tradingSymbol": "USDINR20NOVFUT",
        "triggerPrice": "0.0000",
        "exchange": "CDS",
        "totalQuantity": "1",
        "transactionType": "BUY",
        "productType": "BO",
        "orderType": "L",
        "quantity": "1",
        "filledQuantity": "0",
        "orderPrice": "74.11",
        "filledPrice": "0.0000",
        "orderValidity": "DAY",
        "orderTime": "23/11/2020 14:33:58"
    }
}
  ```
</details>
<details>
  <summary>Sample PlaceOrderBO Request/Response  for Commodity segment</summary>

Request:
  ```python
  samco.place_order_bo(body={
            "symbolName": "GOLDPETAL20NOVFUT",
            "exchange": sn.constants.EXCHANGE_MCX,
            "transactionType": sn.constants.TRANSACTION_TYPE_BUY,
            "orderType": sn.constants.ORDER_TYPE_LIMIT,
            "quantity": "10",
            "disclosedQuantity": "",
            "price": "5027",
            "priceType": "LTP",
            "valueType": "Absolute",
            "orderValidity": sn.constants.VALIDITY_DAY,
            "productType": sn.constants.PRODUCT_BO,
            "squareOffValue": "50.00",
            "stopLossValue": "20.00",
            "trailingStopLoss": "5"
        })
  ```

Response:  
  ```python
    {
      "serverTime": "23/11/20 13:11:30",
      "msgId": "13dbdb56-818c-4e08-8072-2ed7a3c0b8fc",
      "orderNumber": "201123000000009",
      "status": "Success",
      "exchangeOrderStatus": "PENDING",
      "statusMessage": "Bracket Order request placed successfully",
      "orderDetails": {
        "pendingQuantity": "10",
        "avgExecutionPrice": "0.00",
        "tradingSymbol": "GOLDPETAL20NOVFUT",
        "triggerPrice": "0.00",
        "exchange": "MCX",
        "totalQuantity": "10",
        "transactionType": "BUY",
        "productType": "BO",
        "orderType": "L",
        "quantity": "10",
        "filledQuantity": "0",
        "orderPrice": "5027.0",
        "filledPrice": "0.00",
        "orderValidity": "DAY",
        "orderTime": "23/11/2020 13:11:32"
      }
    }
  ```
</details>

<a name="placeOrderCO"/>

## PlaceOrderCO

The PlaceOrderCO function `place_order_co()` can be used to place an equity/derivative CO order to the exchange i.e the place order CO request typically registers the order with OMS and when it happens successfully, a success response is returned. Successful placement of an order via the API does not imply its successful execution. So when an order is successfully placed the placeOrderCO returns an orderNumber in response, and in scenarios as above the actual order status can be checked separately using the orderStatus API call. 

#### Parameters:
```python
symbol_name,exchange,transactionType,orderType,price,quantity,disclosedQuantity,orderValidity,productType,marketProtection,triggerPrice
```
<details>
  <summary>Sample PlaceOrderCO Request/Response  for Cash segment</summary>
  
Request:
  ```python
	samco.place_order_co(body={
        "symbolName": "TCS",
        "exchange": sn.constants.EXCHANGE_NSE,
        "transactionType": sn.constants.TRANSACTION_TYPE_BUY,
        "orderType": sn.constants.ORDER_TYPE_MARKET,
        "quantity": "15",
        "disclosedQuantity": "",
        "orderValidity": sn.constants.VALIDITY_DAY,
        "productType": sn.constants.PRODUCT_CO,
        "afterMarketOrderFlag": "NO",
        "triggerPrice": "2650"

    })
  ```
Response:  
  ```python
  {
    "serverTime": "20/11/20 16:17:46",
    "msgId": "7ae6d72c-a64c-4884-976a-f8723904cd57",
    "orderNumber": "201120000000031",
    "status": "Success",
    "exchangeOrderStatus": "PENDING",
    "statusMessage": "CO Order request placed successfully",
    "orderDetails": {
      "pendingQuantity": "15",
      "avgExecutionPrice": "0.00",
      "tradingSymbol": "TCS-EQ",
      "triggerPrice": "2650.00",
      "exchange": "NSE",
      "totalQuantity": "15",
      "transactionType": "BUY",
      "productType": "CO",
      "orderType": "L",
      "quantity": "15",
      "filledQuantity": "0",
      "orderPrice": "2745.95",
      "filledPrice": "0.00",
      "orderValidity": "DAY",
      "orderTime": "20/11/2020 16:17:46"
    }
    }
  ```
</details>

<details>
  <summary>Sample PlaceOrderCO Request/Response  for Future & Options segment</summary>
  
Request:
  ```python
	samco.place_order_co(body={
        "symbolName": "BANKNIFTY20NOVFUT",
        "exchange": sn.constants.EXCHANGE_NFO,
        "transactionType": sn.constants.TRANSACTION_TYPE_BUY,
        "orderType": sn.constants.ORDER_TYPE_LIMIT,
        "price":"29028.60",
        "quantity": "50",
        "disclosedQuantity": "",
        "orderValidity": sn.constants.VALIDITY_DAY,
        "productType": sn.constants.PRODUCT_CO,
        "afterMarketOrderFlag": "NO",
        "triggerPrice": "28567"

    })
  ```
Response:  
  ```python
  {
    "serverTime": "23/11/20 15:17:31",
    "msgId": "59f7356a-341d-432a-b78f-5e8e536fb550",
    "orderNumber": "201123000154270",
    "status": "Success",
    "statusMessage": "CO Order request placed successfully",
    "exchangeOrderStatus": "PENDING",
    "orderDetails": {
        "pendingQuantity": "0",
        "avgExecutionPrice": "0.00",
        "orderPlacedBy": "--",
        "tradingSymbol": "BANKNIFTY20NOVFUT",
        "triggerPrice": "28567.00",
        "exchange": "NFO",
        "totalQuantity": "50",
        "transactionType": "BUY",
        "productType": "CO",
        "orderType": "L",
        "quantity": "50",
        "filledQuantity": "0",
        "orderPrice": "29028.6",
        "filledPrice": "0.00",
        "orderValidity": "DAY",
        "orderTime": "23/11/2020 15:17:31"
    }
}
  ```
</details>

<details>
  <summary>Sample PlaceOrderCO Request/Response  for Currency segment</summary>

Request:
  ```python
  samco.place_order_co(body= {
        "symbolName": "USDINR20NOVFUT",
        "exchange": sn.constants.EXCHANGE_CDS,
        "transactionType": sn.constants.TRANSACTION_TYPE_BUY,
        "orderType": sn.constants.ORDER_TYPE_MARKET,
        "quantity": "10",
        "disclosedQuantity": "",
        "orderValidity": sn.constants.VALIDITY_DAY,
        "productType": sn.constants.PRODUCT_CO,
        "afterMarketOrderFlag": "NO",
        "triggerPrice": "74"

    })
  ```
Response:  
  ```python
  {
    "serverTime": "23/11/20 14:28:57",
    "msgId": "c4195075-4d9a-4a32-9384-890b6e7525c4",
    "orderNumber": "201123000136146",
    "status": "Success",
    "statusMessage": "CO Order request placed successfully",
    "exchangeOrderStatus": "PENDING",
    "orderDetails": {
        "pendingQuantity": "10",
        "avgExecutionPrice": "0.0000",
        "orderPlacedBy": "--",
        "tradingSymbol": "USDINR20NOVFUT",
        "triggerPrice": "74.0000",
        "exchange": "CDS",
        "totalQuantity": "10",
        "transactionType": "BUY",
        "productType": "CO",
        "orderType": "L",
        "quantity": "10",
        "filledQuantity": "0",
        "orderPrice": "76.3275",
        "filledPrice": "0.0000",
        "orderValidity": "DAY",
        "orderTime": "23/11/2020 14:29:01"
    }
}
  ```
</details>

<details>
  <summary>Sample PlaceOrderCO Request/Response  for Commodity segment</summary>

Request:
  ```python
  samco.place_order_co(body={
        "symbolName": "ZINC20NOVFUT",
        "exchange": sn.constants.EXCHANGE_MCX,
        "transactionType": sn.constants.TRANSACTION_TYPE_BUY,
        "orderType": sn.constants.ORDER_TYPE_MARKET,
        "quantity": "150",
        "disclosedQuantity": "",
        "orderValidity": sn.constants.VALIDITY_DAY,
        "productType": sn.constants.PRODUCT_CO,
        "afterMarketOrderFlag": "NO",
        "triggerPrice": "220.25"
    })
  ```

Response:  
  ```python
    {
      "serverTime": "23/11/20 13:37:29",
      "msgId": "855b6efa-41b0-411b-8e92-54d49b8183b2",
      "orderNumber": "201123000117467",
      "status": "Success",
      "statusMessage": "CO Order request placed successfully",
      "exchangeOrderStatus": "PENDING",
      "orderDetails": {
          "pendingQuantity": "150",
          "avgExecutionPrice": "0.00",
          "orderPlacedBy": "--",
          "tradingSymbol": "ZINC20NOVFUT",
          "triggerPrice": "220.25",
          "exchange": "MCX",
          "totalQuantity": "150",
          "transactionType": "BUY",
          "productType": "CO",
          "orderType": "MKT",
          "quantity": "150",
          "filledQuantity": "0",
          "orderPrice": "0.0",
          "filledPrice": "0.00",
          "orderValidity": "DAY",
          "orderTime": "23/11/2020 13:37:32"
      }
    }
  ```
</details>

<a name="modifyOrder"/>

## ModifyOrder

The ModifyOrder function `modify_order()` can be used to modify some attributes of an order as long as it is with open/pending status in system. For modification order identifier is mandatory. With order identifier you need to send the optional parameter(s) which needs to be modified. In case the optional parameters aren't sent, the default will be considered from the original order. Modifiable attributes include quantity, Order Type (L,MKT, SL,SL-M). This API cannot be used for modifying attributes of an executed/rejected/cancelled order. Only the attribute that needs to be modified should be sent in the request alongwith the Order Identifier.

#### Parameters:
```python
orderType,quantity,disclosedQuantity,orderValidity,price,triggerPrice,parentOrderId,marketProtection
```
<details>
  <summary> Sample ModifyOrder Request/Response  for Cash segment</summary>
  
Request:
  ```python
samco.modify_order(order_number="201120000000030",body={"quantity": "20"})
  ```
Response :
  
  ```python
	{
      "serverTime": "20/11/20 17:38:56",
      "msgId": "b066db36-9661-44e7-aa43-b193a6c90fa3",
      "orderNumber": "201120000000030",
      "status": "Success",
      "statusMessage": "Order 201120000000030 modified successfully",
      "exchangeOrderStatus": "PENDING",
      "orderDetails": {
        "pendingQuantity": "78",
        "avgExecutionPrice": "2660.10",
        "tradingSymbol": "TCS-EQ",
        "triggerPrice": "0.00",
        "exchange": "NSE",
        "totalQuantity": "100",
        "transactionType": "BUY",
        "productType": "BO",
        "orderType": "L",
        "quantity": "100",
        "filledQuantity": "22",
        "orderPrice": "2660.1",
        "filledPrice": "2660.10",
        "exchangeOrderNo": "1100000000041268",
        "orderValidity": "DAY",
        "orderTime": "20/11/2020 17:38:57"
      }
    }
  ```
</details>

<details>
  <summary>Sample ModifyOrder Request/Response  for Future & Options segment</summary>

Request:
  ```python
samco.modify_order(order_number="201123000152416",body={"quantity": "50"})
  ```

Response:  
  ```python
{
    "serverTime": "23/11/20 15:24:11",
    "msgId": "28837fc5-23e3-4a39-9da8-9d0ffdd36f31",
    "orderNumber": "201123000152416",
    "status": "Success",
    "statusMessage": "Order 201123000152416 modified successfully",
    "exchangeOrderStatus": "PENDING",
    "orderDetails": {
        "pendingQuantity": "150",
        "avgExecutionPrice": "0.00",
        "orderPlacedBy": "--",
        "tradingSymbol": "BANKNIFTY20NOVFUT",
        "triggerPrice": "0.00",
        "exchange": "NFO",
        "totalQuantity": "150",
        "transactionType": "BUY",
        "productType": "MIS",
        "orderType": "L",
        "quantity": "150",
        "filledQuantity": "0",
        "orderPrice": "29891.05",
        "filledPrice": "0.00",
        "orderValidity": "DAY",
        "orderTime": "23/11/2020 15:24:11"
    }
}
  ```
</details>

<details>
  <summary>Sample ModifyOrder Request/Response  for Currency segment</summary>

Request:
  ```python
	samco.modify_order(order_number='200616000000350',body={"quantity": "50"})
  ```

Response:  
  ```python
	{
    "serverTime": "23/11/20 14:25:15",
    "msgId": "bfe30991-22a1-4814-9b36-c654cf96c21a",
    "orderNumber": "201123000134794",
    "status": "Success",
    "statusMessage": Order 201123000134794 modified successfully",
    "exchangeOrderStatus": "PENDING",
    "orderDetails": {
        "pendingQuantity": "15",
        "avgExecutionPrice": "0.0000",
        "orderPlacedBy": "--",
        "tradingSymbol": "USDINR20NOVFUT",
        "triggerPrice": "72.0000",
        "exchange": "CDS",
        "totalQuantity": "25",
        "transactionType": "BUY",
        "productType": "MIS",
        "orderType": "L",
        "quantity": "25",
        "filledQuantity": "0",
        "orderPrice": "76.3325",
        "filledPrice": "0.0000",
        "orderValidity": "DAY",
        "orderTime": "23/11/2020 14:25:19"
    }
}
  ```
</details>

<details>
  <summary>Sample ModifyOrder Request/Response  for Commodity segment</summary>

Request:
  ```python
		samco.modify_order(order_number="201123000000008",body={"quantity": "15"})
  ```

Response:  
  ```python
  {
      "serverTime": "23/11/20 12:51:39",
      "msgId": "b7d6acfe-a147-4421-8fd4-60551a8f3c72",
      "orderNumber": "201123000000008",
      "status": "Success",
      "statusMessage": "Order 201123000000008 modified successfully",
      "exchangeOrderStatus": "PENDING",
      "orderDetails": {
        "pendingQuantity": "20",
        "avgExecutionPrice": "0.00",
        "tradingSymbol": "GOLDPETAL20NOVFUT",
        "triggerPrice": "0.00",
        "exchange": "MCX",
        "totalQuantity": "20",
        "transactionType": "BUY",
        "productType": "NRML",
        "orderType": "L",
        "quantity": "20",
        "filledQuantity": "0",
        "orderPrice": "5027.0",
        "filledPrice": "0.00",
        "orderValidity": "DAY",
        "orderTime": "23/11/2020 12:51:39"
      }
    }
  ```
</details>

  
<a name="orderBook"/>

## OrderBook

The OrderBook function `get_order_book()` retrieves and displays details of all orders placed by the user on a specific day. This API returns all states of the orders, namely, open, pending, rejected and executed ones.

<details>
  <summary>Sample OrderBook Request</summary>
  
  ```python
samco.get_order_book()
  ```
</details>

<details>
  <summary>Sample OrderBook Response</summary>
  
  ```python
  {
  "serverTime": "16/06/20 18:25:18",
  "msgId": "2e2d2926-1a15-4510-b98e-c86d1f87cb7e",
  "status": "Success",
  "statusMessage": "Order Book details retrieved successfully",
  "orderBookDetails": [
    {
      "orderNumber": "200616000000350",
      "exchange": "NSE",
      "tradingSymbol": "RELIANCE",
      "transactionType": "BUY",
      "productCode": "MIS",
      "orderType": "L",
      "orderPrice": "1282.00",
      "triggerPrice": "0.00",
      "orderValidity": "DAY",
      "orderStatus": "Open",
      "orderValue": "0.0",
      "orderTime": "16-Jun-2020 18:03:47",
      "userId": "DS37591",
      "filledQuantity": "0",
      "fillPrice": "0.00",
      "averagePrice": "0.00",
      "rejectionReason": "--",
      "exchangeConfirmationTime": "16-Jun-2020 18:12:41",
      "coverOrderPercentage": "0.0",
      "orderRemarks": "--",
      "exchangeOrderNumber": "1100000000015551",
      "symbol": "2885_NSE",
      "displayStrikePrice": "00.00",
      "displayNetQuantity": "50",
      "status": "Open",
      "exchangeStatus": "open",
      "expiry": "NA",
      "pendingQuantity": "50",
      "totalQuanity": "50",
      "optionType": "XX",
      "orderPlaceBy": "Dv999"
    }
  ]
}
  ```
</details>


<a name="triggerOrders"/>

## TriggerOrders

The TriggerOrders function `get_trigger_order_numbers()` is used to get the trigger order numbers in case of BO and CO orders so that their attribute values can be modified for BO orders. It will give the order identifiers for Stop loss leg and target leg. Similarly for CO orders, it will return order identifier of stop loss leg only. Using the order identifier, the user would be able to modify the order attributes using the modifyOrder API. Refer modifyOrder API documentation for the parameters details.

#### Parameters:
```python
order_number
```

<details>
  <summary>Sample TriggerOrders Request</summary>
  
  ```python
samco.get_trigger_order_numbers(order_number="200617000000378")
  ```
</details>

<details>
  <summary>Sample TriggerOrders Response</summary>
  
  ```python
	
		{
    "serverTime": "17/06/20 18:40:00",
    "msgId": "ccff75e1-9d79-4b54-b4cb-bc48e080758f",
    "status": "Success",
    "statusMessage": "SubOrder details retrieved successfully.",
    "triggerOrders": [
        {
            "targetOrderNo": "200617000000380",
            "orderStatus": "Complete",
            "orderPrice": "2010.00",
            "triggerPrice": "0.00"         
        },
        {
            "targetOrderNo": "200617000000379",
            "orderStatus": "Cancelled",
            "orderPrice": "2029.95",
            "triggerPrice": "0.00"
        }
    ]
}
	
  ```
</details>

<a name="orderStatus"/>

## OrderStatus

The OrderStatus function `get_order_status` is used to get status of an order placed previously. This API returns all states of the orders,but not limited to open, pending, and partially filled ones.

#### Parameters:
```python
order_number
```
<details>
  <summary>Sample OrderStatus Request</summary>
  
  ```python
	samco.get_order_status(order_number="200617000000378")
  ```
</details>

<details>
  <summary>Sample OrderStatus Response</summary>
  
  ```python

    "serverTime": "17/06/20 20:54:53",
    "msgId": "d45688d9-31c0-4195-90ba-5474e7f50873",
    "orderNumber": "200617000000378",
    "orderStatus": "EXECUTED",
    "orderDetails": {
        "pendingQuantity": "0",
        "avgExecutionPrice": "2014.95",
        "orderPlacedBy": "--",
        "tradingSymbol": "TCS",
        "triggerPrice": "0.00",
        "exchange": "BSE",
        "totalQuantity": "10",
        "transactionType": "BUY",
        "productType": "BO",
        "orderType": "L",
        "quantity": "10",
        "filledQuantity": "10",
        "orderPrice": "2021.0",
        "filledPrice": "2014.95",
        "exchangeOrderNo": "1592387449638000143",
        "orderValidity": "DAY",
        "orderTime": "17/06/2020 18:38:37"
    }
}
```
</details>

      
<a name="cancelOrder"/>

## CancelOrder:

The CancleOrder function `cancel_order()` is used to cancel an order which is in open or pending status in system. In other words, cancellation cannot be initiated for already Executed, Rejected orders.This is for CNC, MIS and NRML Orders.

#### Parameters:
```python
order_number
```
<details>
  <summary>Sample CancelOrder Request</summary>
  
  ```python
samco.cancel_order(order_number='200616000000350')
  ```
</details>

<details>
  <summary>Sample CancelOrder Response</summary>
  
  ```python
	{
	  "serverTime" : "16/06/20 14:50:36",
	  "msgId" : "25d6d99b-3224-4a77-b129-a5d0bd38349b",
	  "status" : "Success",
	  "orderNumber" : "200616000000350",
	  "statusMessage" : "Order cancelled successfully"
	}
  ```
</details>

<a name="cancelOrderCO"/>

## CancelOrderCO

The CancleOrder function `cancel_order_co()` is used for Cancellation/exit of CO orders by passing main leg Order number. 

If main leg is in Open/Pending state that order will be cancelled.
If the main leg is executed and the sublegs are created and in open/Trigger pending state, the order will be exited.
If the main leg is executed and if Stop loss is hit, API will return error message "SubOrder is in Executed status. Cannot exit/cancel such orders.

#### Parameters:
```python
order_number
```
<details>
  <summary>Sample CancelOrderCO Request</summary>
  
  ```python
	samco.cancel_order(order_number='200617000000181')
  ```
</details>

<details>
  <summary>Sample CancelOrderCO Response</summary>
  
  ```python
	{
	  "serverTime" : "16/06/20 14:50:36",
	  "msgId" : "25d6d99b-3224-4a77-b129-a5d0bd38349b",
	  "status" : "Success",
	  "orderNumber" : "200617000000181",
	  "statusMessage" : "Cover Order 200617000000181 exited successfully"
	}
  ```
</details>

## CancelOrderBO

The CancleOrder function `cancel_order_bo()` is used for Cancellation/exit of BO orders pass main leg Order number. 
If main leg is in Open/Pending state that order will be cancelled.
If the main leg is executed and the sublegs are created and in open/Trigger pending state, the order will be exited.
If the main leg is executed and if either of Stop loss or target is hit, API will return error message "SubOrder is in Executed status. Cannot exit/cancel such orders.

#### Parameters:
```python
order_number
```

<details>
  <summary>Sample CancelOrderBO Request</summary>
  
  ```python
samco.cancel_order_bo(order_number='200617000000375')
  ```
</details>

<details>
  <summary>Sample CancelOrderBO Response</summary>
  
  ```python
	{
	  "serverTime" : "16/06/20 14:50:36",
	  "msgId" : "25d6d99b-3224-4a77-b129-a5d0bd38349b",
	  "status" : "Success",
	  "orderNumber" : "200617000000375",
	  "statusMessage" : "Bracket Order exited successfully"
	}
  ```
</details>

<a name="tradeBook"/>


## TradeBook

The TradeBook function is `get_trade_book()`which gives details of all successfully executed orders placed by the user.

<details>
  <summary>Sample TradeBook Request</summary>
  
  ```python
samco.get_trade_book()
  ```
</details>

<details>
  <summary> Sample TradeBook Response</summary>
  
  ```python
	 {
    "serverTime": "17/06/20 21:01:25",
    "msgId": "c4b7ec88-32e5-4e1f-a56b-7186f6933d79",
    "status": "Success",
    "statusMessage": "Request Successfull",
    "tradeBookDetails": [
        {
            "orderNumber": "200617000000380",
            "exchange": "BSE",
            "tradingSymbol": "TCS",
            "transactionType": "SELL",
            "productCode": "BO",
            "orderType": "L",
            "orderPrice": "2010.00",
            "quantity": "10",
            "orderValidity": "DAY",
            "orderTime": "06:39:50 PM",
            "filledQuantity": "10",
            "exchangeOrderNumber": "1592387449638000145",
            "tradeNumber": "25400",
            "tradePrice": "2010.00",
            "tradeDate": "17JUN2020",
            "tradeTime": "06:39:49 PM",
            "strikePrice": "0.00",
            "optionType": "XX",
            "expiry": "NA"
        }
    ]
}
  ```
</details>

  
<a name="positions"/>

## Positions

The Postions function `get_positions_data()` gets the position details of the user (The details of equity, derivative, commodity, currency borrowed or owned by the user).

#### Parameters:
```python
position_type
```
<details>
  <summary>Sample Positions Request</summary>
  
  ```python
samco.get_positions_data(position_type=samco.POSITION_TYPE_DAY)

  ```
</details>

<details>
  <summary>Sample Positions Response</summary>
  
  ```python
{
    "serverTime": "17/06/20 21:06:10",
    "msgId": "36a2cb48-2ce8-48e4-ac0a-90e68c6d26f1",
    "status": "Success",
    "statusMessage": "User Positions details retrieved successfully",
    "positionDetails": [
        {
            "averagePrice": "-4.95",
            "exchange": "BSE",
            "markToMarketPrice": "-99.00",
            "lastTradedPrice": "2,010.00",
            "previousClose": "2067.80",
            "productCode": "BO",
            "tradingSymbol": "TCS",
            "calculatedNetQuantity": "0.0",
            "averageBuyPrice": "2014.95",
            "averageSellPrice": "2010.00",
            "boardLotQuantity": "1",
            "boughtPrice": "40299.00",
            "buyQuantity": "20",
            "carryForwardQuantity": "0",
            "carryForwardValue": "0.00",
            "multiplier": "1",
            "netPositionValue": "-99.00",
            "netQuantity": "0",
            "netValue": "-99.00",
            "positionType": "DAY",
            "positionConversions": [
                "CNC",
                "NRML"
            ],
            "soldValue": "40200.00",
            "transactionType": "BUY",
            "realizedGainAndLoss": "-99.00",
            "unrealizedGainAndLoss": "0.00",
            "companyName": "TATA CONSULTANCY SERVICES LTD."
        }
    ]
}
  ```
</details>

       
<a name="positionConversion"/>

## PositionConversion

The PostionConversion function `convert_position()` is used to convert an existing position of a margin product to a different margin product type. All or a subset of an existing position quantity can be converted to a different product type.The available margin product types are MARGIN_INTRADAY_SQUAREOFF(MIS), CASHNCARRY(CNC), NORMAL(NRML).

#### Parameters:
```python
symbolName,exchange,transactionType,positionType,quantityToConvert,fromProductType,toProductType,netQuantity
```
<details>
  <summary>Sample PositionConverstion Request/Response  for Cash segment</summary>
  
Request :
  ```python
samco.convert_position(body= {
        "symbolName": "TCS",
        "exchange": sn.constants.EXCHANGE_BSE,
        "transactionType": sn.constants.TRANSACTION_TYPE_BUY,
        "positionType": sn.constants.VALIDITY_DAY,
        "quantityToConvert": "2",
        "fromProductType": sn.constants.PRODUCT_MIS,
        "toProductType": sn.constants.PRODUCT_CNC,
        "netQuantity": "2"
    })
  ```
  Response:
  ```python
  {
  "serverTime" : "23/11/20 15:06:42",
  "msgId" : "ba32c75f-ee4b-4af6-a580-f17ad36fefd4",
  "status" : "Success",
  "statusMsg" : "Position Conversion from MIS to CNC successful"
}
  ```
</details>

<details>
  <summary>Sample PositionConverstion Request/Response for Future & Options segment</summary>
  
Request :
  ```python
samco.convert_position(body={
        "symbolName": "BANKNIFTY20NOVFUT",
        "exchange": sn.constants.EXCHANGE_NFO,
        "transactionType": sn.constants.TRANSACTION_TYPE_BUY,
        "positionType": sn.constants.VALIDITY_DAY,
        "quantityToConvert": "10",
        "fromProductType": sn.constants.PRODUCT_NRML,
        "toProductType": sn.constants.PRODUCT_MIS,
        "netQuantity": "60"
    })
  ```

Response :  
  ```python
  {
  "serverTime" : "23/11/20 15:06:42",
  "msgId" : "ba23c75f-ee4b-4af6-a850-f17ad36fefd4",
  "status" : "Success",
  "statusMsg" : "Position Conversion from NRML to MIS successful"
}
  ```
</details>

<details>
  <summary>Sample PositionConverstion Request/Response for Currency segment</summary>
  
Request :
  ```python
samco.convert_position(body= {
        "symbolName": "USDINR20NOVFUT",
        "exchange": sn.constants.EXCHANGE_CDS,
        "transactionType": sn.constants.TRANSACTION_TYPE_BUY,
        "positionType": sn.constants.VALIDITY_DAY,
        "quantityToConvert": "10",
        "fromProductType": sn.constants.PRODUCT_NRML,
        "toProductType": sn.constants.PRODUCT_MIS,
        "netQuantity": "50"
    })
  ```

Response :  
  ```python
{
  "serverTime" : "23/11/20 15:06:42",
  "msgId" : "ba23c75f-ee4b-4af6-a850-f17ad36fefd4",
  "status" : "Success",
  "statusMsg" : "Position Conversion from NRML to MIS successful"
}
  ```
</details>

<details>
  <summary>Sample PositionConverstion Request/Response for Commodity segment</summary>
  
Request :
  ```python
samco.convert_position(body={
        "symbolName": "GOLDPETAL20NOVFUT",
        "exchange": sn.constants.EXCHANGE_MCX,
        "transactionType": sn.constants.TRANSACTION_TYPE_BUY,
        "positionType": sn.constants.VALIDITY_DAY,
        "quantityToConvert": "50",
        "fromProductType": sn.constants.PRODUCT_NRML,
        "toProductType": sn.constants.PRODUCT_MIS,
        "netQuantity": "150"
    })
  ```

Response :  
  ```python
{
  "serverTime" : "23/11/20 15:06:42",
  "msgId" : "ba23c75f-ee4b-4af6-a850-f17ad36fefd4",
  "status" : "Success",
  "statusMsg" : "Position Conversion from NRML to MIS successful"
}
  ```
</details>


<a name="positionSquareOff"/>

## PositionSquareOff

The PositionSquareoff function `square_off_position()` helps the user to SqareOff existing position. Mostly used in day trading, in which user buy or sell a particular quantity of a stock and later in the day reverse the transaction to earn a profit. 

#### Parameters:
```python
symbolName,exchange,transactionType,productType,netQuantity
```
<details>
  <summary>Sample PositionSquareoff Request/Response  for Cash segment</summary>
  
  Request :
  ```python
  samco.square_off_position(body={ 
    "positionSquareOffRequestList": [
    { 
            "exchange":sn.constants.EXCHANGE_NSE,
            "symbolName":"TCS",
            "productType":sn.constants.PRODUCT_MIS,
            "netQuantity":"1",
            "transactionType":sn.constants.TRANSACTION_TYPE_BUY
        }    
       ]
    })
  ```
  Response :
  
  ```python
 {
  "serverTime": "25/06/20 20:04:30",
  "msgId": "fcb519b8-dd74-422a-8a65-1dc0a0caedb7",
  "positionSquareOffResponseList": [
    {
      "status": "Success",
      "statusMessage": "Position square off successful -TCS-EQ NetQty:1"
    }
  ]
}
  ```
</details>

<details>
  <summary>Sample PositionSquareoff Request/Response for Future & Options segment</summary>
  
  Request :
  ```python
  samco.square_off_position(body={ 
        "positionSquareOffRequestList": [
        {
            "exchange":sn.constants.EXCHANGE_NFO,
            "symbolName":"INFY20NOVFUT",
            "productType":sn.constants.PRODUCT_MIS,
            "netQuantity":"10",
            "transactionType":sn.constants.TRANSACTION_TYPE_BUY
        }    
       ]
    })
  ```
  Response :
  ```python
{
  "serverTime": "25/11/20 20:04:30",
  "msgId": "fcb519b8-dd74-422a-8a65-1dcsda0caedb7",
  "positionSquareOffResponseList": [
    {
      "status": "Success",
      "statusMessage": "Position square off successful -INFY20NOVFUT NetQty:10"
    }
  ]
}
  ```
</details>

<details>
  <summary>Sample PositionSquareoff Request/Response for Currency segment</summary>
  
  Request :
  ```python
  samco.square_off_position(body={
        "positionSquareOffRequestList": [
        {
            "exchange":sn.constants.EXCHANGE_CDS,
            "symbolName":"USDINR20DEC75PE",
            "productType":sn.constants.PRODUCT_MIS,
            "netQuantity":"10",
            "transactionType":sn.constants.TRANSACTION_TYPE_BUY
        }    
       ]
    })
  ```
  Response :
  
  ```python
{
  "serverTime": "25/11/20 20:04:30",
  "msgId": "fcb519b8-dd74-422a-8a65-1dcsda0caedb7",
  "positionSquareOffResponseList": [
    {
      "status": "Success",
      "statusMessage": "Position square off successful -USDINR20DEC75PE NetQty:10"
    }
  ]
}
  ```
</details>

<details>
  <summary>Sample PositionSquareoff Request/Response for Commodity segment</summary>
  
  Request :
  ```python
  samco.square_off_position(body={
        "positionSquareOffRequestList": [
        {
            "exchange":sn.constants.EXCHANGE_MCX,
            "symbolName":"GOLDM21JANFUT",
            "productType":sn.constants.PRODUCT_MIS,
            "netQuantity":"10",
            "transactionType":sn.constants.TRANSACTION_TYPE_BUY
        }    
       ]
    })
  ```
  Response :
  
  ```python
{
  "serverTime": "25/11/20 20:04:30",
  "msgId": "fcb519b8-dd74-422a-8a65-1dcsda0caedb7",
  "positionSquareOffResponseList": [
    {
      "status": "Success",
      "statusMessage": "Position square off successful -GOLDM21JANFUT NetQty:10"
    }
  ]
}
  ```
</details>

<a name="holdings"/>

## Holdings

The Holdings function `get_holding()` helps the user to get the details of the Stocks which client is holding. Here, you will be able to get the Client holdings which are bought under ‘CNC’ product type and are not sold yet.

<details>
  <summary>Sample Holdings Request</summary>
  
  ```python
samco.get_holding()
  ```
</details>

<details>
  <summary>Sample Holdings Response</summary>
  
  ```python
{
    "serverTime": "16/06/20 18:31:52",
    "msgId": "192d039e-6647-4e2f-8d97-5a91143d47a7",
    "status": "Success",
    "statusMessage": "User Holding details retrieved successfully",
    "holdingSummary": {
        "gainingTodayCount": "2",
        "losingTodayCount": "2",
        "totalGainAndLossAmount": "-242900000.00",
        "portfolioValue": "176205000.00"
    },
    "holdingDetails": [
        {
            "averagePrice": "51.10",
            "exchange": "BSE",
            "lastTradedPrice": "0.00",
            "previousClose": "51.10",
            "productCode": "CNC",
            "symbolDescription": "ASHOK LEYLAND LTD.",
            "tradingSymbol": "ASHOKLEY",
            "totalGainAndLoss": "-51100000.00",
            "holdingsQuantity": "1000000",
            "collateralQuantity": "0",
            "holdingsValue": "0.00",
            "sellableQuantity": "1000000"
        },
        {
            "averagePrice": "1610.60",
            "exchange": "NSE",
            "lastTradedPrice": "1760.30",
            "previousClose": "1610.60",
            "productCode": "CNC",
            "symbolDescription": "ASIAN PAINTS LIMITED",
            "tradingSymbol": "ASIANPAINT-EQ",
            "totalGainAndLoss": "14970000.00",
            "holdingsQuantity": "100000",
            "collateralQuantity": "0",
            "holdingsValue": "176030000.00",
            "sellableQuantity": "100000"
        },
        {
            "averagePrice": "1.65",
            "exchange": "NSE",
            "lastTradedPrice": "1.75",
            "previousClose": "1.65",
            "productCode": "CNC",
            "symbolDescription": "JAIPRAKASH ASSOCIATES LTD",
            "tradingSymbol": "JPASSOCIAT-EQ",
            "totalGainAndLoss": "10000.00",
            "holdingsQuantity": "100000",
            "collateralQuantity": "0",
            "holdingsValue": "175000.00",
            "sellableQuantity": "100000"
        },
        {
            "averagePrice": "2067.80",
            "exchange": "BSE",
            "lastTradedPrice": "0.00",
            "previousClose": "2067.80",
            "productCode": "CNC",
            "symbolDescription": "TATA CONSULTANCY SERVICES LTD.",
            "tradingSymbol": "TCS",
            "totalGainAndLoss": "-206780000.00",
            "holdingsQuantity": "100000",
            "collateralQuantity": "0",
            "holdingsValue": "0.00",
            "sellableQuantity": "100000"
        }
    ]
}
                       
  ```
</details>
           
<a name="intraDayCandleData"/>

## IntraDayCandleData

The IndexIntraDayCandleData function `get_intraday_candle_data()` gets the Intraday candle data such as Open, high, low, close and volume within specific time period per min for a specific symbol.


#### Parameters:
```python
symbol_name,exchange,from_date,to_date
```
<details>
  <summary>Sample IntraDayCandleData Request/Response  for Cash segment </summary>
  
Request:
  ```python
samco.get_intraday_candle_data(symbol_name='INFY',exchange=samco.EXCHANGE_NSE, from_date='2020-06-17 10:22:00',to_date='2020-06-17 10:28:00')
 ```
Response:  
  ```python
{
  "serverTime": "17/06/20 10:50:31",
  "msgId": "c3a1ae34-8078-4f56-8a00-83f92bfa3a4b",
  "status": "Success",
  "statusMessage": "Intraday candle data retrieved successfully",
  "intradayCandleData": [
    {
      "dateTime": "2020-06-17 10:22:00.0",
      "open": "705.25",
      "high": "705.3",
      "low": "704.6",
      "close": "704.65",
      "volume": "7627"
    },
    {
      "dateTime": "2020-06-17 10:23:00.0",
      "open": "704.6",
      "high": "704.7",
      "low": "704.0",
      "close": "704.0",
      "volume": "16154"
    },
    {
      "dateTime": "2020-06-17 10:24:00.0",
      "open": "704.25",
      "high": "704.6",
      "low": "704.05",
      "close": "704.6",
      "volume": "13767"
    },
    {
      "dateTime": "2020-06-17 10:25:00.0",
      "open": "704.75",
      "high": "704.75",
      "low": "703.8",
      "close": "703.95",
      "volume": "13091"
    },
    {
      "dateTime": "2020-06-17 10:26:00.0",
      "open": "703.95",
      "high": "704.3",
      "low": "703.8",
      "close": "704.1",
      "volume": "7039"
    },
    {
      "dateTime": "2020-06-17 10:27:00.0",
      "open": "704.15",
      "high": "704.15",
      "low": "703.55",
      "close": "703.95",
      "volume": "17886"
    },
    {
      "dateTime": "2020-06-17 10:28:00.0",
      "open": "704.0",
      "high": "704.95",
      "low": "703.75",
      "close": "704.85",
      "volume": "17760"
    }
  ]
}
  ```
</details>

<details>
  <summary>Sample IntraDayCandleData Request/Response  for Future & Options segment </summary>
  
Request:
  ```python
    samco.get_intraday_candle_data(symbol_name='TCS20DEC2700CE',exchange=samco.EXCHANGE_NFO, from_date='2020-11-11 02:22:00',to_date='2020-11-12 08:22:00')
 ```
Response:  
  ```python
  intradayCandleData:{
      "serverTime": "20/11/20 11:33:02",
      "msgId": "54597ad9-1a04-4a66-a2a0-e537dd685675",
      "status": "Success",
      "statusMessage": "Intraday candle data retrieved successfully",
      "intradayCandleData": [
        {
        "dateTime": "2020-11-11 10:00:00",
        "open": "95.0",
        "high": "98.25",
        "low": "81.8",
        "close": "94.85",
        "volume": "1200"
        },
        {
        "dateTime": "2020-11-11 11:00:00",
        "open": "94.85",
        "high": "106.15",
        "low": "94.85",
        "close": "106.15",
        "volume": "300"
        },
        {
        "dateTime": "2020-11-11 12:00:00",
        "open": "106.15",
        "high": "106.15",
        "low": "102.0",
        "close": "102.0",
        "volume": "600"
        },
        {
        "dateTime": "2020-11-11 13:00:00",
        "open": "102.0",
        "high": "102.0",
        "low": "102.0",
        "close": "102.0",
        "volume": "0"
        },
        {
        "dateTime": "2020-11-11 14:00:00",
        "open": "102.0",
        "high": "102.0",
        "low": "88.0",
        "close": "88.0",
        "volume": "300"
        },
        {
        "dateTime": "2020-11-11 15:00:00",
        "open": "88.0",
        "high": "110.0",
        "low": "88.0",
        "close": "110.0",
        "volume": "600"
        }
      ]
      }
  ```
</details>

<details>
  <summary>Sample IntraDayCandleData Request/Response  for Currency  segment </summary>
  
Request:
  ```python
    samco.get_intraday_candle_data(symbol_name='GBPINR20NOV97PE',exchange=samco.EXCHANGE_CDS, from_date='2020-11-11 02:22:00',to_date='2020-11-12 08:22:00')

 ```
Response:  
  ```python
  intradayCandleData:{
      "serverTime": "20/11/20 11:38:52",
      "msgId": "0070df31-0037-4be4-89fa-87ca0f03ee1c",
      "status": "Success",
      "statusMessage": "Intraday candle data retrieved successfully",
      "intradayCandleData": [
        {
        "dateTime": "2020-11-11 10:00:00",
        "open": "0.19",
        "high": "0.19",
        "low": "0.19",
        "close": "0.19",
        "volume": "1"
        },
        {
        "dateTime": "2020-11-11 11:00:00",
        "open": "0.19",
        "high": "0.19",
        "low": "0.14",
        "close": "0.14",
        "volume": "50"
        },
        {
        "dateTime": "2020-11-11 12:00:00",
        "open": "0.14",
        "high": "0.14",
        "low": "0.14",
        "close": "0.14",
        "volume": "0"
        },
        {
        "dateTime": "2020-11-11 13:00:00",
        "open": "0.14",
        "high": "0.1525",
        "low": "0.1225",
        "close": "0.1225",
        "volume": "69"
        },
        {
        "dateTime": "2020-11-11 14:00:00",
        "open": "0.1225",
        "high": "0.1525",
        "low": "0.11",
        "close": "0.11",
        "volume": "53"
        },
        {
        "dateTime": "2020-11-11 15:00:00",
        "open": "0.11",
        "high": "0.125",
        "low": "0.1",
        "close": "0.1",
        "volume": "77"
        },
        {
        "dateTime": "2020-11-11 16:00:00",
        "open": "0.1",
        "high": "0.165",
        "low": "0.1",
        "close": "0.165",
        "volume": "26"
        }
      ]
      }
  ```
</details>

<details>
  <summary>Sample IntraDayCandleData Request/Response  for Commodity segment </summary>
  
Request:
  ```python
   samco.get_intraday_candle_data(symbol_name='GOLD20NOV51000CE',exchange=samco.EXCHANGE_MCX, from_date='2020-11-11 02:22:00',to_date='2020-11-12 08:22:00')
 ```
Response:  
  ```python
    intradayCandleData:{
    "serverTime": "20/11/20 11:42:55",
    "msgId": "749d7dcf-0136-4a9f-a20a-4fb59f1eb53b",
    "status": "Success",
    "statusMessage": "Intraday candle data retrieved successfully",
    "intradayCandleData": [
      {
      "dateTime": "2020-11-11 10:00:00",
      "open": "405.5",
      "high": "405.5",
      "low": "405.5",
      "close": "405.5",
      "volume": "0"
      },
      {
      "dateTime": "2020-11-11 11:00:00",
      "open": "405.5",
      "high": "405.5",
      "low": "390.0",
      "close": "405.0",
      "volume": "8"
      },
      {
      "dateTime": "2020-11-11 12:00:00",
      "open": "405.0",
      "high": "415.0",
      "low": "405.0",
      "close": "415.0",
      "volume": "3"
      },
      {
      "dateTime": "2020-11-11 13:00:00",
      "open": "415.0",
      "high": "425.0",
      "low": "390.0",
      "close": "390.0",
      "volume": "3"
      },
      {
      "dateTime": "2020-11-11 14:00:00",
      "open": "390.0",
      "high": "405.0",
      "low": "390.0",
      "close": "405.0",
      "volume": "1"
      },
      {
      "dateTime": "2020-11-11 15:00:00",
      "open": "405.0",
      "high": "405.0",
      "low": "360.0",
      "close": "360.0",
      "volume": "10"
      },
      {
      "dateTime": "2020-11-11 16:00:00",
      "open": "360.0",
      "high": "390.0",
      "low": "345.0",
      "close": "345.0",
      "volume": "7"
      },
      {
      "dateTime": "2020-11-11 17:00:00",
      "open": "345.0",
      "high": "352.5",
      "low": "330.0",
      "close": "340.0",
      "volume": "20"
      },
      {
      "dateTime": "2020-11-11 18:00:00",
      "open": "340.0",
      "high": "377.0",
      "low": "340.0",
      "close": "346.0",
      "volume": "11"
      },
      {
      "dateTime": "2020-11-11 19:00:00",
      "open": "346.0",
      "high": "346.0",
      "low": "320.0",
      "close": "320.0",
      "volume": "3"
      },
      {
      "dateTime": "2020-11-11 20:00:00",
      "open": "320.0",
      "high": "325.0",
      "low": "270.0",
      "close": "302.5",
      "volume": "36"
      },
      {
      "dateTime": "2020-11-11 21:00:00",
      "open": "302.5",
      "high": "315.0",
      "low": "262.5",
      "close": "285.0",
      "volume": "14"
      },
      {
      "dateTime": "2020-11-11 22:00:00",
      "open": "285.0",
      "high": "296.0",
      "low": "243.5",
      "close": "274.0",
      "volume": "32"
      },
      {
      "dateTime": "2020-11-11 23:00:00",
      "open": "258.0",
      "high": "264.0",
      "low": "248.0",
      "close": "263.0",
      "volume": "27"
      }
    ]
    }
  ```
</details>


<a name="indexIntraDayCandleData"/>

### IndexIntraDayCandleData

The IndexIntraDayCandleData function `get_index_intraday_candle_data()` gets the Index intraday candle data such as Open, high, low, close and volume within specific time period per min for a specific index.

#### Parameters:
```python
index_name,from_date,to_date
```

  <details>
  <summary>Sample IndexIntraDayCandleData Request</summary>
  
  ```python
samco.get_index_intraday_candle_data(index_name='sensex', from_date='2020-06-16 09:23:00',to_date='2020-06-16 9:28:00')

  ```
</details>

<details>
  <summary>Sample IndexIntraDayCandleData Response</summary>
  
  ```python
  {
  "serverTime": "16/06/20 19:09:13",
  "msgId": "42bc5657-2d2b-49f3-8ead-1bb07a157e2a",
  "status": "Success",
  "statusMessage": "Index IntraDay Candle data retrieved successfully ",
  "indexIntraDayCandleData": [
    {
      "dateTime": "2020-06-16 09:23:00.0",
      "open": "33896.83",
      "high": "33914.65",
      "low": "33874.05",
      "close": "33874.96",
      "volume": "0"
    },
    {
      "dateTime": "2020-06-16 09:24:00.0",
      "open": "33878.08",
      "high": "33915.78",
      "low": "33874.27",
      "close": "33909.3",
      "volume": "0"
    },
    {
      "dateTime": "2020-06-16 09:25:00.0",
      "open": "33905.3",
      "high": "33911.31",
      "low": "33884.92",
      "close": "33900.15",
      "volume": "0"
    },
    {
      "dateTime": "2020-06-16 09:26:00.0",
      "open": "33899.02",
      "high": "33936.46",
      "low": "33899.02",
      "close": "33936.46",
      "volume": "0"
    },
    {
      "dateTime": "2020-06-16 09:27:00.0",
      "open": "33936.5",
      "high": "33951.67",
      "low": "33924.21",
      "close": "33925.92",
      "volume": "0"
    },
    {
      "dateTime": "2020-06-16 09:28:00.0",
      "open": "33925.2",
      "high": "33928.91",
      "low": "33886.56",
      "close": "33890.5",
      "volume": "0"
    }
  ]
}
  ```
</details>      
      
      
<a name="historicalCandleData"/>

## HistoricalCandleData:

The HistoricalCandleData function `get_index_intraday_candle_data()` gets the historical candle data such as Open, high, low, close, last traded price and volume within specific dates for a specific symbol. From date is mandatory. End date is optional and defaults to Today.

#### Parameters:
```python
symbol_name,exchange,from_date,to_date
```
<details>
  <summary>Sample HistoricalCandleData Request/Response  for Cash segment</summary>
  
Request :
  ```python
    samco.get_historical_candle_data(symbol_name='TCS',exchange=samco.EXCHANGE_NSE, from_date='2020-11-01',to_date='2020-11-05')

  ```
Respone:
  
  ```python
    {
      "serverTime": "20/11/20 12:04:39",
      "msgId": "45f1f334-948b-4106-a8b0-a31798eb5966",
      "status": "Success",
      "statusMessage": "Historical candle data retrieved successfully",
      "historicalCandleData": [
        {
        "date": "2020-11-02",
        "open": "2660.0",
        "high": "2664.85",
        "low": "2600.05",
        "close": "2604.6",
        "ltp": "2608.0",
        "volume": "2571196"
        },
        {
        "date": "2020-11-03",
        "open": "2604.0",
        "high": "2665.0",
        "low": "2601.05",
        "close": "2633.6",
        "ltp": "2629.0",
        "volume": "2879269"
        },
        {
        "date": "2020-11-04",
        "open": "2610.0",
        "high": "2721.85",
        "low": "2610.0",
        "close": "2653.15",
        "ltp": "2656.0",
        "volume": "4893928"
        },
        {
        "date": "2020-11-05",
        "open": "2685.0",
        "high": "2710.0",
        "low": "2667.0",
        "close": "2685.7",
        "ltp": "2688.0",
        "volume": "2816502"
        }
      ]
    }
  ```
</details>

<details>
  <summary>Sample HistoricalCandleData Request/Response  for Future & Options segment</summary>
  
Request :
  ```python
    samco.get_historical_candle_data(symbol_name='TCS20NOV3000CE',exchange=samco.EXCHANGE_NFO, from_date='2020-11-01',to_date='2020-11-05')

  ```
Respone:
  ```python
    {
      "serverTime": "20/11/20 12:16:55",
      "msgId": "6a3743c2-3fa9-4eb0-8aea-e176d85a7cbf",
      "status": "Success",
      "statusMessage": "Historical candle data retrieved successfully",
      "historicalCandleData": [
        {
        "date": "2020-11-02",
        "open": "6.95",
        "high": "7.2",
        "low": "4.7",
        "close": "5.3",
        "ltp": "5.3",
        "volume": "138000"
        },
        {
        "date": "2020-11-03",
        "open": "5.35",
        "high": "6.8",
        "low": "5.1",
        "close": "5.55",
        "ltp": "5.55",
        "volume": "190200"
        },
        {
        "date": "2020-11-04",
        "open": "5.3",
        "high": "10.5",
        "low": "5.0",
        "close": "6.75",
        "ltp": "6.75",
        "volume": "603900"
        },
        {
        "date": "2020-11-05",
        "open": "7.95",
        "high": "8.0",
        "low": "5.9",
        "close": "6.45",
        "ltp": "6.45",
        "volume": "301800"
        }
      ]
    }
  ```
</details>

<details>
  <summary>Sample HistoricalCandleData Request/Response  for Currency segment</summary>
  
Request :
  ```python
  samco.get_historical_candle_data(symbol_name='USDINR20DEC75CE',exchange=samco.EXCHANGE_CDS, from_date='2020-11-01',to_date='2020-11-05')
  ```
Respone:
  ```python
  {
    "serverTime": "20/11/20 12:19:38",
    "msgId": "e8c08a30-289e-458e-a14b-e85f173ace0b",
    "status": "Success",
    "statusMessage": "Historical candle data retrieved successfully",
    "historicalCandleData": [
      {
      "date": "2020-11-02",
      "open": "0.0",
      "high": "0.0",
      "low": "0.0",
      "close": "0.6575",
      "ltp": "0.6575",
      "volume": "0"
      },
      {
      "date": "2020-11-03",
      "open": "0.0",
      "high": "0.0",
      "low": "0.0",
      "close": "0.6575",
      "ltp": "0.6575",
      "volume": "0"
      },
      {
      "date": "2020-11-04",
      "open": "0.0",
      "high": "0.0",
      "low": "0.0",
      "close": "0.6575",
      "ltp": "0.6575",
      "volume": "0"
      },
      {
      "date": "2020-11-05",
      "open": "0.0",
      "high": "0.0",
      "low": "0.0",
      "close": "0.725",
      "ltp": "0.725",
      "volume": "0"
      }
    ]
  }    
  ```
</details>

<details>
  <summary>Sample HistoricalCandleData Request/Response  for Commodity segment</summary>
  
Request :
  ```python
samco.get_historical_candle_data(symbol_name='SILVER20DECFUT',exchange=samco.EXCHANGE_MCX, from_date='2020-11-01',to_date='2020-11-05')

  ```
Respone:
  
  ```python
  {
      "serverTime": "20/11/20 12:22:07",
      "msgId": "c0bf5f3a-bfd8-4b81-815a-55fd3045ae45",
      "status": "Success",
      "statusMessage": "Historical candle data retrieved successfully",
      "historicalCandleData": [
        {
        "date": "2020-11-02",
        "open": "61422.0",
        "high": "62272.0",
        "low": "61330.0",
        "close": "62007.0",
        "ltp": "60865.0",
        "volume": "26238"
        },
        {
        "date": "2020-11-03",
        "open": "61987.0",
        "high": "62791.0",
        "low": "61612.0",
        "close": "62685.0",
        "ltp": "62007.0",
        "volume": "24837"
        },
        {
        "date": "2020-11-04",
        "open": "61420.0",
        "high": "62335.0",
        "low": "60800.0",
        "close": "61389.0",
        "ltp": "62685.0",
        "volume": "38258"
        },
        {
        "date": "2020-11-05",
        "open": "62020.0",
        "high": "64380.0",
        "low": "61900.0",
        "close": "64253.0",
        "ltp": "61389.0",
        "volume": "35098"
        }
      ]
    }
  ```
</details>

<a name="indexHistoricalCandleData"/>

### IndexHistoricalCandleData:
The IndexHistoricalCandleData function `get_index_candle_data()` gets the Index historical candle data such as Open, high, low, close, last traded price and volume within specific dates for a specific index. From date is mandatory. End date is optional and defaults to Today.

#### Parameters:
```python
index_name,from_date,to_date
```

<details>
  <summary>Sample IndexHistoricalCandleData Request</summary>
  
  ```python
samco.get_index_candle_data(index_name='NIFTY 200', from_date='2019-05-24',to_date='2019-05-29')

  ```
</details>

<details>
  <summary>Sample IndexHistoricalCandleData Response</summary>
  
  ```python

{
  "serverTime": "17/06/20 11:39:11",
  "msgId": "bb015c56-74e5-401b-bfe0-e2c9c415d088",
  "status": "Success",
  "statusMessage": "Index HistoricalCandle data retrieved successfully ",
  "indexCandleData": [
    {
      "date": "2019-05-24",
      "open": "6067.65",
      "high": "6134.4",
      "low": "6029.9",
      "close": "6129.8",
      "ltp": "6129.8",
      "volume": "0"
    },
    {
      "date": "2019-05-27",
      "open": "6134.35",
      "high": "6189.0",
      "low": "6114.5",
      "close": "6177.15",
      "ltp": "6177.15",
      "volume": "0"
    },
    {
      "date": "2019-05-28",
      "open": "6195.7",
      "high": "6195.7",
      "low": "6151.25",
      "close": "6181.35",
      "ltp": "6181.35",
      "volume": "0"
    },
    {
      "date": "2019-05-29",
      "open": "6172.55",
      "high": "6178.85",
      "low": "6132.0",
      "close": "6143.8",
      "ltp": "6143.8",
      "volume": "0"
    }
  ]
}      
  ```
</details>

            
<a name="streamingData"/>

## StreamingData

StockNote API platform provides the Broadcast API, as the most effective way to receive quote data for instruments across all exchanges during live market hours. The API provides continuous streaming data of quote based on user request, and primarily consists of fields such as last traded price, open, high, low, close, last traded quantity, last traded volume, last traded time etc.

The API uses WebSocket protocol to establish a dedicated TCP connection after an HTTP handshake to receive streaming quotes and thereby provides seamless streaming of quote data. You need to use a WebSocket client to connect to our broadcast API. If you have already subscribed to our StockNote API services, you will be able to access broadcast API too.


<details>
  <summary>Sample Positions Request</summary>

    value=[{"symbol":"-53"},{"symbol":"1143_CDS"},{"symbol":"1270_NSE"},{"symbol":"10604_NSE"},{"symbol":"11195_NSE"}]
    samco.set_streaming_data(value)
    samco.start_streaming()

</details>


<details>
  <summary>Sample Positions Response</summary>

      Message Arrived:{"response":{"data":{"aPr":"0.00","aSz":"0","avgPr":"0.00","bPr":"0.00", "bSz":"0","c":"29.65","ch":"0.38","chPer":"1.28",
      "h":"30.28","l":"27.24","lTrdT":"09 Jun 2020, 02:11:58 PM","ltp":"30.03","ltq":"0","ltt":"09 Jun 2020, 02:11:58 PM","lttUTC":"09 Jun 2020, 08:41:58 AM",
      "o":"29.65","oI":"","oIChg":"","sym":"-53","tBQ":"0","tSQ":"0","ttv":"0.00","vol":"0","yH":"0.00","yL":"0.00"},"streaming_type":"quote"}}

      Message Arrived:{"response":{"data":{"aPr":"0.00","aSz":"0","avgPr":"0.00","bPr":"0.00", "bSz":"0","c":"29.65","ch":"0.38","chPer":"1.28",
      "h":"30.28","l":"27.24","lTrdT":"09 Jun 2020, 02:11:58 PM","ltp":"30.03","ltq":"0","ltt":"09 Jun 2020, 02:11:58 PM","lttUTC":"09 Jun 2020, 08:41:58 AM",
      "o":"29.65","oI":"","oIChg":"","sym":"-53","tBQ":"0","tSQ":"0","ttv":"0.00","vol":"0","yH":"0.00","yL":"0.00"},"streaming_type":"quote"}}

 </details>


<a name="logout"/>

## Logout
Logging out user from the application.
The Logout function name in python is `logout()`

<details>
  <summary>Sample Logout Request</summary>
  
  ```python
samco.logout()
  ```
</details>

<details>
  <summary>Sample Logout Response</summary>
  
  ```python
{
  "serverTime" : "17/06/20 12:27:52",
  "msgId" : "41627994-5c96-411c-b15c-dbda00029269",
  "status" : "Success",
  "statusMessage" : "User has successfully logged out"
}
  ```
</details>

## Constant List:
This section contains the list of possible constant values that can be passed for input attributes like exchanges, product types etc.

<details>
  <summary>Product types</summary>
  
 	PRODUCT_MIS 
    PRODUCT_CNC
    PRODUCT_NRML
    PRODUCT_CO
    PRODUCT_BO
   
    Example:- "productType":sn.constants.PRODUCT_MIS
</details>
   
<details>
  <summary>Exchanges</summary>

    EXCHANGE_NSE
    EXCHANGE_BSE
    EXCHANGE_NFO
    EXCHANGE_CDS
    EXCHANGE_MCX
   
    Example:- "exchange":sn.constants.EXCHANGE_NFO
</details>

<details>
  <summary>Transaction types</summary>

    TRANSACTION_TYPE_BUY
    TRANSACTION_TYPE_SELL
   
    Example:- "transactionType":sn.constants.TRANSACTION_TYPE_BUY
</details>
   
<details>
  <summary>Order types</summary>
  
    ORDER_TYPE_MARKET
    ORDER_TYPE_LIMIT 
    ORDER_TYPE_SLM 
    ORDER_TYPE_SL 
   
    Example:- "orderType": sn.constants.ORDER_TYPE_LIMIT
</details>  

<details>
  <summary>Validity types</summary> 
   
    VALIDITY_DAY 
    VALIDITY_IOC 
 
    Example:- "orderValidity": sn.constants.VALIDITY_DAY
</details>

<details>
  <summary>Position types</summary>
   
    POSITION_TYPE_DAY
    POSITION_TYPE_NET
 
    Example:- "positionType": sn.constants.POSITION_TYPE_DAY
</details>

<details>
  <summary>Intervals</summary>

    INTERVAL_1MIN
    INTERVAL_5MIN 
    INTERVAL_10MIN
    INTERVAL_15MIN
    INTERVAL_30MIN
    INTERVAL_60MIN
    Example:- "interval": sn.constants.INTERVAL_10MIN
</details>

   
   
   
  