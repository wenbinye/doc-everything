开发环境
==============================

android sdk 安装
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. 启动 Android SDK Manager
2. 打开主界面，依次选择 Tools -> Options...，弹出 Android SDK Manager - Settings 窗口
3. 在 HTTP Proxy Server 和 HTTP Proxy Port 输入框内填入 mirrors.neusoft.edu.cn 和 80，并且选中 ``Force https://... sources to be fetched using http://...`` 复选框
4. 设置完成后单击 Close 按钮关闭窗口返回到主界面
5. 依次选择 Packages -> Reload

其它镜像： mirrors.opencas.cn

linux 可修改 ``~/.android/androidtool.cfg`` ::

    http.proxyHost=mirrors.neusoft.edu.cn
    http.proxyPort=80
    sdkman.ask.adb.restart=false
    sdkman.enable.previews=false
    sdkman.force.http=true
    sdkman.show.update.only=true
    sdkman.use.dl.cache=true

参考 http://blog.csdn.net/singleton1900/article/details/12911333

gradle 安装
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

下载 gradle-2.3 解压缩，设置 GRADLE_HOME 和 PATH 环境变量

https://spring.io/guides/gs/gradle-android/
