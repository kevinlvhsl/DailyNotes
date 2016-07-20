## vue-resource demo

```
import Vue from 'vue'
import VueResource from 'vue-resource'
import App from 'common/app'
import { getCookie } from 'common/utils'

Vue.use(VueResource)

Vue.http.options.crossOrigin = true
Vue.http.options.emulateJSON = true
Vue.http.options.emulateHTTP = false
Vue.http.options.timeout = 15000
Vue.http.options.cache = false

Vue.http.interceptors.push((request, next) => {
  !request.params.hideLoading && App.showLoading()

  // debug
  if (App.isLocal) {
    request.params.mode = 'DEBUG'
    request.params.openid = 'o9lXxw281cUoP2_5iUCxUd7qqnPA'
  }
  next((response) => {
    if (response.status === 401) {
      // 干点啥
      const href = `${response.data.loginurl}?url=${location.href}`
      window.location.href = href
    } else if (response.status === 402) {
    // 干点啥
    } else if (response.status === 403) {
    // 干点啥
    }

    !request.params.hideLoading && App.hideLoading()
  })
})

const accessToken = getCookie('access_token')
if (accessToken) Vue.http.headers.common['Authorization'] = `WEIXIN ${accessToken}`

const host = App.isProd ? 'https://api.wx.yiheshanghai.com' : 'https://apitest.wx.yiheshanghai.com'

export const baseResource = Vue.resource(`${host}{/uri}`)
export const dataResource = Vue.resource(`${host}/users{/userId}{/uri}`)
export const devicesResource = Vue.resource(`${host}/devices{/deviceId}{/uri}`)
export const remindersResource = Vue.resource(`${host}/devices{/deviceId}/reminders`)
export const remindResource = Vue.resource(`${host}/devices{/deviceId}/reminders{/reminderId}`)
```
