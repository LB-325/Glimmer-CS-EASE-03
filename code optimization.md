# 一、传参技巧

***数组传参***：在函数调用时，若以数组为参数传递时，不能在数字名后加[ ]，应再传递一个参数代表数组长度，可以利用此特性，当一个数组中数据没填满或只想传入前面部分数据时，可以控制传入长度，可以减少运算时间，优化了代码

[Glimmer-CS-EASE-03/452e42eabebbb102d5e82c52abbc15b7.jpg at main · LB-325/Glimmer-CS-EASE-03](https://github.com/LB-325/Glimmer-CS-EASE-03/blob/main/452e42eabebbb102d5e82c52abbc15b7.jpg)

![1729779230996](image/codeoptimization/1729779230996.png)

# 二、判定素数算法优化

```
#include<stdio.h>
#include<stdbool.h>
bool is_prime(int n){
    int divisor;
    if(n<=1){
        return false;
    }else {for(divisor=2;divisor*divisor<=n;++divisor){
            if(n%divisor==0){
            return false;
            }else{
                return true;
            }
        }
    }
}
int main(){
    int n;
    printf("Enter a number:");
    scanf("%d",&n);
    if(is_prime(n)){
        printf("Prime\n");
    }else{
        printf("Not prime\n");
    }
    return 0;
}
```

运算时是用被判定数依次除以比它小的数，但是对于运算而言，只用计算到被判定数的1/2次方即可，所以将 `for(divisor=2;divisor<=n;++divisor)`优化为 `for(divisor=2;divisor*divisor<=n;++divisor)`。当n很大时便大大节省了计算机算力

# 三、简洁函数

```
int main(){
    int a=2,b=3;
    if(a>b){
        printf("max=%d\n",a);
    }else{
        printf("max=%d\n",b);
    }
    return 0;
}
```

可以将代码简化，运用运算符 ***表达式1？表达式2：表达式3*** 代替 ***if*** 条件语句

```
int main(){
    int a=2,b=3;
    printf("max=%d\n",a>b?a:b);
    return 0;
}
```
