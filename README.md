# axios [![Build Status](https://travis-ci.org/mzabriskie/axios.svg?branch=master)](https://travis-ci.org/mzabriskie/axios)

Promise based XHR library

## Features

- Making [XMLHttpRequests](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) supporting the [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) API
- Transforming request and response data
- Client side support for protecting against [XSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery)
- Specifying HTTP request headers
- Automatic transforms for JSON data

## Installing

Using bower:

```bash
$ bower install axios
```

Using npm:

```bash
$ npm install axios
```

## Compatability

Tested to work with >=IE8, Chrome, Firefox, Safari, and Opera.

## Example

Performing a `GET` request

```js
// Make a request for a user with a given ID
axios.get('/user?ID=12345')
	.then(function (response) {
		console.log(response);
	})
	
// Optionally the request above could also be done as
axios.get('/user', {
		params: {
			ID: 12345
		}
	})
	.then(function (response) {
		console.log(response);
	})
```

Performing a `POST` request

```js
axios.post('/user', {
		firstName: 'Fred',
		lastName: 'Flintstone'
	})
	.then(function (response) {
		console.log(response);
	})
```

Aliases are provided for success and error

```js
axios.get('/user/12345')
	.success(function () {
		console.log('user found');
	})
	.error(function () {
		console.log('error finding user');
	});
```

## Request API

Requests can be made by passing the relevant config to `axios`.

##### axios(config)

```js
axios({
	method: 'get',
	url: '/user/12345'
});
```

### Request method aliases

For convenience aliases have been provided for all supported request methods.

##### axios.get(url[, config])
##### axios.delete(url[, config])
##### axios.head(url[, config])
##### axios.post(url[, data[, config]])
##### axios.put(url[, data[, config]])
##### axios.patch(url[, data[, config]])

###### NOTE
When using the alias methods `url`, `method`, and `data` properties don't need to be specified in config.

### Config

This is the available config options for making requests. Only the `url` is required. Requests will default to `GET` if `method` is not specified.

```js
{
	// `url` is the server URL that will be used for the request
	url: '/user',
	
	// `method` is the request method to be used when making the request
	method: 'get', // default
	
	// `transformRequest` allows changes to the request data before it is sent to the server
	// This is only applicable for request methods 'PUT', 'POST', and 'PATCH'
	transformRequest: [function (data) {
		// Do whatever you want to transform the data
		
		return data;
	}],
	
	// `transformResponse` allows changes to the response data to be made before
	// it is passed to the success/error handlers
	transformResponse: [function (data) {
		// Do whatever you want to transform the data
		
		return data;
	}],
	
	// `headers` are custom headers to be sent
	headers: {'X-Requested-With': 'XMLHttpRequest'},
	
	// `param` are the URL parameters to be sent with the request
	params: {
		ID: 12345
	},
	
	// `data` is the data to be sent as the request body
	// Only applicable for request methods 'PUT', 'POST', and 'PATCH'
	data: {
		firstName: 'Fred'
	},
	
	// `withCredentials` indicates whether or not cross-site Access-Control requests
	// should be made using credentials
	withCredentials: false, // default
	
	// `responseType` indicates the type of data that the server will respond with
	// options are 'arraybuffer', 'blob', 'document', 'json', 'text'
	responseType: 'json', // default
	
	// `xsrfCookieName` is the name of the cookie to use as a value for xsrf token
	xsrfCookieName: 'XSRF-TOKEN', // default
	
	// `xsrfHeaderName` is the name of the http header that carries the xsrf token value
	xsrfHeaderName: 'X-XSRF-TOKEN' // default
}
```

## Response API

For either `success` or `error`, the following response will be provided.

```js
axios.get('/user/12345')
	.success(function (
		// `data` is the response that was provided by the server
		data,
		
		// `status` is the HTTP status code from the server response
		status,
		
		// `headers` the headers that the server responded with
		headers,
		
		// `config` is the config that was provided to `axios` for the request
		config
		) {
		// Do something with result
	});
}
```

## Credits

axios is heavily inspired by the [$http service](https://docs.angularjs.org/api/ng/service/$http) provided in [Angular](https://angularjs.org/). Ultimately axios is an effort to provide a standalone `$http`-like service for use outside of Angular.

axios uses the [es6-promise](https://github.com/jakearchibald/es6-promise) polyfill by [Jake Archibald](https://github.com/jakearchibald). Until we [can use](http://caniuse.com/promises) ES6 Promises natively in all browsers, this polyfill is a life saver.

## License

MIT