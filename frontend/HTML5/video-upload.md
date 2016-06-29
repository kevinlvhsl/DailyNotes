### HTMLM5 video 上传

在页面上传视频的难题： 视频一般都是比较大的， 如果通过base64来转码后再由ajax来传输的话，那基本会奔溃掉！
所以用另一种常用的方法 formData来上传。 
代码如下：(jade + vue + es6)
```
.i-video-bg
    input(
        v-if="!form.videoUrl",
        type="file"
        accept="video/*"
        @change="uploadVideo"
        id="video",
    )
    .uped-video(v-if="form.videoUrl")
        video(:src="form.videoUrl", controls="controls")
    .btn-del(v-if="form.videoUrl", @click="form.videoUrl = ''") 删 除
    
  //将参数封装成一个FormData，再来传送给后台
 uploadVideo(e){
    this.isloading = true
    let self = this
    let file = $('#video').get(0).files[0]
    let formData  = new FormData()
    formData.append("file", file)
    formData.append("act_id", 2)
    formData.append("file_type", 2)
    formData.append("file_id", 2)
    formData.append("file_desc", '123')
    console.log('------',file.size)
    var M = file.size / 1024 / 1024
    if(M > 20){
            App.pop('上传的视频不能超过20兆哦')
        return
    }
    App.ajax({
        url:'/yao/feature-api-files/userfile/upvideo',
        type: 'post',
        loading: false,
        data: formData,
        useFormData: true,
        success: ({meta, data})=> {
            if(meta.status === 200){
                self.$set('form.videoUrl', data.file_url)
                $('#video').val('')
                this.isloading = false
            }else{
                App.pop()
                this.isloading = false
            }
        },
        error: (d)=> {
            console.error(d)
            App.pop()
        }
    });
},
```
