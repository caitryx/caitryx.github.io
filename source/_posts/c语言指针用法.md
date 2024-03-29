---
title: c语言指针用法
date: 2021-06-09 18:00:43
tags: 
    - pointer
categories:
    - c
index_img: https://cdn-ali-img-shstaticbz.shanhutech.cn/bizhi/staticwp/202105/58ecbeb7dbd1e25a1e063d6c7f47037b--3853100870.jpg
---

*这里指针的内容根据c Primer Plus上整理出来的，省略了书上部分内容，只记录了容易混淆的一些内容。*
<!-- more -->



## 指针

数据存储在内存中，他们都有特定的存放位置，而内存地址便是像门牌一样，用来表示数据的位置，想要找到这些数据，就要通过地址来进行查找。先定义一个整型变量: int num = 10，这个num的变量存储的值是10。而指针变量，和普通的变量不同，其存储的值为地址。

## 声明指针

```c
int *num;  // num是指向int类型数据的指针变量
```

指针变量的声明和普通的变量声明类似，星号*用于表明声明的变量是一个指针，int表明指针所指向的数据的类型。

## 操作指针

### 指针赋值

```c
int ca = 20;
num = &ca;  // 必须是将地址赋值给指针变量
```

上面的num = &ca，就是使用&地址运算符，将ca的地址赋值给num，赋值后，num便指向ca。

### 获取指针的值

```c
printf("%p ", num);  // 输出num的值(也就是其指向的地址)。输出结果: 000000000061FE14
```

这里获取的是num的值，num是一个指针变量，其存储的便是地址。

```c
printf("%d ", *num);
```

通过*解引用运算符可以获得指针变量所指向的地址中存储的数据。注意: 在定义指针变量和在定义指针变量后，星号 * 的含义和作用是不一样的。

*在定义时，星号表示声明的变量是一个指针*

*在定义完之后使用，星号表示获取存储在地址上的数据:*

## 数组和指针

```c
int arr[] = {1, 2, 3, 4, 5, 6};
int *pti = arr;  // pti为指向int类型数据的指针
printf("%s %d", pti, *pti);  // 输出结果: 000000000061FE0C  1
```

从上面的例子可以看出，数组名就是该数组首元素的地址。数组中的数据在内存中的存放是连续的，也就是说通过对指针变量的加减，可以实现指针指向数组中的不同元素。

```c
// 注意，*运算符优先级高于+，如果写成这种方式:*pti + 1，这表示先获取pti所指向的值然后再加1
printf("%d %s", *(pti + 1), (pti + 1));  // 输出结果: 2 000000000061FE10
```

将pti指针+1后，输出它所指向的地址和地址所存储的值，发现pti这时候指向的是数组中的2这个元素，但是"000000000061FE0C"和"000000000061FE10"这两个地址之间并不是只加了1，两者相减发现是相差了4，这表示指针加1不是直接加1，而是加一次指针所指向的类型的大小(int 类型占用4个字节)，指针加1之后就是下一个元素的地址。

```c
   int *t1 = arr;  // 将数组第一个元素的地址赋值给t1
   int *t2 = &arr[3];  // 将数组第四个元素赋值给t2
   printf("地址相减的差值为%td ", t2 - t1);  // 输出结果:地址相减的差值为3
```

对地址的相减，会得出两个地址之间相差多少个元素。指针的相加相减，都是以一个元素的大小为单位的，而不是直接对地址进行整数的加减。

## 多维数组和指针

### 指向多维数组的指针

```c
int arr2[4][2] = {{2, 3}, {4, 5}, {6, 7}, {8, 9}};
int (*pz)[2];  // 指向一个内含两个int类型值的数组
pz = arr;
// 由于[]的优先级高于*，所以会先和pzx进行结合，那么pzx就成为了一个内含两个元素的数组，*
// 则表示pax数组内含两个指针
int *pzx[2];  // pzx是一个内含两个指针元素的数组，每个元素都指向int的指针
```

将arr首元素的地址赋值给pz，pz就指向一个内含两个int类型元素的数组，pz的地址就是{2, 3}这个数组的首元素的地址，pz和arr2\[0\]、arr2\[0\]\[0\]的地址是相同的。

因为pz指向的对象是一个包含两个int类型元素的数组，arr[0]指向一个int类型的元素，两者地址虽然相同，但是在指向这一方面是不一样的。所以，如果想通过pz获取数组中2这个元素，需要解引用两次:\*\*pz，第一次解引用，*pz代表着获取这个数组的首元素的地址(也就是2的地址)，第二次解引用才能获取pz所指向的地址所存储的值。

### 指针赋值的需要注意的地方

1. 定义的指针为什么类型，就只能赋什么类型的值。
2. 如果定义了一个指向指针的指针(例如: int **pu;)，那么就只能将其他指针赋值给pu，而\*pu获取的值就是指针。
3. 不能直接使用指针来创建数组，因为指针只能存储地址。

## 字符串、字符串数组与指针的联系

### 声明字符串

```c
// 方式1
char str2[] = "testing2";  // 字符串数组
// 方式2
char *str3 = "testing3";  // 使用指针表示法创建字符串

```

这两种方式都可以用来创建字符串，str2和str3的值都是字符串的地址。

### 数组形式和指针形式创建的字符串的不同

数组形式创建的字符串，字符串存储在静态存储取中，程序运行后会将字符串拷贝到数组，也就是有两份相同的字符串，一份在静态内存中，一份存储在数组中(也就是str2的地址所存储的值便是这个字符串)。str2是地址常量，不能对其进行修改(例如str2++这样对str2本身进行修改是不行的)。而指针形式创建的字符串，指针变量存储的值是字符串的地址，可以对指针变量进行修改，这样不会影响到字符串。数组形式创建的字符串可以进行值的修改(例如:str2[1]  = 'x')，不能对指针形式创建的字符串进行修改(例如: str3[3] = 'x' 这样是不允许的)。

## 指针与函数

### 一维数组和函数

```c
void test(int *ar, int);  // 函数原型

int main(void)
{
    int arr[] = {1, 2, 3, 4, 5};
    test(arr, 5);
    return 0;
}

void test(int *ar, int size)  // 函数定义头
{
    for (int i = 0; i < size;i++)
    {
        printf("%d", *(ar++));  //@2
    }
}
```

上面调用test函数时，将数组arr作为参数传递，传递的是arr数组的地址(数组名是该数组首元素的地址)。在test函数中，ar是作为一个指针。函数原型和函数定义头中，使用的是int \*ar，但是也可以将其替换称int ar[]。

```c
// 将int \*ar换成int ar[]
void test(int ar[], int);
```

这样也是可以的，都表示ar是一个指向int的指针，但是int ar[]这种形式可以明确的表示ar是一个数组。

### 多维数组和函数

```c
void test2(int (*ar)[3]);
main(void)
{
	int tp[2][3] = {{2, 3, 4}, {5, 6, 7}};
	test2(tp);
}

void test2(int (*ar)[3])
{
	;
}

```

这里的int (\*ar)[3]代表着ar是一个指向数组的指针，而数组中包含有3个元素，这样定义函数原型就可以将一个二维数组作为参数传递给test2函数。当然了，也可以直接使用int ar[\]\[3\]放在函数原型和函数定义头中，第一个括号为空代表着ar是一个指针，即使在第一个括号中写具体的大小，编译器也会将忽略该值。