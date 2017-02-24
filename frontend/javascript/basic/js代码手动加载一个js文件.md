## 有很多时候，我们需要自己主动去加载一个javascript文件
> 兼容ie
```
function loadScript(url, callback){
var script = document.createElement ("script")
script.type = "text/javascript";
if (script.readyState){ //IE
script.onreadystatechange = function(){
if (script.readyState == "loaded" || script.readyState == "complete"){
script.onreadystatechange = null;
callback();
}
};
} else { //Others
script.onload = function(){
callback();
};
}
script.src = url;
document.getElementsByTagName_r("head")[0].appendChild(script);
}
```
