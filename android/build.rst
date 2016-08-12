aapt 生成 R.java 和编译后的资源文件

aidl 转换成 Java Interfaces 文件

.dex 和编译后的资源文件 apkbuilder 转换成 .apk

jarsigner

build.gradle

compileSdkVersion
buildToolsVersion

Gradle
==============================

gradle tasks
gradle projects
gradle dependencies
gradle properties

gradle -q
gradle --profile

依赖管理
---------------------------------

dependencies
publications

配置
------------------------------

gradle.properties 当前项目
gradle.properties user home
-Dsome.property

org.gradle.daemon
org.gradle.java.home
org.gradle.jvmargs

代理配置
systemProp.http.proxyHost=www.somehost.org
systemProp.http.proxyPort=8080
systemProp.http.proxyUser=userid
systemProp.http.proxyPassword=password
systemProp.http.nonProxyHosts=*.nonproxyrepos.com|localhost

systemProp.https.proxyHost=www.somehost.org
systemProp.https.proxyPort=8080
systemProp.https.proxyUser=userid
systemProp.https.proxyPassword=password
systemProp.https.nonProxyHosts=*.nonproxyrepos.com|localhost


build 脚本
==============================

task hello << {
}

task world(dependsOn: hello) << {
}

hello.doFirst {
}
hello << {
}

初始化命令

gradle init --type java-library

当构建项目时，Gradle 创建 Project 对象，如果属性或方法没有定义，则由 Project 对象代理。

project 对象属性：

project 自身
name 项目目录名
path 绝对路径
description 说明
projectDir 项目路径
buildDir 项目路径/build
group
version
ant

Task
==============================

task (hello) << {
}
task(copy, type: Copy) {
}
tasks.create(name: 'copy', type: Copy) {
}

tasks['hello']
tasks.getByPath(':hello')

更新检查 inputs, outputs

API
==============================

Project.file 查询项目文件
Project.files 
Project.fileTree

copy
rename
filter() 可使用 closure 或过滤
expand( vars ) 使用模板

LifeCycle
==============================

initialization

configuration

execution

settings.gradle 在 initialization 阶段执行。

artifactory
==============================

1. 如果 artifactory 下载失败，会有缓存，如果希望重新下载，清除缓存
Admin -> Repositories -> Remote 选择 jcenter, Advanced 中将 Missed Retrieval Cache Period 设置为 0

2. gradle 对未成功下载也会有缓存，可通过加参数 --refresh-dependencies 参数刷新

