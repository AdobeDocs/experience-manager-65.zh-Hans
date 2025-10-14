---
title: 使用PhoneGap CLI开发应用程序
description: 了解如何使用引导式开发环境通过PhoneGap CLI开发适用于移动设备的应用程序。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: fbeceb70-b199-478b-907b-253ed212ff99
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 1%

---

# 使用PhoneGap CLI开发应用程序{#developing-apps-with-phonegap-cli}

{{ue-over-mobile}}

在任何指定时间，作为开发人员，您可以在设备上或模拟器中运行应用程序，前提是您已配置开发环境。

要运行以下示例，您需要运行带有Xcode的macOS X的系统，或者运行带有Android™ SDK的Mac/Win/Linux系统。

## Bootstrap开发环境 {#bootstrap-your-development-environment}

设置PhoneGap CLI (`https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface`)

对于iOS：要针对iPhone和iPad进行开发，您需要Apple的Xcode IDE。

* 在[此处](https://idmsa.apple.com/IDMSWebAuth/signin?appIdKey=891bd3417a7776362562d2197f89480a8547b108fd934911bcbea0110d07f757&path=%2Fdownload%2F&rv=1)免费下载。
* PhoneGap iOS平台指南(`https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide`)

对于Android™：要针对iPhone和iPad进行开发，您需要Google的Android™ Stuido IDE。

* 在[此处](https://developer.android.com/studio)免费下载。
* PhoneGap Android™平台指南(`https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide`)

## 下载Source {#download-the-source}

成功引导开发环境后，请从AEM App Build拼贴下载源：

* 单击PhoneGap Build拼贴下拉式V形。

![chlimage_1-45](assets/chlimage_1-45.png)

* 单击下载Source。
* 从下载Source模式中选择所需的源。

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>开发源包含应用程序的最新状态，同时包含未暂存的更改。 使用暂存源构建候选版本，以提交到应用商店供应商。
>
>如果从未暂存应用程序，则选择暂存将触发暂存工作流(提示：在AppStore和Google PlayStore提供的PhoneGap Enterprise Viewer应用程序中显示为暂存应用程序)。

* 单击“Download（下载）”并将ZIP文件保存到您的计算机。
* 将下载的zip文件解压到工作区。

## 构建和加载应用程序（从源） {#build-and-load-the-app-from-source}

PhoneGap CLI可以通过单个命令创建平台项目、编译源以及部署应用程序。

>[!NOTE]
>
>您可以单独执行所有这些步骤，请参阅PhoneGap CLI文档(`https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/`)。

1. 确保您已安装PhoneGap CLI，请参阅上文。
1. 在控制台（或终端）窗口中，导航到已提取源的根目录。
1. 输入以下命令：

```xml
phonegap run android

// -- or -- //

phonegap run ios
```

>[!NOTE]
>
>如果此时遇到问题，请返回到基础知识以进行故障排除 — 
>
>1. 创建文件夹（mkdir测试）
>1. 导航到此新文件夹（cd测试）
>1. 运行`phonegap create helloWorld`
>1. 导航到helloWorld (cd helloWorld)
>1. 运行`phonegap run android`(或将Android™替换为iOS，如上所述)。
>1. 运行新创建的PhoneGap应用程序时，模拟器会打开，并显示“设备就绪”(如果JavaScript Bridge to native可运行)。
>
>此故障排除可验证您的PhoneGap CLI开发环境是否正常运行。

## 使用Safari和IOS Debug调试JavaScript {#debug-javascripts-with-safari-and-ios-debug}

您可以像调试Web应用程序一样，使用Safari的开发人员工具调试应用程序的JavaScript。

## 启用Safari开发人员工具 {#enable-safari-developer-tools}

要启用开发人员工具：

* 打开Safari的偏好设置

   * 单击菜单栏中的Safari
   * 单击“首选项”

* 在“首选项”窗口中单击“高级”

![chlimage_1-47](assets/chlimage_1-47.png)

* 选中“在菜单栏中显示开发菜单”
* 关闭首选项窗口

## 将Safari连接到iOS {#connect-safari-to-ios}

您可以将Safari连接到iOS设备或模拟器。

* 在控制台窗口中，导航到已提取源的根目录。
* 输入以下命令，以便在设备或仿真器上启动应用程序。

```xml
phonegap run <platform> --device

// -- or -- //

phonegap run <platform> --emulator
```

* 打开Safari
* 单击菜单栏中的开发
* 选择iOS Simulator子菜单
* 单击home.html

![chlimage_1-48](assets/chlimage_1-48.png)

## 使用Safari的Web检查器调试JavaScript {#debug-javascript-with-safari-s-web-inspector}

您可以在源中的任意位置设置断点。 当您与模拟器或设备交互时，应用程序的运行将在这些断点处停止。 您可以逐步完成运行并检查变量中的值。

* 在Web检查器窗口中单击资源
* 导航源树并单击所需的源文件
* 单击添加断点旁边的行号
* 与设备或模拟器交互

![chlimage_1-49](assets/chlimage_1-49.png)

* 使用控制按钮继续执行、逐步、单步执行或逐出方法：

![水平行中有五个功能不同的控件按钮对齐。](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
>要查看当前方法中变量的值，请将鼠标悬停在上。

## 后续步骤 {#the-next-steps}

了解如何使用PhoneGap CLI开发应用后，请参阅[访问设备功能](/help/mobile/phonegap-access-device-features.md)。
