## vue-touch
今天要用到一个长按的动作， 第一时间想起了vue-touch， 
vue-touch 是在hammer.js基础上封装的。 
### press
长按： 
```
  const record = document.getElementById('btn-record')
    const mc = new Hammer(record)
    let interval = null
    mc.on('press', (ev) => {
      App.log('按下了record按钮')
      this.record = 0
      interval = setInterval(() => {
        App.log(this.record++)
      }, 1000)
    })
    mc.on('pressup', (ev) => {
      if (this.record <= 2) {
        App.pop2('录音时间太短')
        wx.stopRecord()
      } else {
        App.log(this.record)
        wx.stopRecord({
          success: (res) => {
            App.log('结果', res)
            self.localId = res.localId
          }
        })
      }
      App.log('抬起了record按钮')
      clearInterval(interval)
    })
```
