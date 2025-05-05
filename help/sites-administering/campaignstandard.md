---
title: 将AEM 6.5与Adobe Campaign Standard集成
description: 了解如何将AEM 6.5与Adobe Campaign Standard集成。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: caa43d80-1f38-46fc-a8b9-9485c235c0ca
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 12%

---


# 将AEM 6.5与Adobe Campaign Standard集成 {#integrating-with-adobe-campaign-standard}

通过将AEM 6.5与Adobe Campaign Standard (ACS)集成，您可以直接在AEM中管理电子邮件投放、内容和表单。 需要同时执行Adobe Campaign Standard和AEM的配置步骤才能在解决方案之间实现双向通信。

此集成允许单独使用AEM和Adobe Campaign Standard。 营销人员可以在Adobe Campaign中创建活动并使用定位，而内容创建者则可以同时在AEM中进行内容设计。 借助该集成，Adobe Campaign可以定位和交付在AEM中创建的营销活动的内容和设计。

>[!INFO]
>
>本文档详细介绍如何将Adobe Campaign Standard与AEM 6.5集成。有关其他Campaign集成，请参阅文档[将AEM 6.5与Adobe Campaign集成。](campaign.md)

## 集成步骤 {#integration-steps}

配置AEM与Adobe Campaign Standard之间的集成需要在这两个解决方案中执行多个步骤。

1. [配置 ](#aemserver-user)
1. [验证 ](#resource-type-filter)
1. [在Campaign中创建特定于AEM的电子邮件投放模板](#aem-email-delivery-template)
1. [在AEM中配置Campaign集成](#campaign-integration)
1. [配置到AEM Publish实例的复制](#replication)
1. [配置 AEM 外部化器](#externalizer)
1. [配置 ](#campaign-remote-user)
1. [在Campaign中配置AEM外部帐户](#acc-external-user)

本文档将详细介绍其中的每个步骤。

## 先决条件 {#prerequisites}

* Adobe Campaign Standard的管理员访问权限
   * 如果您需要有关如何设置和配置Adobe Campaign Standard的其他详细信息，请参阅[Adobe Campaign Standard文档。](https://experienceleague.adobe.com/docs/campaign-standard/using/campaign-standard-home.html)
* 管理员访问AEM

## 在Campaign中配置aemserver用户 {#aemserver-user}

默认情况下，Adobe Campaign Standard附带一个`aemserver`用户，AEM使用该用户连接到Adobe Campaign。 为此用户分配适当的安全组并设置其密码。

1. 以管理员身份登录Adobe Campaign。

1. 单击菜单栏左上角的Adobe Campaign徽标可打开全局导航，然后从导航菜单中选择&#x200B;**管理** > **用户和安全** > **用户**。

1. 在用户控制台中单击`aemserver`用户。

1. 确保至少将`aemserver`用户分配给角色为`deliveryPrepare`的安全组。 默认情况下，组`Standard Users`具有此角色。

   Adobe Campaign中的![aemserver用户](assets/acs-aemserver-user.png)

1. 单击&#x200B;**保存**&#x200B;以保存更改。

您的`aemserver`用户现在拥有必要的权限，以便AEM可以使用该用户与Adobe Campaign通信。

但是，在AEM可以使用`aemserver`用户之前，必须设置其密码。 这不能通过Adobe Campaign完成。 必须由Adobe支持工程师执行。 [通过Adobe客户关怀](https://experienceleague.adobe.com/?support-tab=home#support)提交票证，以请求重置`aemserver`密码。 获得Adobe客户关怀团队提供的密码后，请将其保存在安全位置。

## 验证Campaign中的AEMResourceTypeFilter {#resource-type-filter}

`AEMResourceTypeFilter`是Adobe Campaign中的一个选项，用于筛选可以在Adobe Campaign中使用的AEM资源。 由于AEM包含许多内容，因此此选项将用作过滤器，允许Adobe Campaign仅检索专门设计用于Adobe Campaign的类型的AEM内容。

此选项是预配置的。 但是，如果您自定义了AEM的Campaign组件，则可能需要更新它。 要验证是否已配置`AEMResourceTypeFilter`选项，请执行以下步骤。

1. 以管理员身份登录Adobe Campaign。

1. 单击菜单栏左上角的Adobe Campaign徽标可打开全局导航，然后从导航菜单中选择&#x200B;**管理** > **应用程序设置** > **选项**。

1. 单击选项控制台中的`AEMResourceTypeFilter`。

1. 确认`AEMResourceTypeFilter`的配置。 路径以逗号分隔，默认包含：

   * `mcm/campaign/components/newsletter`
   * `mcm/campaign/components/campaign_newsletterpage`
   * `mcm/neolane/components/newsletter`

   ![AEMResourceTypeFilter](assets/acs-aem-resource-type-filter.png)

1. 单击&#x200B;**保存**&#x200B;以保存更改。

您的`AEMResourceTypeFilter`现在配置为从AEM检索正确的内容。

## 在Campaign中创建特定于AEM的电子邮件投放模板 {#aem-email-delivery-template}

默认情况下，Adobe Campaign的电子邮件模板中未启用AEM。 配置新的电子邮件投放模板，该模板可用于使用AEM内容创建电子邮件。 要创建特定于AEM的电子邮件投放模板，请执行以下步骤。

1. 以管理员身份登录Adobe Campaign。

1. 单击菜单栏左上角的Adobe Campaign徽标可打开全局导航，然后从导航菜单中选择&#x200B;**资源** > **模板** > **投放模板**。

1. 在投放模板控制台中，找到默认电子邮件模板&#x200B;**通过电子邮件发送（邮件）**，并将鼠标悬停在代表该模板的卡片（或行）上以显示选项。 单击&#x200B;**重复元素**。

   ![重复元素](assets/acs-copy-template.png)

1. 在&#x200B;**确认**&#x200B;对话框中，单击&#x200B;**确认**&#x200B;以复制模板。

   ![确认对话框](assets/acs-confirmation.png)

1. 此时将打开模板编辑器，其中包含&#x200B;**通过电子邮件发送（邮件）**&#x200B;模板的副本。 单击窗口右上角的&#x200B;**编辑属性**&#x200B;图标。

   ![模板编辑器](assets/acs-template-editor.png)

1. 在“属性”窗口中，将&#x200B;**标签**&#x200B;字段更改为新AEM模板的描述性字段。

1. 单击&#x200B;**Content**&#x200B;标题将其展开，然后在&#x200B;**Content source**&#x200B;下拉列表中选择&#x200B;**Adobe Experience Manager**。

1. 这会显示&#x200B;**Adobe Experience Manager帐户**&#x200B;字段。 使用下拉菜单选择&#x200B;**Adobe Experience Manager实例(aemInstance)**&#x200B;用户。 这是AEM集成的默认外部用户。

![配置模板属性](assets/acs-template-properties.png)

1. 单击&#x200B;**确认**&#x200B;保存对属性所做的更改。

1. 在模板编辑器中，单击&#x200B;**保存**&#x200B;以保存电子邮件模板的修改副本，以便与AEM一起使用。

现在，您有一个可以使用AEM内容的电子邮件模板。

## 在AEM中配置Campaign集成 {#campaign-integration}

AEM使用内置集成以及您在Adobe Campaign中配置的`aemserver`用户与Adobe Campaign通信。 按照以下步骤配置此集成。

1. 以管理员身份登录到您的 AEM 创作实例。

1. 从全局导航侧栏中，选择&#x200B;**“工具”**>**“Cloud Service”**＞**“传统 Cloud Service”**>**“Adobe Campaign”**，然后单击&#x200B;**“立即配置”**。

   ![配置 Adobe Campaign](assets/configure-campaign-service.png)

1. 在对话框中，通过输入&#x200B;**“标题”**&#x200B;并单击&#x200B;**“创建”**&#x200B;来创建 Campaign 服务配置。

   ![配置 Campaign 对话框](assets/configure-campaign-dialog.png)

1. 会打开新窗口和对话框会，用以编辑配置。 提供必要的信息。

   * **用户名** — 这是您在上一步中配置的Adobe Campaign中的[用户`aemserver`。](#aemserver-user)默认情况下，这是 `aemserver`。
   * **密码** — 这是您在上一步中向Adobe客户关怀部门请求的Adobe Campaign中[用户`aemserver`的密码。](#aemserver-user)
   * **API 端点** – 这是 Adobe Campaign 实例 URL。

   ![在 AEM 中配置 Adobe Campaign](assets/configure-campaign.png)

1. 选择&#x200B;**“连接到 Adobe Campaign”**&#x200B;以验证连接，然后单击&#x200B;**确定**。

AEM 现在可以与 Adobe Campaign 通信。

>[!NOTE]
>
>确保您的 Adobe Campaign 服务器可以通过 Internet 访问。AEM无法访问专用网络。

## 配置到AEM Publish实例的复制 {#replication}

Campaign内容由内容作者在AEM创作实例上创建。 此实例通常仅在贵组织内部可用。 要使营销活动的收件人能够访问图像和资产等内容，您需要发布该内容。

复制代理负责将内容从AEM创作实例发布到发布实例，必须设置该代理才能使集成正常工作。 此外，还需要执行此步骤以将某些创作实例配置复制到发布实例。

要配置从AEM创作实例到发布实例的复制，请执行以下操作：

1. 以管理员身份登录到您的 AEM 创作实例。

1. 从全局导航侧栏中，选择&#x200B;**工具** > **部署** > **复制** > **作者代理**，然后单击&#x200B;**默认代理（发布）**。

   ![配置复制代理](assets/acc-replication-config.png)

1. 单击&#x200B;**编辑**，然后选择&#x200B;**传输**&#x200B;选项卡。

1. 将默认`localhost`值替换为AEM发布实例的IP地址，以配置&#x200B;**URI**&#x200B;字段。

   ![传输选项卡](assets/acc-transport-tab.png)

1. 单击&#x200B;**确定**&#x200B;保存对代理设置的更改。

您已配置复制到AEM发布实例，以便活动收件人可以访问您的内容。

>[!NOTE]
>
>如果您不想使用复制URL，而是使用面向公众的URL，则可以通过OSGi在下面的配置设置中设置公共URL
>
>从全局导航侧栏中，选择&#x200B;**工具** > **操作** > **Web控制台** > **OSGi配置**，然后搜索&#x200B;**AEM Campaign集成 — 配置**。 编辑配置并更改字段&#x200B;**公共URL** (`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`)。

## 配置 AEM 外部化器 {#externalizer}

[外部化器](/help/sites-developing/externalizer.md)是AEM中的OSGi服务，它可将资源路径转换为外部和绝对URL，这是AEM提供Campaign可以使用的内容所必需的。 对其进行配置，以便Campaign集成正常工作。

1. 以管理员身份登录到 AEM 创作实例。
1. 从全局导航侧边栏中，选择&#x200B;**工具** > **操作** > **Web控制台** > **OSGi配置**，然后搜索&#x200B;**Day CQ链接外部化器**。
1. 默认情况下，**域**&#x200B;字段中的最后一个条目适用于发布实例。 将URL从默认`http://localhost:4503`更改为公开可用的发布实例。

   ![配置外部化器](assets/acc-externalizer-config.png)

1. 单击&#x200B;**保存**。

您已配置外部化器，Adobe Campaign现在可以访问您的内容。

>[!NOTE]
>
>发布实例必须可以从Adobe Campaign服务器访问。 如果它指向`localhost:4503`或Adobe Campaign无法访问的其他服务器，则来自AEM的图像将不会显示在Adobe Campaign控制台中。

## 在AEM中配置活动远程用户 {#campaign-remote-user}

正如AEM在Adobe Campaign中需要用户可以与Adobe Campaign通信一样，Adobe Campaign也需要AEM中的用户才能与AEM通信。 默认情况下，Campaign集成会在AEM中创建`campaign-remote`用户。 按照以下步骤配置此用户。

1. 以管理员身份登录 AEM。
1. 在主导航控制台上，单击左边栏中的&#x200B;**工具**。
1. 然后单击&#x200B;**安全** > **用户**&#x200B;以打开用户管理控制台。
1. 找到`campaign-remote`用户。
1. 选择`campaign-remote`用户，然后单击&#x200B;**“属性”**&#x200B;来编辑用户。
1. 在&#x200B;**“编辑用户设置”**&#x200B;窗口中，单击&#x200B;**“更改密码”**。
1. 为用户提供新密码，并将密码记在安全位置以备将来使用。
1. 单击&#x200B;**“保存”**&#x200B;以保存密码更改。
1. 单击&#x200B;**“保存并关闭”**&#x200B;以将更改保存到`campaign-remote`用户。

## 在Campaign中配置AEM外部帐户 {#acc-external-user}

当您[创建特定于AEM的电子邮件投放模板时，](#aem-email-delivery-template)您指定该模板应使用`aemInstance`外部帐户与AEM通信。 要启用这两种解决方案之间的双向通信，您需要在Adobe Campaign中配置此帐户。

1. 以管理员身份登录Adobe Campaign。

1. 单击菜单栏左上角的Adobe Campaign徽标可打开全局导航，然后从导航菜单中选择&#x200B;**管理** > **应用程序设置** > **外部帐户**。

1. 在用户控制台中单击&#x200B;**Adobe Experience Manager实例(aemInstance)**&#x200B;用户。

1. 确保用户具有&#x200B;**Adobe Experience Manager**&#x200B;作为&#x200B;**类型**。

1. 在&#x200B;**连接**&#x200B;部分中，定义以下字段：

   1. 服务器：这是AEM创作服务器的URL。 不应以斜杠结尾。
   1. 帐户：这是您[之前在AEM中配置的`campaign-remote`用户。](#campaign-remote-user)
   1. 密码：这是您[之前在AEM中配置的`campaign-remote`用户的密码。](#campaign-remote-user)

   ![编辑aemInstance用户](assets/acs-external-acount-editor.png)

1. 确保选中&#x200B;**已启用**&#x200B;复选框，然后单击&#x200B;**保存**&#x200B;以保存更改。

恭喜！您已完成AEM与Adobe Campaign Standard之间的集成！

## 后续步骤 {#next-steps}

在配置Adobe Campaign Classic和AEM后，集成现已完成。

您现在可以通过继续阅读[本文档](/help/sites-authoring/campaign.md)学习如何在 Adobe Experience Manager 中创建新闻稿。
