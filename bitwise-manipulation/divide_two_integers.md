# Divide Two Integers

## 扩展
判断两个数a,b相除或相乘结果的符号？
最直接写法
if((a>0 && b<0) || a<0 && b> 0)
  sign = -1;
else 
  sign = 1;