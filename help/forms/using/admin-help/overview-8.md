---
title: 输出服务概述
description: 输出允许您将XML表单数据与Designer中创建的表单设计合并，以创建各种格式的文档输出流。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e99b72d0-fbd5-4150-a225-1a91ad4c5867
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
source-wordcount: '263'
ht-degree: 3%
---
# 输出服务概述 {#overview-of-output-service}

输出允许您将XML表单数据与Designer中创建的表单设计合并，以创建各种格式的文档输出流。 输出流可以发送到网络打印机、本地打印机或磁盘文件

可以使用管理控制台中的“输出”页管理Output服务。 如果未通过AEM Forms API指定等效设置，则在运行时将使用您配置的设置。 通过AEM Forms SDK完成的配置将覆盖使用管理控制台配置的设置。

有关Output服务的详细信息，请参阅[服务参考](https://www.adobe.com/go/learn_aemforms_services_61)。

在管理控制台的“输出”页面上，可以执行多项任务：

* 指定国际化的字符集。 （请参阅[更改字符集](/help/forms/using/admin-help/change-character-set.md#change-the-character-set)。）
* 指定URL、URI、XCI和文件位置的绝对路径和相对路径。 （请参阅[为输出](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)指定文件位置。）
* 配置缓存大小和策略。 （请参阅[指定缓存模式](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode)和[配置缓存设置](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings)。）
* 使字体在应用程序服务器上可用。 （请参阅[使字体可用](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available)。）
* 指定要嵌入的字体。 （请参阅[指定要嵌入的字体](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed)。）
* 指定XCI配置选项。 （请参阅[指定XCI配置选项](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options)。）
* 指定安全设置。 （请参阅[指定安全设置](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings)。）

更改设置后，单击“保存”以将其应用于“输出”。 您不需要重新启动服务器以使更改生效，但在配置缓存设置时，您可能需要重新启动输出服务。
