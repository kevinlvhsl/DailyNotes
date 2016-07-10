## 响应式布局的年代必不可少css横竖屏判断

```
@media screen and (orientation: landscape){
    .test::after {
        content: "横屏";
    }
}
@media screen and (orientation: portrait){
    .test::after {
        content: "竖屏";
    }
}
```

### demo
```
<!DOCTYPE html>
<html lang="zh-cmn-Hans">
<head>
<meta charset="utf-8" />
<title>media features orientation_CSS判断横竖屏</title>
<meta name="author" content="Joy Du(飘零雾雨), dooyoe@gmail.com, www.doyoe.com" />
<style>
.test::after {
    color: red;
}
@media screen and (orientation: portrait){
    .test::after {
        content: "竖屏";
    }
}
@media screen and (orientation: landscape){
    .test::after {
        content: "横屏";
    }
}
</style>
</head>
<body>
<div class="test">你现在是：</div>
</body>
</html>
```
