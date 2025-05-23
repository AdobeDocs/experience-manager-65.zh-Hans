---
title: 构建移动应用程序
description: 此页面提供了有关如何使用GitHub中提供的代码构建移动应用程序的完整分步文章，请单击此处获得。 构建您的应用程序以安装到设备或模拟器以进行测试或发布到应用商店。 您可以使用PhoneGap命令行界面在本地构建应用程序，也可以使用PhoneGap Build在云中构建应用程序。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7c2e5ed8-9f8e-4a81-b736-589ef4089f29
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# 构建移动应用程序{#building-mobile-applications}

{{ue-over-mobile}}

构建您的应用程序以安装到设备或模拟器以进行测试或发布到应用商店。 您可以使用PhoneGap命令行界面在本地构建应用程序，也可以使用PhoneGap Build在云中构建应用程序。

有关如何使用GitHub中提供的代码构建移动应用程序的完整分步文章，请参阅[此处](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html)。

## 将应用程序移动到Publish实例 {#moving-the-application-to-the-publish-instance}

将应用程序文件移动到发布实例，以便您可以为已安装的移动应用程序实例提供内容更新，并使用已发布的内容构建应用程序。 应用程序由存储库中的两个节点分支组成：

* `/content/phonegap/apps/<application name>`：作者创建和激活的网页。
* `/content/phonegap/content/<application name>`：应用程序配置文件和内容同步配置。

>[!NOTE]
>
>如果不将应用程序文件移动到发布实例，则内容作者无法更新内容同步缓存。

您只需要将`/content/phonegap/content/<application name>`分支中的文件移动到发布实例。 当作者激活页面时，`/content/phonegap/apps/<application name>`分支中的文件将被移动。

AEM提供了两种将批量内容移动到发布实例的方法：

* [在复制控制台上使用“激活树”命令](/help/sites-authoring/publishing-pages.md)。
* [创建包含内容的包](/help/sites-administering/package-manager.md)并复制该包。

例如，将创建一个名为phonegapapp的移动应用程序。 必须将以下节点移到发布实例：/content/phonegap/content/phonegapapp。

**提示：**&#x200B;要将包从创作实例移动到发布实例，请对包使用Replicate命令。

![chlimage_1-16](assets/chlimage_1-16.png)

## 使用PhoneGap命令行界面构建 {#building-using-the-phonegap-command-line-interface}

使用PhoneGap命令行界面(CLI)编译计算机上的PhoneGap应用程序。 要在应用程序中包含AEM内容，AEM会创建一个ZIP文件，其中包含移动应用程序的内容、内容同步配置和其他必需资源。 下载ZIP文件并将其包含在您的内部版本中。

### 准备构建环境 {#preparing-your-build-environment}

要使用PhoneGap CLI进行构建，您需要安装Node.js和PhoneGap客户端实用程序。 您需要连接Internet才能执行以下步骤。

1. 下载并安装[Node.js](https://nodejs.org/en)。
1. 打开终端或命令提示符并输入以下节点命令以安装PhoneGap实用程序：

   ```shell
   npm install -g phonegap
   ```

   在UNIX®或Linux®系统上，可能需要在命令的前缀中加上`sudo`。

   该终端显示了一系列HTTPGET命令的结果。 安装成功后，终端会显示库的安装位置，类似于以下示例：

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

1. （可选）获取目标移动平台的SDK：

   * 若要为iOS平台构建应用程序，请安装最新版本的[Xcode](https://developer.apple.com/xcode/)。
   * 要构建Android™应用程序，请安装[Android™ SDK](https://developer.android.com/)。

### 下载内容ZIP文件 {#downloading-the-content-zip-file}

将移动应用程序的内容移动到文件系统。

1. 在“移动设备应用程序”页面上，选择您的应用程序。
1. （可选）要构建应用程序以完成安装，请在工具栏上单击清除缓存图标。

   ![清除由断开的链接符号表示的缓存图标。](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >缓存保存已安装应用程序的内容更新。 清除缓存将会使所有缓存的更新失效。

1. 在工具栏上，单击下载CLI Assets图标。

   ![下载CLI Assets图标，以重叠的平板电脑符号表示。](do-not-localize/chlimage_1-1.png)

1. 保存ZIP文件后，在“成功”对话框中单击“关闭”。
1. 解压缩ZIP文件的内容。

### 使用PhoneGap CLI构建 {#using-the-phonegap-cli-to-build}

使用PhoneGap CLI编译和安装应用程序。 有关如何使用PhoneGap CLI的信息，请参阅PhoneGap命令行界面(`https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html`)文档。

1. 打开终端或命令提示符并将当前目录更改为下载的应用程序ZIP文件。 例如，以下内容将目录更改为ng-app-cli.1392137825303.zip文件：

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. 输入要定位的平台的phonegap命令。 例如，以下命令可为Android构建应用程序™：

   ```shell
   phonegap build android
   ```

## 使用PhoneGap Build构建 {#building-using-phonegap-build}

使用PhoneGap云服务构建您的应用程序。 要执行此过程，必须首先创建PhoneGap Build配置。

### 正在连接到PhoneGap Build {#connecting-to-phonegap-build}

创建PhoneGap Build配置，以便您可以从AEM中使用PhoneGap Build服务。 提供用于构建移动应用程序的PhoneGap Build的用户名和密码。

1. 打开“工具”页面。 ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))。
1. 在“CQ操作”区域中，单击“Cloud Service”。
1. 单击PhoneGap Build的“立即配置”链接。

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. 在创建配置对话框中，为Title属性键入一个值。 默认情况下，“名称”属性的值派生自标题，但您可以输入名称。 单击“创建”。
1. 在“PhoneGap Build配置”对话框中，键入您的PhoneGap Build用户名和密码，然后单击“确定”。

### 使用PhoneGap Build {#using-phonegap-build}

将您的应用程序资源发送到PhoneGap Build，以便针对各种移动平台进行编译。

1. 在移动设备应用程序页面上，打开您的移动设备应用程序。 ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. （可选）要为完整的安装构建应用程序，请选择该应用程序，然后单击“清除缓存”图标。

   ![清除由断开的链接符号表示的缓存图标。](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >缓存保存已安装应用程序的内容更新。 清除缓存将会使所有缓存的更新失效。

1. 选择启动页面，然后单击构建远程图标。

   ![由两个圆齿轮指示的“生成远程”图标。](do-not-localize/chlimage_1-3.png)

   **注意：** AEM Beta的Beta版本在生成成功完成时未创建收件箱通知。

1. 在“成功”对话框中，单击“PhoneGap Build”以打开`https://build.phonegap.com/apps`处的Adobe PhoneGap Build页面。 如果您正在等待应用程序出现，则可以在`https://status.build.phonegap.com/`上查看PhoneGap Build状态。

   有关安装内部版本的信息，请参阅[PhoneGap Build文档](https://github.com/phonegap/phonegap-docs/tree/master/docs/4-phonegap-build)。

   >[!NOTE]
   >
   >允许一个私有PhoneGap Build的免费帐户。 如果您正在构建其他私有应用程序，PhoneGap构建会失败。

### 后续步骤 {#the-next-steps}

构建过程后的下一步是了解应用程序[&#128279;](/help/mobile/phonegap-structure-an-app.md)的结构。
