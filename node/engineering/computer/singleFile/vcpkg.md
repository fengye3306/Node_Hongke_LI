
## vcpkg 使用 


当你执行 `.\vcpkg install duckdb`  

1. vcpkg 下载 DuckDB 源码
2. vcpkg 调用你本地的编译器把源码编译成库
3. 编译产物放到 installed/ 目录

所以，下载源码的版本，编译器的选择, 编译要的版本产出，动态库或静态库的选择  必须在 vcpkg 这边命令行形式指定。  

> **编译器的选择**


查询本地msvc的方法：
```cmd
"C:\Program Files (x86)\Microsoft Visual Studio\Installer\vswhere.exe"
```


通过 **三元组（triplet）** 指定，格式 `包名:三元组`。vcpkg 不会在 install 里切换编译器，编译器由三元组决定。



```shell
x64-windows           # MSVC，动态库（Windows 默认）
x64-windows-static    # MSVC，静态库
x64-mingw-dynamic     # MinGW (GCC)，动态库
x64-mingw-static      # MinGW (GCC)，静态库
```

```shell
.\vcpkg install duckdb:x64-windows
.\vcpkg install duckdb:x64-mingw-dynamic   # 需本机已装 MinGW-w64
```

MSVC 无 `--msvc-version` 参数，使用当前环境里找到的 MSVC（建议在 VS Developer PowerShell 中执行）。要固定工具集可在自定义 triplet 中设置 `VCPKG_PLATFORM_TOOLSET`（如 `v143` = VS 2022）。

> 动态库或者静态库的指定

完全由三元组决定，与包装名无关：

```shell
# 动态库 (.dll + .lib 导入库)
.\vcpkg install duckdb:x64-windows

# 静态库 (.lib)
.\vcpkg install duckdb:x64-windows-static
```

同一项目不要混用不同三元组的依赖，否则链接阶段容易 ABI 冲突。

> 编译版本产出

默认 **Debug 和 Release 都会编译**，装一次两者都有：

```shell
installed/x64-windows/
├── bin/          # .dll — Release
├── debug/bin/    # .dll — Debug
├── lib/          # .lib — Release
├── debug/lib/    # .lib — Debug
└── include/      # 头文件（共用）
```

使用 vcpkg 的 CMake 工具链时，项目的 Debug/Release 配置会自动链接对应版本的库，无需手动区分路径。







## vcpkg 迁移 

## vcpkg下载安装

有问题找AI  

1. 源码仓库clone 
2. 进入 vcpkg 目录，根据你的系统执行对应命令
```shell
#Windows (PowerShell)：
.\bootstrap-vcpkg.bat

#Linux / macOS： 
./bootstrap-vcpkg.sh
```


