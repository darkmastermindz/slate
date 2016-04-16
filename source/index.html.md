---
title: API Reference

language_tabs:
  - shell
  - ruby
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Alexandria API! You can use our API to access Alexandria.io API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

<aside class="notice">
Follow these instructions to run install Daemons locally so you can run these APIs in a fully decentralized way instead of relying on "Trusted Third Parties"<code>meowmeowmeow</code>.
</aside>

# Publishers

## Get All Publishers

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://libraryd.alexandria.io/alexandria/v1/publisher/get/all"
```

> The above command returns JSON structured like this:

```json
[
    {
        "publisher-data": {
            "alexandria-publisher": {
                "name": "Imogen Heap",
                "address": "FAiWWyUEuXkxo7oQLWfD3oTWkHM6eu5JJH",
                "timestamp": 1443896107000,
                "emailmd5": "06b762d6e133b3dee9a62575a3babf1f",
                "bitmessage": ""
            },
            "signature": "H/7+wbTjR87fv2Qy96jp3oCfBdu9o/D5rzgA74UGSb/4f0iACwd/5YyehJ0y/uSaRwW3Tk6uT8x+OJZL3kro9hQ="
        },
        "txid": "bf3c92f97728a4f0875cd837af0851cd340d855346928dc047157a07cf874214",
        "block": 1397171
    }
]
```

This endpoint retrieves all Publishers in the Alexandria library index.

### HTTP Request

`GET http://libraryd.alexandria.io/alexandria/v1/publisher/get/all`

<aside class="success">
Note — if you have Libraryd running locally, you can also use this local API endpoint:<code>GET http://localhost:41289/alexandria/v1/publisher/get/all</code>
</aside>

## Get a Specific Publisher

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
[
    {
        "publisher-data": {
            "alexandria-publisher": {
                "name": "Imogen Heap",
                "address": "FAiWWyUEuXkxo7oQLWfD3oTWkHM6eu5JJH",
                "timestamp": 1443896107000,
                "emailmd5": "06b762d6e133b3dee9a62575a3babf1f",
                "bitmessage": ""
            },
            "signature": "H/7+wbTjR87fv2Qy96jp3oCfBdu9o/D5rzgA74UGSb/4f0iACwd/5YyehJ0y/uSaRwW3Tk6uT8x+OJZL3kro9hQ="
        },
        "txid": "bf3c92f97728a4f0875cd837af0851cd340d855346928dc047157a07cf874214",
        "block": 1397171
    }
]
```

This endpoint retrieves a specific Publisher.

### HTTP Request

`POST http://libraryd.alexandria.io/alexandria/v1/search`

### URL Parameters

Parameter | Description
--------- | -----------
protocol | "<code>publisher</code>",
search-on | "<code>address</code>, <code>name</code>, <code>emailmd5</code>, <code>bitmessage</code> or <code>txid</code>",
search-for | "<code>search string</code>"

### Optional URL Parameters

Parameter | Description
--------- | -----------
search-like | <code>true</code> or <code>false</code>

<aside class="success">
The POST data should be a json encoded string
</aside>

<aside class="success">
Note — if you have Libraryd running locally, you can also use this local API endpoint:<code>GET http://localhost:41289/alexandria/v1/search</code>
</aside>

## Sign Publisher Announcement Message

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://localhost:41289/alexandria/v1/sign"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
    "status": "success",
    "response": [
        "<code>signature</code>"
    ]
}
```

This endpoint is used to sign a Publisher announcement message.

<aside class="warning">This endpoint currently communicates only with a local wallet via RCP. To use it, install Librarian and turn on <code>Florincoin</code> and <code>Libraryd</code>.</aside>

### HTTP Request

`POST http://localhost:41289/alexandria/v1/sign`

### URL Parameters

Parameter | Description
--------- | -----------
address | "<code>florincoin address</code>"
text | "<code>publisher name</code>-<code>florincoin address</code>-<code>unixtime</code>"

<aside class="success">
The POST data should be a json encoded string
</aside>

## Announce New Publisher

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://localhost:41289/alexandria/v1/send"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
    "status": "success",
    "response": [
        "<code>florincoin tx-id of publisher announcement</code>"
    ]
}
```

This endpoint is used to announce a new Publisher using the signature created by the previous endpoint.

<aside class="warning">This endpoint currently communicates only with a local wallet via RCP. To use it, install Librarian and turn on <code>Florincoin</code> and <code>Libraryd</code>.</aside>

### HTTP Request

`POST http://localhost:41289/alexandria/v1/send`

### URL Parameters

Parameter | Description
--------- | -----------
alexandria-publisher: | {
name | "<code>publisher name</code>",
address | "<code>florincoin address</code>",
timestamp | <code>unixtime</code>,
bitmessage | "<code>bitmessage address</code>",
emailmd5 | "<code>md5 hash of email</code>"
 | },
signature | "<code>signature</code>"

<aside class="success">
The POST data should be a json encoded string
</aside>

<aside class="success">
For the new Publisher announcement to be considered valid, the <code>bitmessage</code> and <code>emailmd5</code> fields must be included, but they can be submitted empty.
</aside>

# Artifacts

## Get All Artifacts

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://libraryd.alexandria.io/alexandria/v1/media/get/all"
```

> The above command returns JSON structured like this:

```json
[
{
    "media-data": {
        "alexandria-media": {
            "torrent": "QmTHG1ieXUA9a8cEMzEAR9qC7B2DXMCtmZZdwYQhdJc4HZ",
            "publisher": "FAiWWyUEuXkxo7oQLWfD3oTWkHM6eu5JJH",
            "timestamp": 1445935671000,
            "type": "music",
            "info": {
                "title": "Tiny Human",
                "description": "Tiny Human ISRCGBJPX1500151 Tiny Human (instrumental) ISRCGBJPX1500152 Published by Megaphonic Publishing Record label - Megaphonic Records copyright 2015 for information on use of sync please contact Info@imogenheap.com",
                "year": 2015,
                    "extra-info": {
                        "Bitcoin Address": "16diWTDN8DUxsX994WzyNAotVp36qBqXku",
                        "DHT Hash": "QmTHG1ieXUA9a8cEMzEAR9qC7B2DXMCtmZZdwYQhdJc4HZ",
                        "artist": "Imogen Heap",
                        "company": "Megaphonic Records",
                        "coverArt": "Imogen_Heap_Tiny_Human_cover.jpg",
                        "element1": {
                            "flac": "Imogen_Heap_Tiny_Human.flac",
                            "mp3": "Imogen_Heap_Tiny_Human.mp3",
                            "name": "Tiny Human"
                        },
                        "filename": "Imogen_Heap_Tiny_Human.mp3",
                        "pwyw": "1,0.6",
                        "runtime": 260,
                        "tags": "Mycelia"
                    }
                },
                "payment": {
                    "amount": "1,10,50",
                    "currency": "USD",
                    "pinners": {
                        "disc_amount": "50",
                        "disc_thresh": "1000",
                        "free": "500"
                    },
                    "pricing": {
                        "element1": "6,10,700,990"
                    },
                    "promoters": "10",
                    "sug_tip": "1,11,51",
                    "type": "tip"
                },
                "extras": ""
            },
            "signature": "H27r7UxUb8BozjEvV0v++nCyRI7S6yyroeKCJQpgU5NO3CP6FpXWs5kCxy8vhmMhbtpj/FMj+8s3+updw7g+bmE="
    },
    "txid": "fc9220025df5f2bf76fcda8f66bced4c95846e136ff3f5ff4c36fede3a5e3fc5",
    "block": 1440095,
    "publisher-name": "Imogen Heap"
}
]
```

This endpoint retrieves all Artifacts in the Alexandria library index.

### HTTP Request

`GET http://libraryd.alexandria.io/alexandria/v1/media/get/all`

<aside class="success">
Note — if you have Libraryd running locally, you can also use this local API endpoint:<code>GET http://localhost:41289/alexandria/v1/media/get/all</code>
</aside>

## Get a Specific Artifact

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://libraryd.alexandria.io/alexandria/v1/search"
```

> The above command returns JSON structured like this:

```json
[
{
    "media-data": {
        "alexandria-media": {
            "torrent": "QmTHG1ieXUA9a8cEMzEAR9qC7B2DXMCtmZZdwYQhdJc4HZ",
            "publisher": "FAiWWyUEuXkxo7oQLWfD3oTWkHM6eu5JJH",
            "timestamp": 1445935671000,
            "type": "music",
            "info": {
                "title": "Tiny Human",
                "description": "Tiny Human ISRCGBJPX1500151 Tiny Human (instrumental) ISRCGBJPX1500152 Published by Megaphonic Publishing Record label - Megaphonic Records copyright 2015 for information on use of sync please contact Info@imogenheap.com",
                "year": 2015,
                    "extra-info": {
                        "Bitcoin Address": "16diWTDN8DUxsX994WzyNAotVp36qBqXku",
                        "DHT Hash": "QmTHG1ieXUA9a8cEMzEAR9qC7B2DXMCtmZZdwYQhdJc4HZ",
                        "artist": "Imogen Heap",
                        "company": "Megaphonic Records",
                        "coverArt": "Imogen_Heap_Tiny_Human_cover.jpg",
                        "element1": {
                            "flac": "Imogen_Heap_Tiny_Human.flac",
                            "mp3": "Imogen_Heap_Tiny_Human.mp3",
                            "name": "Tiny Human"
                        },
                        "filename": "Imogen_Heap_Tiny_Human.mp3",
                        "pwyw": "1,0.6",
                        "runtime": 260,
                        "tags": "Mycelia"
                    }
                },
                "payment": {
                    "amount": "1,10,50",
                    "currency": "USD",
                    "pinners": {
                        "disc_amount": "50",
                        "disc_thresh": "1000",
                        "free": "500"
                    },
                    "pricing": {
                        "element1": "6,10,700,990"
                    },
                    "promoters": "10",
                    "sug_tip": "1,11,51",
                    "type": "tip"
                },
                "extras": ""
            },
            "signature": "H27r7UxUb8BozjEvV0v++nCyRI7S6yyroeKCJQpgU5NO3CP6FpXWs5kCxy8vhmMhbtpj/FMj+8s3+updw7g+bmE="
    },
    "txid": "fc9220025df5f2bf76fcda8f66bced4c95846e136ff3f5ff4c36fede3a5e3fc5",
    "block": 1440095,
    "publisher-name": "Imogen Heap"
}
]
```

This endpoint retrieves all Artifacts in the Alexandria library index that match the search criteria.

### HTTP Request

`POST http://libraryd.alexandria.io/alexandria/v1/search`

### URL Parameters

Parameter | Description
--------- | -----------
protocol | "<code>media</code>"
search-on | "<code>publisher</code>", "<code>timestamp</code>", "<code>type</code>",or "<code>*</code>" to search all fields
search-for | "<code>search string</code>"

### Optional URL Parameters

Parameter | Description
--------- | -----------
"search-like" | <code>true</code> or <code>false</code>,

<aside class="success">
The POST data should be a json encoded string
</aside>

<aside class="success">
Note — if you have Libraryd running locally, you can also use this local API endpoint:<code>POST http://localhost:41289/alexandria/v1/search</code>
</aside>

## Sign Artifact Publish Message

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://localhost:41289/alexandria/v1/sign"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
    "status": "success",
    "response": [
        "<signature>"
    ]
}
```

This endpoint is used to sign a Publisher announcement message.

<aside class="warning">This endpoint currently communicates only with a local wallet via RCP. To use it, install Librarian and turn on <code>Florincoin</code> and <code>Libraryd</code>.</aside>

### HTTP Request

`POST http://localhost:41289/alexandria/v1/sign`

### URL Parameters

Parameter | Description
--------- | -----------
address | "<code>florincoin address</code>"
text | "<code>primary ipfs hash</code>-<code>florincoin address</code>-<code>unixtime</code>"

<aside class="success">
The POST data should be a json encoded string
</aside>

## Publish New Artifact

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://localhost:41289/alexandria/v1/send"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
    "status": "success",
    "response": [
        "<florincoin tx-id of artifact's main tx>"
    ]
}
```

This endpoint is used to announce a new Publisher using the signature created by the previous endpoint.

<aside class="warning">This endpoint currently communicates only with a local wallet via RCP. To use it, install Librarian and turn on <code>Florincoin</code> and <code>Libraryd</code>.</aside>

### HTTP Request

`POST http://localhost:41289/alexandria/v1/send`

### URL Parameters

Parameter | Description
--------- | -----------
alexandria-media | {
torrent | "<code>location hash</code>",
publisher | "<code>publisher florincoin address</code>",
timestamp | <code>unixtime</code>,
type | "<code>music</code>","<code>video</code>","<code>podcast</code>","<code>book</code>","<code>movie</code>","<code>thing</code>" or "<code>html</code>",
payment | {},
info | {
title | "<code>artifact title</code>",
description | "<code>artifact description</code>",
year | <code>artifact creation year</code>,
extra-info | {
filename | "<code>file name[]</code>",
runtime | "<code>file runtime[]</code>"
 | }}}, 
signature | "<code>signature</code>" 

### Optional URL Parameters

Parameter | Description
--------- | -----------
extra-info | {
artist | "<code>content creator</code>"
company | "<code>company in possession of distribution rights for content</code>"
tags | "<code>tags[]</code>"
displayName | "<code>file display name[]</code>"
 | } 
payment | {
fiat | "<code>preferred fiat currency pricing</code>",
paymentToken | "<code>preferred cryptocurrency</code>",
paymentAddress | "<code>preferred cryptocurrency payment address</code>",
suggPlayPrice | "<code>Play Price Suggestion[]</code>",
minPlayPrice | "<code>Play Price Minimum[]</code>",
suggBuyPrice | "<code>Buy Price Suggestion[]</code>",
minBuyPrice | "<code>Buy Price Minimum[]</code>",
suggTips | "<code>Suggested Tip Ammount[1]</code>","<code>Suggested Tip Ammount[2]</code>",
 | "<code>Suggested Tip Ammount[3]</code>"
promotersRate | "<code>Discount Rate For Promoters</code>",
pinToPlay | {
ptpFreeThreshold | "<code>Number of Pin To Play for Free Users at any given time[]</code>",
ptpDiscThreshold | "<code>Number of Pin to Play for Discount Users at any given time[]</code>",
ptpDiscAmount | "<code>Discount Rate for Pin to Play Users beyond the Free Threshold</code>"
 | }
 | }

<aside class="success">
The POST data should be a json encoded string
</aside>


# Florincoin

## Get Market Data

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://libraryd.alexandria.io:41290/flo-market-data/v1/getAll"
```

> The above command returns JSON structured like this:

```json
{
    "unixtime": 1460840591,
    "cryptsy": "0.0000",
    "poloniex": "0.9262",
    "bittrex": "0.0738",
    "daily-volume": "182473.54687500",
    "weighted": "0.00000438",
    "USD": "0.00190"
}
```

This endpoint retrieves current Florincoin token market data, including its trade price against BTC on 3rd party exchanges Poloniex and Bittrex. The field <code>weighted</code> is a calculated average token value for FLO/BTC weighted by the 24-hour volume of each exchange. The field <code>USD</code> is calculated from <code>weighted</code> using data from the 3rd party service <code>api.bitcoinaverage.com</code>.

### HTTP Request

`GET http://libraryd.alexandria.io:41290/flo-market-data/v1/getAll`

<aside class="success">
Note — if you have Libraryd running locally, you can also use this local API endpoint:<code>GET http://localhost:41289/alexandria/v1/media/get/all</code>
</aside>

## Get Blockchain Mining Info

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://florincoin.alexandria.io/getMiningInfo"
```

> The above command returns JSON structured like this:

```json
{
    "blocks": 1714586,
    "currentblocksize": 0,
    "currentblocktx": 0,
    "difficulty": 26.03072741,
    "errors": "",
    "generate": false,
    "genproclimit": -1,
    "hashespersec": 0,
    "networkhashps": 1804091648,
    "pooledtx": 1,
    "testnet": false
}
```

This endpoint retrieves current Florincoin blockchain information, including its total network hashrate, difficutly and current block height.

### HTTP Request

`GET http://florincoin.alexandria.io/getMiningInfo`

<aside class="success">
Note — if you have Libraryd running locally, you can also use this local API endpoint:<code>GET http://localhost:41289/alexandria/v1/media/get/all</code>
</aside>

## Get Rental Data for Scrypt Rigs from Miningrigrentals.com (third party service)

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "https://www.miningrigrentals.com/api/v1/rigs?method=list&type=scrypt&max_cost=0.00001"
```

> The above command returns JSON structured like this:

```json
{
    "success": true,
    "version": "1",
    "data": {
        "info": {
            "start_num": 1,
            "end_num": 100,
            "total": "248",
            "available": {
                "rigs": "158",
                "hash": "31612538674"
            },
            "rented": {
                "rigs": "90",
                "hash": "13542513000"
            },
            "price": {
                "lowest": "0.000103",
                "last_10": "0.000131139000",
                "last": "0.0001089"
            }
        },
        "records": []
    }
}
```

This endpoint retrieves current Florincoin blockchain information, including its total network hashrate, difficutly and current block height.

### HTTP Request

`GET https://www.miningrigrentals.com/api/v1/rigs?method=list&type=scrypt&max_cost=0.00001`

<aside class="success">
Note — the specific arguments in this endpoint are intended to reveal only the rental prices of currently rented Scrypt mining rigs. To search for rigs currently available to be rented, exclude the argument <code>max_cost=0.00001</code>.
</aside>

## Search Florincoin tx-comments

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://florincoin.alexandria.io:5831/searchTxComment"
```

> The above command returns JSON structured like this:

```json
[
    {
        "Hash": "a79bdd6532bfab790fb30eaa8a1751fe54bf2011ef08d8da9be9ca2fcbc04475",
        "Message": "alexandria-media-multipart(1,2,FKVt3L7z6z8QDVG35Kif3tsReWACmNQVo7,c5834dc707fe9ea1f44c74064fd53313a688588020cacb5691e642a0531fdb79,IBBeLPqfwPFYfJQbGDDzMLl1CzDAql+vK1mjIz5XsejcCS5Okfi9ETKxXr3AGcvtu7bEZLHk0sIAcYFEqyESl9c=):nfo\":\n      {\n        \"DHT Hash\":\"QmWRkWn9NPA1zY1FobYqPSWaBjgj3rqZjVNJEdik5122fD\",\n        \"element1\":\n        {\n          \"name\":\"Chick-A-Layin Instrumental\",\n          \"flac\":\"chick-a-layin.flac\"\n        }\n      }\n    }  \n  },\n  \"signature\":\"H8+kK8I2zVwui5adAWvpUVn4WI"
    }
]
```

This endpoint retrieves all Florincoin transaction comments matching a given search query.

### HTTP Request

`POST http://florincoin.alexandria.io:5831/searchTxComment`

### URL Parameters

Parameter | Description
--------- | -----------
search | "<code>search query</code>"
results-per-page | <code>number of results per page</code>(integer)
page | <code>page number for paginated results</code>(integer)

<aside class="success">
The POST data should be a json encoded string
</aside>

# Alexandria's No-Accounts Mining Pool

## Get Alexandria's Pool Stats

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://pool.alexandria.media/api/stats"
```

> The above command returns JSON structured like this:

```json
{
    "time": 1460842179,
    "global": {
        "workers": 2,
        "hashrate": 0
    },
    "algos": {
        "scrypt": {
            "workers": 2,
            "hashrate": 128073013.6777632,
            "hashrateString": "128.07 MH"
        }
    },
    "pools": {
        "florincoin": {
            "name": "florincoin",
            "symbol": "FLO",
            "algorithm": "scrypt",
            "poolStats": {
                "validShares": "167493",
                "validBlocks": "577",
                "invalidShares": "480",
                "totalPaid": "8657.95307198000001314"
            },
            "blocks": {
                "pending": 10,
                "confirmed": 552,
                "orphaned": 0
            },
            "workers": {
                "FTAGReXCGcFtfjU2mtMAs3T1GZ4wMKYxpc": {
                    "shares": 10752,
                    "invalidshares": 0,
                    "hashrateString": "2.35 MH"
                },
                "FRY8aEM6PZqkeMCAfgEQikevdZmXrumiKu": {
                    "shares": 575519.7300922998,
                    "invalidshares": 0,
                    "hashrateString": "125.72 MH"
                }
            },
            "hashrate": 128073013.6777632,
            "workerCount": 2,
            "hashrateString": "128.07 MH"
        }
    }
}
```

This endpoint retrieves current summary stats for the Alexandria mining pool, including which tokens are currently being mined, how many workers are contributing to each and their hash rates.

### HTTP Request

`GET http://pool.alexandria.media/api/stats`

## Get Last 24 Hours of Alexandria's Pool Stats

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://pool.alexandria.media/api/pool_stats"
```

> The above command returns JSON structured like this:

```json
[
    {
        "time": 1460799148,
        "pools": {
            "florincoin": {
                "hashrate": 75168256.05864379,
                "workerCount": 2,
                "blocks": {
                    "pending": 29,
                    "confirmed": 502,
                    "orphaned": 0
                }
            }
        }
    },
]    
```

This endpoint retrieves the past 24 hours of summary stats for the Alexandria mining pool, including which tokens are currently being mined, how many workers are contributing to each and their total hash. One record is returned for each 20 second interval between now and exactly 24 hours ago.

### HTTP Request

`GET http://pool.alexandria.media/api/pool_stats`

## Get Alexandria's Pool Live Stats

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://pool.alexandria.media/api/pool_stats"
```

> The above command returns JSON structured like this:

```json
{
    "data": {
        "time":1460842980,
        "global": {
            "workers":2,
            "hashrate":0
        },
        "algos": {
            "scrypt": {
                "workers":2,
                "hashrate":162605649.03394008,
                "hashrateString":"162.61 MH"
            }
        },
        "pools": {
            "florincoin": {
                "name":"florincoin",
                "symbol":"FLO",
                "algorithm":"scrypt",
                "poolStats": {
                    "validShares":"167674",
                    "validBlocks":"577",
                    "invalidShares":"480",
                    "totalPaid":"8657.95307198000001314"
                },
                "blocks": {
                    "pending":10,
                    "confirmed":552,
                    "orphaned":0
                },
                "workers": {
                    "FRY8aEM6PZqkeMCAfgEQikevdZmXrumiKu": {
                        "shares":740509.5896939395,
                        "invalidshares":0,
                        "hashrateString":"161.77 MH"
                    },
                    "FTAGReXCGcFtfjU2mtMAs3T1GZ4wMKYxpc": {
                        "shares":3840,
                        "invalidshares":0,
                        "hashrateString":"838.86 KH"
                    }
                },
                "hashrate":162605649.03394008,
                "workerCount":2,
                "hashrateString":"162.61 MH"
            }
        }
    }
}
```

This endpoint retrieves live summary stats for the Alexandria mining pool, including which tokens are currently being mined, how many workers are contributing to each and their total hash. One new record is added every 20 seconds.

### HTTP Request

`GET http://pool.alexandria.media/api/pool_stats`





