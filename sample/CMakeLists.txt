# 定义 cmake 最低兼容版本
cmake_minimum_required(VERSION 3.13)

project(cm-demo)

# 配置编译程序到可执行文件,所有 c/c++ 文件都要添加进去
add_executable(zkf src/main.c src/test/test.c)