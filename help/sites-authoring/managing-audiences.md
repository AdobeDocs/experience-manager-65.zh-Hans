---
title: 管理受众
seo-title: 管理受众
description: 通过“受众”控制台，您可以创建、组织和管理 Adobe Target 帐户的受众，或管理 ContextHub 或 Client Context 的区段
seo-description: 通过“受众”控制台，您可以创建、组织和管理 Adobe Target 帐户的受众，或管理 ContextHub 或 Client Context 的区段
uuid: 76408a8c-25db-4e9f-8a69-27e820a2a7cf
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 9a7a31f9-aeb8-455f-a07e-7b1d1f0a88b6
docset: aem65
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# 管理受众{#managing-audiences}

通过“受众”控制台，您可以创建、组织和管理 Adobe Target 帐户的受众，或管理 ContextHub 或 Client Context 的区段：

* 添加受众 - Adobe Target 受众或 ContextHub 区段。
* 管理受众。

An Audience, called *segment* in ContextHub and Client Context, is a class of visitors defined by specific criteria, which then determines who sees a targeted activity. 定位活动时，您可以直接在“定位”过程中选择受众，也可以在“受众”控制台中创建新受众。

在“受众”控制台中，各受众按品牌进行组织。

Audiences are available in Targeting mode for [authoring targeted content](/help/sites-authoring/content-targeting-touch.md), where you can also create audiences (but you need to create Adobe Target audiences in the Audiences console). 在“定位”模式下创建的受众会显示在“受众”控制台中。

受众显示有相应的标签，用于说明定义的受众类型：

* CH - ContextHub 区段
* CC - Client Context 区段
* AT - Adobe Target 受众

## 在“受众”控制台中创建 ContextHub 区段 {#creating-a-contexthub-segment-in-the-audiences-console}

您可以在“受众”控制台中或在定位过程中创建 ContextHub 区段。

要在“受众”控制台中创建 ContextHub 区段，请执行以下操作：

1. 在“导航”控制台中，单击或点按&#x200B;**个性化**。Click or tap **Audiences**.
1. 单击或点按&#x200B;**创建 ContextHub 区段**。

   ![screen-shot_2019-03-05at124034](assets/screen-shot_2019-03-05at124034.png)

1. 在&#x200B;**新 ContextHub 区段**&#x200B;对话框中，输入标题并调整提升，然后单击&#x200B;**创建**。您的新ContextHub区段将显示在受众列表中。

   >[!NOTE]
   >
   >You can sort the modified list by tapping or clicking **Modified** to sort by descending order to see any newly created audiences.

有关使用 ContextHub 创建区段的更多详细信息，请参阅[使用 ContextHub 配置分段](/help/sites-administering/segmentation.md)文档。

## 使用“受众”控制台创建 Adobe Target 受众 {#creating-an-adobe-target-audience-using-the-audience-console}

您可以直接在 AEM 中使用“受众”控制台创建 Adobe Target 受众。

受众由确定目标活动中包含哪些人的规则进行定义。受众定义可以包含多个规则，每个规则可以包含多个参数。

使用多个规则时，这些规则会通过布尔运算符 AND 进行组合，这意味着任何潜在的受众成员必须满足所有定义的条件才能包含在活动中。例如，如果您定义了操作系统规则和浏览器规则，则只有同时使用定义的操作系统和定义的浏览器的访客才会包含在活动中。

>[!NOTE]
>
>If you do not see **Create Target Audience **in the **Create** menu, you do not have the necessary permissions to create an audience. You need write permissions under **/etc/segmentation** to be able to create audiences. 默认情况下，组内容作者具有写权限。

要创建 Adobe Target 受众，请执行以下操作：

1. 在“导航”控制台中，单击或点按&#x200B;**个性化**。Click or tap **Audiences**.

   ![screen-shot_2019-03-05at124139](assets/screen-shot_2019-03-05at124139.png)

1. In the Audiences console, tap or click **Create** and then** Create Target Audience**.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 在 **Adobe Target 配置**&#x200B;对话框中，选择目标配置，然后单击或点按&#x200B;**确定**。
1. 在“规则#1”区域中，单击或点按属性类型并在可用字段中输入任何属性信息。完成后，选中该属性右侧的复选标记以保存该属性。有关所有属性的信息，请参阅[属性及其选项](#attributes-and-their-options)。
1. 单击&#x200B;**添加规则**&#x200B;以添加其他规则。输入所需数量的规则。这些规则会通过布尔运算符 AND 进行组合，这意味着受众必须满足每个规则的所有要求才有资格包含在活动中。
1. 单击或点按&#x200B;**下一步**。
1. 为受众输入一个名称，然后单击或点按&#x200B;**保存**。
1. Tap or click **Save**. 受众随即会列在“受众”列表中。

### 属性及其选项 {#attributes-and-their-options}

您可以为以下每个属性创建定位规则。

| **属性** | **描述** | **有关更多信息** |
|---|---|---|
| **移动设备** | 根据移动设备、设备类型、设备供应商、屏幕尺寸（按像素）等参数定位移动设备。 | 请参 [阅Adobe Target的](https://marketing.adobe.com/resources/help/en_US/target/target/c_mobile.html) Mobile文档。 |
| **自定义** | 自定义参数是mbox参数。 如果您将任何 mbox 参数传递给 mbox，或者使用 targetPageParams 函数，这些参数将会显示在此处以供在受众中使用。 | 请参 [阅Adobe Target的自定义参数](https://marketing.adobe.com/resources/help/en_US/target/target/c_custom_parameters.html) 文档。 |
| **操作系统** | 您可以定位使用特定操作系统的访客。 | 定位使用Linux、Macintosh或Windows的用户。 |
| **站点页面** | 定位位于特定页面或具有特定mbox参数的访客。 | 请参 [阅Adobe Target的网站页](https://marketing.adobe.com/resources/help/en_US/target/target/c_site_pages.html) 。 |
| **浏览器** | 您可以定位在用户访问页面时使用特定浏览器或特定浏览器选项的用户。 | 请参 [阅Adobe Target的](https://marketing.adobe.com/resources/help/en_US/target/target/c_browser_options.html)浏览器选项文档。 |
| **访客配置文件** | 定位满足特定配置文件参数的访客。 | 请参 [阅Adobe Target的访客资料](https://marketing.adobe.com/resources/help/en_US/target/target/c_visitor_profile.html) 文档。 |
| **流量源** | 根据搜索引擎或将访客引用到您网站的登录页面定位访客。 | 请参 [阅Adobe Target的](https://marketing.adobe.com/resources/help/en_US/target/target/c_traffic_sources.html) Traffic Sources文档。 |

## 在“受众”控制台中修改受众 {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>您只能编辑在当前所编辑的相同 AEM 实例中创建的 Adobe Target 受众。无法编辑在不同的 AEM 环境中创建的目标受众。

您可以从“受众”控制台中编辑任何 ContextHub 或 Client Context 受众。您也可以编辑 Adobe Target 受众，但只能编辑在 AEM 中创建的受众：

1. 在“导航”控制台中，单击或点按&#x200B;**个性化**。Click or tap **Audiences**.
1. 单击或点按要编辑的 ContextHub 或 Client Context 区段旁边的图标，然后单击或点按&#x200B;**编辑**。
1. 在区段编辑器中进行任何编辑。请参阅 [Client Context](/help/sites-administering/campaign-segmentation.md) 或 [ContextHub](/help/sites-administering/contexthub-config.md) 文档。
