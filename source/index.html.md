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

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`POST http://libraryd.alexandria.io/alexandria/v1/search`

### URL Parameters

Parameter | Description
--------- | -----------
protocol | <code>publisher</code>
search-on | <code>address</code>, <code>name</code>, <code>emailmd5</code>, <code>bitmessage</code> or <code>txid</code>
search-for | search string

## Announce New Publisher

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

## Publish New Artifact


# Florincoin

## Get Market Data

## Get Blockchain Mining Info

## Get Rental Data for Scrypt Rigs from Miningrigrentals.com (third party service)

## Get Alexandria's Florincoin Pool Stats

## Search Florincoin tx-comments