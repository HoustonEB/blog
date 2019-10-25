---
title: react-native
date: 2019-10-22 16:13:42
categories: react-native
tags: 
- react-native
---

## 发版app
1.生成签名密钥
```bash
keytool -genkeypair -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
```
这个命令会在当前目录生成{% label primary@my-release-key.keystore%}文件
2.设置gradle变量
-把{% label primary@my-release-key.keystore%}文件放入android/app文件夹下.
-编辑~/.gradle/gradle.properties（全局配置，对所有项目有效）或是项目目录/android/gradle.properties（项目配置，只对所在项目有效）。
如果没有gradle.properties文件你就自己创建一个，添加如下的代码（注意把其中的****替换为相应密码）
 注意：~符号表示用户目录，比如 windows 上可能是C:\Users\用户名，而 mac 上可能是/Users/用户名。
 ```bash
MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
MYAPP_RELEASE_KEY_ALIAS=my-key-alias
MYAPP_RELEASE_STORE_PASSWORD=*****
MYAPP_RELEASE_KEY_PASSWORD=*****
```
{% note warning %}
一旦你在 Play Store 发布了你的应用，如果想修改签名，就必须用一个不同的包名来重新发布你的应用（这样也会丢失所有的下载数和评分）。所以请务必备份好你的密钥库和密码
{% endnote %}
提示：如果你不想以明文方式保存密码，同时你使用的是 macOS 系统，那么你也可以把密码保存到钥匙串（Keychain）中。这样一来你就可以省略掉上面配置中的后两行（即 MYAPP_RELEASE_STORE_PASSWORD 和 MYAPP_RELEASE_KEY_PASSWORD）
3.生成发行APK包
```bash
cd android
./gradlew assembleRelease
```
Gradle 的assembleRelease参数会把所有用到的 JavaScript 代码都打包到一起，然后内置到 APK 包中。如果你想调整下这个行为（比如 js 代码以及静态资源打包的默认文件名或是目录结构等），可以看看android/app/build.gradle文件，然后琢磨下应该怎么修改以满足你的需求。
注意：请确保 gradle.properties 中没有包含_org.gradle.configureondemand=true_，否则会跳过 js 打包的步骤，导致最终生成的 apk 是一个无法运行的空壳。
生成的 APK 文件位于android/app/build/outputs/apk/release/app-release.apk，它已经可以用来发布了。

4.测试应用的发行版本
在把发行版本提交到 Play Store 之前，你应该做一次最终测试。输入以下命令可以在设备上安装发行版本：
`react-native run-android --variant=release`
注意--variant=release参数只能在你完成了上面的签名配置之后才可以使用。你现在可以关掉运行中的 packager 了，因为你所有的代码和框架依赖已经都被打包到 apk 包中，可以离线运行了。
注意：在 debug 和 release 版本间来回切换安装时可能会报错签名不匹配，此时需要先卸载前一个版本再尝试安装。
## 遇到的问题
1.发版app时报的错误
```bash
Execution failed for task ':app:bundleReleaseJsAndAssets'.
> Could not list contents of '/Users/v_yuzhuang01/Desktop/mobileApp/elm-react-native/node_modules/fsevents/node_modules/.bin/node-pre-gyp'. Couldn't follow symbolic link.
```
解决方法: 删除node_modules,重新npm install
