

----------------------------------------------------------------------------------

 #file(GLOB_RECURSE DIR_LIB_SRCS
 #        src/module1/*.c
 #        src/module2/*.c
 #    )

# 将当前目录下所有源文件的名字保存到 DIR_LIB_SRCS 变量
aux_source_directory(. DIR_LIB_SRCS)

# 正则表达式得到当前目录名字作为提供给上一层的库名字
string(REGEX REPLACE ".*/(.*)" "\\1" LIB_NAME ${CMAKE_CURRENT_SOURCE_DIR})

# 生成静态链接库
add_library (${LIB_NAME} ${DIR_LIB_SRCS})

# 生成动态链接库
add_library (${LIB_NAME} SHARED ${DIR_LIB_SRCS})


#指定安装路径
set(CMAKE_INSTALL_PREFIX "/usr/local")

#RUNTIME 可执行文件
#LIBRARY 库文件
#ARCHIVE 归档文件
install(TARGETS math yrxns
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)



