---
title: 运行Administration Console时的注意事项
description: 本文档列出了运行Administration Console时要考虑的一些要点。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
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
source-wordcount: '147'
ht-degree: 0%
---
# 运行Administration Console时的注意事项 {#considerations-when-running-administrationconsole}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

运行Administration Console时需要考虑以下几点：

* 如果使用URL `https://[hostname]:'port'/adminui`访问管理控制台，则指定的主机名不能包含下划线字符。 否则，指向管理控制台某些区域的链接可能无法正常工作。
* 如果在日语操作系统的Windows资源管理器中运行管理控制台，则可能会遇到以下问题：

  * 单击链接会返回登录页面，而不是预期的链接。
  * 单击链接会显示权限错误。

  最佳实践是从其他浏览器（如Mozilla Firefox）运行管理控制台，以确保没有任何链接失败。

* 在管理控制台中执行搜索时，请勿使用反斜杠字符()。
