---
title: 复制
description: 了解如何在Adobe Experience Manager中配置和监控复制代理。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
docset: aem65
feature: Configuring
exl-id: 09943de5-8d62-4354-a37f-0521a66b4c49
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '3363'
ht-degree: 1%

---

# 复制{#replication}

复制代理在Adobe Experience Manager (AEM)中占有重要地位，作为一种机制，用于：

* [Publish（激活）](/help/sites-authoring/publishing-pages.md#activatingcontent)内容从创作环境到Publish环境。
* 明确刷新Dispatcher缓存中的内容。
* 将用户输入（例如表单输入）从Publish环境返回到创作环境（在创作环境的控制下）。

请求[已排队](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler)到相应的代理以进行处理。

>[!NOTE]
>
>不会在Author实例和Publish实例之间复制用户数据（用户、用户组和用户配置文件）。
>
>对于多个Publish实例，启用[用户同步](/help/sites-administering/sync.md)后，用户数据将通过Sling分发。

## 从“创作”复制到Publish {#replicating-from-author-to-publish}

复制到Publish实例或Dispatcher需要执行几个步骤：

* 作者请求发布（激活）某些内容；这可以由手动请求或预配置的自动触发器启动。
* 请求将传递到相应的默认复制代理；一个环境可以有多个默认代理，这些代理始终为此类操作选择。
* 复制代理将内容“打包”并放置在复制队列中。
* 在“网站”选项卡中，为各个页面设置了[彩色状态指示器](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus)。
* 内容将从队列中提升，并使用配置的协议传输到Publish环境；通常为HTTP。
* Publish环境中的servlet接收请求并发布接收的内容；默认servlet为`https://localhost:4503/bin/receive`。

* 可以配置多个创作和Publish环境。

![chlimage_1-21](assets/chlimage_1-21.png)

### 从Publish复制到创作 {#replicating-from-publish-to-author}

某些功能允许用户在Publish实例上输入数据。

有时候，需要执行一种称为反向复制的复制，将此数据返回到创作环境，然后再将该数据重新分发到其他Publish环境。 出于安全考虑，必须严格控制从Publish到创作环境的任何流量。

反向复制使用Publish环境中引用“创作”环境的代理。 此代理将数据放入发件箱。 此发件箱与创作环境中的复制侦听器匹配。 监听器轮询发件箱以收集输入的任何数据，然后根据需要进行分发。 这可确保创作环境控制所有流量。

在其他情况下，例如对于Communities功能（例如，论坛、博客、评论和评论），在Publish环境中输入的用户生成内容(UGC)数量很难使用复制在AEM实例之间有效同步。

AEM [Communities](/help/communities/overview.md)从未对UGC使用复制。 社区部署需要用于UGC的公用存储（请参阅[社区内容存储](/help/communities/working-with-srp.md)）。

### 复制 — 开箱即用 {#replication-out-of-the-box}

AEM的标准安装中包含的We-Retail网站可用于说明复制。

要遵循此示例并使用默认复制代理，请[安装AEM](/help/sites-deploying/deploy.md)：

* 端口`4502`上的创作环境
* 端口`4503`上的Publish环境

>[!NOTE]
>
>默认启用：
>
>* 创作代理：默认代理（发布）
>
>默认情况下有效禁用(自AEM 6.1起)：
>
>* 创作代理：反向复制代理(publish_reverse)
>* Publish上的代理：反向复制（发件箱）
>
>要检查代理或队列的状态，请使用&#x200B;**工具**&#x200B;控制台。
>请参阅[监视复制代理](#monitoring-your-replication-agents)。

#### 复制(创作到Publish) {#replication-author-to-publish}

1. 导航到创作环境上的支持页面。
   **https://localhost:4502/content/we-retail/us/en/experience.html** `<pi>`
1. 编辑页面，以便添加新文本。
1. **激活页面**，以便发布更改。
1. 在Publish环境中打开支持页面：
   **https://localhost:4503/content/we-retail/us/en/experience.html**
1. 您现在可以看到您在“创作”中输入的更改。

此操作将从创作环境中进行，方法是：

* **默认代理（发布）**
此代理会将内容复制到默认的Publish实例。
可从创作环境的“工具”控制台访问此的详细信息（配置和日志）；或：
  `https://localhost:4502/etc/replication/agents.author/publish.html`。

#### 复制代理 — 现成可用 {#replication-agents-out-of-the-box}

标准AEM安装中提供了以下代理：

* [默认代理](#replication-author-to-publish)
用于从Author复制到Publish。

* Dispatcher Flush
用于管理Dispatcher缓存。 有关详细信息，请参阅[使创作环境中的Dispatcher缓存失效](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=zh-Hans#invalidating-dispatcher-cache-from-the-authoring-environment)和[使发布实例中的Dispatcher缓存失效](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=zh-Hans#invalidating-dispatcher-cache-from-a-publishing-instance)。

* [反向复制](#reverse-replication-publish-to-author)
用于从Publish复制到创作。 反向复制不用于Communities功能，例如论坛、博客和评论。 由于未启用发件箱，因此该功能实际上已被禁用。 使用反向复制需要自定义配置。

* 静态代理
这是一个“将节点的静态表示存储在文件系统中的代理”。
例如，在默认设置下，内容页面和DAM资源作为HTML或相应的资源格式存储在`/tmp`下。 查看配置的`Settings`和`Rules`选项卡。
这是请求的，以便当直接从应用程序服务器请求页面时，可以看到内容。 这是一个专用代理，（可能）在大多数情况下不需要它。

## 复制代理 — 配置参数 {#replication-agents-configuration-parameters}

从“工具”控制台配置复制代理时，对话框中提供了四个选项卡：

### 设置 {#settings}

* **名称**

  复制代理的唯一名称。

* **描述**

  此复制代理用途的描述。

* **已启用**

  指示是否启用复制代理。

  当代理处于&#x200B;**启用**&#x200B;状态时，队列显示为：

   * 正在处理项目时&#x200B;**活动**。
   * 队列为空时&#x200B;**空闲**。
   * 当项目在队列中但无法处理（例如，接收队列被禁用）时，**已阻止**。

* **序列化类型**

  序列化的类型：

   * **默认值**：设置是否自动选择代理。
   * **Dispatcher刷新**：如果要使用代理刷新Dispatcher缓存，请选择此选项。

* **重试延迟**

  如果遇到问题，两次重试之间的延迟（等待时间，以毫秒为单位）。

  默认： `60000`

* **代理用户ID**

  根据环境，代理会使用此用户帐户来：

   * 从创作环境收集内容并对其进行打包
   * 在Publish环境中创建和编写内容

  将此字段留空以使用系统用户帐户（在sling中定义为管理员用户的帐户；默认情况下为`admin`）。

  >[!CAUTION]
  >
  >对于创作环境上的代理，此帐户&#x200B;*必须*&#x200B;对要复制的所有路径具有读取访问权限。

  >[!CAUTION]
  >
  >对于Publish环境中的代理，此帐户&#x200B;*必须*&#x200B;具有复制内容所需的创建/写入权限。

  >[!NOTE]
  >
  >这可用作选择复制特定内容的机制。

* **日志级别**

  指定用于日志消息的详细级别。

   * `Error`：仅记录错误
   * `Info`：记录错误、警告和其他信息性消息
   * `Debug`：在消息中使用高级别的详细信息，主要用于调试目的

  默认： `Info`

* **用于反向复制**

  指示此代理是否用于反向复制；将用户输入从Publish返回到创作环境。

* **别名更新**

  选择此选项可允许向Dispatcher发送别名或虚名路径失效请求。 另请参阅[配置Dispatcher Flush代理](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent)。

#### 传输 {#transport}

* **URI**

  这会指定目标位置的接收servlet。 特别是，您可以在此处指定目标实例的主机名（或别名）和上下文路径。

  例如：

   * 默认代理可能会复制到`https://localhost:4503/bin/receive`
   * Dispatcher Flush代理可能会复制到`https://localhost:8000/dispatcher/invalidate.cache`

  此处指定的协议（HTTP或HTTPS）确定传输方法。

  对于Dispatcher Flush代理，仅在您使用基于路径的虚拟主机条目来区分场时使用URI属性，并使用此字段来定位要失效的场。 例如，场 #1 的虚拟主机为 `www.mysite.com/path1/*`，场 #2 的虚拟主机为 `www.mysite.com/path2/*`。您可以使用URL `/path1/invalidate.cache`定位第一个场，使用`/path2/invalidate.cache`定位第二个场。

* **用户**

  用于访问目标的帐户的用户名。

* **密码**

  用于访问目标的帐户的密码。

* **NTLM域**

  NTML身份验证的域。

* **NTLM主机**

  用于NTML身份验证的主机。

* **启用宽松SSL**

  如果希望接受自认证的SSL证书，则启用。

* **允许过期的证书**

  如果希望接受过期的SSL证书，则启用此选项。

#### 代理 {#proxy}

仅在需要代理时才需要以下设置：

* **代理主机**

  用于传输的代理的主机名。

* **代理端口**

  代理的端口。

* **代理用户**

  要使用的帐户的用户名。

* **代理密码**

  要使用的帐户的密码。

* **代理NTLM域**

  代理NTLM域。

* **代理NTLM主机**

  代理NTLM域。

#### 扩展 {#extended}

* **接口**

  您可以在此定义要绑定的套接字接口。

  这会设置创建连接时要使用的本地地址。 如果未设置，则使用默认地址。 这对于指定要在多宿主或群集系统上使用的接口非常有用。

* **HTTP方法**

  要使用的HTTP方法。

  对于Dispatcher Flush代理，这几乎总是GET，不应更改(POST是另一个可能的值)。

* **HTTP标头**

  它们用于Dispatcher Flush代理，并指定必须刷新的元素。

  对于Dispatcher Flush代理，不需要更改三个标准条目：

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

  在刷新手柄或路径时，将酌情使用这些参数来指示要使用的操作。 子参数是动态的：

   * `{action}`表示复制操作

   * `{path}`表示路径

  与请求相关的路径/操作将替换它们，因此无需“硬编码”：

  >[!NOTE]
  >
  >如果您在推荐的默认上下文以外的其他上下文中安装了AEM，则必须在HTTP标头中注册该上下文。 例如：
  >`CQ-Handle:/<*yourContext*>{path}`

* **关闭连接**

  启用，以便您可以在每次请求后关闭连接。

* **连接超时**

  尝试建立连接时应用的超时（以毫秒为单位）。

* **套接字超时**

  建立连接后等待流量时应用的超时（以毫秒为单位）。

* **协议版本**

  协议的版本。 例如，`1.0`表示HTTP/1.0。

#### 触发器 {#triggers}

这些设置用于定义自动复制的触发器：

* **忽略默认值**

  如果选中，代理将从默认复制中排除；这意味着如果内容作者发出复制操作，则不会使用代理。

* **修改**

  此处，修改页面时，此代理的复制操作将自动触发。 用于Dispatcher Flush代理，但也用于反向复制。

* **在分发时**

  如果选中，代理会在修改内容时自动复制标记为分发的任何内容。

* 已达到&#x200B;**开启/结束时间**

  当为页面定义的时间或超时发生时，将触发自动复制（根据需要激活或停用页面）。 这主要用于Dispatcher Flush代理。

* 接收时&#x200B;**&#x200B;**

  如果选中，代理将在收到复制事件时进行链式复制。

* **无状态更新**

  选中后，代理不会强制复制状态更新。

* **无版本控制**

  选中后，代理不会强制活动页面的版本控制。

## 配置复制代理 {#configuring-your-replication-agents}

有关使用MSSL将复制代理连接到Publish实例的信息，请参阅[使用双向SSL复制](/help/sites-deploying/mssl-replication.md)。

### 从创作环境配置复制代理 {#configuring-your-replication-agents-from-the-author-environment}

在创作环境的“工具”选项卡中，您可以配置驻留在创作环境（**个创作代理**）或PublishPublish环境（**个创作代理**）中的复制代理。 以下过程说明了为“创作”环境配置代理，但可用于两者。

>[!NOTE]
>
>当Dispatcher处理创作或Publish实例的HTTP请求时，复制代理发出的HTTP请求必须包含PATH标头。 除了以下过程之外，还必须将PATH标头添加到Dispatcher的客户端标头列表中。 请参阅[/clientheaders （客户端标头）](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hans#specifying-the-http-headers-to-pass-through-clientheaders)。
>

1. 访问AEM中的&#x200B;**工具**&#x200B;选项卡。
1. 单击&#x200B;**复制**（左窗格打开文件夹）。
1. 双击作者&#x200B;**上的**&#x200B;代理（左窗格或右窗格）。
1. 单击相应的代理名称（链接）以显示有关该代理的详细信息。
1. 单击&#x200B;**编辑**&#x200B;以打开配置对话框：

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. 提供的值应足以进行默认安装。 如果进行了更改，请单击&#x200B;**确定**&#x200B;以保存它们（有关各个参数的信息，请参阅[复制代理 — 配置参数](#replication-agents-configuration-parameters)）。

>[!NOTE]
>
>AEM的标准安装将`admin`指定为默认复制代理中传输凭据的用户。
>
>这应该更改为站点特定的复制用户帐户，该帐户具有复制所需路径的权限。

### 配置反向复制 {#configuring-reverse-replication}

反向复制用于将在Publish实例上生成的用户内容取回创作实例。 这通常用于调查表和登记表等功能。

出于安全原因，大多数网络拓扑不允许&#x200B;*来自*&#x200B;的“非军事区域”(将外部服务公开给不受信任网络（如Internet）的子网络)的连接。

由于Publish环境通常位于DMZ中，因此要将内容返回到“创作”环境，必须从“创作”实例启动连接。 此操作可通过以下方式完成：

* 内容所在的Publish环境中的&#x200B;*发件箱*。
* 创作环境中的代理（发布），定期轮询发件箱以获取新内容。

>[!NOTE]
>
>对于AEM [Communities](/help/communities/overview.md)，复制不用于Publish实例上用户生成的内容。 查看[社区内容存储](/help/communities/working-with-srp.md)。

为此，您需要：

**创作环境中的反向复制代理** — 充当活动组件，从Publish环境中的发件箱中收集信息：

如果要使用反向复制，请确保已激活此代理。

![chlimage_1-23](assets/chlimage_1-23.png)

**Publish环境中的反向复制代理（发件箱）** — 被动元素充当“发件箱”。 用户输入放置在此处，代理从此处在创作环境中收集用户输入。

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### 为多个Publish实例配置复制 {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>仅复制内容 — 不复制用户数据（用户、用户组和用户配置文件）。
>
>若要在多个Publish实例间同步用户数据，请启用[用户同步](/help/sites-administering/sync.md)。

安装后，已配置默认代理以将内容复制到本地主机的端口4503上运行的Publish实例。

要为其他Publish实例配置内容复制，请创建和配置新的复制代理：

1. 在AEM中打开&#x200B;**工具**&#x200B;选项卡。
1. 在左侧面板中选择&#x200B;**复制**，然后选择作者上的&#x200B;**代理**。
1. 选择&#x200B;**新建……**。
1. 设置&#x200B;**标题**&#x200B;和&#x200B;**名称**，然后选择&#x200B;**复制代理**。
1. 单击&#x200B;**创建**，以便创建代理。
1. 双击新代理项目，配置面板将打开。
1. 单击&#x200B;**编辑** - **代理设置**&#x200B;对话框打开 — **序列化类型**&#x200B;已定义为默认值，必须保持此状态。

   * 在&#x200B;**设置**&#x200B;选项卡中：

      * 激活&#x200B;**已启用**。
      * 输入&#x200B;**描述**。
      * 将&#x200B;**重试延迟**&#x200B;设置为`60000`。

      * 将&#x200B;**序列化类型**&#x200B;保留为`Default`。

   * 在&#x200B;**传输**&#x200B;选项卡中：

      * 输入新Publish实例所需的URI；例如，

        `https://localhost:4504/bin/receive`。

      * 输入用于复制的站点特定用户帐户。
      * 您可以根据需要配置其他参数。

1. 单击&#x200B;**确定**。

然后，您可以通过更新创作环境中的页面，然后发布页面来测试该操作。

更新将显示在已如上配置的所有Publish实例上。

如果您遇到任何问题，可以检查创作实例上的日志。 根据所需的详细级别，您还可以使用如上所述的&#x200B;**代理设置**&#x200B;对话框将&#x200B;**日志级别**&#x200B;设置为`Debug`。

>[!NOTE]
>
>这可以结合使用[代理用户ID](#agentuserid)选择其他内容以复制到各个Publish环境。 对于每个Publish环境：
>
>1. 配置复制代理以复制到该Publish环境。
>1. 配置用户帐户；具有读取复制到该特定Publish环境的内容所需的访问权限。
>1. 将用户帐户指定为复制代理的&#x200B;**代理用户ID**。
>

### 配置Dispatcher Flush代理 {#configuring-a-dispatcher-flush-agent}

默认代理包含在安装中。 但是，仍需要特定配置，如果您定义新代理，同样需要该配置：

1. 在AEM中打开&#x200B;**工具**&#x200B;选项卡。
1. 单击&#x200B;**部署**。
1. 选择&#x200B;**复制**，然后选择Publish **上的**&#x200B;代理。
1. 双击&#x200B;**Dispatcher Flush**&#x200B;项以打开概述。
1. 单击&#x200B;**编辑** - **代理设置**&#x200B;对话框打开：

   * 在&#x200B;**设置**&#x200B;选项卡中：

      * 激活&#x200B;**已启用**。
      * 输入&#x200B;**描述**。
      * 将&#x200B;**序列化类型**&#x200B;保留为`Dispatcher Flush`，或者在创建代理时将其设置为此类型。

      * （可选）选择&#x200B;**别名更新**&#x200B;以启用对Dispatcher的别名或虚名路径失效请求。

   * 在&#x200B;**传输**&#x200B;选项卡中：

      * 输入新Publish实例所需的URI；例如，

        `https://localhost:80/dispatcher/invalidate.cache`。

      * 输入用于复制的站点特定用户帐户。
      * 您可以根据需要配置其他参数。

   对于Dispatcher Flush代理，仅在您使用基于路径的虚拟主机条目来区分场时使用URI属性，并使用此字段来定位要失效的场。 例如，场 #1 的虚拟主机为 `www.mysite.com/path1/*`，场 #2 的虚拟主机为 `www.mysite.com/path2/*`。您可以使用URL `/path1/invalidate.cache`定位第一个场，使用`/path2/invalidate.cache`定位第二个场。

   >[!NOTE]
   >
   >如果您在非推荐的默认上下文中安装了AEM，请在&#x200B;**扩展**&#x200B;选项卡中配置[HTTP标头](#extended)。

1. 单击&#x200B;**确定**。
1. 返回&#x200B;**工具**&#x200B;选项卡，从此处，您可以&#x200B;**激活** **Dispatcher Flush**&#x200B;代理(&lbrace;Publish上的&#x200B;**个代理**)。

**Dispatcher Flush**&#x200B;复制代理在创作实例上不是活动的。 您可以使用等效的URI在Publish环境中访问同一页面；例如，`https://localhost:4503/etc/replication/agents.publish/flush.html`。

### 控制对复制代理的访问 {#controlling-access-to-replication-agents}

通过使用`etc/replication`节点上的用户和/或组页面权限，可以控制对用于配置复制代理的页面的访问。

>[!NOTE]
>
>设置此类权限不会影响用户复制内容（例如，从网站控制台或Sidekick选项复制）。 在复制页面时，复制框架不使用当前用户的“用户会话”来访问复制代理。

### 从CRXDE Lite配置复制代理 {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>仅支持在`/etc/replication`存储库位置中创建复制代理。 要正确处理关联的ACL ，需要此项。 在树的其他位置创建复制代理可能会导致未经授权的访问。

可以使用CRXDE Lite配置复制代理的各种参数。

如果导航到`/etc/replication`，则可以看到以下三个节点：

* `agents.author`
* `agents.publish`
* `treeactivation`

两个`agents`保存有关相应环境的配置信息，并且仅在环境运行时处于活动状态。 例如，`agents.publish`仅在Publish环境中使用。 以下屏幕截图显示了创作环境中的Publish代理(随AEM WCM提供)：

![chlimage_1-24](assets/chlimage_1-24.png)

## 监视复制代理 {#monitoring-your-replication-agents}

监视复制代理：

1. 访问AEM中的&#x200B;**工具**&#x200B;选项卡。
1. 单击&#x200B;**复制**。
1. 双击相应环境（左窗格或右窗格）的代理链接。 例如，作者&#x200B;**上的**&#x200B;代理。

   生成的窗口将显示创作环境的所有复制代理的概述，包括其目标和状态。

1. 单击相应的代理名称（链接）以显示有关该代理的详细信息：

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   在这里，您可以执行以下操作：

   * 查看代理是否已启用。
   * 查看任何复制的目标。
   * 查看复制队列是否处于活动状态（已启用）。
   * 查看队列中是否有任何项目。
   * **刷新**&#x200B;或&#x200B;**清除**&#x200B;以更新队列条目的显示。 这有助于您看到项目进入和离开队列。

   * **查看日志**&#x200B;以访问复制代理执行的任何操作的日志。
   * **测试目标实例的连接**。
   * 如有必要，对任何队列项目&#x200B;**强制重试**。

   >[!CAUTION]
   >
   >请勿对Publish实例上的反向复制发件箱使用“测试连接”链接。
   >
   >
   >如果为Outbox队列执行复制测试，则使用每次反向复制重新处理早于测试复制的任何项目。
   >
   >
   >如果此类项目存在于队列中，则可通过以下XPath JCR查询找到它们，应将其删除。
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## 批量复制 {#batch-replication}

批量复制不会复制单个页面或资产，而是等待触发两者的第一个阈值（基于时间或大小）。

然后，它将所有复制项目打包到一个包中，然后作为一个文件复制到发布服务器。

Publisher将解压缩所有项目，保存它们并向作者报告。

### 配置批量复制 {#configuring-batch-replication}

1. 转到`http://serveraddress:serverport/siteadmin`
1. 按屏幕上方的&#x200B;**[!UICONTROL 工具]**&#x200B;图标
1. 从左侧导航栏中，转到&#x200B;**[!UICONTROL 复制 — 作者上的代理]**，然后双击&#x200B;**[!UICONTROL 默认代理]**。
   * 您还可以通过直接转到`http://serveraddress:serverport/etc/replication/agents.author/publish.html`访问默认的Publish复制代理
1. 按复制队列上方的&#x200B;**[!UICONTROL 编辑]**&#x200B;按钮。
1. 在以下窗口中，转到&#x200B;**[!UICONTROL 批处理]**&#x200B;选项卡：
   ![批次复制](assets/batchreplication.png)
1. 配置代理。

### 参数 {#parameters}

* `[!UICONTROL Enable Batch Mode]` — 启用或禁用批处理复制模式
* `[!UICONTROL Max Wait Time]` — 启动批次请求之前的最长等待时间（以秒为单位）。 默认值为2秒。
* `[!UICONTROL Trigger Size]` — 在此大小限制时开始批量复制

## 其他资源 {#additional-resources}

有关疑难解答的详细信息，请参阅[Troubleshooting Replication](/help/sites-deploying/troubleshoot-rep.md)页。
