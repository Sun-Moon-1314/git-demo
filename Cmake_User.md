# CMake使用说明
[CMake视频讲解](https://youtu.be/maDhQ57-gr8)

## 一. cmake原理
- CMake 是一个跨平台的构建工具，主要用于管理软件项目的编译过程。通过简单的配置文件（CMakeLists.txt），它可以生成本地构建系统（如 Makefile 或 Visual Studio 项目文件）。
- **输入配置文件**：CMake 使用 CMakeLists.txt 文件作为输入，定义项目的构建规则、依赖关系和目标。
- **生成构建系统**：CMake 解析 CMakeLists.txt 文件后，根据目标平台生成相应的构建系统文件，例如在 Linux 上生成 Makefile，在 Windows 上生成 Visual Studio 项目文件。
- **构建过程**：
  - 用户运行 CMake 命令生成构建系统。
  - 使用生成的构建系统（如 make 或 Visual Studio）进行编译、链接和生成可执行文件或库。
- **跨平台支持**：CMake 提供了统一的接口，屏蔽了不同平台构建工具的差异，使得开发者可以更方便地在多个平台上构建项目。
- **模块化和可扩展性**：CMake 支持模块化配置，可以通过自定义模块扩展其功能。

## 二. 使用命令以及步骤

1. **安装 CMake**
   - 在 macOS 上可以通过 Homebrew 安装：
     ```bash
     brew install cmake
     ```

2. **创建 CMakeLists.txt 文件**
   - 在项目根目录下创建一个名为 `CMakeLists.txt` 的文件，定义项目的构建规则。

### 示例 1：简单的 main.cpp
```cmake
# 指定 CMake 的最低版本要求。
cmake_minimum_required(VERSION 3.10)

# 定义可执行文件及其源文件。
project(SimpleProject)

# 设置 C++ 标准。
set(CMAKE_CXX_STANDARD 11)

# 普通情况
add_executable(SimpleExecutable main.cpp)

# 如果目录层次比较深
set(SOURCE_DIR src/app) # 定义源文件目录
add_executable(SimpleExecutable ${SOURCE_DIR}/main.cpp)
```

### 示例 2：main.cpp 与 main.h 分离
```cmake
cmake_minimum_required(VERSION 3.10) 

project(HeaderProject)

set(CMAKE_CXX_STANDARD 11) 

add_executable(HeaderExecutable main.cpp main.h) 
```

### 示例 3：main.cpp、main.h 和第三方库
```cmake
cmake_minimum_required(VERSION 3.10)

project(ThirdPartyProject)

set(CMAKE_CXX_STANDARD 11)

find_package(SomeLibrary REQUIRED) # 查找并加载第三方库。

add_executable(ThirdPartyExecutable main.cpp main.h) # 定义一个可执行文件 
ThirdPartyExecutable，并指定其源文件为 main.cpp 和 main.h。

target_link_libraries(ThirdPartyExecutable SomeLibrary::SomeLibrary) # 链接第三方库到可执行文件。
```

### 示例 4：多层级目录
```cmake
cmake_minimum_required(VERSION 3.10)

project(MultiLevelProject)

set(CMAKE_CXX_STANDARD 11)

add_executable(MainExecutable main.cpp)

add_subdirectory(algorithms) # 添加子目录并处理其 CMakeLists.txt。

target_link_libraries(MainExecutable AlgorithmsLibrary) # 链接子目录生成的库到主可执行文件。
```

#### 子目录 algorithms/CMakeLists.txt
```cmake
cmake_minimum_required(VERSION 3.10)

add_library(AlgorithmsLibrary astar.cpp astar.h) # 定义库及其源文件。

find_package(SomeLibrary REQUIRED) # 查找并加载第三方库。
target_link_libraries(AlgorithmsLibrary SomeLibrary::SomeLibrary) # 链接第三方库到库文件。
```

3. **运行 CMake 生成构建系统**
   - 在终端中进入项目目录，运行以下命令生成构建系统：
     ```bash
     cmake -S . -B build
     ```
     - `-S .` 指定源代码目录。
     - `-B build` 指定生成的构建系统存放目录。

   - 或者
     ```bash
     mkdir build
     cd build
     cmake ..
     ```
     
     - **区别**：
       - `cmake -S . -B build` 不需要切换目录，直接在项目根目录运行即可，适合脚本化和自动化构建。
       - 进入 `build` 目录后运行 `cmake ..` 需要手动切换到 `build` 目录，`..` 表示源代码目录是 `build` 目录的上一级目录，适合手动操作。
       - 两者功能等价，但 `-S` 和 `-B` 的方式更现代化，推荐使用。

4. **构建项目**
   - 使用生成的构建系统进行编译：
     ```bash
     cmake --build build
     ```
   - **不同平台的构建示例**：
     - 三个系统普通构建都一样：
         ```bash
         cmake -S . -B build
         cmake --build build
         ```
     - **Windows 系统**：
       - 使用 Visual Studio 构建：
         ```shell
         # 主目录运行
         cmake -S . -B build -G "Visual Studio 17 2022"
         # build命令运行
         cmake .. -G "Visual Studio 17 2022"
         - S .：指定源代码目录为当前目录（.）。
         - B build：指定生成的构建系统存放在 build 目录中。
         - G "Visual Studio 16 2019"：指定生成器为 Visual Studio 2019，生成适用于 Visual Studio 的项目文件。
         使用该方式构建需要使用vs运行，如果想直接运行就不指定目标。

         如果在子目录中存在多个文件，但其中有几个不需要,就使用: 
         file(GLOB ...)
         ```

         <img width="1315" alt="截屏2025-04-14 11 48 26" src="picture/截屏2025-04-19 14.04.00.png" />

         ```
         cmake --build build --config Release
         --build build：使用 build 目录中的构建系统进行编译。
         --config Release：指定构建配置为 Release 模式（优化后的版本，适合发布）。
         ```

         ```shell
         Remove-Item -Path ".\build\*"
         ```

     - **macOS 系统**：
       - 使用 Xcode 构建：
         ```bash
         cmake -S . -B build -G "Xcode"
         cmake --build build --config Release
         ```


5. **运行生成的可执行文件**
   - 进入构建目录并运行生成的可执行文件：
     ```bash
     cd build
     ./<可执行文件名>
     或者
     ./build/<可执行文件名>
     ```

6. **清理构建文件**
   - 如果需要清理构建文件，可以删除 `build` 目录：
     ```bash
     rm -rf build
     ```
   - 保留build文件夹，删除build里面的文件
     ```bash
     rm -rf build/*
     ```

## 三. 常用 CMake 命令

1. **生成构建系统**
   ```bash
   cmake -S . -B build
   ```
   - 指定源代码目录和构建目录，生成构建系统。

2. **构建项目**
   ```bash
   cmake --build build
   ```
   - 使用生成的构建系统进行编译。

3. **清理构建目录**
   - 删除整个构建目录：
     ```bash
     rm -rf build
     ```
   - 仅删除构建目录中的内容：
     ```bash
     rm -rf build/*
     ```
     Windows中使用
     ```shell
      Remove-Item -Path ".\build\*"
     ```
4. **指定构建类型**
   ```bash
   cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
   ```
   - 指定构建类型为 Release（优化后的版本）。
   - 其他可选值：`Debug`、`RelWithDebInfo`、`MinSizeRel`。

5. **重新配置项目**
   ```bash
   cmake -S . -B build
   ```
   - 如果修改了 `CMakeLists.txt`，需要重新运行此命令以更新构建系统。

6. **安装项目**
   ```bash
   cmake --install build
   ```
   - 安装构建的目标到指定的安装目录（需在 `CMakeLists.txt` 中配置 `install` 规则）。

7. **生成特定生成器的构建系统**
   - 使用 Ninja：
     ```bash
     cmake -S . -B build -G "Ninja"
     ```
   - 使用 Unix Makefiles：
     ```bash
     cmake -S . -B build -G "Unix Makefiles"
     ```

8. **检查 CMake 版本**
   ```bash
   cmake --version
   ```
   - 查看当前安装的 CMake 版本。

9. **显示帮助信息**
   ```bash
   cmake --help
   ```
   - 显示 CMake 的帮助信息和可用选项。