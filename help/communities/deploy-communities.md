---
title: 部署社区
seo-title: Deploying Communities
description: 如何部署AEM Communities
seo-description: How to deploy AEM Communities
uuid: 18d9b424-004d-43b2-968a-318e27a93759
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: c8d7355f-5a70-40d1-bf22-62fab8002ea0
docset: aem65
exl-id: 5b3d572d-e73d-4626-b664-c985949469c9
source-git-commit: 07f8a9f629122102d30676926b225d57e542147d
workflow-type: tm+mt
source-wordcount: '1914'
ht-degree: 1%

---

# 部署社区 {#deploying-communities}

## 前提条件 {#prerequisites}

* [AEM 6.5平台](/help/sites-deploying/deploy.md)

* AEM Communities许可证

* 可选许可证：

   * [Adobe Analytics for Communities功能](/help/communities/analytics.md)
   * [MongoDB for MSRP](/help/communities/msrp.md)
   * [ASRP的Adobe云](/help/communities/asrp.md)

## 安装核对清单 {#installation-checklist}

**对于 [AEM平台](/help/sites-deploying/deploy.md#what-is-aem)**

* 安装最新版本 [AEM 6.5更新](#aem64updates)

* 如果不使用默认端口(4502、4503)，则 [配置复制代理](#replication-agents-on-author)
* [复制加密密钥](#replicate-the-crypto-key)
* 如果支持全球化， [设置自动翻译](/help/sites-administering/translation.md)
（为开发提供了示例设置）

**对于 [Communities功能](/help/communities/overview.md)**

* 如果部署 [发布场](/help/sites-deploying/recommended-deploys.md#tarmk-farm)， [标识主要发布者](#primary-publisher)

* [启用通道服务](#tunnel-service-on-author)
* [启用社交登录](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [配置Adobe Analytics](/help/communities/analytics.md)
* 设置 [默认电子邮件服务](/help/communities/email.md)
* 确定以下各项的选择 [共享UGC存储](/help/communities/working-with-srp.md) (**SRP**)

   * 如果MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [安装和配置MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [配置Solr](/help/communities/solr.md)
      * [选择MSRP](/help/communities/srp-config.md)
   * 如果关系数据库SRP [(DSRP)](/help/communities/dsrp.md)

      * [安装用于MySQL的JDBC驱动程序](#jdbc-driver-for-mysql)
      * [安装和配置MySQL for DSRP](/help/communities/dsrp-mysql.md)
      * [配置Solr](/help/communities/solr.md)
      * [选择DSRP](/help/communities/srp-config.md)
   * 如果AdobeSRP [(ASRP)](/help/communities/asrp.md)

      * 与您的客户代表合作进行配置
      * [选择ASRP](/help/communities/srp-config.md)
   * 如果JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * 不是共享的UGC存储：

         * 从不复制UGC
         * UGC仅在输入它的AEM实例或群集中可见

         * 默认值为JSRP
   对于 **[启用功能](/help/communities/overview.md#enablement-community)**

   * [安装和配置FFmpeg](/help/communities/ffmpeg.md)
   * [安装用于MySQL的JDBC驱动程序](#jdbc-driver-for-mysql)
   * [安装AEM Communities SCORM-Engine](#scorm-package)
   * [安装和配置用于启用的MySQL](/help/communities/mysql.md)





## 最新版本 {#latest-releases}

AEM 6.5 Communities GA包含Communities包。 了解AEM 6.5的更新 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities)，请参阅 [AEM 6.5发行说明](/help/release-notes/release-notes.md#communities-release-notes.html).

### AEM 6.5更新 {#aem-updates}

从AEM 6.4开始，对Communities的更新作为AEM累积修补程序包和Service Pack的一部分提供。

有关AEM 6.5的最新更新，请参阅 [Adobe Experience Manager 6.4累积修补程序包和Service Pack](https://helpx.adobe.com/cn/experience-manager/aem-releases-updates.html).

### 版本历史记录 {#version-history}

与AEM 6.4及更高版本一样，AEM Communities功能和修补程序是AEM Communities累积修补程序包和Service Pack的一部分。 因此，没有单独的功能包。

### 适用于MySQL的JDBC驱动程序 {#jdbc-driver-for-mysql}

有两个Communities功能使用MySQL数据库：

* 对象 [启用](/help/communities/enablement.md)：记录SCORM活动和学习者
* 对象 [DSRP](/help/communities/dsrp.md)：存储用户生成的内容(UGC)

必须单独获取和安装MySQL连接器。

必需的步骤包括：

1. 下载ZIP存档，从 [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * 版本必须>= 5.1.38

1. 提取mysql-connector-java-&lt;version>-bin.jar（捆绑）
1. 使用Web控制台安装和启动捆绑包：

   * 例如， https://localhost:4502/system/console/bundles
   * 选择 **`Install/Update`**
   * 浏览……以选择从下载的ZIP存档中提取的包
   * 检查 *oracle公司的MySQLcom.mysql.jdbc的JDBC驱动程序* 处于活动状态，如果未处于活动状态，则启动它（或检查日志）

1. 如果在配置JDBC之后在现有部署上进行安装，则通过从Web控制台重新保存JDBC配置来将JDBC重新绑定到新连接器：
   * 例如， https://localhost:4502/system/console/configMgr
   * 查找 `Day Commons JDBC Connections Pool` 配置
   * 选择以打开
   * 选择 `Save`

1. 对所有创作和发布实例重复步骤3和4

有关安装捆绑包的更多信息，请参阅 [Web控制台](/help/sites-deploying/web-console.md) 页面。

#### 示例：已安装MySQL连接器捆绑包 {#example-installed-mysql-connector-bundle}

![connect-bundle](assets/connector-bundle.png)

### SCORM包 {#scorm-package}

可共享内容对象参考模型(SCORM)是电子学习标准和规范的集合。 SCORM还定义如何将内容打包到可传输的ZIP文件中。

以下项需要AEM Communities SCORM引擎： [启用](/help/communities/overview.md#enablement-community) 功能。 AEM 6.5 Communities支持的Scorm包：

* [cq-social-scorm-package，版本2.3.7](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq640%2Fsocial%2Fscorm%2Fcq-social-scorm-2017-pkg) 包括 [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) 引擎。

**安装SCORM包**

1. 安装 [cq-social-scorm-package，版本2.3.7](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq640%2Fsocial%2Fscorm%2Fcq-social-scorm-2017-pkg)  包共享中的。
1. 下载 `/libs/social/config/scorm/database_scormengine_data.sql` 从cq实例并在mysql server中执行它以创建升级的scormEngineDB架构。
1. 添加 `/content/communities/scorm/RecordResults` 的CSRF过滤器中的“排除的路径”属性 `https://<hostname>:<port>/system/console/configMgr` 发布者的。


#### SCORM日志记录 {#scorm-logging}

安装完毕后，所有启用活动都会详细记录到系统控制台。

如果需要，可将的日志级别设置为WARN `RusticiSoftware.*` 包。

有关使用日志，请参阅 [使用审计记录和日志文件](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

### AEM高级MLS {#aem-advanced-mls}

对于SRP集合（MSRP或DSRP）以支持高级多语言搜索(MLS)，除了自定义架构和Solr配置之外，还需要新的Solr插件。 所有必需的项目都打包到一个可下载的zip文件中。

高级MLS下载（也称为“phasetwo”）可从Adobe存储库中获取：

* AEM-SOLR-MLS-phasetwo

   要获取高级MLS包，请参阅 [AEM高级MLS](deploy-communities.md#aem-advanced-mls) 在文档的“部署”部分中。

   * 版本1.2.40,2016年4月6日
   * 下载AEM-SOLR-MLS-phasetwo-1.2.40.zip

有关详细信息和安装信息，请访问 [Solr配置](/help/communities/solr.md) 用于SRP。

### 关于指向包共享的链接 {#about-links-to-package-share}

**AdobeAEM Cloud中可见的软件包**

此页上的包链接不需要正在运行的AEM实例，因为它们将在其上共享包 `adobeaemcloud.com`. 虽然可以查看包，但是 `Install` 按钮用于将包安装到托管Adobe的站点。 如果要在本地AEM实例上安装，请选择 `Install` 将导致错误。

**如何在本地AEM实例上安装**

要安装中显示的包，请执行以下操作 `adobeaemcloud.com` 在本地AEM实例上，必须首先将软件包下载到本地磁盘：

* 选择 **资产** 选项卡
* 选择 **下载到磁盘**

在本地AEM实例上，使用包管理器(例如 [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/))，以上传到本地AEM包存储库。

或者，使用本地AEM实例中的包共享访问包(例如， [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/))，则 `Download` 按钮将下载到本地AEM实例的包存储库。

进入本地AEM实例的包存储库后，使用包管理器安装包。

有关详细信息，请访问 [如何使用包](/help/sites-administering/package-manager.md#package-share).

## 建议的部署 {#recommended-deployments}

在AEM Communities中，公用存储用于存储用户生成的内容(UGC)，通常称为 [存储资源提供程序(SRP)](/help/communities/working-with-srp.md). 建议的部署侧重于为公用存储选择一个SRP选项。

公用存储支持在发布环境中审核和分析UGC，同时消除了对的必要 [复制](/help/communities/sync.md) UGC的。

* [社区内容存储](/help/communities/working-with-srp.md) ：讨论AEM社区的SRP存储选项

* [推荐的拓扑](/help/communities/topologies.md) ：根据用例和SRP选择讨论要使用的拓扑

## 升级 {#upgrading}

从以前版本的AEM升级到AEM 6.5平台时，请务必阅读 [升级到AEM 6.5](/help/sites-deploying/upgrade.md).

除了升级平台外，请阅读 [升级到AEM Communities 6.5](/help/communities/upgrade.md) 以了解社区更改。

## 配置 {#configurations}

### 主要发布者 {#primary-publisher}

当选择的部署是 [发布场](/help/communities/topologies.md#tarmk-publish-farm)，则必须将一个AEM发布实例标识为 **`primary publisher`** 对于不应在所有实例上发生的活动，例如依赖以下项的功能 **通知** 或 **Adobe Analytics**.

默认情况下， `AEM Communities Publisher Configuration` OSGi配置使用 **`Primary Publisher`** 选中复选框，以便发布场中的所有发布实例都将自行标识为主发布实例。

因此，有必要 **编辑所有辅助发布实例上的配置** 取消选中 **`Primary Publisher`** 复选框。

![primary-publish](assets/primary-publisher.png)

对于发布场中的所有其他（辅助）发布实例：

* 使用管理员权限登录
* 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* 找到 `AEM Communities Publisher Configuration`
* 选择编辑图标
* 取消选中 **主要发布者** 框
* 选择 **保存**

### 创作实例上的复制代理 {#replication-agents-on-author}

复制用于发布环境中创建的站点内容，如社区组，以及使用 [隧道服务](#tunnel-service-on-author).

对于主发布者，请确保 [复制代理配置](/help/sites-deploying/replication.md) 正确标识发布服务器和授权用户。 默认授权用户， `admin,` 已经具有相应的权限(是 `Communities Administrators`)。

为了使其他某个用户具有适当的权限，必须将这些用户作为成员添加到 `administrators` 用户组(也是 `Communities Administrators`)。

创作环境中有两个复制代理需要正确配置传输配置。

* 访问创作实例上的复制控制台

   * 在全局导航中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 复制]** > **[!UICONTROL 作者代理]**

* 对于这两个代理，请遵循相同的过程：

   * **默认代理（发布）**
   * **反向复制代理（反向发布）**

      1. 选择代理
      1. 选择 **编辑**
      1. 选择 **传输** 选项卡
      1. 如果没有端口 `4503`，编辑 **URI** 指定正确的端口

      1. 如果不是用户 `admin`，编辑 **用户** 和 **密码** 指定以下项的成员： `administrators` 用户组

下图显示了将端口从4503更改为6103的结果：

#### 默认代理（发布） {#default-agent-publish}

![default-agent-publish](assets/default-agent-publish.png)

#### 反向复制代理（反向发布） {#reverse-replication-agent-publish-reverse}

![reverse-replication-agent](assets/reverse-replication-agent.png)

### 作者上的隧道服务 {#tunnel-service-on-author}

使用创作环境时 [创建站点](/help/communities/sites-console.md)， [修改站点属性](/help/communities/sites-console.md#modifying-site-properties) 或 [管理社区成员](/help/communities/members.md)时，必须访问在发布环境中注册的成员（用户），而不是访问在作者中注册的用户。

通道服务使用创作实例上的复制代理提供此访问权限。

启用通道服务：

* 使用作者实例的管理权限登录。
* 如果publisher不是localhost：4503，或者传输用户不是 `admin`，则 [配置复制代理](#replication-agents-on-author)

* 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* 找到 `AEM Communities Publish Tunnel Service`
* 选择编辑图标
* 查看 **启用** 框
* 选择 **保存**

   ![tunnel-service](assets/tunnel-service.png)

### 复制加密密钥 {#replicate-the-crypto-key}

AEM Communities有两项功能要求所有AEM服务器实例使用相同的加密密钥。 这些是 [分析](/help/communities/analytics.md) 和 [ASRP](/help/communities/asrp.md).

从AEM 6.3开始，密钥资料存储在文件系统中，不再存储在存储库中。

要将关键资料从创作实例复制到所有其他实例，有必要执行以下操作：

* 访问包含要复制的关键材料的AEM实例，通常是创作实例

   * 找到 `com.adobe.granite.crypto.file` 捆绑包，例如，

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * 此 `bundle.info` 文件将标识该捆绑包
   * 导航到数据文件夹，例如，

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * 复制hmac和主节点文件


* 对于每个目标AEM实例

   * 导航到数据文件夹，例如，

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * 粘贴之前复制的2个文件
   * 有必要 [刷新Granite加密包](#refresh-the-granite-crypto-bundle) 目标AEM实例当前是否正在运行


>[!CAUTION]
>
>如果已配置了基于加密密钥的其他安全功能，则复制加密密钥可能会损坏配置。 如需帮助， [联系客户关怀团队](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html).

#### 存储库复制 {#repository-replication}

将关键资料存储在存储库中(对于AEM 6.2及更早版本)，可以通过在每个AEM实例的首次启动时指定以下系统属性（这将创建初始存储库）来保留：

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>务必确认 [作者上的复制代理](#replication-agents-on-author) 已正确配置。

将密钥资料存储在存储库中，将加密密钥从创作实例复制到其他实例的方式如下：

使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)：

* 浏览到 [https://&lt;server>：&lt;port>/crx/de](https://localhost:4502/crx/de)
* 选择 `/etc/key`
* 打开 `Replication` 选项卡
* 选择 `Replicate`

* [刷新Granite加密包](#refresh-the-granite-crypto-bundle)

   ![replicare-repository](assets/replicare-repository.png)

#### 刷新Granite加密包 {#refresh-the-granite-crypto-bundle}

* 在每个发布实例上，访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://&lt;server>：&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* 查找 `Adobe Granite Crypto Support` 包(com.adobe.granite.crypto)
* 选择 **刷新**

   ![花岗岩密码](assets/granite-crypto.png)

* 片刻之后， **成功** 对话框应会出现：
   `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

如果使用Apache HTTP Server，请确保为所有相关条目使用正确的服务器名称。

特别是，请注意使用正确的服务器名称，而不是 `localhost`，在 `RedirectMatch`.

#### httpd.conf示例 {#httpd-conf-sample}

```shell
<IfModule alias_module>
     # XAMPP does not have a favicon; this prevents any 404 errors which may arise.
     Redirect 404 /favicon.ico
     <Location /favicon.ico>
         ErrorDocument 404 "No favicon"
     </Location>

    # Return from "Sign Out" generates response header directing you to "/", generating a 404 error
    # The RedirectMatch resolves it correctly when modified for the target Community Site :
    RedirectMatch ^/$ https://[server name]/content/sites/engage/en.html
 ...
 </IfModule>
```

### Dispatcher {#dispatcher}

如果使用Dispatcher，请参阅：

* AEM [调度程序](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) 文档
* [安装 Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [为社区配置Dispatcher](/help/communities/dispatcher.md)
* [已知问题](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## 相关社区文档 {#related-communities-documentation}

* 访问 [管理社区站点](/help/communities/administer-landing.md) 了解有关创建社区站点、配置社区站点模板、审核社区内容、管理成员和配置消息传送的信息。

* 访问 [发展中的社区](/help/communities/communities.md) 了解社交组件框架(SCF)和自定义社区组件和功能。

* 访问 [创作社区组件](/help/communities/author-communities.md) 了解如何使用创作和配置社区组件。
