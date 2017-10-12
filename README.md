The Eventer API
===============


Making a request
----------------

All URLs start with `http://api.my-eventer.de/v1/`. **(TODO: SSL only)**. The path is prefixed with the API version. If we change the API in backward-incompatible ways, we'll bump the version marker and maintain stable support for the old URLs.

Here's a simple example to grab some events:

```shell
curl -s http://api.my-eventer.de/v1/events
```


No XML, just JSON
-----------------

We only support JSON for serialization of data. Our format is to have no root element and we use snake\_case to describe attribute keys. This means that you have to send `Content-Type: application/json; charset=utf-8` when you're POSTing or PUTing data into Eventer.

You'll receive a `415 Unsupported Media Type` response code if you leave out the `Content-Type` header.

TODO: date formats


Pagination & Limit
------------------

Most collection APIs paginate their results. Normally you can specify a limit with the parameter `limit` which must be greater than 0 and lower than 101 (default: 10). If there are more results to paginate for you will get a `cursor` in the reposonse which can be used as parameter for the next request `&cursor=foo`, and so on until you get a response without cursor.


API ready for use
-----------------

* [Events](https://github.com/haed/eventer-rest-api/blob/master/endpoints/events.md)
* [Places](https://github.com/haed/eventer-rest-api/blob/master/endpoints/places.md)


API libraries
-------------

Coming soon..


Help us make it better
----------------------

Please tell us how we can make the API better. If you have a specific feature request or if you found a bug, please use GitHub issues. Fork these docs and send a pull request with improvements.

To talk with us and other developers about the API, [post a question on StackOverflow](http://stackoverflow.com/questions/ask) tagged `eventer`.
