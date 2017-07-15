## dva中路由控制

> dva中路由控制大都是通过dva-router模块来完成， 少数时候回直接使用`window.location.href`来完成

#### 基于 action 进行页面跳转
```
  import { routerRedux } from 'dva/router';

  // Inside Effects
  yield put(routerRedux.push('/logout'));

  // Outside Effects
  dispatch(routerRedux.push('/logout'));

  // With query
  routerRedux.push({
    pathname: '/logout',
    query: {
      page: 2,
    },
  });
```
除 push(location) 外还有更多方法，详见 [react-router-redux](https://github.com/reactjs/react-router-redux#pushlocation-replacelocation-gonumber-goback-goforward)

```
export default {
  state: {
    isLogin: false,
    loginfail:false,
  },
  subscriptions: {
    setup({ dispatch, history }) {
      history.listen(location => {
        if (location.pathname.includes('app')) {
          dispatch({
            type: 'loginhook',
          });
        }
      });
    },
  },
    effects: {
    * login({ payload },{call, put}) {
      const { data } = yield call(login, payload);
      if (data && data.success) {    
        yield put({
                  type: 'checklogin',
                  payload:{
                    isLogin:true,
                  }
              });
        yield put(routerRedux.push('/app/users'));
      }else{
        yield put({
                    type: 'loginfail',
                    payload:{
                      loginfail:true,
                    }
                });
      }
    },

    * loginhook({ payload },{select,call, put}){
      const isLogin = yield select(({session}) => session.isLogin);
      console.log('logincheck',isLogin);
      if(isLogin === false){
        yield put((routerRedux.push('/login')));
      }

    },
  },
  reducers: {

    checklogin(state,action) {
      return {...state,isLogin:action.payload.isLogin };
    },

    loginfail(state,action) {
      return {...state, loginfail:action.payload.loginfail};
    },
  }
 }
```
以上内容来自[csdn-浪漫不属意](http://blog.csdn.net/ohmyauthentic/article/details/53543441)

#### 在route/下 基于 browserHistory  直接跳转

`import { browserHistory } from 'dva/router';`
`browserHistory.push(`/updatetask?taskId=${encodeURIComponent(e.currentTarget.id)}`);`

这个是根据index.js中使用的history方式来使用
`this.props.history.push(`/updatetask?taskId=${encodeURIComponent(e.currentTarget.id)}`);`



