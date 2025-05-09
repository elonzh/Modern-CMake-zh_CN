# CMake 行为准则(Do's and Don'ts)

## CMake 应避免的行为

接下来的两个列表很大程度上基于优秀的 gist [Effective Modern CMake]. 那个列表更长且更详细，也非常欢迎你去仔细阅读它。

* **不要使用具有全局作用域的函数**：这包含 `link_directories`、 `include_libraries` 等相似的函数。
* **不要添加非必要的 PUBLIC 要求**：你应该避免把一些不必要的东西强加给用户（-Wall）。相比于 **PUBLIC**，更应该把他们声明为 **PRIVATE**。
* **不要在file函数中添加 GLOB 文件**：如果不重新运行 CMake，Make 或者其他的工具将不会知道你是否添加了某个文件。值得注意的是，CMake 3.12 添加了一个 `CONFIGURE_DEPENDS` 标志能够使你更好的完成这件事。
* **将库直接链接到需要构建的目标上**：如果可以的话，总是显式地将库链接到目标上。
* **当链接库文件时，不要省略 PUBLIC 或 PRIVATE 关键字**：这将会导致后续所有的链接都是缺省的。


## CMake 应遵守的规范

* **把 CMake 程序视作代码**：它是代码。它应该和其他的代码一样，是整洁并且可读的。
* **建立目标的观念**：你的目标应该代表一系列的概念。为任何需要保持一致的东西指定一个 （导入型）INTERFACE 目标，然后每次都链接到该目标。
* **导出你的接口**：你的 CMake 项目应该可以直接构建或者安装。
* **为库书写一个 Config.cmake 文件**：这是库作者为支持客户的体验而应该做的。
* **声明一个 ALIAS 目标以保持使用的一致性**：使用 `add_subdirectory` 和 `find_package` 应该提供相同的目标和命名空间。
* **将常见的功能合并到有详细文档的函数或宏中**：函数往往是更好的选择。
* **使用小写的函数名**： CMake 的函数和宏的名字可以定义为大写或小写，但是一般都使用小写，变量名用大写。
* **使用 `cmake_policy` 和/或 限定版本号范围**： 每次改变版本特性 (policy) 都要有据可依。应该只有不得不使用旧特性时才降低特性 (policy) 版本。




[Effective Modern CMake]: https://gist.github.com/mbinna/c61dbb39bca0e4fb7d1f73b0d66a4fd1
