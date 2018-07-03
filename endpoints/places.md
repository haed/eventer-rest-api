# /places

Use this endpoint to retrieve places. This endpoint supports [GET and POST requests](https://github.com/haed/eventer-rest-api/blob/master/README.md#getpost-methods).

Examples:
* [`GET https://api.eventer.app/v1/places?google_place_ids=ChIJYzs3_URGp0cRspbeorh84LM,ChIJQXmv10JGp0cROM6S5hB1AG8`](https://api.eventer.app/v1/places?google_place_ids=ChIJYzs3_URGp0cRspbeorh84LM,ChIJQXmv10JGp0cROM6S5hB1AG8) to get informations about 2 interesting locations in Chemnitz.


## Request parameters

parameter | description
--------- | -----------
`google_place_ids` | A comma separated list of ids of google places to get informations of these places.<br/><br/>You can use the google maps api to search for google place ids: [google place id finder](https://developers.google.com/maps/documentation/javascript/examples/places-placeid-finder)


## Reponse

Example response:
```json
{
    "places": {
        "ChIJQXmv10JGp0cROM6S5hB1AG8": {
            "name": "Weltecho",
            "location": {
                "lat": 50.8284307,
                "lng": 12.9203243
            },
            "google_place_id": "ChIJQXmv10JGp0cROM6S5hB1AG8",
            "website_url": "http://www.weltecho.eu/"
        },
        "ChIJYzs3_URGp0cRspbeorh84LM": {
            "name": "Kino Metropol",
            "location": {
                "lat": 50.8283138,
                "lng": 12.9144548
            },
            "google_place_id": "ChIJYzs3_URGp0cRspbeorh84LM",
            "website_url": "http://www.metropol-chemnitz.de/"
        }
    },
    "request": {
        "google_place_ids": [
            "ChIJYzs3_URGp0cRspbeorh84LM",
            "ChIJQXmv10JGp0cROM6S5hB1AG8"
        ]
    },
    "timestamp": "2017-10-15T20:57:11.766Z"
}
```
