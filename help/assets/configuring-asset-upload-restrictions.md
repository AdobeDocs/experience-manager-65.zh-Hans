---
title: 配置资产上传限制
description: 限制用户可以上传的资源类型（文件）
contentOwner: AG
role: Developer, Admin
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: cda65036-5305-4f01-89da-9b3506ae8c50
    internal-label: Administration
subfeature_v2:
  - id: f1dc0c96-022d-4003-afbe-47bd40173c4a
    internal-label: Upload assets
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 9%
---
# 配置资产上传限制 {#configuring-asset-upload-restrictions}

您可以将[!DNL Adobe Experience Manager Assets]配置为限制用户可以上传的资源类型。 它有助于防止意外上传不需要的格式和恶意文件。 通过`Day CQ DAM Asset Upload Restriction`服务，您可以控制用户可以上传的文件类型。 默认情况下，[!DNL Assets]允许用户上传所有MIME类型的资产。 但是，您可以将服务配置为限制用户仅上载特定MIME类型的文件。

1. 打开Configuration Manager web控制台。 访问`https://[aem_server]:[port]/system/console/configMgr`。
1. 在编辑模式下打开&#x200B;**[!UICONTROL Day CQ DAM资产上传限制]**&#x200B;服务。 默认情况下，**允许所有MIME**&#x200B;选项处于选中状态，该选项允许用户上传所有MIME类型的文件。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. 要限制用户仅上载某些MIME类型的文件，请取消选中&#x200B;**[!UICONTROL 允许所有MIME]**&#x200B;选项，并使用正则表达式在&#x200B;**[!UICONTROL 允许的资产MIME (regex)]**&#x200B;字段中指定允许的MIME类型。

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;即可保存更改。 如果为允许的MIME类型指定MIME字符串，则对于任何MIME类型与这些字段中配置的MIME字符串不匹配的资源，上传操作都将失败。
