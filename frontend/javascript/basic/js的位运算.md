## javascript中高性能的运算 位运算

### 重温整数

> ECMAScript整数有两种类型，有符号整数（允许用正数和负数）和无符号整数（只允许用正数）。在ECMAScript中，所有整数字面量默认都是有符号整数。
有符号整数，数值范围从-2147483648到2147483647；无符号整数，数值范围从0到4294967295。记住，所有整数字面量都默认存储为有符号整数，只有ECMAScript的位运算符才能创建无符号整数。
把无符号整数转换为字符串，只返回有效位。也就是前面都是0的就不返回了。

```
var i = 18, j = -18;
alert(i.toString(2)); // -> '10010'
alert(j.toString(2)); // -> '-10010'
```
虽然负数的二进制显示是在正数的二进制表示前加负号,但负数存储也是二进制代码，采用的形式是二进制补码。

#### 计算二进制补码步骤有3步：

1. 确定数字的非负版本的二进制表示。如，-18的补码要先确定18的二进制表示
2. 求得二进制反码，即把0替换为1，把1替换为0
3. 在二进制反码上加1

### 位运算符NOT(~)

> 位运算符由否定好(~)表示，它是ECMAScript中为数不多的与二进制算术有关的运算符之一。位运算符NOT是三步的处理过程：

1. 把运算数转为32位二进制数字
2. 再转为它的二进制反码
3. 把二进制反码转为浮点数
感觉很麻烦，而上述操作简单来说，可以相当于对数字求负，然后减1，比如~25 === -26

#### 位运算符AND(&)
> 它对数字的二进制进行操作，把数字转换为二进制后，把每个数字中的数位对齐，然后以下面规则进行AND运算：

```
1 对 1 -> 1
1 对 0 -> 0
0 对 1 -> 0
0 对 0 -> 0
```

因此，25 & 3 = 1

### 位运算符OR(|)

同理AND运算符，只不过它的规则是：
```
1 对 1 -> 1
1 对 0 -> 1
0 对 1 -> 1
0 对 0 -> 0
````
因此， 25 | 3 = 27

### 位运算符XOR(^)

同上理，只不过它的规则是：
> 1 对 1 -> 0
  1 对 0 -> 1
  0 对 1 -> 1
  0 对 0 -> 0

因此， 25 ^ 3 = 26

### 左移运算(<<)

> 移位运算一般在开发中用不到，都是用于极度优化的代码中如驱动程序。左移运算把数字的所有数位向左移动指定的数量。在左移数位时，数字右边多出的空位会被0填充，使结果为完整的32位数字。注：左移操作保留数字的符号位。“符号仍然存储在第32位中吗？”是的。

### 有符号右移运算(>>)
> 它把32位数字中的所有数位整体右移，同时保留该数的符号。移位后会造成空位，这时空位位于数字的左侧，位于符号为的右侧，ECMAScript用符号位来填充空位，创建完整的数字。

### 无符号右移运算(>>>)
它把32位数字中的所有数位整体右移。对于正数，它与有符号右移运算是一样的。对于负数，情况就不同了。无符号右移用0填充所有空位。对于正数，这与有符号右移运算的操作完全一样，而负数则被作为正数来处理。由于无符号右移运算的结果是一个32位的正数，所以负数的无符号右移运算得到的是一个非常大的数字。要实现这点，需要把数字转为无符号的等价形式（尽管这个数字还是有符号的），可以这样来转换：

`var iUnsigned64 = -64 >>> 0;`
然后用Number类型的toString()获取它真正的位表示，采用的基为2：

`alert(iUnsigned64.toString(2));`
结果生成 11111111111111111111111111000000，即有符号的-64的二进制补码表示，不过它等于无符号整数4294967232。出于这种原因，使用无符号右移运算符时要小心。
