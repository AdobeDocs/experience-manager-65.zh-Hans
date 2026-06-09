---
title: 权限管理的主要视图
description: 了解有利于权限管理的全新触屏 UI 界面。
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
docset: aem65
exl-id: 4ce19c95-32cb-4bb8-9d6f-a5bc08a3688d
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 8adc566113beedc408698dccc3a4c072349af5dc
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 84%

---


# 权限管理的主要视图{#principal-view-for-permissions-management}

## 概述 {#overview}

AEM 6.5引入了用户和组的权限管理。 主要功能与经典用户 UI 保持一致，但更加友好和高效。

## 使用方法 {#how-to-use}

### 访问 UI {#accessing-the-ui}

新的基于 UI 的权限管理可通过“安全性”下的“权限”信息卡访问，如下所示：

![权限管理 UI](assets/screen_shot_2019-03-17at63333pm.png)

通过新视图，可以更轻松地查看给定主体在明确授予权限的所有路径上的整套特权和限制。 这样就无需前往

CRXDE 来管理高级特权和限制。 它已在同一个视图中得到合并。 该视图默认为“everyone”组。

![“所有人”组的视图](assets/unu-1.png)

有一个过滤器，允许用户通过查看&#x200B;**用户**、**群组**&#x200B;或&#x200B;**全部**&#x200B;来选择主体类型，并搜索任何主体&#x200B;**。**

![搜索主体类型](assets/image2019-3-20_23-52-51.png)

### 查看主体的权限 {#viewing-permissions-for-a-principal}

左侧的框架允许用户向下滚动，以查找任何主体或根据所选过滤器搜索群组或用户，如下所示：

![查看主体的权限](assets/doi-1.png)

单击名称会在右侧显示分配的权限。 权限窗格显示特定路径上的访问控制条目列表以及配置的限制。

![查看 ACL 列表](assets/trei-1.png)

### 为主体添加新的访问控制条目 {#adding-new-access-control-entry-for-a-principal}

可以通过添加访问控制条目来添加新权限。 只需单击“添加 ACE”按钮即可。

![为主体添加新的 ACL](assets/patru.png)

这将打开如下所示的窗口，下一步是选择必须配置权限的路径。

![配置权限路径](assets/cinci-1.png)

这里选择了一条路径，您可以在其中为 **dam-users** 配置权限：

![dam-users 的示例配置](assets/sase-1.png)

选择路径后，工作流返回到此屏幕，用户可以从可用的命名空间中选择一个或多个特权（如 `jcr`、`rep` 或 `crx`），如下所示。

可以通过使用文本字段搜索然后从列表中选择来添加特权。

>[!NOTE]
>
>有关特权和说明的完整列表，请参阅[用户、群组和访问权限管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)。

![给定路径的搜索权限。](assets/image2019-3-21_0-5-47.png) ![为“dam-users”添加新条目，如在垂直列中选择的路径所示。](assets/image2019-3-21_0-6-53.png)

选择特权列表后，用户可以选择权限类型：拒绝或允许，如下所示。

![选择权限](assets/screen_shot_2019-03-17at63938pm.png) ![选择权限](assets/screen_shot_2019-03-17at63947pm.png)

### 使用限制 {#using-restrictions}

除了给定路径上的权限和权限类型列表之外，此屏幕还允许您为细粒度访问控制添加限制，如下所示：

![添加限制](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>有关每个限制含义的更多信息，请参阅 [Jackrabbit Oak 文档](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)。

可以通过选择限制类型、输入值并点击 **+** 图标来添加限制，如下所示。

![添加限制类型](assets/sapte-1.png) ![添加限制类型](assets/opt-1.png)

新的 ACE 反映在访问控制列表中，如下所示。 请注意，`jcr:write`是一个聚合特权，它包含上面添加的`jcr:removeNode`，但不显示于下方，因为它包含在`jcr:write`中。

### 编辑 ACE {#editing-aces}

访问控制条目可以通过选择主体和选择要编辑的 ACE 来编辑。

例如，您可以单击右侧的铅笔图标来编辑以下 **dam-users** 条目：

![添加限制](assets/image2019-3-21_0-35-39.png)

编辑屏幕显示预先选择的已配置 ACE，可以通过单击旁边的十字图标来删除它们，或者可以为给定的路径添加新的特权，如下所示。

![编辑条目](assets/noua-1.png)

此处为给定路径上的 **dam-users** 添加了 `addChildNodes` 特权。

![添加特权](assets/image2019-3-21_0-45-35.png)

单击右上方的&#x200B;**保存**&#x200B;按钮可保存更改，更改将反映在&#x200B;**dam-users**&#x200B;的新权限中，如下所示：

![保存更改](assets/zece-1.png)

### 删除 ACE {#deleting-aces}

可以删除访问控制条目，以移除特定路径上给定主体的所有权限。 可以用 ACE 旁边的 X 图标删除它，如下所示：

![删除 ACE](assets/image2019-3-21_0-53-19.png) ![删除 ACE](assets/unspe.png)

### 经典 UI 特权组合 {#classic-ui-privilege-combinations}

新的权限 UI 明确使用基本特权集，而不是预定义的组合，因为预定义的组合不能真正反映授予的确切底层特权。

这导致人们对具体配置的内容感到困惑。 下表列出了经典 UI 中的特权组合与构成它们的实际特权之间的映射：

<table>
 <tbody>
  <tr>
   <th>经典 UI 特权组合</th>
   <th>权限 UI 特权</th>
  </tr>
  <tr>
   <td>读取</td>
   <td><code>jcr:read</code></td>
  </tr>
  <tr>
   <td>修改</td>
   <td><p><code>jcr:modifyProperties</code></p> <p><code>jcr:lockManagement</code></p> <p><code>jcr:versionManagement</code></p> </td>
  </tr>
  <tr>
   <td>创建</td>
   <td><p><code>jcr:addChildNodes</code></p> <p><code>jcr:nodeTypeManagement</code></p> </td>
  </tr>
  <tr>
   <td>删除</td>
   <td><p><code>jcr:removeNode</code></p> <p><code>jcr:removeChildNodes</code></p> </td>
  </tr>
  <tr>
   <td>读取 ACL</td>
   <td><code>jcr:readAccessControl</code></td>
  </tr>
  <tr>
   <td>编辑 ACL</td>
   <td><code>jcr:modifyAccessControl</code></td>
  </tr>
  <tr>
   <td>复制</td>
   <td><code>crx:replicate</code></td>
  </tr>
 </tbody>
</table>
