cmake_minimum_required(VERSION 3.30.0)
project(kalman)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
#变量和目录设置
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)#动态库和exe生成到同一文件
# set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)#不需要这句


#包含文档生成动态库
aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LIST)
add_library(common 
    SHARED
    ${SRC_LIST}
)#将src中的内容生成动态库名叫common

target_include_directories(common
PUBLIC
${PROJECT_SOURCE_DIR}/include
)#动态库common包含头文件库



#可执行文件

add_executable(kalman_main kalman_main.cpp)

#可执行文件包含头文件
target_include_directories(kalman_main
PUBLIC
${PROJECT_SOURCE_DIR}/include
)#包含头文件库

#可执行文件链接到动态库上
target_link_libraries(kalman_main
PUBLIC
common
)


# #第三方库
# SET(EIGEN3_INCLUDE_DIR "C:/eigen")
# list(APPEND CMAKE_MODULE_PATH "${EIGEN3_INCLUDE_DIR}/cmake")
# message("CMAKE MODULE PATH= ${CMAKE_MODULE_PATH}")

# find_package(Eigen3 3.4 REQUIRED)

# if(TARGET Eigen3::Eigen)
#     message(STATUS "******Eigen3 found in ${EIGEN3_INCLUDE_DIR}")
# endif()

include_directories("C:/eigen")