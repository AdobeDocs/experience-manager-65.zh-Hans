---
title: 识别 PDF 文档中的有效证书和过期证书
description: 了解如何在PDF文档中识别有效证书和过期的证书。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 8%
---
# 识别 PDF 文档中的有效证书和过期证书 {#recognizing-valid-and-expired-certificates-in-pdf-documents}

在Adobe Reader中打开具有Reader扩展应用的使用权限的PDF文档时，将显示一个状态栏，其中描述在PDF文档中启用的特定使用权限。

当指定PDF文档使用权限的数字证书过期并在Adobe Reader中打开PDF文档时，会出现一个对话框，告知用户该PDF文档具有使用权限，但这些权限被禁用。 尽管消息表明PDF文档被更改或篡改，但情况不一定如此。 当证书过期或修改文档时，Adobe Reader会显示此消息。 在Adobe Reader 7.0.x或更高版本中，无法确定当前问题是哪种情况。

关闭对话框后，Adobe Reader将打开PDF文档。 使用Acrobat Reader DC扩展应用的使用权限无法按预期使用。 如果PDF文档是交互式表单，则表单字段会被锁定，用户无法更改表单数据。
