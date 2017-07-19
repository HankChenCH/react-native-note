# React-native 学习笔记之一 安装运行环境（windows）
* 必须安装的程序
 1. Ptyhon2（3暂时不支持）
 2. Node.js
 3. JDK
 4. Android Studio
 5. Git
* 安装步骤
 1. 从[ptyhon官网](https://www.python.org/)下载对应版本安装程序。安装完毕后，配置计算机环境变量（[如何配置环境变量](http://jingyan.baidu.com/article/3ea51489e1c2b752e61bbad0.html)）。
 2. 从[node中文网](http://nodejs.cn/)下载对应版本安装程序。安装完毕后打开命令行（win键 + R，输入cmd进入）
 3. 使用以下命令`npm install -g nrm`,安装nrm工具用来切换npm安装源（原生源速度很慢）。命令行输入调用`nrm ls`查看可切换的源，输入`nrm use taobao`切换淘宝源
 4. 继续输入`npm install -g yarn react-native`安装本文主角
 5. 从[官网](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)下载JDK并安装
 6. 从[android studio官网](http://developer.android.com/sdk/index.html)下载并安装Android Studio（可能会被墙，自备梯子）
 7. 安装完成Android Studio后，进入SDK Manager页面，如下图![](http://otbs2h7e2.bkt.clouddn.com/study_react_native1.png)在SDK Platforms里点击Show Package Details选择Android SDK Platform 23，如下图![](http://otbs2h7e2.bkt.clouddn.com/study_react_native2.png)在SDK Tools里同样点击Show Package Details选择23.0.1和Android Support Repository，如下图![](http://otbs2h7e2.bkt.clouddn.com/study_react_native3.png)待所有SDK下载完毕后，将SDK所在目录新建环境变量ANDROID_HOME中，另外将SDK文件夹里的tools目录和platform-tools目录配置到计算机环境变量中去。
 8. 所有程序文件安装完毕和配置环境变量后，开始新建第一个app。打开命令行输入`react-native init myApp`（请耐性等候），待命令运行完毕，进入到app目录，执行`react-native run-android`（请耐心等候，且不要关闭自动打开的命令行）。待如下图出现，证明程序成功运行，开始愉快的app开发之旅吧！![](http://otbs2h7e2.bkt.clouddn.com/study_react_native4.png)
***
安装过程中可能遇到的坑在这里补充：
    