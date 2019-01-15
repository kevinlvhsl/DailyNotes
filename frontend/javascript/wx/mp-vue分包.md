## 微信小程序分包(mpvue)

使用mpvue分包示例：
1、下载vue脚手架（先有node环境，v8.12.0）
```bash
npm install -g vue-cli
```
2、先用vue初始化一个mpvue小程序项目(一路按步骤走下去)
```bash
vue init mpvue/mpvue-quickstart mp-fenbao
cd mp-fenbao
npm install
npm run dev
```
注意：这里使用的版本时 `"mpvue : v1.0.11"`、`"mpvue-loader":  "v1.1.2" ` ` "webpack-mpvue-asset-plugin": "^0.1.2",`
如果发现版本比这个低很多，那可能你需要去看一下官方提供的手动升级方案了。[官方issue](https://github.com/Meituan-Dianping/mpvue/issues/672)
如果你的版本没问题，那到这里，一个基本的小程序项目就起起来了。

3、改造代码目录和配置（重点）
根据小程序[官方的教程](https://developers.weixin.qq.com/miniprogram/dev/framework/subpackages/basic.html)配置下来, 可能在mpvue中会行不通。 因为他们的代码目录结构是不一样的。尤其是mpvue是要编译后。

琢磨了一阵之后，终于找到了正确的方案：(如图)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181221111826493.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTE0MDEzOTA=,size_16,color_FFFFFF,t_70)
>几个注意的点 
>1、首先要把子包的目录建在src/pages/ 下，而不是官方的平级。
>2、子包目录下还需要建一个pages/ 的目录，然后下面才是你的页面目录。
>3、app.json中的配置如上图所示就可以了
```
		{
			"pages": [
			        "pages/index/main",
			        "pages/logs/main"
			    ],
			    "subPackages": [{
			        "root": "pages/myMO/",
			        "pages": [
			            "counter/main"
			        ]
			    },{
		            "root": "pages/OPKG/",
		            "pages": [
		                "logs2/main"
		            ]
		        }
		 ],
		}
		// ** 根目录的pages中，配置的是主包的页面（一般就是你的tabbar里面的页面）
		// ** 分包配置 多个分包就在subPackages下建多个对象
		// ** 最重要的一点： root对应的配置一定要是 "pages/myMO/" 。  
		// myMO就是你的分包名，随便取。 最后的 / 不能省略，否则会报 subPackages[0].root 必须为 目录 这个错
```	

 4、到这里， 重启`npm run dev` 应该就能跑起你的项目了
 如果看到了一下图示结果，就表示分包没问题了。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/2018122111194524.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTE0MDEzOTA=,size_16,color_FFFFFF,t_70)
 有一点注意的： 就是改变目录结构以后， 记得清理dist下的文件， 然后重新` npm run dev `  免得被旧代码影响。
