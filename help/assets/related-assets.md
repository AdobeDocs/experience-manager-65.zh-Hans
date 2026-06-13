---
title: 关联资产
description: 了解如何关联那些共享某些共用属性的数字资产。 此外，还可以在数字资源之间创建源派生的关系。
contentOwner: AG
role: User
feature: Collaboration,Asset Management
exl-id: ddb69727-74a0-4a4d-a14e-7d3bb5ceea2a
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 45%

---

# 关联资产 {#related-assets}

[!DNL Adobe Experience Manager Assets] 允许您使用相关的资产功能，根据您组织的需求手动关联资产。 例如，您可以将一个许可证文件与类似主题的一个资产或图像/视频相关联。 您可以关联那些共享某些共用属性的资产。 您还可以使用此功能创建资产之间的来源/派生关系。 例如，如果您有一个从 INDD 文件生成的 PDF 文件，就可以将这个 PDF 文件与其 INDD 源文件相关联。

使用此功能，您可以灵活地与供应商或机构共享一个低分辨率 PDF 文件或 JPG 文件，仅在接受请求时才提供高分辨率 INDD 文件。

>[!NOTE]
>
>只有对资产具有编辑权限的用户才能关联资产和取消关联。

## 关联资源 {#relating-assets}

1. 在 [!DNL Experience Manager] 界面中打开您想关联的资产的&#x200B;**[!UICONTROL 属性]**&#x200B;页面。

   ![打开资产的属性页面，以关联该资产](assets/asset-properties-relate-assets.png)

   *图： [!DNL Assets] [!UICONTROL 属性]页面与资源相关。*

   或者，从列表视图中选择资产。

   ![chlimage_1-273](assets/chlimage_1-273.png)

   您还可以从收藏集中选择资产。

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. 要将其他资源与您选择的资源相关联，请在工具栏中单击&#x200B;**[!UICONTROL 相关]** ![相关资源](assets/do-not-localize/link-relate.png)。
1. 执行下列操作之一：

   * 若要关联资产的源文件，请从列表中选择&#x200B;**[!UICONTROL Source]**。
   * 若要关联派生文件，请从列表中选择&#x200B;**[!UICONTROL 派生]**。
   * 若要在资产之间创建双向关系，请从列表中选择&#x200B;**[!UICONTROL 其他]**。

1. 从&#x200B;**[!UICONTROL 选择资源]**&#x200B;屏幕中，导航到要关联的资源的位置，然后选择该资源。

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. 单击&#x200B;**[!UICONTROL 确认]**。
1. 单击&#x200B;**[!UICONTROL 确定]**&#x200B;关闭对话框。 根据您在步骤3中选择的关系，**[!UICONTROL 相关]**&#x200B;部分中的相应类别下列出了相关资产。 例如，如果您关联的资产是当前资产的源文件，它就会列在&#x200B;**[!UICONTROL 来源]**&#x200B;下。

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. 要取消关联某个资源，请在工具栏中单击&#x200B;**[!UICONTROL 取消关联]** ![取消关联资源](assets/do-not-localize/link-unrelate-icon.png)。

1. 从&#x200B;**[!UICONTROL 删除关系]**&#x200B;对话框中选择要取消关联的资源，然后单击&#x200B;**[!UICONTROL 取消关联]**。

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. 单击&#x200B;**[!UICONTROL 确定]**&#x200B;关闭对话框。 您为其删除关系的资源将从&#x200B;**[!UICONTROL 相关]**&#x200B;部分下的相关资源列表中删除。

## 翻译关联的资产 {#translating-related-assets}

使用关联资产功能创建资产之间的来源/派生关系，这在翻译工作流中也很有帮助。 如果您在派生资产上运行翻译工作流，[!DNL Experience Manager Assets] 会自动获取源文件引用的任何资产，并将其包含用于翻译。 通过这种方式，源资产引用的资产会与源资产和派生资产一起被翻译。 例如，假定您的英语副本包含派生的资源及其源文件，如图所示。

![chlimage_1-281](assets/chlimage_1-281.png)

如果源文件与另一个资产关联，[!DNL Experience Manager Assets] 就会获取被引用的资产，并将其包含用于翻译。

![资源属性页面显示要包含以进行翻译的相关资源的源文件](assets/asset-properties-source-asset.png)

*图：要包含以进行翻译的相关资源的Source资源。*

1. 执行[创建翻译项目](translation-projects.md#create-a-new-translation-project)中的步骤，将源文件夹中的资源翻译为目标语言。 例如，在本例中，请将您的资产翻译为法语。

1. 从[!UICONTROL 项目]页面，打开翻译文件夹。

1. 单击项目拼贴以打开详细信息页面。

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. 单击翻译作业信息卡下方的省略号可查看翻译状态。

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. 选择资源，然后单击工具栏中的&#x200B;**[!UICONTROL 在Assets中展现]**&#x200B;以查看资源的翻译状态。

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. 要验证与源相关的资产是否已翻译，请单击源资产。

1. 选择与源相关的资源，然后单击Assets中的&#x200B;**[!UICONTROL 显示]**。 将显示已翻译的相关资产。
