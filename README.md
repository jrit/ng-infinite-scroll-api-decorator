# ng-infinite-scroll-api-decorator

Makes it easier to connect paged API responses to ngInfiniteScroll

## Use

### Initialization

```js
$scope.list = new infiniteScroll( urlString, apiService );
```

- `urlString` - url to the paged route with the token `{page}` which will be replaced with a number as each page is loaded. For example: `/users?p={page}`.
- `apiService` - Angular service that at a minimum has a `$get` method that take a url parameter and returns a promise where the resolved value includes a `data` object with a `results` array. This is intended to be [vokal-ng-api](https://github.com/vokal/vokal-ng-api) but any compatible interface should work.

```html
<tbody infinite-scroll="list.getNextPage()" infinite-scroll-distance="0"
    infinite-scroll-disabled="list.busy || list.hasMore === false">
    <tr data-ng-repeat="item in list.items">
        ...
    </tr>
</tbody>
```

The attributes shown are attributes of ngInfiniteScroll, but the values `list.busy`, `list.hasMore`, `list.getNextPage()`, and `list.items` are derived from infiniteScrollDecorator.

### API

#### `reload()`

Reinitialize paging. Empties item list and resets to first page.

#### `getNextPage()`

Loads the next page and appends items on callback.

#### `url` String

The paging url

#### `API` Service

The API service

#### `scope.items` Array

Currently loaded results

#### `page` Number

Current page index, start at 1

#### `busy` Boolean

Whether there is currently a pending XHR

#### `hasMore` Boolean

Whether there are more results available. This will default to `true` and change to `false` when no more results can be loaded.


## Prerequisites

- [ngInfiniteScroll](https://github.com/sroze/ngInfiniteScroll)

## Dependencies

- [toastr](https://github.com/CodeSeven/toastr) (may be removed in a future version), which has a dependency on jQuery
