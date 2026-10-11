---
title: 更改字符集
description: 您可以指定用于编码输出流的字符集。 了解如何更改字符集。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9ff75d98-54ad-425d-912f-d5a7501bf564
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
source-wordcount: '144'
ht-degree: 6%
---
# 更改字符集 {#change-the-character-set}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

您可以指定用于编码输出流的字符集。

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 服务>输出]**。
1. 在“国际化”下的“字符集”列表中，选择一个字符集。 此设置依赖于通过API指定的`TransformationFormat`和`PrintFormat`。 要指定列出的字符集以外的字符集，请选择自定义，然后在显示的框中指定编码值。

   如果`TransformationFormat`是PDF，而PDF/A或`PrintFormat`是PCL、PostScript、Zebra标签、IPL、DPL、TPCL、GenericColorPCL或GenericPSLevel3，则仅支持特定字符集。

   字符集必须是有效的规范名称。 默认值为ISO-8859-1。

1. 单击&#x200B;**[!UICONTROL 保存]**。
