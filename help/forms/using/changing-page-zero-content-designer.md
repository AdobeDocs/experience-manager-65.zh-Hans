---
title: 在 Designer 中更改 Page Zero 内容
description: 在非Adobe PDF查看器中查看XFA PDF时，您知道如何更改在该页面的第0页上显示的消息吗？
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Forms Designer,Designer
exl-id: 466b7e85-a2f8-4e1e-8afc-1566b0ccb84c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 1af3c3d4-88d7-5e0f-813c-eb70824bfcdd
    internal-label: Forms Designer
  - id: 794033c1-20ea-55a4-a8a6-b1107e12deb0
    internal-label: Designer
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
source-wordcount: '232'
ht-degree: 6%
---
# 在 Designer 中更改 Page Zero 内容 {#changing-page-zero-content-in-designer}

如果非Adobe PDF查看器（如[!DNL Chrome]或[!DNL Firefox]中的默认PDF查看器）无法读取PDF/XFA表单的内容，则默认显示零页内容。 默认的Page Zero消息如下所示。

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms]版本的Designer允许您更改在第0页上显示的消息。 要更改Page Zero消息，请执行以下步骤：

1. 确保您已安装[!DNL AEM Forms]版本的Designer。 您可以从设计器的“关于”屏幕中检查版本。

1. 打开要为其更改“页面零”内容的表单。

1. 单击&#x200B;**[!UICONTROL 文件]** > **[!UICONTROL 表单属性]**。

1. 在[!UICONTROL 表单属性]对话框中，单击![加号](assets/plus.png)（加号图标）以添加自定义属性。

1. 将&#x200B;**_pagezerocontent**&#x200B;指定为属性的名称。
1. 以富文本格式添加新的“页面零”消息作为值。 例如：


   `<body xmlns="http://www.w3.org/1999/xhtml" xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </span></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </span>https://www.adobe.com/go/reader_download_cn.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </span></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </span>https://www.adobe.com/go/acrreader_cn.</p></body>`

1. 将表单另存为PDF。

1. 在浏览器中查看PDF表单，确认消息已更新。 上面的示例值如下所示：

   ![changedmessage](assets/changedmessage.png)

>[!NOTE]
>
>重新打开表单时，您创建的自定义属性可能无法正确显示在表单属性对话框中。 但是，它可正常使用，并且表单会显示更新的零页消息。
