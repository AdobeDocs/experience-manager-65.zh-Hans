---
title: 目录生成器
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
description: 目录生成器
exl-id: 76a46c62-d47d-4970-8a3a-d56015639548
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: ht
source-wordcount: '846'
ht-degree: 100%

---

# 目录生成器{#catalog-producer}

了解如何在 AEM Assets 中使用目录生成器，通过您的数字资产生成产品目录。

借助 Adobe Experience Manager（AEM）Assets 的目录生成器，您可以使用从 InDesign 应用程序导入的 InDesign 模板为品牌产品创建目录。在导入 InDesign 模板之前，您需要先将 AEM Assets 与 InDesign Server 集成。

## 与 InDesign Server 集成 {#integrating-with-indesign-server}

在集成过程中，需要配置 **DAM 更新资产**&#x200B;工作流，该工作流适用于与 InDesign 集成。此外，还需要为 InDesign Server 配置代理工作器。有关详细信息，请参阅[将 AEM Assets 与 InDesign Server 集成](/help/assets/indesign.md)。

>[!NOTE]
>
>您可以在将 InDesign 文件导入 AEM Assets 之前，从这些文件生成 InDesign 模板。有关详细信息，请参阅[处理文件和模板](https://helpx.adobe.com/cn/indesign/using/files-templates.html)。
>
>您可以将 InDesign 模板中的元素映射到 XML 标记。在目录生成器中将产品属性与模板属性进行映射时，这些已映射的标记会显示为属性。要了解如何在 InDesign 文件中进行 XML 标记，请参阅[为 XML 标记内容](https://helpx.adobe.com/cn/indesign/using/tagging-content-xml.html)。

>[!NOTE]
>
>仅支持使用 InDesign 文件（.indd）作为模板。不支持扩展名为 .indt 的文件。

## 创建目录 {#creating-a-catalog}

目录生成器使用产品信息管理（PIM）数据，将产品属性与模板中显示的 XML 属性进行映射。要创建目录，请执行以下步骤：

1. 在 Assets 用户界面中，点击 **AEM 徽标**，然后依次选择 **资产 > 目录**。
1. 在&#x200B;**目录**&#x200B;页面中，从工具栏点击&#x200B;**创建**，然后在列表中选择&#x200B;**目录**。
1. 在&#x200B;**创建目录**&#x200B;页面中，为目录输入名称和描述（可选），并指定标记（如有）。您还可以为目录添加缩略图。

   ![create_catalog](assets/create_catalog.png)

1. 单击&#x200B;**保存**。确认对话框会提示目录已创建。单击&#x200B;**完成**&#x200B;以关闭对话框。
1. 要打开您创建的目录，请在&#x200B;**目录**&#x200B;页面中点击该目录。

   >[!NOTE]
   >
   >您也可以在上一步提到的确认对话框中点击&#x200B;**打开**&#x200B;来打开目录。

1. 要向目录添加页面，请从工具栏点击&#x200B;**创建**，然后选择&#x200B;**新页面**&#x200B;选项。
1. 在向导中，为页面选择一个 InDesign 模板。然后点击&#x200B;**下一步**。
1. 为页面指定名称和可选的描述。请指定标记（如有）。
1. 在工具栏中点击&#x200B;**创建**。然后，在对话框中点击&#x200B;**打开**。产品属性会显示在左侧窗格中。InDesign 模板的预定义属性会显示在右侧窗格中。
1. 从左侧窗格将产品属性拖动到 InDesign 模板属性中，以创建映射关系。

   要实时查看页面效果，请点击右侧窗格中的&#x200B;**预览**&#x200B;选项卡。

1. 要创建更多页面，请重复步骤 6 – 9。要为其他产品创建类似页面，请选择页面，并从工具栏点击&#x200B;**创建类似页面**&#x200B;图标。

   ![创建类似页面](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >您只能为结构相似的产品创建类似页面。

   点击添加图标，在产品选择器中选择产品，然后从工具栏点击&#x200B;**选择**。

   ![select_product](assets/select_product.png)

1. 在工具栏点击&#x200B;**创建**。单击&#x200B;**完成**&#x200B;以关闭对话框。类似页面将会被添加到您的目录中。
1. 要将现有的 InDesign 文件添加到目录中，请从工具栏点击&#x200B;**创建**，然后选择&#x200B;**添加到现有页面**&#x200B;选项。
1. 选择 InDesign 文件，并从工具栏点击&#x200B;**添加**。然后点击&#x200B;**确定**&#x200B;以关闭对话框。

   如果目录页面中引用的产品元数据发生更改，这些更改不会自动反映在目录页面中。在引用目录页面的产品图像上会显示一个标记为&#x200B;**陈旧**&#x200B;的横幅，提示所引用产品的元数据不是最新的。

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   要确保产品图像反映最新的元数据更改，请在目录控制台中选择页面，并从工具栏点击&#x200B;**更新页面**&#x200B;图标。

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >要更改引用产品的元数据，请导航至“产品”控制台（**AEM 徽标** > **Commerce** > **产品**），并选择该产品。然后，从工具栏点击&#x200B;**查看属性**&#x200B;图标，并在资产的“属性”页面中编辑元数据。

1. 要重新排列目录中的页面，请从工具栏点击&#x200B;**创建**&#x200B;图标，然后在菜单中选择&#x200B;**合并**。在向导中，顶部的轮播允许您通过拖动重新排序页面。您也可以移除页面。

1. 单击&#x200B;**“下一步”。**&#x200B;要将现有的 InDesign 文件添加为封面页，请点击&#x200B;**选择封面页**&#x200B;框旁的&#x200B;**浏览**，并指定封面页模板的路径。
1. 点击&#x200B;**保存**，然后点击&#x200B;**完成**以关闭确认对话框。
选择**完成**选项后，会打开一个对话框，供您选择是否需要 .pdf 演绎版。
   ![导出到 pdf](assets/CatalogPDF.png)
如果选择了 Acrobat（PDF）选项，除了 InDesign 演绎版之外，还会在 **/jcr:content/renditions** 中生成一个 pdf 演绎版。您可以在下载对话框中勾选“演绎版”复选框来下载所有演绎版。

1. 要为已创建的目录生成预览，请在&#x200B;**目录**&#x200B;控制台中选择该目录，然后从工具栏点击&#x200B;**预览**&#x200B;图标。

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   在预览中查看目录中的页面。点击&#x200B;**关闭**&#x200B;来关闭预览。
