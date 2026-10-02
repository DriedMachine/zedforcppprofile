cmake_minimum_required(VERSION 4.0)

# 1. 定义项目名称和版本
project(
    HelloWorld
    VERSION 1.0
    LANGUAGES C CXX
)

# 2. 设置 C++ 标准
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(SOURCES
    src/main.cpp
)

# 3. 创建可执行文件
# 假设你的源码在 src/main.cpp，请根据实际情况修改
add_executable(${PROJECT_NAME} ${SOURCES})
target_include_directories(${PROJECT_NAME} PRIVATE
    ${PROJECT_SOURCE_DIR}/src
    ${PROJECT_SOURCE_DIR}/include
)

add_library(glad STATIC
    third_party/glad/src/gl.c
)

target_include_directories(glad PUBLIC
    third_party/glad/include
)

# 4. 查找并链接 fmt 库
find_package(fmt CONFIG REQUIRED)
find_package(glfw3 CONFIG REQUIRED)
find_package(OpenGL REQUIRED)

target_link_libraries(${PROJECT_NAME} PRIVATE
    glad
    fmt::fmt
    glfw
    OpenGL::GL
)
