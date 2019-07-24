# Flight Data Access API v1

Travelpayouts Flight Data API – the way to get travel insights for your site or blog. You can get flight price trends and find popular destinations for your customers.

<aside class="notice">
Dear partners! Attention, the data is transferred from the cache, so it is recommended to use them to generate static pages.
</aside>

To access the API you must pass your token in the X-Access-Token header or in the token parameter. To obtain a token for the Data Access API, go to https://www.travelpayouts.com/developers/api.

Dates are accepted in the formats YYYY-MM and YYYY-MM-DD.

The server response is always sent in JSON format with the following structure:

  - **success** – true for a successful request, false in case of errors;
  - **data** – a result of the request; in case of an error is equal to null;
  - **error** – short description of the error that prevented request completion; for a successful request is equal to null.

Dates and times are given in UTC, formatted according to [ISO 8601](https://ru.wikipedia.org/wiki/ISO_8601). Prices are given in rubles as of when the ticket is put in the search results. It is not recommended to use expired prices (the approximate expiration date is given in the value of the expires_at parameter).

<aside class="warning">
Important. We strongly urge receiving data in compressed GZIP format, which saves a significant amount of time in receiving the response. To get data in compressed form, send the header Accept-Encoding: gzip, deflate.
</aside>

To obtain access to the API for searching for plane tickets and hotels, [send a request](https://support.travelpayouts.com/hc/en-us/requests/new).

## Cheapest tickets

Returns the cheapest non-stop tickets, as well as tickets with 1 or 2 stops, for the selected route with departure/return date filters.

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/a2e83057d1fc995298dd)

> Example of a request:

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/v1/prices/cheap?origin=MOW&destination=HKT&depart_date=2017-11&return_date=2017-12' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/v1/prices/cheap?origin=MOW&destination=HKT&depart_date=2017-11&return_date=2017-12")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)
request["x-access-token"] = '321d6a221f8926b5ec41ae89a3b2ae7b'

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/v1/prices/cheap?origin=MOW&destination=HKT&depart_date=2017-11&return_date=2017-12",
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

url = "https://api.travelpayouts.com/v1/prices/cheap"

querystring = {"origin":"MOW","destination":"HKT","depart_date":"2017-11","return_date":"2017-12"}

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

`GET https://api.travelpayouts.com/v1/prices/cheap?origin=MOW&destination=HKT&depart_date=2016-11&return_date=2016-12&token=PutHereYourToken`

<aside class="warning">
Important Old dates may be specified in a query. No error will be generated, but no data will be returned.
</aside>

### Request parameters

Parameter | Default | Description
--------- | ------- | -----------
 origin | - | IATA code of the departure city. IATA code is shown by uppercase letters, for example, MOW.
 destination | - | IATA code of the destination city (for all routes, enter "-"). IATA code is shown by uppercase letters, for example, MOW.
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

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/a2e83057d1fc995298dd)

> Example of a request:

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/v1/prices/cheap?origin=MOW&destination=HKT&depart_date=2017-11&return_date=2017-12' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/v1/prices/direct?origin=MOW&destination=LED&depart_date=2017-11&return_date=2017-12")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)
request["x-access-token"] = '321d6a221f8926b5ec41ae89a3b2ae7b'

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/v1/prices/direct?origin=MOW&destination=LED&depart_date=2017-11&return_date=2017-12",
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

url = "https://api.travelpayouts.com/v1/prices/direct"

querystring = {"origin":"MOW","destination":"LED","depart_date":"2017-11","return_date":"2017-12"}

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

`GET https://api.travelpayouts.com/v1/prices/direct?origin=MOW&destination=LED&depart_date=2016-11&return_date=2016-12&token=PutHereYourToken`

### Request parameters

Parameter | Default | Description
--------- | ------- | -----------
origin | - | IATA code of departure city. IATA code is shown by uppercase letters, for example, MOW.
destination | - | IATA code of destination city (for all routes, enter “-”). IATA code is shown by uppercase letters, for example, MOW.
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

## Tickets for each day of a month

Returns the cheapest non-stop, one-stop, and two-stop flights for the selected route for each day of the selected month.

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/a2e83057d1fc995298dd)

> Example of a request:

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/v1/prices/calendar?depart_date=2017-11&origin=MOW&destination=BCN&calendar_type=departure_date&currency=USD' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/v1/prices/calendar?depart_date=2017-11&origin=MOW&destination=BCN&calendar_type=departure_date&currency=USD")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)
request["x-access-token"] = '321d6a221f8926b5ec41ae89a3b2ae7b'

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/v1/prices/calendar?depart_date=2017-11&origin=MOW&destination=BCN&calendar_type=departure_date&currency=USD",
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

url = "https://api.travelpayouts.com/v1/prices/calendar"

querystring = {"depart_date":"2017-11","origin":"MOW","destination":"BCN","calendar_type":"departure_date","currency":"USD"}

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

`GET https://api.travelpayouts.com/v1/prices/calendar?depart_date=2016-11&origin=MOW&destination=BCN&calendar_type=departure_date&token=PutHereYourToken`

### Request parameters

Parameter | Default | Description
--------- | ------- | -----------
origin | - | IATA code of departure city. IATA code is shown by uppercase letters, for example MOW.
 destination | - | IATA code of destination city. IATA code is shown by uppercase letters, for example MOW.
 departure_date | - | Day or month of departure (yyyy-mm-dd or yyyy-mm).
 return_date *(optional)* | - | Day or month of return (yyyy-mm-dd or yyyy-mm). **Pay attention!** If the return_date is not specified, you will get the "One way" flights.
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

## Cheapest tickets grouped by month

Returns the cheapest non-stop tickets, as well as tickets with 1 or 2 stops, for the selected route grouped by month.

### HTTP Request

`GET http://api.travelpayouts.com/v1/prices/monthly?currency=USD&origin=MOW&destination=HKT&token=PutHereYourToken`

### Request parameters

> Example of request:

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/v1/prices/monthly?currency=USD&origin=MOW&destination=HKT' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/http'

url = URI("http://api.travelpayouts.com/v1/prices/monthly?currency=USD&origin=MOW&destination=HKT")

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
  CURLOPT_URL => "http://api.travelpayouts.com/v1/prices/monthly?currency=USD&origin=MOW&destination=HKT",
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

url = "http://api.travelpayouts.com/v1/prices/monthly"

querystring = {"origin":"MOW","destination":"BCN","currency":"USD"}

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

Parameter | Default | Description
--------- | ------- | -----------
origin | - | IATA code of departure city. IATA code is shown by uppercase letters, for example MOW.
destination | - | IATA code of destination city. IATA code is shown by uppercase letters, for example MOW.
currency | RUB | Currency of prices.
token | - | Individual affiliate token.

### Response

> The above command returns JSON structured like this:

```json
{  
   "success":true,
   "data":{  
      "2019-07":{  
         "origin":"MOW",
         "destination":"LON",
         "price":166,
         "transfers":1,
         "airline":"W6",
         "flight_number":7898,
         "departure_at":"2019-07-31T14:10:00Z",
         "return_at":"2019-08-31T19:15:00Z",
         "expires_at":"2019-07-27T03:07:40Z"
      }
   },
   "error":null,
   "currency":"USD"
}
```

### Response parameters

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
 currency | - | Currency of prices. 

## Popular airline routes

Returns routes for which an airline operates flights, sorted by popularity.

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/a2e83057d1fc995298dd)

> Example of a request:

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/v1/airline-directions?airline_code=SU&limit=10' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/v1/airline-directions?airline_code=SU&limit=10")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)
request["x-access-token"] = '321d6a221f8926b5ec41ae89a3b2ae7b'

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/v1/airline-directions?airline_code=SU&limit=10",
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

url = "https://api.travelpayouts.com/v1/airline-directions"

querystring = {"airline_code":"SU","limit":"10"}

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

`GET https://api.travelpayouts.com/v1/airline-directions?airline_code=SU&limit=10&token=PutHereYourToken`

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

## The popular directions from a city

Brings the most popular directions from a specified city back.

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/a2e83057d1fc995298dd)

> Example of a request:

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/v1/city-directions?origin=MOW&currency=usd' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/v1/city-directions?origin=MOW&currency=usd")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)
request["x-access-token"] = '321d6a221f8926b5ec41ae89a3b2ae7b'

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/v1/city-directions?origin=MOW&currency=usd",
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

url = "https://api.travelpayouts.com/v1/city-directions"

querystring = {"origin":"MOW","currency":"usd"}

headers = {'x-access-token': '321d6a221f8926b5ec41ae89a3b2ae7b'}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

`GET https://api.travelpayouts.com/v1/city-directions?origin=MOW&currency=usd&token=PutHereYourToken`

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
 transfers | - | The number of directs.
 airline | - | IATA of an airline.
 flight_number | - | Flight number.
 currency | - | Currency of response.
