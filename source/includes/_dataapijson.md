# API for different data in JSON format

<aside class="notice">
Note! The data in the JSON files is updated no more than twice a year.
</aside>

## Data of countries in JSON format

The query returns a file with a list of countries from the database. 

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/data/countries.json' \
  --header 'x-access-token: 321d6a221f8926b5ec41ae89a3b2ae7b'
```

```ruby
require 'uri'
require 'net/http'

url = "http://api.travelpayouts.com/data/countries.json"
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

## City data in JSON format

The query returns a file with a list of cities from the database. 

> Example of a request:

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

## Airline data in JSON format

The query returns a file with a list of airlines from the database. 

> Example of a request:

```shell
curl --request GET \
  --url 'http://api.travelpayouts.com/data/airlines.json' \
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

## Alliance data in JSON format

The query returns a file with a list of alliances from the database. 

> Example of a request:

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
 airline_iata | - | IATA of an airline.
 airline_icao | - | ICAO of an airline.
 departure_airport_iata | - | IATA of an airport of departure.
 departure_airport_icao | - | ICAO of an airport of departure.
 arrival_airport_iata | - | IATA of an airport of arrival.
 arrival_airport_icao | - | ICAO of an airport of arrival.
 codeshare | - | It shows whether the flight performs the same company that sells the ticket.
 transfers | - | The number of directs.
 planes | - | IATA of an airplane.
