---
title: 配置Adobe PhoneGap BuildCloud Service
description: 按照本页上的说明配置云服务并使用PhoneGap Build构建应用程序。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# 配置Adobe PhoneGap BuildCloud Service {#configure-your-adobe-phonegap-build-cloud-service}

{{ue-over-mobile}}

应用程序仪表板上的&#x200B;**PhoneGap Build磁贴**&#x200B;允许您通过Adobe PhoneGap Build服务构建和分发PhoneGap移动应用程序。

使用&#x200B;**PhoneGap Build**&#x200B;图块推送远程生成时，**管理应用程序**&#x200B;图块中定义的所有受支持平台都是使用PhoneGap Build生成的。

您可以将远程生成推送到`https://build.phonegap.com`或下载源以使用位于`https://docs.phonegap.com/references/phonegap-cli/`的PhoneGap CLI在本地生成。

![PhoneGap Build磁贴](assets/chlimage_1-60.png)

## 配置Cloud Service {#configuring-the-cloud-service}

要利用PhoneGap Build功能，您必须使用PhoneGap Build帐户信息配置AEMPhoneGap BuildCloud Service。

如果您当前没有帐户，请导航到`https://build.phonegap.com`并注册！ 如果您拥有Adobe Creative Cloud会员资格，则最多可以支持25个私有应用程序（非开源应用程序）。

在验证PhoneGap Build帐户处于活动状态后，请导航到您的AEM Cloud Management Console，特别是[PhoneGap BuildCloud Service](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html)。

使用&#x200B;**管理Cloud Service**&#x200B;磁贴配置新的云服务配置。

### 使用“管理Cloud Service”拼贴 {#using-manage-cloud-services-tile}

在开始使用&#x200B;**PhoneGap Build**&#x200B;图块构建应用程序之前，您必须使用AEM Mobile仪表板中的&#x200B;**管理Cloud Service**&#x200B;图块配置云服务。

要为应用程序配置云服务，请执行以下步骤：

1. 单击&#x200B;**管理Cloud Service**&#x200B;图块的右上角。

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. 从&#x200B;**添加或编辑PhoneGap Build**&#x200B;屏幕中选择&#x200B;**Cloud Service**&#x200B;选项。

   单击&#x200B;**下一步**。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 输入您的凭据，以便创建云配置。

   验证后，单击&#x200B;**提交**。 此配置的云配置现在显示在&#x200B;**管理Cloud Service**&#x200B;图块中。

   ![chlimage_1-63](assets/chlimage_1-63.png)

### 使用PhoneGap Build构建应用程序 {#building-your-application-with-phonegap-build}

配置云服务后，可以使用&#x200B;**PhoneGap Build**&#x200B;磁贴构建应用程序。 单击右上角，以便您可以从&#x200B;**构建远程**&#x200B;或&#x200B;**下载Source**&#x200B;选项中进行选择。

![chlimage_1-64](assets/chlimage_1-64.png)

要使用Adobe PhoneGap Build调用远程生成，请单击&#x200B;**生成远程**。

>[!NOTE]
>
>如果构建由于任何原因失败(下面的红色iOS图标表示平台失败)，您可以将鼠标悬停在该图标上以获取错误消息。 或者，您可以单击图块底部的三点图标“……”以直接导航到`https://build.phonegap.com`（您必须进行身份验证），并直接查看和管理您的内部版本。

### 使用PhoneGap CLI构建应用程序 {#building-your-application-with-phonegap-cli}

PhoneGap提供了一个命令行界面，用于在本地构建应用程序。

使用PhoneGap命令行界面(CLI)编译计算机上的PhoneGap应用程序。 要在应用程序中包含AEM内容，AEM会创建一个ZIP文件，其中包含移动应用程序的内容、内容同步配置和其他必需资源。 下载ZIP文件并将其包含在您的内部版本中。

要利用PhoneGap的CLI，您必须将本地环境设置为包括：

1. Platform SDK (iOS、Android™、WindowsPhone...)和
1. PhoneGap CLI

您可以在`https://docs.phonegap.com/references/phonegap-cli/`阅读更多内容。

安装先决条件后，可通过创建简单的应用程序并在模拟器中运行或更佳地在您的设备上从终端尝试运行该应用程序，从而对其进行简单的测试：

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>添加 — 如果不想在连接的设备上运行该线路，则在该线路的结尾进行模拟。

验证上述功能后，请使用&#x200B;**PhoneGap Build**&#x200B;磁贴来&#x200B;**下载Source**。 将文件保存并解压缩到本地系统中。 完成此操作后：

* 导航到该保存的文件（文件夹）
* 运行“phonegap run ios”（或android等）

### 其他资源 {#additional-resources}

要了解作者和开发人员的角色和责任，请参阅以下资源：

* [使用AEM开发Adobe PhoneGap Enterprise](/help/mobile/developing-in-phonegap.md)
* [在AEM中为Adobe PhoneGap Enterprise创作](/help/mobile/phonegap.md)
