---
title: Camera raw支持
description: 了解如何在Adobe Experience Manager Assets中启用Camera raw支持。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0b8472dbfbfe326b4b5fe0d43b0f361318b37d16

---


# 支持使用Camera Raw处理图像 {#camera-raw-support}

您可以启用Camera raw支持来处理CR2、NEF和RAF等原始文件格式，并以JPEG格式渲染图像。 Adobe Experience Manager资产中使用通过包共享提供的 [Camera raw包支持](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) 此功能。

>[!NOTE]
>
>该功能仅支持JPEG再现。 Windows 64位、Mac OS和RHEL 7.x支持此功能。

要在Adobe Experience Manager资产中启用Camera raw支持，请执行以下步骤：

1. 从包共 [享中下载Camera Raw包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) 。
1. 访问 `https://[aem_server]:[port]/workflow`. 打开 **[!UICONTROL DAM更新资产工作流]** 。
1. 打开“流 **[!UICONTROL 程缩略图]** ”步骤。
1. 在“缩略图”选项卡中提供 **[!UICONTROL 以下配置]** :

   * **[!UICONTROL 缩略图]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL 跳过 MIME 类型]**: `skip:image/dng, skip:image/x-raw-(.*)`
   ![chlimage_1-128](assets/chlimage_1-334.png)

1. 在“启 **[!UICONTROL 用Web的图像]** ”选项卡的“跳 **[!UICONTROL 过列表”字段中]** ，指定 `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`。

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. 从侧面板中，在“缩览图创建” **[!UICONTROL 步骤下添加Camera Raw/DNG处理程序]****[!UICONTROL 步骤]** 。
1. 在Camera Raw/ **[!UICONTROL DNG处理程序步骤中]** ，在“参数”选项卡中添加以 **[!UICONTROL 下配置]** :

   * **[!UICONTROL MIME类型]**: `image/dng` 和 `image/x-raw-(.*)`
   * **[!UICONTROL Command]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`
   ![chlimage_1-130](assets/chlimage_1-336.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

>[!NOTE]
>
>确保以上配置与Camera RAW和DNG处理步 **[!UICONTROL 骤配置中的示例DAM更新资产相同]** 。

您现在可以将相机原始数据文件导入AEM资产。 安装Camera RAW包并配置所需的工作流程后，侧窗格列表中会 **[!UICONTROL 显示“图像调整]** ”选项。

![chlimage_1-131](assets/chlimage_1-337.png)


*图：侧窗格中的选项。*

![chlimage_1-132](assets/chlimage_1-338.png)


*图：使用选项对图像进行轻量级编辑。*

将编辑保存到Camera raw图像后，将为该图像生 `AdjustedPreview.jpg` 成新的再现。 对于除Camera raw之外的其他图像类型，更改会反映在所有再现中。

## 最佳实践、已知问题和限制 {#best-practices}

该功能具有以下限制：

* 该功能仅支持JPEG再现。 Windows 64位、Mac OS和RHEL 7.x支持此功能。
* RAW和DNG格式不支持元数据写回。
* Camera raw库在每次可处理的像素总数方面存在限制。 目前，它最多可以处理文件长边的65000像素，或者处理先遇到的条件为512 MP。
