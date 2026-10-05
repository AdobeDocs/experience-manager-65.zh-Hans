---
title: 启用多线程文件转换
description: 了解如何启用多线程文件转换。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 4a55f87d3b8aa9944f0b32760aa645c42efd93e8
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%
---
# 启用多线程文件转换 {#enabling-multi-threaded-file-conversions}

PDF Generator可以同时运行多个文件转换以提高转换吞吐量。 选择适用的转换模式：

| 转换模式 | 支持并发转换的应用程序 | 用户帐户模型 |
|---|---|---|
| 多用户模式 | OpenOffice | 每个OpenOffice实例运行的是单独的用户帐户。 |
| 单用户模式 | ® Word和Microsoft® Excel | 一个用户帐户运行多个Word和Excel实例。 PowerPoint转换仍保持序列化。 |

在启用任一模式之前，请为您使用的应用程序和操作系统完成[PDF Generator预安装配置](/help/forms/using/install-configure-document-services.md#preinstallationconfigurations)。 有关支持的应用程序版本，请参阅[PDF Generator的软件支持](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)。

## 多用户模式 {#multi-user-mode}

在多用户模式下，PDF Generator会在单独的用户帐户下启动每个OpenOffice实例。 为所需的并发转化数量配置足够的有效管理用户帐户。 在群集中，在每个节点上配置相同的帐户。

在Windows上，确保PDF Generator用户具有[Replace进程级令牌特权](/help/forms/using/install-configure-document-services.md#grant-the-replace-a-process-level-token-privilege)，并完成[配置文档服务](/help/forms/using/install-configure-document-services.md#disable-user-account-control-uac)中描述的适用用户帐户控制配置。

### OpenOffice转换 {#openoffice-conversions}

为可同时运行的每个OpenOffice实例配置一个PDF Generator用户帐户。 将OpenOffice安装在每个配置的用户都可以访问的位置，并取消每个用户的初始OpenOffice激活对话框。

对于基于UNIX的系统，请在[配置文档服务](/help/forms/using/install-configure-document-services.md#preinstallationconfigurations)中完成OpenOffice安装和用户权限要求。

## Windows上的单用户模式 {#single-user-mode-on-windows}

单用户模式允许PDF Generator在一个配置的用户帐户下运行并发转化。

在此模式下，® Word（DOC和DOCX）和Excel（XLS和XLSX）的多个实例在同一用户下运行。 ® PowerPoint（PPT和PPTX）不支持单用户模式。 PDF Generator一次只能启动一个PowerPoint实例，因此PowerPoint转换会序列化。

要为Word和Excel转换启用单用户模式，请执行以下操作：

1. 在管理控制台中，导航到&#x200B;**主页>服务>应用程序和服务>服务管理**。
1. 筛选&#x200B;**PDF Generator**&#x200B;并选择&#x200B;**GeneratePDFervice**。
1. 在&#x200B;**配置**&#x200B;选项卡上，配置以下选项：

   * 将PDFMaker **的**&#x200B;启用单用户模式设置为&#x200B;**true**。
   * 将&#x200B;**PDFMaker池大小**&#x200B;设置为可以同时运行转换的最大Word实例数。
   * 将&#x200B;**Native2PDF**&#x200B;的“启用单用户模式”设置为&#x200B;**true**。
   * 将&#x200B;**Native2PDF池大小**&#x200B;设置为可以同时运行转换的最大Excel实例数。

1. 重新启动AEM Forms服务器。
