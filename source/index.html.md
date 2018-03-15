---
title: API Reference

language_tabs:
  - shell: cURL
  - ruby: Ruby
  - php: PHP
  - python: Python

toc_footers:
  - <a href='https://www.travelpayouts.com/'>Sign Up for a Developer Token</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Flight Data Access API

Travelpayouts Flight Data API – the way to get travel insights for your site or blog. You can get flight price trends and find popular destinations for your customers.

<aside class="notice">
Dear partners! Attention, the data is transferred from the cache, so it is recommended to use them to generate static pages.
</aside>

To access the API you must pass your token in the X-Access-Token header or in the token parameter. To obtain a token for the Data Access API, go to http://www.travelpayouts.com/developers/api.

Dates are accepted in the formats YYYY-MM and YYYY-MM-DD.

The server response is always sent in json format with the following structure:

  - **success** – true for successful request, false in case of errors;
  - **data** – result of the request; in case of an error is equal to null;
  - **error** – short description of the error that prevented request completion; for successful request is equal to null.

Dates and times are given in UTC, formatted according to [ISO 8601](https://ru.wikipedia.org/wiki/ISO_8601). Prices are given in rubles as of when the ticket is put in the search results. It is not recommended to use expired prices (the approximate expiration date is given in the value of the expires_at parameter).

<aside class="warning">
**Important**. We strongly urge receiving data in compressed GZIP format, which saves a significant amount of time in receiving the response. To get data in compressed form, send the header Accept-Encoding: gzip, deflate.
</aside>

To obtain access to the API for searching for plane tickets and hotels, [send a request](https://support.travelpayouts.com/hc/en-us/requests/new).

## The prices for the airline tickets

Brings back the list of prices found by our users during the most recent 48 hours according to the filters used.

> Example of request:

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
beginning_of_period | - | The beginning of the period, within which the dates of departure fall (in the YYYY-MM-DD format, for example, 2016-05-01). Must be specified if **period_type** is equal to month.
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

> Example of request:

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

GET 'http://api.travelpayouts.com/v2/prices/month-matrix?currency=usd&show_to_affiliates=true&origin=LED&destination=HKT'

### Request parameters

**Note!** If the point of departure and the point of destination are not specified, then the API shall bring 30 the most cheapest tickets, which have been found during the recent 48 hours, back.

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
{{
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
}}
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

> Example of request:

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
 gate | - | The agents, which was found in the ticket.
 token | - | Individual affiliate token.

## Cheapest tickets

Returns the cheapest non-stop tickets, as well as tickets with 1 or 2 stops, for the selected route with departure/return date filters.

> Example of request:

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/v1/prices/cheap?origin=MOW&destination=HKT&depart_date=2017-11&return_date=2017-12' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/http'

url = URI("http://api.travelpayouts.com/v1/prices/cheap?origin=MOW&destination=HKT&depart_date=2017-11&return_date=2017-12")

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
  CURLOPT_URL => "http://api.travelpayouts.com/v1/prices/cheap?origin=MOW&destination=HKT&depart_date=2017-11&return_date=2017-12",
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

url = "http://api.travelpayouts.com/v1/prices/cheap"

querystring = {"origin":"MOW","destination":"HKT","depart_date":"2017-11","return_date":"2017-12"}

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

`GET http://api.travelpayouts.com/v1/prices/cheap?origin=MOW&destination=HKT&depart_date=2016-11&return_date=2016-12&token=PutHereYourToken`

<aside class="warning">
**Important** Old dates may be specified in a query. No error will be generated, but no data will be returned.
</aside>

### Request parameters

Parameter | Default | Description
--------- | ------- | -----------
 origin | - | IATA code of the departure city. IATA code is shown by uppercase letters, for example MOW.
 destination | - | IATA code of the destination city (for all routes, enter "-"). IATA code is shown by uppercase letters, for example MOW.
 depart_date *(optional)* | - |Day or month of departure (yyyy-mm-dd or yyyy-mm).
 return_date *(optional)* | - |Day or month of return (yyyy-mm-dd or yyyy-mm).
 page | - | Optional parameter, is used to display the found data (by default the page displays 100 found prices. If the **destination** isn't selected, there can be more data. In this case, use the **page**, to display the next set of data, for example, page=2).
 token | - | Individual affiliate token.
currency | RUB | Currency of prices

### Response

> The above command returns JSON structured like this:

```json
{
"success": true,
"data": {
	"HKT": {
		"0": {
			"price": 35443,
			"airline": "UN",
			"flight_number": 571,
			"departure_at": "2015-06-09T21:20:00Z",
			"return_at": "2015-07-15T12:40:00Z",
			"expires_at": "2015-01-08T18:30:40Z"
		}}
	}
}
```

Parameter | Default | Description
--------- | ------- | -----------
 0, 1, 2 | - | Sequence number in the search results.
 price | - | Ticket price (in the currency specified in the currency parameter).
 airline | - | IATA code of the airline operating the flight.
 flight_number | - | Flight number.
 departure_at | - | Departure Date.
 return_at | - | Return Date.
 expires_at | - | Date on which the found price expires (UTC+0).
 token | - | Individual affiliate token.

## Non-stop tickets

Returns the cheapest non-stop tickets for the selected route with departure/return date filters.

> Example of request:

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/v1/prices/cheap?origin=MOW&destination=HKT&depart_date=2017-11&return_date=2017-12' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/http'

url = URI("http://api.travelpayouts.com/v1/prices/direct?origin=MOW&destination=LED&depart_date=2017-11&return_date=2017-12")

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
  CURLOPT_URL => "http://api.travelpayouts.com/v1/prices/direct?origin=MOW&destination=LED&depart_date=2017-11&return_date=2017-12",
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

url = "http://api.travelpayouts.com/v1/prices/direct"

querystring = {"origin":"MOW","destination":"LED","depart_date":"2017-11","return_date":"2017-12"}

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

`GET http://api.travelpayouts.com/v1/prices/direct?origin=MOW&destination=LED&depart_date=2016-11&return_date=2016-12&token=PutHereYourToken`

### Request parameters

Parameter | Default | Description
--------- | ------- | -----------
origin | - | IATA code of departure city. IATA code is shown by uppercase letters, for example MOW.
destination | - | IATA code of destination city (for all routes, enter “-”). IATA code is shown by uppercase letters, for example MOW.
depart_date *(optional)* | - | Day or month of departure (yyyy-mm-dd or yyyy-mm).
return_date *(optional)* | - | Day or month of return (yyyy-mm-dd or yyyy-mm).
token | - | Individual affiliate token.
currency | RUB | Currency of prices

### Response

> The above command returns JSON structured like this:

```json
{
    "success": true,
    "data": {
        "LED": {
            "0": {
                "price": 4363,
                "airline": "UT",
                "flight_number": 369,
                "departure_at": "2015-06-27T11:35:00Z",
                "return_at": "2015-07-04T16:00:00Z",
                "expires_at": "2015-01-08T20:21:46Z"
            }
        }
    }
}
```

Parameter | Default | Description
--------- | ------- | -----------
 price | - | Ticket price (in specified currency).
 airline | - | IATA code of airline operating the flight.
 flight_number | - | Flight number.
 departure_at | - | Departure date.
 return_at | - | Return date.
 expires_at | - | Date on which the found price expires (UTC+0). 

## Tickets for each day of month

Returns the cheapest non-stop, one-stop, and two-stop flights for the selected route for each day of the selected month.

> Example of request:

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/v1/prices/calendar?depart_date=2017-11&origin=MOW&destination=BCN&calendar_type=departure_date&currency=USD' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/http'

url = URI("http://api.travelpayouts.com/v1/prices/calendar?depart_date=2017-11&origin=MOW&destination=BCN&calendar_type=departure_date&currency=USD")

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
  CURLOPT_URL => "http://api.travelpayouts.com/v1/prices/calendar?depart_date=2017-11&origin=MOW&destination=BCN&calendar_type=departure_date&currency=USD",
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

url = "http://api.travelpayouts.com/v1/prices/calendar"

querystring = {"depart_date":"2017-11","origin":"MOW","destination":"BCN","calendar_type":"departure_date","currency":"USD"}

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

`GET http://api.travelpayouts.com/v1/prices/calendar?depart_date=2016-11&origin=MOW&destination=BCN&calendar_type=departure_date&token=PutHereYourToken`

### Request parameters

Parameter | Default | Description
--------- | ------- | -----------
origin | - | IATA code of departure city. IATA code is shown by uppercase letters, for example MOW.
 destination | - | IATA code of destination city. IATA code is shown by uppercase letters, for example MOW.
 departure_date | - | Day or month of departure (yyyy-mm-dd or yyyy-mm).
 return_date** *(optional)* | - | Day or month of return (yyyy-mm-dd or yyyy-mm). **Pay attention!** If the return_date is not specified, you will get the "One way" flights.
 calendar_type | - | Field used to build the calendar. Equal to either: departure_date or return_date
 length *(optional)* | - |Length of stay in the destination city.
 token | - | Individual affiliate token.
currency | RUB | Currency of prices

### Response

> The above command returns JSON structured like this:

```json
{
    "success": true,
    "data": {
        "2015-06-01": {
            "origin": "MOW",
            "destination": "BCN",
            "price": 12449,
            "transfers": 1,
            "airline": "PS",
            "flight_number": 576,
            "departure_at": "2015-06-01T06:35:00Z",
            "return_at": "2015-07-01T13:30:00Z",
            "expires_at": "2015-01-07T12:34:14Z"
        }
    }
}
```

Parameter | Default | Description
--------- | ------- | -----------
 origin | - | IATA code of departure city.
 destination | - | IATA code of destination city.
 price | - | Ticket price in the specified currency.
 transfers | - | Number of stops.
 airline | - | IATA code of airline.
 flight_number | - |Flight number.
 departure_at | - | Departure Date.
 return_at | - | Return Date.
 expires_at | - | When the found price expires (UTC+0). 

## Popular airline routes

Returns routes for which an airline operates flights, sorted by popularity.

> Example of request:

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/v1/airline-directions?airline_code=SU&limit=10' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/http'

url = URI("http://api.travelpayouts.com/v1/airline-directions?airline_code=SU&limit=10")

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
  CURLOPT_URL => "http://api.travelpayouts.com/v1/airline-directions?airline_code=SU&limit=10",
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

url = "http://api.travelpayouts.com/v1/airline-directions"

querystring = {"airline_code":"SU","limit":"10"}

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

`GET http://api.travelpayouts.com/v1/airline-directions?airline_code=SU&limit=10&token=PutHereYourToken`

### Request parameters

Parameter | Default | Description
--------- | ------- | -----------
 airline_code | - | IATA code of airline.
 limit | - | Records limit per page. Default value is 100. Not less than 1000.
 token | - | Individual affiliate token.

### Response

> The above command returns JSON structured like this:

```json
{
    "success": true,
    "data": {
        "MOW-BKK": 187491,
        "MOW-BCN": 113764,
        "MOW-PAR": 91889,
        "MOW-NYC": 77417,
        "MOW-PRG": 71449,
        "MOW-ROM": 67190,
        "MOW-TLV": 62132,
        "MOW-HKT": 58549,
        "MOW-GOI": 47341,
        "MOW-IST": 45553
    },
    "error": null,
    "currency":"rub"
}
```

### Description of response

Returns a list of popular routes of an airline, sorted by popularity.

## The calendar of prices for a week

Brings the prices for the nearest dates to the target ones back.

> Example of request:

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

## The popular directions from a city

Brings the most popular directions from a specified city back.

> Example of request:

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/v1/city-directions?origin=MOW&currency=usd' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/http'

url = URI("http://api.travelpayouts.com/v1/city-directions?origin=MOW&currency=usd")

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
  CURLOPT_URL => "http://api.travelpayouts.com/v1/city-directions?origin=MOW&currency=usd",
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

url = "http://api.travelpayouts.com/v1/city-directions"

querystring = {"origin":"MOW","currency":"usd"}

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

`GET http://api.travelpayouts.com/v1/city-directions?origin=MOW&currency=usd&token=PutHereYourToken`

### Request parameters

Parameter | Default | Description
--------- | ------- | -----------
 currency | RUB | The airline tickets currency.
 origin | - | The point of departure. The IATA city code or the country code. The length - from 2 to 3 symbols.
 token | - | Individual affiliate token.

### Response

> The above command returns JSON structured like this:

```json
{
    "success":true,
    "data":{
        "AER":{
            "origin":"MOW",
            "destination":"AER",
            "price":3673,
            "transfers":0,
            "airline":"WZ",
            "flight_number":125,
            "departure_at":"2016-03-08T16:35:00Z",
            "return_at":"2016-03-17T16:05:00Z",
            "expires_at":"2016-02-22T09:32:44Z"
        }
    },
    "error":null,
    "currency":"rub"
}
```

Parameter | Default | Description
--------- | ------- | -----------
 origin | - | The point of departure.
 destination | - | The point of destination.
 departure_at | - | The date of departure.
 return_at | - | The date of return.
 expires_at | - | Date on which the found price expires (UTC+0).
number_of_changes | - |The number of transfers.
 price | - | The cost of a flight, in the currency specified.
found_at | - | The time and the date, for which a ticket was found.
 transfers | - | The number of direct.
 airline | - | IATA of airline.
 flight_number | - | Flight number.
 currency | - | Currency of response.

## Data of countries in json format

The query returns a file with a list of countrys from the database. 

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/data/countries.json' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
import requests

url = "http://api.travelpayouts.com/v1/city-directions"

querystring = {"origin":"MOW","currency":"usd"}

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "http://api.travelpayouts.com/data/countries.json",
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

url = "http://api.travelpayouts.com/data/countries.json"

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers)

print(response.text)
```

### Request

GET `http://api.travelpayouts.com/data/countries.json`

### Response

> The above command returns JSON structured like this:

```json
[{
    "code":"NC",
    "name":"New Caledonia",
    "currency":"XPF",
    "name_translations":{
        "de":"Neukaledonien",
        "en":"New Caledonia",
        "tr":"Yeni Kaledonya",
        "ru":"Новая Каледония",
        "fr":"Nouvelle-Caledonie",
        "es":"Nueva Caledonia",
        "it":"Nuova Caledonia"
    }}
]
```

Parameter | Default | Description
--------- | ------- | -----------
 code | - | IATA-code of country.
 name | - | Country name.
 currency | - | Currency country.
 name_translations | - | Translation of country name.

## City data in json format

The query returns a file with a list of cities from the database. 

> Example of request:

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/data/cities.json' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/http'

url = URI("http://api.travelpayouts.com/data/cities.json")

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
  CURLOPT_URL => "http://api.travelpayouts.com/data/cities.json",
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

url = "http://api.travelpayouts.com/data/cities.json"

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers)

print(response.text)
```

### Request

GET `http://api.travelpayouts.com/data/cities.json`

### Response

> The above command returns JSON structured like this:

```json
[{
    "code":"SCE",
    "name":"State College",
    "coordinates":{
        "lon":-77.84823,
        "lat":40.85372
    },
    "time_zone":"America/New_York",
    "name_translations":{
        "de":"State College",
        "en":"State College",
        "zh-CN":"???",
        "tr":"State College",
        "ru":"Стейт Колледж",
        "it":"State College",
        "es":"State College",
        "fr":"State College",
        "th":"??????????"
    },
    "country_code":"US"
}]
```

Parameter | Default | Description
--------- | ------- | -----------
 code | - | City IATA-code.
 name | - | City name.
 coordinates | - | City coordinates.
 time_zone | - | Timezone relative to GMT.
 name_translations | - | Translation of city name.
 country_code | - | Country IATA-code.

## Airport data in json format

The query returns a file with a list of airports from the database. 

> Example of request:

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/data/airports.json' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/http'

url = URI("http://api.travelpayouts.com/data/airports.json")

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
  CURLOPT_URL => "http://api.travelpayouts.com/data/airports.json",
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

url = "http://api.travelpayouts.com/data/airports.json"

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers)

print(response.text)
```

### Request

GET `http://api.travelpayouts.com/data/airports.json`

### Response

> The above command returns JSON structured like this:

```json
[{
    "code":"MQP",
    "name":"Kruger Mpumalanga International Airport",
    "coordinates":{
        "lon":31.098131,
        "lat":-25.384947
    },
    "time_zone":"Africa/Johannesburg",
    "name_translations":{
        "de":"Nelspruit",
        "en":"Kruger Mpumalanga International Airport",
        "tr":"International Airport",
        "it":"Kruger Mpumalanga",
        "fr":"Kruger Mpumalanga",
        "es":"Kruger Mpumalanga",
        "th":"???????????????"
    },
    "country_code":"ZA",
    "city_code":"NLP"
}]
```

Parameter | Default | Description
--------- | ------- | -----------
 code | - | Airport IATA code.
 name | - | Airport name.
 lon | - | Airport longitude.
 lat | - | Airport latitude.
 time_zone | - | Time zone relative to GMT.
 name_translations | - | The name of the airport in different languages.
 country_code | - | Country IATA code.
 city_code | - | City IATA code.

## Airline data in json format

The query returns a file with a list of airlines from the database. 

> Example of request:

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/v1/city-directions?origin=MOW&currency=usd' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/http'

url = URI("http://api.travelpayouts.com/data/airlines.json")

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
  CURLOPT_URL => "http://api.travelpayouts.com/data/airlines.json",
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

url = "http://api.travelpayouts.com/data/airlines.json"

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers)

print(response.text)
```

### Request

GET `http://api.travelpayouts.com/data/airlines.json`

### Response

> The above command returns JSON structured like this:

```json
[{
    "name":"Private flight",
    "alias":null,
    "iata":null,
    "icao":null,
    "callsign":null,
    "country":null,
    "is_active":true
}]
```

Parameter | Default | Description
--------- | ------- | -----------
 name | - | Airline name.
 alias | - | Alliance name (if the airline is an alliance member).
 iata | - | Airline IATA code.
 icao | - | Airline ICAO code.
 callsign | - | Airline call sign.
 country | - | Airline country of registration.
 is_active | - | True: company is active, false: company is not active.

## Alliance data in json format

The query returns a file with a list of alliances from the database. 

> Example of request:

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/data/airlines_alliances.json' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'rubygems' if RUBY_VERSION < '1.9'
require 'rest_client'

headers  = {:x_access_token => "YOUR_API_TOKEN_HERE"}
response = RestClient.get "http://api.travelpayouts.com/data/airlines_alliances.json", headers
puts response
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "http://api.travelpayouts.com/data/airlines_alliances.json",
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
request = Request("http://api.travelpayouts.com/data/airlines_alliances.json", headers=headers)
response_body = urlopen(request).read()
print response_body
```

### Request

GET `http://api.travelpayouts.com/data/airlines_alliances.json`

### Response

> The above command returns JSON structured like this:

```json
[{
    "name":"oneworld",
    "airlines":["4M","AA","AB","BA","CX","AY","HG","IB","JC","JL","JO","KA","LA","LP","MA","MN","MX","NU","QF","RJ","S7","XL"]
}]
```

Parameter | Default | Description
--------- | ------- | -----------
 name | - | Alliance name.
 airlines | - | Codes for alliance member companies.

## Airplane data in json format

The query returns a file with a list of airplanes from the database. 

> Example of request:

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/data/planes.json' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'rubygems' if RUBY_VERSION < '1.9'
require 'rest_client'

headers  = {:x_access_token => "YOUR_API_TOKEN_HERE"}
response = RestClient.get "http://api.travelpayouts.com/data/planes.json", headers
puts response
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "http://api.travelpayouts.com/data/planes.json",
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
request = Request("http://api.travelpayouts.com/data/planes.json", headers=headers)
response_body = urlopen(request).read()
print response_body
```

### Request

GET `http://api.travelpayouts.com/data/planes.json`

### Response

> The above command returns JSON structured like this:

```json
[{
    "code":"100",
    "name":"Fokker 100"
}]
```

Parameter | Default | Description
--------- | ------- | -----------
 code | - | Plane IATA code.
 name | - | Plane name.

## Routes list in json format

The query returns a file with a list of routes from the database.

> Example of request:

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/data/routes.json' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'rubygems' if RUBY_VERSION < '1.9'
require 'rest_client'

headers  = {:x_access_token => "YOUR_API_TOKEN_HERE"}
response = RestClient.get "http://api.travelpayouts.com/data/routes.json", headers
puts response
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "http://api.travelpayouts.com/data/routes.json",
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
request = Request("http://api.travelpayouts.com/data/routes.json", headers=headers)
response_body = urlopen(request).read()
print response_body
```

### Request

GET `http://api.travelpayouts.com/data/planes.json`

### Response

> The above command returns JSON structured like this:

```json
[{
    "airline_iata":"2B",
    "airline_icao":null,
    "departure_airport_iata":"AER",
    "departure_airport_icao":null,
    "arrival_airport_iata":"DME",
    "arrival_airport_icao":null,
    "codeshare":false,
    "transfers":0,
    "planes":[
        "CR2"
    ]
}]
```

Parameter | Default | Description
--------- | ------- | -----------
 airline_iata | - | IATA of airline.
 airline_icao | - | ICAO of airline.
 departure_airport_iata | - | IATA of airport of departure.
 departure_airport_icao | - | ICAO of airport of departure.
 arrival_airport_iata | - | IATA of airport of arrival.
 arrival_airport_icao | - | ICAO of airport of arrival.
 codeshare | - | It shows whether the flight performs the same company that sells the ticket.
 transfers | - | The number of direct.
 planes | - | IATA of airplane.

## The definition of a user's location by IP address

The query is returned the IATA-code and the name of nearest city from the user.

> Example of request:

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

## Reduction of prices into the other currency

Brings the current rate of all popular currencies to RUB back.

> Example of request:

```shell
curl --request GET \
  --url 'http://yasen.aviasales.ru/adaptors/currency.json'
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/http'

url = URI("http://yasen.aviasales.ru/adaptors/currency.json")

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
  CURLOPT_URL => "http://yasen.aviasales.ru/adaptors/currency.json",
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

url = "http://yasen.aviasales.ru/adaptors/currency.json"

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers)

print(response.text)
```

### Request

`GET http://yasen.aviasales.ru/adaptors/currency.json`

### Response

> The above command returns JSON structured like this:

```json
{
    "cny":8.24394,
    "eur":57.1578,
    "mzn":1.49643,
    "nio":1.97342,
    "usd":51.1388,
    "hrk":7.48953
}
```

## Special offers

Brings the recent special offers from the airline companies back in the .XML format.

### Request

`GET http://api.travelpayouts.com/v2/prices/special-offers`