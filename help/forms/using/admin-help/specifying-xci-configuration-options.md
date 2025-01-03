---
title: 指定XCI配置选项
description: 了解如何指定XCI配置选项 您可以为自适应表单指定自定义XCI文件值，以便在表单渲染时使用该值。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 1%

---

# 指定XCI配置选项 {#specifying-xci-configuration-options}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

Forms允许您指定可用于呈现的自定义XCI文件。 (请参阅[为Forms配置位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)。)默认情况下，Forms会覆盖XCI文件中指定的某些选项，包括：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以选择取消上面所列选项覆盖的选项，在这种情况下，Forms使用自定义XCI文件中指定的值。

1. 在管理控制台中，单击&#x200B;**服务** > **Forms**。
1. 选中或取消选中使用系统默认XCI选项复选框。 如果选择该选项，Forms会将其默认值用于数据包、创建者、生成者和compressObjectStream设置。 取消选择此选项时，Forms使用自定义XCI文件中指定的值。
1. 单击&#x200B;**保存**。
