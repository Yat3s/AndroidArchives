# AndroidArchives
Collect some questions and troubles in android. hope it can help  u ~

**You can search and quick find your answer**
**你可以搜索(cmd+f/ctrl+f)关键字来快速找到你的问题**

## Gradle
**1. 如何加快Gradle编译速度** `编译速度` `Gradle编译` `Gradle加速`
>- 尽可能的使用最新版本IDE的**Instant run**来调试你的项目。
>- 请随手开启Android Studio的**offline**模式。
>- 在你确保你的混淆没问题的情况下在debug模式下关闭所有混淆**minifyEnabled false, shrinkResources false**。
>- 尽可能的让你的所有module的同一个依赖库版本一致。
>- 如果不想开offline模式的话在添加依赖的时候尽量明确版本号，省去gradle查找最新版的时间，**尽量不要compile ‘com.facebook.fresco:fresco:latest’ 或compile ‘com.facebook.fresco:fresco:1.+’**。
>- 开启守护线程并行编译，并尽可能的加大你的编译在gradle.properties中添加
**org.gradle.parallel=true**
**org.gradle.daemon=true**。
>- 在debug模式下build尽可能的不要在gradle里面写任务（比如获取git revision/date/version name等等参数），你可以在你的耗时任务之前加一个判断：
**if (!System.getenv('CI_BUILD')) {**
	    **return 0**
 **}**
 来跳过当前任务（假设你在debug下不用到该值）。
 >- 如果在用Shadowsocks的话可以给Android studio也加上proxy来加快Gradle的下载，**在preference里面修改http Proxy方式为socks并且设置ip：127.0.0.1， 端口1080**，也就是用本机来代理。
 >- 用Gradle下载一些新的库时候，如果觉得慢你可以建立另外一个新的project， 在另外一个新的project来下载你所需要的库，下载好了开启offline模式一键同步到你当前开发的工程，再也不用浪费时间在等库下载了。
 >- 如果你电脑够fast够niubility就尽可能的加大你的VM options，在AS的help--Edit Custom VM Options里面修改（量力而行）：
 **-Xms2048m **
 **-Xmx2048m **
 **-XX:MaxPermSize=2048m **
 **-XX:ReservedCodeCacheSize=1024m **
 **-XX:+UseCompressedOops **。

**refer to**: [stackoverflow >> building-and-running-app-via-gradle-and-android-studio-is-slower-than-via-eclips](http://stackoverflow.com/questions/16775197/building-and-running-app-via-gradle-and-android-studio-is-slower-than-via-eclips/17286002#17286002)



----
## Dialog

**1. 如何设置Dialog的背景为透明?**`dialog` `dialog透明` `背景透明`  
> 重写dialog，然后调用执行**getWindow().setBackgroundDrawableResource(R.color.transparent)**
