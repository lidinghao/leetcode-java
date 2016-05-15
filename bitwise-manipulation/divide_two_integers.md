# Divide Two Integers
## 问题描述
首先通过计算结果符号，把问题reduce到两个整数相除。然后把两个数字转为long型，以免溢出。
最后把被除数减去除数，并通过将被除数每次加倍来加快速度。当被除数大于剩余的除数时，再从初始的除数开始，重复以上步骤。
## 代码实现
```java
public int divide(int dividend, int divisor) {
        int sign = (( dividend<0) ^ (divisor <0))  ? -1 : 1;
        long dvd = Math.abs((long)dividend);
        long dvs = Math.abs((long)divisor);
        long result = 0;
        while (dvd > dvs) {
            long temp = dvs;
            for (int i = 0; dvd >= temp; i++, temp <<= 1) {
                dvd -= temp;
                result += 1<<i;
            }
        }
        result = sign*result > Integer.MAX_VALUE ? Integer.MAX_VALUE : sign*result;
        return (int) result ;
    }
```
## 扩展
判断两个数a,b相除或相乘结果的符号？
**最直接写法**
if((a>0 && b<0) || a<0 && b> 0)
  sign = -1;
else 
  sign = 1;
**通过异或操作来写
sign = (a < 0) ^ (b < 0) ? -1 : 1;

**位移加异或**
sign = (a^b)>>>31 == 0 ?  1 : -1;

**通过布尔逻辑**
sing = a < 0 != b < 0 ? -1 : 1; 