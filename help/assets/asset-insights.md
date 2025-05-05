---
title: Assets Insights
description: 了解Assets Insights功能如何让您跟踪第三方网站、营销活动和Adobe创意解决方案中使用的图像的用户评级和使用情况统计数据。
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 0130ac40-a72b-4caf-a10f-3c7d76eaa1e6
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 8%

---

# Assets Insights {#asset-insights}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/assets-insights.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

Assets Insights功能允许您跟踪第三方网站、营销活动和Adobe创意解决方案中使用的图像的用户评级和使用情况统计数据。 这有助于获得有关其性能和受欢迎程度的见解。

[!DNL Assets]分析会捕获用户活动详细信息，例如对图像进行评级、点击和展示的次数（图像加载到网站上的次数）。 它根据这些统计数据为图像分配分数。 您可以使用得分和性能统计信息选择热门图像以将其包含在目录、营销活动等中。 您甚至可以根据这些统计数据制定存档和许可证更新策略。

若要使用[!DNL Assets]分析从网站中捕获图像的使用情况统计数据，您必须在网站代码中包含该图像的嵌入代码。

要让Assets Insights显示资源的使用情况统计数据，请首先配置该功能以从Adobe Analytics获取报表数据。 有关详细信息，请参阅[配置Assets分析](/help/assets/configure-asset-insights.md)。 要在内部部署安装中使用此功能，请单独购买[!DNL Adobe Analytics]许可证。 [!DNL Managed Services]上的客户将收到与[!DNL Experience Manager]捆绑的[!DNL Analytics]许可证。 请参阅[Managed Services产品说明](https://helpx.adobe.com/cn/legal/product-descriptions/adobe-experience-manager-managed-services.html)。

>[!NOTE]
>
>仅支持图像并提供见解。

## 查看图像的统计信息 {#viewing-statistics-for-an-image}

您可以从元数据页面查看Assets Insights分数。

1. 从[!DNL Assets]用户界面(UI)中，选择图像，然后单击工具栏中的&#x200B;**[!UICONTROL 属性]**。
1. 在“属性”页面中，单击&#x200B;**[!UICONTROL 分析]**&#x200B;选项卡。
1. 在&#x200B;**[!UICONTROL 分析]**&#x200B;选项卡中查看资产的使用情况详细信息。 **[!UICONTROL 得分]**&#x200B;部分描述了资源的总使用情况和性能损失。

   使用情况得分描述了资产在各种解决方案中的使用次数。

   **[!UICONTROL 展示次数]**&#x200B;分数是资源加载到网站上的次数。 在&#x200B;**[!UICONTROL 点击次数]**&#x200B;下显示的数量是点击资产的次数。

1. 查看&#x200B;**[!UICONTROL 使用情况统计数据]**&#x200B;部分，了解资产所属的实体以及最近使用它的创意解决方案。 使用率越高，资产在用户中受欢迎的可能性就越大。 使用情况数据显示在以下标题下：

   * **资源**：资源属于收藏集或复合资源的次数
   * **Web和移动设备**：资产属于网站和应用程序的次数
   * **Social**：在解决方案(如Adobe Social和Adobe Campaign)中使用资源的次数
   * **电子邮件**：在电子邮件营销活动中使用该资源的次数

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >由于Assets Insights功能通常会定期从Adobe Analytics中获取解决方案数据，因此解决方案部分可能不会显示最新数据。 显示数据的时间段取决于Assets Insights为检索Analytics数据而运行的获取操作的计划。

1. 要以图形方式查看一段时间内资产的性能统计信息，请在&#x200B;**[!UICONTROL 性能统计信息]**&#x200B;部分中选择时间段。包括点击次数和印象在内的详细信息将显示为图形的趋势线。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >与“解决方案”部分中的数据不同，“性能统计信息”部分显示最新数据。

1. 若要获取您在网站中包含的资产嵌入代码以获取性能数据，请单击资产缩略图下方的&#x200B;**[!UICONTROL 获取嵌入代码]**。 有关如何将嵌入代码包含在第三方网页中的更多信息，请参阅[在网页中使用页面跟踪器和嵌入代码](/help/assets/use-page-tracker.md)。

   ![chlimage_1-98](assets/chlimage_1-303.png)

## 查看图像的聚合统计信息 {#viewing-aggregate-statistics-for-images}

您可以使用&#x200B;**[!UICONTROL 分析视图]**&#x200B;同时查看文件夹中所有资产的分数。

1. 在[!DNL Assets]用户界面中，导航到包含要查看其分析的资产的文件夹。
1. 单击工具栏中的“布局”，然后选择&#x200B;**[!UICONTROL 分析视图]**。
1. 页面显示资源的使用分数。 比较各种资源的评级并得出见解。

## 计划后台作业 {#scheduling-background-job}

Assets Insights会定期从Adobe Analytics报表包中获取资产的使用情况数据。 默认情况下，Assets Insights在凌晨2点每24小时运行一次获取数据的后台作业。 但是，您可以通过从Web控制台配置&#x200B;**[!UICONTROL Adobe CQ DAM资产性能报表同步作业]**&#x200B;服务来修改频率和时间。

1. 单击[!DNL Experience Manager]徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 打开&#x200B;**[!UICONTROL Adobe CQ DAM资产性能报表同步作业]**&#x200B;服务配置。

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. 在属性调度程序表达式中指定所需的调度程序频率和作业的开始时间。 保存更改。
