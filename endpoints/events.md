# /events

Use this endpoint to search for events. This endpoint supports [GET and POST requests](https://github.com/haed/eventer-rest-api/blob/master/README.md#getpost-methods).

Examples:
* `GET /v1/events?geo_area=50.838948,12.912577,50.827132,12.933774` will return events from the inner city of Chemnitz.
* `GET /v1/events?categories=movie` will return only movies.
* `GET /v1/events?categories=!movie` will return events which are not movies.
* `GET /v1/events?search=Party` will search for "Party" events.

All returned events will be primarily sorted by `event.starts_at` timestamps.


## GET request parameters

parameter | description
--------- | -----------
`starts_at_min` | The minimum starts-at timestamp for events. If not given the default value will be *now*.
`starts_at_max` | The maximum starts-at timestamp for events.
`geo_area` | Restricts the event search to a geo area bounding box specified by 4 comma separated coordinates: top (latitude), left (longitude), bottom (latitude) and right (longitude). <br/><br/>Example value for the inner city of Chemnitz: `50.838948,12.912577,50.827132,12.933774`.
`geo_raster_points` | Restricts the event search to a geo areas specified by "raster points". A raster point is a latitude/longitude combination of double values rounded off to 2 decimal places (separated by a semicolon). For example the "raster point" `50.83;12.91` restricts events to locations within a latitude starting with `50.83` and longitude starting with `12.91`. <br/><br/>Example for a list of raster points: `50.83;12.91,50.82,12.91`.
`categories` | A comma separated list of event categories to search for (not all events are categorized yet). If not specified all events of all categories (or without category) will be returned.<br/><br/>Note: also you can exclude categories from the result by using `!` as a category suffix.<br/><br/>Currently the following categories are supported: <br/>`meetup`, `movie`
`google_place_ids` | A comma separated list of ids of google places to restrict search to events from these places only.<br/><br/>You can use the google maps api to search for google place ids: [google place id finder](https://developers.google.com/maps/documentation/javascript/examples/places-placeid-finder)
`search` | Searches events by a free text search.
`updated_since` | If set only events will be returned which has been added or modified since the given timestamp. Can be used for synchronization or fetch scenarios.
`limit` | Sets the limit how much events should be returned by the response. Limit must be greater than 0 and lower than 101. If not set the default limit will be 10.<br/><br/>See [Pagination & limit](https://github.com/haed/eventer-rest-api/blob/master/README.md#pagination--limit) for details.
`cursor` | Continues a search by an "offset" specified by this cursor. Any event search could return a cursor which represents an offset to paginate to the next events. To use a cursor you have the re-run the request with same parameters again but with the given cursor value to retrieve the next events of your search behind the limit.<br/><br/>See [Pagination & limit](https://github.com/haed/eventer-rest-api/blob/master/README.md#pagination--limit) for details.


## POST request parameters

Same as described GET request parameters (see also: [GET/POST methods](https://github.com/haed/eventer-web-api#getpost-methods)), but the following parameters are different:

parameter | description
--------- | -----------
`geo_area` | Geo area is an object with following properties: `{top, left, bottom, right}`.  <br/><br/>Example: `{"top": 50.838948, "left": 12.912577, "bottom": 50.827132, "right": 12.933774}`.
`geo_raster_points` | Raster points is an array of arrays of two double values. <br/><br/>Example: `[[50.83, 12.91], [50.82, 12.91]]`.


## Response

Example response:
```json
{
    "events": [
        {
            "id": 5128325034934272,
            "title": "´S wär schon schön",
            "description": "Gestern war heute Morgen, und übermorgen ist auch noch ein Tag. Doch etwas muss passieren, so geht's nicht weiter. Und was sagt eigentlich Mutti? Wenn unter einem Dach drei Generationen leben, haben nicht nur die ihren Spaß, sondern auch das Publikum.",
            "google_place_id": "ChIJabRmd1lGp0cRiBOpVGgAKx4",
            "updated_at": "2018-01-10T18:45:41.374Z",
            "starts_at": "2018-01-20T16:00:00.000Z"
        },
        {
            "id": 6050746571161600,
            "title": "2. Basketball-Bundesliga ProA",
            "categories": [
                "sport"
            ],
            "google_place_id": "ChIJleR_61lGp0cRrD7wwgVz6fA",
            "updated_at": "2018-01-10T18:47:00.662Z",
            "starts_at": "2018-01-20T18:00:00.000Z"
        },
        {
            "id": 6238292492156928,
            "title": "Bombenstimmung",
            "description": "Konzerne freuen sich über die Kreditschwemme, Rüstungsschmieden auf Aufträge, Taxifahrer auf den Mindestlohn und Familien auf die Kindergelderhöhung um 2 €. Nur bei Griechen und Asylbewerbern ist die Freude noch getrübt. Doch Abhilfe ist in Sicht.",
            "google_place_id": "ChIJabRmd1lGp0cRiBOpVGgAKx4",
            "updated_at": "2018-01-10T18:47:31.389Z",
            "starts_at": "2018-01-20T19:00:00.000Z"
        },
        {
            "id": 6043889655873536,
            "title": "English Comedy Showcase #18",
            "description": "Das Show-Format für Liebhaber amerikanischer TV-Serien und Englisch-Lernende in englischer Sprache. Zu Gast sind Miles Lloyd und Tim Whelan.",
            "google_place_id": "ChIJgYD4qVBGp0cRILA3_lFAsuI",
            "updated_at": "2018-01-10T18:46:59.854Z",
            "starts_at": "2018-01-20T19:30:00.000Z"
        },
        {
            "id": 5119862875619328,
            "title": "Nils Holgersson",
            "description": "Vogelforscher Lundgren findet eine graue Feder und sofort fällt ihm die Geschichte von Nils Holgersson ein, einem Jungen, der auf dem Rücken eines weißen Gänserichs versucht, einer Schar Wildgänse zu folgen. Kreatives Schauspiel für Kinder ab 4.",
            "google_place_id": "ChIJgYD4qVBGp0cRILA3_lFAsuI",
            "updated_at": "2018-01-10T18:45:40.349Z",
            "starts_at": "2018-01-21T14:30:00.000Z"
        }
    ],
    "cursor": "WzE1MTY1NDUwMDAsImV2ZW50IzUxMTk4NjI4NzU2MTkzMjgiXQ==",
    "request": {
        "limit": 5,
        "starts_at_min": "2018-01-20T12:00:00.000Z",
        "geo_raster_points": [
            [
                50.83,
                12.91
            ]
        ]
    },
    "timestamp": "2018-01-17T08:56:08.542Z"
}
```
