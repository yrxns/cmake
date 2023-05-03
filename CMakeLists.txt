#       cmake -S . -B build
#       cmake --build build
#       ./build/yrxns

#       mkdir build
#       cd build
#       cmake ..
#       make


# CMake 最低版本号要求
cmake_minimum_required (VERSION 3.24.2)

# 项目名称
project (yrxns)

#C99
set(CMAKE_C_STANDARD 99)
#C++11
set(CMAKE_CXX_STANDARD 11)
add_compile_options(-Wall -Wextra -Werror -Wpedantic -Wshadow -Wconversion)
#指定编译器
set(CMAKE_C_COMPILER g++)
#C编译选项
set(CMAKE_C_FLAGS "${CMAKE_CXX_FLAGS} -std=c99")
#C++编译选项
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
#指定编译类型
set(CMAKE_BUILD_TYPE release)


# 子目录
set(SUBDIRS src a b c)
# 头文件路径
set(INCDIRS include)

# 添加头文件目录
foreach(incdir ${INCDIRS})
    include_directories(${incdir})
endforeach()
# 添加子目录
foreach(subdir ${SUBDIRS})
    add_subdirectory(${subdir})
endforeach()

# 将当前目录下所有源文件的名字保存到 DIR_SRCS 变量
aux_source_directory(. DIR_SRCS)

message("..." ${DIR_SRCS})

# 指定生成目标
add_executable (${CMAKE_PROJECT_NAME} ${DIR_SRCS})

# 添加链接库
target_link_libraries(${CMAKE_PROJECT_NAME} ${SUBDIRS})



----------------------------------------------------------------------------------



