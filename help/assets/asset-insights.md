---
title: 资产分析
description: 了解资产分析功能如何让您跟踪第三方网站、营销活动和Adobe创意解决方案中使用的图像的用户评级和使用情况统计数据。
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

# 资产分析 {#asset-insights}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/assets-insights.html?lang=en) |
| AEM 6.5 | 本文 |

通过Assets Insights功能，您可以跟踪第三方网站、营销活动和Adobe创意解决方案中使用的图像的用户评级和使用统计数据。 这有助于获得有关其性能和受欢迎程度的见解。

[!DNL Assets] 分析会捕获用户活动详细信息，例如对图像进行评级、单击的次数和展示次数（图像加载到网站上的次数）。 它根据这些统计数据为图像分配分数。 您可以使用得分和性能统计信息选择热门图像以将其包含在目录、营销活动等中。 您甚至可以根据这些统计数据制定存档和许可证更新策略。

对象 [!DNL Assets] 分析要从网站中捕获图像的使用情况统计数据，您必须在网站代码中包含该图像的嵌入代码。

要让Assets Insights显示资源的使用情况统计数据，请首先配置该功能以从Adobe Analytics获取报表数据。 有关详细信息，请参阅 [配置资产分析](/help/assets/configure-asset-insights.md). 要在内部部署安装中使用此功能，请购买 [!DNL Adobe Analytics] 单独许可。 客户位于 [!DNL Managed Services] 接收 [!DNL Analytics] 与捆绑在一起的许可证 [!DNL Experience Manager]. 请参阅 [Managed Services产品描述](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>仅支持图像并提供见解。

## 查看图像的统计信息 {#viewing-statistics-for-an-image}

您可以从元数据页面查看资产分析分数。

1. 从 [!DNL Assets] 用户界面(UI)，选择图像，然后单击 **[!UICONTROL 属性]** 工具栏中。
1. 在“属性”页面中，单击 **[!UICONTROL Insights]** 选项卡。
1. 在中查看资产的使用情况详细信息 **[!UICONTROL Insights]** 选项卡。 此 **[!UICONTROL 分数]** 部分介绍了资源的总资源使用情况和性能损失。

   使用情况得分描述了资产在各种解决方案中的使用次数。

   此 **[!UICONTROL 展示次数]** score是资产在网站上加载的次数。 下显示的编号 **[!UICONTROL 点击次数]** 是点击资源的次数。

1. 查看 **[!UICONTROL 使用情况统计数据]** 部分，了解资产所属的实体以及最近使用它的创意解决方案。 使用率越高，资产在用户中受欢迎的可能性就越大。 使用情况数据显示在以下标题下：

   * **资产**：资产属于收藏集或复合资产的次数
   * **Web和移动**：资产属于网站和应用程序的次数
   * **Social**：资产在解决方案(如Adobe Social和Adobe Campaign)中的使用次数
   * **电子邮件**：电子邮件营销活动中使用资源的次数

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >由于资产分析功能通常会定期从Adobe Analytics中获取解决方案数据，因此解决方案部分可能不会显示最新数据。 显示数据的时间段取决于资产分析运行的获取操作计划，以检索Analytics数据。

1. 要以图形方式查看一段时间内资产的性能统计信息，请在&#x200B;**[!UICONTROL 性能统计信息]**&#x200B;部分中选择时间段。包括点击次数和印象在内的详细信息将显示为图形的趋势线。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >与“解决方案”部分中的数据不同，“性能统计信息”部分显示最新数据。

1. 要获取包括在网站中的资产的嵌入代码以获取性能数据，请单击 **[!UICONTROL 获取嵌入代码]** 资产缩略图下方。 有关如何将嵌入代码包含在第三方网页中的更多信息，请参阅 [在网页中使用页面跟踪器和嵌入代码](/help/assets/use-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## 查看图像的聚合统计信息 {#viewing-aggregate-statistics-for-images}

您可以使用&#x200B;**[!UICONTROL 分析视图]**&#x200B;同时查看文件夹中所有资产的分数。

1. 在 [!DNL Assets] 在用户界面中，导航到包含要查看其见解的资产的文件夹。
1. 单击工具栏中的布局，然后选择 **[!UICONTROL 分析视图]**.
1. 页面显示资源的使用分数。 比较各种资源的评级并得出见解。

## 计划后台作业 {#scheduling-background-job}

资产分析会定期从Adobe Analytics报表包中获取资产的使用情况数据。 默认情况下，Assets Insights在凌晨2点每24小时运行一次获取数据的后台作业。 但是，您可以通过配置 **[!UICONTROL Adobe CQ DAM资产性能报表同步作业]** Web控制台中的服务。

1. 单击 [!DNL Experience Manager] 徽标，然后转到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.
1. 打开 **[!UICONTROL Adobe CQ DAM资产性能报表同步作业]** 服务配置。

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. 在属性调度程序表达式中指定所需的调度程序频率和作业的开始时间。 保存更改。
