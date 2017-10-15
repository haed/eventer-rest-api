# /events
-------------------

Use this endpoint to search for events.

Examples
* `GET /v1/events?area=50.838948,12.912577,50.827132,12.933774` will return events from the inner city of Chemnitz.
* `GET /v1/events?categories=movie` will return only movies.
* `GET /v1/events?categories=!movie` will return events which are not movies.
* `GET /v1/events?search=Party` will search for "Party" events.

All returned events will be primarily sorted by `event.starts_at` timestamps.

Request parameters
------------------

parameter | description
--------- | -----------
`starts_at_min` | The minimum starts-at timestamp for events. If not given the default value will be *now*.
`starts_at_max` | The maximum starts-at timestamp for events.
`area` | Restricts the event search to a geolocation rectangle specified by 4 comma separated coordinates: top (latitude), left (longitude), bottom (latitude) and right (longitude). <br/><br/>Example value for the inner city of Chemnitz: `50.838948,12.912577,50.827132,12.933774`.
`categories` | A comma separated list of event categories to search for (not all events are categorized yet). If not specified all events of all categories (or without category) will be returned.<br/><br/>Note: also you can exclude categories from the result by using `!` as a category suffix.<br/><br/>Currently the following categories are supported: <ul><li>movie</li></ul>
`google_place_ids` | blah
`search` | blah
`updated_since` | blah
`limit` | blah
`cursor` | blah
