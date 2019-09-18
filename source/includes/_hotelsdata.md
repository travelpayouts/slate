# Hotels data API

## Authorization

The authorization is based on [affilliate token](https://www.travelpayouts.com/developers/api).

## Hotel search by name or location

**Endpoint**: [http://engine.hotellook.com/api/v2/lookup.json](http://engine.hotellook.com/api/v2/lookup.json)

Search for a specific location or name places of a hotel (city, island).

**Attention!** If you send a request without a token, the number of queries will be limited. The values of restrictions are passed in the response header:

* X-Ratelimit-Interval - limit interval in seconds;
* X-Ratelimit-Remaining - how many requests left of this limit;
* X-Ratelimit-Limit - the value limit.

> Sample request

```shell
http://engine.hotellook.com/api/v2/lookup.json?query=moscow&lang=ru&lookFor=both&limit=1&token=PasteYourTokenHere
```

### Request

`GET http://engine.hotellook.com/api/v2/lookup.json?query=moscow&lang=ru&lookFor=both&limit=1&token=PasteYourTokenHere`

### Request parameters

Required parameters are highlighted in **bold**.

* **query** – main parameter, it is set:
    * as a text;
    * by longitude and latitude (also displays the nearest objects).
* lang – display language. It can take any iso-language code (pt, en, fr, de, id, it, pl, es, th, ru); if the database doesn’t include a translation for the requested language, it returns the English name of the object. By default, lang="en".
* lookFor – objects displayed in the results:
    * city;
    * hotel;
    * both (city&hotel).
* limit – limitation of output results from 1 to 100, default - 10.
* convertCase – automatically change the keyboard layout (actual for Russian users, for example, when requesting "vjcrdf" will be found "москва"). Values - 1 or 0. Default - 1. 
* token - your affiliate token.

### Response

> Sample response

```json
{
    "results": {
        "locations": [
            {
                "cityName": "Москва",
                "fullName": "Москва, Россия",
                "countryCode": "RU",
                "countryName": "Россия",
                "iata": [
                    "BKA",
                    "DME",
                    "SVO",
                    "VKO",
                    "MOW"
                ],
                "id": "12153",
                "hotelsCount": "930",
                "location": {
                    "lat": "55.752222200",
                    "lon": "37.615555600"
                },
                "_score": 3.2695
            }
        ],
        "hotels": [
            {
                "label": "Отель Novotel Moscow City",
                "locationName": "Москва, Россия",
                "locationId": "12153",
                "id": "1074388",
                "fullName": "Отель Novotel Moscow City, Москва, Россия",
                "location": {
                    "lat": "55.747160",
                    "lon": "37.539302"
                }
            }
        ]
    },
    "status": "ok"
}
```

The block "**locations**" includes:

* **cityName** – city name;
* **fullName** – name of city and country;
* **countryCode** – IATA code of country;
* **countryName** – country name;
* **iata** – IATA airport code in this city, there may be several;
* **id** – location id in the database;
* **hotelsCount** – number of hotels in this location;
* **location**:
    * **lat** – latitude of location;
    * **lon** – longitude of location.
* **score** – internal parameter, used for sorting.
* **token** - your affiliate token.

The block "**hotels**" includes:

* **label** – name of hotel;
* **locationName** – location of hotel;
* **locationId** – location id in the database;
* **Id** – hotel id in the database;
* **fullName** – full name of the hotel and the location of it;
* **location**:
    * **lat** – latitude of hotel;
    * **lon** – longitude of hotel.

## Searching a hotel or location by coordinates

**Endpoint**: [http://engine.hotellook.com/api/v2/lookup.json](http://engine.hotellook.com/api/v2/lookup.json)

Search for a specific location or hotel (city, island) by coordinates.

**Attention!** If you send a request without a token, the number of queries will be limited. The values of restrictions are passed in the response header:

* X-Ratelimit-Interval - limit interval in seconds;
* X-Ratelimit-Remaining - how many requests left of this limit;
* X-Ratelimit-Limit - the value limit.

> Sample request

```shell
http://engine.hotellook.com/api/v2/lookup.json?query=55.0291,82.9059&lang=ru&lookFor=both&limit=1&token=PasteYourTokenHere
```

### Request

`GET http://engine.hotellook.com/api/v2/lookup.json?query=55.0291,82.9059&lang=ru&lookFor=both&limit=1&token=PasteYourTokenHere`

### Request parameters

Required parameters are highlighted in **bold**.

* **query** – main parameter, it is set:
    * as a text;
    * by the longitude and latitude (also displays the nearest objects).
* lang – display language. It can take any iso-language code (pt, en, fr, de, id, it, pl, es, th, ru) - if the database doesn’t include a translation for the requested language, it returns the English name of the object. By default lang="en".
* lookFor – objects displayed in the results:
    * city;
    * hotel;
    * both (city&hotel).
* limit – limitation of output results from 1 to 100, default - 10.
* convertCase – automatically change the keyboard layout (actual for Russian users, for example, when requesting "vjcrdf" will be found "москва"). Values - 1 or 0. Default - 1.
* token - your affiliate token.

### Response

> Sample response

```json
{
    "results": {
        "locations": [
            {
                "id": "12167",
                "type": "City",
                "countryIso": "RU",
                "name": "Новосибирск",
                "state": "",
                "fullname": "Новосибирск, Россия",
                "geo": {
                    "lat": "55.028705000",
                    "lon": "82.906898000"
                }
            }
        ],
        "hotels": [
            {
                "id": "380923",
                "name": "AZIMUT Отель Сибирь",
                "locationId": "12167",
                "location": {
                    "lat": "55.029140",
                    "lon": "82.905990"
                }
            }
        ]
    },
    "status": "ok"
}
```

The block "**locations**" includes:

* **id** – id of locations in the database.
* **type** – type of locations (city, isle).
* **countryIso** – country code.
* **name** – name of locations.
* **state** – code of state.
* **fullname** – full name of the location with the name of the country.
* **geo**:
    * **lat** – latitude of location.
    * **on** – longitude of location.

The block "**hotels**" includes:

* **Id** – id of hotel in the database.
* **name** – name of hotel.
* **locationId** – location id in the database.
* **location**:
    * **lat** – latitude of hotel.
    * **lon** – longitude of hotel.

## Displays the cost of living in hotels

**Endpoint**: [http://engine.hotellook.com/api/v2/cache.json](http://engine.hotellook.com/api/v2/cache.json)

The request is used to get the price of hotel rooms from the cache for the period. It doesn't contain information about room availability.

**Attention**! If you send a request without a token, the number of queries will be limited. The values of restrictions are passed in the response header:

* X-Ratelimit-Interval - limit interval in seconds;
* X-Ratelimit-Remaining - how many requests left of this limit;
* X-Ratelimit-Limit - the value limit.

> Sample request

```shell
http://engine.hotellook.com/api/v2/cache.json?location=Saint-Petersburg&hotelId=277083&checkIn=2017-09-13&checkOut=2017-09-18&currency=rub&limit=1&token=PasteYourTokenHere
```

### Request

`GET http://engine.hotellook.com/api/v2/cache.json?location=Saint-Petersburg&hotelId=277083&checkIn=2017-09-13&checkOut=2017-09-18&currency=rub&limit=1&token=PasteYourTokenHere`

### Request parameters

* **location** - location name (IATA code can be used location);
* **checkIn** - date of check-in;
* **checkOut** - date of check-out;
* locationId - id of location (can be used instead of the location);
* hotelId - id of the hotel;
* hotel - name of the hotel (when entering the name necessarily indicate the location or locationId;
* adults - number of guests (by default, 2);
* children - number of children (2 to 18 years);
* infants - number of infants (0 to 2 years);
* limit - number of hotels. If this parameter is used in a query without specifying a precise ID or name of the hotel, the following applies:
    * limit = 4 (default) - will return for one hotel each category (Stars);
    * limit = 5 - return two five-stars hotel and one of the other categories;
    * limit = 6 - two 5 and 4-star hotel and the other one;
    * limit = 7 - two 5, 4 and 3-star hotels and one comfortable;
    * limit = 8 - all of two. And so on, with the growth parameters in turn increasing the number of hotels in every star. If the specified star hotels are no more, the issue will begin to fall and hotels 1 0 star by the same rule.
* customerIp - parameter to specify the user IP if the request is not sent directly, but through a proxy server.
* currency - currency of price (rub, usd, eur). 
* token - your affiliate token.

### Response

> Sample response

```json
{
    "location": {
        "country": "Russia",
        "geo": {
            "lon": 37.617508,
            "lat": 55.752041
        },
        "state": null,
        "name": "Moscow"
    },
    "priceAvg": 60897.74,
    "pricePercentile": {
        "3": 28863.56,
        "10": 28863.56,
        "35": 47805.27,
        "50": 59531.09,
        "75": 65435,
        "99": 120128.17
    },
    "hotelName": "Mercure Arbat Moscow",
    "stars": 4,
    "locationId": 12153,
    "hotelId": 333561,
    "priceFrom": 28863.56
}
```

* **stars** - number of the hotel's stars;
* **locationId** - location id of this hotel;
* **priceFrom** - minimum price per stay in a hotel room for the period;
* **priceAvg** - average price per stay in a hotel room for the period;
* **pricePercentile** - segmentation price for proportions (e.g., record type "50": 59531.09 means that 50% of the price is in the range of 59531.09 to rub);
* **hotelName** - name of hotel;
* **location** - information about the location of the hotel:
    * **geo** - coordinates of the hotel;
    * **name** - name of location (city);
    * **state** - state in which the city is located;
    * **country** - a country of hotel.
* hotelId - id of hotel.

## List of hotels in the archive

**Endpoint**: http://yasen.hotellook.com/tp/v1/hotels

This request return the file with a list of all hotels for the specified locale.

### Request

`GET http://yasen.hotellook.com/tp/v1/hotels?language=en`

### Request parameters

The **language** parameter can take the values:

* ru (Russian);
* en (English);
* th (Thai);
* de (German);
* es (Spanish);
* fr (French);
* it (Italian);
* pl (Polish).

### Response

The file with a list of hotels includes the following data:

* **id** - unique id of the hotel;
* **name** - name of the hotel;
* **location_name** - name of the place location of the hotel;
* **location_id** - a unique id location of the hotel;
* **location_iata** - IATA code for the location of the hotel;
* **country_name** - name of the country in which the hotel is located;
* **photos_count** - number of photos of the hotel in the database.

The hotels file is updated once a week in the morning (GMT) on Saturday.

**Note**! To download the list of hotels you **do not need** access to the search hotels API.

## Hotels Selections

**Endpoint**: [http://yasen.hotellook.com/tp/public/widget_location_dump.json](http://yasen.hotellook.com/tp/public/widget_location_dump.json)

The request recovers the list of specific hotels according to the ID of a location. A collection is formed according to the specified period. If the period is not specified, a collection shall be formed from the hotels found for the last three days.

> Sample request

```shell
http://yasen.hotellook.com/tp/public/widget_location_dump.json?currency=rub&language=ru&limit=5&id=12209&type=popularity&check_in=2017-02-02&check_out=2017-02-17&token=PasteYourTokenHere
```

### Request

`GET http://yasen.hotellook.com/tp/public/widget_location_dump.json?currency=rub&language=ru&limit=5&id=12209&type=popularity&check_in=2017-02-02&check_out=2017-02-17&token=PasteYourTokenHere`

### Request parameters

* **check_in** — date of check-in;
* **check_out** — date of check-out;
* **currency** — currency of response;
* **language** — language of reaponse (pt, en, fr, de, id, it, pl, es, th, ru);
* **limit** — limitation of output results from 1 to 100, default - 10;
* **type** — type of hotels from request `/tp/public/available_selections.json`;
* **id** — id of the city.
* **token** — your affiliate token.

### Response

> Sample response

```json
{
    "popularity": [
        {
            "hotel_id": 713859,
            "distance": 6.68,
            "name": "President Hotel",
            "stars": 4,
            "rating": 87,
            "property_type": "hotel",
            "hotel_type": [
                "Solo Hotel"
            ],
            "last_price_info": {
                "price": 39707,
                "old_price": 42761,
                "discount": 7,
                "insertion_time": 1485464441,
                "nights": 15,
                "search_params": {
                    "adults": 2,
                    "children": {},
                    "checkIn": "2017-02-02",
                    "checkOut": "2017-02-17"
                },
                "price_pn": 2647,
                "old_price_pn": 2851
            },
            "has_wifi": true
        }
    ]
}
```

* **hotel_id** – unique hotels’ ID;
* **distance** – distance from the city’s center;
* **name** – hotel’s name;
* **stars** – number of stars;
* **rating** – hotel’s rating, assigned by its visitors;
* **property_type** – type of a hotel;
* **hotel_type** – description of a hotel’s type;
* **last_price_info** – information about the last found price of a hotel (if any):
    * **price** – price of accommodation during the whole period with a discount;
    * **old_price** - price of accommodation without a discount;
    * **discount** – amount of a discount;
    * **insertion_time** – time, when the collection was found;
    * **nights** – number of nights.
* **search_params** – search parameters;
* **price_pn** – price of a night in a hotel room with a discount;
* **old_price_pn** - price of a night in a hotel room without a discount;
* **has_wifi** – availability of Wi-Fi.

## The types of hotel collections

**Endpoint**: [http://yasen.hotellook.com/tp/public/available_selections.json](http://yasen.hotellook.com/tp/public/available_selections.json)

The request recovers the list of all available separate collections. This type is used to search for hotels with a discount.

> Sample request

```shell
http://yasen.hotellook.com/tp/public/available_selections.json?id=12209&token=PasteYourTokenHere
```

### Request

`GET http://yasen.hotellook.com/tp/public/available_selections.json?id=12209&token=PasteYourTokenHere`

### Request parameters

* **id** — id of the city.
* **token** — your affiliate token.

### Response

> Sample response

```json
[
	"center",
	"tophotels",
	"highprice",
	"3-stars",
	"4-stars",
	"5-stars",
	"restaurant",
	"pets",
	"pool",
	"cheaphotel_ufa",
	"luxury_ufa",
	"price",
	"rating",
	"distance",
	"popularity",
	"2stars",
	"3stars",
	"4stars",
	"5stars"
]
```

* **center** – hotels, located in the center of a city;
* **tophotels** – best hotels;
* **highprice** – most expensive hotels;
* **3-stars, 4-stars, 5-stars** – automatic searching of the hotels, having 3, 4 or 5 stars;
* **restaurant** – availability of the own restaurant;
* **pets** – opportunity to live with the pets;
* **pool** – availability of the own pool;
* **cheaphotel** – cheapest hotels;
* **luxury** – luxury hotels;
* **price** – manually formed collections by the price;
* **rating** – hotels with the highest rating;
* **distance** – distance from an airport;
* **popularity** – popularity of a hotel;
* **2stars, 3stars, 4stars, 5stars** – manually formed collections with the corresponding number of stars.
