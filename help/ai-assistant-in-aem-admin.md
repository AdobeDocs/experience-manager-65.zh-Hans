---
title: 配置 AEM 中的 AI 助手
description: 了解如何在 Adobe Experience Manager 中使用 Admin Console 设置和配置 AI 助手。
solution: Experience Manager
feature: Authoring, AI Assistant, AI Tools
role: Admin, Developer, User
exl-id: 06824b3d-f912-4922-8fb6-ee2ca04c6326
autotag-review: '2026-05-18T18:35:37.980Z'
TQID: 'https://experienceleague.adobe.com/5YTQUJbJPlJuxToS6AVhJww1KQ20tuOlRoCVquyfSng'
product_v2: id: e14eb250-3c22-4a07-9061-a78112b2b826id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2: id: ac5ecfc1-cc78-4ecc-a90a-0362685062ce
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 1202
ht-degree: 98%

---

# 配置 AEM 中的 AI 助手 {#aem-ai-asst-admin-setup}

<!-- An Administrator must configure access, permissions, and settings before users in their organization can use the features in AI Assistant in AEM. -->

<!-- badge: label="Beta" type="Positive" -->

要使用 AEM (Adobe Experience Manager) 中的 AI 助手，必须具有通过 AI 助手访问产品知识的权限。 此权限在默认情况下已开启。

如果您希望控制谁可以访问产品知识，请使用与您的 Adobe ID 相关联的电子邮件地址给 [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com) 发送电子邮件。 Adobe 可以启用用户级访问控制。 启用后，您的管理员可以按照下述步骤授予用户级访问权限。

如果您请求用户级访问控制，您的组织就必须通过 Adobe Admin Console 选择加入。 产品管理员创建（或选择）一个用户组，然后授予其新的“AI 助手”权限。 任何添加到该组的人都会立即获得访问 AEM 中 AI 助手的权限。 如果目标是在全公司范围内使用，管理员只需将所有用户分配给这个组。

从员工的角度来说这个过程非常简单：确定您组织中 Adobe Experience Manager 的产品管理员，然后请求将自己添加到启用了 AI 的用户组。 只要您出现在这个组中，您下次登录时就会自动显示“助手”图标。

管理员应牢记常规的 Cloud Manager 治理原则。 在 Admin Console 中保持产品管理员创建配置文件、管理用户组的权限或编辑权限。 如果用户还需要助手工具中内置的&#x200B;**创建支持工单**&#x200B;功能，可将标准的&#x200B;**支持管理员**&#x200B;角色（标准 Admin Console 角色）添加到相同的个人或组。

AEM 中的 AI 助手配置过程包含以下步骤：

1. [在 Adobe Admin Console 中创建一个新的产品配置文件](#create-profile)。
1. [启用 AI 助手产品知识权限](#enable-permission)。
1. [创建一个新的用户组（或使用一个现有的用户组）](#create-user-group)。
1. [将用户添加到这个用户组](#add-users)。
1. [将产品配置文件分配给用户组](#assign-product-profile)。

**先决条件**

在开始之前，请确保您已满足以下前提条件：

* 您在 Adobe Admin Console 中必须至少具有产品管理员权限。
* 您了解组织的用户管理结构。

**配置考虑事项**

* 处理时间：Cloud Manager 中创建的资源可能需要 2 分钟才能显示在 Admin Console 中，用于进行权限配置。
* 多个配置文件：用户可以是多个配置文件的一部分，所有已分配的配置文件中的权限都会合并在一起。
* 组织范围：有些权限可能在所有计划中都在组织级别上应用。
* 预定义的配置文件：不要从 Admin Console 删除预定义的权限配置文件。


## 1 - 在 Adobe Admin Console 中创建一个新的产品配置文件{#create-profile}

1. 按照 Experience Platform 文档中[在 Adobe Admin Console 中创建一个新的产品配置文件](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/access-control/ui/create-profile)中的详细说明操作。

1. 创建新的产品配置文件时，您可以为 AI 助手使用以下建议的值。

   | 文本字段 | 建议的值 |
   | --- | --- |
   | 产品配置文件名称 | `AI Assistant in AEM`（或您首选的描述性名称） |
   | 显示名称（可选） | `AI Assistant` |
   | 描述（可选） | `Product profile for managing AI Assistant in AEM access` |
   | 通知 | 根据您组织的首选项进行配置 |


## 2 - 启用 AI 助手产品知识权限{#enable-permission}

将自定义权限分配给产品配置文件的过程会遵循标准 Adobe Cloud Manager 自定义权限工作流。

参考文章：[将自定义权限分配给产品配置文件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. 在 Admin Console 中，点击您新创建的产品配置文件（`AI Assistant in AEM`）的名称。

   ![屏幕快照](/help/assets/assets-ai/ai-assistant-console.png)

1. 要查看可编辑权限的列表，点击&#x200B;**权限**&#x200B;选项卡。

1. 在表格列表中，找到 `AI Assistant Product Knowledge` 权限。

   ![Admin Console 中的 AI 助手权限选项卡](/help/assets/assets-ai/ai-assistant-permission.png)

1. 在权限名称的右侧，点击![铅笔图标或编辑图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg)。

1. 在&#x200B;**编辑 AI 助手的权限**&#x200B;页面上，打开 **AI 助手产品知识**&#x200B;切换开关。

   ![编辑权限页面上的 AI 助手产品知识切换选项](/help/assets/assets-ai/ai-assistant-prod-knowledge.png)

1. 在页面的右下角，点击&#x200B;**保存**。

   现在，您的产品配置文件已启用 AI 助手产品知识权限。


## 3 - 创建一个新的用户组（或使用一个现有的用户组）{#create-user-group}

1. 执行下列操作之一：

>[!BEGINTABS]

>[!TAB 创建一个新的用户组]

1. 在 Admin Console 中，点击&#x200B;**用户** > **用户组**。

   ![用户组](/help/assets/assets-ai/ai-assistant-user-groups.png)

1. 在&#x200B;**用户组**&#x200B;页面上点击&#x200B;**新建用户组**。

   ![用户组页面上的新建用户组按钮](/help/assets/assets-ai/ai-assistant-new-user-group.png)

1. 在&#x200B;**创建一个新的用户组**&#x200B;页面上提供以下信息：

   | 选项 | 建议的值 |
   | --- | --- |
   | 用户组名称 | `AI Assistant in AEM`（或您首选的名称） |
   | 描述（可选） | `User group for managing AI Assistant in AEM access` |

   ![创建一个新的用户组页面](/help/assets/assets-ai/ai-assistant-create-new-user-group.png)

1. 在页面的右下角，点击&#x200B;**保存**。

>[!TAB 使用一个现有的用户组]

如果现有的 AEM 用户组符合 AI 助手访问权限的要求，您就可以使用这个用户组，而不用新建。

>[!ENDTABS]

## 4 - 将用户添加到这个用户组{#add-users}

1. 执行下列操作之一：

>[!BEGINTABS]

>[!TAB 添加单个用户]

1. 在&#x200B;**用户组**&#x200B;页面的&#x200B;**组名称**&#x200B;表中，点击您新创建的用户组名称或现有的用户组名称。

   ![用户组页面的表格中显示 AEM 中的 AI 助手用户组名称](/help/assets/assets-ai/ai-assistant-user-group-name-in-table.png)

1. 在 **AEM 中的 AI 助手**&#x200B;的&#x200B;**用户组**&#x200B;页面中，点击&#x200B;**用户**&#x200B;选项卡，然后点击&#x200B;**添加用户**。

   ![AEM用户组页面中的AI助手，显示“用户”选项卡和“添加用户”按钮](/help/assets/assets-ai/ai-assistant-add-users.png)

1. 在 **`Add users to this user group`** 页面上，搜索并选择需要 AEM 中的 AI 助手访问权限的用户。

   ![将用户添加到这个用户组页面](/help/assets/assets-ai/ai-assistant-add-users-to-this-group.png)

1. 在页面的右下角，点击&#x200B;**保存**。
1. 现在，[将产品配置文件分配给用户组](#assign-product-profile)。

>[!TAB 批量添加用户]

您可以使用 Admin Console 中的批量上传功能。

1. 准备包含用户信息的 CSV 文件。
1. 使用 **`Add users by CSV`** 选项，高效批量添加。
1. 现在，[将产品配置文件分配给用户组](#assign-product-profile)。

>[!ENDTABS]


## 5 - 将产品配置文件分配给用户组{#assign-product-profile}

这个步骤遵循将产品配置文件分配给用户组的标准 Adobe Admin Console 工作流。

参考文章：[管理企业用户的产品配置文件](https://helpx.adobe.com/cn/enterprise/using/manage-product-profiles.html)

1. 仍然在来自 [4 - 将用户添加到用户组](#add-users)的 AEM 中的 AI 助手用户组中，点击&#x200B;**已分配的产品配置文件**&#x200B;选项卡。
1. 点击 **分配配置文件**。

   ![AEM 中的 AI 助手用户组页面中选择了“已分配的产品配置文件”选项卡](/help/assets/assets-ai/ai-assistant-assign-profile.png)

1. 在&#x200B;**分配产品和配置文件**&#x200B;页面中的&#x200B;**选择产品配置文件**&#x200B;对话框中，搜索并选择您的 **AI 助手**&#x200B;产品配置文件。

   ![“分配产品和配置文件”页面中显示“选择产品配置文件”对话框和已选择的“AI 助手”产品配置文件](/help/assets/assets-ai/ai-assistant-select-product-profile.png)

1. 在对话框的右下角，点击&#x200B;**应用**。
1. 在&#x200B;**分配产品和配置文件**&#x200B;页面右下角附近，点击&#x200B;**保存**。

   ![显示的 AI 助手产品配置文件已分配给 AEM 中的 AI 助手用户组](/help/assets/assets-ai/ai-assistant-profile-assigned-to-user-group.png)


## 验证配置

* 检查您的产品配置文件是否显示正确的已分配用户组数量。
* 验证用户组是否显示正确的用户数量。
* 确认已启用并正确配置了 AI 助手产品知识权限。


## 测试配置

让已分配组中的一名用户执行以下操作：

1. 登录 AEM。
2. 验证 AI 助手功能是否可访问。
3. 测试 AI 助手的功能，确保正确激活。

## 另请参阅

* [AEM 中的 AI 助手](/help/ai-assistant-in-aem.md)
* [Adobe Experience Platform 访问控制](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/access-control/ui/overview)
<!-- * [Cloud Manager Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md) -->
