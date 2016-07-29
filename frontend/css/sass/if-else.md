## if-else
 ```
 $time: morning;
a {
  @if $time == morning {
    color: red;
  } @else if $time == afternoon {
    color: blue;
  } @else {
    color: grey;
  }
}
 ```
  也可以在在里面进行赋值 
 ```
 @if $theme == 'blue'
    $success-wrapper-bgcolor: #fff
    $success-p-color: #1f456c
    $success-ptitle-color: #1f456c
 @if $theme == 'red'
    $success-wrapper-bgcolor: #f7f6f5
    $success-p-color: #cc311f
    $success-ptitle-color: #440404
 ```
