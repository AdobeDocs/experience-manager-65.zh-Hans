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
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 1%

---

# 更改字符集 {#change-the-character-set}

您可以指定用于编码输出流的字符集。

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 服务>输出]**。
1. 在“国际化”下的“字符集”列表中，选择一个字符集。 此设置依赖于通过API指定的`TransformationFormat`和`PrintFormat`。 要指定列出的字符集以外的字符集，请选择自定义，然后在显示的框中指定编码值。

   如果`TransformationFormat`PDF且PDF/A或`PrintFormat`为PCL、PostScript、Zebra标签、IPL、DPL、TPCL、GenericColorPCL或GenericPSLevel3，则仅支持特定字符集。

   字符集必须是有效的规范名称。 默认值为ISO-8859-1。

1. 单击&#x200B;**[!UICONTROL 保存]**。
