---
title: 将水印添加到您的数字资产
description: 了解如何使用水印功能向资源添加数字水印。
contentOwner: AG
role: 业务从业者，管理员
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# 为您的数字资产设置水印{#watermarking}

[!DNL Adobe Experience Manager Assets] 允许您向资产添加数字水印，以帮助用户验证资产的真实性和版权所有权。[!DNL Experience Manager Assets] 支持将文本用作PNG和JPEG文件上的水印。

要能够对资产应用水印，请在[!UICONTROL DAM更新资产]工作流中添加水印步骤。

1. 访问[!DNL Experience Manager]用户界面，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 在&#x200B;**[!UICONTROL 工作流模型]**&#x200B;页面中，选择&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;工作流，然后单击&#x200B;**[!UICONTROL 编辑]**。

1. 从侧面板中，将&#x200B;**[!UICONTROL 添加水印]**&#x200B;步骤拖到[!UICONTROL DAM更新资产]工作流。

   ![拖动“添 [!UICONTROL 加] 水印”步骤并添加到 [!UICONTROL DAM更新资] 产流](assets/add_watermark_step_aem_assets.png)

   *图：拖动“ [!UICONTROL 添] 加水印”步骤并添加 [!UICONTROL 到DAM更新] 资产流。*

   >[!NOTE]
   >
   >将[!UICONTROL 添加水印]步骤放在[!UICONTROL 处理缩略图]步骤之前的任意位置。

1. 打开&#x200B;**[!UICONTROL 添加水印]**&#x200B;步骤以显示其属性。
1. 在&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡中，在各个字段中指定有效值，包括文本、字体类型、大小、颜色、位置、方向等。 要确认更改，请单击&#x200B;**[!UICONTROL 完成]**。

   ![在添加水印步骤中提供参数  [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *图：在中的添加水印步骤中提供参数 [!DNL Assets]。*

1. 使用水印步骤保存&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;工作流。
1. 从[!DNL Assets]用户界面上传示例资产。 在您在上述步骤中配置的位置，水印会以字体大小、颜色等显示。

要以编程方式或使用动态信息对PDF文档进行水印，请考虑使用[Experience Manager文档服务](/help/forms/using/overview-aem-document-services.md)产品。

## 提示和限制{#tips-limitations}

* 仅支持基于文本的水印。 图像不用作水印，即使您可以在创建[!UICONTROL 添加水印过程]时上传图像。
* 仅支持PNG和JPEG文件加水印。 其他资产格式不加水印。
