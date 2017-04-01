## react的数据状态管理--redux
redux是数据流flux思想的一个实现，被官方承认的、比较好的实现方案  
对比vuejs 的vuex（store、actions、mutation、state）
store 由reducer 和 state 组成
  state是 应用的一些数据状态
  reducer 操作数据的纯方法， 由action来触发
action： 是由界面触发调用的方法（函数）， 方法返回一个对象、对象中有一个type字段(必须)

[中文文档](http://cn.redux.js.org/index.html)

> Redux 是 JavaScript 状态容器，提供可预测化的状态管理。

> 一个超级简单的app容器组件，里面一个header组件 一个列表 和一个footer组件
```
import React from 'react'
import { connect } from 'react-redux'
import { setVisibilityFilter } from '../actions';
import Header from '../components/header'
import Footer from '../components/footer'

class App extends React.Component {

  render () {
    // App 接收 state 映射后的对象obj中的属性和 dispatch 传递给子组件
    const { dispatch, visibilityFilter } = this.props
    console.log('props中的filter', visibilityFilter)
    return (
      <div className="container">
        <h1>这里是TODO List管理</h1>
        <Header />
        <Footer
          filter={visibilityFilter}
          onFilterChange={
            (status) => {
              console.log('状态status', status)
              dispatch(setVisibilityFilter(status))
            }
        }/>
      </div>
    )
  }
}
/**
 * mapStateToProps 映射state
 *
 * @param  state  [store里的state]
 * @return object [返回一个对象，把对象里面的参数以属性传送给App，以及附带一个 dispatch]
 */
const select = (state) => {
  return {
    visibilityFilter: state.visibilityFilter
  }
}
export default  connect(select)(App)

```

> header组件
```
import React from 'react'

class Header extends React.Component {
  hanldeClick (e) {
    const node = this.refs.input
    const text = node.value.trim()
    console.log('您输入的是：', text)
  }
  render () {
    return (
      <div className="head-bar">
        <input ref="input" placeholder="请输入代办项" />
        <button onClick={ (e) =>{
          this.hanldeClick(e)
          e.preventDefault()
        }}> 添 加
        </button>
      </div>
    )
  }
}

export default Header

```

> footer 组件
```
import React, { PropTypes } from 'react'

class Footer extends React.Component {
  renderFilter (filter, name) {
    return (
      <a href="#"
        className={this.props.filter === filter ? 'active' : ''}
      onClick={
        (e) => {
          this.props.onFilterChange(filter)
        }
      }>{name}</a>
    )
  }
  render () {
    console.log('active:', this.props.filter)
    return (
      <div className="foot-bar">
        <p>
          展示：
          <span>  </span>
          { this.renderFilter('ALL', '全部') }
          <span> | </span>
          { this.renderFilter('ACTIVE', '进行中') }
          <span> | </span>
          { this.renderFilter('COMPLETED', '已完成') }
        </p>
      </div>
    )
  }
}

Footer.propTypes = {
  onFilterChange: PropTypes.func.isRequired,
  filter: PropTypes.oneOf([
    'ALL',
    'ACTIVE',
    'COMPLETED'
  ]).isRequired
}

export default Footer

```
