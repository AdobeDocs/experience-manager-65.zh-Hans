---
title: 与Adobe Campaign Standard集成
seo-title: Integrating with Adobe Campaign Standard
description: 与Adobe Campaign Standard集成。
seo-description: Integrating with Adobe Campaign Standard.
uuid: ef31339e-d925-499c-b8fb-c00ad01e38ad
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5c0fec99-7b1e-45d6-a115-e498d288e9e1
exl-id: caa43d80-1f38-46fc-a8b9-9485c235c0ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 0%

---

# 与Adobe Campaign Standard集成{#integrating-with-adobe-campaign-standard}

>[!NOTE]
>
>本文档介绍如何将AEM与基于订阅的解决方案Adobe Campaign Standard集成。 如果您使用的是Adobe Campaign 6.1，请参阅 [与Adobe Campaign 6.1集成](/help/sites-administering/campaignonpremise.md) 的说明。

Adobe Campaign允许您直接在Adobe Experience Manager中管理电子邮件投放内容和表单。

要同时使用两个解决方案，您必须首先将它们配置为彼此连接。 这涉及在Adobe Campaign和Adobe Experience Manager中执行配置步骤。 本文档详细介绍了这些步骤。

在AEM中使用Adobe Campaign包括通过Adobe Campaign发送电子邮件和表单的功能，相关介绍请参见 [使用Adobe Campaign](/help/sites-authoring/campaign.md).

此外，将AEM与集成时，可能会关注以下主题 [Adobe Campaign](https://docs.campaign.adobe.com/doc/standard/en/home.html):

* [电子邮件模板的最佳实践](/help/sites-administering/best-practices-for-email-templates.md)
* [Adobe Campaign集成故障诊断](/help/sites-administering/troubleshooting-campaignintegration.md)

如果您扩展了与Adobe Campaign的集成，则可能希望看到以下页面：

* [创建自定义扩展](/help/sites-developing/extending-campaign-extensions.md)
* [创建自定义表单映射](/help/sites-developing/extending-campaign-form-mapping.md)

## 配置Adobe Campaign {#configuring-adobe-campaign}

配置Adobe Campaign涉及以下事项：

1. 配置 **aemserver** 用户。
1. 创建专用外部帐户。
1. 验证AEMResourceTypeFilter选项。
1. 创建专用投放模板。

>[!NOTE]
>
>要执行这些操作，您必须具有 **管理** 在Adobe Campaign中的角色。

### 前提条件 {#prerequisites}

请事先确保您具有以下元素：

* [AEM创作实例](/help/sites-deploying/deploy.md#getting-started)
* [AEM发布实例](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Adobe Campaign实例](https://docs.adobe.com/content/docs/en/campaign/ACS.html)

>[!CAUTION]
>
>操作详见 [配置Adobe Campaign](#configuring-adobe-campaign) 和 [配置Adobe Experience Manager](#configuring-adobe-experience-manager) 要使AEM和Adobe Campaign之间的集成功能正常工作，需要部分内容。

### 配置aemserver用户 {#configuring-the-aemserver-user}

的 **aemserver** 必须在Adobe Campaign中配置用户。 的 **aemserver** 是技术用户，用于将AEM服务器连接到Adobe Campaign。

转到 **管理** >  **用户和安全** >  **用户**，然后选择 **aemserver** 用户。 单击该图标可打开用户设置。

* 您必须为此用户设置密码。 无法通过UI完成此操作。 此配置必须由技术管理员在REST中完成。
* 您可以为此用户分配特定角色，例如 **deliveryPrepare**，以便用户创建和编辑投放。

### 配置Adobe Experience Manager外部帐户 {#configuring-an-adobe-experience-manager-external-account}

您必须配置一个外部帐户，以便将Adobe Campaign连接到AEM实例。

>[!NOTE]
>
>在AEM中，确保为campaign-remote用户设置密码。 您需要设置此密码才能将Adobe Campaign与AEM连接。 以管理员身份登录，在用户管理控制台中，搜索campaign-remote用户并单击 **设置密码**.

要配置AEM外部帐户，请执行以下操作：

1. 转到 **管理** > **应用程序设置** > **外部帐户**.

   ![chlimage_1-124](assets/chlimage_1-124a.png)

1. 选择默认 **aemInstance** 外部帐户，或通过单击 **创建** 按钮。
1. 选择 **Adobe Experience Manager** in **类型** 字段，然后输入用于AEM创作实例的访问参数：服务器地址、帐户名和密码。

   >[!NOTE]
   >
   >确保不添加结尾 **/** URL末尾的斜杠或连接将不起作用。

1. 确保 **已启用** 复选框，然后单击 **保存** 以保存修改。

### 验证AEMResourceTypeFilter选项 {#verifying-the-aemresourcetypefilter-option}

的 **AEMResourceTypeFilter** 选项用于筛选可在Adobe Campaign中使用的AEM资源类型。 这允许Adobe Campaign检索专门设计为仅在Adobe Campaign中使用的AEM内容。

此选项已预配置；但是，如果更改此选项，可能会导致集成无法正常运行。

验证 **AEMResourceTypeFilter** 选项：

1. 转到 **管理** > **应用程序设置** > **选项**.
1. 在列表中，您可以确保 **AEMResourceTypeFilter** 选项，并且路径正确。

### 创建特定于AEM的电子邮件投放模板 {#creating-an-aem-specific-email-delivery-template}

默认情况下，Adobe Campaign的电子邮件模板中未启用AEM功能。 您可以配置新的电子邮件投放模板，以用于创建包含AEM内容的电子邮件。

要创建特定于AEM的电子邮件投放模板，请执行以下操作：

1. 转到 **资源** > **模板** > **投放模板**.
1. **启用选择** 单击操作栏中的复选标记，然后选择现有 **标准电子邮件（邮件）** 默认模板，然后通过单击 **复制** 图标，单击 **确认**.
1. 通过单击 **x** 并打开新创建的 **标准电子邮件（邮件）的副本** 模板，然后选择 **编辑属性** 从模板仪表板的操作栏。

   您可以修改模板的 **标签**.

1. 在属性中 **内容** ，请更改 **内容源** to **Adobe Experience Manager**. 然后，选择之前创建的外部帐户并单击 **确认**.

   通过单击 **确认** 单击 **保存。**

   通过此模板创建的电子邮件投放将启用AEM内容功能。

   ![chlimage_1-125](assets/chlimage_1-125a.png)

## 配置Adobe Experience Manager {#configuring-adobe-experience-manager}

要配置AEM，您必须执行以下操作：

* 配置实例之间的复制。
* 将AEM连接到Adobe Campaign。
* 配置外部器。

### 在AEM实例之间配置复制 {#configuring-replication-between-aem-instances}

首先，从AEM创作实例创建的内容会发送到发布实例。 然后，此发布实例会将内容传输到Adobe Campaign。 因此，必须将复制代理配置为从AEM创作实例复制到AEM发布实例。

>[!NOTE]
>
>如果您不想使用复制URL，而是使用面向公众的URL，则可以将 **公共URL** 在OSGi的以下配置设置中(**工具** > **Web控制台** > **OSGi配置> AEM Campaign集成 — 配置**):
**公共URL:** com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl

要将某些创作实例配置复制到发布实例中，还需要执行此步骤。

要在AEM实例之间配置复制，请执行以下操作：

1. 在创作实例中，选择 **AEM徽标**> **工具** > **部署** > **复制** > **作者代理**，然后单击 **默认代理**.

   ![chlimage_1-126](assets/chlimage_1-126a.png)

   >[!NOTE]
   配置与Adobe Campaign的集成时，请避免使用localhost(AEM的本地副本)，除非发布和创作实例都位于同一台计算机上。

1. 单击 **编辑** 然后选择 **运输** 选项卡。
1. 通过替换 **localhost** 的IP地址或AEM发布实例的地址。

   ![chlimage_1-127](assets/chlimage_1-127a.png)

### 将AEM连接到Adobe Campaign {#connecting-aem-to-adobe-campaign}

在将AEM和Adobe Campaign结合使用之前，您必须在两个解决方案之间建立链接，以便它们能够进行通信。

1. 连接到AEM创作实例。
1. 选择 **工具** > **操作** > **云** > **Cloud Services**，则 **立即配置** 在Adobe Campaign部分。

   ![chlimage_1-128](assets/chlimage_1-128a.png)

1. 通过输入 **标题** 单击 **创建**，或选择要与Adobe Campaign实例链接的现有配置。
1. 编辑配置，使其与Adobe Campaign实例的参数匹配。

   * **用户名**: **aemserver**，使用Adobe Campaign AEM集成包运算符在两个解决方案之间建立链接。
   * **密码**:Adobe Campaign aemserver操作员密码。 您可能需要直接在Adobe Campaign中为此运算符重新指定密码。
   * **API端点**:Adobe Campaign实例URL。

1. 选择 **连接到Adobe Campaign** 单击 **确定**.

   ![chlimage_1-129](assets/chlimage_1-129a.png)

   >[!NOTE]
   在 [创建电子邮件并发布](/help/sites-authoring/campaign.md)，则需要将配置重新发布到发布实例。

   ![chlimage_1-130](assets/chlimage_1-130a.png)

>[!NOTE]
如果连接失败，请确保检查以下内容：
* 使用到Adobe Campaign实例(https)的安全连接时，您可能会遇到证书问题。 您必须将Adobe Campaign实例证书添加到JDK的**cacerts**文件中。
* 此外，请参阅 [AEM/Adobe Campaign集成故障诊断](/help/sites-administering/troubleshooting-campaignintegration.md).
>


### 配置外部器 {#configuring-the-externalizer}

您需要 [配置外部器](/help/sites-developing/externalizer.md) 在AEM中。 外部器是一种OSGi服务，它允许您将资源路径转换为外部URL和绝对URL。 此服务提供了一个配置和构建这些外部URL的中心位置。

请参阅 [配置外部器](/help/sites-developing/externalizer.md) 常规说明。 对于Adobe Campaign集成，请确保在 `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl` 未指向 `localhost:4503` 但可以连接到可通过Adobe Campaign控制台访问的服务器。

如果它指向 `localhost:4503` 或Adobe Campaign无法访问的其他服务器上，您的图像将不会显示在Adobe Campaign控制台中。

![chlimage_1-131](assets/chlimage_1-131a.png)
