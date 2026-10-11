---
title: 导入和导出配置文件
description: 了解如何导入和导出配置文件以编辑服务器首选项或配置其他AEM表单产品实例。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
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
source-wordcount: '264'
ht-degree: 4%
---
# 导入和导出配置文件 {#importing-and-exporting-the-configuration-file}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

使用“手动配置”页可以以XML格式下载配置设置的副本。 此文件中的设置控制所有服务器首选项。 然后，您可以编辑该文件并将其上传回服务器。 您还可以使用文件配置另一个AEM Forms产品实例。

为避免安全风险，导出的配置文件中不包含目录服务器的绑定密码值。 在将文件导入到新系统之前，请更新XML文件中的密码。

>[!NOTE]
>
>导入配置文件会根据文件中的信息重新配置AEM表单。 只有熟悉AEM Forms产品和XML的系统管理员或专业服务顾问才应考虑修改配置文件。 用户可能需要编辑配置文件，例如，重新配置损坏的设置。

**导出配置信息**

1. 在Administration Console中，单击Settings > User Management > Configuration > Import and Export Configuration Files。
1. 单击“导出”。 如果您使用的是Microsoft Internet Explorer，系统会提示您指定保存文件的位置。 如果您使用的是Firefox，则文件会保存在您的桌面上。

**导入配置信息**

1. 在Administration Console中，单击Settings > User Management > Configuration > Import and Export Configuration Files。
1. 单击“浏览”查找配置文件，单击“导入”，然后单击“确定”。
