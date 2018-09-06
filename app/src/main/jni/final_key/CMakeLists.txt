# 声明要求的cmake最低版本
cmake_minimum_required(VERSION 3.4.1)

# 添加c++11标准支持
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DUSE_SHA256")

# 头文件
include_directories(aes/)
include_directories(sha/)

# 创建共享库（把工程内的c文件都创建成共享库文件，方便通过头文件来调用）
add_library(
    final-key SHARED
    kpd_jni.c
    aes/aescrypt.c
    aes/aeskey.c
    aes/aes_modes.c
    aes/aestab.c
    sha/hmac.c
    sha/sha1.c
    sha/sha2.c
)

# 找到后面需要库和头文件的包
find_library(log-lib log)

# 链接库
# 把刚刚生成的${PROJECT_NAME}库和所需的其它库链接起来
target_link_libraries(final-key ${log-lib})
