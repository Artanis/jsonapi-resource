# jsonapi-resource

An element that reads a [JSON API](https://jsonapi.org) endpoint.

## Installation

*This package has not yet been published to bower. Please install from Github directly.*

    bower install https://github.com/Artanis/jsonapi-resource.git#0.1.0

## Usage

This component makes a request to a JSON API endpoint. The data returned by the endpoint is deserialized with [simple-jsonapi](https://github.com/Artanis/simple-jsonapi), and the primary data (an array for collections, a single object for single resources) is exposed through the `documents` parameter.

    <jsonapi-resource
      url="http://example.com/api/articles"
      documents="{{docs}}"
      origin="{{origin}}"></jsonapi-resource>

    <template is="dom-repeat" items="{{docs}}">
      <jsonapi-resource
        url="{{item.comments._links.related}}"
        origin="{{origin}}"></jsonapi-resource>
    </template>

* `url` and `origin` are a pair. An absolute URL can be given, which will be used to populate `origin`, or `url` can be a relative path and `origin` is required (this will cause `url` to be rewritten to be absolute). Requests will only be made to an absolute URL.
* `params` is passed wholesale to [`<iron-ajax>`](https://elements.polymer-project.org/elements/iron-ajax">PolymerElements/iron-ajax).
* `documents` is the deserialized primary data from the response. Included documents are available on their respective relationship attributes.
* `links` and `meta` are both the raw response-level `links` and `meta` objects.
