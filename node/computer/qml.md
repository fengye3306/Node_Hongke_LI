## qml系统架构设计


```qml
my-app/
├── main.qml                  # 主入口文件
│
├── components/               # 可复用组件
│   ├── CustomButton.qml
│   └── Header.qml
├── styles/                   # 样式定义
│   ├── Theme.js
│   └── Colors.js
├── utils/                    # 工具函数
│   ├── Formatters.js
│   └── Validators.js
├── models/                   # 数据模型
│   └── UserModel.js
└── assets/                   # 静态资源
    ├── images/
    └── fonts/
```

> QML 实现类似HTML+CSS加载外部CSS   

```qml
//  创建外部的 JavaScript 样式文件 ： styles.js
const XXStyles = {
    colors: {
        primary: "#3498db",
        secondary: "#2ecc71",
        background: "#ecf0f1"
    },
    sizes: {
        padding: 10,
        fontSize: 16,
        buttonHeight: 40
    },
    fonts: {
        main: "Arial",
        title: "Helvetica"
    }
}

// 导出样式对象
Qt.include("styles.js")

```

```qml
// 在 QML 中使用

import "styles.js" as Style

Rectangle {
    color: Style.colors.background
    width: 100 + Style.sizes.padding * 2
    
    Text {
        font.family: Style.fonts.main
        font.pixelSize: Style.sizes.fontSize
    }
}
```


## qml与qwidget嵌套



## qml实现mvvm架构


    
## qml热调试

qmlscene.exe，支持对qml的渲染，但它并不是实时刷新的。


> 配置felgo实现qml界面的实时刷新

```path
# felgo 下载地址
https://felgo.com/


# qt 提供下载方式 教程
https://felgo.com/doc/felgo-installation/#add-felgo-to-existing-qt-installation

# felgo基础下载安装教程
https://blog.csdn.net/luoyayun361/article/details/103631476
```


## vscode开发插件

* `QML Format` ：代码格式自动优化  

快捷键alt+shift+f

* `QML`：语法提示
* `QML Syntax/Tools`：配置felgo实现qml界面热重载


## 资料库

```link
#########################未归档资料#########################

# qml使用体验
https://www.zhihu.com/question/58326567/answer/3148971386


# Qml嵌入Widget以及Qml与Widget交互
https://zhuanlan.zhihu.com/p/658704300?utm_psn=1856024090122526721
```







## 语法  

> Repeater 组件，重复创建多个项目


```qml
Repeater {
    model: 9 // 表示要创建9个相同的项目
    
    // 在这里定义要重复创建的组件
    Rectangle {
        width: 50
        height: 50
        color: "red"
    }
}
```