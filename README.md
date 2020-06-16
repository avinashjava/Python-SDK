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
3. Get the login function so you can login with your Stocknote APi 

### Parameters:

    userId, password, yob
