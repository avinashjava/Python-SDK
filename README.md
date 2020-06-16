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
## Login sample request:
  ```python
  print(samco.login(body={"userId":'*****','password':'*****','yob':'****'}))
  ##this will return a user details and generated session token
  ```
 ## Login response:
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

