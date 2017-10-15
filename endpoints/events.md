# /events
---------

Use this endpoint to search for events. This endpoint supports [GET and POST requests](https://github.com/haed/eventer-rest-api/blob/master/README.md#getpost-methods).

Examples:
* `GET /v1/events?area=50.838948,12.912577,50.827132,12.933774` will return events from the inner city of Chemnitz.
* `GET /v1/events?categories=movie` will return only movies.
* `GET /v1/events?categories=!movie` will return events which are not movies.
* `GET /v1/events?search=Party` will search for "Party" events.

All returned events will be primarily sorted by `event.starts_at` timestamps.


## Request parameters
---------------------

parameter | description
--------- | -----------
`starts_at_min` | The minimum starts-at timestamp for events. If not given the default value will be *now*.
`starts_at_max` | The maximum starts-at timestamp for events.
`area` | Restricts the event search to a geolocation rectangle specified by 4 comma separated coordinates: top (latitude), left (longitude), bottom (latitude) and right (longitude). <br/><br/>Example value for the inner city of Chemnitz: `50.838948,12.912577,50.827132,12.933774`.
`categories` | A comma separated list of event categories to search for (not all events are categorized yet). If not specified all events of all categories (or without category) will be returned.<br/><br/>Note: also you can exclude categories from the result by using `!` as a category suffix.<br/><br/>Currently the following categories are supported: <ul><li>movie</li></ul>
`google_place_ids` | A comma separated list of ids of google places to restrict search to events from these places only.<br/><br/>You can use the google maps api to search for google place ids: [google place id finder](https://developers.google.com/maps/documentation/javascript/examples/places-placeid-finder)
`search` | Searches events by a free text search.
`updated_since` | If set only events will be returned which has been added or modified since the given timestamp. Can be used for synchronization and fetch scenarios.
`limit` | Sets the limit for count of events whcih should be returned. Limit must be greater than 0 and lower than 101. If not set a the default limit will be 10.
`cursor` | Continues a search by "offest" specified by this cursor. Any event search could return a cursor which represents an offset to paginate to the following events. To use a cursor you have the re-run the request with same parameters but with the given cursor value to retrieve the next events of your search behind the limit.
