---
title: 社区站点要点
description: 导出和删除社区站点并创建自定义站点模板
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 1%

---

# 社区站点要点 {#community-site-essentials}

## 自定义站点模板 {#custom-site-template}

可以为社区站点的每个语言副本单独指定自定义站点模板。

为此，请执行以下操作：

* 创建自定义模板。
* 覆盖默认站点模板路径。
* 将自定义模板添加到叠加路径。
* 通过将`page-template`属性添加到`configuration`节点来指定自定义模板。

**默认模板**：

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**覆盖路径中的自定义模板**：

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**属性**：页面模板

**类型**：字符串

**值**： `template-name` （无扩展名）

**配置节点**：

`/content/community site path/lang/configuration`

例如：`/content/sites/engage/en/configuration`

>[!NOTE]
>
>覆盖路径中的所有节点只需要是`Folder`类型。

>[!CAUTION]
>
>如果自定义模板被指定为&#x200B;*sitepage.hbs*，则所有社区站点都是自定义的。

### 自定义站点模板示例 {#custom-site-template-example}

例如，`vertical-sitepage.hbs`是一个网站模板，它导致菜单链接在页面左侧垂直向下放置，而不是在横幅下方水平放置。

[获取文件](assets/vertical-sitepage.hbs)
将自定义站点模板放置在覆盖文件夹中：

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

通过向配置节点添加`page-template`属性来标识自定义模板：

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

请务必&#x200B;**全部保存**&#x200B;并将自定义代码复制到所有Adobe Experience Manager (AEM)实例（从控制台发布社区站点内容时不包括自定义代码）。

复制自定义代码的推荐做法是[创建包](../../help/sites-administering/package-manager.md#creating-a-new-package)并在所有实例上部署它。

## 导出社区站点 {#exporting-a-community-site}

创建社区站点后，可以将站点导出为存储在包管理器中的AEM包，并可供下载和上传。

这可以从[社区站点控制台](sites-console.md#exporting-the-site)中获得。

UGC和自定义代码未包含在社区站点包中。

要导出UGC，请使用[AEM Communities UGC迁移工具](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration)，它是GitHub上提供的开源迁移工具。

## 删除社区站点 {#deleting-a-community-site}

截至AEM Communities 6.3 Service Pack 1，将鼠标悬停在&#x200B;**[!UICONTROL 社区]** > **[!UICONTROL 站点]**&#x200B;控制台中的社区站点上时，将显示“删除站点”图标。 在开发过程中，如果想要删除社区站点并重新开始，则可以使用此功能。 删除社区站点时，将删除与该站点关联的以下项目：

* [UGC](#user-generated-content)
* [用户组](#community-user-groups)
* [数据库记录](#database-records)

### 社区唯一站点ID {#community-unique-site-id}

要使用CRXDE识别与社区站点关联的唯一站点ID，请执行以下操作：

* 导航到站点的语言根，如`/content/sites/*<site name>*/en/rep:policy`。

* 找到格式为`rep:principalName = *community-enable-nrh9h-members*`且带有`rep:principalName`的`allow<#>`节点。

* 网站ID是`rep:principalName`的第三个组件

  例如，如果`rep:principalName = community-enable-nrh9h-members`

   * **站点名称** = *启用*
   * **站点ID** = *nrh9h*
   * **唯一站点ID** = *enable-nrh9h*

### 用户生成的内容 {#user-generated-content}

从GitHub获取communities-srp-tools项目：

* [https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

这包含一个servlet，用于从任何SRP中删除所有UGC。

可以删除所有UGC或针对特定站点的UGC，例如：

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

这仅会删除用户生成的内容（在发布时输入），而不会删除创作的内容（在创作时输入）。 因此，[影子节点](srp.md#shadownodes)不受影响。

### 社区用户组 {#community-user-groups}

在所有作者和发布实例上，从[安全控制台](../../help/sites-administering/security.md)中，查找并删除符合以下条件的[用户组](users.md)：

* 以`community`为前缀
* 后跟[唯一站点ID](#community-unique-site-id)

例如：`community-engage-x0e11-members`。
