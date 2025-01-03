---
title: 提供字体
description: 确保表单中使用的字体可用于托管AEM表单的J2EE应用程序服务器。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 2%

---

# 提供字体 {#make-fonts-available}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

确保表单中使用的字体可用于托管AEM表单的J2EE应用程序服务器。 例如，请考虑以下方案。 表单设计人员将字体添加到Designer使用的字体目录中，并创建在单独的计算机上使用该字体的表单。 要使Output服务使用该字体，请将其放置在Customer fonts目录中。 如果Customer fonts目录不存在，请在托管AEM表单的J2EE应用程序服务器上创建一个目录。

有关其他字体设置的信息，请参阅[配置常规AEM表单设置](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)。

**指定Customer fonts目录的位置**

1. 在管理控制台中，单击设置>核心系统设置>配置。
1. 在“System Fonts目录的位置”框中，键入Customer Fonts目录的路径。 可以添加多个目录，用分号&#x200B;**；**&#x200B;分隔
1. 单击“确定”。
1. 重新启动安装了AEM表单的系统。

>[!NOTE]
>
>字体是从Windows系统字体缓存中挑选的，需要重新启动系统才能更新缓存。 指定Customer font目录后，请确保重新启动安装了AEM表单的系统。
