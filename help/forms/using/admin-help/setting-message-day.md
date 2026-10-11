---
title: 设置每日消息
description: 每天的消息允许您设置一条显示在Workspace用户界面的“欢迎”页面上的消息。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d8bab1c4-b830-4491-9486-d7e7f4dc2c99
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
source-wordcount: '186'
ht-degree: 7%
---
# 设置每日消息 {#setting-the-message-of-the-day}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

您可以在Workspace用户界面中设置要显示在欢迎页面上的消息。

如有必要，您可以使用Adobe Flash® Player支持的HTML标记来设置文本外观的格式：

* &lt;a>锚点标记
* &lt;b>粗体标记
* &lt;br>中断标记
* &lt;font>字体标记
* &lt;img>图像标记
* &lt;i>斜体标记
* &lt;li>列表项标记
* &lt;p>段落标记
* &lt;span> Span标记
* &lt;textformat>文本格式标记
* &lt;u>为标记加下划线

有关支持的标记的详细信息，请参阅[Flex语言参考](https://flex.apache.org/)中TextField类的`htmlText`属性的定义。

## 设置当天消息 {#set-the-message-of-the-day}

1. 在管理控制台中，单击服务> Workspace >每日消息。
1. 在当天消息框中，提供要在欢迎屏幕上显示的文本。
1. 单击“保存”。

>[!NOTE]
>
>AEM Forms版本已弃用Flex Workspace。
