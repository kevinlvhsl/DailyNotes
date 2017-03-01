## php中的类 对象


```
 <?php
 class Site {
     /* 成员变量 */
     var $url;
     var $title;
 
     /* 成员函数 */
     function setUrl($par){
         $this->url = $par;
     }
 
     function getUrl(){
         echo $this->url ."<br/>";
     }
 
     function setTitle($par){
         $this->title = $par;
     }
 
     function getTitle(){
         echo $this->title . "<br/>";
     }
 }?>
```

