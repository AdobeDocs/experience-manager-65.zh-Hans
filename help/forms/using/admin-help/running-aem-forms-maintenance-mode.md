---
title: 在维护模式下运行 AEM Forms
description: 在执行诸如为DSC打补丁、升级AEM表单或应用Service Pack等任务时，维护模式很有用。 了解有关在维护模式下运行AEM表单的更多信息。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
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
source-wordcount: '259'
ht-degree: 4%
---
# 在维护模式下运行 AEM Forms {#running-aem-forms-in-maintenance-mode}

在执行诸如为DSC打补丁、升级AEM表单或应用Service Pack等任务时，维护模式很有用。

避免在服务器处于维护模式时调用任何进程。 如果在服务器处于维护模式时调用进程，则会发生以下情况：

* 如果进程是长期的，则会将其添加到作业数据库，但不会启动。 当您退出维护模式时，AEM表单会处理其队列中的长期作业，即使服务器在维护模式下重新启动也是如此。
* 如果处理的时间较短，则会立即进行处理。

**将AEM表单置于维护模式**

1. 在Web浏览器中，输入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   浏览器窗口中将显示“现已暂停”消息。

   >[!NOTE]
   >
   >如果在服务器处于维护模式时将其关闭，则在重新启动时它仍处于维护模式。 完成维护任务后关闭维护模式。

**检查AEM表单是否正在维护模式下运行**

1. 在Web浏览器中，输入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   状态将显示在浏览器窗口中。 状态“true”表示服务器正在维护模式下运行，“false”表示服务器不在维护模式下。

**关闭维护模式**

1. 在Web浏览器中，输入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   浏览器窗口中将显示“正在运行”消息。
