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