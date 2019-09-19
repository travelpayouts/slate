# Hotels statistical data

Requests as a result of which the partner receives information about the countries, cities and hotels.

**Attention**! The default number of requests is limited to **60 per minute**. If you need to process more requests, send a letter to support@travelpayouts.com.

## Request "Country"

The request returns a file with a list of countries from the database.

> Sample request

```shell
curl --request GET \
  --url 'http://engine.hotellook.com/api/v2/static/countries.json?token=PasteYourTokenHere' \
```

```ruby
require 'uri'
require 'net/https'

url = URI("http://engine.hotellook.com/api/v2/static/countries.json?token=PasteYourTokenHere")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "http://engine.hotellook.com/api/v2/static/countries.json?token=PasteYourTokenHere",
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

url = "http://engine.hotellook.com/api/v2/static/countries.json"

querystring = {"token":"PasteYourTokenHere"}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

`GET http://engine.hotellook.com/api/v2/static/countries.json?token=PasteYourTokenHere`

### Request parameters

* **token** - your affiliate token

### Response

> Sample response

```json
[
    {
        "id": "9",
        "code": "DZ",
        "name": {
            "EN": [
                {
                    "isVariation": "0",
                    "name": "Algeria"
                }
            ],
            "RU": [
                {
                    "isVariation": "0",
                    "name": "Алжир"
                }
            ]
        }
    },
    {
        "id": "10",
        "code": "AO",
        "name": {
            "EN": [
                {
                    "isVariation": "0",
                    "name": "Angola"
                }
            ],
            "RU": [
                {
                    "isVariation": "0",
                    "name": "Ангола"
                }
            ]
        }
    }
]
```

The response contains: 

* **Id** – id of country
* **code** – code of country
* The block EN:
    * **isVariation** – primary or secondary title. 1 - secondary, 0 - primary
    * **name** – country name in English
* The block RU:
    * **isVariation** – primary or secondary title
    * **name** – country name in Russian

## Request "Cities"

The request returns a file with a list of cities from the database.

> Sample request

```shell
curl --request GET \
  --url 'http://engine.hotellook.com/api/v2/static/locations.json?token=PasteYourTokenHere' \
```

```ruby
require 'uri'
require 'net/https'

url = URI("http://engine.hotellook.com/api/v2/static/locations.json?token=PasteYourTokenHere")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "http://engine.hotellook.com/api/v2/static/locations.json?token=PasteYourTokenHere",
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

url = "http://engine.hotellook.com/api/v2/static/locations.json"

querystring = {"token":"PasteYourTokenHere"}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

`GET http://engine.hotellook.com/api/v2/static/locations.json?token=PasteYourTokenHere`

### Request parameters

* token - your affiliate token

### Response

> Sample response

```json
[
    {
        "id": "373",
        "code": "",
        "countryId": "77",
        "latitude": "15.501950000",
        "longitude": "73.910090000",
        "name": {
            "EN": [
                {
                    "isVariation": "0",
                    "name": "Goa"
                }
            ],
            "RU": [
                {
                    "isVariation": "0",
                    "name": "Гоа"
                }
            ]
        }
    }
]
```

* **Id** – id of city
* **code** – iata-code of city
* **countryId** – id of country
* **latitude** – latitude of city
* **longitude** – longitude of city
* The block DE:
    * **isVariation** - primary or secondary title. 1 - secondary, 0 - primary
    * **name** – city name in German
* The block EN:
    * **isVariation** - primary or secondary title
    * **name** – city name in English
* The block RU:
    * **isVariation** – primary or secondary title
    * **name** – city name in Russian

## Request "Amenities"

The request returns a file with a list of amenities from the database.

> Sample request

```shell
curl --request GET \
  --url 'http://engine.hotellook.com/api/v2/static/amenities/en.json?token=PasteYourTokenHere' \
```

```ruby
require 'uri'
require 'net/https'

url = URI("http://engine.hotellook.com/api/v2/static/amenities/en.json?token=PasteYourTokenHere")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "http://engine.hotellook.com/api/v2/static/amenities/en.json?token=PasteYourTokenHere",
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

url = "http://engine.hotellook.com/api/v2/static/amenities/en.json"

querystring = {"token":"PasteYourTokenHere"}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

` GET http://engine.hotellook.com/api/v2/static/amenities/en.json?token=PasteYourTokenHere`

### Request parameters

* **en.json** - language that you want to see result (en, ru, fr, de and etc)
* **token** - your affiliate token

### Response

> Sample response

```json
[
    {
        "id": "2",
        "name": "Hairdryer",
        "groupName": "Room"
    },
    {
        "id": "3",
        "name": "Safe",
        "groupName": "Room"
    },
    {
        "id": "4",
        "name": "TV",
        "groupName": "Room"
    }
]
```

* **Id** – id of amenities in the database
* **name** – name of amenities
* **groupName** - location of amenities

## Request 'Hotels list'

The request returns a file with a list of hotels from the database.

> Sample request

```shell
curl --request GET \
  --url 'http://engine.hotellook.com/api/v2/static/hotels.json?locationId=895&token=PasteYourTokenHere' \
```

```ruby
require 'uri'
require 'net/https'

url = URI("http://engine.hotellook.com/api/v2/static/hotels.json?locationId=895&token=PasteYourTokenHere")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "http://engine.hotellook.com/api/v2/static/hotels.json?locationId=895&token=PasteYourTokenHere",
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

url = "http://engine.hotellook.com/api/v2/static/hotels.json"

querystring = {"locationId":"895", "token":"PasteYourTokenHere"}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

` GET http://engine.hotellook.com/api/v2/static/hotels.json?locationId=895&token=PasteYourTokenHere`

### Request parameters

* **locationId** – id of location
* **token** – your affiliate token

### Response

> Sample response

```json
{
    "gen_timestamp": 1510729858.8067338,
    "pois": [
        {
            "id": 70643,
            "rating": 0,
            "category": "airport",
            "name": "Koggala Airport",
            "location": {
                "lat": 5.983056,
                "lon": 80.33305
            },
            "geom": {
                "type": "Point",
                "coordinates": [
                    80.33305,
                    5.983056
                ]
            },
            "confirmed": true
        }
    ],
    "hotels": [
        {
            "id": 1399511245,
            "cityId": 895,
            "stars": 0,
            "pricefrom": 30,
            "rating": 0,
            "popularity": 900,
            "propertyType": 6,
            "checkIn": "14:00",
            "checkOut": "12:00",
            "distance": 6,
            "photoCount": 9,
            "photos": [
                {
                    "url": "http://photo.hotellook.com/image_v2/limit/h1399511245_8/320/240.auto",
                    "width": 320,
                    "height": 240
                }
            ],
            "photosByRoomType": {},
            "yearOpened": null,
            "yearRenovated": null,
            "cntRooms": null,
            "cntSuites": null,
            "cntFloors": null,
            "facilities": [
                7
            ],
            "shortFacilities": [],
            "location": {
                "lon": 81.201033,
                "lat": 6.208641
            },
            "name": {
                "en": "Sayonara Resorts"
            },
            "address": {
                "ru": "Sayonara Resorts - Pallemalala , Weligatta , Hambantota., Тиссамахарама",
                "en": "Sayonara Resorts - Pallemalala , Weligatta , Hambantota."
            },
            "link": "/lk/weerawila-895/sayonara_resorts-1399511245.html",
            "poi_distance": {
                "70642": 96987,
                "70643": 99193,
                "70650": 57116
            }
        }
    ]
}
```

### Response parameters

The response contains:

* **id** – id of hotel in database hotellook
* **cityId** – id of city
* **stars** – number of stars
* **pricefrom** – average minimum cost of the period, in USD
* **rating** – rating visitors
* **popularity** – popularity of hotel
* **propertyType** – type of hotel (hostel, motel, villa, etc.)
* **checkOut** – check out time
* **checkIn** – check in time
* **distance** – distance to the center
* **photoCount** – number of photos
* **photos**:
    * **url** – link to the photo
    * **width** – width of photo
    * **height** – height of photo
* **facilities** – id amenities in the database
* **shortFacilities** – availability of the amenities from the list: 'restaurant', 'parking', 'non-smoking', 'pets', 'tv', 'laundry', 'air conditioning', 'internet', 'pool', 'fitness', 'wi-fi in public areas', 'wi-fi in room', 'hairdryer', 'shared bathroom', 'safe', 'babysitting', 'children care/activities' (the list can change)
* **photosByRoomType** - photos of rooms types. The key - id of the room type, the value - number of photos
* **location**:
    * **lat** – latitude of hotel
    * **lon** – longitude of hotel
* **name** – hotel name
* **address** – hotel address
* **link** – link to this page of hotel
* **poi_distance** - distance to the important places (shown in the list of places id array pois and distance in meters)
* **pois** - an array of the important places:
    * **confirmed** - confirmed place
    * **rating** - place ranking
    * **location** - location
    * **name** - the name of the place
    * **geom** - coordinates of the point
    * **category** - the place category
    * **id** - id of place in the base

## Request "Types of rooms"

The request returns a file with a list of rooms type from the database.

> Sample request

```shell
curl --request GET \
  --url 'http://engine.hotellook.com/api/v2/static/roomTypes.json?language=en&token=PasteYourTokenHere' \
```

```ruby
require 'uri'
require 'net/https'

url = URI("http://engine.hotellook.com/api/v2/static/roomTypes.json?language=en&token=PasteYourTokenHere")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "http://engine.hotellook.com/api/v2/static/roomTypes.json?language=en&token=PasteYourTokenHere",
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

url = "http://engine.hotellook.com/api/v2/static/roomTypes.json"

querystring = {"language":"en", "token":"PasteYourTokenHere"}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

` GET http://engine.hotellook.com/api/v2/static/roomTypes.json?language=en&token=PasteYourTokenHere`

### Request parameters

* language - language of reaponse (pt, en, fr, de, id, it, pl, es, th, ru)
* **token** - your affiliate token

### Response

> Sample response

```json
{
   "8":"Apartment",
   "18":"Bungalow",
   "15":"Business",
   "73":"Business apartment",
   "86":"Business deluxe"
}
```

## Request "Types of hotels"

The request returns a file with a list of hotels type from the database.

> Sample request

```shell
curl --request GET \
  --url 'http://engine.hotellook.com/api/v2/static/hotelTypes.json?language=en&token=PasteYourTokenHere' \
```

```ruby
require 'uri'
require 'net/https'

url = URI("http://engine.hotellook.com/api/v2/static/hotelTypes.json?language=en&token=PasteYourTokenHere")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "http://engine.hotellook.com/api/v2/static/hotelTypes.json?language=en&token=PasteYourTokenHere",
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

url = "http://engine.hotellook.com/api/v2/static/hotelTypes.json"

querystring = {"language":"en", "token":"PasteYourTokenHere"}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

` GET http://engine.hotellook.com/api/v2/static/hotelTypes.json?language=en&token=PasteYourTokenHere`

### Request parameters

* language - language of reaponse (pt, en, fr, de, id, it, pl, es, th, ru)
* **token** - your affiliate token

### Response

> Sample response

```json
{
    "0": "Other",
    "1": "Hotel",
    "2": "Apartment Hotel",
    "3": "Bed & Breakfast",
    "4": "Apartment / Condominium",
    "5": "Motel",
    "6": "Guest House",
    "7": "Hostel",
    "8": "Resort",
    "9": "Agriturismo / Farm Stay",
    "10": "Vacation Rental",
    "11": "Lodge",
    "12": "Villa"
}
```

## Request "Hotel photos". Old method

The request returns a hotel photos from the database.

> Sample request

https://photo.hotellook.com/image_v2/limit/hId_photoId/photosize.jpg

> Examples of links to the hotel's photos with Id 503387 size 48*48, 640*480 and .auto format:

https://photo.hotellook.com/image_v2/limit/h503387_1/48.jpg

https://photo.hotellook.com/image_v2/limit/h503387_1/640/480.jpg

https://photo.hotellook.com/image_v2/limit/h503387_1/800/520.auto

```shell
curl --request GET \
  --url 'https://photo.hotellook.com/image_v2/limit/hId_photoId/photosize.jpg' \
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://photo.hotellook.com/image_v2/limit/hId_photoId/photosize.jpg")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://photo.hotellook.com/image_v2/limit/hId_photoId/photosize.jpg",
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

url = "https://photo.hotellook.com/image_v2/limit/hId_photoId/photosize.jpg"

querystring = {}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

`GET https://photo.hotellook.com/image_v2/limit/hId_photoId/photosize.jpg`

### Request parameters

* **h+Id** – h + **hotel's id**
* **photoId** – number of the hotel's photo
* **photosize** – size of the photo (width/height)
* **file_type** - you can use **.auto** in the type part of file. It means that our system detects whether a user’s browser can accept the Webp image format. If yes, the server will send the image in Webp format (smaller size). If no, the image will be in JPEG format

## Request for hotel photos. New method

The request returns a hotel photos from the database.

> Example request

```shell
curl --request GET \
  --url 'https://yasen.hotellook.com/photos/hotel_photos?id=27926056,4' \
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://yasen.hotellook.com/photos/hotel_photos?id=27926056,4")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://yasen.hotellook.com/photos/hotel_photos?id=27926056,4",
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

url = "https://yasen.hotellook.com/photos/hotel_photos"

querystring = {"id":"27926056,4"}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### First request

`GET https://yasen.hotellook.com/photos/hotel_photos?id=27926056,4`

where **id** is the id of the hotels indicated through a comma.

### Response

In response, there will be an array of photos id for each hotel:

> Sample response

```json
{
   "4": [5162091534,5162091993], "27926056": [7505789398,7505803908]
}
```

### Second request

> Sample request

```shell
curl --request GET \
  --url 'https://photo.hotellook.com/image_v2/limit/photo_id/800/520.auto' \
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://photo.hotellook.com/image_v2/limit/photo_id/800/520.auto")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://photo.hotellook.com/image_v2/limit/photo_id/800/520.auto",
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

url = "https://photo.hotellook.com/image_v2/limit/photo_id/800/520.auto"

querystring = {}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

After that, send a request to the address [https://photo.hotellook.com/image_v2/limit/photo_id/800/520.auto](https://photo.hotellook.com/image_v2/limit/photo_id/800/520.auto)

where instead of **photo_id** substitute id photos.

## Request "Hotel's room photos (in a sprite)"

The request returns a hotel's rooms photos from the database.

Use this request to get a sprite with photos of rooms.

> Sample request

```shell
curl --request GET \
  --url 'https://photo.hotellook.com/rooms/sprite/h4_1/100/3/50.auto' \
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://photo.hotellook.com/rooms/sprite/h4_1/100/3/50.auto")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://photo.hotellook.com/rooms/sprite/h4_1/100/3/50.auto",
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

url = "https://photo.hotellook.com/rooms/sprite/h4_1/100/3/50.auto"

querystring = {}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

> To get a sprite with rectangular photographs, along with the need to specify the width of the height of the photos:

https://photo.hotellook.com/rooms/sprite/h4_12/100x50/3/50x25.auto

### Request

` GET https://photo.hotellook.com/rooms/sprite/hhotel-id_group-id/first_width/photos_count-1/rest_photos_width.auto`

### Request parameters

* **h + hotel-Id** - letter h + Hotel identifier (from static/hotels.json)
* **group-id** - ID room type (from static/hotels.json and internalTypeId of the search for an answer)
* **first_width** - width of the first photo in the sprite
* **photos_count-1** - number of photos of the room type minus one (from the static/hotels.json). For example, if the answer is that photographs of this type have four pieces, it indicates three instead of this parameter
* **rest_photos_width** - width of the rest of the photos in the sprite
* **auto** - our system checks whether a user's browser can accommodate the WebP image format. If yes, the server will provide a WebP image format. If not, the image will be in JPEG format

### Additional information

To get a picture of the room, given the size, use code like:

`https://photo.hotellook.com/rooms/crop/h<hotel_id>_<group_id>_<photo_idx>/<width>/<height>.auto`

This photo will be scaled and cropped to the specified size.

To get a photo that is no longer a given size or type, use the code:

`https://photo.hotellook.com/rooms/limit/h<hotel_id>_<group_id>_<photo_idx>/<widt*>/<height>.auto`

Parameters similar to those described in the request above, except for photo_idx - an index image in the list (first index pictures - 0).

[https://photo.hotellook.com/rooms/limit/h4_12_1/200/200.auto](https://photo.hotellook.com/rooms/limit/h4_12_1/200/200.auto)

## Request 'City photo'

The request returns a city photos from the database.

> Sample request

```shell
curl --request GET \
  --url 'https://photo.hotellook.com/static/cities/960x720/LED.jpg' \
```

```ruby
require 'uri'
require 'net/https'

url = URI("https://photo.hotellook.com/static/cities/960x720/LED.jpg")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)

response = https.request(request)
puts response.read_body
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://photo.hotellook.com/static/cities/960x720/LED.jpg",
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

url = "https://photo.hotellook.com/static/cities/960x720/LED.jpg"

querystring = {}

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)
```

### Request

`GET https://photo.hotellook.com/static/cities/960x720/LED.jpg`

### Request parameters

* **photosize** – size of the photo (width/height)
* **city_iata** - IATA code of the city
