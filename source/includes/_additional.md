# Additional API methods
 
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
    * **flights_number** - the flight's number
    * **min_flight_duration** - minimum flight duration for flights
      * **days** - flight duration in days
      * **hours** - flight duration in hours
      * **min** - flight duration in minutes
  * **subtitle**:
    * **origin** - information about the origin point:
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
    * **airline_logo** - the logo for an airline company
    * **airline_code** - the airline company IATA code
    * **airline_name** - the airline company name
    * **flight_number** - the flight number
    * **op_days** - daily flight of the week
    * **choose_dates_url** - the URL for chosen dates
    * **origin_iata** - the origin IATA code
    * **destination_iata** - the destination IATA code
