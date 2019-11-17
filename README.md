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
add_executable(demo src/main.c src/test/test.c)
```

**每次修改 CMakeLists.txt  文件，CLion 都提示 Reload changes ，需要点击一次。**

配置完成后可直接  run 程序 ，在  cmake-build-debug 目录下生成的 demo 程序即是可执行文件。

### 创建库工程

**库工程用于生成库文件，供主工程或其他库使用。**

创建步骤与主工程相似，定义目录层级时，可以将头文件放置在 include 目录下，与源文件分开。

还是以 test.h 和 test.c 的例子：（详见工程 library）

在 library 目录下创建  **CMakeLists.txt** 配置工程。

```cm
# 定义 cmake 最低兼容版本
cmake_minimum_required(VERSION 3.13)
# 定义工程 名称 
project(cm-lib)
# 包含头文件目录
include_directories("src/include")
# 定义源码文件
SET(SRC_LIST src/test.c)
# 添加源码文件到库中
add_library(test SHARED ${SRC_LIST})
```

配置完成后 ，编译工程将在 cmake-build-debug 目录下生成 libtest.dylib 文件（Mac 系统后缀 dylib，Linux  系统后缀 so，Windows 系统后缀 dll）。

### 关联工程

在库工程编译成功之后，将库文件复制到主工程 lib 目录下，在主工程的 **CMakeLists.txt** 文件中修改下配置 ，关联库文件和库文件的头文件。

```cmake
# 定义 cmake 最低兼容版本
cmake_minimum_required(VERSION 3.13)
# 定义工程名称
project(cm-demo)
# 关联库文件的头文件
include_directories("../library/src/include")
# 关联库文件所在目录
link_directories(lib)
# 关联库文件，前缀 lib 省略，后缀  dll/so/dylib 省略
link_libraries(test)
# 配置编译程序到可执行文件,所有 c/c++ 文件都要添加进去
add_executable(demo src/main.c)
# 关联库文件，前缀 lib 省略，后缀  dll/so/dylib 省略
# 同 link_libraries 作用一样
#target_link_libraries(zkf demo)
```

