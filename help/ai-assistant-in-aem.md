---
title: AEM 6.5人工智能助理
description: 使用 AI 助手帮助您找到答案，并为 Adobe Experience Manager 中提供的解决方案修复错误。
solution: Experience Manager, Experience Manager 6.5
feature: Authoring, AI Assistant, AI Tools
role: Admin, Architect, Developer, User
exl-id: 3b4a484e-55b5-4924-82dd-56735f6ed46d
source-git-commit: 773a3e1ce6365589c968dd56a44d7adc9a4ec447
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 4%

---

# AEM 6.5人工智能助理 {#about-ai-assistant-in-aem}

>[!IMPORTANT]
>
>未使用AEM/Experience Hub的AEM 6.5和Cloud Manager 6.5 LTS客户必须联系其Adobe客户成功工程师以请求访问AI助手。

AEM 6.5/AEM 6.5 LTS中的AI Assistant提供了一个对话界面，旨在简化为Adobe Experience Manager相关查询查找答案的过程。 它可以帮助您即时获得AEM产品相关问题的答案（*可供所有用户使用*），并自动创建支持工单（*可供支持管理员使用*）。

AI Assistant支持AEM as a Cloud Service，包括以下解决方案：

* Experience Hub概述页面
* Edge Delivery Services
* Sites
* Assets
* 表单
* Dynamic Media
* Cloud Manager


它直接嵌入在 AEM 中，可从 AEM Experience Hub、Cloud Manager 和 Author UI 访问。

以下时长3分钟、时长25秒的视频分步介绍了AEM中的AI助手。

>[!VIDEO](https://video.tv.adobe.com/v/3475357/?learn=on&enablevpops)

## 访问AEM中的AI助手{#get-access}

要访问AEM中的AI助手，客户必须具备以下功能：

* 在AEM中使用AI助手获取产品知识的权限。 此权限允许您在AI Assistant聊天中询问产品相关问题。 必须启用此权限。
* 打开支持票证的权限，该权限需要&#x200B;**支持管理员**&#x200B;角色。

>[!NOTE]
>
>AEM中的AI助手请求通过Adobe Identity Management服务(IMS)进行身份验证。 有关详细信息，请参阅[Adobe Identity Management服务概述](https://www.adobe.com/content/dam/cc/en/trust-center/ungated/whitepapers/corporate/adobe-identity-management-services-security-overview.pdf)。

**要访问AEM中的AI助手：**

1. 客户必须签订附加协议才能访问Adobe Experience Manager中的大多数AI支持的和代理功能。 有关详细信息，请与Adobe代表联系。

1. 要在AEM中使用AI助手，必须获得通过AI助手访问产品知识的权限。 默认情况下，此权限处于打开状态。

   如果您希望控制谁可以访问产品知识，请从与Adobe ID关联的电子邮件地址向[aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com)发送电子邮件。 Adobe可以启用用户级别的访问控制。 启用后，您的管理员可以按照[在AEM中配置AI助手](/help/ai-assistant-in-aem-admin.md)中的步骤授予用户级访问权限。


## 范围 {#scope}

AEM中AI助理的当前范围侧重于解决AEMr as a Cloud Service的产品知识问题。 该范围包括对关键领域的全面支持。<!--, such as Sites, Assets, Forms, Edge Delivery Services, Dynamic Media, and Cloud Manager. -->

* **表面**：在AEM Experience Hub、创作UI、Cloud Manager中可用。
* **功能**：产品知识以及故障排除和指导的第一站，支持票证的自动创建和查找。
* **值**：节省时间，加快学习并加快价值实现，减少手动创建支持票证的需求，并提高创建支持票证的效率。

## 隐私、安全和治理{#privacy-security-governance}

AEM中的AI助手在设计中特别强调隐私、安全和治理。

本文概述了AEM中的AI助手可期待的以信任为中心的功能：

* AEM中的AI助手不使用任何个人数据，包括培训目的。
* AEM中的AI助手无法访问消费者数据。
* 需要明确权限才能与AEM中的AI助手交互。
* 不与其他客户共享用户提供的提示（问题、查询等）。

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## 了解AEM中的AI助手，了解产品知识和自动创建支持工单 {#ai-prod-insights}

产品知识包含从Adobe Experience League文档衍生的概念和主题。 这些问题可划分为以下子组：


| 产品知识 | 可供所有用户使用<br>示例 |
| :--- | :--- |
| 点式学习 | <ul><li>什么是通用编辑器？</li><li>如何在Cloud Manager中创建程序？</li></ul> |
| 打开发现 | <ul><li>如何使用通用编辑器？</li><li>是否有办法将内容从一个环境复制到另一个环境？</li></ul> |
| 疑难解答 | <ul><li>为何无法访问通用编辑器？</li><li>我的管道为什么会失败？</li></ul> |
| **支持票证创建** | **仅支持管理员&#x200B;**<br>**示例** |
| 自动创建支持工单，以捕获AI Assistant聊天历史记录和上下文 | <ul><li>为我创建支持工单。</li></ul> |
| 检索支持票证的状态 | <ul><li>显示我已打开的所有支持票证。</li><li>显示票证“E-----------”的状态</li></ul> |

{style="table-layout:auto"}


## 如何提出有效的问题 {#ai-craft-questions}

要从AEM中的AI助手获得最准确的响应，请务必用清楚明了的上下文表述您的问题。 使用以下提示来确保您的查询清晰且结构合理：

* 以简洁明了的方式清楚地陈述您的任务或问题。
* 避免使用含糊不清的措辞或过于复杂的语法，以增进理解。
* 包含有关您的任务或问题的相关上下文，因为此方法有助于AEM中的AI助手提供更精确且相关的答案。
例如，在提示符下，为您正在使用的AEM解决方案命名(Sites、Assets、Dynamic Media、Edge Delivery Services、Cloud Manager或Forms)会很有帮助。

### 不支持的问题的示例 {#ai-unsupported-questions}

| 区域 | 示例 |
| --- | --- |
| 运营见解 | <ul><li>我的租户中有多少个开发环境？</li><li>谁启动了最后一个生产管道？</li></ul> |
| 疑难解答 | <ul><li>为什么我的生产管道失败？</li></ul> |
| 任务和自动化 | <ul><li>从开发分支为我配置代码质量管道。</li></ul> |


## 在AEM中使用AI助手 {#ai-use}

<!-- UNHIDE AFTER BETA or at GA
### Enable AI Assistant in AEM access through Admin Console 

To use AI Assistant in AEM, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AI Assistant in AEM in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in AI Assistant in AEM of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md). -->


### 在AEM对话中启动AI助手

您可以在AEM中重置AI助手，并在要更改主题时开始新对话。 在排除查询失败或提供错误信息时，此功能特别有用。

**在AEM对话中启动AI助手：**

1. 在AEM用户界面的右上角(从Cloud Manager页面或AEM环境的创作实例)附近，单击&#x200B;**AI助手**&#x200B;图标。

   工具栏上的![AI助手图标](/help/assets/assets-ai/ai-assistant-icon.png)

1. 在底部附近的&#x200B;**AI助手**&#x200B;面板文本框中，键入您的问题或提示，然后按`Enter`或单击![发送图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg)。

   >[!NOTE]
   >
   >个人数据不应包含在您的输入中，因为使用此工具没有必要。

   ![AI助手面板底部的文本框](/help/assets/assets-ai/ai-assistant-prompt-text-box.png)

1. 要开始新对话（新主题或主题中的更改），请单击![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) > **开始新对话**。

   ![从省略号图标在AI助手中开始新对话](/help/assets/assets-ai/ai-assistant-start-new-conversation.png)

### 按类别发现提示

AEM中的AI助手包括可发现功能，可帮助您探索支持的主题和类别。

**要按类别发现提示：**

1. 在AI助手面板中，单击![学习图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)以打开提示发现面板。

   ![允许您在AI助手中按类别浏览提示的面板](/help/assets/assets-ai/ai-assistant-discover-prompts.png)
   显示AI助手中的提示类别的&#x200B;*面板。*

1. 选择一个类别以查看相关提示的列表。
1. 选择提示以查看AI助手可以回答的问题类型的示例。

1. 若要隐藏提示发现面板，请再次单击![学习图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)。

### 在AEM中分享您对AI助手的反馈

您的输入可帮助Adobe改进AI Assistant以提高性能和准确性。

通过以下选项，分享您对AEM中AI助手体验的反馈：

![竖起拇指、竖下拇指和标记图标](/help/assets/assets-ai/ai-assistant-feedback-icons.png)

| 单击 | 描述 |
| --- | --- |
| ![竖起大拇指图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | 指出哪些方面进展顺利，并分享积极反馈。 |
| ![拇指朝下缩进图示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | 提供改进建议。 添加有关您的体验的特定评论，这些评论每天都会审核。 |
| ![标记图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | 报告有关您在AEM中与AI助理交互的问题或提供详细反馈。 |

## 关于AEM中AI助理的常见问题解答 {#ai-faq}

以下是有关AI Assistant的一些常见问题的答案：

* **AEM中的AI助手实时提供信息吗？**\
  不行。AI Assistant从Adobe Experience League文档获取其内容。 对内容的更新可能需要一些时间才能反映在其响应中。
* **AEM中的AI助手支持哪些Adobe应用程序？**\
  目前，AI Assistant支持AEM as a Cloud Service中的产品知识查询，包括Sites、Assets、Dynamic Media、Cloud Manager和Forms。
* **AEM中的AI助手有哪些功能？**\
  AEM中的AI助手可回答与Adobe产品知识相关的查询。
* **AEM中的AI助手是否将个人信息用于训练数据？**\
  不行。AEM中的AI助手不使用个人信息进行培训。 避免与AEM中的AI助手共享您或其他人的个人信息，包括姓名或联系详情。

<!-- IS THE DOCUMENTATION BELOW STILL NEEDED? IF SO, GO AHEAD AND DELETE THE COMMENT TAGS!!

## AEM Forms AI Assistant (Forms Experience Builder) {#ai-forms-builder}

In addition to the general AI Assistant in AEM for product knowledge, AEM offers a specialized **[AEM Forms AI Assistant (Forms Experience Builder)](/help/edge/docs/forms/forms-ai-assistant.md)**. This enhanced assistant can actively help you create and configure forms through natural language prompts and answer questions specific to forms.

### Key capabilities

The AEM Forms AI Assistant provides:

* **Form Creation**: Create new forms from scratch using natural language descriptions.
* **Design Import**: Convert existing designs (PDF, Figma, images) into functional AEM Forms. 
* **Form Configuration**: Add fields, panels, validation rules, and conditional logic.
* **Layout Management**: Organize form structure and optimize for different devices.
* **Integration Setup**: Configure form submissions and data handling.
* **Product Knowledge**: Answer questions about AEM Forms features and best practices.

### Where to access

The AEM Forms AI Assistant is available in the following:

* **Universal Editor**: For Edge Delivery Services forms with visual editing capabilities.
* **Adaptive Forms Editor**: For detailed form configuration and advanced features.
* **Forms Management UI**: For high-level form creation and management tasks.

### Getting started

>[!NOTE]
>
> The AEM Forms AI Assistant (Forms Experience Builder) is available under the private beta program. Send an email from your work address to [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) to request access.

To learn more about using the AEM Forms AI Assistant , see the [AEM Forms AI Assistant](/help/edge/docs/forms/forms-ai-assistant.md) documentation.

### Example Use Cases

* **"Create a customer feedback form with name, email, rating, and comments fields"**
* **"Convert this uploaded PDF application form into a digital adaptive form"**  
* **"Add conditional logic to show spouse information only when marital status is 'Married'"**
* **"Configure this form to submit data to the Customer Relationship Management system"**

This specialized AEM Forms AI Assistant represents the next evolution in form building, combining the power of AI with AEM's robust forms capabilities to streamline your form creation workflow.
-->
