---
title: 用户同步
description: 了解AEM中用户同步的内部工作原理。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 89f55598-e749-42b8-8f2a-496f45face66
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '2433'
ht-degree: 1%

---


# 用户同步{#user-synchronization}

## 简介 {#introduction}

当部署是[发布场](/help/sites-deploying/recommended-deploys.md#tarmk-farm)时，成员必须能够在任何Publish节点上登录并查看其数据。

创作环境中不需要在发布环境中创建的用户和用户组（用户数据）。

在创作环境中创建的大多数用户数据都会保留在创作环境中，而不会复制到Publish实例。

对一个Publish实例所做的注册和修改必须与其他Publish实例同步，它们才能访问相同的用户数据。

从AEM 6.1开始，当用户同步启用时，用户数据将自动在场中的Publish实例之间同步，并且不会在author上创建。

## Sling分发 {#sling-distribution}

用户数据及其[ACL](/help/sites-administering/security.md)存储在Oak JCR下层的[Oak Core](/help/sites-deploying/platform.md)中，并使用[Oak API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/oak/api/package-tree.html)访问。 由于更新不频繁，因此可以使用[Sling内容分发](https://github.com/apache/sling-old-svn-mirror/blob/trunk/contrib/extensions/distribution/README.md)（Sling分发）将用户数据与其他Publish实例同步。

与传统复制相比，使用Sling分发的用户同步具有以下优势：

* 在Publish中创建的&#x200B;*用户*、*用户配置文件*&#x200B;和&#x200B;*用户组*&#x200B;不是在Author上创建的

* Sling分发可设置jcr事件中的属性，从而能够在发布端事件侦听器内执行操作，而无需考虑无限复制循环
* Sling Distribution仅将用户数据发送到非原始Publish实例，从而消除不必要的流量
* 同步中包括用户节点中设置的[ACL](/help/sites-administering/security.md)

>[!NOTE]
>
>如果需要进行会话，建议使用SSO解决方案或使用粘性会话，并且在客户切换到其他Publish实例时让他们登录。

>[!CAUTION]
>
>不支持同步&#x200B;**管理员**&#x200B;组，即使启用了用户同步也是如此。 相反，错误日志中会记录“导入差异”失败。
>
>因此，当部署是发布场时，如果将某个用户添加到&#x200B;**管理员**&#x200B;组或从中删除，则必须对每个Publish实例手动进行修改。

## 启用用户同步 {#enable-user-sync}

>[!NOTE]
>
>默认情况下，用户同步为`disabled`。
>
>启用用户同步涉及修改&#x200B;*现有* OSGi配置。
>
>启用用户同步后，不应添加任何新配置。

用户同步依赖作者环境管理用户数据分发，即使未在作者上创建用户数据也是如此。 大部分配置（但不是全部）发生在创作环境中，每个步骤都清楚地标识是要在创作环境还是在Publish上执行。

以下是启用用户同步所需的步骤，随后是[疑难解答](#troubleshooting)部分：

### 先决条件 {#prerequisites}

1. 如果已在某个Publish实例上创建用户和用户组，则建议在配置和启用用户同步之前，将用户数据[手动同步](#manually-syncing-users-and-user-groups)到所有Publish实例。

启用用户同步后，将仅同步新创建的用户和组。

1. 确保安装了最新的代码：

* [AEM平台更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=zh-Hans)
* [AEM Communities更新](/help/communities/deploy-communities.md#latestfeaturepack)

### 1. Apache Sling分发代理 — 同步代理工厂 {#apache-sling-distribution-agent-sync-agents-factory}

**启用用户同步**

* 作者&#x200B;**上的**

   * 使用管理员权限登录
   * 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * 找到`Apache Sling Distribution Agent - Sync Agents Factory`

      * 选择现有配置，以便打开它进行编辑（铅笔图标）
验证`name`： **`socialpubsync`**

      * 选中`Enabled`复选框
      * 选择`Save`

![Apache Sling分发代理](assets/chlimage_1-20.png)

### 2.创建授权用户 {#createauthuser}

**配置权限**

在步骤3中使用授权用户在Author上配置Sling分发。

* 每个Publish实例上的&#x200B;**&#x200B;**

   * 使用管理员权限登录
   * 访问[安全控制台](/help/sites-administering/security.md)

      * 例如，[https://localhost:4503/useradmin](https://localhost:4503/useradmin)

   * 创建用户

      * 例如，`usersync-admin`

   * 将此用户添加到&#x200B;**`administrators`**&#x200B;用户组
   * [将此用户的ACL添加到/home](#howtoaddacl)

      * 具有限制`rep:glob=*/activities/*`的`Allow jcr:all`

>[!CAUTION]
>
>必须创建新用户。
>
>* 分配的默认用户是&#x200B;**`admin`**。
>* 不使用`communities-user-admin user.`
>

#### 如何添加ACL {#addacls}

* 访问CRXDE Lite

   * 例如，[https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* 选择`/home`节点
* 在右窗格中，选择`Access Control`选项卡
* 要添加ACL项，请选择`+`按钮

   * **主体**： *搜索为用户同步创建的用户*
   * **类型**：`Allow`
   * **权限**： `jcr:all`
   * **限制** `rep:glob`： `*/activities/*`
   * 选择&#x200B;**确定**

* 选择&#x200B;**全部保存**

![添加ACL窗口](assets/chlimage_1-21.png)

另请参阅

* [访问权限管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* 疑难解答部分[在响应处理期间修改操作异常](#modify-operation-exception-during-response-processing)。

### 3. Granite分发Adobe — 加密的密码传输密钥提供程序 {#adobegraniteencpasswrd}

**配置权限**

在所有Publish实例上创建授权用户（即&#x200B;**`administrators`**&#x200B;用户组的成员）后，必须在Author上将该授权用户标识为具有将用户数据从Author同步到Publish的权限。

* 作者&#x200B;**上的**

   * 使用管理员权限登录
   * 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * 找到`com.adobe.granite.distribution.core.impl.CryptoDistributionTransportSecretProvider.name`
   * 要打开进行编辑，请选择现有配置（铅笔图标）
验证`property name`： **`socialpubsync-publishUser`**

   * 在步骤2中将用户名和密码设置为在Publish中创建的[授权用户](#createauthuser)

      * 例如，`usersync-admin`

![加密密码传输密钥提供程序](assets/chlimage_1-22.png)

### 4. Apache Sling分发代理 — 队列代理工厂 {#apache-sling-distribution-agent-queue-agents-factory}

**启用用户同步**

* 每个Publish实例上的&#x200B;**&#x200B;**：

   * 使用管理员权限登录
   * 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * 找到`Apache Sling Distribution Agent - Queue Agents Factory`

      * 要打开进行编辑，请选择现有配置（铅笔图标）
验证`Name`： `socialpubsync-reverse`

      * 选中`Enabled`复选框
      * 选择`Save`

   * 针对每个Publish实例&#x200B;**重复**

![队列代理工厂](assets/chlimage_1-23.png)

### 5. Adobe Social同步 — 观察者工厂差异 {#diffobserver}

**启用组同步**

* 每个Publish实例上的&#x200B;**&#x200B;**：

   * 使用管理员权限登录
   * 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * 找到&#x200B;**`Adobe Social Sync - Diff Observer Factory`**

      * 要打开进行编辑，请选择现有配置（铅笔图标）

        验证`agent name`： `socialpubsync-reverse`

      * 选中`Enabled`复选框
      * 选择`Save`

![比较观察者工厂](assets/screen-shot_2019-05-24at090809.png)

### 6. Apache Sling Distribution Trigger — 计划触发器工厂 {#apache-sling-distribution-trigger-scheduled-triggers-factory}

**（可选）修改轮询间隔**

默认情况下，作者每30秒轮询一次更改。 更改此间隔：

* 作者&#x200B;**上的**

   * 使用管理员权限登录
   * 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * 找到`Apache Sling Distribution Trigger - Scheduled Triggers Factory`

      * 要打开进行编辑，请选择现有配置（铅笔图标）

         * 验证`Name`： `socialpubsync-scheduled-trigger`

      * 将`Interval in Seconds`设置为所需的间隔
      * 选择`Save`

![计划触发器工厂](assets/chlimage_1-24.png)

## 为多个Publish实例配置 {#configure-for-multiple-publish-instances}

默认配置是单个Publish实例。 由于启用用户同步的原因是同步多个Publish实例，例如对于发布场，必须将额外的Publish实例添加到同步代理工厂。

### 7. Apache Sling分发代理 — 同步代理工厂 {#apache-sling-distribution-agent-sync-agents-factory-1}

**添加Publish实例：**

* 作者&#x200B;**上的**

   * 使用管理员权限登录
   * 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * 找到`Apache Sling Distribution Agent - Sync Agents Factory`

      * 要打开进行编辑，请选择现有配置（铅笔图标）
验证`Name`： `socialpubsync`

![同步代理工厂](assets/chlimage_1-25.png)

* **导出程序终结点**
每个Publish实例都应该有一个导出程序端点。 例如，如果有2个Publish实例localhost：4503和4504，则应该有两个条目：

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **导入程序端点**
每个Publish实例都应该有一个导入程序端点。 例如，如果有2个Publish实例localhost：4503和4504，则应该有两个条目：

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* 选择`Save`

### 8. AEM Communities用户同步侦听器 {#aem-communities-user-sync-listener}

**（可选）同步其他JCR节点**

如果存在要在多个Publish实例之间同步的自定义数据，则：

* 每个Publish实例上的&#x200B;**&#x200B;**：

   * 使用管理员权限登录
   * 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如，`https://localhost:4503/system/console/configMgr`

   * 找到`AEM Communities User Sync Listener`
   * 要打开进行编辑，请选择现有配置（铅笔图标）
验证`Name`： `socialpubsync-scheduled-trigger`

![AEM Communities用户同步侦听器](assets/chlimage_1-26.png)

* **节点类型**
这是已同步的节点类型的列表。 必须在此处列出sling：Folder以外的任何节点类型（sling：folder单独处理）。
要同步的节点类型的默认列表：

   * rep：User
   * nt:unstructured
   * nt：resource

* **可忽略的属性**
这是如果检测到任何更改将被忽略的属性的列表。 对这些属性的更改可能会作为其他更改的副作用而同步（因为同步始终在节点级别），但是对这些属性的更改本身不会触发同步。
要忽略的默认属性：

   * cq:lastModified

* **可忽略的节点**
同步期间被忽略的子路径。 这些子路径下的任何内容都不会随时同步。
要忽略的默认节点：

   * .tokens
   * 系统

* **分布式文件夹**
大多数sling：Folders被忽略，因为不需要同步。 这里列出了少数例外。
要同步的默认文件夹

   * 区段/得分
   * 社交/关系
   * 活动

### 9.唯一Sling ID {#unique-sling-id}

>[!CAUTION]
>
>如果Sling ID在两个或更多Publish实例之间匹配，则用户组同步失败。

如果发布场中的多个Publish实例的Sling ID相同，则用户组不会同步。

要验证所有Sling ID值是否不同，请在每个Publish实例中执行以下操作：

1. 浏览到`http://<host>:<port>/system/console/status-slingsettings`
1. 检查&#x200B;**Sling ID**&#x200B;的值

![检查Sling ID的值](assets/chlimage_1-27.png)

如果Publish实例的Sling ID与任何其他Publish实例的Sling ID匹配，则：

1. 停止具有匹配Sling ID的某个Publish实例
1. 在crx-quickstart/launchpad/felix目录中

   * 搜索并删除名为&#x200B;*sling.id.file*&#x200B;的文件

      * 例如，在Linux®系统上：

        `rm -i $(find . -type f -name sling.id.file)`

      * 例如，在Windows系统上：

        `use windows explorer and search for *sling.id.file*`

1. 启动Publish实例

   * 启动时，会为其分配一个新的Sling ID

1. 验证&#x200B;**Sling ID**&#x200B;现在是否是唯一的

重复这些步骤，直到所有Publish实例都具有唯一的Sling ID。

## Vault Package Builder工厂 {#vault-package-builder-factory}

要使更新正确同步，必须修改用于用户同步的Vault包生成器：

* 在每个AEM Publish实例上
* 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* 找到`Apache Sling Distribution Packaging - Vault Package Builder Factory`

   * `Builder name: socialpubsync-vlt`

* 选择编辑图标
* 添加两个`Package Node Filters`：

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* 策略处理：

   * 要使用新节点覆盖现有rep：policy节点，请添加第三个包过滤器：

      * `/home/users|+.*/rep:policy`

   * 要防止策略被分发，请设置

      * `Acl Handling:` `IGNORE`

![保险库包生成器工厂](assets/vault-package-builder-factory.png)

## 当……发生时 {#what-happens-when}

### 在Publish上用户自行注册或编辑个人资料 {#user-self-registers-or-edits-profile-on-publish}

根据设计，在发布环境（自注册）中创建的用户和配置文件不会显示在创作环境中。

当拓扑是[发布场](/help/sites-deploying/recommended-deploys.md#tarmk-farm)并且已正确配置用户同步时，将使用Sling分发跨发布场同步&#x200B;*用户*&#x200B;和&#x200B;*用户配置文件*。

### 用户或用户组是使用安全控制台创建的 {#users-or-user-groups-are-created-using-security-console}

根据设计，在发布环境中创建的用户数据不会出现在创作环境中，反之亦然。

当使用[用户管理和安全性](/help/sites-administering/security.md)控制台在发布环境中添加新用户时，如有必要，用户同步会将新用户及其组成员资格同步到其他Publish实例。 用户同步还会同步通过安全控制台创建的用户组。

## 疑难解答 {#troubleshooting}

### 如何让用户同步脱机 {#how-to-take-user-sync-offline}

若要使用户同步脱机，要[删除Publish实例](#how-to-remove-a-publish-instance)或[手动同步数据](#manually-syncing-users-and-user-groups)，分发队列必须为空且静默。

检查分发队列的状态：

* 对于作者：

   * 使用[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)

      * 在`/var/sling/distribution/packages`中查找条目

         * 使用模式`distrpackage_*`命名的文件夹节点

   * 使用[包管理器](/help/sites-administering/package-manager.md)

      * 查找挂起的包（尚未安装）

         * 使用模式`socialpubsync-vlt*`命名
         * 由`communities-user-admin`创建

当分发队列为空时，禁用用户同步：

* 在作者上

   * *取消选中*针对[Apache Sling分发代理 — 同步代理工厂](#apache-sling-distribution-agent-sync-agents-factory)的`Enabled`复选框

完成任务后，要重新启用用户同步，请执行以下操作：

* 在作者上

   * 选中[Apache Sling分发代理 — 同步代理工厂](#apache-sling-distribution-agent-sync-agents-factory)的`Enabled`复选框

### 使用同步诊断 {#user-sync-diagnostics}

用户同步诊断是一种检查配置并尝试识别任何问题的工具。

在作者中，只需从主控制台导航到&#x200B;**工具、操作、诊断、用户同步诊断。**

只需进入“User Sync Diagnostics（用户同步诊断）”控制台即可显示结果。

这是未启用用户同步时显示的内容：

![警告：未启用用户同步诊断](assets/chlimage_1-28.png)

#### 如何对Publish实例运行诊断 {#how-to-run-diagnostics-for-publish-instances}

从创作环境运行诊断时，通过/失败结果包括一个[INFO]部分，其中显示已配置的Publish实例列表以供确认。

列表中包括运行该实例诊断的每个Publish实例的URL。 已将URL参数`syncUser`附加到诊断URL，其值设置为在[步骤2](#createauthuser)中创建的&#x200B;*授权同步用户*。

**注意**：在启动该URL之前，*授权同步用户*&#x200B;必须已登录到该Publish实例。

Publish实例的![诊断](assets/chlimage_1-29.png)

### 未正确添加配置 {#configuration-improperly-added}

当用户同步失败时，最常见的问题是添加了&#x200B;*其他配置*。 相反，*existing *default配置应该已&#x200B;*编辑*。

以下是有关已编辑的默认配置应如何显示在Web控制台中的视图。 如果出现多个实例，则应删除添加的配置。

#### （作者）一个Apache Sling分发代理 — 同步代理工厂 {#author-one-apache-sling-distribution-agent-sync-agents-factory}

![已编辑，Web控制台中的默认配置视图](assets/chlimage_1-30.png)

#### （作者）一个Apache Sling分发传输凭据 — 基于用户凭据的DistributionTransportSecretProvider {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![已编辑，Web控制台中的默认配置视图](assets/chlimage_1-31.png)

#### (Publish)一个Apache Sling分发代理 — 队列代理工厂 {#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![已编辑，Web控制台中的默认配置视图](assets/chlimage_1-32.png)

#### (Publish)一个Adobe Social同步 — 观察者工厂差异 {#publish-one-adobe-social-sync-diff-observer-factory}

![已编辑，Web控制台中的默认配置视图](assets/chlimage_1-33.png)

#### （作者）一个Apache Sling Distribution Trigger — 计划触发器工厂 {#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![已编辑，Web控制台中的默认配置视图](assets/chlimage_1-34.png)

### 处理响应期间修改操作异常 {#modify-operation-exception-during-response-processing}

如果日志中显示以下内容：

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

然后验证节[2。 已正确遵循创建授权用户](#createauthuser)的操作。

本节介绍如何创建存在于所有Publish实例上的授权用户，以及在创作实例的“机密提供程序”OSGi配置中标识这些用户。 默认情况下，用户为`admin`。

授权用户应成为&#x200B;**`administrators`**&#x200B;用户组的成员，且不应更改该组的权限。

授权用户对所有Publish实例应明确具有以下权限和限制：

| **path** | **jcr：all** | **rep：glob** |
|---|---|---|
| /home | X | &#42;/活动/&#42; |
| /home/users | X | &#42;/活动/&#42; |
| /home/groups | X | &#42;/活动/&#42; |

作为`administrators`组的成员，授权用户在所有Publish实例上应具有以下权限：

| **path** | **jcr：all** | **jcr：read** | **rep：write** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### 用户组同步失败 {#user-group-sync-failed}

如果Sling ID在两个或更多Publish实例之间匹配，则用户组同步失败。

请参阅第[9部分。 唯一的Sling ID](#unique-sling-id)

### 手动同步用户和用户组 {#manually-syncing-users-and-user-groups}

* 在存在用户和用户组的Publish实例上：

   * [如果启用，则禁用用户同步](#how-to-take-user-sync-offline)
   * [创建包](/help/sites-administering/package-manager.md#creating-a-new-package)/`/home`

      * 编辑包时

         * 筛选器选项卡：添加筛选器：根路径： `/home`
         * 高级选项卡： AC处理： `Overwrite`

   * [导出资源包](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)

* 在其他Publish实例上：

   * [导入资源包](/help/sites-administering/package-manager.md#installing-packages)

要配置或启用用户同步，请转到步骤1：[Apache Sling分发代理 — 同步代理工厂](#apache-sling-distribution-agent-sync-agents-factory)

### 当Publish实例变得不可用时 {#when-a-publish-instance-becomes-unavailable}

当Publish实例变得不可用时，如果它将来重新联机，则不应将其删除。 更改将排队等候Publish实例，当它重新联机时，将处理更改。

如果Publish实例从未重新联机，或者永久脱机，则必须将其删除，因为队列累积会导致在创作环境中显着占用磁盘空间。

当Publish实例关闭时，创作日志会出现与以下内容类似的异常：

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### 如何删除Publish实例 {#how-to-remove-a-publish-instance}

要从[Apache Sling分发代理 — 同步代理工厂](#apache-sling-distribution-agent-sync-agents-factory)中删除Publish实例，分发队列必须为空且安静。

* 对于作者：

   * [使用户同步脱机](#how-to-take-user-sync-offline)
   * 执行[步骤7](#apache-sling-distribution-agent-sync-agents-factory)以从两个服务器列表中删除Publish实例：

      * `Exporter Endpoints`
      * `Importer Endpoints`

   * 重新启用用户同步

      * 选中[Apache Sling分发代理 — 同步代理工厂](#apache-sling-distribution-agent-sync-agents-factory)的`Enabled`复选框
