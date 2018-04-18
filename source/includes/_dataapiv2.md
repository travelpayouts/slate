---
title: Flight Data Access API v2

language_tabs:
  - shell: cURL
  - ruby: Ruby
  - php: PHP
  - python: Python

search: true
---

# Flight Data Access API v2

The server response is always sent in JSON format with the following structure:

  - **success** – true for a successful request, false in case of errors;
  - **data** – a result of the request; in case of an error is equal to null;
  - **error** – short description of the error that prevented request completion; for a successful request is equal to null.

Dates are accepted in the formats YYYY-MM and YYYY-MM-DD.

Dates and times are given in UTC, formatted according to [ISO 8601](https://ru.wikipedia.org/wiki/ISO_8601). Prices are given in rubles as of when the ticket is put in the search results. It is not recommended to use expired prices (the approximate expiration date is given in the value of the expires_at parameter).

<aside class="warning">
**Important**. We strongly urge receiving data in compressed GZIP format, which saves a significant amount of time in receiving the response. To get data in compressed form, send the header Accept-Encoding: gzip, deflate.
</aside>

To obtain access to the API for searching for plane tickets and hotels, [send a request](https://support.travelpayouts.com/hc/en-us/requests/new).

## The prices for the airline tickets

Brings back the list of prices found by our users during the most recent 48 hours according to the filters used.

> Example of a request:

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/v2/prices/latest?currency=usd&period_type=year&page=1&limit=30&show_to_affiliates=true&sorting=price&trip_class=0' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/http'

url = URI("http://api.travelpayouts.com/v2/prices/latest?currency=usd&period_type=year&page=1&limit=30&show_to_affiliates=true&sorting=price&trip_class=0")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)
request["x-access-token"] = '321d6a221f8926b5ec41ae89a3b2ae7b'

response = http.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "http://api.travelpayouts.com/v2/prices/latest?currency=usd&period_type=year&page=1&limit=30&show_to_affiliates=true&sorting=price&trip_class=0",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_HTTPHEADER => array(
    "x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b"
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

```python
import requests

url = "http://api.travelpayouts.com/v2/prices/latest"

querystring = {"currency":"usd","period_type":"year","page":"1","limit":"30","show_to_affiliates":"true","sorting":"price","trip_class":"0"}

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

`GET http://api.travelpayouts.com/v2/prices/latest?currency=usd&period_type=year&page=1&limit=30&show_to_affiliates=true&sorting=price&trip_class=0&token=PutHereYourToken`

### Request parameters

<aside class="notice">
**Note** If the point of departure and the point of destination are not specified, the API shall bring back 30 of the cheapest tickets that have been found during the most recent 48 hours.
</aside>

Parameter | Default | Description
--------- | ------- | -----------
currency | RUB | The airline ticket’s currency.
origin | - | The point of departure. The IATA city code or the country code. The length - from 2 to 3 symbols.
destination | - | The point of destination. The IATA city code or the country code. The length - from 2 to 3 symbols.
beginning_of_period | - | The beginning of the period, within which the dates of departure fall (in the YYYY-MM-DD format, for example, 2016-05-01). Must be specified if **period_type** is equal to a month.
period_type | - | The period for which the tickets have been found (the required parameter): **year** — for the whole time, **month** — for a month.
one_way | false | **true** - one way, **false** - back-to-back.
page | 1 | A page number.
limit | 30 | The total number of records on a page. The maximum value - 1000.
show_to_affiliates | true | **false** - all the prices, **true** - just the prices, found using the partner marker (recommended).
sorting | price | The assorting of prices: **price** — by the price. For the directions, only **city - city** assorting by the price is possible; **route** — by the popularity of a route; **distance_unit_price** — by the price for 1 km.
trip_duration | 1 | A page number.
token | - | Individual affiliate token.

### Response

> The above command returns JSON structured like this:

```json
{
  "success": true,
  "data": [
    {
      "show_to_affiliates": true,
      "trip_class": 0,
      "origin": "BKK",
      "destination": "PHS",
      "depart_date": "2018-02-09",
      "return_date": "2018-02-11",
      "number_of_changes": 0,
      "value": 36.36,
      "found_at": "2017-07-24T06:33:32+04:00",
      "distance": 339,
      "actual": true
    }
  ]
}
```

Parameter | Default | Description
--------- | ------- | -----------
 Origin | - | The point of departure.
 destination | - | The point of destination.
 show_to_affiliates | true | False - all the prices, true — just the prices, found using the partner marker (recommended)
 trip_class | - | The flight class: **0** — the economy class, **1** — the business class, **2** — the first class.
 depart_date | - | The date of departure.
 return_date | - | The date of return.
 number_of_changes | - | The number of transfers.
 value | - | The cost of a flight, in the currency specified.
 found_at | - | The time and the date, for which a ticket was found.
 distance | - | The distance between the point of departure and the point of destination.
 actual | - | The actuality of an offer.
 token | - | Individual affiliate token.

## The calendar of prices for a month

Brings the prices for each day of a month, grouped together by the number of transfers, back.

> Example of a request:

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/v2/prices/month-matrix?currency=usd&show_to_affiliates=true&origin=LED&destination=HKT' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/http'

url = URI("http://api.travelpayouts.com/v2/prices/month-matrix?currency=usd&show_to_affiliates=true&origin=LED&destination=HKT")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)
request["x-access-token"] = '321d6a221f8926b5ec41ae89a3b2ae7b'

response = http.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "http://api.travelpayouts.com/v2/prices/month-matrix?currency=usd&show_to_affiliates=true&origin=LED&destination=HKT",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_HTTPHEADER => array(
    "x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b"
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

```python
import requests

url = "http://api.travelpayouts.com/v2/prices/month-matrix"

querystring = {"currency":"usd","show_to_affiliates":"true","origin":"LED","destination":"HKT"}

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

'GET http://api.travelpayouts.com/v2/prices/month-matrix?currency=usd&show_to_affiliates=true&origin=LED&destination=HKT'

### Request parameters

**Note!** If the point of departure and the point of destination are not specified, then the API shall bring 30 the cheapest tickets, which have been found during the recent 48 hours, back.

Parameter | Default | Description
--------- | ------- | -----------
currency | RUB | The airline ticket’s currency
origin | - | The point of departure. The IATA city code or the country code. The length - from 2 to 3 symbols.
destination | - | The point of destination. The IATA city code or the country code. The length - from 2 to 3 symbols.
month | - | The beginning of the month in the YYYY-MM-DD format.
show_to_affiliates | true | False - all the prices, true - just the prices, found using the partner marker (recommended).
token | - | Individual affiliate token.

### Response

> The above command returns JSON structured like this:

```json
{
    "success":true,
    "data":[{
        "show_to_affiliates":true,
        "trip_class":0,
        "origin":"LED",
        "destination":"HKT",
        "depart_date":"2015-10-01",
        "return_date":"",
        "number_of_changes":1,
        "value":29127,
        "found_at":"2015-09-24T00:06:12+04:00",
        "distance":8015,
        "actual":true
    }]
}
```



Parameter | Default | Description
--------- | ------- | -----------
 origin | - | The point of departure.
 destination | - | The point of destination.
 show_to_affiliates | true | False - all the prices, true - just the prices, found using the partner marker (recommended).
 trip_class | - | The flight class: **0** — The economy class, **1** — The business class, **2** — The first class.
 depart_date | - | The date of departure.
 return_date | - | The date of return.
 number_of_changes | - | The number of transfers.
 value | - | The cost of a flight, in the currency specified.
 found_at | - | The time and the date, for which a ticket was found.
 distance | - | The distance between the point of departure and the point of destination.
 actual | - | The actuality of an offer.

## The prices for the alternative directions

Brings the prices for the directions between the nearest to the target cities back.

> Example of a request:

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/v2/prices/nearest-places-matrix?currency=usd&show_to_affiliates=true&origin=LED&destination=HKT' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/http'

url = URI("http://api.travelpayouts.com/v2/prices/nearest-places-matrix?currency=usd&show_to_affiliates=true&origin=LED&destination=HKT")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)
request["x-access-token"] = '321d6a221f8926b5ec41ae89a3b2ae7b'

response = http.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "http://api.travelpayouts.com/v2/prices/nearest-places-matrix?currency=usd&show_to_affiliates=true&origin=LED&destination=HKT",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_HTTPHEADER => array(
    "x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b"
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

```python
import requests

url = "http://api.travelpayouts.com/v2/prices/nearest-places-matrix"

querystring = {"currency":"usd","show_to_affiliates":"true","origin":"LED","destination":"HKT"}

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

`GET http://api.travelpayouts.com/v2/prices/nearest-places-matrix?currency=usd&origin=LED&destination=HKT&show_to_affiliates=true&token=PutHereYourToken`

### Request parameters

Parameter | Default | Description
--------- | ------- | -----------
currency | RUB | The airline ticket’s currency
 origin | - | The point of departure. The IATA city code or the country code. The length - from 2 to 3 symbols.
 destination | - | The point of destination. The IATA city code or the country code. The length - from 2 to 3 symbols.
 limit | - | The number of variants entered, from 1 to 20. Where 1 – is just the variant with the specified points of departure and the points of destination.
 show_to_affiliates | true | False - all the prices, true - just the prices, found using the partner marker (recommended).
depart_date** *(optional)* | - | Day or month of departure (yyyy-mm-dd or yyyy-mm).
 return_date** *(optional)* | - | Day or month of return (yyyy-mm-dd or yyyy-mm).
 flexibility | - | Expansion of the range of dates upward or downward. The value may vary from 0 to 7, where 0 shall show the variants for the dates specified, 7 – all the variants found for a week prior to the specified dates and a week after.
 distance | - | The number of variants entered, from 1 to 20. Where 1 – is just the variant with the specified points of departure and the points of destination.
 token | - | Individual affiliate token.

### Response

> The above command returns JSON structured like this:

```json
{
"prices":[{
    "value":26000.0,
    "trip_class":0,
    "show_to_affiliates":true,
    "return_date":"2016-09-18",
    "origin":"BAX",
    "number_of_changes":0,
    "gate":"AMADEUS",
    "found_at":"2016-07-28T04:57:47Z",
    "duration":null,
    "distance":3643,
    "destination":"SIP",
    "depart_date":"2016-09-09",
    "actual":true
    }],
"origins":[
    "BAX"
    ],
"errors":{
    "amadeus":{
    }},
"destinations":[
    "SIP"
    ]
}
```

Parameter | Default | Description
--------- | ------- | -----------
 origin | - | The point of departure.
 destination | - | The point of destination.
 show_to_affiliates | true | False - all the prices, true - just the prices, found using the partner marker (recommended).
 trip_class | - | The flight class: **0** — the economy class, **1** — the business class, **2** — the first class.
 depart_date | - | The date of departure.
 return_date | - | The date of return.
 number_of_changes | - | The number of transfers.
 value | - | The cost of a flight, in the currency specified.
 found_at | - | The time and the date, for which a ticket was found.
 distance | - | The distance between the point of departure and the point of destination.
 actual | - | The actuality of an offer.
 duration | - | Flight duration in minutes, taking into account direct and expectations.
 errors | - | If the error "Some error occurred" is returned, so in this area do not have the data in the cache.
 gate | - | The agents, which was found on the ticket.
 token | - | Individual affiliate token.

## The calendar of prices for a week

Brings the prices for the nearest dates to the target ones back.

> Example of a request:

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/v2/prices/week-matrix?currency=usd&origin=LED&destination=HKT&show_to_affiliates=true&depart_date=2017-11-04&return_date=2017-11-18' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/http'

url = URI("http://api.travelpayouts.com/v2/prices/week-matrix?currency=usd&origin=LED&destination=HKT&show_to_affiliates=true&depart_date=2017-11-04&return_date=2017-11-18")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)
request["x-access-token"] = '321d6a221f8926b5ec41ae89a3b2ae7b'

response = http.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "http://api.travelpayouts.com/v2/prices/week-matrix?currency=usd&origin=LED&destination=HKT&show_to_affiliates=true&depart_date=2017-11-04&return_date=2017-11-18",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_HTTPHEADER => array(
    "x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b"
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

```python
import requests

url = "http://api.travelpayouts.com/v2/prices/week-matrix"

querystring = {"currency":"usd","origin":"LED","destination":"HKT","show_to_affiliates":"true","depart_date":"2017-11-04","return_date":"2017-11-18"}

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

Parameter | Default | Description
--------- | ------- | -----------
 currency | RUB |The airline tickets currency.
 origin | - | The point of departure. The IATA city code or the country code. The length - from 2 to 3 symbols.
 destination | - | The point of destination. The IATA city code or the country code. The length - from 2 to 3 symbols.
 show_to_affiliates | true | False - all the prices, true - just the prices, found using the partner marker (recommended).
 depart_date *(optional)* | - | Day or month of departure (yyyy-mm-dd or yyyy-mm).
 return_date *(optional)* | - | Day or month of return (yyyy-mm-dd or yyyy-mm).
 token | - | Individual affiliate token.

### Response

> The above command returns JSON structured like this:

```json
{
    "success":true,
    "data":[
    {
        "show_to_affiliates":true,
        "trip_class":0,
        "origin":"LED",
        "destination":"HKT",
        "depart_date":"2016-03-01",
        "return_date":"2016-03-15",
        "number_of_changes":1,
        "value":71725,
        "found_at":"2016-02-19T00:04:37+04:00",
        "distance":8015,
        "actual":true
    }]
}
```

### Request

`GET http://api.travelpayouts.com/v2/prices/week-matrix?currency=usd&origin=LED&destination=HKT&show_to_affiliates=true&depart_date=2016-09-04&return_date=2016-09-18&token=PutHereYourToken`

### Request parameters

Parameter | Default | Description
--------- | ------- | -----------
 origin | - | The point of departure.
 destination | - | The point of destination.
 show_to_affiliates | true | False - all the prices, true - just the prices, found using the partner marker (recommended). 
 trip_class | - | The flight class: **0** — the economy class, **1** — the business class, **2** — the first class.
 depart_date | - | The date of departure.
 return_date | - | The date of return.
 number_of_changes | - | The number of transfers.
 value | - | The cost of a flight, in the currency specified.
 found_at | - | The time and the date, for which a ticket was found.
 distance | - | The distance between the point of departure and the point of destination.
 actual | - | The actuality of an offer.

## The definition of a user's location by IP address

The query is returned the IATA-code and the name of the nearest city from the user.

> Example of a request:

```shell
curl --request GET \
  --url 'http://www.travelpayouts.com/whereami?locale=ru&callback=useriata&ip=62.105.128.0' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'rubygems' if RUBY_VERSION < '1.9'
require 'rest_client'

headers  = {:x_access_token => "YOUR_API_TOKEN_HERE"}
response = RestClient.get "http://www.travelpayouts.com/whereami?locale=ru&callback=useriata&ip=62.105.128.0", headers
puts response
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "http://www.travelpayouts.com/whereami?locale=ru&callback=useriata&ip=62.105.128.0",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_HTTPHEADER => array(
    "x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b"
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

```python
from urllib2 import Request, urlopen
headers = {"X-Access-Token": "YOUR_API_TOKEN_HERE"}
request = Request("http://www.travelpayouts.com/whereami?locale=ru&callback=useriata&ip=62.105.128.0", headers=headers)
response_body = urlopen(request).read()
print response_body
```

### Request

GET `http://www.travelpayouts.com/whereami?locale=ru&callback=useriata&ip=62.105.128.0`

### Request parameters

Parameter | Default | Description
--------- | ------- | -----------
locale | Russian | The language in which returns the name of the city (available languages: en, ru, de, fr, it, pl, th.);
callback | - | Specifies the name of the function, which contains a response to a query (mandatory);
ip | - | Ip-addresses of the users (if the address is not passed, the system determines IP from the header of the request).

### Response

> The above command returns JSON structured like this:

```json
useriata ({"iata": "MOW", "name": "Moscow"})
```

Parameter | Default | Description
--------- | ------- | -----------
 iata | - | IATA code of the city where the user is located;
 name | - | The name of the city.

## Special offers

Brings the recent special offers from the airline companies back in the XML format.

### Request

`GET http://api.travelpayouts.com/v2/prices/special-offers?token=PutHereYourToken`
