---
title: AEM 6.5人工智能助理
description: 使用 AI 助手帮助您找到答案，并为 Adobe Experience Manager 中提供的解决方案修复错误。
solution: Experience Manager, Experience Manager 6.5
feature: Authoring, AI Assistant, AI Tools
role: Admin, Developer, User
exl-id: 3b4a484e-55b5-4924-82dd-56735f6ed46d
autotag-review: '2026-05-18T18:36:07.915Z'
TQID: 'https://experienceleague.adobe.com/dlFmrtn05S20z96wtAfkpGliITeVJhVkofqPix6QMxk'
product_v2: id: e14eb250-3c22-4a07-9061-a78112b2b826id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2: id: ac5ecfc1-cc78-4ecc-a90a-0362685062ce
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: c1579802-ddd4-4214-8a91-97b2066abe11id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adebid: d095671a-1355-40aa-8b5f-06c33c68080bid: e1e0219c-f879-479f-8427-888ed2a6e9c2id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 1379
ht-degree: 93%

---

# AEM 6.5人工智能助理 {#about-ai-assistant-in-aem}

>[!IMPORTANT]
>
>不使用 Cloud Manager/Experience Hub 的 AEM 6.5 和 AEM 6.5 LTS 客户必须联系其 Adobe 客户成功工程师，获取 AI 助手访问权限。

AEM 6.5/AEM 6.5 LTS中的AI Assistant提供了一个对话界面，旨在简化为Adobe Experience Manager相关查询查找答案的过程。 它可以帮助您立即获得与 AEM 产品相关的问题的回答（*提供给所有用户使用*），可自动创建支持工单（*提供给支持管理员使用*）。

AI 助手支持 AEM as a Cloud Service，包括以下解决方案：

* Experience Hub 概述页面
* Edge Delivery Services
* Sites
* Assets
* 表单
* Dynamic Media
* Cloud Manager


它直接嵌入在 AEM 中，可从 AEM Experience Hub、Cloud Manager 和 Author UI 访问。

以下这段时长 3 分 25 秒的视频分步介绍了 AEM 中的 AI 助手。

>[!VIDEO](https://video.tv.adobe.com/v/3475357/?learn=on&enablevpops)

## 访问 AEM 中的 AI 助手{#get-access}

要获得 AEM 中 AI 助手的访问权限，客户必须：

* 有权使用 AEM 中的 AI 助手获取产品知识。 此权限允许您在 AI 助手聊天中询问产品相关的问题。 此权限必须启用。
* 有权打开支持工单，这需要&#x200B;**支持管理员**&#x200B;的角色。

>[!NOTE]
>
>AEM 中的 AI 助手请求通过 Adobe Identity Management Services (IMS) 进行身份验证。 有关详细信息，请参阅 [Adobe Identity Management Services 概述](https://www.adobe.com/cn/content/dam/cc/en/trust-center/ungated/whitepapers/corporate/adobe-identity-management-services-security-overview.pdf)。

**要访问 AEM 中的 AI 助手：**

1. 客户必须另外签订协议才能访问 Adobe Experience Manager 中的大多数 AI 驱动的代理式功能。 请联系您的 Adobe 代表，获取更多详情。

1. 要使用 AEM 中的 AI 助手，必须具有通过 AI 助手访问产品知识的权限。 此权限在默认情况下已开启。

   如果您希望控制谁可以访问产品知识，请使用与您的 Adobe ID 相关联的电子邮件地址给 [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com) 发送电子邮件。 Adobe 可以启用用户级访问控制。 启用后，您的管理员可以按照[配置 AEM 中的 AI 助手](/help/ai-assistant-in-aem-admin.md)中说明的步骤授予用户级访问权限。


## 范围 {#scope}

AEM中AI助理的当前范围侧重于解决AEMr as a Cloud Service的产品知识问题。 此范围包括了对关键领域的全面支持。<!--, such as Sites, Assets, Forms, Edge Delivery Services, Dynamic Media, and Cloud Manager. -->

* **表面**：在 AEM Experience Hub、作者 UI、Cloud Manager 中可用。
* **功能**：提供产品知识，是疑难解答和指导的第一站，自动创建支持工单和查找。
* **价值**：节省时间，加快学习，缩短价值实现时间，减少手动创建支持工单的需求，提高创建支持工单的效率。

## 隐私、安全和治理{#privacy-security-governance}

AEM 中的 AI 助手的设计特别强调隐私、安全和治理。

本文概述了您可以从 AEM 中的 AI 助手获得的特别重视可信度的各种功能：

* AEM 中的 AI 助手不使用，也不会以训练为目的使用任何个人数据。
* AEM 中的 AI 助手不会访问消费者数据。
* 需要明确的权限才能与 AEM 中的 AI 助手交互。
* 用户提供的提示词（问题、查询等）不会与其他客户共享。

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## 了解 AEM 中的 AI 助手提供的产品知识和自动创建支持工单的功能 {#ai-prod-insights}

产品知识包含从 Adobe Experience League 文档派生的各种概念和主题。 这些问题可分类为以下几个子组：


| 产品知识 | 提供给所有用户使用<br>示例 |
| :--- | :--- |
| 有针对性的学习 | <ul><li>什么是通用编辑器？</li><li>如何在 Cloud Manager 中创建程序？</li></ul> |
| 打开发现 | <ul><li>如何使用通用编辑器？</li><li>是否可以将内容从一个环境复制到另一个环境？</li></ul> |
| 疑难解答 | <ul><li>为什么无法访问通用编辑器？</li><li>我的管道为什么会失败？</li></ul> |
| **创建支持工单** | **仅提供给支持管理员使用&#x200B;**<br>**示例** |
| 自动创建支持工单，捕获 AI 助手聊天记录和上下文 | <ul><li>为我创建一个支持工单。</li></ul> |
| 检索支持工单的状态 | <ul><li>显示我已打开的所有支持工单。</li><li>显示工单“E-----------”的状态</li></ul> |

{style="table-layout:auto"}


## 如何表述有效的问题 {#ai-craft-questions}

要通过 AEM 中的 AI 助手获得最准确的回答，清晰地表述您的问题并提供上下文，这一点十分重要。 采用以下建议可确保您的查询语句清晰、有条有理：

* 以简洁明了的方式清晰地表述您的任务或问题。
* 避免使用含糊不清的词语或过于复杂的语法，使表述更加易于理解。
* 提供有关您的任务或问题的相关上下文，因为这可以帮助 AEM 中的 AI 助手提供更准确、更相关的回答。
例如，在提示词中说明您正在使用哪种 AEM 解决方案（Sites、Assets、Dynamic Media、Edge Delivery Services、Cloud Manager 或 Forms）会很有帮助。

### 不受支持的问题示例 {#ai-unsupported-questions}

| 区域 | 示例 |
| --- | --- |
| 运营洞察 | <ul><li>我的租户中有多少个开发环境？</li><li>谁启动了最后一个生产管道？</li></ul> |
| 疑难解答 | <ul><li>为什么我的生产管道失败了？</li></ul> |
| 任务和自动化 | <ul><li>为我从开发分支开始配置一个代码质量管道。</li></ul> |


## 使用 AEM 中的 AI 助手 {#ai-use}

<!--
UNHIDE AFTER BETA or at GA
### Enable AI Assistant in AEM access through Admin Console 

To use AI Assistant in AEM, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AI Assistant in AEM in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in AI Assistant in AEM of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md).
-->


### 开始一个 AEM 中的 AI 助手对话

如果您想更改主题，可以重置 AEM 中的 AI 助手，开始一个新的对话。 如果您在查询失败或提供错误信息的情况下想修正错误，这个功能就特别有用。

**要开始一个 AEM 中的 AI 助手对话：**

1. 在 AEM 用户界面（从 Cloud Manager 页面或者 AEM 环境的作者实例中）的右上角附近，点击 **AI 助手**&#x200B;图标。

   ![工具栏中的 AI 助手图标](/help/assets/assets-ai/ai-assistant-icon.png)

1. 在底部的 **AI 助手**&#x200B;面板文本框中，输入您的问题或提示词，然后按下 `Enter` 或点击![发送图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg)。

   >[!NOTE]
   >
   >不要在您的输入中提供个人数据，因为使用这个工具不需要个人数据。

   ![AI 助手面板底部的文本框](/help/assets/assets-ai/ai-assistant-prompt-text-box.png)

1. 要开始一个新的对话（新主题或更改主题），请点击![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) > **开始新对话**。

   ![通过省略号图标开始 AI 助手中的新对话](/help/assets/assets-ai/ai-assistant-start-new-conversation.png)

### 按类别发现提示词

AEM 中的 AI 助手包括一个可发现性功能，帮助您探索受支持的主题和类别。

**要按类别发现提示词：**

1. 在 AI 助手面板中，点击![学习图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)，打开提示词发现面板。

   ![面板允许您在 AI 助手中按类别浏览提示词](/help/assets/assets-ai/ai-assistant-discover-prompts.png)
   *面板中显示 AI 助手中的提示词类别。*

1. 选择一个类别，查看相关提示词的列表。
1. 选择一个提示词，查看 AI 助手可以回答的各类问题的示例。

1. 如要隐藏提示词发现面板，再次点击![学习图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)。

### 分享您关于 AEM 中的 AI 助手的反馈

您的输入可帮助 Adobe 改进 AI 助手，提高其性能和准确性。

通过以下选项分享您关于 AEM 中 AI 助手体验的反馈：

![点赞、点踩和旗帜图标](/help/assets/assets-ai/ai-assistant-feedback-icons.png)

| 单击 | 描述 |
| --- | --- |
| ![点赞图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | 表示哪些方面做得很好，并分享正面反馈。 |
| ![点踩图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | 提出改进建议。 添加关于您的体验的具体评论，这些评论每天都会审阅。 |
| ![旗帜图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | 报告有关您与 AEM 中的 AI 助手交互的问题或提供相关详细反馈。 |

## 关于 AEM 中 AI 助手的常见问题解答 {#ai-faq}

以下是关于 AI 助手的一些常见问题的解答：

* **AEM 中的 AI 助手提供的是实时信息吗？**\
  不行。 AI 助手从 Adobe Experience League 文档获取内容。 这个内容更新以后，可能需要一段时间才能在回答中反映出来。
* **AEM 中的 AI 助手支持哪些 Adobe 应用程序？**\
  目前，AI Assistant支持AEM as a Cloud Service中的产品知识查询，包括Sites、Assets、Dynamic Media、Cloud Manager和Forms。
* **AEM 中的 AI 助手有哪些功能？**\
  AEM中的AI助手可回答与Adobe产品知识相关的查询。
* **AEM 中的 AI 助手是否会将个人信息用于训练数据？**\
  不行。 AEM 中的 AI 助手不会将个人信息用于训练目的。 不用为 AEM 中的 AI 助手提供您或其他人的个人信息，包括姓名或联系方式。

<!--
IS THE DOCUMENTATION BELOW STILL NEEDED? IF SO, GO AHEAD AND DELETE THE COMMENT TAGS!!

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
