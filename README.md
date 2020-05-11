# mt4-web-trader
Backend part of web trader based on mt4 manager api

# Endpoints

## Symbols

GET /symbols

retrun:
`
{
  ["EURUSD", "GBPUSD"]
}
`

## Symbols history data

GET /symbols/{symbol}/{period}/{from}/{count}

return:

`
{
  "symbol": "EURUSD",
  "period": M1,
  "data": [
  {
    "time": 1231313,
    "bid": 1.222,
    "ask": 1.333,
    "o": 1.444,
    "h": 1.333,
    "l": 1.555,
    "c": 1.666
  }
  ]
}
`

## User authorize

POST /auth/login

params: login, passowrd

returns: 

`
{
  "code": 0,
  "expire": "string",
  "token": "string"
}
`

## Trades. Returns live trades

GET trades/{login}

headers: Authorization {token}

returns:

`{
  "close_price": 0,
  "close_time": 0,
  "cmd": 0,
  "comment": "string",
  "digits": 0,
  "expiration": 0,
  "login": 0,
  "magic": 0,
  "open_price": 0,
  "open_time": 0,
  "profit": 0,
  "sl": 0,
  "symbol": "string",
  "ticket": 0,
  "tp": 0,
  "volume": 0
}`

## Trades. Update open trade

headers: Authorization {token}

PATCH trades/update

params:

`
{
  "price": 1.1456,
  "sl": 1.1456,
  "ticket": 101,
  "tp": 1.1456
}
`

return:

`{
  "code": 400,
  "message": "status bad request"
}`

## Trades. CLose open trade

PATCH /trades/close

headers: Authorization {token}

params:

`
{
  "ticket": 101,
  "volume": 0.1
}
`

return:

`
{
  "code": 400,
  "message": "status bad request"
}
`

# Websocket endponts

## Quotes

real-time quotes

path: /ws/quotes

header: manager token

data:

`
{
	"symbol": "EURUSD",
	"ask": 1.1212,
	"bid": 1.1.11,
	"time": 123123213
}
`

## Trades

real-time event of trade. open, close, modify

path: /ws/trades

header: token

data:

`
{
	"ticket" 1,
	"symbol": "",
	"digits": 4,
	"cmd": 1,
	"volume":0.1,
	"open_time": 12313,
	"open_price": 1.1232,
	"close_time": 12313,
	"close_price": 1.23232,
	"sl": 1.23424,
	"tp": 1.2323,
	"comment": "test",
	"expiration": 123123,
	"profit": 45.44,
	"magic": 123
}
`

## Trade Profits

real-time event of each trade P/L update

path: /ws/trade_profits

header: token

data:

`
{
  "ticket": 12123,
  "pl": 12.23
}
`

## Margins

real-time update of user marging, balance,

path: /ws/margins

header: token

data:

`
{
  "balance": 12.22
  "margin": 23.22,
  "free_margin": 32.23
}
`
