---
title: 配置 AEM DS 设置
description: 了解如何在提交表单之前指定处理服务器URL。
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: c43cab7b-3421-4e1b-a834-b2dd6eb23c1d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
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
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 3%
---
# 配置 AEM DS 设置{#configuring-aem-ds-settings}

本文介绍了如何配置&#x200B;**AEM DS设置服务**。 此设置可用于多种场景，例如：

* 在通信管理中

  * 用于配置AEM Forms工作流程
  * 使用Forms门户远程保存草稿/提交内容时

* 在自适应表单中，适用于从发布实例提交自适应表单的情况

以下是配置&#x200B;**[!UICONTROL AEM DS设置]**&#x200B;的步骤：

1. 使用URL在发布实例上打开配置管理器：\
   *https://localhost:port/system/console/configMgr*。

   ![AEM Web控制台配置](assets/web_configuration_console_new.png)

1. 在&#x200B;**[!UICONTROL Adobe Experience Manager Web控制台配置]**&#x200B;窗口中，找到并单击&#x200B;**[!UICONTROL AEM DS设置]**&#x200B;选项。

   ![DS设置](assets/ds_settings_new.png)

1. **[!UICONTROL AEM DS设置服务]**&#x200B;窗口显示AEM DS组件的通用配置设置。

   ![DS设置服务](assets/ds_settings_service_new.png)

1. 在相应字段中添加以下信息：

   **[!UICONTROL 处理服务器URL]**：处理服务器是必须触发Forms或AEM工作流的服务器。 这可以与AEM创作实例的URL或其他服务器URL（即https://localhost:port/）相同。

   **[!UICONTROL 正在处理服务器用户名]**：工作流用户的用户名[基于正在使用的服务器URL]

   **[!UICONTROL 正在处理服务器密码]**：工作流用户的密码

   >[!NOTE]
   >
   >
   >    
   >    
   >    * 使用Forms或AEM工作流时，在从发布服务器进行任何提交之前，必须配置DS设置服务。 否则，表格提交将失败。
   >    
   >
