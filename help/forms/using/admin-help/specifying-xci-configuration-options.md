---
title: 指定 XCI 配置选项
description: 了解如何指定XCI配置选项 您可以为自适应表单指定自定义XCI文件值，以便在表单渲染时使用该值。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 6%
---
# 指定 XCI 配置选项 {#specifying-xci-configuration-options}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

Forms允许您指定可用于呈现的自定义XCI文件。 （请参阅[为Forms配置位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)。） 默认情况下，Forms会覆盖XCI文件中指定的某些选项，其中包括以下选项：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以选择取消上面所列选项覆盖的选项，在这种情况下，Forms使用自定义XCI文件中指定的值。

1. 在管理控制台中，单击&#x200B;**服务** > **Forms**。
1. 选中或取消选中使用系统默认XCI选项复选框。 如果选择该选项，Forms会将其默认值用于数据包、创建者、生成者和compressObjectStream设置。 取消选择此选项时，Forms使用自定义XCI文件中指定的值。
1. 单击&#x200B;**保存**。
