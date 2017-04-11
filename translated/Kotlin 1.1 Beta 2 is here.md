---
title: [译]Kotlin 1.1 Beta 2 is here
date: 2017-02-02 23:24:00
author: Dmitry Jemerov
tags:
keywords:
categories: 官方动态
reward: false
reward_title: Have a nice Kotlin!
reward_wechat:
reward_alipay:
source_url: https://blog.jetbrains.com/kotlin/2017/02/kotlin-1-1-beta-2-is-here/
---

我们很高兴地宣布Kotlin 1.1的第二个测试版。请尝试新版本 - 您的反馈对于确保我们可以提供质量版本至关重要。
自从第一个测试版本开始，我们主要关注稳定性，错误修正以及改进此版本的关键重点领域：协同程序支持和JavaScript后端。自1.1 Beta版以来的更改的完整列表可以在更新日志中找到。如果您有兴趣了解1.1版中添加的所有内容，请查看我们的新功能页面。

{% raw %}
<p><span id="more-4562"></span></p>
{% endraw %}

## 迁移说明

对于JavaScript项目，我们更改了标准库的工件名称。而不是kotlin-js-library，现在是kotlin-stdlib-js。当您更新到1.1 beta 2或更新的版本时，您将需要更新您的Maven和Gradle脚本。
除此之外，JavaScript的测试支持类（在kotlin.test中）现在被打包为单独的工件，就像之前为Java版本一样。如果您在JS项目中使用kotlin.test，请添加对kotlin-test-js的依赖。
Kotlin标准库中的协程API已被移动到kotlin.coroutines.experimental包中;如果您在代码中使用了这些API，则需要更新导入。有关这一变化的背景，请参阅Andrey的论坛帖子。
我们还使您的Gradle项目中的实验协同程序支持变得更加容易。您可以将以下代码片段添加到build.gradle中，而不是编辑gradle.properties：

{% raw %}
<p></p>
{% endraw %}

```kotlin
kotlin {
    experimental {
        coroutines 'enable'
    }
}
```

{% raw %}
<p></p>
{% endraw %}

如果您正在使用kotlinx.coroutines库，请将您的依赖关系更新为0.6-beta版本。该库的早期版本与此Kotlin更新不兼容。
## 新功能

我们在此测试版中添加了几个最新功能。这里是最重要的：

* 编译器现在报告一个警告，如果您声明一个扩展名与同一个类的成员具有相同的签名，并且将始终被遮蔽（例如String.length（））
* 传递给通用功能的成员引用的类型推断现在得到很大的改进（KT-10711）
* 减号运算符现在可以与地图一起使用，返回地图的副本，并删除给定的键。 -  =操作符可以在可变地图上使用，以从地图中删除给定的键。
* 现在可以使用KPropertyN.getDelegate（）访问委托属性的委托实例（详见KT-8384）;
* 意图（由Kirill Rakhman贡献）合并两个嵌套if语句;
* 支持在启用Jack工具链时构建Android项目（jackOptions {true}）;
* 意图（由Kirill Rakhman贡献）在Android应用程序中生成View构造函数。

## 源兼容性Kotlin 1.0

在本次更新中我们非常关注的另一个领域是与Kotlin 1.0的源兼容性。这样，即使您的团队使用Kotlin 1.0，您也可以尝试使用Kotlin 1.1，而不用担心通过使用新版本中添加的一些功能来打破构建。
要启用兼容性模式：

* 对于Maven，Ant和命令行编译器，将-language-version编译器参数设置为1.0。
* 在Gradle构建中，将kotlinOptions {languageVersion =“1.0”}添加到您的compileKotlin任务中。
* 在IDE中，在Kotlin facet设置或Settings |中指定语言版本构建，执行，部署|编译器| Kotlin编译器

## 如何尝试

在Maven / Gradle中：添加http://dl.bintray.com/kotlin/kotlin-eap-1.1作为构建脚本和项目的存储库;使用1.1.0-beta-38作为编译器和标准库的版本号。
在IntelliJ IDEA：转到工具→Kotlin→配置Kotlin插件更新，然后在更新频道下拉列表中选择“早期访问预览1.1”，然后按检查更新。
命令行编译器可以从Github发行页面下载。
在try.kotlinlang.org。即将推出。
让我们来吧！