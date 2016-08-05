##  leancloud- relatime 做即时通讯 
[https://leancloud.cn/docs/realtime_guide-js.html](https://leancloud.cn/docs/realtime_guide-js.html)
 以上是文档地址；
> 大致流程
-- 注册
    -- 先在leancloud上注册或购买账号、然后登陆后创建一个应用，拿到当前应用的appId
-- 安装
    -- 在你的应用代码中 安装leancloud-realtime的node包或者js文件
-- 使用 
    + 在页面中引用所需要的组件 RealTime
    `import { Realtime, TextMessage } from 'leancloud-realtime'`
    ```const realtime = new Realtime({
        appId: 'kR3hoBNiAnhTlWq5PUTfpBzm-gzGzoHsz', // 珠江公众号 appid
        region: 'cn',

        // 这里是官方代码在浏览器中直接加载时，SDK 暴露的所有的成员都挂载在 AV 命名空间下
        var Realtime = AV.Realtime;
        var realtime = new Realtime({
          appId: 'bSVRPHEG1elv2lN4R0PBlpAm-gzGzoHsz',
          region: 'cn', // 美国节点为 "us"
        });
    })```
    + 然后创建房间、并初始化房间
        let Conversation
        let messageIterator
        let Client = {}
        ```
            initConversation () {
                this.roomId = 'zhujiang' // `${App.userInfo.device_id}`
                this.clientId = 'zhujiang' // `${App.userInfo.wx_user}`
                App.pop2('加入房间中...', 10000)
                realtime.createIMClient(this.clientId).then(client => {
                Client = client
                client.on('message', message => {
                  App.log('收到消息')
                  App.log(message)
                  this.addToList(this.messageToList(message))
                })
                return client.getQuery().equalTo('name', this.roomId).find()
                }).then(conversations => {
                const room = conversations.find(conversation => conversation._name === this.roomId)
                console.log(conversations)
                if (room) return Client.getConversation(room.id)
                // 房间不存在 创建
                return Client.createConversation({
                  name: this.roomId,
                  members: [],
                })
                })
                .then(conversation => conversation.join())
                .then(conversation => {
                  Conversation = conversation
                  messageIterator = conversation.createMessagesIterator({ limit: 4 })
                  this.loadPrev()
                  App.hidePop()
                  App.pop('成功加入房间', 500)
                  App.log(`用户:${this.clientId} 加入房间: ${conversation._name}`)
                })
                }
        ```
  
        + 以下是一些交互的方法
        ```
          scrollBottom () {
            this.$broadcast('scroller:reset', this.$refs.scroll.uuid)

            const xscroll = this.$refs.scroll._xscroll
            xscroll.scrollTo(0, xscroll.containerHeight - xscroll.height, 300, 'ease')
          },
          fixScrollTop () {
            if (App.isIos) {
              setTimeout(() => { document.body.scrollTop = document.body.clientHeight }, 100)
            } else {
              if (!this.inputType) setTimeout(() => { document.body.scrollTop = 0 }, 100)
            }

            this.scrollBottom()
          },
          messageToList (message, has_read = false) {
            return {
              has_read,
              sender_type: 1,
              id: message.id,
              from: message.from,
              content: message.text,
              length: message.attributes.length,
              msg_type: message.attributes.msg_type,
              label: message.from === this.clientId ? '我' : message.attributes.label,
              headimgurl: message.attributes.headimgurl,
              isMe: message.from === this.clientId,
              isPlay: false
            }
          },
          addMessagePrevList (list) {
            const localList = []

            list.forEach((v, k) => {
              localList.push(this.messageToList(v, true))
            })
            this.list.unshift(...localList)
          },
          loadPrev (uuid) {
            if (this.loadPrevState || !messageIterator) return
            this.loadPrevState = true

            // 第一次调用 next 方法，获得前 10 条消息，还有更多消息，done 为 false
            messageIterator.next().then(res => {
              if (res.done) {
                App.log(res.value)
                this.addMessagePrevList(res.value)
                this.$nextTick(() => {
                  this.$broadcast('pulldown:disable', uuid)
                  this.$broadcast('scroller:reset', uuid)
                  this.$refs.scroll._xscroll.scrollTop()
                  this.loadPrevState = false
                })

                return
              }

              this.addMessagePrevList(res.value)
              this.$nextTick(() => {
                this.$broadcast('pulldown:reset', uuid)
                this.$broadcast('scroller:reset', uuid)
                this.$refs.scroll._xscroll.scrollTop()
                this.loadPrevState = false
              })
            })
          },
          sendMessage(obj) {
            const textMsg = new TextMessage(obj.content)
            const accessToken = getCookie('access_token')
            const attr = {
              headimgurl: App.userInfo.headimgurl,
              label: App.userInfo.label,
              msg_type: obj.msg_type,
              length: obj.length,
              token: accessToken
            }

            textMsg.setAttributes(attr)
            Conversation && Conversation.send(textMsg).then(res => {
              App.log(res)
            })
          },
          sendText () {
            const msg = this.msg
            if (msg === '') {
              App.pop('请输入聊天内容', 800)
              return
            }

            const obj = {
              sender_type: 1,
              sender: App.userInfo.wx_user,
              msg_type: 2,
              content: msg,
              isMe: true,
              label: '我',
              headimgurl: App.userInfo.headimgurl
            }

            this.addToList(obj)
            this.sendMessage(obj)
            this.$els.input.blur()
            this.msg = ''
          },
          addToList (obj) {
            if (this.list.length >= this.maxListLength) {
              this.list = this.list.splice(-this.maxListLength)
            }

            this.list.push(obj)
            this.$nextTick(() => {
              this.$broadcast('scroller:reset', this.$refs.scroll.uuid)

              const xscroll = this.$refs.scroll._xscroll
              const maxY = xscroll.containerHeight - xscroll.height
              const scrolly = Math.abs(xscroll.y)

              if (maxY - scrolly < xscroll.height / 2) {
                xscroll.scrollTo(0, xscroll.containerHeight - xscroll.height, 300, 'ease')
              }
            })
          },
        ```
        + html代码
        ```
          .chat(v-el:chat)
            scroller(
              v-ref:scroll,
              lock-x,
              scrollbar-y,
              use-pulldown,
              height='100%',
              :pulldown-config="{content:'下拉刷新',downContent:'下拉刷新',upContent:'释放加载',loadingContent:'加载中'}",
              @pulldown:loading='loadPrev',
            )
              .warp
                .msg(v-for="msg in list", transition="fadeInUp")
                  .con(:class="{me: msg.isMe}")
                    .ava(:style="{backgroundImage: 'url('+msg.headimgurl+')'}")
                    .name {{msg.label}}
                    .text {{msg.content}}
          .foot
            input.input(
              v-el:input
              type="text"
              placeholder='说点什么~'
              maxlength="30"
              v-model="msg"
              @click="fixScrollTop"
            )
            a.send-btn(@click="sendText") 发送
        ```






