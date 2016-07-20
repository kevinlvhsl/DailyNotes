##  vue-resource
--------
` npm install vue-resource`
or
`<script src="https://cdn.jsdelivr.net/vue.resource/0.9.3/vue-resource.min.js"></script>`
[Configuration](https://github.com/vuejs/vue-resource/blob/master/docs/config.md)
[HTTP Requests/Response](https://github.com/vuejs/vue-resource/blob/master/docs/http.md)
[Creating Resources](https://github.com/vuejs/vue-resource/blob/master/docs/resource.md)
[Code Recipes](https://github.com/vuejs/vue-resource/blob/master/docs/recipes.md)


### Configuration
Set default values using the global configuration.

Vue.http.options.root = '/root';
Vue.http.headers.common['Authorization'] = 'Basic YXBpOnBhc3N3b3Jk';
Set default values inside your Vue component options.

new Vue({

    http: {
      root: '/root',
      headers: {
        Authorization: 'Basic YXBpOnBhc3N3b3Jk'
      }
    }

})
> Webpack/Browserify

Add vue and vue-resource to your package.json, then npm install, then add these lines in your code:

`var Vue = require('vue');`
`var VueResource = require('vue-resource');`

`Vue.use(VueResource);`
Legacy web servers

> If your web server can't handle requests encoded as application/json, you can enable the emulateJSON option. This will send the request as application/x-www-form-urlencoded MIME type, as if from an normal HTML form.

`Vue.http.options.emulateJSON = true;`
> If your web server can't handle REST/HTTP requests like PUT, PATCH and DELETE, you can enable the emulateHTTP option. This will set  the X-HTTP-Method-Override header with the actual HTTP method and use a normal POST request.

`Vue.http.options.emulateHTTP = true;`

### HTTP
--------------

The http service can be used globally Vue.http or in a Vue instance this.$http.

Usage

A Vue instance provides the this.$http service which can send HTTP requests. A request method call returns a Promise that resolves to the response. Also the Vue instance will be automatically bound to this in all function callbacks.

new Vue({

    ready() {

      // GET /someUrl
      this.$http.get('/someUrl').then((response) => {
          // success callback
      }, (response) => {
          // error callback
      });

    }

})
Methods

> Shortcut methods are available for all request types. These methods work globally or in a Vue instance.

// global Vue object
`Vue.http.get('/someUrl', [options]).then(successCallback, errorCallback);`
`Vue.http.post('/someUrl', [body], [options]).then(successCallback, errorCallback);`

// in a Vue instance
`this.$http.get('/someUrl', [options]).then(successCallback, errorCallback);`
`this.$http.post('/someUrl', [body], [options]).then(successCallback, errorCallback);`
`this.$http.put('/someUrl', [body], [options]).then(successCallback, errorCallback);`
List of shortcut methods:
```
get(url, [options])
head(url, [options])
delete(url, [options])
jsonp(url, [options])
post(url, [body], [options])
put(url, [body], [options])
patch(url, [body], [options])
```

* Options

Parameter	Type	Description
url	string	URL to which the request is sent
method	string	HTTP method (e.g. GET, POST, ...)
body	Object, FormData string	Data to be sent as the request body
params	Object	Parameters object to be sent as URL parameters
headers	Object	Headers object to be sent as HTTP request headers
timeout	number	Request timeout in milliseconds (0 means no timeout)
before	function(request)	Callback function to modify the request options before it is sent
progress	function(event)	Callback function to handle the ProgressEvent of uploads
credentials	boolean	Indicates whether or not cross-site Access-Control requests should be made using credentials
emulateHTTP	boolean	Send PUT, PATCH and DELETE requests with a HTTP POST and set the X-HTTP-Method-Override header
emulateJSON	boolean	Send request body as application/x-www-form-urlencoded content type

> Response

> A request resolves to a response object with the following properties and methods:

| Method==|	Type	Description
+ text()	string	Response body as string
+ json()	Object	Response body as parsed JSON object
+ blob()	Blob	Response body as Blob object

> Property	Type	Description
+ ok	  boolean	HTTP status code between 200 and 299
+ status	number	HTTP status code of the response
+ statusText	string	HTTP status text of the response
+ headers	Object	HTTP headers of the response

 + Example
```
new Vue({

    ready() {

      // POST /someUrl
      this.$http.post('/someUrl', {foo: 'bar'}).then((response) => {

          // get status
          response.status;

          // get status text
          response.statusText;

          // get all headers
          response.headers;

          // get 'Expires' header
          response.headers['Expires'];

          // set data on vm
          this.$set('someData', response.json())

      }, (response) => {
          // error callback
      });

    }

})```


### Interceptors

> Interceptors can be defined globally and are used for pre- and postprocessing of a request.

#### Request processing
``` 
Vue.http.interceptors.push((request, next) => {

    // modify request
    request.method = 'POST';

    // continue to next interceptor
    next();
});```


#### Request and Response processing
```
Vue.http.interceptors.push((request, next)  => {

    // modify request
    request.method = 'POST';

    // continue to next interceptor
    next((response) => {

        // modify response
        response.body = '...';

    });
});```

#### Return a Response and stop processing
```
Vue.http.interceptors.push((request, next) => {

    // modify request ...

    // stop and return response
    next(request.respondWith(body, {
         status: 404,
         statusText: 'Not found'
    }));
});```



### Code Recipes
------

The Recipes provide code examples to common use-cases. If you want to share your recipe feel free to send a pull request.

Forms

+ Sending forms using FormData.
```
{
    var formData = new FormData();

    // append string
    formData.append('foo', 'bar');

    // append Blob/File object
    formData.append('pic', fileInput, 'mypic.jpg');

    // POST /someUrl
    this.$http.post('/someUrl', formData).then((response) => {
        // success callback
    }, (response) => {
        // error callback
    });
}
```
+ Abort a request

> Abort a previous request when a new request is about to be sent. For example when typing in a autocomplete input.
```
{
    // GET /someUrl
    this.$http.get('/someUrl', {

        // use before callback
        before(request) {

            // abort previous request, if exists
            if (this.previousRequest) {
                this.previousRequest.abort();
            }

            // set previous request on Vue instance
            this.previousRequest = request;
        }

    }).then((response) => {
        // success callback
    }, (response) => {
        // error callback
    });
}```
