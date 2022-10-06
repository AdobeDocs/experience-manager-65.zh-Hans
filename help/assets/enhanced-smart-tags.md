---
title: 增强型智能标记
description: 增强型智能标记
contentOwner: AG
feature: Smart Tags, Search
role: User
exl-id: 5eff4a0f-30b1-4753-ad0b-002656eed972
source-git-commit: dd1e08bee03a6c7b07b32b0fb929d02dad467744
workflow-type: tm+mt
source-wordcount: '1579'
ht-degree: 1%

---

# 了解、应用和策划智能标记 {#enhanced-smart-tags}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/smart-tags.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/enhanced-smart-tags.html?lang=en) |

处理数字资产的组织越来越多地在资产元数据中使用分类控制的词汇。 基本上，它包括员工、合作伙伴和客户通常用来引用和搜索特定类别数字资产的关键词列表。 使用分类控制的词汇标记资产可确保轻松识别和检索资产。

与自然语言词汇相比，基于业务分类的数字资产标记有助于使其与公司的业务保持一致，并确保最相关的资产出现在搜索中。

例如，汽车制造商可以使用型号名称标记汽车图像，以便在搜索各种型号的图像以设计促销活动时，只显示相关图像。

要使智能内容服务应用正确的标记，请对其进行培训以识别您的分类。 要培训服务，请首先组织一组最能描述这些资产的资产和标记。 要帮助该服务学习，请在资产上应用这些标记并运行培训工作流。

培训标记并准备就绪后，该服务现在可以通过标记工作流将这些标记应用于资产。

在后台，智能内容服务使用Adobe Sensei AI框架，根据您的标记结构和业务分类培训其图像识别算法。 然后，可使用此内容智能对不同的资产集应用相关标记。

智能内容服务是托管在 [!DNL Adobe Developer Console]. 要在 [!DNL Adobe Experience Manager]，系统管理员必须将 [!DNL Experience Manager] 部署 [!DNL Adobe Developer Console].

总之，以下是使用智能内容服务的主要步骤：

* 新用户引导
* 审核资产和标记（分类定义）
* 培训智能内容服务
* 自动标记

![流程图](assets/flowchart.gif)

## 先决条件和支持的格式 {#prerequisites}

在使用智能内容服务之前，请确保满足以下条件在 [!DNL Adobe Developer Console]:

* 具有组织管理员权限的Adobe ID帐户。
* 为贵组织启用智能内容服务。
* 要将智能内容服务基础包添加到部署，请获取许可证 [!DNL Adobe Experience Manager Sites] 基本包和 [!DNL Assets] 附加组件。

该服务将智能标记应用于以下MIME类型的资产：

* `image/jpeg`
* `image/tiff`
* `image/png`
* `image/bmp`
* `image/gif`
* `image/pjpeg`
* `image/x-portable-anymap`
* `image/x-portable-bitmap`
* `image/x-portable-graymap`
* `image/x-portable-pixmap`
* `image/x-rgb`
* `image/x-xbitmap`
* `image/x-xpixmap`
* `image/x-icon`
* `image/photoshop`
* `image/x-photoshop`
* `image/psd`
* `image/vnd.adobe.photoshop`

该服务将智能标记应用于以下MIME类型的资产演绎版：

* `image/jpeg`
* `image/pjpeg`
* `image/png`

## 新用户引导 {#onboarding}

智能内容服务可作为的加载项进行购买 [!DNL Experience Manager]. 购买后，系统会向贵组织的管理员发送一封电子邮件，其中包含指向 [!DNL Adobe I/O].

管理员可以按照链接将智能内容服务与 [!DNL Experience Manager]. 将服务与 [!DNL Experience Manager Assets]，请参阅 [配置智能标记](config-smart-tagging.md).

当管理员配置服务并将用户添加到 [!DNL Experience Manager].

## 审核资产和标记 {#reviewing-assets-and-tags}

入门后，您首先想要做的就是确定一组标记，这些标记在您的业务环境中最好地描述这些图像。

接下来，查看图像以识别最能代表您产品以满足特定业务需求的图像集。 确保策划集中的资产符合 [智能内容服务培训指南](/help/assets/config-smart-tagging.md#training-the-smart-content-service).

将资产添加到文件夹中，并从属性页面将标记应用于每个资产。 然后，在此文件夹上运行培训工作流。 经过策划的资产集使智能内容服务能够使用您的分类定义有效地培训更多资产。

>[!NOTE]
>
>1. 培训是一个不可撤消的过程。 Adobe建议您在对标记培训智能内容服务之前，先查看策划资产集中的标记。
>1. 在培训标记之前，请参阅 [智能内容服务培训指南](/help/assets/config-smart-tagging.md#training-the-smart-content-service).
>1. 首次培训智能内容服务时，Adobe建议您至少在两个不同的标记上对其进行培训。


## 了解 [!DNL Experience Manager] 使用智能标记搜索结果 {#understandsearch}

默认情况下， [!DNL Experience Manager] 搜索将搜索词与 `AND` 子句。 使用智能标记不会更改此默认行为。 使用智能标记会添加 `OR` 子句来查找与智能标记相关的任何搜索词。 例如，请考虑搜索 `woman running`. 仅包含 `woman` 或 `running` 默认情况下，元数据中的关键字不会显示在搜索结果中。 但是，标有以下任一项的资产 `woman` 或 `running` 在此类搜索查询中会显示使用智能标记。 所以搜索结果是，

* 资产 `woman` 和 `running` 元数据中的关键词。

* 使用任一关键字标记的资产智能。

首先显示与元数据字段中的所有搜索词匹配的搜索结果，然后显示与智能标记中的任意搜索词匹配的搜索结果。 在上例中，搜索结果的显示大致顺序为：

1. 匹配 `woman running` 在各种元数据字段中。
1. 匹配 `woman running` 在智能标记中。
1. 匹配 `woman` 或 `running` 在智能标记中。

>[!CAUTION]
>
>如果Lucene索引在 [!DNL Adobe Experience Manager]，则基于智能标记的搜索将无法按预期工作。

## 自动标记资产 {#tagging-assets-automatically}

在培训了智能内容服务后，您可以触发标记工作流，以自动对其他相似资产集应用适当的标记。

您可以定期或在需要时运行标记工作流。

>[!NOTE]
>
>标记工作流可在资产和文件夹上运行。

### 定期标记 {#periodic-tagging}

您可以启用智能内容服务来定期标记文件夹中的资产。 打开资产文件夹的属性页面，选择 **[!UICONTROL 启用智能标记]** 下 **[!UICONTROL 详细信息]** ，然后保存更改。

为文件夹选择此选项后，智能内容服务会自动为文件夹中的资产添加标记。 默认情况下，标记工作流每天中午12:00运行。

### 按需标记 {#on-demand-tagging}

您可以从工作流控制台或时间轴触发标记工作流，以立即标记您的资产。

>[!NOTE]
>
>如果您从时间轴运行标记工作流，则一次最多可以对15个资产应用标记。

#### 从工作流控制台中标记资产 {#tagging-assets-from-the-workflow-console}

1. 在 [!DNL Experience Manager] 界面，转到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.
1. 从 **[!UICONTROL 工作流模型]** 页面，选择 **[!UICONTROL DAM智能标记资产]** 工作流，然后单击 **[!UICONTROL 启动工作流]** 中。

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. 在 **[!UICONTROL 运行工作流]** 对话框中，浏览到包含要自动应用标记的资产的有效负荷文件夹。
1. 指定工作流的标题和可选注释。 单击 **[!UICONTROL 运行]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   要验证智能内容服务是否正确标记了您的资产，请导航到资产文件夹并查看标记。

#### 从时间轴标记资产 {#tagging-assets-from-the-timeline}

1. 从 [!DNL Assets] 用户界面中，选择包含要应用智能标记的资产或特定资产的文件夹。
1. 从左上角，打开 **[!UICONTROL 时间轴]**.
1. 从左侧边栏的底部打开操作，然后单击 **[!UICONTROL 启动工作流]**.

   ![start_workflow](assets/start_workflow.png)

1. 选择 **[!UICONTROL DAM智能标记资产]** 工作流，并为工作流指定标题。
1. 单击 **[!UICONTROL 开始]**. 工作流会对资产应用标记。 要验证智能内容服务是否正确标记了您的资产，请导航到资产文件夹并查看标记。

>[!NOTE]
>
>在后续的标记周期中，只有已修改的资产会再次使用新培训的标记进行标记。 但是，如果标记工作流的最后一个标记周期与当前标记周期之间的间隔超过24小时，则即使是未更改的资产也会进行标记。 对于定期标记工作流，当时间间隔超过6个月时，将标记未更改的资产。

## 策划或审核应用的智能标记 {#manage-smart-tags}

您可以策划智能标记，以删除分配给品牌图像的任何不准确标记，以便仅显示最相关的标记。

审核智能标记还可确保图像显示在最相关标记的搜索结果中，从而帮助优化基于标记的图像搜索。 从本质上讲，这有助于消除不相关图像在搜索结果中出现的可能性。

您还可以为标记分配更高的排名，以提高其与图像的相关性。 提升图像的标记会增加在搜索特定标记时在搜索结果中出现图像的可能性。

1. 在搜索框中，使用标记作为关键字来搜索资产。
1. 要识别您找不到与搜索相关的图像，请查看搜索结果。
1. 选择图像，然后单击 **[!UICONTROL 管理标记]** 中。
1. 从 **[!UICONTROL 管理标记]** 页面，查看标记。 如果您不希望根据特定标记搜索图像，请选择该标记，然后单击 **[!UICONTROL 删除]** 中。 或者，单击 `x` 标记旁边显示的符号。
1. （可选）要为标记分配更高的排名，请选择标记并单击 **[!UICONTROL 提升]** 中。 您提升的标记将移至 **[!UICONTROL 标记]** 中。
1. 单击 **[!UICONTROL 保存]** 然后单击 **[!UICONTROL 确定]**
1. 导航到 **[!UICONTROL 属性]** 页面。 请注意，您促销的标记被分配得更相关，并显示在搜索结果的前面。

## 提示和限制 {#tips-best-practices-limitations}

* 要训练模型，请使用最合适的图像。 无法恢复培训或删除培训模型。 您的标记准确性取决于当前培训，因此请谨慎进行。
* 智能内容服务的使用限制为每年最多200万张标记图像。 处理和标记的任何重复图像都计为标记图像。
* 如果您从时间轴运行标记工作流，则一次最多可以对15个资产应用标记。
* 智能标记仅适用于PNG和JPG图像格式。 因此，对于以这两种格式创建演绎版的受支持资产，将使用智能标记进行标记。
