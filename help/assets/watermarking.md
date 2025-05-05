---
title: 向数字资产添加水印
description: 了解如何使用水印功能向资源添加数字水印。
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 4%

---

# 为您的数字资产添加水印 {#watermarking}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager Assets]允许您向资产添加数字水印，以帮助用户验证资产的真实性和版权所有权。 [!DNL Experience Manager Assets]支持在PNG和JPEG文件上用作水印的文本。

要对资产应用水印，请在[!UICONTROL DAM更新资产]工作流中添加水印步骤。

1. 访问[!DNL Experience Manager]用户界面，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 从&#x200B;**[!UICONTROL 工作流模型]**&#x200B;页面中，选择&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;工作流，然后单击&#x200B;**[!UICONTROL 编辑]**。

1. 从侧面板中，将&#x200B;**[!UICONTROL 添加水印]**&#x200B;步骤拖动到[!UICONTROL DAM更新资产]工作流。

   ![拖动[!UICONTROL 添加水印]步骤并添加到[!UICONTROL DAM更新资产]工作流](assets/add_watermark_step_aem_assets.png)

   *图：拖动[!UICONTROL 添加水印]步骤并将它添加到[!UICONTROL DAM更新资产]工作流。*

   >[!NOTE]
   >
   >将[!UICONTROL 添加水印]步骤放在[!UICONTROL 处理缩略图]步骤之前的任意位置。

1. 打开&#x200B;**[!UICONTROL 添加水印]**&#x200B;步骤以显示其属性。
1. 在&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡中，指定各字段中的有效值，包括文本、字体类型、大小、颜色、位置、方向等。 要确认更改，请单击&#x200B;**[!UICONTROL 完成]**。

   ![在[!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)的添加水印步骤中提供参数

   *图：在[!DNL Assets].*&#x200B;的添加水印步骤中提供参数

1. 使用水印步骤保存&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;工作流。
1. 从[!DNL Assets]用户界面上传示例资源。 水印以字体大小、颜色等显示在您在上述步骤中配置的位置。

若要以编程方式或使用动态信息对PDF文档添加水印，请考虑使用[Experience Manager文档服务](/help/forms/using/overview-aem-document-services.md)产品。

## 提示和限制 {#tips-limitations}

* 仅支持基于文本的水印。 图像不用作水印，即使您在创建[!UICONTROL 添加水印进程]时可以上载图像。
* 仅支持PNG和JPEG文件添加水印。 其他资产格式没有添加水印。
