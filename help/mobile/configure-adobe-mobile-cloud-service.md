---
title: 配置AdobeMobile ServicesCloud Service
description: 请按照本页上的说明配置您的AdobeMobile ServicesCloud Service。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
exl-id: 209c36f9-1a4b-4eea-8dde-22e0fc9718c1
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# 配置AdobeMobile ServicesCloud Service {#configure-your-adobe-mobile-services-cloud-service}

{{ue-over-mobile}}

命令中心上的&#x200B;**移动量度图块**&#x200B;为您的移动应用程序提供实时分析。

[Adobe移动分析](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK可通过PhoneGap插件使用。 收集量度并将其缓存在设备上，直到设备连接为止，届时，会将数据推送到AdobeMobile Services云以供生成报表和分析。

AdobeMobile Analytics SDK提供以下功能：

1. **移动渠道的数据收集** — 收集所有主要操作系统上移动网站和应用程序的全面数据。
1. **移动参与分析** — 了解用户在您的移动应用程序、网站或视频中的参与情况，包括消费者启动渠道的频率、他们是否从中购买等。
1. **移动应用功能板和报表** — 获取包含应用生命周期量度和应用商店量度的使用情况报表 — 查看用户、启动次数、平均会话时长、保留时长和崩溃次数趋势。
1. **移动营销活动分析** — 量化特定移动营销活动（如短信、移动搜索广告、移动显示广告和二维码）的有效性。
1. **地理位置分析** — 通过GPS位置或目标点查找应用程序用户启动的位置并与移动体验交互。
1. **路径分析** — 了解用户如何在您的应用程序中导航以确定哪些屏幕和UI元素吸引用户以及导致用户流失。

>[!CAUTION]
>
>仅当您配置了云服务时，**分析量度**&#x200B;图块才会显示在仪表板中。

![chlimage_1-22](assets/chlimage_1-22.png)

AEM Command Center Metrics图块

## 配置Cloud Service {#configuring-the-cloud-service}

要利用AdobeMobile Services Analytics，您需要使用Adobe Analytics帐户信息配置AEM Mobile Analytics Cloud服务。

1. 单击右上角的图标以从应用程序仪表板的“**管理Cloud Service**”拼贴中添加或编辑Cloud Service。

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. 将显示&#x200B;**添加或编辑Cloud Service**&#x200B;屏幕。 选择&#x200B;**AdobeMobile Services**，然后单击&#x200B;**下一步**。

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. 从&#x200B;**Mobile Services**&#x200B;中选择现有配置，或选择&#x200B;**创建配置**&#x200B;以创建配置。

   对于新配置，请输入&#x200B;**Mobile Services属性**&#x200B;并单击&#x200B;**验证。**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   如果凭据已验证，**验证**&#x200B;按钮将更改为&#x200B;**已验证**。 您可以从&#x200B;**选择移动应用服务**&#x200B;中选择移动服务应用。

   单击&#x200B;**提交**&#x200B;以设置您的配置。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. 设置云配置后，您可以在功能板中查看该配置。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >设置云配置后，您可以在应用程序仪表板中查看&#x200B;**分析量度**&#x200B;图块。

   ![chlimage_1-28](assets/chlimage_1-28.png)
