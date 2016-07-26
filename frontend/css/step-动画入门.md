 ## step帧动画 
 ```
 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>step demo</title>
    <style>
    body {
        margin: 0;
        padding: 0;
    }
        .step {
            margin: 50px;
            height: 28px;
            width: 19px;
            background-image: url('cast.png');
            background-position: 0 0;
            background-size: 57px 28px;
            background-repeat: no-repeat;
            -webkit-animation: voiceplay .9s infinite steps(3, end);
            -o-animation: voiceplay .9s infinite steps(3, end);
            animation: voiceplay .9s infinite steps(3, end);
        }
    @-webkit-keyframes voiceplay {
        100% {
            background-position-x: -57px
        }
    }
    @keyframes voiceplay {
        100% {
            background-position-x: -57px
        }
    }

    </style>
</head>
<body>
    <div class="step"></div>
</body>
</html>

 ```
 > steps(3, end)  表示要3步完成动画   end ： 从最后开始 
 ```
    height: 28px;    高度 （ 如果 如果是竖直图则 宽为最大 ）
    width: 19px;     
    background-image: url('cast.png');
    background-position: 0 0;
    background-size: 57px 28px;  // 整个图的尺寸 
    background-repeat: no-repeat;
 ```
 
 
