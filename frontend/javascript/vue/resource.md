##  vue-resource
--------
` npm install vue-resource`
or
`<script src="https://cdn.jsdelivr.net/vue.resource/0.9.3/vue-resource.min.js"></script>`
[Configuration](https://github.com/vuejs/vue-resource/blob/master/docs/config.md)
[HTTP Requests/Response](https://github.com/vuejs/vue-resource/blob/master/docs/http.md)
[Creating Resources](https://github.com/vuejs/vue-resource/blob/master/docs/resource.md)
[Code Recipes](https://github.com/vuejs/vue-resource/blob/master/docs/recipes.md)

Set default values inside your Vue component options.

new Vue({

    http: {
      root: '/root',
      headers: {
        Authorization: 'Basic YXBpOnBhc3N3b3Jk'
      }
    }

})
W
