# /events

Use this endpoint to search for events. This endpoint supports [GET and POST requests](https://github.com/haed/eventer-rest-api/blob/master/README.md#getpost-methods).

Examples:
* `GET /v1/events?area=50.838948,12.912577,50.827132,12.933774` will return events from the inner city of Chemnitz.
* `GET /v1/events?categories=movie` will return only movies.
* `GET /v1/events?categories=!movie` will return events which are not movies.
* `GET /v1/events?search=Party` will search for "Party" events.

All returned events will be primarily sorted by `event.starts_at` timestamps.


## Request parameters

parameter | description
--------- | -----------
`starts_at_min` | The minimum starts-at timestamp for events. If not given the default value will be *now*.
`starts_at_max` | The maximum starts-at timestamp for events.
`area` | Restricts the event search to a geolocation rectangle specified by 4 comma separated coordinates: top (latitude), left (longitude), bottom (latitude) and right (longitude). <br/><br/>Example value for the inner city of Chemnitz: `50.838948,12.912577,50.827132,12.933774`.
`categories` | A comma separated list of event categories to search for (not all events are categorized yet). If not specified all events of all categories (or without category) will be returned.<br/><br/>Note: also you can exclude categories from the result by using `!` as a category suffix.<br/><br/>Currently the following categories are supported: <br/>`meetup`, `movie`
`google_place_ids` | A comma separated list of ids of google places to restrict search to events from these places only.<br/><br/>You can use the google maps api to search for google place ids: [google place id finder](https://developers.google.com/maps/documentation/javascript/examples/places-placeid-finder)
`search` | Searches events by a free text search.
`updated_since` | If set only events will be returned which has been added or modified since the given timestamp. Can be used for synchronization or fetch scenarios.
`limit` | Sets the limit how much events should be returned by the response. Limit must be greater than 0 and lower than 101. If not set the default limit will be 10.<br/><br/>See [Pagination & limit](https://github.com/haed/eventer-rest-api/blob/master/README.md#pagination--limit) for details.
`cursor` | Continues a search by an "offset" specified by this cursor. Any event search could return a cursor which represents an offset to paginate to the next events. To use a cursor you have the re-run the request with same parameters again but with the given cursor value to retrieve the next events of your search behind the limit.<br/><br/>See [Pagination & limit](https://github.com/haed/eventer-rest-api/blob/master/README.md#pagination--limit) for details.


## Reponse

Example response:
```json
{
    "events": [
        {
            "id": 5007441972428800,
            "title": "Die Hochzeit des Figaro",
            "description": "An seinem Hochzeitstag erfährt Figaro, dass sein Freund Graf Almaviva seiner Braut nachstellt, zumal Figaro dem Schürzenjäger Almaviva die Wege für dessen Frauengeschichten ebnete. Nun führt einer der Wege aber in sein eigenes Schlafzimmer.",
            "google_place_id": "ChIJ8aXQ2iwqckERIgNrPqoGhkQ",
            "starts_at": "2017-10-15T16:00:00.000Z"
        },
        {
            "id": 5907333720834048,
            "title": "Peter Pan - Fliege deinen Traum!",
            "description": "Als die Eltern nachts ausgegangen sind, fliegen Wendy, John und Michael Darling mit Peter Pan nach Nimmerland, der Insel der ewigen Kindheit und erleben dort die wunderlichsten Abenteuer. Alles nur ein Traum? Mitreißendes und poetisches Musical.",
            "google_place_id": "ChIJc7ob_KmtoEcRQcLWddwXRRE",
            "starts_at": "2017-10-15T17:00:00.000Z"
        },
        {
            "id": 4662429128589312,
            "title": "hautnah! - Musikgeschichte(n) mit Sebastian Krumbiegel",
            "description": "Der Frontmann der „Prinzen“ gründete bereits in der Schule 1981 seine erste Band, kaufte sich vom eigenen Geld ein Schlagzeug und studierte an der Leipziger Musikhochschule. Er erzählt von seinem Leben zwischen Popband und Engagement gegen Rechts.",
            "google_place_id": "ChIJK8JQU-9Ip0cRFDaGuD-Fw1k",
            "starts_at": "2017-10-15T17:30:00.000Z"
        },
        {
            "id": 4637810107613184,
            "title": "Doppelkonzert: Giovanni Weiss & Django Deluxe",
            "description": "Das Giovanni Weiss-Quartett Django Deluxe steht ganz in der Tradition des großen Gypsy-Swing-Meisters Django Reinhardt. Neben den klassischen Sinti-Klängen ist Weiss jedoch auch beeinflusst von Musikern wie Wes Montgomery, George Benson und Pat Metheny",
            "google_place_id": "ChIJMRsSZcT5pkcRRW_wBP-MjpU",
            "starts_at": "2017-10-15T18:00:00.000Z"
        },
        {
            "id": 6356852245790720,
            "title": "Poetry Slam mit I-Slam",
            "description": "Ursprünglich als muslimische Version des Poetry Slams gestartet, sind neben Chemnitzer Slammern auch Künstler des Berliner Vereins I-Slam zu Gast. Vor dem Hintergrund des Empowerment-Gedanken setzen sie  klare Zeichen gegen Rassismus und Stereotypen.",
            "google_place_id": "ChIJQXmv10JGp0cROM6S5hB1AG8",
            "starts_at": "2017-10-15T18:00:00.000Z"
        }
    ],
    "cursor": "WzE1MDgwOTA0MDAsImV2ZW50IzYzNTY4NTIyNDU3OTA3MjAiXQ==",
    "request": {
        "limit": 5,
        "starts_at_min": "2017-10-15T15:00:00.000Z",
        "categories": [
            "!movie"
        ]
    },
    "timestamp": "2017-10-15T20:51:01.558Z"
}
```
