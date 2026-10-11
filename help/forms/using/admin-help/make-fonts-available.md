---
title: 使字体可用
description: 确保表单中使用的字体在托管AEM表单的J2EE应用程序服务器中可用。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
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
source-wordcount: '228'
ht-degree: 2%
---
# 使字体可用 {#make-fonts-available}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

确保表单中使用的字体在托管AEM表单的J2EE应用程序服务器中可用。 例如，请考虑以下方案。 表单设计人员将字体添加到Designer使用的字体目录中，并创建在单独的计算机上使用该字体的表单。 要使Output服务使用该字体，请将其放置在Customer fonts目录中。 如果Customer fonts目录不存在，请在托管AEM表单的J2EE应用程序服务器上创建一个目录。

有关其他字体设置的信息，请参阅[配置常规AEM表单设置](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)。

**指定Customer fonts目录的位置**

1. 在管理控制台中，单击设置>核心系统设置>配置。
1. 在“System Fonts目录的位置”框中，键入Customer Fonts目录的路径。 可以添加多个目录，用分号&#x200B;**；**&#x200B;分隔
1. 单击“确定”。
1. 重新启动安装了AEM表单的系统。

>[!NOTE]
>
>字体是从Windows系统字体缓存中挑选的，需要重新启动系统才能更新缓存。 指定Customer font目录后，请确保重新启动安装了AEM表单的系统。
