---
title: 在C++中使用format
date: 2023-03-31 21:14:04
tags: 
- C++ 
- format
---

到目前为止，还没有编译器支持C++20的`format`模块。这个模块提供了安全、优雅和高效的文本格式化，主要以`std::format()`函数的形式出现。

那么我们想要在C++中使用`format`该怎么办呢？

我们可以使用`fmt`来实现！`fmt`是一个免费和开源的现在标准化的`format`模块的超集的实现。

下面以Mac为力介绍如何使用`fmt`.
我的Mac是M1芯片，系统是Ventura 13.0.1

第一步：使用homebrew安装fmt

如果你的电脑是MacOS或Linux，强烈建议安装homebrew，安装教程可以参考 [Homebrew安装](https://brew.idayer.com/guide)

```shell
brew install fmt
```

同时也安装：
```shell
brew install pkg-config
```
注：`pkg-config`是一个在编译应用程序和库时使用的辅助工具。它帮助你在命令行中插入正确的编译器选项。`pkg-config`官网：https://freedesktop.org/wiki/Software/pkg-config/

第二步：在用命令行编译C++程序时，我们需要知道fmt安装的位置。

使用`pkg-config`可以直接生成相关库的在编译时的参数

```shell
pkg-config --libs --cflags fmt
# 输出：-I/opt/homebrew/Cellar/fmt/9.1.0/include -L/opt/homebrew/Cellar/fmt/9.1.0/lib -lfmt
```

现在就准备完毕了，写一个测试程序：

```c++
// test_format.cpp
#include <iostream>
#define FMT_HEADER_ONLY
/*
#define FMT_HEADER_ONLY 建议加上这句
使用Mac OS自带的gcc编译器时，不加这句不会报错
使用自己安装的GNU的gcc编译器，不加这句会报错
*/

#include <fmt/format.h>

int main()
{
  std::cout << fmt::format("{:7}|{:7}|{:7}|{:7}|{:7}\n", 1, -.2, "str", 'c', true);
  std::cout << fmt::format("{:*<7}|{:*<7}|{:*>7}|{:*>7}|{:*>7}\n", 1, -.2, "str", 'c', true);
  std::cout << fmt::format("{:^07}|{:^07}|{:^7}|{:^7}|{:^7}\n", 1, -.2, "str", 'c', true);
}

```

编译命令：
```shell
g++ -Wall -std=c++20 -I/opt/homebrew/Cellar/fmt/9.1.0/include -L/opt/homebrew/Cellar/fmt/9.1.0/lib -lfmt -o test_format test_format.cpp
```

程序输入：
```shell
      1|   -0.2|str    |c      |true   
1******|-0.2***|****str|******c|***true
0001000|0-0.200|  str  |   c   | true 
```

成功了！

`fmt`更多用法:

- 官网：https://fmt.dev/latest/index.html
- Cheat Sheets：https://hackingcpp.com/cpp/libs/fmt.html
- Github：https://github.com/fmtlib/fmt