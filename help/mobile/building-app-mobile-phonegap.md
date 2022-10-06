---
title: 构建移动设备应用程序
seo-title: Building Mobile Applications
description: 本页提供了有关如何使用GitHub中提供的代码构建移动应用程序的完整分步文章。请将应用程序构建到设备或模拟器以进行测试或发布到应用商店。 您可以使用PhoneGap命令行界面在本地构建应用程序，或使用PhoneGap Build在云中构建应用程序。
seo-description: This page provides a complete step-by-step article on how to build a mobile application using code available from GitHub is available here.Build your application to install to a device or simulator for testing or for publishing to app stores. You can build applications locally using the PhoneGap Command Line Interface, or in the cloud using PhoneGap Build.
uuid: 1ff6fe1a-24cc-4973-a2cd-8d356bc649b0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b2778086-8280-4306-bf3a-f6ec2a0e04df
exl-id: 7c2e5ed8-9f8e-4a81-b736-589ef4089f29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 1%

---

# 构建移动设备应用程序{#building-mobile-applications}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

构建应用程序以安装到设备或模拟器以进行测试或发布到应用商店。 您可以使用PhoneGap命令行界面在本地构建应用程序，或使用PhoneGap Build在云中构建应用程序。

有关如何使用GitHub中提供的代码构建移动应用程序的完整分步文章 [此处](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html).

## 将应用程序移动到发布实例 {#moving-the-application-to-the-publish-instance}

将应用程序文件移动到发布实例，以便您能够为移动设备应用程序的已安装实例提供内容更新，并使用发布的内容构建应用程序。 应用程序由存储库中的两个节点分支组成：

* `/content/phonegap/apps/<application name>`:作者创建和激活的网页。
* `/content/phonegap/content/<application name>`:应用程序配置文件和内容同步配置。

>[!NOTE]
>
>如果不将应用程序文件移动到发布实例，内容作者将无法更新内容同步缓存。

您只需在 `/content/phonegap/content/<application name>` 分支到发布实例。 中的文件 `/content/phonegap/apps/<application name>` 分支会在作者激活页面时进行移动。

AEM提供了两种将批量内容移动到发布实例的方法：

* [使用激活树命令](/help/sites-authoring/publishing-pages.md) 在复制控制台上。
* [创建资源包](/help/sites-administering/package-manager.md) ，其中包含内容和复制包。

例如，将创建名为phonegapapp的移动应用程序。 必须将以下节点移动到发布实例：/content/phonegap/content/phonegapp。

**提示：** 要将包从创作实例移动到发布实例，请使用包上的Replicate命令。

![chlimage_1-16](assets/chlimage_1-16.png)

## 使用PhoneGap命令行界面构建 {#building-using-the-phonegap-command-line-interface}

使用PhoneGap命令行界面(CLI)在计算机上编译PhoneGap应用程序。 要将AEM内容包含到您的应用程序中，AEM会创建一个ZIP文件，其中包含移动应用程序内容、内容同步配置和其他必需资产。 下载ZIP文件并将其包含在内部版本中。

### 准备构建环境 {#preparing-your-build-environment}

要使用PhoneGap CLI进行构建，您需要安装Node.js和PhoneGap客户端实用程序。 您需要Internet连接才能执行以下过程。

1. 下载并安装 [Node.js](https://nodejs.org/).
1. 打开终端或命令提示符，然后输入以下节点命令以安装PhoneGap实用程序：

   ```shell
   npm install -g phonegap
   ```

   在Unix或Linux系统上，可能需要为命令添加前缀 `sudo`.

   终端显示一系列HTTPGET命令的结果。 安装成功后，终端会显示库的安装位置，如下例所示：

   ```xml
   /usr/local/bin/phonegap -> /usr/local/lib/node_modules/phonegap/bin/phonegap.js
   phonegap@3.3.0-0.19.6 /usr/local/lib/node_modules/phonegap
   ├── pluralize@0.0.4
   ├── colors@0.6.0-1
   ├── semver@1.1.0
   ├── qrcode-terminal@0.9.4
   ├── shelljs@0.1.4
   ├── optimist@0.6.0 (...)
   ├── prompt@0.2.11 (...)
   ├── phonegap-build@0.8.4 (...)
   ├── connect-phonegap@0.8.1 (...)
   └── cordova@3.3.0-0.1.1 (...)
   ```

1. （可选）获取您定位的移动平台的SDK:

   * 要为iOS平台构建应用程序，请安装 [Xcode](https://developer.apple.com/xcode/).
   * 要构建Android应用程序，请安装 [Android SDK](https://developer.android.com/).

### 下载内容ZIP文件 {#downloading-the-content-zip-file}

将移动应用程序的内容移动到文件系统。

1. 在“移动设备应用程序”页面上，选择您的应用程序。
1. （可选）要构建应用程序以完成安装，请在工具栏中单击或点按清除缓存图标。

   ![](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >缓存中包含已安装应用程序的内容更新。 清除缓存会撤消所有缓存的更新。

1. 在工具栏中，单击或点按下载CLI资产图标。

   ![](do-not-localize/chlimage_1-1.png)

1. 保存ZIP文件后，单击成功对话框中的关闭。
1. 解压缩ZIP文件的内容。

### 使用PhoneGap CLI构建 {#using-the-phonegap-cli-to-build}

使用PhoneGap CLI编译和安装应用程序。 有关如何使用PhoneGap CLI的信息，请参阅PhoneGap [命令行界面](https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html) 文档。

1. 打开终端或命令提示符，并将当前目录更改为下载的应用程序ZIP文件。 例如，以下内容会将目录更改为ng-app-cli.1392137825303.zip文件：

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. 输入所定向平台的phonegap命令。 例如，以下命令构建适用于Android的应用程序：

   ```shell
   phonegap build android
   ```

## 使用PhoneGap Build构建 {#building-using-phonegap-build}

使用PhoneGap云服务构建您的应用程序。 要执行此过程，必须先创建PhoneGap Build配置。

### 正在连接到 PhoneGap Build {#connecting-to-phonegap-build}

创建PhoneGap Build配置，以便您能够从AEM中使用PhoneGap Build服务。 提供用于构建移动应用程序的PhoneGap Build帐户的用户名和密码。

1. 打开“工具”页面。 ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))。
1. 在“CQ操作”区域，单击Cloud Services。
1. 单击立即配置链接以获取PhoneGap Build。

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. 在创建配置对话框中，为标题属性键入一个值。 默认情况下，Name属性的值是从标题派生的，但您可以输入名称。 单击创建。
1. 在“PhoneGap Build配置”对话框中，键入您的PhoneGap Build用户名和密码，然后单击“确定”。

### 使用PhoneGap Build {#using-phonegap-build}

将您的应用程序资源发送到PhoneGap Build，以便为各种移动平台进行编译。

1. 在“移动设备应用程序”页面上，打开您的移动设备应用程序。 ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. （可选）要构建应用程序以完成安装，请选择应用程序，然后单击清除缓存图标。

   ![](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >缓存中包含已安装应用程序的内容更新。 清除缓存会撤消所有缓存的更新。

1. 选择启动页面，然后单击“生成远程”图标。

   ![](do-not-localize/chlimage_1-3.png)

   **注意：** 测试版AEM测试版在成功完成内部版本后不会创建收件箱通知。

1. 在成功对话框中，单击PhoneGap Build以在 [https://build.phonegap.com/apps](https://build.phonegap.com/apps). 如果您正在等待应用程序显示，则可以检查 [PhoneGap Build状态](https://status.build.phonegap.com/) 页面。

   有关安装内部版本的信息，请参阅 [PhoneGap Build文档](https://docs.build.phonegap.com/en_US/3.1.0/#googtrans%28en%29).

   >[!NOTE]
   >
   >免费PhoneGap Build帐户允许使用一个专用应用程序。 如果您要构建其他私有应用程序，则PhoneGap生成会失败。

### 后续步骤 {#the-next-steps}

构建过程后的下一步是了解 [应用程序的结构](/help/mobile/phonegap-structure-an-app.md).
