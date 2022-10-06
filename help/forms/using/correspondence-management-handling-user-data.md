---
title: 通信管理 |处理用户数据
seo-title: Correspondence Management | Handling user data
description: 通信管理 |处理用户数据
uuid: d5bb190b-d668-4da3-95da-b7705ad302d9
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 764d8e0d-604d-4c7b-89cd-7686ce5f03ff
role: Admin
exl-id: a0c6a02c-47a3-4e70-a14c-953ee016b8e4
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# 通信管理 |处理用户数据 {#correspondence-management-handling-user-data}

AEM Forms通信管理使您能够创建、管理和简化安全的个性化客户信函。 它为商业用户提供了直观的用户界面，以便使用预先批准的内容块和媒体元素创建对应。 有关创建通信的更多信息，请参阅 [创建通信](/help/forms/using/create-correspondence.md).

当业务用户或代理将通信保存为草稿或提交时，信件实例会保存在AEM存储库中。 信件实例包括通信数据和元数据。

>[!NOTE]
>
>在AEM 6.5 Forms中，无法开箱即用地进行通信管理。 如果您从以前的AEM Forms版本进行升级，请安装兼容包并迁移通信管理资产，以继续在AEM 6.5 Forms中使用它们。 有关更多信息，请参阅 [兼容包](/help/forms/using/compatibility-package.md).

## 用户数据和数据存储 {#data}

仅当将发布实例配置为管理信件实例时，通信管理才会在AEM存储库中存储草稿和提交信件的数据。 有关配置的更多信息，请参阅 [通信管理配置属性](/help/forms/using/cm-configuration-properties.md).

根据为AEM部署配置的数据存储持久性，草稿和提交的通信数据存储在以下位置。

<table>
 <tbody>
  <tr>
   <td><p><strong>持久性类型</strong></p> </td>
   <td><p><strong>数据存储</strong></p> </td>
   <td><p><strong>位置</strong></p> </td>
  </tr>
  <tr>
   <td><p>默认</p> </td>
   <td><p>AEM在反向复制配置中指定的发布实例和创作实例存储库</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code> </p> </td>
  </tr>
  <tr>
   <td><p>远程</p> </td>
   <td><p>AEM远程处理创作实例存储库</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

在以上指定的AEM存储库位置中：

* `[yyyy]/[mm]/[dd]` 是基于创建信件实例日期的节点结构
* `[node-id]` 是分配给包含信件的文件夹的ID
* `[letter-instance-name]` 是保存或提交信件时指定的名称

在 [letter-instance-name] 节点中，将创建以下节点结构，并且每个信件实例的数据都存储在AEM存储库中：

| 节点 | 描述 |
|---|---|
| `extendedProperties` | 存储信件实例的元数据属性。 |
| `dataXML` | 以二进制格式存储包含通信数据的可下载dataXML文件。 |
| `processedXDP` | 包括用于创建已提交信件的XDP模板的详细信息。 此节点仅为提交的通信创建。 |
| `submittedLetter` | 以可下载的二进制格式存储提交的信件数据。 此节点仅为提交的通信创建。 |

## 访问和删除用户数据 {#access-and-delete-user-data}

您可以访问已配置数据存储中的草稿和已提交的通信数据，并在必要时将其删除。

### 访问用户数据 {#access-user-data}

通信管理提供了API，您可以使用这些API来查找和访问草稿和提交的信件实例。 使用API，您可以使用信件实例ID或保存或提交通信的用户查找和打开信件实例。 有关更多信息，请参阅 [用于访问信件实例的API](/help/forms/using/cm-apis-to-access-letter-instances.md).

或者，您也可以使用CRX DELite导航到AEM存储库中的信件实例。 请参阅 [用户数据和数据存储](/help/forms/using/correspondence-management-handling-user-data.md#data) 有关存储的数据和存储库位置的信息。

### 删除用户数据 {#delete-user-data}

要查找包含特定用户数据的信件实例，您可以：

* 如果已知信件实例名称或保存草稿或提交信件的用户，请使用通信管理API
* 使用AEM存储库搜索（使用电子邮件ID或名称等个人身份信息）来查找存储信息的节点

要从AEM系统中完全删除草稿和提交的通信中的用户数据，您必须从所有适用的AEM实例中手动删除信件实例节点。
