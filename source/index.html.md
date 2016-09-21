---
title: API Reference

language_tabs:
  - shell
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Alexandria API! You can use our API to access Alexandria.io API endpoints, which can get info about Publishers and Artifacts in the Alexandria library, publish to the library, and retreive other information about Alexandria's networks and blockchain tokens.

We have language bindings in Shell and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

<aside class="notice">
Follow these instructions to run install Daemons locally so you can run these APIs in a fully decentralized way instead of relying on "Trusted Third Parties"<code>Download Librarian</code>.
</aside>

# Publishers

## Get All Publishers

```python
import requests

r = requests.get('https://api.alexandria.io/alexandria/v1/publisher/get/all')
r.json()
```

```shell
curl "https://api.alexandria.io/alexandria/v1/publisher/get/all"
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

`GET https://api.alexandria.io/alexandria/v1/publisher/get/all`

<aside class="success">
Note — if you have Libraryd running locally, you can also use this local API endpoint:<br>
<code>GET http://localhost:41289/alexandria/v1/publisher/get/all</code>
</aside>

## Get a Specific Publisher

```python
import requests, json
payload = {'protocol': 'publisher', 'search-on': 'name', 'search-for': 'Imogen Heap'}

r = requests.post("https://api.alexandria.io/alexandria/v1/search", data=json.dumps(payload))
print(r.text)
```

```shell
curl -X POST -H "Content-Type: application/json" --data '{"protocol":"publisher","search-on":"name","search-for":"Imogen Heap" }' https://libraryd.alexandria.io/alexandria/v1/search
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

`POST https://api.alexandria.io/alexandria/v1/search`

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
Note — if you have Libraryd running locally, you can also use this local API endpoint:<br> 
<code>GET http://localhost:41289/alexandria/v1/search</code>
</aside>

## Sign Publisher Announcement Message

```python
import requests, json
payload = {'address': 'FAiWWyUEuXkxo7oQLWfD3oTWkHM6eu5JJH', 'text': 'Imogen Heap-FAiWWyUEuXkxo7oQLWfD3oTWkHM6eu5JJH-1443896107000'}

r = requests.post("http://localhost:41289/alexandria/v1/sign", data=json.dumps(payload))
print(r.text)
```

```shell
curl -X POST -H "Content-Type: application/json" --data '{"address":"FAiWWyUEuXkxo7oQLWfD3oTWkHM6eu5JJH","text":"Imogen Heap-FAiWWyUEuXkxo7oQLWfD3oTWkHM6eu5JJH-1443896107000" }' http://localhost:41289/alexandria/v1/sign
```

> The above command returns JSON structured like this:

```json
{
    "status": "success",
    "response": [
        "H/7+wbTjR87fv2Qy96jp3oCfBdu9o/D5rzgA74UGSb/4f0iACwd/5YyehJ0y/uSaRwW3Tk6uT8x+OJZL3kro9hQ="
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

```python
import requests, json
payload = {'alexandria-publisher':{'name':'Imogen Heap','address':'FAiWWyUEuXkxo7oQLWfD3oTWkHM6eu5JJH','timestamp':1443896107000,'emailmd5':'06b762d6e133b3dee9a62575a3babf1f','bitmessage':''},'signature':'H/7+wbTjR87fv2Qy96jp3oCfBdu9o/D5rzgA74UGSb/4f0iACwd/5YyehJ0y/uSaRwW3Tk6uT8x+OJZL3kro9hQ='}

r = requests.post("http://localhost:41289/alexandria/v1/send", data=json.dumps(payload))
print(r.text)
```

```shell
curl -X POST -H "Content-Type: application/json" --data '{"alexandria-publisher":{"name":"Imogen Heap","address":"FAiWWyUEuXkxo7oQLWfD3oTWkHM6eu5JJH","timestamp":1443896107000,"emailmd5":"06b762d6e133b3dee9a62575a3babf1f","bitmessage":""},"signature":"H/7+wbTjR87fv2Qy96jp3oCfBdu9o/D5rzgA74UGSb/4f0iACwd/5YyehJ0y/uSaRwW3Tk6uT8x+OJZL3kro9hQ="}' http://localhost:41289/alexandria/v1/send
```

> The above command returns JSON structured like this:

```json
{
    "status": "success",
    "response": [
        "bf3c92f97728a4f0875cd837af0851cd340d855346928dc047157a07cf874214"
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
signature | "<a href="#sign-publisher-announcement-message">signature</a>"

<aside class="success">
The POST data should be a json encoded string
</aside>

<aside class="success">
For the new Publisher announcement to be considered valid, the <code>bitmessage</code> and <code>emailmd5</code> fields must be included, but they can be submitted empty.
</aside>

# Artifacts

## Get All Artifacts

```python
import requests

r = requests.get('https://api.alexandria.io/alexandria/v1/media/get/all')
r.json()
```

```shell
curl "https://api.alexandria.io/alexandria/v1/media/get/all"
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

`GET https://api.alexandria.io/alexandria/v1/media/get/all`

<aside class="success">
Note — if you have Libraryd running locally, you can also use this local API endpoint:<br>
<code>GET http://localhost:41289/alexandria/v1/media/get/all</code>
</aside>

## Get a Specific Artifact

```python
import requests, json
payload = {'protocol': 'media', 'search-on': 'txid', 'search-for': '62a63b3b59b3f5fc786ad05a37af656c88507ae959f53c233520b755aaa8a841'}

r = requests.post("https://api.alexandria.io/alexandria/v1/search", data=json.dumps(payload))
print(r.text)
```

```shell
curl -X POST -H "Content-Type: application/json" --data '{"protocol":"media","search-on":"txid","search-for":"62a63b3b59b3f5fc786ad05a37af656c88507ae959f53c233520b755aaa8a841","search-like":true}' https://libraryd.alexandria.io/alexandria/v1/search
```

> The above command returns JSON structured like this:

```json
{
    "media-data": {
        "alexandria-media": {
            "torrent": "QmcZVwZ5RGamnaxwgB8ZUE9WCjG1nU9rEaDNV5wy9jJP3S",
            "publisher": "FAiWWyUEuXkxo7oQLWfD3oTWkHM6eu5JJH",
            "timestamp": 1444032978000,
            "type": "video",
            "info": {
                "title": "Tiny Human Music Video",
                "description": "Tiny Human ISRCGBJPX1500151 Tiny Human (instrumental) ISRCGBJPX1500152 Published by Megaphonic Publishing Record label - Megaphonic Records copyright 2015 for information on use of sync please contact Info@imogenheap.com",
                "year": 2015,
                "extra-info": {
                    "Bitcoin Address": "16diWTDN8DUxsX994WzyNAotVp36qBqXku",
                    "DHT Hash": "QmcZVwZ5RGamnaxwgB8ZUE9WCjG1nU9rEaDNV5wy9jJP3S",
                    "artist": "Imogen Heap",
                    "collection": "Tiny Human",
                    "company": "Megaphonic Records",
                    "filename": "Imogen Heap - Tiny Human Video-H264 720P web.m4v",
                    "posterFrame": "Imogen Heap - Tiny-Human-Video-poster-frame.jpg",
                    "runtime": 261,
                    "tags": "Mycelia, Sennheiser, Music Videos"
                }
            },
            "payment": {
                "amount": "2,50,200",
                "currency": "USD",
                "type": "tip"
            },
            "extras": ""
        },
        "signature": "HxzC3DclNtMAT+S0cLqqPCMJMsJEfwB2DKQrllvIgpa5EwYSQokG5eDtbvV8j51aousz1yxXYrc1Ob+B5gxU4ms="
    },
    "txid": "62a63b3b59b3f5fc786ad05a37af656c88507ae959f53c233520b755aaa8a841",
    "block": 1400090,
    "publisher-name": "Imogen Heap"
}
```

This endpoint retrieves all Artifacts in the Alexandria library index that match the search criteria.

### HTTP Request

`POST https://api.alexandria.io/alexandria/v1/search`

### URL Parameters

Parameter | Description
--------- | -----------
protocol | "<code>media</code>"
search-on | "<code>publisher</code>", "<code>timestamp</code>", "<code>type</code>","<code>block</code>","<code>txid</code>" or "<code>*</code>" to search all fields
search-for | "<code>search string</code>"

### Optional URL Parameters

Parameter | Description
--------- | -----------
"search-like" | <code>true</code> or <code>false</code>,

<aside class="success">
The POST data should be a json encoded string
</aside>

<aside class="success">
Note — if you have Libraryd running locally, you can also use this local API endpoint:<br>
<code>POST http://localhost:41289/alexandria/v1/search</code>
</aside>

## Sign Artifact Publish Message

```python
import requests, json
payload = {'address': 'FAiWWyUEuXkxo7oQLWfD3oTWkHM6eu5JJH', 'text': 'QmcZVwZ5RGamnaxwgB8ZUE9WCjG1nU9rEaDNV5wy9jJP3S-FAiWWyUEuXkxo7oQLWfD3oTWkHM6eu5JJH-1444032978000'}

r = requests.post("http://localhost:41289/alexandria/v1/sign", data=json.dumps(payload))
print(r.text)
```

```shell
curl -X POST -H "Content-Type: application/json" --data '{"address":"FAiWWyUEuXkxo7oQLWfD3oTWkHM6eu5JJH","text":"QmcZVwZ5RGamnaxwgB8ZUE9WCjG1nU9rEaDNV5wy9jJP3S-FAiWWyUEuXkxo7oQLWfD3oTWkHM6eu5JJH-1444032978000"}' http://localhost:41289/alexandria/v1/sign
```

> The above command returns JSON structured like this:

```json
{
    "status": "success",
    "response": [
        "HxzC3DclNtMAT+S0cLqqPCMJMsJEfwB2DKQrllvIgpa5EwYSQokG5eDtbvV8j51aousz1yxXYrc1Ob+B5gxU4ms="
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

```python
import requests, json
payload = {'media-data':{'alexandria-media':{'torrent':'QmcZVwZ5RGamnaxwgB8ZUE9WCjG1nU9rEaDNV5wy9jJP3S','publisher':'FAiWWyUEuXkxo7oQLWfD3oTWkHM6eu5JJH','timestamp':1444032978000,'type':'video','info':{'title':'Tiny Human Music Video','description':'Tiny Human ISRCGBJPX1500151','year':2015,'extra-info':{'Bitcoin Address':'16diWTDN8DUxsX994WzyNAotVp36qBqXku','DHT Hash':'QmcZVwZ5RGamnaxwgB8ZUE9WCjG1nU9rEaDNV5wy9jJP3S','artist':'Imogen Heap','collection':'Tiny Human','company':'Megaphonic Records','filename':'Imogen Heap - Tiny Human Video-H264 720P web.m4v','posterFrame':'Imogen Heap - Tiny-Human-Video-poster-frame.jpg','runtime':261,'tags':'Mycelia, Sennheiser, Music Videos'}},'payment':{'amount':'2,50,200','currency':'USD','type':'tip'},'extras':''}},'signature':'H/7+wbTjR87fv2Qy96jp3oCfBdu9o/D5rzgA74UGSb/4f0iACwd/5YyehJ0y/uSaRwW3Tk6uT8x+OJZL3kro9hQ='}

r = requests.post("http://localhost:41289/alexandria/v1/send", data=json.dumps(payload))
print(r.text)
```

```shell
curl -X POST -H "Content-Type: application/json" --data '{"media-data":{"alexandria-media":{"torrent":"QmcZVwZ5RGamnaxwgB8ZUE9WCjG1nU9rEaDNV5wy9jJP3S","publisher":"FAiWWyUEuXkxo7oQLWfD3oTWkHM6eu5JJH","timestamp":1444032978000,"type":"video","info":{"title":"Tiny Human Music Video","description":"Tiny Human ISRCGBJPX1500151 Tiny Human (instrumental) ISRCGBJPX1500152 Published by Megaphonic Publishing Record label - Megaphonic Records copyright 2015 for information on use of sync please contact Info@imogenheap.com","year":2015,"extra-info":{"Bitcoin Address":"16diWTDN8DUxsX994WzyNAotVp36qBqXku","DHT Hash":"QmcZVwZ5RGamnaxwgB8ZUE9WCjG1nU9rEaDNV5wy9jJP3S","artist":"Imogen Heap","collection":"Tiny Human","company":"Megaphonic Records","filename":"Imogen Heap - Tiny Human Video-H264 720P web.m4v","posterFrame":"Imogen Heap - Tiny-Human-Video-poster-frame.jpg","runtime":261,"tags":"Mycelia, Sennheiser, Music Videos"}},"payment":{"amount":"2,50,200","currency":"USD","type":"tip"},"extras":""},"signature":"HxzC3DclNtMAT+S0cLqqPCMJMsJEfwB2DKQrllvIgpa5EwYSQokG5eDtbvV8j51aousz1yxXYrc1Ob+B5gxU4ms="}}' http://localhost:41289/alexandria/v1/send
```

> The above command returns JSON structured like this:

```json
{
    "status": "success",
    "response": [
        "62a63b3b59b3f5fc786ad05a37af656c88507ae959f53c233520b755aaa8a841",
        "991cbd71e06e6b810fddf65cbcdee9221045b1d44436b48916635199d35c9237",
        "fe29a84e2e29b4bf97ef73678a7f669edfa9537de23ba112c6f278d6defdf1cf",
        "014cd6b04d5abda8a05b5c8aa3e1e06916cc97247e6d30c6b610556957d67bd9"
    ]
}
```

This endpoint is used to announce a new Artifact using the signature created by the previous endpoint.

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
signature | "<a href="#sign-artifact-publish-message">signature</a>" 

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

## Sign an Artifact Deactivation Message

```python
import requests, json
payload = {'address':'F6yEsikfYQPRAEL8FfDzumLqPD9WDPmKtK','text':'F6yEsikfYQPRAEL8FfDzumLqPD9WDPmKtK-eac32af20eb7452067604b259c2acbebb81274a9321a1f99b980dc561df98b57'}

r = requests.post("http://localhost:41289/alexandria/v1/sign", data=json.dumps(payload))
print(r.text)
```

```shell
curl -X POST -H "Content-Type: application/json" --data '{"address":"F6yEsikfYQPRAEL8FfDzumLqPD9WDPmKtK","text":"F6yEsikfYQPRAEL8FfDzumLqPD9WDPmKtK-fce07bfd598949026719e9243868c3ff755884a8d80d7de655a784ba282cb1a9"}' http://localhost:41289/alexandria/v1/sign
```

> The above command returns JSON structured like this:

```json
{
    "status":"success",
    "response": [
        "H+WWxpgJ+MdwlP5c/f4dsdii9Bc6cZwUVu4Mu5X7RSLUUgBtEZ6EL0H3rpwkch/qqTTJXUMYd4lTGNebf3nndV8="
    ]
}
```

> Note, if any user other than the actual Publisher of an Artifact attempts to run this step, they will receive the following error message:

```json
{
    "status":"failure",
    "response": [
        "couldn't sign message with address FB2h62qtDpGuag7BAzwvuFwmRZUiVPhnv5"
    ]
}
```

This endpoint is used to sign an Artifact Deactivation message. Note, only the user who Published the Artifact may deactivate it.

<aside class="warning">This endpoint currently communicates only with a local wallet via RCP. To use it, install Librarian and turn on <code>Florincoin</code> and <code>Libraryd</code>.</aside>

### HTTP Request

`POST http://localhost:41289/alexandria/v1/sign`

### URL Parameters

Parameter | Description
--------- | -----------
address | "<code>florincoin address</code>"
text | "<code>florincoin address</code>-<code>artifact txid</code>"

<aside class="success">
The POST data should be a json encoded string
</aside>

## Deactivate an Artifact

```python
import requests, json
payload = {'alexandria-deactivation':{'address':'F6yEsikfYQPRAEL8FfDzumLqPD9WDPmKtK','txid':'96f10338e371c1f6ad5dbe886cf9ea891f1bbee70c76ac30c5fa8ebce9365784'},'signature':'H+WWxpgJ+MdwlP5c/f4dsdii9Bc6cZwUVu4Mu5X7RSLUUgBtEZ6EL0H3rpwkch/qqTTJXUMYd4lTGNebf3nndV8='}

r = requests.post("http://localhost:41289/alexandria/v1/send", data=json.dumps(payload))
print(r.text)
```

```shell
curl -X POST -H "Content-Type: application/json" --data '{"alexandria-deactivation":{"address":"F6yEsikfYQPRAEL8FfDzumLqPD9WDPmKtK","txid":"96f10338e371c1f6ad5dbe886cf9ea891f1bbee70c76ac30c5fa8ebce9365784"},"signature":"H+WWxpgJ+MdwlP5c/f4dsdii9Bc6cZwUVu4Mu5X7RSLUUgBtEZ6EL0H3rpwkch/qqTTJXUMYd4lTGNebf3nndV8="}' http://localhost:41289/alexandria/v1/send
```

> The above command returns JSON structured like this:

```json
{
    "status": "success",
    "response": [
        "332cb594cb7e5504dcffb9973cdb5ea643b06252c879a3a5e2975b6386cfa84b"
    ]
}
```

This endpoint is used to deactivate an Artifact currently in the Alexandria library. Note, only the user who Published the Artifact may deactivate it.

<aside class="warning">This endpoint currently communicates only with a local wallet via RCP. To use it, install Librarian and turn on <code>Florincoin</code> and <code>Libraryd</code>.</aside>

### HTTP Request

`POST http://localhost:41289/alexandria/v1/send`

### URL Parameters

Parameter | Description
--------- | -----------
alexandria-deactivation | {
address | "<code>florincoin address</code>",
txid | "<code>artifact txid</code>"
 | }, 
signature | "<a href="#sign-an-artifact-deactivation-message">signature</a>"

<aside class="success">
The POST data should be a json encoded string
</aside>


# Florincoin

## Get Market Data

```python
import requests

r = requests.get('https://api.alexandria.io/flo-market-data/v1/getAll')
r.json()
```

```shell
curl "https://api.alexandria.io/flo-market-data/v1/getAll"
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

`GET https://api.alexandria.io/flo-market-data/v1/getAll`

<aside class="success">
Note — if you have Libraryd running locally, you can also use this local API endpoint:<code>GET http://localhost:41289/alexandria/v1/media/get/all</code>
</aside>

## Get Blockchain Mining Info

```python
import requests

r = requests.get('https://api.alexandria.io/florincoin/getMiningInfo')
r.json()
```

```shell
curl "https://api.alexandria.io/florincoin/getMiningInfo"
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

`GET https://api.alexandria.io/florincoin/getMiningInfo`

<aside class="success">
Note — if you have Libraryd running locally, you can also use this local API endpoint:<code>GET http://localhost:41289/alexandria/v1/media/get/all</code>
</aside>

## Get Rental Data for Scrypt Rigs from Miningrigrentals.com (third party service)

```python
import requests

r = requests.get('https://www.miningrigrentals.com/api/v1/rigs?method=list&type=scrypt&max_cost=0.00001')
r.json()
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

```python
import requests, json
payload = {'search': 'Alexandria', 'page': 0, 'results-per-page': 5}

r = requests.post("https://api.alexandria.io/florincoin/searchTxComment", data=json.dumps(payload))
print(r.text)
```

```shell
curl -X POST -H "Content-Type: application/json" --data '{"search":"Alexandria","page":0,"results-per-page":5}' https://api.alexandria.io/florincoin/searchTxComment
```

> The above command returns JSON structured like this:

```json
[
    {
        "Hash": "03c4527decc9b305b4376398082b0f2392df53b636f9db4725d8959c7643d437",
        "Message": "{title: 'Alexandria', term: project alexandria, type: search}"
    }
]
```

This endpoint retrieves all Florincoin transaction comments matching a given search query.

### HTTP Request

`POST https://api.alexandria.io/florincoin/searchTxComment`

### URL Parameters

Parameter | Description
--------- | -----------
search | "<code>search query</code>"
results-per-page | <code>number of results per page</code>(integer)
page | <code>page number for paginated results</code>(integer)

<aside class="success">
The POST data should be a json encoded string
</aside>

# TradeBot

## Get TradeBot Balance for Alexandria.io node

```python
import requests

r = requests.get('https://api.alexandria.io/tradebot/flobalance')
r.json()
print(r.text)
```

```shell
curl "https://api.alexandria.io/tradebot/flobalance"
```

> The above command returns JSON structured like this:

```json
90775.5660569
```

This endpoint retrieves the number of Florincoin tokens available for BTC-FLO trades on Alexandria.io's TradeBot node.

### HTTP Request

`GET https://api.alexandria.io/tradebot/flobalance`

## Get A Bitcoin Address from Alexandria.io's TradeBot node

```python
import requests

r = requests.get('https://api.alexandria.io/tradebot/depositaddress?floaddress=FSZm9tRgH4XDfeTvQPmMq7M8ZVDsyW2utQ&raw')
r.json()
print(r.text)
```

```shell
curl "https://api.alexandria.io/tradebot/depositaddress?floaddress=FSZm9tRgH4XDfeTvQPmMq7M8ZVDsyW2utQ&raw"
```

> The above command returns JSON structured like this:

```json
"1LnAqVZo7eB3zYRmWFmyKCQWUAT73Nc36c"
```

This endpoint provides a Florincoin address and retreives a Bitcoin address for facilitating trading with Alexandria.io's TradeBot node.

### HTTP Request

`GET https://api.alexandria.io/tradebot/depositaddress?floaddress={floaddress}&raw`

### URL Parameters

Parameter | Description
--------- | -----------
floaddress | "<code>florincoin receiving address for deposit from trade</code>"

<aside class="success">
Note — if you exclude <code>raw</code> from the endpoint, html code will be returned, including an <code>img src</code> of the QR code for the Bitcoin address.
</aside>

# Using the Client Library (Javascript)
Alexandria is comprised of many different components, each of which have some deep and complex APIs.

Luckily, there's a set of Javascript files available to ease the pain:

 - **SimpleWallet.js** - Used for **FloVault** client-side wallet (forked from LiteVault)
 - **libraryd-js.js** - A light wrapper over the FloVault and publisher APIs for publishing
 - **ipfs.js** - A wrapper for interacting with IPFS.
 - **publishArtifact.js** - This isn't a library, however there's a lot of important code related to the publishing process in here.

## Using FloVault (https://flovault.alexandria.io/)


```javascript
// Initialize a FloVault instance
var wallet = new Wallet(your_identifier, your_password);

wallet.load(function() {
    console.log('Wallet was loaded');
});
// You will need to run refreshBalances before you make any transactions
// so it is recommended to have this run on some form of timer.
// 60 seconds is probably good enough
setInterval(60000, wallet.refreshBalances);
```

If you don't want to set up a FloVault node locally, you can use the node running for Alexandria.IO - by
default, the **SimpleWallet.js** is pre-configured to use Alexandria's own server at https://flovault.alexandria.io/. Don't worry about tracking or hacking, everything happens
client side, we just host an encrypted copy of your wallet for easy access.

If you wish to change this, you'll need to modify `flovaultBaseURL` and/or `florinsightBaseURL` (block explorer used)
in SimpleWallet.js

You need to register for a wallet, and note down the identifier.

Once you've registered, you can use the wallet in your code simply by using the JS code on the right:


<aside class="error">
Note — if you attempt to use the SimpleWallet.js code server-side (i.e. NodeJS), you will run into issues,
as it is bound to jQuery, SWAL (alert system), and uses localStorage for certain caching.
</aside>


## Sending transactions using FloVault

FloVault was modified from the original to include comments, as those are the key feature of FlorinCoin.

To send coins (required to create a comment), you can use the `sendCoins` function. This will build a transaction
locally, and then broadcast it to the defined `florinsightBaseURL` defined in SimpleWallet.js

```javascript

wallet.sendCoins('Fabcd', 'Fbcdc', 3.1415, "Florin Comment", function(err,data) {
    if(err) {
        return console.error('failed to send transaction');
    }
    return console.log('successfully send transaction. TXID: ', data);
});
```

### wallet.sendCoins(fromAddress, toAddress, amount, txComment, callback)

Parameter | Description
--------- | -----------
fromAddress | A public address inside of `wallet` to be used to send the coins
toAddress | The receiver of the coins
amount | Amount of florincoins to send (decimal, i.e. 0.1 == 0.1 florincoins) 
txComment | Comment for the transaction
callback | A callback in the form of (err,data), where data is the TXID on success


## Putting files onto IPFS

```javascript
// Alexandria.IO's IPFS node. WARNING THIS ADDRESS MAY CHANGE IN FUTURE
ipfs.setProvider({host: 'ipfs.alexandria.io', port: '443', protocol: 'https'});

var file_input = document.getElementById('my_file_input');
ipfs.add(file_input, function(err,hashes) {
    if(err || !hashes) {
        return console.error('there was an error uploading your file(s):', err); 
    }
    // note that hashes is an array of IPFS DHT hashes
    return hashes
});

```

Inside of `ipfs.js` we have a function called **add**. This encodes the data from a file form input, or DropZone
and publishes it to the configured IPFS node. By default, this would be the IPFS node running on Alexandria.IO

The file contains many other useful IPFS functions, however adding files is the most important part
of publishing.

### ipfs.add(files, callback)

Parameter | Description
--------- | -----------
files | A standard HTML file input, containing one or more files
callback | A callback in the form of (err,hashes), where hashes is an array of the DHT hashes

## Publishing a file

Publishing a file combines FloVault's client side code, IPFS client side code, Florinsight behind the scenes for balances, 
as well as the publisher API to finalize it.

The first step is to upload each file to IPFS (see the previous section) that is used by your artifact, such as posters
cover art, album art, and the actual content. Make sure you save the hashes after each upload.

```javascript
var yourPublisherAddress = 'Fxxx...';
// -*- Put the files into IPFS
var hashes = {};
// main content
ipfs.add(the_movie, function(err,data) { 
    if(err) return console.error('error');
    hashes['the_movie'] = data[0];
});
// any additional files
ipfs.add(poster, function(err,data) { ... });
ipfs.add(cover, function(err,data) { ... });
```

Next, you'll need to generate a JSON artifact. This is an object which contains various metadata about your content
and where to find that content (i.e. IPFS hashes), along-side meta-content such as cover images, posters, and album art.

```javascript
// -*- Build the artifact. Insert hashes from earlier
var artifact = {
    'media-data': {
        torrent: hashes['the_movie'].Hash, // DHT hash from IPFS
        timestamp: Date.now(),
        type: "video",
        publisher: yourPublisherAddress,
        payment: {
            // see Publishing an Artifact for payment data
        }
        info: {
            title: "My Movie",
            description: "This is my movie",
            "extra-info": {
                "DHT Hash": hashes['the_movie'].Hash,
                filename: hashes['the_movie'].Name,
                files: []
            }
        }
    }
}

```

You can find the schema for the JSON artifact under [Publish New Artifact](#publish-new-artifact)

Once you've produced your artifact, you can pass the data to libraryd-js' `publishArtifact`. You'll also need a FloVault
instance at hand, as it will cost some FlorinCoin to publish. 

Be aware publishArtifact will automatically handle the transactions for you (as long as your FloVault is loaded, as per the previous section);
you don't need to worry about creating them. It will also automatically attempt to sign your artifact using the publisher API.

```javascript
// -*- Now publish the artifact we've built, using FloVault + the publisher API
LibraryDJS.publishArtifact(wallet, hashes['the_movie'].Hash, yourPublisherAddress, artifact, function(err, data)
{
    if(err) {
        return console.error('error publishing artifact: ', err);
    }
    return console.log('Successfully published your artifact');
}
```


# Mining Pool

## Get Alexandria's Pool Stats

```python
import requests

r = requests.get('https://api.alexandria.io/pool/api/stats')
r.json()
print(r.text)
```

```shell
curl "https://api.alexandria.io/pool/api/stats"
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

`GET https://api.alexandria.io/pool/api/stats`

## Get Last 24 Hours of Alexandria's Pool Stats

```python
import requests

r = requests.get('https://api.alexandria.io/pool/api/pool_stats')
r.json()
print(r.text)
```

```shell
curl "https://api.alexandria.io/pool/api/pool_stats"
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

`GET https://api.alexandria.io/pool/api/pool_stats`

## Get Alexandria's Pool Live Stats

```python
import requests

r = requests.get('https://api.alexandria.io/pool/api/live_stats')
r.json()
print(r.text)
```

```shell
curl "https://api.alexandria.io/pool/api/live_stats"
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

`GET https://api.alexandria.io/pool/api/live_stats`


# Payment Processor

## Test payment processor is running

This is a simple test to check whether the service is running.

### HTTP Request

`GET https://api.alexandria.io/payproc/ping`

```shell
curl https://api.alexandria.io/payproc/ping
```

>If running, the request returns

```text
ALIVE
```

## Retrieve payment address

### HTTP Request

`GET https://api/alexandria.io/payproc/receive?address=bitcoin_address&amount=bitcoin_amount`

To generate a receive address for payments, use /payproc/receive.

### Parameters:

**address** Address to receive coins

**amount** Amount to send to address in BTC

### Return:

temporary address The temporary address that can be shown to the buyer.

```shell
curl "https://api.alexandria.io/payproc/receive?address=2N4ajxiM1xHc83mehV2LTXk2Z65TAfc9MhX&amount=0.432"
```

>This request returns the temporary address to receive payment.

```json
{"input_address":"2N6dDdHGx24ss6AoAqjx8gnc2JQpETe1mBp"}
```

## Check unconfirmed address balance

### HTTP request

`GET https://api.alexandria./payproc/getreceivedbyaddress/payment_address`

Check the total amount of the *unconfirmed* balance of the given BTC address.

```shell
curl "https://api.alexandria.io/payproc/getreceivedbyaddress/2N4ajxiM1xHc83mehV2LTXk2Z65TAfc9MhX"
```
> The request returns the unconfirmed balance in Bitcoin.

```text
0.00000000
```

### Path Parameter:

/payproc/getreceivedbyaddress/payment_address

**payment_address** The temporary payment address to monitor.

### Return:

The unconfirmed balance in BTC.
