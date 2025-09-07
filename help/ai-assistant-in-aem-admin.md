---
title: 在AEM中配置AI助手
description: 了解如何使用Adobe Experience Manager中的Admin Console设置和配置AI助手。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 06824b3d-f912-4922-8fb6-ee2ca04c6326
source-git-commit: 11be37d5a96dd7236f2011b6df3e39bf0b1904b7
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 3%

---

# 在AEM中配置AI助手 {#aem-ai-asst-admin-setup}

<!-- An Administrator must configure access, permissions, and settings before users in their organization can use the features in AI Assistant in AEM. -->

<!-- badge: label="Beta" type="Positive" -->

要在AEM (Adobe Experience Manager)中使用AI助手，您的组织必须选择Admin Console级别的加入。 产品管理员创建（或选择）用户组并授予其新的“AI助手”权限。 任何添加到该组的人都会立即获得AEM人工智能助理的访问权限。 如果目标是实现公司范围的可用性，管理员只需将所有用户分配给该组即可。

从员工的角度来看，此过程非常简单：确定贵组织中Adobe Experience Manager的产品管理员，并请求将其添加到支持AI的用户组。 一旦您出现在该组中，“助理”图标将在您下次登录时自动显示。

管理员应牢记常规的Cloud Manager管理。 在Admin Console中保留产品管理员权限以创建配置文件、管理用户组或编辑权限。 如果用户还需要该助理的内置&#x200B;**创建支持票证**&#x200B;功能，请将标准&#x200B;**支持管理员**&#x200B;角色(标准Admin Console角色)添加到相同的个人或组。

AEM中的AI助手配置过程包含以下步骤：

1. [在Adobe Admin Console中创建新产品配置文件](#create-profile)。
1. [启用AI助理产品知识权限](#enable-permission)。
1. [创建新用户组（或使用现有用户组）](#create-user-group)。
1. [将用户添加到用户组](#add-users)。
1. [将产品配置文件分配给用户组](#assign-product-profile)。

**先决条件**

在开始之前，请确保已满足以下先决条件：

* 您在Adobe Admin Console中必须至少具有产品管理员权限。
* 您了解组织的用户管理结构。

**配置注意事项**

* 处理时间：在Cloud Manager中创建的资源可能最多需要2分钟才能在Admin Console中显示以进行权限配置。
* 多个配置文件：用户可以是多个配置文件的一部分，并且所有分配的配置文件中的权限都会合并在一起。
* 组织范围：某些权限可能适用于所有项目的组织级别。
* 预定义配置文件：请勿从Admin Console中删除预定义权限配置文件。


## 1 — 在Adobe Admin Console中创建新产品配置文件{#create-profile}

1. 按照Experience Platform文档中的[在Adobe Admin Console中创建新产品配置文件](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/access-control/ui/create-profile)中的详细说明操作。

1. 创建新的产品配置文件时，您可以为AI助手使用以下建议值。

   | 文本字段 | 建议的值 |
   | --- | --- |
   | 产品配置文件名称 | `AI Assistant in AEM`（或您的首选描述性名称） |
   | 显示名称（可选） | `AI Assistant` |
   | 描述（可选） | `Product profile for managing AI Assistant in AEM access` |
   | 通知 | 根据贵组织的首选项进行配置 |


## 2 — 启用“AI助手产品知识”权限{#enable-permission}

将自定义权限分配给产品配置文件的过程遵循标准Adobe Cloud Manager自定义权限工作流程。

参考文章： [将自定义权限分配给新产品配置文件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. 在Admin Console中，单击新创建的产品配置文件的名称(`AI Assistant in AEM`)

   ![屏幕快照](/help/assets/assets-ai/ai-assistant-console.png)

1. 要查看可编辑权限列表，请单击&#x200B;**权限**&#x200B;选项卡。

1. 在表列表中，找到`AI Assistant Product Knowledge`权限。

   Admin Console中的![AI助手权限选项卡](/help/assets/assets-ai/ai-assistant-permission.png)

1. 在权限名称的右侧，单击![铅笔图标或编辑图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg)。

1. 在&#x200B;**编辑AI助理的权限**&#x200B;页面上，打开&#x200B;**AI助理产品知识**&#x200B;切换开关。

   ![AI助手产品知识切换选项的“编辑权限”页面](/help/assets/assets-ai/ai-assistant-prod-knowledge.png)

1. 在页面的右下角，单击&#x200B;**保存**。

   您的产品配置文件现在已启用AI助理产品知识权限。


## 3 — 创建新用户组（或使用现有用户组）{#create-user-group}

1. 执行下列操作之一：

>[!BEGINTABS]

>[!TAB 创建新用户组]

1. 在Admin Console中，单击&#x200B;**用户** > **用户组**。

   ![用户组](/help/assets/assets-ai/ai-assistant-user-groups.png)

1. 在&#x200B;**用户组**&#x200B;页面上，单击&#x200B;**新建用户组**。

   “用户组”页面上的![新建用户组按钮](/help/assets/assets-ai/ai-assistant-new-user-group.png)

1. 在&#x200B;**创建新用户组**&#x200B;页面上，提供以下信息：

   | 选项 | 建议的值 |
   | --- | --- |
   | 用户组名称 | `AI Assistant in AEM`（或您的首选名称） |
   | 描述（可选） | `User group for managing AI Assistant in AEM access` |

   ![创建新的用户组页面](/help/assets/assets-ai/ai-assistant-create-new-user-group.png)

1. 在页面的右下角，单击&#x200B;**保存**。

>[!TAB 使用现有用户组]

如果现有AEM用户组符合AI Assistant访问要求，则可以使用该用户组，而不是创建新组。

>[!ENDTABS]

## 4 — 将用户添加到用户组{#add-users}

1. 执行下列操作之一：

>[!BEGINTABS]

>[!TAB 添加个人用户]

1. 在&#x200B;**用户组**&#x200B;页面的&#x200B;**组名称**&#x200B;表中，单击您新创建的用户组名称或现有用户组名称。

   ![用户组页面显示表中的AEM用户组名称中的AI助手](/help/assets/assets-ai/ai-assistant-user-group-name-in-table.png)

1. 在AEM **中** AI助手的&#x200B;**用户组**&#x200B;页面中，单击&#x200B;**用户**&#x200B;选项卡，然后单击&#x200B;**添加用户**。

   ![AEM用户组页面中的AI助手，显示“用户”选项卡和“添加用户”按钮](/help/assets/assets-ai/ai-assistant-add-users.png)

1. 在&#x200B;**`Add users to this user group`**&#x200B;页面上，搜索并选择需要访问AEM中的AI助手的用户。

   ![将用户添加到此用户组页面](/help/assets/assets-ai/ai-assistant-add-users-to-this-group.png)

1. 在页面的右下角，单击&#x200B;**保存**。
1. 现在，[将产品配置文件分配给用户组](#assign-product-profile)。

>[!TAB 批量添加用户]

您可以使用Admin Console中的批量上传功能。

1. 准备包含用户信息的CSV文件。
1. 使用&#x200B;**`Add users by CSV`**&#x200B;选项进行高效的批量添加。
1. 现在，[将产品配置文件分配给用户组](#assign-product-profile)。

>[!ENDTABS]


## 5 — 将产品配置文件分配给用户组{#assign-product-profile}

此步骤遵循标准Adobe Admin Console工作流，以将产品配置文件分配给用户组。

参考文章： [管理企业用户的产品配置文件](https://helpx.adobe.com/cn/enterprise/using/manage-product-profiles.html)

1. 当仍在AEM用户组的AI助手中时（该用户组来自[4 — 将用户添加到用户组](#add-users)），单击&#x200B;**已分配的产品配置文件**&#x200B;选项卡。
1. 单击&#x200B;**分配配置文件**。

   ![AEM用户组页面中的AI助手，已选择“已分配产品配置文件”选项卡](/help/assets/assets-ai/ai-assistant-assign-profile.png)

1. 在&#x200B;**分配产品和配置文件**&#x200B;页面的&#x200B;**选择产品配置文件**&#x200B;对话框中，搜索并选择您的&#x200B;**AI助手**&#x200B;产品配置文件。

   ![“分配产品和配置文件”页面，显示“选择产品配置文件”对话框和已选择的“AI助手”产品配置文件](/help/assets/assets-ai/ai-assistant-select-product-profile.png)

1. 在对话框的右下角附近，单击&#x200B;**应用**。
1. 在&#x200B;**分配产品和配置文件**&#x200B;页面的右下角附近，单击&#x200B;**保存**。

   显示的![AI助手产品配置文件已分配给AEM用户组中的AI助手](/help/assets/assets-ai/ai-assistant-profile-assigned-to-user-group.png)


## 验证配置

* 检查产品配置文件是否显示正确数量的已分配用户组。
* 验证用户组是否显示正确数量的用户。
* 确认已启用并正确配置了AI助手产品知识权限。


## 测试配置

让已分配组中的用户执行以下操作：

1. 登录 AEM。
2. 验证AI助手功能是否可访问。
3. 测试AI Assistant的功能以确保正确激活。

## 另请参阅

* [AEM 中的 AI 助手](/help/ai-assistant-in-aem.md)
* [Adobe Experience Platform访问控制](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/access-control/ui/overview)
<!-- * [Cloud Manager Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md) -->
