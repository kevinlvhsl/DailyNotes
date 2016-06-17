### input上传手机图片，并且声称预览缩略图，不喜欢，点击可以删除、

```
    .i-input-bg
            .thumb(:class="{'po-top': !!thumbImgs[0]}", @click="removeImg(0)")
                img(:src="thumbImgs[0]")
            input.i-input-bg(
                type="file"
                accept="image/jpeg"
                @change="getImage"
                id="img0",
            )

```
js
```
// 移出图片（利用双向绑定）
removeImg(index){
            this.$set('thumbImgs[' + index+ ']', null)
            this.$set('imgs[' + index+ ']', null)
            if (!this.imgs[0] && !this.imgs[1]) {
                this.uploaded = false
            }
        },
// 将选中的图片转成dataURL
getImage(e){
        let file = e.target.files[0]
        let id = e.target.id.split('img')[1]
        let thumb = $(e.target).prev()
        let self = this
            console.log(file)
            var fr = new FileReader()
            fr.onload = function(){
                var dataURL = this.result
                let img = new Image()
                img.src = this.result
                img.onload = ()=>{
                    let thumbImg = self.drawThumbImg(img, 146, 146)
                    self.$set('thumbImgs['+ id + ']', thumbImg)
                    // thumb.find('img').attr('src', self.thumbImgs[id])
                    self.imgs[id] = self.drawThumbImg(img, img.width, img.height)
                    self.uploaded = true
                }
            }
            fr.readAsDataURL(file)
        },
// 画缩略图 接受缩略的尺寸大小
        drawThumbImg(img, cavsW, cavsH){
            let cavs = document.createElement('canvas')
            cavs.width = cavsW
            cavs.height = cavsH
            cavs.fillStyle = '#fff'
            let ctx = cavs.getContext('2d')
            ctx.fillRect(0, 0, cavsW, cavsH)
            ctx.drawImage(img, 0, 0, cavsW, cavsH)
            return cavs.toDataURL('image/jpeg', .7)
        },
```

微信访问 [http://devstatic.myintv.com.cn/yao/jsws/wmyql/index.dev.html](http://devstatic.myintv.com.cn/yao/jsws/wmyql/index.dev.html)

注意图片与 input的上下层叠关系。 缩略图生成以前，是input在上， 生成以后，是图片在上



