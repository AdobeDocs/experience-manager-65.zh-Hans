---
title: 资产模板
description: 了解 [!DNL Adobe Experience Manager Assets] 中的资产模板以及如何使用资产模板创建营销宣传品。
contentOwner: AG
role: User
feature: Asset Management,Developer Tools
exl-id: 12c92aad-3a1d-486e-a830-31de2fc6d07b
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---

# 资产模板 {#asset-templates}

资产模板是一类特殊的资产，有助于快速调整视觉内容用途，以便用于数字和印刷媒体。 资产模板包括固定消息传递部分和可编辑部分两部分。 固定消息部分可以包含专有内容，例如禁用编辑的品牌徽标和版权信息。 可编辑部分可在可编辑以自定义消息传递的字段中包含可视和文本内容。

在保护全局标牌的同时进行有限编辑的灵活性使资产模板成为快速内容调整和分发的理想构建块，可作为各种功能的内容构件。 重新调整内容用途有助于降低管理打印和数字渠道的成本，并在这些渠道中提供全面、一致的体验。

作为营销人员，您可以在[!DNL Experience Manager Assets]中存储和管理模板，并使用单个基本模板轻松创建多个个性化打印体验。 您可以创建各种类型的营销宣传资料，包括小册子、传单、明信片、名片等，以便向客户清楚地传达您的营销信息。 您还可以从现有或新的打印输出组合多页打印输出。 最重要的是，您可以轻松地同时提供数字和打印体验，从而为用户提供一致的集成体验。

虽然资产模板大多是[!DNL Adobe InDesign]文件，但熟练掌握[!DNL Adobe InDesign]并不妨碍创建出色的工件。 您不需要将[!DNL Adobe InDesign]模板的字段映射到在创建目录时所需的产品字段。 可直接在Web界面上以WYSIWYG模式编辑模板。 但是，要使[!DNL Adobe InDesign]处理您的编辑更改，您必须首先将[!DNL Experience Manager Assets]配置为与[!DNL Adobe InDesign Server]集成。

能够从Web界面编辑[!DNL Adobe InDesign]模板有助于促进创意人员和营销人员之间的更大协作。 提高的内容速度缩短了营销抵押品的上市时间。

您可以使用资产模板实现以下目标：

* 从Web界面修改可编辑的模板字段。
* 控制文本的基本样式，例如，标签级别的字体大小、样式和文字。
* 使用内容选取器更改模板中的图像。
* 预览模板编辑。
* 合并多个模板文件，以便创建多页构件。

当您为宣传材料选择模板时，[!DNL Experience Manager Assets]将创建可编辑的模板副本。 原始模板将被保留，这将确保您的全局标牌保持不变，并且可重复使用以强制实施品牌一致性。

您可以以INDD、PDF或JPG格式导出父文件夹中的更新文件。 您还可以将这些格式的输出下载到本地文件系统。

## 创建宣传材料 {#creating-a-collateral}

考虑以下情景：您希望为即将到来的营销活动创建数字可打印的宣传资料，例如宣传册、传单和广告，并在全球范围内与折扣商店共享。 基于模板创建宣传材料有助于跨渠道提供统一的客户体验。 设计人员可以使用创意解决方案（如[!DNL InDesign]）创建营销活动模板（单页或多页），然后为您上传这些模板到[!DNL Experience Manager Assets]。 在创建宣传品之前，请提前在[!DNL Experience Manager]中上传一个或多个INDD模板并提供。

1. 在[!DNL Experience Manager]界面中，选择[!UICONTROL Assets]。

1. 从选项中选择&#x200B;**[!UICONTROL 模板]**。

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. 选择&#x200B;**[!UICONTROL 创建]**，然后从菜单中选择要创建的宣传品。 例如，选择&#x200B;**[!UICONTROL 宣传册]**。

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. 提前将一个或多个INDD模板上传到[!DNL Experience Manager]并可用。 选择小册子的模板，然后单击&#x200B;**[!UICONTROL 下一步]**。
1. 指定小册子的名称和可选描述。

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. （可选）单击&#x200B;**[!UICONTROL 标记]**&#x200B;并为宣传册选择一个或多个标记。 单击&#x200B;**[!UICONTROL 确认]**&#x200B;确认您的选择。
1. 单击&#x200B;**[!UICONTROL 创建]**。将显示一个对话框，确认已创建新宣传册。 单击&#x200B;**[!UICONTROL 打开]**&#x200B;以在编辑模式下打开宣传册。

   <!--![chlimage_1-106](assets/.png) -->

   或者，关闭对话框并导航到开始使用的“模板”页面中的文件夹，以查看您创建的宣传册。 宣传品的类型将显示在卡片视图的缩略图上。 例如，在本例中，缩略图上显示[!UICONTROL 宣传册]。

   ![chlimage_1-107](assets/chlimage_1-312.png)

## 编辑宣传品 {#editing-a-collateral}

您可以在创建宣传品后立即对其进行编辑。 或者，您也可以从[!UICONTROL 模板]页面或资产页面打开它。

1. 要打开宣传资料进行编辑，请执行下列操作之一：

   * 打开您在[创建宣传品片段](/help/assets/asset-templates.md#creating-a-collateral)的步骤7中创建的宣传品（本例中为宣传册）。
   * 在“模板”页面中，导航到创建宣传品的文件夹，然后单击宣传品缩略图上的[!UICONTROL 编辑]快速操作。
   * 在宣传品的资产页面中，单击工具栏中的&#x200B;**[!UICONTROL 编辑]**。
   * 选择宣传品，然后单击工具栏中的&#x200B;**[!UICONTROL 编辑]**。

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   资产查找器和文本编辑器将显示在页面左侧。 默认情况下，文本编辑器处于打开状态。

   使用文本编辑器修改要在文本字段中显示的文本。 您可以在标记级别修改字体大小、样式、颜色和文字。

   要使用资产查找器，您可以浏览或搜索[!DNL Experience Manager Assets]中的图像，并将模板中的可编辑图像替换为您选择的图像。

   ![chlimage_1-109](assets/chlimage_1-314.png)

   可编辑的图像显示在右侧。 要使字段在[!DNL Experience Manager Assets]中可编辑，模板中的相应字段必须在[!DNL InDesign]中标记。 换言之，它们应在[!DNL InDesign]中标记为可编辑。

   >[!NOTE]
   >
   >确保您的[!DNL Experience Manager]部署与[!DNL InDesign Server]集成，以使[!DNL Experience Manager Assets]能够从[!DNL InDesign]模板中提取数据并使其可用于编辑。 有关详细信息，请参阅[将Experience Manager Assets与InDesign Server集成](/help/assets/indesign.md)。

1. 要修改可编辑字段中的文本，请单击可编辑字段列表中的文本字段，然后编辑该字段中的文本。

   ![chlimage_1-111](assets/chlimage_1-316.png)

   您可以使用提供的选项编辑文本属性，例如字体样式、颜色和大小。

1. 选择&#x200B;**[!UICONTROL 预览]**，以便预览文本更改。

1. 要交换图像，请选择&#x200B;**[!UICONTROL 资产查找器]** ![chlimage_1-113](assets/chlimage_1-318.png)。

1. 从可编辑字段列表中选择图像字段，然后将所需图像从资产选取器拖到可编辑字段中。

   ![chlimage_1-114](assets/chlimage_1-319.png)

   您还可以使用关键字、标记并根据其发布状态搜索图像。 您可以浏览[!DNL Experience Manager Assets]存储库并导航到所需图像的位置。

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. 选择&#x200B;**[!UICONTROL 预览]**，以便预览图像。
1. 要编辑多页宣传资料中的特定页面，请使用底部的页面导航器。

1. 在工具栏上选择&#x200B;**[!UICONTROL 预览]**，以便预览所有更改。 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以保存对宣传品的编辑更改。

   >[!NOTE]
   >
   >仅当宣传品中的可编辑图像字段没有任何缺少图标时，才会启用“预览”和“完成”选项。 如果您的宣传资料中缺少图标，这是因为[!DNL Experience Manager]无法解析[!DNL InDesign]模板中的图像。 通常，[!DNL Experience Manager]在以下情况下无法解析图像：
   >
   >* 图像未嵌入到基础[!DNL InDesign]模板中。
   >* 从本地文件系统链接图像。
   >
   >要使[!DNL Experience Manager]能够解析图像，请执行以下操作：
   >
   >* 创建[!DNL InDesign]模板时嵌入图像（请参阅[关于链接和嵌入的图形](https://helpx.adobe.com/indesign/using/graphics-links.html)）。
   >* 将[!DNL Experience Manager]装载到本地文件系统，然后将缺少的图标与[!DNL Experience Manager]中的现有资源进行映射。
   >
   >有关使用[!DNL InDesign]文档的更多信息，请参阅使用Experience Manager](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html)中的InDesign文档的[最佳实践。

1. 要为宣传册生成PDF演绎版，请选择对话框中的Acrobat选项，然后单击&#x200B;**[!UICONTROL 继续]**。
1. 宣传品部分是在您开始使用的文件夹中创建的。 要查看格式副本，请打开宣传品，然后从GlobalNav列表中选择&#x200B;**[!UICONTROL 格式副本]**。

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. 从格式副本列表中选择PDF格式副本，以便下载PDF文件。 打开PDF文件以查看宣传品。

   ![chlimage_1-119](assets/chlimage_1-324.png)

## 合并宣传品 {#merge-collateral}

1. 在[!DNL Experience Manager]界面中，选择“导航”页面上的[!UICONTROL Assets]。

1. 从选项中选择&#x200B;**[!UICONTROL 模板]**。

1. 选择&#x200B;**[!UICONTROL 创建]**，然后从菜单中选择&#x200B;**[!UICONTROL 合并]**。

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. 从[!UICONTROL 模板合并]页面中，选择&#x200B;**[!UICONTROL 合并]** ![添加资源](assets/do-not-localize/assets_add_icon.png)。

1. 定位至要合并的宣传品段的位置，选择要合并的宣传品缩略图以将其选定。

   ![chlimage_1-122](assets/chlimage_1-327.png)

   您还可以从Omnisearch框中搜索模板。

   您可以浏览[!DNL Experience Manager Assets]存储库或收藏集，导航到所需模板的位置，然后选择要合并的模板。

   您可以应用各种筛选器来搜索所需的模板。 例如，您可以根据文件类型或标记搜索模板。

1. 从工具栏中选择&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**[!UICONTROL 预览和重新排序]**&#x200B;屏幕中，根据需要重新排列模板并预览要合并的模板选择。 从工具栏中选择&#x200B;**[!UICONTROL 下一步]**。

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. 在[!UICONTROL 配置模板]屏幕中，指定宣传品的名称。 （可选）指定您认为合适的任何标记。 如果要以PDF格式导出输出，请选择&#x200B;**[!UICONTROL Acrobat (.PDF)]**。 默认情况下，以JPG和[!DNL InDesign]格式导出宣传品。 若要更改多页宣传品的显示缩略图，请单击&#x200B;**[!UICONTROL 更改缩略图]**。

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. 选择&#x200B;**[!UICONTROL 保存]**，然后选择&#x200B;**[!UICONTROL 确定]**&#x200B;关闭对话框。 多页宣传资料是在您开始使用的文件夹中创建的。

   >[!NOTE]
   >
   >您以后不能编辑合并的宣传品段，也不能使用它来创建其他宣传品段。

## 最佳实践和限制 {#best-practices-limitations-tips}

* [!DNL Experience Manager]中的[!DNL InDesign]编辑器在标记级别工作，单个标记下的所有文本被视为单个实体。 要在编辑时保留文本格式和样式，请单独标记每个段落（或使用不同样式的文本）。
