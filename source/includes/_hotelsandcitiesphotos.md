# Photos of hotels, rooms and cities

## Request "Hotel photos". Old method

Endpoint: [https://photo.hotellook.com/image_v2/limit](https://photo.hotellook.com/image_v2/limit)

> Sample request

https://photo.hotellook.com/image_v2/limit/hId_photoId/photosize.jpg

> Examples of links to the hotel's photos with Id 503387 size 48*48, 640*480 and .auto format:

https://photo.hotellook.com/image_v2/limit/h503387_1/48.jpg

https://photo.hotellook.com/image_v2/limit/h503387_1/640/480.jpg

https://photo.hotellook.com/image_v2/limit/h503387_1/800/520.auto

### Request

`GET https://photo.hotellook.com/image_v2/limit/hId_photoId/photosize.jpg`

### Request parameters

* **h+Id** – h + **hotel's id**.
* **photoId** – number of the hotel's photo.
* **photosize** – size of the photo (width/height).
* **file_type** - you can use **.auto** in the type part of file. It means that our system detects whether a user’s browser can accept the Webp image format. If yes, the server will send the image in Webp format (smaller size). If no, the image will be in JPEG format.

## Request for hotel photos. New method

**Endpoint**: [https://yasen.hotellook.com/photos/hotel_photos](https://yasen.hotellook.com/photos/hotel_photos)

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

https://photo.hotellook.com/image_v2/limit/photo_id/800/520.auto

After that, send a request to the address [https://photo.hotellook.com/image_v2/limit/photo_id/800/520.auto](https://photo.hotellook.com/image_v2/limit/photo_id/800/520.auto)

where instead of **photo_id** substitute id photos.

## Request "Hotel's room photos (in a sprite)"

**Endpoint**: [https://photo.hotellook.com/rooms/sprite/](https://photo.hotellook.com/rooms/sprite/)

Use this request to get a sprite with photos of rooms.

> Sample request

https://photo.hotellook.com/rooms/sprite/h4_1/100/3/50.auto

> To get a sprite with rectangular photographs, along with the need to specify the width of the height of the photos:

https://photo.hotellook.com/rooms/sprite/h4_12/100x50/3/50x25.auto

### Request

` GET https://photo.hotellook.com/rooms/sprite/hhotel-id_group-id/first_width/photos_count-1/rest_photos_width.auto`

### Request parameters

* **h + hotel-Id** - letter h + Hotel identifier (from static/hotels.json).
* **group-id** - ID room type (from static/hotels.json and internalTypeId of the search for an answer).
* **first_width** - width of the first photo in the sprite.
* **photos_count-1** - number of photos of the room type minus one (from the static/hotels.json). For example, if the answer is that photographs of this type have four pieces, it indicates three instead of this parameter.
* **rest_photos_width** - width of the rest of the photos in the sprite.
* **auto** - our system checks whether a user's browser can accommodate the WebP image format. If yes, the server will provide a WebP image format. If not, the image will be in JPEG format.

### Additional information

To get a picture of the room, given the size, use code like:

`https://photo.hotellook.com/rooms/crop/h<hotel_id>_<group_id>_<photo_idx>/<width>/<height>.auto`

This photo will be scaled and cropped to the specified size.

To get a photo that is no longer a given size or type, use the code:

`https://photo.hotellook.com/rooms/limit/h<hotel_id>_<group_id>_<photo_idx>/<widt*>/<height>.auto`

Parameters similar to those described in the request above, except for photo_idx - an index image in the list (first index pictures - 0).

[https://photo.hotellook.com/rooms/limit/h4_12_1/200/200.auto](https://photo.hotellook.com/rooms/limit/h4_12_1/200/200.auto)

## Request 'City photo'

**Endpoint**: [https://photo.hotellook.com/static/cities/](https://photo.hotellook.com/static/cities/)

> Sample request

https://photo.hotellook.com/static/cities/960x720/LED.jpg

### Request parameters

* **photosize** – size of the photo (width/height)
* **city_iata** - IATA code of the city
