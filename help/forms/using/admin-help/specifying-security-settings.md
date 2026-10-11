---
title: 指定安全性设置
description: 了解如何指定安全设置以保护XML数据文件。 安全设置功能控制XML输入中的外部实体。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 004b8a2f-66a0-43a4-be56-7e42b703ebb2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
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
source-wordcount: '101'
ht-degree: 7%
---
# 指定安全性设置 {#specifying-security-settings}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

Forms允许您控制是否解析XML输入中的外部实体。 默认情况下，这些问题会得到解决，但您可以更改此行为以提高AEM表单系统的安全性。

**阻止处理包含外部实体引用的XML数据文件**

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 服务> Forms]**。
1. 清除“解析外部图元”复选框。
1. 单击&#x200B;**[!UICONTROL 保存]**。
