

# 数组

  数组是一组相同类型元素的集合
    数组创建的方式：
    type_t   array_name   [const_n];
    type_t     是数组的元素类型
    array_name   是数组名
    const_n   是一个常量表达式，用来指定数组的大小

## 一、一维数组的创建和初始化

```c
#include <stdio.h>
int main()
{
    //创建一个数组-存放整型-10个
    int arr[10];
    //创建一个数组-存放字符-5个
    char arr2[5];
    return 0;
}
```

注意：数组创建，[ ]中要给一个常量才可以，不能使用变量。

### 1、数组的初始化

数组的初始化是指创建数组是同时给数组的内容一些合理的初始值。

```c
#include <stdio.h>
int main()
{
    int arr[10]={1,2,3};
    //不完全初始化，剩下的元素默认初始化为0
    char arr2[5]={'a','b'};
     //不完全初始化，剩下的元素默认初始化为0
    char arr3[5]="ab";
    //三个初始化元素：'a','b','/0';
    char arr4[ ]="abcdef";
    //系统自动识别存储元素个数abcdef+/0，7个
    printf("%d/n",sizeof(arr4));//7
    printf("%d/n",strlen(arr4));//6
    return 0;
}
```

##  2、sizeof ( )  

是一个操作符，计算变量所占空间大小，任何类型都可以使用

只关心空间大小，不在乎内存中是否存在\0（存在\0，也纳入计算）

例：

char arr4[ ]="abcdef"；

printf("%d/n",sizeof(arr4));

arr4中存储七个元素【a,b,c,d,e,f,\0】

 所占空间sizeof(arr4)=7

## 3、strlen ( )

是一个库函数，计算字符串长度，并且只能针对字符串

关于字符串中是否有\0，计算的是\0之前的字符个数

例： 

 char arr4[ ]="abcdef";

printf("%d/n",strlen(arr4));

arr4中存储六个字符【a,b,c,d,e,f】

字符串长度strlen(arr4)=6

### 4、数组名

数组名是数组首元素的地址

补充：

1、sizeof（数组名），表示计算整个数组的大小

2、&数组名，取出的是整个数组的地址

3、数组名，取出的是数组首元素的地址

```c
#include <stdio.h>
int main()
{
    int arr[10]={1,2,3,4,5,6,7,8,9,0};
    
    printf("%d",sizeof(arr));
    printf("%d\n", sizeof(arr));
    printf("%p\n", &arr);
    printf("%p\n", arr);
    printf("%p\n", &arr+1);
    printf("%p\n", arr+1);
  
    return  0;
}
    /*
    运行结果：
    40
    000000F524D8F588
    000000F524D8F588
    000000F524D8F5B0
    000000F524D8F58C
    */
```

 注： &arr与arr取地址结果一样，&arr取的地址是以首元素地址开头，arr取的是首元素地址

## 二、二维数组的创建和初始化

### 1、行和列

行，是指二维数组里有几个一维数组；

列，是指这些数组里最多含有多少个元素；

### 2、二维数组的创建和初始化

```c
#include <stdio.h>
int main()
{
    //二维数组的创建和初始化
    //未赋值的元素系统默认为0
    int arr[3]][4]={{1,2,3},{4,5}};
    //元素：
    //{1，2，3，0}
    //{4，5，0，0}
    //{0，0，0，0}
    char arr[2][6]={{1,2},{4,5}};
    //元素：
    //{1，2，0，0，0，0}
    //{4，5，0，0，0，0}
    double arr[4][3]={{2,3},{4,5}};
    //元素：
    //{2,3,0}
    //{4,5,0}
    //{0,0,0}
    //{0,0,0}
    return 0;  
  } 
```

### 3、二维数组元素的打印使用

```c
#include <stdio.h>
  int main()
  {
    //二维数组元素的打印使用
    int arr[3]][4]={{1,2,3},{4,5}};
    int i=0;
    for(i=0;i<3;i++)
    {
        int j=0;
        for(j=0;j<4;j++)
        {
            printf("%d",arr[i][j]);
        }
    }
        printf("\n");
      //结果：
      //1 2 3 0
      //4 5 0 0
      //0 0 0 0
        return 0;
    }
```

### 4、二维数组元素地址的打印使用

```c
#include <stdio.h>
  int main()
  {
    //二维数组元素地址的打印使用
    int arr[3]][4]={{1,2,3},{4,5}};
    int i=0;
    for(i=0;i<3;i++)
    {
        int j=0;
        for(j=0;j<4;j++)
        {
            printf("&arr[%d][%d]=%p\n",i,j,&arr[i][j]);
        }
    }
      /*
      结果：
      &arr[0][0]=000000EE78CFF6C8
      &arr[0][1]=000000EE78CFF6CC
      &arr[0][2]=000000EE78CFF6D0
      &arr[0][3]=000000EE78CFF6D4
      &arr[1][0]=000000EE78CFF6D8
      &arr[1][1]=000000EE78CFF6DC
      &arr[1][2]=000000EE78CFF6E0
      &arr[1][3]=000000EE78CFF6E4
      &arr[2][0]=000000EE78CFF6E8
      &arr[2][1]=000000EE78CFF6EC
      &arr[2][2]=000000EE78CFF6F0
      &arr[2][3]=000000EE78CFF6F4
      */
        return 0;
    }
```

## 三、数组越界

数组的下表是有范围限制的

数组的下标规定是从0开始的，如果输入有n个元素，最后一个元素的下标就是n-1

故 数组的下标如果小于0或者大于n-1，就是数组越界访问了，超出了数组合法的空间访问

C语言本身是不做数组下标的检查，编译器也不一定报错，但并不意味着程序是正确的

二维数组的行和列也存在越界

## 四、 冒泡排序

### 1、升序排列

```c
#include <stdio.h>
int main()
{
    //利用冒泡排序实现升序排列
    //排序总轮数=元素个数-1
    //每轮对比次数=元素个数-排序次数-1
    int arr[9] = { 2,4,0,5,7,1,3,8,9 };
    int i = 0;
    printf("排序前：\n");
    for (i = 0; i < 9; i++)
    {
        printf("%d  ", arr[i]);
    }
    /*
    排序前：
    2  4  0  5  7  1  3  8  9
    */
    printf("\n");
    //开始冒泡排序
    for (i = 0;i < 9; i++)
    {
        //内层循环对比 次数=元素个数-当前轮数-1
        int j = 0;
        for (j = 0; j < 9 - 1; j++)
        {
            //如果第一个数比第二个数大，就交换两个数
            if (arr[j]>arr[j + 1])
            {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    printf("排序后：\n");
    int x = 0;
    for (x = 0; x< 9; x++)
    {
        printf("%d  ", arr[x]);
    }
    /*
    排序后:
    0  1  2  3  4  5  7  8  9
    */
    return 0;

}
```

### 2、降序排列

```c
#include <stdio.h>
int main()
{
    //利用冒泡排序实现升序排列
    //排序总轮数=元素个数-1
    //每轮对比次数=元素个数-排序次数-1
    int arr[9] = { 2,4,0,5,7,1,3,8,9 };
    int i = 0;
    printf("排序前：\n");
    for (i = 0; i < 9; i++)
    {
        printf("%d  ", arr[i]);
    }
    /*
    排序前：
    2  4  0  5  7  1  3  8  9
    */
    printf("\n");
    //开始冒泡排序
    for (i = 0;i < 9; i++)
    {
        //内层循环对比 次数=元素个数-当前轮数-1
        int j = 0;
        for (j = 0; j < 9 - 1; j++)
        {
            //如果第一个数比第二个数大，就交换两个数
            if (arr[j]<arr[j + 1])
            {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    printf("排序后：\n");
    int x = 0;
    for (x = 0; x< 9; x++)
    {
        printf("%d  ", arr[x]);
    }
    /*
    排序后：
    9  8  7  5  4  3  2  1  0
    */
    return 0;
}
```





