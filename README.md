## CMake 构建 C/C++ 工程

### 创建主工程

**主工程 用于生成可执行文件。**

创建  sample 文件夹，在  sample 目录下创建 src 文件夹存放源码。

在  src 目录下，创建 main.c 文件做工程入口。

为演示些更充足的场景，在  src 目录下建立 test 文件夹，用于存放些编写的函数库。

```c
// test.h 文件内容 
#ifndef TEST_H
#define TEST_H

void print();

#endif // define TEST_H

// test.c 文件内容
#include "test.h"
#include <stdio.h>

void print() {
    printf("hello test\n");
}
```

最终在 main.c 中调用。

```c
#include <stdio.h>
#include "test/test.h"

int main(){
    printf("hello world\n");
    print();
    return  0;
}
```

在 sample 目录下创建  **CMakeLists.txt** 配置工程。

```cmake
# 定义 cmake 最低兼容版本
cmake_minimum_required(VERSION 3.13)

project(cm-demo)

# 配置编译程序到可执行文件,所有 c/c++ 文件都要添加进去
add_executable(zkf src/main.c src/test/test.c)
```

**每次修改 CMakeLists.txt  文件，CLion 都提示 Reload changes ，需要点击一次。**

配置完成后可直接  run 程序 。

### 创建库工程

**库工程用于生成库文件，供主工程或其他库使用。**

