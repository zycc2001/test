## c++的配置文件

```c++
cpp.json
{
    "configurations": [
        {
            "name": "MinGW64",
            "intelliSenseMode": "gcc-x64",
            "compilerPath": "C:\\MinGW\\bin\\g++.exe",
            "includePath": [
                "${workspaceFolder}"
            ],
            "cppStandard": "c++17"
        }
    ],
    "version": 4
 }
```

```c++
launch.json
    
{  
    "version": "0.2.0",  
 "configurations": [  
        {  
         "name": "(gdb) Launch", // 配置名称，将会在启动配置的下拉菜单中显示  
            "type": "cppdbg",       // 配置类型，这里只能为cppdbg  
         "request": "launch",    // 请求配置类型，可以为launch（启动）或attach（附加）  
            "program": "${workspaceFolder}/${fileBasenameNoExtension}.exe",// 将要进行调试的程序的路径  
            "args": [],             // 程序调试时传递给程序的命令行参数，一般设为空即可  
            "stopAtEntry": false,   // 设为true时程序将暂停在程序入口处，一般设置为false  
         "cwd": "${workspaceFolder}", // 调试程序时的工作目录，一般为${workspaceFolder}即代码所在目录  
            "environment": [],  
         "externalConsole": true, // 调试时是否显示控制台窗口，一般设置为true显示控制台  
            "MIMode": "gdb",  
         "miDebuggerPath": "C:\\MinGW\\bin\\gdb.exe", // miDebugger的路径，注意这里要与MinGw的路径对应  
            "preLaunchTask": "g++", // 调试会话开始前执行的任务，一般为编译程序，c++为g++, c为gcc  
         "setupCommands": [  
                {   
            "description": "Enable pretty-printing for gdb",  
                    "text": "-enable-pretty-printing",  
                    "ignoreFailures": true  
                }  
            ]  
        }  
    ]  
}
```

```c++
tasks.json
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558 
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "type": "shell",
            "label": "g++", //这里注意一下，见下文
            "command": "C:\\MinGW\\bin\\g++.exe",
            "args": [
                "-g",
                "${file}",
                "-o",
                "${fileDirname}\\${fileBasenameNoExtension}.exe",
                "-ggdb3",   // 生成和调试有关的信息
                "-Wall",    // 开启额外警告
                "-static-libgcc",   // 静态链接
                "-std=c++17",       // 使用c++17标准
                "-finput-charset=UTF-8",    //输入编译器文本编码 默认为UTF-8
                "-fexec-charset=GB18030",   //输出exe文件的编码
                "-D _USE_MATH_DEFINES"
            ],
            "options": {
                "cwd": "C:\\MinGW\\bin"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "presentation": {
                "echo": true,
                "reveal": "always", // 在“终端”中显示编译信息的策略，可以为always，silent，never
                 "focus": false,
                 "panel": "shared" // 不同的文件的编译信息共享一个终端面板
            },
        }
    ]
}

```

## vscode配置java

1.先配置`jdk`在系统环境变量中

2.在`vscode`中搜索`java`

![img](E:\Program Files (x86)\有道云\有道云文件保存\qq2B377EA9EDDC0065ACBC1677361811C3\37380f438a2e4169a49d4e1d55556363\clipboard.png)

找到这个点击进去

![img](E:\Program Files (x86)\有道云\有道云文件保存\qq2B377EA9EDDC0065ACBC1677361811C3\34b27ba3a4da4ba6951f05a9eba90225\clipboard.png)

自行选择

![img](E:\Program Files (x86)\有道云\有道云文件保存\qq2B377EA9EDDC0065ACBC1677361811C3\991d4ee242184f5a80582f71686c3165\clipboard.png)

然后`vscode`中打开一个文件

`shift+Ctrl+p`打开命令行输入

![img](E:\Program Files (x86)\有道云\有道云文件保存\qq2B377EA9EDDC0065ACBC1677361811C3\9343c926a1b34ec1b56a6b33b97c37ca\clipboard.png)

点击创建项目

![img](E:\Program Files (x86)\有道云\有道云文件保存\qq2B377EA9EDDC0065ACBC1677361811C3\e44ca0c7c26f445295c5cde042495191\clipboard.png)

选`No build tools `选其他的没试过

​	如何在用`vscode`在命令行输出

1.点击左下角的设置

![img](E:\Program Files (x86)\有道云\有道云文件保存\qq2B377EA9EDDC0065ACBC1677361811C3\7da52225d4784fb0873794187ce0985e\clipboard.png)

![img](E:\Program Files (x86)\有道云\有道云文件保存\qq2B377EA9EDDC0065ACBC1677361811C3\c0cc6d8bdfb84c679855e90a79c1989f\clipboard.png)

![img](E:\Program Files (x86)\有道云\有道云文件保存\qq2B377EA9EDDC0065ACBC1677361811C3\c202c5eb1cc94c429afee9aa6f54a837\clipboard.png)

添加红框语句，当添加到其他语句间时注意加","

![img](E:\Program Files (x86)\有道云\有道云文件保存\qq2B377EA9EDDC0065ACBC1677361811C3\117332992ed8490ca34bad6a77ba3d06\clipboard.png)

第一个就是控制台输出

第二个是`vscode`自己的

第三个是`eclipse`的面板，但是不支持输入。