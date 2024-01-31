# Flights search API: Real-time and multi-city search

With the help of API, you can get the results of requests in real time and create a Multi-City search. 

By default, one partner may send no more than 200 queries per hour for one IP, using the airline tickets search API. This restriction may be changed if a situation so requires.

## Аccess to the flights search API

### Requirements for Search API

* Each search query must be initiated by the user and the results must be shown to the user in full. The results for each query must contain a “buy" button next to each flight option.
* The reference to the agency's website must be received only when the user clicks the "Buy" button. Automatic collection of all links from the answer is prohibited. Violation of this rule will disable the API search for the partner.
* It's forbidden to use our search API with the API of other metasearches of flights.
* It's forbidden to use requests with localhost IP addresses (127.0.0.1-127.255.255.255).
* It's forbidden to automatically collect data from search results using the search API.
* Page with found flights should be hidden from search engine bots using the robots.txt file. For example, if flights tickets are displayed on the page www.sitename.com/search, then robots.txt should contain the lines:
  ```
  User-Agent: *
  Disallow: /search/
  ```
* The conversion rate for searches via the Buy link must be 9% or more. The conversion rate from the Buy button to actual purchases must be at least 5%.
* Ajax requests to the API don’t work because the access token is passed unencrypted. You must make requests to the API from the server.

### How to get access

To access the flights search API you should be registered in our [travel affiliate program](https://travelpayouts.com/) and [submit your request](https://support.travelpayouts.com/hc/ru/requests/new) on with the following information:

* URL of your website;
* Design prototypes of a search result;
* Description of your project;
* How you will use the search API?
* Why aren’t the standard methods of integration (search forms, White Label, API access to data) suitable for you.
* Requirements for flights search API access.

## Roundtrip

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/3438c693f7bfb0c14368)

> Body example

```json
{
    "signature": "MD5_signature",
    "marker": "Put_Your_Marker_Here",
    "host": your_server_host,
    "user_ip": user_ip_address,
    "locale": "en",
    "trip_class": "Y",
    "passengers": {
        "adults": 1,
        "children": 0,
        "infants": 0
    },
    "segments": [
    {
        "origin": "MOW",
        "destination": "LON",
        "date": "2018-05-25"
    },
    {
        "origin": "LON",
        "destination": "MOW",
        "date": "2018-06-18"
    }
    ]
} 
```

### Request parameters

Parameter | Type | Description
--------- | ------- | -----------
**marker** | string | the unique identifier of the affiliate. You can find your marker in the affiliate personal account
**host** | string | host's request (must be replaced by the address of your website where the API will be used)
**user_ip** | string | user's IP address
**locale** | string | language of the search result (en-us, en-gb, ru, de, es, fr, pl). Аrom the locale depends on the set of agencies on which the search is performed
**trip_class** | string | flight class (Y – Economy, C – Business)
**passengers** | — | passenger Information
**adults** | integer | the number of adult passengers (from 1 to 9)
**children** | integer | the number of children (from 0 to 6)
**infants** | integer | the number of infants (from 0 to 6)
**segments** | — | a list of the trip components: <li>**origin** (string) — origin IATA or string "City, Country (IATA)". The IATA code is shown in uppercase letters (for example, "Paris, France (PAR)")</li><li>**destination** (string) — destination IATA or string "City, Country (IATA)". The IATA code is shown in uppercase letters (for example, "Berlin, Germany (BER)")</l><li>**date** (date) — departure date yyyy-mm-dd (for example, "2021-09-08")</li>
**know_english** | string | an parameter responsible for the presence of English-speaking gates in the output. Accepted values: true (if it is necessary to display English-language gates to the user) and false (false by default)
**currency** | string | the currency in which the price of the ticket is displayed, after switching to the agency's website (provided that the agency supports this currency)
**signature** | string | the request signature is constructed from token, marker, and all the values of the query parameters sorted alphabetically and separated by a colon. Learn how to create a signature look here

To get "Round trip" tickets, add a JSON to the body of the request:

> Request example

```shell
curl -v -X POST -d '{"signature":"%MD5_signature%","marker":"%Put_Your_Marker_Here%","host":"beta.as.ru","user_ip":"127.0.0.1","locale":"ru","trip_class":"Y","passengers":{"adults":1,"children":0,"infants":0},"segments":[{"origin":"MOW","destination":"LON","date":"2021-05-25"},{"origin":"LON","destination":"MOW","date":"2021-06-18"}]}' -H 'Content-type:application/json' https://api.travelpayouts.com/v1/flight_search
```

### Response

> The answer comes in JSON format. The response contains the parameters:

```json
{
  "chain_name": "jetradar_rt_search_native_format",
  "locale": "en",
  "user_env": {
  },
  "meta": {
    "uuid": "d9266de5-7578-418f-9ddc-6b176ae45923"
  },
  "host": "beta.aviasales.ru",
  "segments": [
    {
      "origin": "CPH",
      "original_origin": "CPH",
      "origin_country": "DK",
      "destination": "ROM",
      "date": "2021-06-24",
      "destination_country": "IT",
      "original_destination": "ROM"
    },
    {
      "origin": "ROM",
      "original_origin": "ROM",
      "origin_country": "IT",
      "destination": "CPH",
      "date": "2021-06-25",
      "destination_country": "DK",
      "original_destination": "CPH"
    }
  ],
  "affiliate_has_sales": true,
  "show_ads": true,
  "destination_country": "IT",
  "passengers": {
    "children": 0,
    "adults": 1,
    "infants": 0
  },
  "currency_rates": {
    "lak": 0.0075,
    "czk": 2.95961
  },
  "travelpayouts_api_request": true,
  "auid": null,
  "server_name": "zoo39.int.avs.io.yasen.bee.13",
  "know_english": "false",
  "currency": "usd",
  "range": "false",
  "geoip_city": "Unknown",
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
  "search_depth": 60,
  "signature": "fb7ded0ddd86270a262d832322f46093",
  "trip_class": "Y",
  "affiliate": true,
  "initiated_at": "2021-04-26 05:09:42.031853",
  "user_id": null,
  "start_search_timestamp": 1524719382.03045,
  "gates_count": 0,
  "market": "dk",
  "user_ip": null,
  "internal": false,
  "_ga": null,
  "clean_marker": "xxxxx",
  "open_jaw": false,
  "origin_country": "DK",
  "marker": "xxxxx",
  "search_id": "d9266de5-7578-418f-9ddc-6b176ae45923",
  "geoip_country": "Unknown"
}
```

Parameter | Description
--------- | -----------
**locale** | the language of the search result
**search_id** | the unique identifier for the search query used to search results
**geoip_city** | the geoip of the city where the request was made
**trip_class** | the class of trip
**affiliate** | the affiliate ID
**marker** | the unique identifier of the affiliate
**user_ip** | the user's IP address
**gates_count** | the total number of agencies
**segments** | a list of the trip components:  <li> **date** — departure date; </li> <li>**origin** — origin IATA;</li> <li>**destination** — destination IATA.</li>
**meta** | technical information
**uuid** | unique identifier of the request
**passengers** | passenger information
**adults** | the number of adult passengers
**children** | the number of children
**infants** | the number of infants
**host** | host's request
**currency_rates** | exchange rate
**geoip_country** | the geoip of the country where the request was made

<aside class="notice">Please note! Use currency rates to convert the prices of flights to the currency you need (because the response contains the flight price in Russian rubles).</aside> 

## One way

### Request initialization

To get "One-way" tickets, add a JSON into the body of the request.

> Body example

```json
{
    "signature": "%MD5_signature%",
    "marker": "%Put_Your_Marker_Here%",
    "host": "beta.as.ru",
    "user_ip": "127.0.0.1",
    "locale": "ru",
    "trip_class": "Y",
    "passengers": {
        "adults": 1,
        "children": 0,
        "infants": 0
    },
    "segments": [
        {
            "origin": "MOW",
            "destination": "LED",
            "date": "2021-06-18"
        }
    ]
}
```

### Request parameters

Parameter | Type | Description
--------- | ------- | -----------
**marker** | string | the unique identifier of the affiliate. You can find your marker in the affiliate personal account
**host** | string | host's request (must be replaced by the address of your website where the API will be used)
**user_ip** | string | user's IP address
**locale** | string | language of the search result (en-us, en-gb, ru, de, es, fr, pl). Аrom the locale depends on the set of agencies on which the search is performed
**trip_class** | string | flight class (Y – Economy, C – Business)
**passengers** | — | passenger Information
**adults** | integer | the number of adult passengers (from 1 to 9)
**children** | integer | the number of children (from 0 to 6)
**infants** | integer | the number of infants (from 0 to 6)
**segments** | — | a list of the trip components: <li>**origin** (string) — origin IATA or string "City, Country (IATA)". The IATA code is shown in uppercase letters (for example, "Paris, France (PAR)");</li><li>**destination** (string) — destination IATA or string "City, Country (IATA)". The IATA code is shown in uppercase letters (for example, "Berlin, Germany (BER)");</l><li>**date** (date) — departure date yyyy-mm-dd (for example, "2021-09-08");</li>
**know_english** | string | an parameter responsible for the presence of English-speaking gates in the output. Accepted values: true (if it is necessary to display English-language gates to the user) and false (false by default)
**currency** | string | the currency in which the price of the ticket is displayed, after switching to the agency's website (provided that the agency supports this currency);
**signature** | string | the request signature is constructed from token, marker, and all the values of the query parameters sorted alphabetically and separated by a colon. Learn how to create a signature look here.

To get data, use the initialization code of the search:

> Request example

```shell
curl -v -X POST -d '{"signature":"%MD5_signature%","marker":"%Put_Your_Marker_Here%","host":"beta.as.ru","user_ip":"127.0.0.1","locale":"ru","trip_class":"Y","passengers":{"adults":1,"children":0,"infants":0},"segments":[{"origin":"MOW","destination":"LED","date":"2021-06-18"}]}' -H 'Content-type:application/json' https://api.travelpayouts.com/v1/flight_search
```

## Open jaw

### Request initialization

Open jaw is a round-trip ticket in which the traveller does not arrive in the same city of departure and/or does not depart from the same city where he/she first landed. For example, London — Paris — Berlin — London.

To get "Open jaw" tickets, add a JSON into the body of the request:

> Body example

```json
{
    "signature": "%MD5_signature%",
    "marker": "%Put_Your_Marker_Here%",
    "host": "beta.as.ru",
    "user_ip": "127.0.0.1",
    "locale": "ru",
    "trip_class": "Y",
    "passengers": {
        "adults": 1,
        "children": 0,
        "infants": 0
    },
    "segments": [
        {
            "origin": "MOW",
            "destination": "LED",
            "date": "2021-02-18"
        },
        {
            "origin": "LED",
            "destination": "BER",
            "date": "2021-02-25"
        },
        {
            "origin": "BER",
            "destination": "LON",
            "date": "2021-03-05"
        }
    ]
}
```

### Request parameters

Parameter | Type | Description
--------- | ------- | -----------
**marker** | string | the unique identifier of the affiliate. You can find your marker in the affiliate personal account
**host** | string | host's request (must be replaced by the address of your website where the API will be used)
**user_ip** | string | user's IP address
**locale** | string | language of the search result (en-us, en-gb, ru, de, es, fr, pl). Аrom the locale depends on the set of agencies on which the search is performed
**trip_class** | string | flight class (Y – Economy, C – Business)
**passengers** | — | passenger Information
**adults** | integer | the number of adult passengers (from 1 to 9)
**children** | integer | the number of children (from 0 to 6)
**infants** | integer | the number of infants (from 0 to 6)
**segments** | — | a list of the trip components: <li>**origin** (string) — origin IATA or string "City, Country (IATA)". The IATA code is shown in uppercase letters (for example, "Paris, France (PAR)");</li><li>**destination** (string) — destination IATA or string "City, Country (IATA)". The IATA code is shown in uppercase letters (for example, "Berlin, Germany (BER)");</l><li>**date** (date) — departure date yyyy-mm-dd (for example, "2021-09-08");</li>
**know_english** | string | an parameter responsible for the presence of English-speaking gates in the output. Accepted values: true (if it is necessary to display English-language gates to the user) and false (false by default)
**currency** | string | the currency in which the price of the ticket is displayed, after switching to the agency's website (provided that the agency supports this currency);
**signature** | string | the request signature is constructed from token, marker, and all the values of the query parameters sorted alphabetically and separated by a colon. Learn how to create a signature look here.

To get data, use the initialization code of the search:

> Request example

```shell
curl -v -X POST -d '{"signature":"%MD5_signature%","marker":"%Put_Your_Marker_Here%","host":"beta.as.ru","user_ip":"127.0.0.1","locale":"ru","trip_class":"Y","passengers":{"adults":1,"children":0,"infants":0},"segments":[{"origin":"MOW","destination":"LED","date":"2017-06-18"},{"origin":"LED","destination":"BER","date":"2021-06-25"},{"origin":"BER","destination":"LON","date":"2021-07-05"}]}' -H 'Content-type:application/json' https://api.travelpayouts.com/v1/flight_search
```

## Getting search results

In the body of the response is the parameter **search_id**; insert it into the URL:

https://api.travelpayouts.com/v1/flight_search_results?uuid=%search_id%

Then send the request to the server for search results:

`GET https://api.travelpayouts.com/v1/flight_search_results?uuid=%search_id%`

> Request example

```shell
curl -v -H 'Accept-Encoding:gzip,deflate,sdch' https://api.travelpayouts.com/v1/flight_search_results?uuid=%search_id% 
--compressed
```

<aside class="notice">As a result of the search, you will get the JSON array where each element is a response from a definite agency. </aside>

<aside class="warning">Repeat the request until you get an associative array with one element search_id. The periodicity of sending requests isn't restricted. </aside>

### Request example

<aside class="warning">Attention! The link to the search results is relevant for 15 minutes. After this time, you must send a search query again.</aside>

> Response example

```json
[{
    "segments":[
    {
        "destination_country":"RU",
        "original_destination":"LED",
        "origin":"MOW",
        "origin_country":"RU",
        "original_origin":"MOW",
        "date":"2021-05-25",
        "destination":"LED"
    },
    {
        "destination_country":"RU",
        "original_destination":"MOW",
        "origin":"LED",
        "origin_country":"RU",
        "original_origin":"LED",
        "date":"2021-06-18",
        "destination":"MOW"
    }],
    "banner_info":{
    },
        "internal":false,
        "airports":{
            "LED":{
                "name":"Пулково",
                "time_zone":"Europe/Moscow",
                "country":"Россия",
                "rates":"259",
                "city":"Санкт-Петербург"
            },
            "DME":{
                "name":"Домодедово",
                "time_zone":"Europe/Moscow",
                "country":"Россия",
                "rates":"392",
                "city":"Москва"
            },
            "SVO":{
                "rates":"307",
                "country":"Россия",
                "name":"Шереметьево",
                "average_rate":"3.63",
                "city":"Москва",
                "time_zone":"Europe/Moscow"
            },
            "VKO":{
                "name":"Внуково",
                "time_zone":"Europe/Moscow",
                "country":"Россия",
                "rates":"211",
                "city":"Москва"
            }},
            "gates_info":{
                "20":{
                    "average_rate":4.43,
                    "rates":2967,
                    "currency_code":"rub",
                    "is_airline":false,
                    "productivity":16.9991,
                    "label":"OneTwoTrip",
                    "airline_iatas":{
                    },
                    "payment_methods":[
                        "card"
                    ],
                    "mobile_version":false
                    }},
                    "city_distance":634,
                    "meta":{
                        "uuid":"c9c6de8c-3fb4-404e-b88c-e9e0a605f183",
                        "gates":[
                        {
                            "duration":22.402996063232422,
                            "id":20,
                            "count":1456,
                            "good_count":1456
                        }]},
                    "airlines":{
                        "SU":{
                            "average_rate":"4.01",
                            "rates":"2362",
                            "alliance_name":"SkyTeam",
                            "name":"Аэрофлот",
                            "id":10
                        },
                        "UN":{
                            "average_rate":"3.98",
                            "rates":"2639",
                            "alliance_name":null,
                            "name":"Трансаэро",
                            "id":492
                        },
                        "S7":{
                            "average_rate":"3.95",
                            "rates":"2430",
                            "alliance_name":"OneWorld",
                            "name":"S7",
                            "id":444
                        },
                        "UT":{
                            "rates":"1843",
                            "alliance_name":null,
                            "name":"ЮТэйр",
                            "id":507
                        },
                        "U6":{
                            "average_rate":"3.62",
                            "rates":"1158",
                            "alliance_name":null,
                            "name":"Уральские авиалинии",
                            "id":503
                        }},
                    "filters_boundary":{
                        "arrival_datetime_0":{
                            "min":1418869200,
                            "max":1418950500
                        },
                        "arrival_datetime_1":{
                            "min":1419486600,
                            "max":1419554400
                        },
                        "flights_duration":{
                            "min":70,
                            "max":120
                        },
                        "stops_count":{
                            "0":4431
                        },
                        "departure_time_1":{
                            "min":"04:30",
                            "max":"22:55"
                        },
                        "departure_time_0":{
                            "min":"00:50",
                            "max":"23:30"
                        },
                        "departure_minutes_0":{
                            "min":50,
                            "max":1410
                        },
                        "departure_minutes_1":{
                            "min":270,
                            "max":1375
                        },
                        "price":{
                            "min":4431,
                            "max":8689
                        }},
                    "flight_numbers":[
                    [
                        "SU30",
                        "SU32"
                    ],
                    [
                        "SU31",
                        "SU33"
                    ]],
                    "affiliate_has_sales":false,
                    "proposals":[
                        {
                            "terms":{
                                "20":{
                                  "currency":"rub",
                                  "price":18418,
                                  "unified_price":18418,
                                  "url":18000000,
                                  "multiplier":1e-06,
                                  "proposal_multiplier":1,
                                  "flights_baggage":[
                                     [
                                        false
                                     ],
                                     [
                                        false
                                     ]
                                  ],
                                  "flights_handbags":[
                                     [
                                        "1PC10"
                                     ],
                                     [
                                        "1PC10"
                                     ]
                                  ],
                                  "baggage_source":[
                                     [
                                        3
                                     ],
                                     [
                                        3
                                     ]
                                  ],
                                  "handbags_source":[
                                     [
                                        3
                                     ],
                                     [
                                        3
                                     ]
                                  ]
                            }},
                            "xterms":{
                               "180":{
                                  "Y_0PC;Y_0PC":{
                                     "currency":"rub",
                                     "price":18418,
                                     "unified_price":18418,
                                     "url":18000000,
                                     "multiplier":1e-06,
                                     "proposal_multiplier":1,
                                     "flights_baggage":[
                                        [
                                           false
                                        ],
                                        [
                                           false
                                        ]
                                     ],
                                     "flights_handbags":[
                                        [
                                           "1PC10"
                                        ],
                                        [
                                           "1PC10"
                                        ]
                                     ],
                                     "baggage_source":[
                                        [
                                           3
                                        ],
                                        [
                                           3
                                        ]
                                     ],
                                     "handbags_source":[
                                        [
                                           3
                                        ],
                                        [
                                           3
                                        ]
                                     ]
                                  }
                               }
                            },
                            "sign":"7573ea707c2ff84b243241961412ed34",
                            "segment":[
                            {
                                "flight":[
                                {
                                    "arrival":"LED",
                                    "aircraft":"AIRBUS A320",
                                    "local_departure_timestamp":1434588600,
                                    "operating_carrier":"UT",
                                    "duration":85,
                                    "local_arrival_timestamp":1432549200,
                                    "departure_date":"2021-05-25",
                                    "departure_time":"11:00",
                                    "arrival_date":"2021-05-25",
                                    "arrival_time":"12:25",
                                    "delay":0,
                                    "departure":"VKO",
                                    "number":369
                            }]},
                            {
                            "flight":[
                              {
                                "arrival":"DME",
                                "aircraft":"AIRBUS A320",
                                "local_departure_timestamp":1434588600,
                                "operating_carrier":"SU",
                                "duration":90,
                                "local_arrival_timestamp":1432549200,
                                "departure_date":"2021-06-18",
                                "departure_time":"10:05",
                                "arrival_date":"2021-06-18",
                                "arrival_time":"11:35",
                                "delay":0,
                                "departure":"LED",
                                "number":6131
                        }]}]},
                   ]}],
            "validating_carrier": "SU"
        }],
    "_ga":null,
    "signature":"4bb635b9353a1e933907d41841e23414",
    "search_id":"c9c6de8c-3fb4-404e-b88c-e9e0a605f183"
    },
    {
    "search_id":"c9c6de8c-3fb4-404e-b88c-e9e0a605f183"
}]
```

The response includes the data:

Parameter | Description
--------- | -----------
search_id | unique identifier for the search query
flight_numbers | umbers of the flight
meta | <li>**gates** — information about phases of gates in the search process; </li> <li>**good_count** — number of relevant tickets (if the agency has returned the ticket for the wrong dates or they are misspelled, they are filtered out by the system); </li><li>**count** — number of tickets uploaded from the agency; </li> <li>**duration** — processing time of request; </li><li> **id** — ID agency;</li> <li>**error** — error information; </li> <li>**tos** -content of error.</li>
uuid | request ID;
city_distance | distance between the cities of origin and destination;
gates_info | information about the agent (Ticket Seller): <li>**currency_code** — payment currency code;</li><li> **is_airline** — is an airline;</li><li> **average_rate** — average rating of agencies;</li><li> **rates** — rating agency (count voters);</li><li> **mobile_version** — having a mobile version of the site;</li> <li>**productivity** — productivity;</li><li> **airline_iatas** — IATA airline code, if the gate sells tickets;</li><li> **payment_methods** — payment methods;</li> <li>**label** — agency name.</li>
signature | signature of request
segments | array data of flights: <li>**destination_country** — code of the country of destination;</li> <li> **original_destination** — code of the city of destination;</li><li> **origin** — origin IATA;</li><li> **destination** — destination IATA;</li><li> **origin_country** — the origin country;</li><li> **date** — departure date.</li>
flight_numbers | flight numbers
airlines | information about the airlines: <li>**deeplink_site_name** — address of the airline's website;</li><li> **id** — identification number of the airline;</li> <li> **site_name** — name of the airline's website;</li><li> **alliance_name** — alliance of the airline; </li><li>**average_rate** — average rating;</li><li> **rates** — number of ratings;</li><li> **deeplink_id** — ID links to airline's website; </li><li>**name** — name of airline.</li>
proposals | an array of variants
sign | unique id of the ticket, to integrate information from different agencies in one ticket;
flight | flight details: <li>**departure** — departure IATA code;</li><li> **duration** — flight duration in minutes;</li><li> **departure_date** — departure date (UNIX-time);</li><li> **departure_time** — departure time (UNIX-time);</li><li> **local_departure_timestamp** — local departure time in UNIX format;</li><li> **arrival_time** — arrival time (UNIX-time);</li><li> **local_arrival_timestamp** — local arrival time in UNIX format;</li><li> **number** — flight number. To generate a full flight number, use the number and **operating_carrier parameters**;</li><li> **delay** — duration of stop between flights (in minutes);</li><li> **operating_carrier** — IATA code of airline that performs the carriage;</li><li> **marketing_carrier** — IATA code of the airline that sells the ticket. Use it to generate a flight number. If this field is empty, use operating_carrier</li><li> **arrival_date** — arrival date;</li><li> **aircraft** — type of aircraft;</li><li> **rating_summary** — some rating information about agency or airline (can be blank);</li><li> **is_bus, is_train** — true, if in this segment they do not travel by plane, but by bus or train;</li><li> **technical_stops** — information about technical stops ;</li><li> **arrival** — IATA code of arrival.</li>
rating | internal information about flight rating
terms | information about the flight’s cost: <li>**price** — trip price in original currency (type listed in the field currency);</li><li> **currency** — currency type;</li><li> **flights_baggage** — the number of pieces of baggage and its weight. _"" — there is no information about baggage; false — baggage is not included in a price; {int}PC{int} — number of bags by %somevalue% kilogram. For example, 2PC23 — means two baggage pieces of 23 kg. {int} — number of bags does not matter, the total weight is limited._ </li> <li>**unified_price** — price of flight in basic currency (Russian ruble);</li> <li>**url** — code to generate links for buyers (as forming the link; see below).</li>
stops_airports | IATA codes of departure airports, destination and transfers;
airports | information about airports;
xterms | contains information similar to terms, plus may contain additional data on tariffs (if it is transmitted from agencies / airlines)
is_direct | true if the flight is non-stop
segments_airports | IATA codes of the main departure and destination airports
is_charter | flight is charter or not (false or true)
segment_durations | total flights duration (for example, there and back)
total_duration | total flight time with stops time
max_stops | maximum number of stops
segments_rating, flight_weight, popularity, tags | system parameters
market | market of routes (**deprecated**);
initiated_at | date and time of search (**deprecated**);
open_jaw | true if it is part of open jaw (**deprecated**);
clean_marker | affiliate marker (**deprecated**);
currency | currency type (**deprecated**);
filters_boundary | array data for filtering: <li>**stops_duration** — time between flights (maximum and minimum);</li><li> **flights_duration** — flights duration (maximum and minimum);</li><li> **arrival_datetime_0** — arrival datetime (maximum and minimum);</li><li> **price** — price of flights (maximum and minimum);</li><li> **departure_time_0** — departure time (maximum and minimum);</li><li> **stops_count** — stops count.</li>

<aside class="warning">Attention! Use currency rates to convert the prices of flights to the currency you need (because the response contains the flight price in Russian rubles).</aside>

## Additional Information in the response

Some airline companies and agencies provide additional information about flights, aircraft, and onboard services. These fields and their content are described below. You may use this information on your websites or ignore it — the main information about the tickets is given above.

Parameter | Description
--------- | -----------
banner_info | service information provided by an airline company
airlines/AF/ | information from a specific airline company (where AF is the IATA designator code): <li>**jets** — information about the airline company’s aircraft: <ul><li>**seatType** — seat type in an aircraft (Angle Lie Flat, Flat Bed — special seat, can be transformed into a bed, etc.; Standard — standard seat);</li> <li>**typeClass** — class type (Business class, Economy class);</li> <li>**seatWidth** — seat width (inches);</li><li> **aircraft** — aircraft type; **seatPitch** — distance between the seats (inches);</li><li> **videoType** — video type (Overhead TV — on a seat, located in front, On-Demand TV — common TV, headphones are given on demand, None — unavailable);</li><li> **wifi** — Wi-Fi on-board; </li><li>**id** — unique aircraft ID (service parameter); </li><li>**powerType** — availability of an AV receptacle in a seat;</li><li> **airline** — IATA designator code;</li><li> **laptopPower** — availability of a notebook receptacle. </li></li></ul><li>**ageOfPlanes** — average age of an airline company’s aircraft;</li><li> **alliance** — alliance joined by an airline company;</li><li> **economyLegroom** — average distance between the seats in economy class (inches);</li><li> **freeStandardCarryOn** — availability of free space for hand luggage;</li><li> **infantsLapCost** — age from which a child is not considered an infant;</li><li> **minorsNotTravelAloneFrom** — opportunity for minors to travel alone;</li><li> **iata** — IATA designator code;</li><li> **checkedBaggagePrice1st** — luggage registration cost;</li><li> **baggage** — information about the luggage on a flight;</li><li> **excess** — text information about restrictions for luggage transportation;</li><li> **checked** — text information about the prepaid luggage weight and size, and the necessity to make an additional payment if the size exceeds the standard; </li><li>**carryOn** — text information about hand-luggage transportation rules;</li><li> **airline** — IATA designator code; </li><li>**sportMusical** — rules for transporting large musical instruments and sport equipment.</li>
frequentFlyerPrograms | loyalty program for clients
aircrafts | the number of aircraft owned by an airline company
carryOnStandard | presence of a hand-luggage transportation standard
lowcost | is/not a low-cost airline company
freeCheckedBag | opportunity for luggage transportation for free within the extent permissible
meals | airline company’s on-board types of menus
checkin | ways to register provided by an airline company: <li>**mobileCheckIn** — opportunity of registration using a mobile app;</li><li> **seatOnlineCheckIn** — seat selection at registration;</li><li> **onlineCheckInwithBag** — online luggage registration; </li> <li>**airline** — IATA designator code;</li><li> **onlineCheckIn** — rules for online registration;</li><li> **requirementOnlineCheckIn** — rules for online registration; </li><li>**airportCheckIn** — rules for registration in an airport;</li><li> **timeBoardingGate** — time for boarding before departure; </li><li>**minorsNotTravelAloneTo** — age from which minors may travel without grown-ups;</li><li> **pet** — information about transportation of animals by an airline company:</li><ul><li> **cargo** — transportation in luggage;</li> <li>**baggage** — rules for transportation in luggage;</li><li> **restriction** — restrictions;</li><li> **documentation** — required documents;</li><li> **book** — booking;</li><li> **airline** — IATA designator code;</li><li> **method** — type of transportation; </li><li> **cabin** — information about transportation in a cabin;</li><li> **kennel** — additional requirements; </li><li>**fee** — information about the fee for transportation of animals; </li></ul><li>**minor**— information about the fee for minors:</li><ul><li> **age** — age from which this tariff may be applied;</li><li> **airline** — IATA designator code;</li><li> **booking** — information about the booking;</li><li> **aboutService** — information about the servicing;</li><li> **flightRestriction** — information about restrictions;</li><li> **fee** — tariff fee.</li></ul><li>infant — information about the tariff for infants:</li> <ul><li>**payInternational** — information about the tariff; **exitRow** — restrictions for selection of a seat near the emergency door;</li><li> **childTurnTwo** — tariff rules for transfer flights; </li><li>**reserveSeat** — information about seats for infants; </li><li>**payInfant** — payment information;</li><li> **airline** — IATA designator code; </li><li>**baggage** — luggage in a ticket for an infant;</li><li> **childRestraintDevices** — information about transportation of luggage required for an infant (baby carriage, carrying bag, etc.);</li><li> **infantAmenitites** — information about additional services rendered on-board for an infant; </li><li>**payDomestic** — additional fee.</li></ul>

## How to get a link to the agency website

<aside class="warning">Attention! The reference to the agency's website must be received only when the user clicks the "Buy" button. Automatic collection of all links from the answer is prohibited. Violation of this rule will disable the API search for the partner. </aside>

> Request example

```shell
curl -v -H 'Accept-Encoding:gzip,deflate,sdch' https://api.travelpayouts.com/v1/flight_searches/%search_id%/clicks/%terms.url%.json 
--compressed
```

To get a link to the site of the ticket booking agencies send a request to the following address:

`GET https://api.travelpayouts.com/v1/flight_searches/%search_id%/clicks/%terms.url%.json`

where **search_id** is the ID from the answer of the request, **terms.url** — URL parameter from the response.

You will receive a response like in the example.

> Response example

```json
{
    "params": {},
    "method": "GET",
    "url": "https://www.svyaznoy.travel/?utm_source=as.ru&utm_medium=cpa&utm_campaign=meta_avia#MOW0906/BKK1506/A1/C0/I0/S0/22316/EK-132;EK-374/EK-373;EK-131&marker=7uh46i0v2",
    "gate_id": 62,
    "click_id": 22135952358110
}
```

To move on to the booking, give your visitors a link from the parameter `"url"`.

The “lifetime” of such links is 15 minutes, after which you will need to search again for the current prices and generate a new reference to the transition.

In our example, this is a link of the form:

`https://www.svyaznoy.travel/?utm_source=as.ru&utm_medium=cpa&utm_campaign=meta_avia#MOW0906/BKK1506/A1/C0/I0/S0/22316/EK-132;EK-374/EK-373;EK-131&marker=7uh46i0v2`
