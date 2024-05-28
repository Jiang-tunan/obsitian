# CMakeLists.txt
`CMakeLists.txt` 是 CMake 的配置文件，用于指定项目的构建过程。以下是一个基本的 `CMakeLists.txt` 文件的示例，适用于一个简单的 C++ 项目：

```cmake
# 设置 CMake 最低版本
cmake_minimum_required(VERSION 3.10)

# 设置项目名称和版本
project(MyProject VERSION 1.0)

# 指定 C++ 标准
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# 添加源文件
set(SOURCES
    src/main.cpp
    src/foo.cpp
    src/bar.cpp
)

# 生成可执行文件
add_executable(MyProject ${SOURCES})

# 包含目录
target_include_directories(MyProject PRIVATE include)

# 链接库（如果有需要）
# target_link_libraries(MyProject PRIVATE some_library)

# 添加自定义命令或自定义目标（如果需要）
# add_custom_command(TARGET MyProject POST_BUILD COMMAND ${CMAKE_COMMAND} -E copy ...)

```
### 解释

1. **cmake_minimum_required(VERSION 3.10)**：指定所需的最低 CMake 版本。
2. **project(MyProject VERSION 1.0)**：定义项目名称和版本。
3. **set(CMAKE_CXX_STANDARD 11)** 和 **set(CMAKE_CXX_STANDARD_REQUIRED True)**：指定 C++ 标准版本（这里是 C++11）并要求使用该标准。
4. **set(SOURCES ...)**：定义项目的源文件。
5. **add_executable(MyProject ${SOURCES})**：将源文件生成一个名为 `MyProject` 的可执行文件。
6. **target_include_directories(MyProject PRIVATE include)**：指定包含目录，这里假设头文件在 `include` 目录中。
7. **target_link_libraries(MyProject PRIVATE some_library)**：如果需要链接外部库，可以使用这条命令。
8. **add_custom_command** 或 **add_custom_target**：如果需要在构建过程中执行额外的命令或目标，可以使用这些命令。

这是一个基本的示例，根据项目的复杂程度，可能需要添加更多的配置，例如处理多个子目录、添加单元测试、配置安装规则等。
