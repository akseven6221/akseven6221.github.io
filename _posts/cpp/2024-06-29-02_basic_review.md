---
title: 2.basic_review
# author: alioth
date: 2024-06-29 23:34:23 +0800
categories: [language, c++]
tags: [c++]
description: 基本类型和复合类型 表达式 类 控制流 函数重载 模板
---

## baisc review

### 基本类型

#### auto

- auto 不能推断(deduce)出引用类型和const，所以一般得显示的指定，不然auto就是原来的数据类型。比如`const auto& a = b;`
- 可以用auto来指定指针，e.g.`auto* a = &b;`。等价于`auto a = &b;`。
- 可以用auto少写很多东西，比如用迭代器进行循环的时候。

#### integer

1. It's ub for signed integers to overflow.
  - 127+1对于8-bit的有符号数是ub行为。
  
    一个典型的关于无符号整数的bug。

    ```c++
    #include <iostream>

    int main () {
        std::string s = "hello world";
        // std::string::find返回的是size_t类型，没有负数形式。所以这个会永远打印found。
        if (s.find("t") >= 0) {
            std::cout << "found\n";
        } else {
            std::cout << "not found\n";
        }
    }
    ```
    解决方案：
    - 用!=
    - c++20中可以用`std::cmp_xxx`来比较`unsigned`和`signed integers`(包括了 `bool/characters`)。
    - `std::cmp_greater_equal(std::string::npos, 0)` 就会返回 `false`
    - `std::in_range<T>(x)`也可以用来检查一个值是否representable by integer type T
    - 总之对无符号数的比较要非常小心仔细


2. It's ub for integers to divide 0.
3. All arithmetic operations will promote integers that are smaller than int to int first.
   - 也就是说(unsigned) char/short 会提升到int，然后才开始做算数运算。
   - 一个很坑的例子：最后输出只有一个`unexpected`。

    ```c++
    #include <iostream>

    int main () {
        unsigned short s1 = 0xff00, s2 = 0x100, s3 = 0xffff;
        if (s1 + s2 > s3)
            std::cout << "unexpected!\n";

        unsigned int i1 = 0xffff0000, i2 = 0x10000, i3 = 0xffffffff;
        
        if (i1 + i2 > i3)
            std::cout << "unexpected, too!\n";
        
        return 0;
    }
    ```

integer在各个平台上可能都不太一样。
如何保证使用确定长度的数？
- 在<cstdint>，这里有一些等长数据
  - 不过有些平台不支持一些数据，所以这个是可选的
  - 不过都用这个了也表示咱不会去碰哪些不支持的机器
  - 如果真的要写更一般的代码，可以：
    - `std::(u)int_least(x)_t`: 最小是 x bits 的数。(x=8/16/32/64)
    - `std::(u)int_fast(x)_t`: 
    - `std::(u)intmax_t`: 系统的最大支持的数。
  - 以上的内容只是 int/long long...的别名，不是其他不同的类型。
    - 一般来说，std::uint8_t就是unsigned char，如果想要打印std::uint8_t的地址，那将会采用c-string的方式打印(直到打印到终止符停止\0)
    - 我们需要将`std::uint8_t*`转成`void*`来拿到地址(用std::cout的时候)

Integer的bit操作：(好像没什么用，跳了)
    - c++20里提供了<bit>
    - `std::has_single_bit`: 看这个整数是不是2的幂次。
    - `std::bit_ceil`: 把当前二进制数的最高位设置为1，其余置0.
    - `std::bit_floor`: 

#### Floating point

所有关于NaN的算数运算得到的还是NaN； inf + (-inf) = NaN。

c++14支持这样分隔数：0x11ff'ffff; 0b0011'0100。

### 复合类型

#### 指针类型

- 对nullptr解引用是ub行为。

- 我们为什么不用NULL而是nullptr?
  - c++中NULL不是一个指针而是一个integer。
  
#### 引用类型

- 一个语法糖
- 和指针不同的地方：
  - 引用不为空
  - 引用的对象永远都是那个对象，不会换别人引用
  - 引用是不确定是否占用内存的
  - 引用禁止做模板参数
  
#### cv-qualifier

- const & volatile
  - volatile: 这是干啥的来着？
  - const: 将其设置为不可变类型。

#### 数组类型