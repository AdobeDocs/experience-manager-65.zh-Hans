---
title: 指定安全设置
description: 了解如何指定安全设置以保护XML数据文件。 安全设置功能控制XML输入中的外部实体。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1f544485-5a01-4a4a-ab0f-dcee67e1a38b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 1%

---

# 指定安全设置 {#specify-security-settings}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

输出使您可以控制是否解析XML输入中的外部实体。 默认情况下，这些问题会得到解决，但您可以更改此行为以提高AEM表单系统的安全性。

**阻止处理包含外部实体引用的XML数据文件**

1. 在管理控制台中，单击“服务”>“输出”。
1. 清除“解析外部图元”复选框。
1. 单击“保存”。
