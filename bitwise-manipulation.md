# 位运算

### Java位操作运算符
#### 符号右移(">>")
负数在最高位填充"1"，正数在最高位填充"0", 右移一位相当于除2,ArrayList中每次扩容1.5倍，所使用的代码就是：
newCapacity = oldCapacity + (oldCapacity >> 1);
#### 左移("<<")
在最低位填充"0", 左移一位相当于乘2。
### 无符号右移(">>>")
在最高位填充"0"。
#### 位与("&")
按位与运算符，常见应用是用来做bitmask运算：
```java
   int bitmask = 0x000F;
   int val = 0x2222;
   val & bitmask == 2
```
#### 位异或("^")
"bitwise exclusive OR"，两个操作数的第n位相同则结果第n位为0，不同即相异则结果第n位为1。

#### 位或("|")
"bitwise inclusive OR"，两个操作数的第n位有一个为1，则结果第n位为0，如果都为0则结果第n位为1。

注意，如果用位运算来进行逻辑运算的话，会导致两边的逻辑表达式都会被运算，如下面所示：
```java
        int array[] = new int[]{1,2,3};
        int i = 0;
        //这里不会发生数组越界
        while(i < array.length && array[i] != 4){
            i++;
        }
       
        i = 0;
        //这里会发生数组越界
        while(i < array.length & array[i] != 4){
            i++;
        }
```
因此，逻辑运算符也叫做"short-circuit" 布尔运算符， 位运算符叫做"non-short-circuiting"运算符。 因为当左边表达式就可以决定整个表达式的值时，右边的就不会被计算。而为位运算符总是计算左右两个表达式。
## 经典算法
对于整型变量a、b，如何不经中间变量，来交换a与b的值？
a = a^b; b = b ^ a; a = b ^ a; 或者 a = a + b; b = a - b; a = a - b;
