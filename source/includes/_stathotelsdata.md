# Statistical hotels data data

Requests as a result of which the partner receives information about the countries, cities and hotels.

**Attention**! The default number of requests is limited to **60 per minute**. If you need to process more requests, send a letter to support@travelpayouts.com.

## Request "Country"

`GET http://engine.hotellook.com/api/v2/static/countries.json`

### Request

> Sample request

```shell
http://engine.hotellook.com/api/v2/static/countries.json?token=PasteYourTokenHere
```

### Request parameters

* **token** - your affiliate token.

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

* **Id** – id of country.
* **code** – code of country.
* The block EN:
    * **isVariation** – primary or secondary title. 1 - secondary, 0 - primary.
    * **name** – country name in English.
* The block RU:
    * **isVariation** – primary or secondary title.
    * **name** – country name in Russian.

## Request "Cities"

`GET http://engine.hotellook.com/api/v2/static/locations.json`

### Request

> Sample request

```shell
http://engine.hotellook.com/api/v2/static/locations.json?token=PasteYourTokenHere
```

### Request parameters

* token - your affiliate token.

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

* **Id** – id of city.
* **code** – iata-code of city.
* **countryId** – id of country.
* **latitude** – latitude of city.
* **longitude** – longitude of city.
* The block DE:
    * **isVariation** - primary or secondary title. 1 - secondary, 0 - primary.
    * **name** – city name in German.
* The block EN:
    * **isVariation** - primary or secondary title.
    * **name** – city name in English.
* The block RU:
    * **isVariation** – primary or secondary title.
    * **name** – city name in Russian.

## Request "Amenities"

`GET http://engine.hotellook.com/static/amenities/`

### Request

> Sample request

```shell
http://engine.hotellook.com/api/v2/static/amenities/en.json?token=PasteYourTokenHere
```

### Request parameters

* **en.json** - language that you want to see result (en, ru, fr, de and etc);
* **token** - your affiliate token.

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

* **Id** – id of amenities in the database.
* **name** – name of amenities.
* **groupName** - location of amenities.

## Request 'Hotels list'

`GET http://engine.hotellook.com/static/hotels.json`

### Request

> Sample request

```shell
http://engine.hotellook.com/api/v2/static/hotels.json?locationId=895&token=PasteYourTokenHere
```

### Request parameters

* **locationId** – id of location.
* **token** – your affiliate token.

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

* **id** – id of hotel in database hotellook.
* **cityId** – id of city.
* **stars** – number of stars.
* **pricefrom** – average minimum cost of the period, in USD
* **rating** – rating visitors.
* **popularity** – popularity of hotel.
* **propertyType** – type of hotel (hostel, motel, villa, etc.).
* **checkOut** – check out time.
* **checkIn** – check in time.
* **distance** – distance to the center.
* **photoCount** – number of photos.
* **photos**:
    * **url** – link to the photo.
    * **width** – width of photo.
    * **height** – height of photo.
* **facilities** – id amenities in the database.
* **shortFacilities** – availability of the amenities from the list: 'restaurant', 'parking', 'non-smoking', 'pets', 'tv', 'laundry', 'air conditioning', 'internet', 'pool', 'fitness', 'wi-fi in public areas', 'wi-fi in room', 'hairdryer', 'shared bathroom', 'safe', 'babysitting', 'children care/activities' (the list can change).
* **photosByRoomType** - photos of rooms types. The key - id of the room type, the value - number of photos.
* **location**:
    * **lat** – latitude of hotel.
    * **lon** – longitude of hotel.
* **name** – hotel name.
* **address** – hotel address.
* **link** – link to this page of hotel. 
* **poi_distance** - distance to the important places (shown in the list of places id array pois and distance in meters).
* **pois** - an array of the important places:
    * **confirmed** - confirmed place;
    * **rating** - place ranking;
    * **location** - location;
    * **name** - the name of the place;
    * **geom** - coordinates of the point;
    * **category** - the place category;
    * **id** - id of place in the base.

## Request "Types of rooms"

`GET http://engine.hotellook.com/static/roomTypes.json`

> Sample request

```shell
http://engine.hotellook.com/api/v2/static/roomTypes.json?language=en&token=PasteYourTokenHere
```

### Request parameters

* language - language of reaponse (pt, en, fr, de, id, it, pl, es, th, ru).
* **token** - your affiliate token.

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

`GET http://engine.hotellook.com/static/hotelTypes.json`

### Request

> Sample request

```shell
http://engine.hotellook.com/api/v2/static/hotelTypes.json?language=en&token=PasteYourTokenHere
```

### Request parameters

* language - language of reaponse (pt, en, fr, de, id, it, pl, es, th, ru).
* **token** - your affiliate token.

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
