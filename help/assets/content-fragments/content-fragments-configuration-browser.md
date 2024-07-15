---
title: 内容片段 – 配置浏览器
description: 了解如何在配置浏览器中启用某些内容片段功能，以便使用Adobe Experience Manager强大的Headless投放功能。
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 49%

---

# 内容片段 – 配置浏览器{#content-fragments-configuration-browser}

了解如何在配置浏览器中启用某些内容片段功能，以便使用Adobe Experience Manager (AEM)强大的Headless投放功能。

## 为您的实例启用内容片段功能 {#enable-content-fragment-functionality-instance}

在使用内容片段之前，请使用&#x200B;**配置浏览器**&#x200B;启用以下功能：

* **内容片段模型** – 强制
* **GraphQL 持久查询** – 可选

>[!CAUTION]
>
>如果未启用&#x200B;**内容片段模型**，则：
>
>* 对于创建模型将无&#x200B;**创建**&#x200B;选项可用。
>* 您无法[选择Sites配置来创建相关的端点](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint)。

要启用内容片段功能，您需要进行以下操作：

* 通过配置浏览器启用内容片段功能
* 将配置应用到 Assets 文件夹

### 在配置浏览器中启用内容片段功能 {#enable-content-fragment-functionality-in-configuration-browser}

要[使用某些内容片段功能](#creating-a-content-fragment-model)，您&#x200B;**必须**&#x200B;首先通过&#x200B;**配置浏览器**&#x200B;启用它们：

>[!NOTE]
>
>有关详细信息，请参阅[配置浏览器：](/help/sites-administering/configurations.md#using-configuration-browser)。

1. 导航到&#x200B;**工具**、**常规**，然后打开&#x200B;**配置浏览器**。

1. 使用&#x200B;**“创建”**&#x200B;来打开对话框，您需要：

   1. 指定&#x200B;**标题**。
   1. 要启用其用法，请选择
      * **内容片段模型**
      * **GraphQL 持久查询**

      ![定义配置](assets/cfm-conf-01.png)

1. 选择&#x200B;**“创建”**&#x200B;以保存定义。

<!-- 1. Select the location appropriate to your website. -->

### 将配置应用到 Assets 文件夹 {#apply-the-configuration-to-your-assets-folder}

为内容片段功能启用配置&#x200B;**global**&#x200B;后，将应用于任何Assets文件夹。

要将其他配置（即不包括全局配置）与类似的Assets文件夹一起使用，您必须定义连接。 这是通过在适当文件夹的&#x200B;**文件夹属性**&#x200B;的 **Cloud Services** 选项卡中选择适当的&#x200B;**配置**&#x200B;来完成的。

![应用配置](assets/cfm-conf-02.png)
