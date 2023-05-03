#       微信公众号：很酷的程序员
#       cmake -S . -B build
#       cmake --build build
#       ./build/yrxns


# CMake 最低版本号要求
cmake_minimum_required (VERSION 3.24.2)

#C99
set(CMAKE_C_STANDARD 99)
#C++11
set(CMAKE_CXX_STANDARD 11)
add_compile_options(-Wall -Wextra -Werror -Wpedantic -Wshadow -Wconversion)
#C编译选项
set(CMAKE_C_FLAGS "${CMAKE_CXX_FLAGS} -std=c99")
#C++编译选项
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

# 项目名称
project (yrxns)


#添加一个需要构建的子目录
add_subdirectory (myqfw)

#设置头文件路径搜索目录
include_directories(include)

# 将当前目录下所有源文件的名字保存到 DIR_SRCS 变量
aux_source_directory(. DIR_SRCS)

message("..." ${DIR_SRCS})

#编译成可执行文件
add_executable (${CMAKE_PROJECT_NAME} ${DIR_SRCS})



----------------------------------------------------------------------------------

file(GLOB_RECURSE DIR_LIB_SRCS
        src/module1/*.c
        src/module2/*.c
    )

# 将当前目录下所有源文件的名字保存到 DIR_LIB_SRCS 变量
aux_source_directory(. DIR_LIB_SRCS)

# 指定生成 math 静态链接库
add_library (math ${DIR_LIB_SRCS})

# 指定生成 math 动态链接库
add_library (math SHARED ${DIR_LIB_SRCS})

#指定编译所需的链接库
target_link_libraries (Demo ${DIR_LIB_SRCS})

#指定安装路径
set(CMAKE_INSTALL_PREFIX "/usr/local")

#RUNTIME 可执行文件
#LIBRARY 库文件
#ARCHIVE 归档文件
install(TARGETS math yrxns
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)



