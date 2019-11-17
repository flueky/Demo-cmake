# 定义 cmake 最低兼容版本
cmake_minimum_required(VERSION 3.13)
# 定义工程名称
project(cm-lib)
# 包含头文件目录
include_directories("src/include")
# 定义源码文件
SET(SRC_LIST src/test.c)
# 添加源码文件到库中
add_library(test SHARED ${SRC_LIST})