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


###  以上方法是用canvas的drawImage来渲染图片， 并将数据转成base64字符串后传送的后台。 此接口不宜传输较大的图片。
> 此外还有一个直接存储线上文件的方法：先将文件通过特定接口上传到cdn，返回图片线上地址
```
// 缩略图默认是在input下，图片上传成功后就将缩略图置顶，点击的时候就直接点击缩略图删除，删除后input又为空了，且在上面可以点击选取文件
.i-input-bg
    .thumb(:class="{'po-top': !!thumbImgs[0]}", @click="removeImg(0)", inas_seed="xwpt_addTopic_remove_img1")
        img(:src="thumbImgs[0]", v-if="thumbImgs[0]")
    input(
        type="file"
        accept="image/jpeg"
        @change="uploadImg"
        id="img0",
        inas_seed="xwpt_addTopic_add_img1"
    )
// 上传图片方法
    uploadImg(e){
        this.isloading = true           // 加loading遮罩
        let self  = this,
            file   = e.target.files[0], // 获取到文件
            reader = new FileReader(),
            img    = new Image(),
            imgData,
            index = e.target.id.split('img')[1]
        reader.readAsDataURL(file)
        reader.onload = function(){
            img.src = this.result
            img.onload = function(){
                imgData = ImgMin.compressWithRatio(img, { // 此处是canvas压缩插件
                    maxWidth: 320,
                    maxHeight: 320,
                    quality: .6
                })
                App.ajax({
                    url:'/yao/feature-api-image/image/upload',  // 上传到七牛云
                    type: 'POST',
                    loading: false,
                    data: {'img': imgData},
                    success: ({meta, data})=> {
                        console.log(meta, data)
                        if (meta.status === 200) {
                            self.isloading = false
                            self.form.imgs[index] = data.data           // 给图片地址赋值为云地址
                            let thumbImg = self.drawThumbImg(img, 146, 146)
                            self.$set('thumbImgs['+ index + ']', thumbImg)
                        }
                    },
                    error: (d)=> {
                        this.isloading = true
                        console.error(d)
                        App.pop('上传图片失败，请稍候再试')
                    }
                });
            };
        };
    },
```


 
// 上传图片的时候会有一些坑， 横图上传上去 可以， 但是竖图就会变成横图了！ 所以需要在 上传 上传的时候  判断 判断一下是横图还是竖直图，
 ### [exif.js](https://github.com/exif-js/exif-js)
可以判断图片的方向 ，
```
<div class="container">
            <h1>Camera API</h1>

            <section class="main-content">
                <p>A demo of the Camera API, currently implemented in Firefox and Google Chrome on Android. Choose to take a picture with your device's camera and a preview will be shown through createObjectURL or a FileReader object (choosing local files supported too).</p>

                <p>
                    <form method="post" enctype="multipart/form-data" action="index.php">
                        <input type="file" id="take-picture" name="image" accept="image/*">
                        <input type="hidden" name="action" value="submit">
                        <input type="submit" >
                    </form>
                </p>

                <h2>Preview:</h2>
                <div style="width:100%;max-width:320px;">
                    <img src="about:blank" alt="" id="show-picture" width="100%">
                </div>

                <p id="error"></p>
                <canvas id="c" width="640" height="480"></canvas>
            </section>

        </div>


        <script>
            (function () {
                var takePicture = document.querySelector("#take-picture"),
                    showPicture = document.querySelector("#show-picture");

                if (takePicture && showPicture) {
                    // Set events
                    takePicture.onchange = function (event) {
                        showPicture.onload = function(){
                            var canvas = document.querySelector("#c");
                            var ctx = canvas.getContext("2d");
                            ctx.drawImage(showPicture,0,0,showPicture.width,showPicture.height);
                        }
                        // Get a reference to the taken picture or chosen file
                        var files = event.target.files,
                            file;
                        if (files && files.length > 0) {
                            file = files[0];
                            try {
                                // Get window.URL object
                                var URL = window.URL || window.webkitURL;

                                // Create ObjectURL
                                var imgURL = URL.createObjectURL(file);

                                // Set img src to ObjectURL
                                showPicture.src = imgURL;

                                // Revoke ObjectURL
                                URL.revokeObjectURL(imgURL);
                            }
                            catch (e) {
                                try {
                                    // Fallback if createObjectURL is not supported
                                    var fileReader = new FileReader();
                                    fileReader.onload = function (event) {
                                        showPicture.src = event.target.result;

                                    };
                                    fileReader.readAsDataURL(file);
                                }
                                catch (e) {
                                    // Display error message
                                    var error = document.querySelector("#error");
                                    if (error) {
                                        error.innerHTML = "Neither createObjectURL or FileReader are supported";
                                    }
                                }
                            }
                        }
                    };
                }
            })();
        </script>
```


exif.js 还有很多很多功能  详情 详情见 详情见官网 
 [查看器](https://exif.cn/)
#### example  https://exif.cn/ 
 ```
 File
FileType	JPEG
FileTypeExtension	jpg
MIMEType	image/jpeg
ImageWidth	308
ImageHeight	177
EncodingProcess	Baseline DCT, Huffman coding
BitsPerSample	8
ColorComponents	3
YCbCrSubSampling	YCbCr4:2:0 (2 2)
JFIF
JFIF版本	1.01
分辨率单位	inches
X轴分辨率	96
Y轴分辨率	96
Composite
图像尺寸	308x177
Megapixels	0.055
 ```






