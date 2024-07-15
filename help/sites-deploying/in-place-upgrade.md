---
title: 执行就地升级
description: 了解如何执行AEM 6.5的就地升级。
topic-tags: upgrading
feature: Upgrading
exl-id: aef6ef00-993c-4252-b0ad-ddc4917beaf7
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 0%

---

# 执行就地升级{#performing-an-in-place-upgrade}

>[!NOTE]
>
>此页概述了AEM 6.5的升级过程。如果您的安装已部署到应用程序服务器，请参阅[应用程序服务器安装的升级步骤](/help/sites-deploying/app-server-upgrade.md)。

## 升级前步骤 {#pre-upgrade-steps}

在执行升级之前，必须完成多个步骤。 有关详细信息，请参阅[升级代码和自定义项](/help/sites-deploying/upgrading-code-and-customizations.md)和[升级前维护任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)。 此外，请确保您的系统符合新版本AEM的要求。 请参阅模式检测器如何帮助您估计升级过程的复杂性，并参阅[计划升级](/help/sites-deploying/upgrade-planning.md)中的“升级范围和要求”部分以了解更多信息。

<!--Finally, the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## 迁移先决条件 {#migration-prerequisites}

* **所需的最低Java版本：**&#x200B;迁移工具仅适用于Java版本7及更高版本。 请注意，对于AEM 6.3及更高版本，Oracle的JRE 8和IBM的JRE 7和8是唯一受支持的版本。

* **已升级实例：**&#x200B;如果您要从5.6 **之前的**&#x200B;版本升级，请确保已按照升级文档的6.0版本中所述的步骤执行了到AEM 6.0的就地升级。

## 准备AEM快速入门jar文件 {#prep-quickstart-file}

1. 如果实例正在运行，请停止该实例。

1. 下载新的AEM jar文件并使用它替换`crx-quickstart`文件夹之外的旧文件。

1. 通过运行以下命令来解压缩新的快速入门jar：

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## 内容存储库迁移 {#content-repository-migration}

如果从AEM 6.3升级，则不需要进行此迁移。对于低于6.3的版本，Adobe提供了一个工具，可用于将存储库迁移到AEM 6.3中存在的Oak Segment Tar的新版本。它作为快速入门程序包的一部分提供，对于任何将使用TarMK的升级而言，它是必需的。 升级使用MongoMK的环境不需要迁移存储库。 有关新的Segment Tar格式好处的详细信息，请参阅[迁移到Oak Segment Tar常见问题解答](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)。

使用标准AEM快速入门jar文件执行实际迁移，并使用新的`-x crx2oak`选项执行，该选项可执行crx2oak工具以简化升级并使其更加稳健。

>[!NOTE]
>
>如果您使用CRX2Oak快速入门扩展执行TarMK存储库内容迁移，则可以通过向迁移命令行添加以下内容来删除&#x200B;**samplecontent**&#x200B;运行模式：
>
>* `--promote-runmode nosamplecontent`
>

要确定应运行的命令，请使用以下命令：

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

其中`<<YOUR_PROFILE>>`和`<<ADDITIONAL_FLAGS>>`被替换为下表列出的配置文件和标志：

<table>
 <tbody>
  <tr>
   <td><strong>Source存储库</strong></td>
   <td><strong>目标存储库</strong></td>
   <td><strong>配置文件</strong></td>
   <td><strong>其他标志</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2或TarMK，带 <code>FileDataStore</code></td>
   <td>tarmk</td>
   <td>segment-fds</td>
   <td>请参阅下面的疑难解答部分</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK或crx2带 <code>S3DataStore</code></td>
   <td>tarmk</td>
   <td>segment-custom-ds</td>
   <td>请参阅下面的疑难解答部分</td>
  </tr>
  <tr>
   <td>不含数据存储的TarMK</td>
   <td>tarmk</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>无需迁移</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**位置：**

* `mongo-host`是MongoDB服务器IP（例如，127.0.0.1）

* `mongo-port`是MongoDB服务器端口(例如： 27017)

* `mongo-database-name`表示数据库的名称（例如：aem-author）

**对于以下情况，您可能还需要其他开关：**

* 如果是在未正确处理Java内存映射的Windows系统上执行升级，请将`--disable-mmap`参数添加到命令中。

有关使用crx2oak工具的其他说明，请参阅使用[CRX2Oak迁移工具](/help/sites-deploying/using-crx2oak.md)。 如果需要，可以手动升级crx2oak助手JAR，方法是在解压缩快速入门后，将其手动替换为较新版本。 它在AEM安装文件夹中的位置为： `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`。 可以从Adobe存储库下载最新版本的CRX2Oak迁移工具： [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

如果迁移成功完成，则该工具将退出，退出代码为零。 此外，检查位于AEM安装目录中的`crx-quickstart/logs`下的`upgrade.log`文件中是否存在WARN和ERROR消息，因为这些消息可能指示迁移期间发生的非致命错误。

检查`crx-quickstart/install`文件夹下的配置文件。 如果需要进行迁移，则将更新以反映目标存储库。

**数据存储上的注释：**

虽然`FileDataStore`是AEM 6.3安装的新默认值，但不需要使用外部数据存储。 虽然建议使用外部数据存储作为生产部署的最佳实践，但它不是升级的先决条件。 由于升级AEM时已存在的复杂性，Adobe建议在不执行数据存储迁移的情况下执行升级。 如果需要，可以稍后单独执行数据存储迁移。

## 迁移问题疑难解答 {#troubleshooting-migration-issues}

如果您从6.3升级，请跳过此部分。虽然提供的crx2oak配置文件应该满足大多数客户的需求，但有时还需要额外的参数。 如果在迁移期间遇到错误，则环境的某些方面可能需要提供其他配置选项。 如果出现这种情况，您可能会遇到以下错误：

**未复制检查点，因为未指定外部数据存储。 这将导致在第一次启动时完全重新索引存储库。 使用 — skip-checkpoints强制迁移，或者访问https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration以了解详细信息。**

出于某种原因，迁移过程需要访问数据存储中的二进制文件，并且无法找到它。 要指定数据存储配置，请在迁移命令的`<<ADDITIONAL_FLAGS>>`部分中包含以下标志：

用于S3数据存储的&#x200B;**：**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

其中`/path/to/SharedS3DataStore.config`表示S3数据存储配置文件的路径，`/path/to/datastore`表示S3数据存储的路径。

**对于文件数据存储：**

```shell
--src-datastore=/path/to/datastore
```

其中`/path/to/datastore`表示文件数据存储的路径。

## 执行升级 {#performing-the-upgrade}

**如果使用S3：**

1. 删除与S3连接器的早期版本关联的`crx-quickstart/install`下的所有jar。

1. 从[https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/)下载1.10.x S3连接器的最新版本

1. 将包提取到临时文件夹，并将`jcr_root/libs/system/install`的内容复制到`crx-quickstart/install`文件夹。

### 确定正确的升级启动命令 {#determining-the-correct-upgrade-start-command}

要执行升级，请务必使用jar文件启动AEM以调出实例。 要升级到6.5，请参阅[延迟内容迁移](/help/sites-deploying/lazy-content-migration.md)中的其他内容重构和迁移选项，您可以使用升级命令选择这些选项。

>[!IMPORTANT]
>
>如果您运行OracleJava 11（或者Java的通常版本高于8），则在启动AEM时，必须在命令行中添加其他开关。 有关详细信息，请参阅[Java 11注意事项](/help/sites-deploying/custom-standalone-install.md#java-considerations)。

请注意，从启动脚本启动AEM将不会启动升级。 大多数客户都使用启动脚本启动AEM，并自定义了此启动脚本，以包含用于环境配置（如内存设置、安全证书等）的交换机。 因此，Adobe建议遵循此过程以确定正确的升级命令：

1. 在运行的AEM实例上，从命令行执行以下命令：

   ```shell
   ps -ef | grep java
   ```

1. 查找AEM进程。 它类似于：

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.5.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 通过将现有jar的路径（在本例中为`crx-quickstart/app/aem-quickstart*.jar`）替换为`crx-quickstart`文件夹的同级新jar来修改命令。 以我们以前的命令为例，我们的命令是：

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   这将确保所有适当的内存设置、自定义运行模式和其他环境参数都适用于升级。 升级完成后，可以从未来启动时的启动脚本启动实例。

## 部署已升级的代码库 {#deploy-upgraded-codebase}

就地升级过程完成后，应部署更新的代码库。 可以在[升级代码和自定义项页面](/help/sites-deploying/upgrading-code-and-customizations.md)中找到将代码库更新为在AEM的目标版本中工作的步骤。

## 执行Post升级检查和故障排除 {#perform-post-upgrade-check-troubleshooting}

请参阅[Post升级检查和疑难解答](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)。
