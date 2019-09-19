# Hotel search API

## Requirements for Hotels API access

1. Each search query must be initiated by the user and the results must be shown to the user in full. The results for each query must contain a “buy” button next to each flight option.
2. The conversion rate for searches via the Buy link must be 9% or more. The conversion rate from the Buy button to actual purchases must be at least 5%.
3. We'll also need to see the URL of your project, your design prototypes, a description of your project and how our API will be used. 

## Hotels search API description

With hotels API, a partner can create his or her own search of hotels. Access to the hotel search API is free, limited, and available on an individual basis on request from the partner.

**To access the search API hotels**, submit your request to support@travelpayouts.com with the following information:

* URL of your website.
* Design prototypes of search result and hotel's page.
* How you will use the search API?
* Why aren’t the standard methods of integration (search forms, White Label, API access to data) suitable for you?

**Attention, please**! Data about Booking.com is missing in the API of hotels. The reason for this is the policy of the company to work through the API and White Label.

## Search management

Search by hotel IATA-code or cityId (ID location), or hotelId (ID hotel). All options or just one can be specified. If you specify hotelId and cityId, only hotelId will be used. If you specify iata and cityId, iata will be used.

When using this search, it is possible to access its results not immediately, but after a period of time not exceeding 15 minutes. Handling is on the request ID searchId.

**Attention**! The default number of requests is limited to **200 requests per hour** for one IP address. If you need to process more requests, send a note to support@travelpayouts.com.

> Sample request

```shell
curl --request GET \
  --url 'http://engine.hotellook.com/api/v2/search/start.json?iata=HKT&checkIn=2018-08-10&checkOut=2018-08-13&adultsCount=2&customerIP=100.168.1.1&childrenCount=1&childAge1=8&lang=ru&currency=USD&waitForResult=0&marker=УкажитеВашМаркер&signature=a475100374414df97a9c6c7d7731b3c6' \
```

```ruby
require 'uri'
require 'net/https'

url = URI("http://engine.hotellook.com/api/v2/search/start.json?iata=HKT&checkIn=2018-08-10&checkOut=2018-08-13&adultsCount=2&customerIP=100.168.1.1&childrenCount=1&childAge1=8&lang=ru&currency=USD&waitForResult=0&marker=УкажитеВашМаркер&signature=a475100374414df97a9c6c7d7731b3c6")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "http://engine.hotellook.com/api/v2/search/start.json?iata=HKT&checkIn=2018-08-10&checkOut=2018-08-13&adultsCount=2&customerIP=100.168.1.1&childrenCount=1&childAge1=8&lang=ru&currency=USD&waitForResult=0&marker=УкажитеВашМаркер&signature=a475100374414df97a9c6c7d7731b3c6",
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
```

```python
import requests

url = "http://engine.hotellook.com/api/v2/search/start.json"

querystring = {"iata":"HKT", "checkIn":"2018-08-10", "checkOut":"2018-08-13", "adultsCount":"2", "customerIP":"100.168.1.1", "childrenCount":"1", "childAge1":"8", "lang":"ru", "currency":"USD", "waitForResult":"0", "marker":"УкажитеВашМаркер", "signature":"a475100374414df97a9c6c7d7731b3c6"}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

where **signature** is md5 of the string: "*YourToken:YourMarker:adultsCount:checkIn:checkOut:childAge1:childrenCount:currency:customerIP:iata:lang:waitForResult*". 

More information about the signature is available [here](https://support.travelpayouts.com/hc/en-us/articles/210995998).

### First request

`GET http://engine.hotellook.com/api/v2/search/start.json?iata=HKT&checkIn=2018-08-10&checkOut=2018-08-13&adultsCount=2&customerIP=100.168.1.1&childrenCount=1&childAge1=8&lang=ru&currency=USD&waitForResult=0&marker=УкажитеВашМаркер&signature=a475100374414df97a9c6c7d7731b3c6`

### Request parameters

Required parameters are highlighted in **bold**.

* **cityId** – the location ID (the query static/locations.json)
* **hotelId** – the hotel ID (the query static/hotels.json)
* **iata** – iata code of city
    
    **Note**. The request must have at least one of the required parameters iata, cityId or hotelId.

* **checkIn** – check-in date format: yyyy–MM–dd
* **checkOut** – check-out date format: yyyy–MM–dd
* **adultsCount** – number of adults
* customerIP – IP of the user who initiated the request
* childrenCount – the number of children; possible values - from 0 to 3. Default - 0
* childAge1, childAge2, childAge3 – ages of children (if childrenCount greater than 0). The default age is 1 year (max = 17)
* lang – the language of the search result. Stated together with the region
    * en_US
    * en_GB
    * ru_RU
    * de_DE
    * en_AU
    * en_CA
    * en_IE
    * es_ES
    * fr_FR
    * it_IT
    * pl_PL
    * th_TH
* currency – USD, RUB, EUR, ...
* waitForResult – wait for the completion of all searches for partners, possible values 0 or 1
    * 1 – the connection is open before all the data from the partners. The result is returned to the user query and its searchId
    * 0 – the connection will be terminated immediately and returned to the user searchId (default)

### Response

> Sample response

```json
{
    "searchId": "5201179",
    "status": "ok"
}
```

### Second request

> Sample request

```shell
http://engine.hotellook.com/api/v2/search/getResult.json?searchId=4034914&limit=10&sortBy=price&sortAsc=1&roomsCount=0&offset=0&marker=PasteYourMarkerHere&signature=364c38baee5cf11b382297bfd4338ce6
```

where **signature** is md5 of the string: *"YourToken:YourMarker:limit:offset:roomsCount:searchId:sortAsc:sortBy"*. 

### Request parameters

* **searchId** – search Id
* limit – maximum number of hotels, from 0 to infinity, where 0 - no limit. Default - 0
* offset – to skip a number of hotels from 0 to infinity, where 0 - no hotel not passed. Default - 0
* sortBy – how to sort:
    * popularity - by popularity
    * price - by price
    * name - by name
    * guestScore – by User Rating
    * stars – by number of stars
    *Default – popularity*
* sortAsc – how to sort the values:
    * 1 – ascending
    * 0 – descending
    *Default – 1.*
* roomsCount – the maximum number of rooms that are returned in each hotel, from 0 to infinity, where 0 - no limit. Default – 0

### Response

> Sample response

When you are trying to get a search result, at the end of search you get the error "errorCode: 4". This means the results are not yet ready. The search is not interrupted; you should repeat the request later.

```json
{
    "status": "ok",
    "result": [
        {
            "fullUrl": "http://search.hotellook.com/?language=ru&marker=16886&hotelId=362691",
            "maxPricePerNight": 46,
            "maxPrice": 138,
            "photoCount": 50,
            "guestScore": 63,
            "address": "23/8 Soi Hub-Aik, Phuket Road, Muang District",
            "minPriceTotal": 40,
            "id": 362691,
            "price": 13,
            "name": "Rome Place Hotel",
            "url": "/search/?marker=16886&hotelId=362691",
            "popularity": 47,
            "location": {
                "lon": 98.39146,
                "lat": 7.878922
            },
            "stars": 3,
            "distance": 10.6,
            "amenities": [],
            "rooms": [
                {
                    "bookingURL": "/r/?language=ru&checkIn=2015-06-10¤cy=USD&children=5&host=v2%3A16886&marker=16886&transparent=1&roomId=0&adults=2&locationId=30553&checkOut=2015-06-13&gateId=43&hotelId=362691",
                    "options": {
                        "available": 5,
                        "deposit": true,
                        "refundable": false,
                        "breakfast": false
                    },
                    "type": "",
                    "tax": 0,
                    "desc": "Double or Twin STANDARD",
                    "fullBookingURL": "http://search.hotellook.com/r?language=ru&checkIn=2015-06-10&cy=USD&children=5&host=v2%3A16886&marker=16886&transparent=1&roomId=0&adults=2&locationId=30553&checkOut=2015-06-13&gateId=43&hotelId=362691",
                    "agencyName": "Travel.ru",
                    "agencyId": "43",
                    "total": 40,
                    "price": 13,
                    "internalTypeId": "1"
                }
            ],
            "rating": 63
        }
    ]
}
```

Block "**result**" contains:

* **fullUrl** - the link to the hotel's page with partner's marker
* **maxPrice** – the highest price of the hotel rooms
* **maxPricePerNight** - the maximum price per night
* **price** – the average price per room
* **minPriceTotal** - the minimum cost per stay
* **photoCount** - the number of photos of the hotel
* **guestScore** - the travelers' rating
* **id** – the ID of hotel in the database
* **name** – hotel's name
* **address** – the hotel's address
* **distance** - the distance from the hotel to the city center
* **amenities** - amenities at the hotel (descriptions of values you can find here)
* **location** – the hotel's location:
    * **lat** – latitude of hotel
    * **lon** – longitude of hotel
* **stars** – the number of stars the hotel
* **url** – the link to the hotel website

Block "**rooms**" contains:

* **type, desc** – the type of rooms
* **total** – the rate for all time
* **price** – the daily room rate
* **tax** – taxes and fees
* **options** – additional services:
    * **breakfast** - whether breakfast included in the rate or not
    * **available** - the number of available rooms of this type
    * **deposit** - payment directly on the site, if it is 0 - then pay at the hotel
    * **refundable** - "free cancellation"
    * **cardRequired** - without reservation card, if 0 - you can book without card and then pay at partners
    * **smoking** - can smoke in the room
    * **freeWifi** - whether there is free wifi in the room
    * **hotelWebsite** - proposal leads to the official hotel website
* **bookingURL** – the link to the booking website
* **fullBookingURL** - complete link to book with filled all data about users (date of check In and check out, number of adults and childrens, currency and ets)
* **internalTypeId** - grouping by type of rooms
* **agencyId** – the id of booking agencies
* **agencyName** – the name of the booking agencies
* **rating** - the ranking of visitors. The parameters are calculated based on guest rating, which is compiled on the basis of a vote

You can get photos and other information about hotel with help of [Hotel Data API](https://support.travelpayouts.com/hc/en-us/articles/115000343268-Hotels-data-API).

**Attention**! The reference to the agency's website must be received only when the user clicks the "Buy" button. Automatic collection of all links from the answer is prohibited. Violation of this rule will disable the API search for the partner.
