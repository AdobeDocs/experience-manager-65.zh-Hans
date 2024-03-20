---
title: 使用Apache Tika检测MIME类型的资源
description: 启用Apache Tika以帮助 [!DNL Experience Manager Assets] 在上传操作期间，从内容流中检测资源的MIME类型，而不是文件扩展名。
contentOwner: AG
role: Admin, Architect
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 使用以下方式检测MIME类型的资源 [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

通常情况下， [!DNL Adobe Experience Manager Assets] 检测您从其文件扩展名上传的资源的MIME类型。

如果您使用 [!DNL Apache Tika] 要上传资源， [!DNL Assets] 在上传操作期间从内容流中检测其MIME类型，而不是文件扩展名。

默认情况下，此功能处于禁用状态。 要启用该功能，请配置 **[!UICONTROL Day CQ DAM Mime类型]** 服务来源 [!UICONTROL 配置管理器].

>[!NOTE]
>
>使用检测的MIME类型 [!DNL Apache Tika] 库是一项资源密集型操作。

1. 要打开Configuration Manager Web控制台，请访问 `https://[aem_server]:[port]/system/console/configMgr`.

1. 在服务列表中，找到 **[!UICONTROL Day CQ DAM Mime类型服务]** 并单击 **[!UICONTROL 编辑]**.

1. 选择 **[!UICONTROL 从内容中检测MIME]** 选项，用于在忽略文件扩展名的同时启用对已上传资源的解析以确定其MIME类型。 默认情况下，此选项处于未选中状态。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 单击 **[!UICONTROL 保存]** 以保存更改。
