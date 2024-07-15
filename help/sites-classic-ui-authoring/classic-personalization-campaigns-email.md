---
title: 电子邮件营销
description: 电子邮件营销（例如，新闻稿）是任何营销活动的重要组成部分，因为您会使用它们将内容推送到潜在客户。 在AEM中，您可以从现有AEM内容创建新闻稿并添加特定于新闻稿的新内容。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: a1d8b74e-67eb-4338-9e8e-fd693b1dbd48
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1767'
ht-degree: 0%

---


# 电子邮件营销{#e-mail-marketing}

>[!NOTE]
>
>Adobe不打算进一步增强对AEM SMTP服务发送的未结/退件（无法投放）的电子邮件跟踪。
>建议使用[Adobe Campaign以及与AEM](/help/sites-administering/campaign.md)的集成。

电子邮件营销（例如，新闻稿）是任何营销活动的重要组成部分，因为您会使用它们将内容推送到潜在客户。 在AEM中，您可以从现有AEM内容创建新闻稿并添加特定于新闻稿的新内容。

创建后，您可以立即或在另一个计划时间（通过使用工作流）向特定用户组发送新闻稿。 此外，用户可以按自己选择的格式订阅新闻稿。

此外，通过AEM可以管理新闻稿功能，包括维护主题、存档新闻稿和查看新闻稿统计数据。

>[!NOTE]
>
>在Geometrixx中，新闻稿模板会自动打开电子邮件编辑器。 您可以在要以邀请等形式发送电子邮件的其他模板中使用电子邮件编辑器。 无论何时从&#x200B;**mcm/components/newsletter/page**&#x200B;继承页面，都会显示电子邮件编辑器。

本文档介绍了在AEM中创建新闻稿的基础知识。 有关如何使用电子邮件营销的更多详细信息，请参阅以下文档：

* [创建有效的新闻稿登陆页面](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-landingpage.md)
* [管理订阅](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-subscriptions.md)
* [将电子邮件发布到电子邮件服务提供商](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-newsletters.md)
* [跟踪退回的电子邮件](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-tracking-bounces.md)

>[!NOTE]
>
>如果您更新电子邮件提供商、进行外部测试或发送新闻稿，并且未先将新闻稿发布到Publish实例或者Publish实例不可用，则这些操作将失败。 请务必发布您的新闻稿，并确保Publish实例已启动并正在运行。

## 创建新闻稿体验 {#creating-a-newsletter-experience}

>[!NOTE]
>
>需要通过osgi配置来配置电子邮件通知。 请参阅[配置电子邮件通知。](/help/sites-administering/notification.md)

1. 在左窗格中选择新营销策划，或在右窗格中双击该营销策划。

1. 使用图标选择列表视图：

   ![列表视图图标](do-not-localize/mcm_icon_listview-1.png)

1. 单击&#x200B;**新建……**

   您可以指定要创建的&#x200B;**标题**、**名称**&#x200B;和体验类型；在本例中，为Newsletter。

   ![创建体验对话框](assets/mcm_createnewsletter.png)

1. 单击&#x200B;**创建**。

1. 随即会打开一个新对话框。 您可以在此输入新闻稿的属性。

   **默认收件人列表**&#x200B;是必填字段，因为这会形成新闻稿的接触点（有关列表的详细信息，请参阅[使用列表](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists)）。

   ![页面属性对话框](assets/mcm_newnewsletterdialog.png)

   * **来自名称**
应作为新闻稿发件人显示的名称。

   * **发件人地址**
应作为新闻稿发件人显示的邮件地址。

   * **主题**
新闻稿的主题。

   * **回复**
邮件地址，负责处理已发送新闻稿的回复。

   * **描述**
新闻稿的说明。

   * **开启时间**
发送新闻稿的准时。

   * **默认收件人列表**
应接收新闻稿的默认列表。

   稍后可以从&#x200B;**属性……**&#x200B;对话框更新这些内容。

1. 单击&#x200B;**确定**&#x200B;进行保存。

## 向新闻稿添加内容 {#adding-content-to-newsletters}

您可以在新闻稿中添加内容（包括动态内容），就像在任何AEM组件中一样。 在Geometrixx中，新闻稿模板具有某些可用于在新闻稿中添加和修改内容的组件。

1. 在MCM中，单击&#x200B;**促销活动**&#x200B;选项卡，然后双击要向其添加内容或编辑的新闻稿。 新闻稿随即打开。

1. 如果组件不可见，请转到“设计”视图并启用必要的组件（例如，新闻稿组件），然后再开始编辑。
1. 根据需要输入任何新文本、图像或其他组件。 在Geometrixx示例中，提供了4个组件：“文本”、“图像”、“标题”和“2列”。 新闻稿中的组件数量可能更多，也可能更少，具体取决于您的设置方式。

   >[!NOTE]
   >
   >您可以使用变量个性化新闻稿。 在Geometrixx新闻稿中，变量位于文本组件中。 变量的值继承自用户配置文件中的信息。

   ![编辑新闻稿内容](assets/mcm_newsletter_content.png)

1. 若要插入变量，请从列表中选择变量，然后单击&#x200B;**插入**。 变量从配置文件中填充。

## 个性化新闻稿 {#personalizing-newsletters}

您可以通过在Geometrixx的新闻稿的文本组件中插入预定义变量来对新闻稿进行个性化设置。 变量的值继承自用户配置文件中的信息。

您还可以通过使用客户端上下文和加载用户档案，模拟新闻稿的个性化方式。

个性化新闻稿并模拟其外观：

1. 从MCM中，打开要为其自定义设置的新闻稿。

1. 打开要个性化的文本组件。

1. 将光标放在您希望变量出现的位置，然后从下拉列表中选择一个变量，然后单击&#x200B;**插入**。 根据需要对任意数量的变量执行此操作，然后单击&#x200B;**确定**。

   ![正在添加变量](assets/mcm_newsletter_variables.png)

1. 要模拟变量在发送时的外观，请按CTRL+ALT+c打开客户端上下文并选择&#x200B;**加载**。 从列表中选择要加载其配置文件的用户，然后单击&#x200B;**确定**。

   您加载的配置文件中的信息已填充变量。

   ![正在测试变量](assets/mc_newsletter_testvariables.png)

## 在不同电子邮件客户端中测试新闻稿 {#testing-newsletters-in-different-e-mail-clients}

>[!NOTE]
>
>在发送新闻稿之前，请检查`https://localhost:4502/system/console/configMgr`处Day CQ Link Externalizer的OSGi配置。
>
>默认情况下，参数的值为`localhost:4502`，如果正在运行的实例的端口发生更改，则无法完成操作。

在常用的电子邮件客户端之间切换，查看您的新闻稿在潜在客户端的外观如何。 默认情况下，会打开您的新闻稿，但不会选择任何电子邮件客户端。

目前，您可以在以下电子邮件客户端中查看新闻稿：

* Yahoo邮件
* Gmail
* Hotmail
* Thunderbird
* Microsoft Outlook 2007
* Apple邮件

要在客户端之间切换，请单击相应的图标以查看该电子邮件客户端中的新闻稿：

1. 从MCM中，打开要为其自定义设置的新闻稿。

1. 单击顶栏中的电子邮件客户端，可查看新闻稿在该客户端中大致是什么样子。

   ![正在切换电子邮件客户端](assets/chlimage_1-119.png)

1. 对要查看的其他电子邮件客户端重复此步骤。

   ![更改电子邮件客户端](assets/chlimage_1-120.png)

## 自定义新闻稿设置 {#customizing-newsletter-settings}

虽然只有授权用户可以发送新闻稿，但您应该自定义以下内容：

* 主题行，以便用户希望打开您的电子邮件，并确保您的新闻稿最终不会被标记为垃圾邮件。
* 发件人地址，例如`noreply@geometrixx.com`，以便用户从指定地址接收电子邮件。

要自定义新闻稿设置，请执行以下操作：

1. 从MCM中，打开要为其自定义设置的新闻稿。

   ![打开新闻稿](assets/mcm_newsletter_open.png)

1. 在新闻稿的顶部，单击&#x200B;**设置**。

   ![正在编辑新闻稿设置](assets/mcm_newsletter_settings.png)
1. 输入&#x200B;**发件人**&#x200B;电子邮件地址

1. 修改电子邮件的&#x200B;**主题**（如有必要）。

1. 从下拉列表中选择&#x200B;**默认收件人列表**。

1. 单击&#x200B;**确定**。

   测试或发送新闻稿时，收件人将收到包含指定电子邮件地址和主题的电子邮件。

## 飞行测试通讯 {#flight-testing-newsletters}

虽然飞行测试不是强制性的，但在您发送新闻稿之前，您可能需要对其进行测试，以确保它按您所需的方式显示。

飞行测试可让您执行以下操作：

* 查看[所有目标客户端](#testing-newsletters-in-different-e-mail-clients)的新闻稿。
* 验证邮件服务器是否已正确设置。
* 确定您的电子邮件是否被标记为垃圾邮件。 （确保将您自己包含在收件人列表中。）

>[!NOTE]
>
>如果您更新电子邮件提供商、进行外部测试或发送新闻稿，并且未先将新闻稿发布到Publish实例或者Publish实例不可用，则这些操作将失败。 请务必发布您的新闻稿，并确保Publish实例已启动并正在运行。

试飞新闻稿：

1. 从MCM中，打开要测试的新闻稿并发送。

1. 在新闻稿的顶部，单击&#x200B;**测试**&#x200B;以在发送前进行测试。

   ![测试新闻稿的设置](assets/mcm_newsletter_testsettings.png)

1. 输入要发送新闻稿的测试邮件地址，然后单击&#x200B;**发送**。 如果要更改配置文件，请在客户端上下文中加载另一个配置文件。 要执行此操作，请按CTRL+ALT+c并选择“加载”并加载配置文件。

## 发送新闻稿 {#sending-newsletters}

>[!NOTE]
>
>Adobe不打算进一步增强对AEM SMTP服务发送的未结/退件（无法投放）的电子邮件跟踪。
>建议使用[Adobe Campaign以及与AEM](/help/sites-administering/campaign.md)的集成。

您可以从新闻稿或列表发送新闻稿。 这两个过程都进行了描述。

>[!NOTE]
>
>在发送新闻稿之前，请检查`https://localhost:4502/system/console/configMgr`处Day CQ Link Externalizer的OSGi配置。
>
>默认情况下，参数的值为`localhost:4502`，如果正在运行的实例的端口发生更改，则无法完成操作。

>[!NOTE]
>
>如果您更新电子邮件提供商、进行外部测试或发送新闻稿，并且未先将新闻稿发布到Publish实例或者Publish实例不可用，则这些操作将失败。 请务必发布您的新闻稿，并确保Publish实例已启动并正在运行。

### 从营销活动发送新闻稿 {#sending-newsletters-from-a-campaign}

要从营销活动内发送新闻稿，请执行以下操作：

1. 从MCM中，打开要发送的新闻稿。

   >[!NOTE]
   >
   >在发送之前，请确保已通过[自定义新闻稿的设置](#customizing-newsletter-settings)自定义了新闻稿的主题和原始电子邮件地址。
   >
   >
   >[小众测试版](#flight-testing-newsletters)建议发送前的新闻稿。

1. 在新闻稿的顶部，单击&#x200B;**发送**。 新闻稿向导将打开。

1. 在收件人的列表中，选择要接收新闻稿的列表，然后单击&#x200B;**下一步**。

   ![发送新闻稿](assets/mcm_newslettersend.png)

1. 已确认安装完成。 单击&#x200B;**发送**&#x200B;以实际发送新闻稿。

   ![新闻稿已发送确认](assets/mcm_newslettersendconfirm.png)

   >[!NOTE]
   >
   >确保您是收件者之一，这样您就可以确保新闻稿已收到。

### 从列表发送新闻稿 {#sending-newsletters-from-a-list}

要从列表发送新闻稿，请执行以下操作：

1. 在MCM中，单击左侧窗格中的&#x200B;**列表**。

   >[!NOTE]
   >
   >在发送之前，请确保已通过[自定义新闻稿的设置](#customizing-newsletter-settings)自定义了新闻稿的主题和原始电子邮件地址。 如果从列表中发送新闻稿，则无法对其进行测试；如果从新闻稿发送，则可以[飞行测试](#flight-testing-newsletters)。

1. 选中要向其发送新闻稿的潜在客户列表旁边的复选框。

1. 在&#x200B;**工具**&#x200B;菜单中，选择&#x200B;**发送新闻稿**。 将打开&#x200B;**发送新闻稿**&#x200B;窗口。

   ![Newletter控制台](assets/mcm_newslettersendfromlist.png)

1. 在&#x200B;**新闻稿**&#x200B;字段中，选择要发送的新闻稿，然后单击&#x200B;**下一步**。

   ![发送新闻稿对话框](assets/mcm_newslettersenddialog.png)

1. 已确认安装完成。 单击&#x200B;**发送**&#x200B;将所选的新闻稿发送到指定的潜在客户列表。

   ![发送确认](assets/mcm_newslettersenddialog_confirmation.png)

   您的新闻稿将发送给选定的收件人。

## 订阅新闻稿 {#subscribing-to-a-newsletter}

本节介绍如何订阅新闻稿。

### 订阅新闻稿 {#subscribing-to-a-newsletter-1}

订阅新闻稿(以Geometrixx网站为例)：

1. 单击&#x200B;**网站**&#x200B;并导航到Geometrixx **工具栏**&#x200B;并将其打开。

   ![订阅示例](assets/chlimage_1-121.png)

1. 在Geometrixx新闻稿&#x200B;**注册**&#x200B;字段中，输入您的电子邮件地址并单击&#x200B;**注册**。 您现在已订阅新闻稿。
