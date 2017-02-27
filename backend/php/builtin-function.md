### php中有很多内置的函数

+ 第一个当然是echo()
> 其实echo 可以直接不加括号就使用，但它也是一个函数 
  参数为要输出的内容
 
+ var_dump()
> 用来查看变量的数据类型和值
  参数为变量

+ empty()
> 查看变量是否为 NULL， 为null则返回ture 否则返回false
  参数为变量

+ unset()
> 将变量置为NULL 返回

+ inset()
> isset()可以向括号中间传入一个或者多个变量，变量与变量间用逗号分开。只要有有一个变量为null，则返回false。否则，则返回true。

+ strlen() 函数
> 故名思议，就是求字符串的长度。函数返回字符串的长度（字符数）。
注意：在UTF-8下 strlen  把中文字符算成 3 个字节，英文，空格，符号占 1 个字节。
提示：strlen() 常常用在循环和其他函数中，因为那时确定字符串何时结束是很重要的。（例如，在循环中，我们需要在字符串中的最后一个字符之后结束循环。）

+ strpos() 函数
> strpos函数 用于在字符串内查找一个字符或一段指定的文本。 类似于indexOf
  如果在字符串中找到匹配，该函数会返回第一个匹配的字符位置。如果未找到匹配，则返回 FALSE。


+ header
> header("Content-type:text/html;charset=utf-8");
  用来 定义文档的类型和字符集编码


+ define 设置 PHP 常量
> define("GREETING", "欢迎访问 php.cn");   它使用三个参数：
  1.   首个参数定义常量的名称
  2.   第二个参数定义常量的值
  3.   可选的第三个参数规定常量名是否对大小写敏感。默认是 false。
```
<?php
header("Content-type:text/html;charset=utf-8");
define("GREETING", "欢迎访问 php.cn");
function myTest() {
 echo GREETING;
}
myTest(); // 输出 "欢迎访问 php.cn"
?>
```
>   常量名	       说明 
    LINE	      当前所在的行
    FILE	      当前文件在服务器的路径
    FUNCTIOIN	  当前函数名
    CLASS	      当前类名
    METHOD	    当前成员方法名
    PHP_OS	    PHP运行的操作系统
    PHP_VERSION	当前PHP的版本
    TRAIT	Trait 的名字,php5.4新加
    DIR       	文件所在的目录
    NAMESPACE	  当前命名空间的名称（区分大小写）

### 数组排序函数

+ sort() - 对数组进行升序排列
> 注：sort大多是用来排序数字索引数组的，如果把一个关联数组放到sort里排序，那么数组的键会丢失
  返回值为： 1 true
  
+ rsort() - 对数组进行降序排列
+ asort() - 根据关联数组的值，对数组进行升序排列
+ ksort() - 根据关联数组的键，对数组进行升序排列
+ arsort() - 根据关联数组的值，对数组进行降序排列
+ krsort() - 根据关联数组的键，对数组进行降序排列






































+
