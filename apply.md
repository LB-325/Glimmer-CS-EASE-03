`constValue`:由于被const修饰，储存在只读数据段       **//地址：00007FF6D1E74000**

`constString`：同上面一样由于const，储存在只读数据段     **//地址：00007FF6D1E73000**

`globalVar`：全局变量，储存在数据段中（静态存储），可以被任何函数访问，如果没储存在数据段中，在其他区如Stack，就无法被其他函数访问，就不是全局变量。所以储存在特定内存区域       **//地址：00007FF7FB313008**

`staticVar`：main函数中定义的局部变量，本来局部变量调用是在Stack上分配空间，但由于被static修饰，会被储存在数据段中（静态存储），但与全局变量不同的是，只有main函数可以访问

显然，局部变量在其他函数中属于未定义存在      **//地址00007FF7FB31300C**

`localVar`：局部变量，调用时在Stack上分配空间

![1729750898387](image/apply/1729750898387.png)

显然，局部变量在其他函数中属于***未定义***存在   **//地址0000002086BFF834**

`ptr`：作为指针指向堆区（由malloc函数分配的内存位置），但其本身存储在Stack上，属于局部变量

![1729749698250](image/apply/1729749698250.png)

显然，局部变量在其他函数中属于***未定义***存在      **//地址000002D42FA656E0**

`localVarMain`：和 `localVar`类似，是局部变量，储存在Stack     **//地址000000EB441FF85C**

```
#include <stdio.h>
#include <stdlib.h>

const int constValue = 100;
const char* constString = "Hello, World!";
int globalVar = 10;

void function(int arg) {
    int localVar = 20;
    int *ptr = malloc(sizeof(int));
    *ptr = 30;
    printf("%p\n",&localVar);     //不能在main函数中打印，因为是function中局部变量
    printf("%p\n",ptr);           //不能在main函数中打印，因为是function中局部变量
    free(ptr);
}

int main() {
    static int staticVar = 40;
    int localVarMain = 50;

    printf("%p\n",&constValue);
    printf("%p\n",&constString);
    printf("%p\n",&globalVar);
    printf("%p\n",&staticVar);
    printf("%p\n",&localVarMain);

    function(60);
    return 0;
}
```

---

***输出结果***：

00007FF764ED4000
00007FF764ED3000
00007FF764ED3008
00007FF764ED300C
000000D1023FFBFC
000000D1023FFBB4
000001F268B356E0
