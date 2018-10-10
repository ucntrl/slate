---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>


search: true
---

# Introduction

Welcome to the Zeno API!

Zeno REST & Streaming API version 1.0 provides programmatic access to cryptocurrency live pricing data and OHLC historical data.

By using Zeno API you confirm that you have read and accept [API License Agreement][https://zenotrader.com/api-license-agreement]

# Development Guide

## API Explorer

You can explore API using [SwaggerUI](https://api.zenotrader.com/explorer/v1)

## API URLs

**Production environment:**

Type | URL
-----|-----
REST | https://api.zenotrader.com/api/v1/
Streaming | wss://api.zenotrader.com/ws/v1


# REST API Reference

## HTTP Status codes

* 200 OK Successful request
* 400 Bad Request. Returns JSON with the error message
* 401 Unauthorized. Authorisation required or failed
* 403 Forbidden. Action is forbidden for API key
* 500 Internal Server. Internal Server Error
* 503 Service Unavailable. Service is down for maintenance
* 504 Gateway Timeout. Request timeout expired

# Authorisation

### HTTP Request

`POST https://api.zenotrader.com/api/v1/auth/signup`
Fields: email, name, password

`POST https://api.zenotrader.com/api/v1/auth/login`
Fields: email, password

`POST https://api.zenotrader.com/api/v1/auth/logout`

```shell

curl "http://api.zenotrader.com/api/v1/auth/logout"
  -H "Authorization: Bearer {JWT}"


# Exchanges

## Get All Exchanges

This endpoint retrieves all supported exchanges.

### HTTP Request

`GET https://api.zenotrader.com/api/v1/exchanges`

```shell

curl "http://api.zenotrader.com/api/v1/exchanges"
  -H "Authorization: Bearer {JWT}"

# The above command returns JSON structured like this:

{
  "exchanges":
  [
    {
      "id": "binance",
      "name": "Binance",
      "active": true,
      "online": true
    },
    {
      "id": "hitbtc",
      "name": "HitBTC",
      "active": true,
      "online": true
    },
    ...
  ]
}

```

<aside class="notice">
You must replace <code>JWT</code> with your JWT.
</aside>

# Currencies & Pairs

## Get All Exchange's Currencies

This endpoint retrieves all supported exchanges.

### HTTP Request

`GET https://api.zenotrader.com/api/v1/exchanges/{exchange_id}/currencies`

```shell

curl "http://api.zenotrader.com/api/v1/exchanges/binance/currencies"
  -H "Authorization: Bearer {JWT}"

# The above command returns JSON structured like this:

{
  "exchange": "zeno",
  "currencies":
  [
    {
      "id": "BTC",
      "name": "Bitcoin",
      "delisted": false
    },
    {
      "id": "ETH",
      "name": "Ethereum",
      "delisted": false
    },
    ...
  ]
}

```

<aside class="notice">
You must replace <code>{JWT}</code> with your JWT.
</aside>


## Get All Pairs

This endpoint retrieves all pairs for specific exchanges.

### HTTP Request

`GET https://api.zenotrader.com/api/v1/candles/{exchange_id}/pairs`

```shell

curl "http://api.zenotrader.com/api/v1/candles/binance/pairs"
  -H "Authorization: Bearer {JWT}"

# The above command returns JSON structured like this:

{
  "exchange": "zeno",
  "pairs":
  [
    {
      "id": "BTCUSD",
      "symbol": "BTC/USD",
      "base": "BTC",
      "quote": "USD",
      'active': true,
      'precision': {
          'price': 8,
          'amount': 8,
          'cost': 8,

      },
      "quantityIncrement": "0.001",
      "tickSize": "0.000001",
      "feeCurrency": "BTC"
    },
    ...
  ]
}

```

<aside class="notice">
You must replace <code>{JWT}</code> with your JWT.
</aside>



# Candles

## Get Candles

This endpoint retrieves candles for specific exchanges, pair and timeframe.

```shell
curl "https://api.zenotrader.com/api/v1/candles/{exchange_id}/{base}/{quote}/{timeframe}"
  -H "Authorization: Bearer {JWT}"
```

> The above command returns JSON structured like this:

```json
{
  "exchange": "zeno",
  "base": "eth",
  "quote": "btc",
  "candles":
  [
    {
      "h": 100.001,
      "o": 95.05,
      "c": 92.75,
      "l": 89.4,
      "ts": 9999999990
    },
    {
      "h": 98.42,
      "o": 92.71,
      "c": 91.15,
      "l": 87.4,
      "ts": 9999999980
    }
  ]
}
```

This endpoint retrieves all kittens.

### HTTP Request

`GET https://api.zenotrader.com/api/v1/candles/{exchange_id}/{base}/{quote}/{timeframe}?offset={offset}&limit={limit}`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
exchange_id | - | ID of the exchange, for example: "zeno"
base | - | ID of the base currency, for example "eth"
quote | - | ID of the quote currency, for example "btc"
timeframe | - | candle timeframe, supported timeframes: m1, m5, m15, m30, h1, d1, w1
offset | current timestamp | timestamp of the first candle
limit | 100 | number of candles to get behind offset  


<aside class="success">
You must replace <code>{JWT}</code> with your JWT.
</aside>
