---
title: Travelpayouts API
language_tabs:
- shell
- ruby
- php
- python
search: true
code_clipboard: true
---



# Travelpayouts API

The way to get travel insights for your site or blog. You can get flight
price trends and find popular destinations for your customers.


Data is transferred from the cache, which is formed on the basis of 
searches of users of sites Aviasales for the last 48 hours. 
So it is recommended that you use them to generate static pages.


To access the API, you must pass your token in the X-Access-Token 
header or in the token parameter. To obtain a token for the Data Access 
API, go to [your account](https://www.travelpayouts.com/programs/100/tools/api).  


### Data by country (markets)  

The API uses such a thing as a market. It depends on various factors, most often it is the language of the Aviasales website where users searched for tickets.


Each search is associated with a specific market. This means that if a user searched for something on the aviasales.ru site, then the data in the cache will be only for the ru market and there will be no data for the us market (which, for example, aviasales.com is associated with).


By default, the market is determined by the place of departure (the origin parameter in the API request). If it was not possible to determine the market, then the data for the ru-market will be returned.


In all requests, you can use the market parameter to specify the market you need (for different markets, different agencies can be connected, which means that it is better for partners in America to see the cache for the us market, and not for the ru market).





# Grouped flights tickets V1 (deprecated)






# Search flight tickets for specific date interval V2






# Grouped flights tickets and search by ticket's price V3






# Reference data





## 

> Sample request

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/aviasales_resources/v3/airlines.json'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/aviasales_resources/v3/airlines.json")
request = Net::HTTP::Get.new(url)
response = https.request(request)

puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/aviasales_resources/v3/airlines.json",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
?>
```

```python
import requests
response = requests.get("https://api.travelpayouts.com/aviasales_resources/v3/airlines.json")
print(response.text)
```



### HTTP Request

GET *https://api.travelpayouts.com/aviasales_resources/v3/airlines.json*



### Query Parameters

Parameter | Type | Default | Required | Description
----------|------|---------|----------|-----------

### Response

### Errors

Code | Description
-----|------------



## 

> Sample request

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/aviasales_resources/v3/airports.json'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/aviasales_resources/v3/airports.json")
request = Net::HTTP::Get.new(url)
response = https.request(request)

puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/aviasales_resources/v3/airports.json",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
?>
```

```python
import requests
response = requests.get("https://api.travelpayouts.com/aviasales_resources/v3/airports.json")
print(response.text)
```



### HTTP Request

GET *https://api.travelpayouts.com/aviasales_resources/v3/airports.json*



### Query Parameters

Parameter | Type | Default | Required | Description
----------|------|---------|----------|-----------

### Response

### Errors

Code | Description
-----|------------



## 

> Sample request

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/aviasales_resources/v3/aliances.json'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/aviasales_resources/v3/aliances.json")
request = Net::HTTP::Get.new(url)
response = https.request(request)

puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/aviasales_resources/v3/aliances.json",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
?>
```

```python
import requests
response = requests.get("https://api.travelpayouts.com/aviasales_resources/v3/aliances.json")
print(response.text)
```



### HTTP Request

GET *https://api.travelpayouts.com/aviasales_resources/v3/aliances.json*



### Query Parameters

Parameter | Type | Default | Required | Description
----------|------|---------|----------|-----------

### Response

### Errors

Code | Description
-----|------------



## 

> Sample request

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/aviasales_resources/v3/cities.json'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/aviasales_resources/v3/cities.json")
request = Net::HTTP::Get.new(url)
response = https.request(request)

puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/aviasales_resources/v3/cities.json",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
?>
```

```python
import requests
response = requests.get("https://api.travelpayouts.com/aviasales_resources/v3/cities.json")
print(response.text)
```



### HTTP Request

GET *https://api.travelpayouts.com/aviasales_resources/v3/cities.json*



### Query Parameters

Parameter | Type | Default | Required | Description
----------|------|---------|----------|-----------

### Response

### Errors

Code | Description
-----|------------



## 

> Sample request

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/aviasales_resources/v3/countries.json'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/aviasales_resources/v3/countries.json")
request = Net::HTTP::Get.new(url)
response = https.request(request)

puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/aviasales_resources/v3/countries.json",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
?>
```

```python
import requests
response = requests.get("https://api.travelpayouts.com/aviasales_resources/v3/countries.json")
print(response.text)
```



### HTTP Request

GET *https://api.travelpayouts.com/aviasales_resources/v3/countries.json*



### Query Parameters

Parameter | Type | Default | Required | Description
----------|------|---------|----------|-----------

### Response

### Errors

Code | Description
-----|------------




# Flights search API: Real-time and multi-city search

With the help of API, you can get the results of requests in real time and create a Multi-City search.<br/><br/> By default, one partner may send no more than 200 queries per hour for one IP, using the airline tickets search API. This restriction may be changed if a situation so requires.
##Аccess to the flights search API


###Requirements for Search API

<ul> <li>Each search query must be initiated by the user and the results must be shown to the user in full. The results for each query must contain a buy button next to each flight option.</li> <li>The reference to the agency's website must be received only when the user clicks the Buy button. Automatic collection of all links from the answer is prohibited. Violation of this rule will disable the API search for the partner.</li> <li>It's forbidden to use our search API with the API of other metasearches of flights.</li> <li>It's forbidden to use requests with localhost IP addresses (127.0.0.1-127.255.255.255).</li> <li>It's forbidden to automatically collect data from search results using the search API.</li> <li>Page with found flights should be hidden from search engine bots using the robots.txt file. For example, if flights tickets are displayed on the page www.sitename.com/search, then robots.txt should contain the lines: `User-Agent: * Disallow: /search/`</li> <li>The conversion rate for searches via the Buy link must be 9% or more. The conversion rate from the Buy button to actual purchases must be at least 5%.</li> <li>Ajax requests to the API don’t work because the access token is passed unencrypted. You must make requests to the API from the server.</li> </ul>


###How to get access

To access the flights search API you should be registered in our <a href="https://travelpayouts.com/">travel affiliate program</a> and <a href="https://support.travelpayouts.com/hc/ru/requests/new">submit your request</a> on with the following information: <ul> <li>URL of your website;</li> <li>Design prototypes of a search result;</li> <li>Description of your project;</li> <li>How you will use the search API?</li> <li>Why aren’t the standard methods of integration (search forms, White Label, API access to data) suitable for you.</li> <li>Requirements for flights search API access.</li> </ul> 



## Flight search

> Sample request

```shell
curl --request POST \ --data-raw '{\"host\":\"your_server_host\",\"locale\":\"en\",\"marker\":\"Put_Your_Marker_Here\",\"passengers\":{\"adults\":1,\"children\":0,\"infants\":0},\"segments\":[{\"date\":\"2018-05-25\",\"destination\":\"LON\",\"origin\":\"MOW\"},{\"date\":\"2018-06-18\",\"destination\":\"MOW\",\"origin\":\"LON\"}],\"signature\":\"MD5_signature\",\"trip_class\":true,\"user_ip\":\"user_ip_address\"}' \
  --url 'https://api.travelpayouts.com/v1/flight_search'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/v1/flight_search")
request = Net::HTTP::Post.new(url)request.body = "{\"host\":\"your_server_host\",\"locale\":\"en\",\"marker\":\"Put_Your_Marker_Here\",\"passengers\":{\"adults\":1,\"children\":0,\"infants\":0},\"segments\":[{\"date\":\"2018-05-25\",\"destination\":\"LON\",\"origin\":\"MOW\"},{\"date\":\"2018-06-18\",\"destination\":\"MOW\",\"origin\":\"LON\"}],\"signature\":\"MD5_signature\",\"trip_class\":true,\"user_ip\":\"user_ip_address\"}"
response = https.request(request)

puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/v1/flight_search",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",CURLOPT_POSTFIELDS => '{\"host\":\"your_server_host\",\"locale\":\"en\",\"marker\":\"Put_Your_Marker_Here\",\"passengers\":{\"adults\":1,\"children\":0,\"infants\":0},\"segments\":[{\"date\":\"2018-05-25\",\"destination\":\"LON\",\"origin\":\"MOW\"},{\"date\":\"2018-06-18\",\"destination\":\"MOW\",\"origin\":\"LON\"}],\"signature\":\"MD5_signature\",\"trip_class\":true,\"user_ip\":\"user_ip_address\"}'),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
?>
```

```python
import requests
response = requests.post("https://api.travelpayouts.com/v1/flight_search", data="{\"host\":\"your_server_host\",\"locale\":\"en\",\"marker\":\"Put_Your_Marker_Here\",\"passengers\":{\"adults\":1,\"children\":0,\"infants\":0},\"segments\":[{\"date\":\"2018-05-25\",\"destination\":\"LON\",\"origin\":\"MOW\"},{\"date\":\"2018-06-18\",\"destination\":\"MOW\",\"origin\":\"LON\"}],\"signature\":\"MD5_signature\",\"trip_class\":true,\"user_ip\":\"user_ip_address\"}")

print(response.text)
```



### HTTP Request

POST *https://api.travelpayouts.com/v1/flight_search*



### Query Parameters

Parameter | Type | Default | Required | Description
----------|------|---------|----------|-----------

### Response

> Sample response

```json
{
  "_ga": null,
  "affiliate": true,
  "affiliate_has_sales": true,
  "auid": null,
  "chain_name": "jetradar_rt_search_native_format",
  "clean_marker": "xxxxx",
  "currency": "usd",
  "currency_rates": {
    "czk": 2.95961,
    "lak": 0.0075
  },
  "destination_country": "IT",
  "gates_count": 0,
  "geoip_city": "Unknown",
  "geoip_country": "Unknown",
  "host": "beta.aviasales.ru",
  "initiated_at": "2021-04-26 05:09:42.031853",
  "internal": false,
  "know_english": "false",
  "locale": "en",
  "marker": "xxxxx",
  "market": "dk",
  "meta": {
    "uuid": "d9266de5-7578-418f-9ddc-6b176ae45923"
  },
  "metropoly_airports": {
    "CPH": [
      "CPH",
      "CPH",
      "ZGH",
      "RKE"
    ],
    "ROM": [
      "ROM",
      "IRR",
      "FCO",
      "ROM",
      "XRJ",
      "IRT",
      "CIA"
    ]
  },
  "open_jaw": false,
  "origin_country": "DK",
  "passengers": {
    "adults": 1,
    "children": 0,
    "infants": 0
  },
  "range": "false",
  "search_depth": 60,
  "search_id": "d9266de5-7578-418f-9ddc-6b176ae45923",
  "segments": [
    {
      "date": "2021-06-24",
      "destination": "ROM",
      "destination_country": "IT",
      "origin": "CPH",
      "origin_country": "DK",
      "original_destination": "ROM",
      "original_origin": "CPH"
    },
    {
      "date": "2021-06-25",
      "destination": "CPH",
      "destination_country": "DK",
      "origin": "ROM",
      "origin_country": "IT",
      "original_destination": "CPH",
      "original_origin": "ROM"
    }
  ],
  "server_name": "zoo39.int.avs.io.yasen.bee.13",
  "show_ads": true,
  "signature": "fb7ded0ddd86270a262d832322f46093",
  "start_search_timestamp": 1524719382.03045,
  "travelpayouts_api_request": true,
  "trip_class": true,
  "user_env": {},
  "user_id": null,
  "user_ip": null
}
```

### 200

Success response

Field | Type | Description
------|------|------
geoip_city | string | the geoip of the city where the request was made
locale | string | the language of the search result
marker | string | the unique identifier of the affiliate
search_id | string | the unique identifier for the search query used to search results
trip_class | string | the class of trip
gates_count | integer | the total number of agencies
meta | object | technical information
geoip_country | string | the geoip of the country where the request was made
segments.origin | string | origin IATA or string "City, Country (IATA)". The IATA code is shown in uppercase letters (for example, "Paris, France (PAR)")
segments.date | string | departure date yyyy-mm-dd (for example, "2021-09-08")
segments.destination | string | destination IATA or string "City, Country (IATA)". The IATA code is shown in uppercase letters (for example, "Berlin, Germany (BER)")
user_ip | string | the user's IP address
uuid | string | unique identifier of the request
affiliate | string | the affiliate ID
currency_rates | object | exchange rate
host | string | host's request
passengers.adults | integer | the number of adult passengers
passengers.children | integer | the number of children
passengers.infants | integer | the number of infants

### Errors

Code | Description
-----|------------
400 | Incorrect request
500 | A techinal trouble in our system



## Getting search results

> Sample request

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/v1/flight_search_results'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/v1/flight_search_results")
request = Net::HTTP::Get.new(url)
response = https.request(request)

puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/v1/flight_search_results",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
?>
```

```python
import requests
response = requests.get("https://api.travelpayouts.com/v1/flight_search_results")
print(response.text)
```

In the body of the response is the parameter **search_id**; insert it into the URL:


https://api.travelpayouts.com/v1/flight_search_results?uuid=%search_id%


Then send the request to the server for search results:


`GET https://api.travelpayouts.com/v1/flight_search_results?uuid=%search_id%`


<aside class="notice">As a result of the search, you will get the JSON array where each element is a response from a definite agency. </aside>


<aside class="warning">Repeat the request until you get an associative array with one element search_id. The periodicity of sending requests isn't restricted. </aside>


<aside class="warning">Attention! The link to the search results is relevant for 15 minutes. After this time, you must send a search query again.</aside>

### HTTP Request

GET *https://api.travelpayouts.com/v1/flight_search_results*



### Query Parameters

Parameter | Type | Default | Required | Description
----------|------|---------|----------|-----------
search_id | string | <no value> | true | The ID from the answer of the request

### Response

> Sample response

```json
[
  {
    "_ga": null,
    "affiliate_has_sales": false,
    "airlines": {
      "S7": {
        "alliance_name": "OneWorld",
        "average_rate": "3.95",
        "id": 444,
        "name": "S7",
        "rates": "2430"
      },
      "SU": {
        "alliance_name": "SkyTeam",
        "average_rate": "4.01",
        "id": 10,
        "name": "Аэрофлот",
        "rates": "2362"
      },
      "U6": {
        "alliance_name": null,
        "average_rate": "3.62",
        "id": 503,
        "name": "Уральские авиалинии",
        "rates": "1158"
      },
      "UN": {
        "alliance_name": null,
        "average_rate": "3.98",
        "id": 492,
        "name": "Трансаэро",
        "rates": "2639"
      },
      "UT": {
        "alliance_name": null,
        "id": 507,
        "name": "ЮТэйр",
        "rates": "1843"
      }
    },
    "airports": {
      "DME": {
        "city": "Москва",
        "country": "Россия",
        "name": "Домодедово",
        "rates": "392",
        "time_zone": "Europe/Moscow"
      },
      "LED": {
        "city": "Санкт-Петербург",
        "country": "Россия",
        "name": "Пулково",
        "rates": "259",
        "time_zone": "Europe/Moscow"
      },
      "SVO": {
        "average_rate": "3.63",
        "city": "Москва",
        "country": "Россия",
        "name": "Шереметьево",
        "rates": "307",
        "time_zone": "Europe/Moscow"
      },
      "VKO": {
        "city": "Москва",
        "country": "Россия",
        "name": "Внуково",
        "rates": "211",
        "time_zone": "Europe/Moscow"
      }
    },
    "banner_info": {},
    "city_distance": 634,
    "filters_boundary": {
      "arrival_datetime_0": {
        "max": 1418950500,
        "min": 1418869200
      },
      "arrival_datetime_1": {
        "max": 1419554400,
        "min": 1419486600
      },
      "departure_minutes_0": {
        "max": 1410,
        "min": 50
      },
      "departure_minutes_1": {
        "max": 1375,
        "min": 270
      },
      "departure_time_0": {
        "max": "23:30",
        "min": "00:50"
      },
      "departure_time_1": {
        "max": "22:55",
        "min": "04:30"
      },
      "flights_duration": {
        "max": 120,
        "min": 70
      },
      "price": {
        "max": 8689,
        "min": 4431
      },
      "stops_count": {
        "0": 4431
      }
    },
    "flight_numbers": [
      [
        "SU30",
        "SU32"
      ],
      [
        "SU31",
        "SU33"
      ]
    ],
    "gates_info": {
      "20": {
        "airline_iatas": {},
        "average_rate": 4.43,
        "currency_code": "rub",
        "is_airline": false,
        "label": "OneTwoTrip",
        "mobile_version": false,
        "payment_methods": [
          "card"
        ],
        "productivity": 16.9991,
        "rates": 2967
      }
    },
    "internal": false,
    "meta": {
      "gates": [
        {
          "count": 1456,
          "duration": 22.402996063232422,
          "good_count": 1456,
          "id": 20
        }
      ],
      "uuid": "c9c6de8c-3fb4-404e-b88c-e9e0a605f183"
    },
    "proposals": [
      {
        "segment": [
          {
            "flight": [
              {
                "aircraft": "AIRBUS A320",
                "arrival": "LED",
                "arrival_date": "2021-05-25",
                "arrival_time": "12:25",
                "delay": 0,
                "departure": "VKO",
                "departure_date": "2021-05-25",
                "departure_time": "11:00",
                "duration": 85,
                "local_arrival_timestamp": 1432549200,
                "local_departure_timestamp": 1434588600,
                "number": 369,
                "operating_carrier": "UT"
              }
            ]
          },
          {
            "flight": [
              {
                "aircraft": "AIRBUS A320",
                "arrival": "DME",
                "arrival_date": "2021-06-18",
                "arrival_time": "11:35",
                "delay": 0,
                "departure": "LED",
                "departure_date": "2021-06-18",
                "departure_time": "10:05",
                "duration": 90,
                "local_arrival_timestamp": 1432549200,
                "local_departure_timestamp": 1434588600,
                "number": 6131,
                "operating_carrier": "SU"
              }
            ]
          }
        ],
        "sign": "7573ea707c2ff84b243241961412ed34",
        "terms": {
          "20": {
            "baggage_source": [
              [
                3
              ],
              [
                3
              ]
            ],
            "currency": "rub",
            "flights_baggage": [
              [
                false
              ],
              [
                false
              ]
            ],
            "flights_handbags": [
              [
                "1PC10"
              ],
              [
                "1PC10"
              ]
            ],
            "handbags_source": [
              [
                3
              ],
              [
                3
              ]
            ],
            "multiplier": 0.000001,
            "price": 18418,
            "proposal_multiplier": 1,
            "unified_price": 18418,
            "url": 18000000
          }
        },
        "xterms": {
          "180": {
            "Y_0PC;Y_0PC": {
              "baggage_source": [
                [
                  3
                ],
                [
                  3
                ]
              ],
              "currency": "rub",
              "flights_baggage": [
                [
                  false
                ],
                [
                  false
                ]
              ],
              "flights_handbags": [
                [
                  "1PC10"
                ],
                [
                  "1PC10"
                ]
              ],
              "handbags_source": [
                [
                  3
                ],
                [
                  3
                ]
              ],
              "multiplier": 0.000001,
              "price": 18418,
              "proposal_multiplier": 1,
              "unified_price": 18418,
              "url": 18000000
            }
          }
        }
      }
    ],
    "search_id": "c9c6de8c-3fb4-404e-b88c-e9e0a605f183",
    "segments": [
      {
        "date": "2021-05-25",
        "destination": "LED",
        "destination_country": "RU",
        "origin": "MOW",
        "origin_country": "RU",
        "original_destination": "LED",
        "original_origin": "MOW"
      },
      {
        "date": "2021-06-18",
        "destination": "MOW",
        "destination_country": "RU",
        "origin": "LED",
        "origin_country": "RU",
        "original_destination": "MOW",
        "original_origin": "LED"
      }
    ],
    "signature": "4bb635b9353a1e933907d41841e23414",
    "validating_carrier": "SU"
  },
  {
    "search_id": "c9c6de8c-3fb4-404e-b88c-e9e0a605f183"
  }
]
```

### 200

Success response

Field | Type | Description
------|------|------
flight_info.IATA | string | IATA code
flight_info.average_rate | integer | average rating of airport
flight_info.city | string | city where airport is located
flight_info.country | string | country where airport is located
flight_info.name | string | airport name
flight_info.ontime_percent | object | delay persant; min — min number of delay; max — max number of delay; mean — average number of delay._
flight_info.rates | integer | number of ratings
flight_info.time_zone | string | time zone of airport
gates_info.productivity | number | productivity
gates_info.average_rate | number | average rating of agencies
gates_info.currency_code | string | payment currency code
gates_info.is_airline | boolean | is an airline
gates_info.mobile_version | boolean | having a mobile version of the site
gates_info.payment_methods | []string | payment methods
gates_info.airline_iatas | object | IATA airline code, if the gate sells tickets
gates_info.label | string | agency name
gates_info.rates | integer | rating agency (count voters)
initiated_at | string | date and time of search (**deprecated**)
is_direct | boolean | true if the flight is non-stop
segments_airports | []string | IATA codes of the main departure and destination airports
currency | string | currency type (**deprecated**)
is_charter | boolean | flight is charter or not (false or true)
open_jaw | boolean | true if it is part of open jaw (**deprecated**)
rating | integer | internal information about flight rating
signature | string | signature of request
city_distance | integer | distance between the cities of origin and destination
flight.arrival | string | IATA code of arrival
flight.arrival_date | string | arrival date
flight.departure_time | string | departure time (UNIX-time)
flight.technical_stops | string | information about technical stops
flight.delay | integer | duration of stop between flights (in minutes)
flight.duration | integer | flight duration in minutes
flight.local_departure_timestamp | integer | local departure time in UNIX format
flight.marketing_carrier | string | IATA code of the airline that sells the ticket. Use it to generate a flight number. If this field is empty, use operating_carrier
flight.arrival_time | string | arrival time (UNIX-time)
flight.departure | string | departure IATA code
flight.local_arrival_timestamp | integer | local arrival time in UNIX format
flight.aircraft | string | type of aircraft
flight.departure_date | string | departure date (UNIX-time)
flight.number | integer | flight number. To generate a full flight number, use the number and **operating_carrier parameters**
flight.operating_carrier | string | IATA code of airline that performs the carriage
flight.rating_summary | integer | some rating information about agency or airline (can be blank)
search_id | string | unique identifier for the search query
sign | string | unique id of the ticket, to integrate information from different agencies in one ticket
terms.flights_baggage | [][]boolean | the number of pieces of baggage and its weight. _"" — there is no information about baggage; false — baggage is not included in a price; {int}PC{int} — number of bags by %somevalue% kilogram. For example, 2PC23 — means two baggage pieces of 23 kg. {int} — number of bags does not matter, the total weight is limited._
terms.price | integer | trip price in original currency (type listed in the field currency)
terms.unified_price | integer | price of flight in basic currency (Russian ruble)
terms.url | integer | code to generate links for buyers (as forming the link; see below)
terms.currency | string | currency type
xterms | object | contains information similar to terms, plus may contain additional data on tariffs (if it is transmitted from agencies / airlines)
clean_marker | string | affiliate marker (**deprecated**)
flight_numbers | [][]string | numbers of the flight
segment_durations | integer | total flights duration (for example, there and back)
filters_boundary.stops_duration | object | time between flights (maximum and minimum)
filters_boundary.arrival_datetime_0 | object | arrival datetime (maximum and minimum)
filters_boundary.departure_time_0 | object | departure time (maximum and minimum)
filters_boundary.flights_duration | object | flights duration (maximum and minimum)
filters_boundary.price | object | price of flights (maximum and minimum)
filters_boundary.stops_count | object | stops count
market | string | market of routes (**deprecated**)
proposals | []object | an array of variants
stops_airports | []string | IATA codes of departure airports, destination and transfers
airlines.deeplink_id | string | ID links to airline's website
airlines.deeplink_site_name | string | address of the airline's website
airlines.id | string | identification number of the airline
airlines.name | string | name of airline
airlines.rates | integer | number of ratings
airlines.site_name | string | name of the airline's website
airlines.alliance_name | string | alliance of the airline
airlines.average_rate | number | average rating
airports | object | information about airports;
uuid | string | request ID
max_stops | integer | maximum number of stops
meta.tos | string | content of error
meta.error | string | error information
meta.gates.count | integer | number of tickets uploaded from the agency
meta.gates.duration | number | processing time of request
meta.gates.good_count | integer | number of relevant tickets (if the agency has returned the ticket for the wrong dates or they are misspelled, they are filtered out by the system)
meta.gates.id | integer | ID agency
segments.date | string | departure date
segments.destination | string | destination IATA
segments.destination_country | string | code of the country of destination
segments.origin | string | origin IATA
segments.origin_country | string | the origin country
segments.original_destination | string | code of the city of destination
total_duration | integer | total flight time with stops time

### Errors

Code | Description
-----|------------
400 | Incorrect request
500 | A techinal trouble in our system



## How to get a link to the agency website

> Sample request

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/v1/flight_searches/{search_id}/clicks/{terms.url}.json'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/v1/flight_searches/{search_id}/clicks/{terms.url}.json")
request = Net::HTTP::Get.new(url)
response = https.request(request)

puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/v1/flight_searches/{search_id}/clicks/{terms.url}.json",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
?>
```

```python
import requests
response = requests.get("https://api.travelpayouts.com/v1/flight_searches/{search_id}/clicks/{terms.url}.json")
print(response.text)
```

<aside class="warning">Attention! The reference to the agency's website must be received only when the user clicks the "Buy" button. Automatic collection of all links from the answer is prohibited. Violation of this rule will disable the API search for the partner. </aside>


To get a link to the site of the ticket booking agencies send a request to the following address:


`GET https://api.travelpayouts.com/v1/flight_searches/%search_id%/clicks/%terms.url%.json`


where **search_id** is the ID from the answer of the request, **terms.url** — URL parameter from the response.


You will receive a response like in the example.


To move on to the booking, give your visitors a link from the parameter `"url"`.


The “lifetime” of such links is 15 minutes, after which you will need to search again for the current prices and generate a new reference to the transition.


In our example, this is a link of the form:


`https://www.svyaznoy.travel/?utm_source=as.ru&utm_medium=cpa&utm_campaign=meta_avia#MOW0906/BKK1506/A1/C0/I0/S0/22316/EK-132;EK-374/EK-373;EK-131&marker=7uh46i0v2`

### HTTP Request

GET *https://api.travelpayouts.com/v1/flight_searches/{search_id}/clicks/{terms.url}.json*



### Query Parameters

Parameter | Type | Default | Required | Description
----------|------|---------|----------|-----------
search_id | string | <no value> | true | The ID from the answer of the request
terms.url | string | <no value> | true | URL parameter from the response

### Response

> Sample response

```json
{
  "click_id": 22135952358110,
  "gate_id": 62,
  "method": "GET",
  "params": {},
  "url": "https://www.svyaznoy.travel/?utm_source=as.ru\u0026utm_medium=cpa\u0026utm_campaign=meta_avia#MOW0906/BKK1506/A1/C0/I0/S0/22316/EK-132;EK-374/EK-373;EK-131\u0026marker=7uh46i0v2"
}
```

### 200

Success response

### Errors

Code | Description
-----|------------
400 | Incorrect request
500 | A techinal trouble in our system




# Hotels data API





## Displays the cost of living in hotels

> Sample request

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/hotellook/v1/cached_prices?location=Saint-Petersburg&hotelId=277083&checkIn=2021-12-13&checkOut=2021-12-18&currency=rub&limit=1'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/hotellook/v1/cached_prices?location=Saint-Petersburg&hotelId=277083&checkIn=2021-12-13&checkOut=2021-12-18&currency=rub&limit=1")
request = Net::HTTP::Get.new(url)
response = https.request(request)

puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/hotellook/v1/cached_prices?location=Saint-Petersburg&hotelId=277083&checkIn=2021-12-13&checkOut=2021-12-18&currency=rub&limit=1",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
?>
```

```python
import requests
response = requests.get("https://api.travelpayouts.com/hotellook/v1/cached_prices?location=Saint-Petersburg&hotelId=277083&checkIn=2021-12-13&checkOut=2021-12-18&currency=rub&limit=1")
print(response.text)
```

The request is used to get the price of hotel rooms from the cache for the period. It doesn't contain information about room availability.

### HTTP Request

GET *https://api.travelpayouts.com/hotellook/v1/cached_prices?location=Saint-Petersburg&hotelId=277083&checkIn=2021-12-13&checkOut=2021-12-18&currency=rub&limit=1*



### Query Parameters

Parameter | Type | Default | Required | Description
----------|------|---------|----------|-----------
location | string | <no value> | true | IATA or name of a location.
checkIn | string | <no value> | true | A date of checkin.
checkOut | string | <no value> | true | A date of checkout.
locationId | string | <no value> | false | An identifier of the location, can be used instead of the location.
hotelId | string | <no value> | true | A hotel identifier.
adults | integer | 2 | false | Number of adults.
children | integer | 0 | false | Number of children (2 to 18 years).
infants | integer | 0 | false | Number of infants (0 to 2 years).
limit | integer | 4 | false | Limitation of output results from 1 to 8.
currency | string | rub | false | An currency in which prices will be given.

### Response

> Sample response

```json
{
  "hotelId": 277083,
  "hotelName": "Saint-Petersburg Hotel",
  "location": {
    "country": "Russia",
    "geo": {
      "lat": 59.95,
      "lon": 30.316667
    },
    "name": "St. Petersburg",
    "state": null
  },
  "locationId": 12196,
  "priceAvg": 32875,
  "priceFrom": 32875,
  "pricePercentile": {
    "10": 32875,
    "3": 32875,
    "35": 32875,
    "50": 32875,
    "75": 32875,
    "99": 32875
  },
  "stars": 4
}
```

### 200

Success response

Field | Type | Description
------|------|------
priceAvg | integer | Average price for a hotel room.
priceFrom | integer | A minimal price
stars | integer | Stars count
hotelId | integer | Identificator of a hotel.
hotelName | string | Hotel name
location.name | string | Location name
location.state | string | The state in which the city is located
location.country | string | A country name.
location.geo.lat | float | A latitude.
location.geo.lon | float | A longitude.
locationId | integer | Identificator of the location where a hotel is located.

### Errors

Code | Description
-----|------------



## Hotels Selections

> Sample request

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/hotellook/v1/hotels?check_in=2021-12-02&check_out=2021-12-17&currency=rub&language=ru&id=12209&type=popularity&limit=1'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/hotellook/v1/hotels?check_in=2021-12-02&check_out=2021-12-17&currency=rub&language=ru&id=12209&type=popularity&limit=1")
request = Net::HTTP::Get.new(url)
response = https.request(request)

puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/hotellook/v1/hotels?check_in=2021-12-02&check_out=2021-12-17&currency=rub&language=ru&id=12209&type=popularity&limit=1",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
?>
```

```python
import requests
response = requests.get("https://api.travelpayouts.com/hotellook/v1/hotels?check_in=2021-12-02&check_out=2021-12-17&currency=rub&language=ru&id=12209&type=popularity&limit=1")
print(response.text)
```

The request recovers the list of specific hotels according to the ID of a location. A collection is formed according to the specified period. If the period is not specified, a collection shall be formed from the hotels found for the last three days.

### HTTP Request

GET *https://api.travelpayouts.com/hotellook/v1/hotels?check_in=2021-12-02&check_out=2021-12-17&currency=rub&language=ru&id=12209&type=popularity&limit=1*



### Query Parameters

Parameter | Type | Default | Required | Description
----------|------|---------|----------|-----------
check_in | string | <no value> | true | A date of checkin.
check_out | string | <no value> | true | A date of checkout.
currency | string | <no value> | true | An currency in which prices will be given.
language | string | en | true | A language in which result will be given (ru, en, th, de, es, fr, it, pl).
limit | integer | 10 | false | limitation of output results from 1 to 100, default - 10
type | string | <no value> | false | A selection type. See */hotellook/v1/selection_types*
id | string | <no value> | false | A city identifier.

### Response

> Sample response

```json
{
  "popularity": [
    {
      "distance": 4.29,
      "has_wifi": true,
      "hotel_id": 46455041,
      "hotel_type": [
        "Городской отель",
        "Отель для индивидуальных путешественников"
      ],
      "last_price_info": {
        "insertion_time": 1638010682,
        "nights": 15,
        "price": 59752,
        "price_pn": 3983,
        "search_params": {
          "adults": 2,
          "checkIn": "2021-12-02",
          "checkOut": "2021-12-17",
          "children": []
        }
      },
      "name": "Хилтон Гарден Инн Уфа Риверсайд",
      "property_type": "hotel",
      "rating": 94,
      "stars": 4,
      "ty_summary": "Превосходный городской отель. Удобно осматривать достопримечательности, рядом есть парковки. Отличные номера и фантастический сервис. Великолепная атмосфера."
    }
  ]
}
```

### 200

Success response

Field | Type | Description
------|------|------
distance | float | distance from the city’s center (km)
hotel_id | integer | A hotel identifier
last_price_info.insertion_time | integer | Time, when the collection was found
last_price_info.nights | integer | Number of nights
last_price_info.price | integer | Price of accommodation during the whole period with a discount
ty_summary | string | Short description about hotel.
rating | float | hotel’s rating, assigned by its visitors
stars | integer | number of stars
has_wifi | boolean | Availability of Wi-Fi
hotel_type | []string | Description of a hotel’s type
name | string | A hotel's name
property_type | string | A type of an accomodation.

### Errors

Code | Description
-----|------------



## Hotel search by name or location

> Sample request

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/hotellook/v1/lookup?query=moscow&lang=ru&lookFor=both&limit=1'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/hotellook/v1/lookup?query=moscow&lang=ru&lookFor=both&limit=1")
request = Net::HTTP::Get.new(url)
response = https.request(request)

puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/hotellook/v1/lookup?query=moscow&lang=ru&lookFor=both&limit=1",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
?>
```

```python
import requests
response = requests.get("https://api.travelpayouts.com/hotellook/v1/lookup?query=moscow&lang=ru&lookFor=both&limit=1")
print(response.text)
```

Search for a specific location or name places of a hotel (city, island).

### HTTP Request

GET *https://api.travelpayouts.com/hotellook/v1/lookup?query=moscow&lang=ru&lookFor=both&limit=1*



### Query Parameters

Parameter | Type | Default | Required | Description
----------|------|---------|----------|-----------
query | string | <no value> | true | It can be set as a text, for instance: `query=moscow` or as a coordinates: `query=54.32,41.32`.
lang | string | en | false | Display language. It can take any iso-language code (pt, en, fr, de, id, it, pl, es, th, ru); if the database doesn’t include a translation for the requested language, it returns the English name of the object.
lookFor | string | both | false | Objects displayed in the results: city, hotel or both.
limit | integer | 10 | false | Limitation of output results from 1 to 10.
convertCase | integer | 1 | false | Automatically change the keyboard layout (actual for Russian users, for example, when requesting "vjcrdf" will be found "москва"). Values - 1 or 0.

### Response

> Sample response

```json
{
  "result": {
    "hotels": [
      {
        "fullName": "AZIMUT Отель Олимпик Москва, Москва, Россия",
        "id": "333526",
        "label": "AZIMUT Отель Олимпик Москва",
        "location": {
          "lat": 55.752041,
          "lon": 37.617508
        },
        "locationId": 12153,
        "locationName": "Москва, Россия"
      }
    ],
    "locations": [
      {
        "cityName": "Москва",
        "countryCode": "RU",
        "countryName": "Россия",
        "fullName": "Москва, Россия",
        "hotelsCount": "3557",
        "iata": [
          "MOW",
          "ZIA",
          "SVO",
          "VKO",
          "DME"
        ],
        "id": 12153,
        "location": {
          "lat": 55.752041,
          "lon": 37.617508
        }
      }
    ]
  },
  "status": "ok"
}
```

### 200

Success response

Field | Type | Description
------|------|------
result.hotels |  | 
result.locations | []object | List of found locations.
status | string | Status of the request.

### Errors

Code | Description
-----|------------



## The types of hotel collections

> Sample request

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/hotellook/v1/selection_types?id=12209'
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/hotellook/v1/selection_types?id=12209")
request = Net::HTTP::Get.new(url)
response = https.request(request)

puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/hotellook/v1/selection_types?id=12209",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
?>
```

```python
import requests
response = requests.get("https://api.travelpayouts.com/hotellook/v1/selection_types?id=12209")
print(response.text)
```

The request recovers the list of all available separate collections. This type is used to search for hotels with a discount.

### HTTP Request

GET *https://api.travelpayouts.com/hotellook/v1/selection_types?id=12209*



### Query Parameters

Parameter | Type | Default | Required | Description
----------|------|---------|----------|-----------
id | integer | <no value> | true | An identifier of a city

### Response

> Sample response

```json
[
  "center",
  "tophotels",
  "highprice",
  "luxury",
  "3-stars",
  "4-stars",
  "5-stars",
  "pool",
  "pets",
  "restaurant",
  "river_view",
  "cheaphotel_ufa",
  "luxury_ufa",
  "price",
  "rating",
  "distance",
  "popularity",
  "0stars",
  "1stars",
  "2stars",
  "3stars",
  "4stars",
  "5stars"
]
```

### 200

Success response

Field | Type | Description
------|------|------
cheaphotel | string | Cheapest hotels.
popularity | string | Popularity of a hotel
restaurant | string | Availability of the own restaurant.
3-stars | string | Automatic searching of the hotels, having 3 stars.
center | string | Hotels, located in the center of a city
rating | string | Hotels with the highest rating.
1stars | string | Manually formed collections with the corresponding number of stars
3stars | string | Manually formed collections with the corresponding number of stars
4-stars | string | Automatic searching of the hotels, having 4 stars.
5stars | string | Manually formed collections with the corresponding number of stars
highprice | string | Most expensive hotels
luxury | string | Luxury hotels.
pets | string | Opportunity to live with the pets.
tophotels | string | Best hotels
0stars | string | Manually formed collections with the corresponding number of stars
2stars | string | Manually formed collections with the corresponding number of stars
4stars | string | Manually formed collections with the corresponding number of stars
5-stars | string | Automatic searching of the hotels, having 5 stars.
distance | string | Distance from an airport
pool | string | Availability of the own pool.
price | string | Manually formed collections by the price.

### Errors

Code | Description
-----|------------




# Hotels glossary






# Hotels search

 <p>Search by hotel IATA-code or cityId (ID location), or hotelId (ID hotel). All options or just one can be specified. If you specify hotelId and cityId, only hotelId will be used. If you specify iata and cityId, iata will be used.</p> <p>When using this search, it is possible to access its results not immediately, but after a period of time not exceeding 15 minutes. Handling is on the request ID searchId.</p> <p><strong>Attention!</strong> The default number of requests is limited to 200 requests per hour for one IP address. If you need to process more requests, send a note to support@travelpayouts.com.</p> <p>More information about the signature is available <a href="https://support.travelpayouts.com/hc/en-us/articles/210995998">here</a></p>



## Create a search

> Sample request

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/hotellook_search/v1/create_search?start.json?iata=HKT&checkIn=2018-08-10&checkOut=2018-08-13&adultsCount=2&customerIP=100.168.1.1&childrenCount=1&childAge1=8&lang=ru&currency=USD&waitForResult=0&marker=&signature='
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/hotellook_search/v1/create_search?start.json?iata=HKT&checkIn=2018-08-10&checkOut=2018-08-13&adultsCount=2&customerIP=100.168.1.1&childrenCount=1&childAge1=8&lang=ru&currency=USD&waitForResult=0&marker=&signature=")
request = Net::HTTP::Get.new(url)
response = https.request(request)

puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/hotellook_search/v1/create_search?start.json?iata=HKT&checkIn=2018-08-10&checkOut=2018-08-13&adultsCount=2&customerIP=100.168.1.1&childrenCount=1&childAge1=8&lang=ru&currency=USD&waitForResult=0&marker=&signature=",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
?>
```

```python
import requests
response = requests.get("https://api.travelpayouts.com/hotellook_search/v1/create_search?start.json?iata=HKT&checkIn=2018-08-10&checkOut=2018-08-13&adultsCount=2&customerIP=100.168.1.1&childrenCount=1&childAge1=8&lang=ru&currency=USD&waitForResult=0&marker=&signature=")
print(response.text)
```

Create search on the server and get a search identifier.

### HTTP Request

GET *https://api.travelpayouts.com/hotellook_search/v1/create_search?start.json?iata=HKT&checkIn=2018-08-10&checkOut=2018-08-13&adultsCount=2&customerIP=100.168.1.1&childrenCount=1&childAge1=8&lang=ru&currency=USD&waitForResult=0&marker=&signature=*



### Query Parameters

Parameter | Type | Default | Required | Description
----------|------|---------|----------|-----------
iata | string | <no value> | true | A city IATA code.
checkIn | string | <no value> | true | Check-in date (format: YYYY-MM-DD).
checkOut | string | <no value> | true | Check-out date (format: YYYY-MM-DD).
adultsCount | integer | <no value> | true | Adults count.
customerIP | string | <no value> | true | IP of a user who initiated the request.
childrenCount | integer | <no value> | true | Children count.
childAge* | integer | 0 | false | `childAge1..n` - where `n = childrenCount`, ages of children (if childrenCount greater than 0). The default age is 1 year (max = 17).
lang | string | <no value> | true | The language of the search result. Stated together with the region. (en_US, en_GB, ru_RU, de_DE, en_AU, en_CA, en_IE, es_ES, fr_FR, it_IT, pl_PL, th_TH)
currency | string | <no value> | true | The currency in which the prices will be given.
waitForResult | integer | 0 | false | Wait for the completion of all searches for partners, possible values 0 or 1. 1 – the connection is open before all the data from the partners. The result is returned to the user query and its searchId. 0 – the connection will be terminated immediately and returned to the user searchId.
marker | string | <no value> | true | Value of your marker.
signature | string | <no value> | true | Value of the signature.

### Response

> Sample response

```json
{
  "searchId": "5201179",
  "status": "ok"
}
```

### 200

Success response

Field | Type | Description
------|------|------
searchId | string | Search identifier.
status | string | Status of the request.

### Errors

Code | Description
-----|------------



## Search result

> Sample request

```shell
curl --request GET \
  --url 'https://api.travelpayouts.com/hotellook_search/v1/result?searchId=4034914&limit=10&sortBy=price&sortAsc=1&roomsCount=0&offset=0&marker=&signature='
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://api.travelpayouts.com/hotellook_search/v1/result?searchId=4034914&limit=10&sortBy=price&sortAsc=1&roomsCount=0&offset=0&marker=&signature=")
request = Net::HTTP::Get.new(url)
response = https.request(request)

puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.travelpayouts.com/hotellook_search/v1/result?searchId=4034914&limit=10&sortBy=price&sortAsc=1&roomsCount=0&offset=0&marker=&signature=",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
?>
```

```python
import requests
response = requests.get("https://api.travelpayouts.com/hotellook_search/v1/result?searchId=4034914&limit=10&sortBy=price&sortAsc=1&roomsCount=0&offset=0&marker=&signature=")
print(response.text)
```

Get search result by a search identifier.

### HTTP Request

GET *https://api.travelpayouts.com/hotellook_search/v1/result?searchId=4034914&limit=10&sortBy=price&sortAsc=1&roomsCount=0&offset=0&marker=&signature=*



### Query Parameters

Parameter | Type | Default | Required | Description
----------|------|---------|----------|-----------
searchId | string | <no value> | true | The search identifier.
limit | integer | 0 | false | Maximum number of hotels, from 0 to infinity, where 0 - no limit.
offset | integer | 0 | false | To skip a number of hotels from 0 to infinity, where 0 - no hotel not passed.
sortBy | string | popularity | false | How to sort (popularity, price, name, guestScore, stars).
sortAsc | integer | 1 | false | 1 - ascending, 0 - descending.
roomsCount | integer | 0 | false | Maximum number of rooms that are returned in each hotel, from 0 to infinity, where 0 - no limit.
marker | string | <no value> | true | Value of your marker.
signature | string | <no value> | true | Value of the signature.

### Response

> Sample response

```json
{
  "result": [
    {
      "address": "23/8 Soi Hub-Aik, Phuket Road, Muang District",
      "amenities": [],
      "distance": 10.6,
      "fullUrl": "http://search.hotellook.com/?language=ru\u0026marker=16886\u0026hotelId=362691",
      "guestScore": 63,
      "id": 362691,
      "location": {
        "lat": 7.878922,
        "lon": 98.39146
      },
      "maxPrice": 138,
      "maxPricePerNight": 46,
      "minPriceTotal": 40,
      "name": "Rome Place Hotel",
      "photoCount": 50,
      "popularity": 47,
      "price": 13,
      "rating": 63,
      "rooms": [
        {
          "agencyId": "43",
          "agencyName": "Travel.ru",
          "bookingURL": "/r/?language=ru\u0026checkIn=2015-06-10¤cy=USD\u0026children=5\u0026host=v2%3A16886\u0026marker=16886\u0026transparent=1\u0026roomId=0\u0026adults=2\u0026locationId=30553\u0026checkOut=2015-06-13\u0026gateId=43\u0026hotelId=362691",
          "desc": "Double or Twin STANDARD",
          "fullBookingURL": "http://search.hotellook.com/r?language=ru\u0026checkIn=2015-06-10\u0026cy=USD\u0026children=5\u0026host=v2%3A16886\u0026marker=16886\u0026transparent=1\u0026roomId=0\u0026adults=2\u0026locationId=30553\u0026checkOut=2015-06-13\u0026gateId=43\u0026hotelId=362691",
          "internalTypeId": "1",
          "options": {
            "available": 5,
            "breakfast": false,
            "deposit": true,
            "refundable": false
          },
          "price": 13,
          "tax": 0,
          "total": 40,
          "type": ""
        }
      ],
      "stars": 3,
      "url": "/search/?marker=16886\u0026hotelId=362691"
    }
  ],
  "status": "ok"
}
```

### 200

Success response

Field | Type | Description
------|------|------
fullUrl | string | A hotel link with partner's marker.
guestScore | integer | The travelers' rating
minPriceTotal | integer | Minimum price for a day.
address | string | The hotel's address
amenities | []string | Amenities list.
maxPricePerNight | integer | Maximum price per night.
rooms.agencyId | string | Booking agency identifier.
rooms.desc | string | Room's description.
rooms.type | string | Room type.
rooms.agencyName | string | Booking agency name.
rooms.bookingURL | string | Link to the booking website.
rooms.fullBookingURL |  | Complete link to book with filled all data about users (date of check In and check out, number of adults and childrens, currency and ets).
rooms.internalTypeId | string | Grouping by type of rooms.
rooms.options.freeWifi | boolean | Whether there is free wifi in the room.
rooms.options.hotelWebsite | boolean | The proposal leads to the official hotel website.
rooms.options.refundable | boolean | To specifies if a booking has free cancellation.
rooms.options.smoking | boolean | Can smoke in the room.
rooms.options.available | integer | Available rooms count.
rooms.options.breakfast | boolean | Whether breakfast included in the rate or not.
rooms.options.cardRequired | integer | Without reservation card, if 0 - you can book without card and then pay at partners.
rooms.options.deposit | integer | Payment directly on the site.
rooms.price | integer | The daily room rate.
rooms.tax | integer | Agency tax.
rooms.total | integer | The rate for all time.
url | string | A hotel link without domain.
location.lat | float | A latitude value.
location.lon | float | A longitude value.
maxPrice | integer | The highest price of the hotel rooms.
photoCount | integer | Hotel photos count.
popularity | integer | Popularity of the hotel.
price | integer | Daily room rate.
stars | integer | Stars count of the hotel.
distance | float | Distance from the hotel to the center (km).
id | integer | Hotel identifier.
name | string | Hotel name.

### Errors

Code | Description
-----|------------



