# Additional API methods

## Visas information

The request returned information about visa rules for Russian citizens.

> Request example

```shell
curl --request GET \
  --url 'https://overmind.jetradar.com/api/ru/visas?api_key=afbadb4ff8485c0adcba486b4ca90cc4' \
  --header 'x-access-token: YOUR_API_TOKEN_HERE'
```

```ruby
require 'rubygems' if RUBY_VERSION < '1.9'
require 'rest_client'

headers  = {:x_access_token => "YOUR_API_TOKEN_HERE"}
response = RestClient.get "https://overmind.jetradar.com/api/ru/visas?api_key=afbadb4ff8485c0adcba486b4ca90cc4", headers
puts response
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://overmind.jetradar.com/api/ru/visas?api_key=afbadb4ff8485c0adcba486b4ca90cc4",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_HTTPHEADER => array(
    "x-access-token: YOUR_API_TOKEN_HERE"
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
request = Request("https://overmind.jetradar.com/api/ru/visas?api_key=afbadb4ff8485c0adcba486b4ca90cc4", headers=headers)
response_body = urlopen(request).read()
print response_body
```

### Request

`GET https://overmind.jetradar.com/api/ru/visas?api_key=afbadb4ff8485c0adcba486b4ca90cc4`

### Request parameters

* **api_key** - your API key

### Response

> Response example

```
[
  {
    "transit_visa_hours": null,
    "is_schengen": false,
    "have_transit_visa": null,
    "get_visa_online": false,
    "get_visa_on_arrival": false,
    "get_visa_in_visa_center": null,
    "entry_by_visa": false,
    "entry_by_local_passport": null,
    "entry_by_international_passport": true,
    "destination_country_id": "4eda5f298792904be400009d",
    "destination_country_code": "DM",
    "created_at": "2019-01-22T11:44:53Z",
    "citizen_country_id": "4eda5f2d8792904be4000193",
    "citizen_country_code": "RU",
    "arrival_visa_hours": 504,
    "_id": null
  }
]
```

### Response parameters

 * transit_visa_hours - how much hours you can stay in the country by transit visa
 * is_schengen - is it possible to enter on a Schengen visa
 * have_transit_visa - deprecated
 * get_visa_online - is it possible to get visa online 
 * get_visa_on_arrival - is it possible to get visa on arrival
 * get_visa_in_visa_center - deprecated
 * entry_by_visa - if visa needed to entry
 * entry_by_local_passport - if you can entry with local passport
 * entry_by_international_passport - if visa-free entry possible
 * destination_country_id - the destination country id
 * destination_country_code - the destination country IATA code
 * created_at - when the data was added to the database
 * citizen_country_id - the citizen country id
 * citizen_country_code - the citizen country IATA code
 * arrival_visa_hours - duration of possible stay in hours
 * _id - deprecated
 
## Routes schedule

The routes schedule API returns information about direct flights from one city or airport to another. 

> Example of a request:

```shell
curl --request GET \
  --url 'https://suggest.travelpayouts.com/api_flight_schedule?origin=BAX&destination=MOW&airline=SU&locale=ru&service=api_flight_schedule' \
  --header 'x-access-token: YOUR_API_TOKEN_HERE'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://suggest.travelpayouts.com/api_flight_schedule?origin=BAX&destination=MOW&airline=SU&locale=ru&service=api_flight_schedule")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)
request["x-access-token"] = 'YOUR_API_TOKEN_HERE'

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://suggest.travelpayouts.com/api_flight_schedule?origin=BAX&destination=MOW&airline=SU&locale=ru&service=api_flight_schedule",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_HTTPHEADER => array(
    "x-access-token: YOUR_API_TOKEN_HERE"
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

url = "https://suggest.travelpayouts.com/api_flight_schedule"

querystring = {"origin":"MOW","destination":"HKT","airline":"SU","locale":"ru","service":"api_flight_schedule"}

headers = {'x-access-token': 'YOUR_API_TOKEN_HERE'}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

`GET https://suggest.travelpayouts.com/api_flight_schedule?origin=BAX&destination=MOW&airline=SU&locale=ru&service=api_flight_schedule`

### Request parameters

 * origin - IATA code of the departure city. IATA code is shown by uppercase letters, for example, MOW
 * destination - IATA code of the destination city (for all routes, enter "-"). IATA code is shown by uppercase letters, for example, MOW
 * airline - IATA code of the airline
 * locale - locale of response
 * service - system parameters, should be api_flight_schedule

### Response

> Sample response

```
{
  "result": {
    "title": {
      "flights_every_day": false,
      "flights_number": 10,
      "min_flight_duration": {
        "days": 0,
        "hours": 4,
        "min": 15
      }
    },
    "subtitle": {
      "origin": {
        "city": "Барнаул",
        "country": "Россия",
        "airport": "Барнаул"
      },
      "destination": {
        "city": "Москва",
        "country": "Россия",
        "airport": ""
      }
    },
    "direct_flights": [
      {
        "depart_time": "07:05",
        "arrival_time": "07:35",
        "arrival_day_indicator": 0,
        "airline_logo": "https://pics.avs.io/al_square/32/32/SU@2x.png",
        "airline_code": "SU",
        "airline_name": "Аэрофлот",
        "flight_number": 1431,
        "op_days": [
          false,
          true,
          true,
          true,
          true,
          true,
          true
        ],
        "choose_dates_url": "https://search.aviasales.ru/?marker=16886&origin_iata=BAX&destination_iata=SVO&locale=ru&open_datepicker=true",
        "origin_iata": "BAX",
        "destination_iata": "SVO"
      },
      {
        "depart_time": "18:20",
        "arrival_time": "18:35",
        "arrival_day_indicator": 0,
        "airline_logo": "https://pics.avs.io/al_square/32/32/SU@2x.png",
        "airline_code": "SU",
        "airline_name": "Аэрофлот",
        "flight_number": 1433,
        "op_days": [
          false,
          true,
          true,
          true,
          false,
          true,
          false
        ],
        "choose_dates_url": "https://search.aviasales.ru/?marker=16886&origin_iata=BAX&destination_iata=SVO&locale=ru&open_datepicker=true",
        "origin_iata": "BAX",
        "destination_iata": "SVO"
      }
    ]
  }
}
```

* **result** - the obtained result
  * **title**:
    * **flights_every_day** - is avaiable flights every day
    * **flights_number** - the flights number
    * **min_flight_duration** - minimum flight duration for flights
      * **days** - flight duration in days
      * **hours** - flight duration in hours
      * **min** - flight duration in minutes
  * **subtitle**:
    * **origin** - information about the origin destination:
      * **city** - city of origin
      * **country** - country of origin
      * **airport** - airport name of origin
    * **destination** - information about final destination:
      * **city** - city of destination
      * **country** - country of destination
      * **airport** - airport name of destination
  * **direct_flights** - information about direct flights:
    * **depart_time** - the depart time for the flight
    * **arrival_time** - the arrival time for the flight
    * **arrival_day_indicator** - the indicator for the arrival day
    * **airline_logo** - the logo for airline company
    * **airline_code** - the airline company IATA code
    * **airline_name** - the airline company name
    * **flight_number** - the flight number
    * **op_days** - daily flight of the week
    * **choose_dates_url** - the url for choosen dates
    * **origin_iata** - the origin IATA code
    * **destination_iata** - the destinational IATA code
