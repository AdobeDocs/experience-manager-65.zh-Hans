---
title: 为iOS构建安全的AEM Forms应用程序
description: 了解如何通过存档Xcode项目为iOS构建安全的AEM Forms应用程序。 这将创建安装程序（.ipa文件）和属性列表（.plist文件）文件。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 12cc2027-ae94-40c3-a7d1-553469426114
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# 为iOS构建安全的AEM Forms应用程序 {#building-a-secure-aem-forms-app-for-ios}

您需要将AEM Forms应用程序的Xcode项目存档，以生成安装程序（.ipa文件）和属性列表（.plist文件）文件。 属性列表文件包含内部托管应用程序的配置信息，例如应用程序的名称和托管位置。 有关属性列表文件的详细信息，请参阅[关于信息属性列表文件](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)。

1. 登录以下网站：

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. 创建应用程序ID。 有关创建应用程序ID的详细步骤，请参阅[创建和配置应用程序ID](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html)。
1. 要为应用程序配置iOS应用程序的包标识符，请单击&#x200B;**[!UICONTROL 配置应用程序ID]**。
1. 在网页底部，选择&#x200B;**[!UICONTROL 启用数据保护]**。 指定数据保护选项。

   单击&#x200B;**[!UICONTROL 完成]**。

1. 导航到“配置”>“分发”，并使用在步骤3中配置的应用程序ID创建新配置文件。
1. 下载配置配置文件并将其添加到Xcode和iPad。
1. 登录到安装了Xcode并配置了iOS SDK的Mac计算机。
1. 在Xcode中打开`AEM Forms.xcodeproj`项目。
1. 单击&#x200B;**[!UICONTROL AEM Forms]**，在&#x200B;**[!UICONTROL 目标]**&#x200B;下，选择&#x200B;**[!UICONTROL AEM Forms]**。 选择&#x200B;**[!UICONTROL 生成设置]**&#x200B;选项卡，找到&#x200B;**[!UICONTROL 代码签名授权]**&#x200B;部分，然后在“授权”下拉列表中选择&#x200B;**[!UICONTROL LC Enterprise]**&#x200B;选项。
1. 在Xcode中查找并打开`LC Enterprise.entitlements`文件以进行编辑。 在&#x200B;**XCode授权**&#x200B;下，添加与预配配置文件中存在的相同的键值对。
1. 在&#x200B;**[!UICONTROL 生成设置]**&#x200B;选项卡中，单击&#x200B;**[!UICONTROL 全部]**，然后单击&#x200B;**[!UICONTROL 组合]**。
1. 从&#x200B;**[!UICONTROL 设置]**&#x200B;列表中，展开&#x200B;**[!UICONTROL 代码签名]**。
1. 对于&#x200B;**[!UICONTROL 代码签名标识]**，请选择适当的签名。 确保为&#x200B;**[!UICONTROL Debug]**、**[!UICONTROL Release]**&#x200B;和&#x200B;**[!UICONTROL 任何iOS SDK]**&#x200B;选择相同的签名。
1. 在&#x200B;**[!UICONTROL PROJECT]**&#x200B;下，选择&#x200B;**[!UICONTROL AEM Forms]**，并确保为&#x200B;**[!UICONTROL 代码签名标识]**、**[!UICONTROL Debug]**、**[!UICONTROL 发行版]**&#x200B;和&#x200B;**[!UICONTROL 任何iOS SDK]**&#x200B;选择适当的签名。
1. 构建和分发AEM Forms应用程序。 有关构建和分发AEM Forms应用程序的详细说明，请参阅[构建AEM Forms应用程序的安装程序](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app)。
