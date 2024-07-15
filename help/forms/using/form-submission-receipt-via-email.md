---
title: 通过电子邮件发送表单提交确认
description: AEM Forms允许您配置电子邮件提交操作，以在提交表单时向用户发送确认。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: bca4044a-18a9-4b97-92de-eff1e9a840f9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# 通过电子邮件发送表单提交确认 {#sending-a-form-submission-acknowledgement-via-email}

## 自适应表单数据提交 {#adaptive-form-data-submission}

自适应表单提供了多个现成的[提交操作](../../forms/using/configuring-submit-actions.md)工作流，用于将表单数据提交到不同的端点。

例如，**[!UICONTROL 发送电子邮件]**&#x200B;提交操作在成功提交自适应表单时发送电子邮件。 您还可以将其配置为通过电子邮件发送表单数据和PDF。

本文详细介绍在自适应表单及其提供的不同配置上启用电子邮件操作的步骤。

>[!NOTE]
>
>您还可以使用&#x200B;**[!UICONTROL 通过电子邮件发送PDF]**&#x200B;选项，通过电子邮件将填写好的表单作为PDF附件发送。 可用于此操作的配置选项与&#x200B;**[!UICONTROL 发送电子邮件]**&#x200B;操作的可用选项相同。 电子邮件PDF操作仅适用于基于XFA的自适应表单

## 发送电子邮件操作 {#email-action}

利用“发送电子邮件”操作，作者可在自适应表单成功提交后自动向一个或多个收件人发送电子邮件。

>[!NOTE]
>
>要使用“发送电子邮件”操作，您需要配置AEM邮件服务，如[配置邮件服务](/help/sites-administering/notification.md#configuring-the-mail-service)中所述。

### 在自适应表单上启用“发送电子邮件”操作 {#enabling-email-action-on-an-adaptive-form}

1. 以&#x200B;**[!UICONTROL 编辑]**&#x200B;模式打开自适应表单。

1. 在&#x200B;**[!UICONTROL 内容]**&#x200B;选项卡中，选择&#x200B;**[!UICONTROL 表单容器]**&#x200B;并选择![配置](assets/configure-icon.svg)以查看自适应表单属性。

1. 在&#x200B;**[!UICONTROL 提交]**&#x200B;部分中，从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 发送电子邮件]**。

   ![提交操作](assets/submission-actions.png)

1. 在&#x200B;**[!UICONTROL 收件人]**、**[!UICONTROL 抄送]**&#x200B;和&#x200B;**[!UICONTROL 密送]**&#x200B;字段中指定有效的电子邮件ID。

   在&#x200B;**[!UICONTROL 主题]**&#x200B;和&#x200B;**[!UICONTROL 电子邮件模板]**&#x200B;字段中分别指定电子邮件的主题和正文。

   您还可以在字段中指定变量占位符，在这种情况下，当最终用户成功提交表单时，将处理字段的值。 有关详细信息，请参阅[使用自适应表单字段名称动态创建电子邮件内容](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p)。

   如果表单包含文件附件，并且您希望在电子邮件中附加这些文件，请选择&#x200B;**[!UICONTROL 包含附件]**。

   >[!NOTE]
   >
   >如果选择&#x200B;**[!UICONTROL 通过电子邮件发送PDF]**&#x200B;选项，则必须选择“包含附件”选项。

1. 单击![保存](assets/save_icon.svg)以保存更改。

### 使用自适应表单字段名称动态创建电子邮件内容 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

自适应表单中的字段名称称为占位符，在用户提交表单后，这些占位符将替换为该字段的值。

在&#x200B;**[!UICONTROL 发送电子邮件]**&#x200B;操作中，您可以使用执行该操作时处理的占位符。 这意味着在用户提交表单时生成电子邮件的标头（如&#x200B;**[!UICONTROL To]**、**[!UICONTROL CC]**、**[!UICONTROL BCC]**、**[!UICONTROL Subject]**）。

要定义占位符，请选择&#x200B;**[!UICONTROL 发送电子邮件]**&#x200B;作为提交操作后，在字段中指定`${<field name>}`。

例如，如果表单包含名为`email_addr`的&#x200B;**[!UICONTROL 电子邮件地址]**&#x200B;字段，用于捕获用户的电子邮件ID，则可以在&#x200B;**[!UICONTROL 收件人]**、**[!UICONTROL 抄送]**&#x200B;或&#x200B;**[!UICONTROL 密送]**&#x200B;字段中指定以下内容。

`${email_addr}`

当用户提交表单时，会向在表单的`email_addr`字段中输入的电子邮件ID发送电子邮件。

>[!NOTE]
>
>您可以在字段的&#x200B;**[!UICONTROL 编辑]**&#x200B;对话框中找到字段的名称。

变量占位符也可以在&#x200B;**[!UICONTROL 主题]**&#x200B;和&#x200B;**[!UICONTROL 电子邮件模板]**&#x200B;字段中使用。

例如：

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>可重复面板中的字段不能用作变量占位符。
