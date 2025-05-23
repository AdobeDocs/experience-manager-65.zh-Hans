---
title: 备份和恢复
description: 了解如何备份和恢复AEM内容和配置。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: dd26dade-b769-483e-bc11-dcfa5ed1f87e
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2314'
ht-degree: 0%

---

# 备份和恢复{#backup-and-restore}

有两种方法可以在AEM中备份和恢复存储库内容：

* 您可以创建存储库的外部备份，并将其存储在安全位置。 如果存储库出现故障，您可以将其恢复到以前的状态。
* 您可以创建存储库内容的内部版本。 这些版本与内容一起存储在存储库中，因此您可以快速恢复已更改或删除的节点和树。

## 常规 {#general}

这里介绍的方法适用于系统备份和恢复。

如果您需要备份和/或恢复少量丢失的内容，则不一定需要恢复系统：

* 您可以通过包从另一个系统获取数据
* 或者，在临时系统上恢复备份，创建一个内容包并将其部署到缺少此内容的系统上。

有关详细信息，请参阅下面的[包备份](/help/sites-administering/backup-and-restore.md#package-backup)。

## 时间安排 {#timing}

请勿与数据存储垃圾收集并行运行备份，因为这样可能会损害两个进程的结果。

## 脱机备份 {#offline-backup}

您始终可以执行脱机备份。 这需要AEM的停机时间，但与在线备份相比，在所需时间方面可以非常高效。

在大多数情况下，您将使用文件系统快照来创建存储区的只读副本。 要创建脱机备份，请执行以下步骤：

* 停止应用程序
* 创建快照备份
* 启动应用程序

由于快照备份通常只需要几秒钟的时间，因此整个停机时间少于几分钟。

## 在线备份 {#online-backup}

此备份方法创建整个存储库的备份，包括部署在其下的任何应用程序，如AEM。 备份包括内容、版本历史记录、配置、软件、修补程序、自定义应用程序、日志文件、搜索索引等。 如果您使用群集，并且共享文件夹是`crx-quickstart`的子目录（物理目录或使用软链接），则共享目录也会备份。

您可以稍后恢复整个存储库（以及任何应用程序）。

此方法作为“热”或“在线”备份运行，因此可在存储库运行时执行。 因此，在备份运行时，存储库可用。 此方法适用于默认的、基于Tar存储的存储库实例。

创建备份时，您有以下选项：

* 使用AEM的集成备份工具备份到目录。
* 使用文件系统快照备份到目录

在任何情况下，备份都会创建存储库的映像（或快照）。 然后，系统备份代理应该注意将此映像实际传输到专用备份系统（磁带机）。

>[!NOTE]
>
>如果在具有自定义Blobstore配置的AEM实例上使用AEM联机备份功能，建议将数据存储的路径配置为在“`crx-quickstart`”目录之外，并单独备份数据存储。

>[!CAUTION]
>
>联机备份仅备份文件系统。 如果将存储库内容和/或存储库文件存储在数据库中，则需要单独备份该数据库。 如果将AEM与MongoDB一起使用，请参阅有关如何使用[MongoDB本机备份工具](https://docs.mongodb.org/manual/tutorial/backup-with-mongodump/)的文档。

### AEM联机备份 {#aem-online-backup}

通过存储库的在线备份，您可以创建、下载和删除备份文件。 它是一种“热”或“在线”备份功能，因此可以在存储库以读写模式正常使用时执行。

>[!CAUTION]
>
>请勿同时运行AEM Online Backup和[数据存储垃圾收集](/help/sites-administering/data-store-garbage-collection.md)或[修订清理](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)。 这将对系统性能产生负面影响。

开始备份时，您可以指定&#x200B;**目标路径**&#x200B;和/或&#x200B;**延迟**。

**目标路径**&#x200B;备份文件通常保存在保存快速入门jar文件(.jar)的文件夹的父文件夹中。 例如，如果AEM jar文件位于/InstallationKits/AEM下，则会在/InstallationKits下生成备份。 您还可以为所选位置指定目标。

如果&#x200B;**TargetPath**&#x200B;是一个目录，则在此目录中创建存储库的图像。 如果存储备份时多次使用同一个目录（或总是使用同一个目录），

* 在TargetPath中相应地修改存储库中已修改的文件
* 存储库中已删除的文件将在TargetPath中删除
* 在存储库中创建的文件在TargetPath中创建

>[!NOTE]
>
>如果将&#x200B;**TargetPath**&#x200B;设置为扩展名为&#x200B;**.zip**&#x200B;的文件名，则存储库将备份到临时目录中，然后压缩此临时目录的内容并将其存储在ZIP文件中。
>
>这种做法令人气馁，因为
>
>* 在备份过程中需要额外的磁盘存储（临时目录加上zip文件）
>* 压缩过程由存储库完成，可能会影响其性能。
>* 这会延迟备份过程。
>* 在Java 1.6中，Java最多只能创建4 GB大小的ZIP文件。
>
>如果需要创建ZIP作为备份格式，则应备份到目录，然后使用压缩程序创建zip文件。

**延迟**&#x200B;表示时间延迟（以毫秒为单位），因此存储库性能不受影响。 默认情况下，存储库备份以全速运行。 您可以减慢创建联机备份的速度，这样就不会减慢其他任务的速度。

如果延迟时间非常长，请确保在线备份不会超过24小时。 如果是，则放弃此备份，因为它可能不包含所有二进制文件。
1毫秒的延迟通常导致10%的CPU使用率，10毫秒的延迟通常导致3%的CPU使用率。 总延迟时间（以秒为单位）的估计如下：存储库大小（以MB为单位），乘以延迟时间（以毫秒为单位），再除以2（如果使用zip选项），或再除以4（备份到目录时）。 这意味着对具有1毫秒延迟的200 MB存储库的目录的备份将备份时间增加约50秒。

>[!NOTE]
>
>有关该过程的内部详细信息，请参阅[AEM Online Backup的工作方式](#how-aem-online-backup-works)。

要创建备份，请执行以下操作：

1. 以管理员身份登录到AEM。

1. 转到&#x200B;**工具 — 操作 — 备份。**
1. 单击&#x200B;**创建**。此时将打开备份控制台。

   ![chlimage_1-1](assets/chlimage_1-1a.png)

1. 在备份控制台上，指定&#x200B;**[目标路径](#aem-online-backup)**&#x200B;和&#x200B;**[延迟](#aem-online-backup)**。

   ![chlimage_1-2](assets/chlimage_1-2a.png)

   >[!NOTE]
   >
   >也可以使用以下方式访问备份控制台：
   >
   >
   >` https://<*hostname*>:<*port-number*>/libs/granite/backup/content/admin.html`

1. 单击&#x200B;**保存**，进度条将指示备份进度。

   >[!NOTE]
   >
   >您可以随时&#x200B;**取消**&#x200B;正在运行的备份。

1. 备份完成后， zip文件将列在备份窗口中。

   ![chlimage_1-3](assets/chlimage_1-3a.png)

   >[!NOTE]
   >
   >不再需要的备份文件可以使用控制台删除。 在左窗格中选择备份文件，然后单击&#x200B;**删除**。

   >[!NOTE]
   >
   >如果已备份到目录：备份过程完成后，AEM将不会写入目标目录。

### 自动化AEM在线备份 {#automating-aem-online-backup}

如果可能，应在系统负荷很小时（例如，早上时）运行联机备份。

可以使用`wget`或`curl` HTTP客户端自动进行备份。 下面显示了如何使用curl自动执行备份的示例。

#### 备份到默认目标目录 {#backing-up-to-the-default-target-directory}

>[!CAUTION]
>
>在以下示例中，`curl`命令中的各种参数可能需要为您的实例进行配置；例如，主机名(`localhost`)、端口(`4502`)、管理员密码(`xyz`)和文件名(`backup.zip`)。

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=backup.zip
```

备份文件/目录在服务器上创建，位于包含`crx-quickstart`文件夹的父文件夹中（与使用浏览器创建备份时相同）。 例如，如果您在目录`/InstallationKits/crx-quickstart/`中安装了AEM，则备份将在`/InstallationKits`目录中创建。

curl命令会立即返回，因此您必须监视此目录以查看zip文件何时准备就绪。 在创建备份时，可以看到临时目录（其名称基于最终zip文件的名称），最后将压缩此目录。 例如：

* 生成的zip文件的名称： `backup.zip`
* 临时目录的名称： `backup.f4d5.temp`

#### 备份到非默认目标目录 {#backing-up-to-a-non-default-target-directory}

通常，备份文件/目录是在服务器上在包含`crx-quickstart`文件夹的文件夹的父文件夹中创建的。

如果要将备份（任何一种）保存到其他位置，可以在`curl`命令中设置到`target`参数的绝对路径。

例如，要在目录`/Backups/2012`中生成`backupJune.zip`：

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=/Backups/2012/backupJune.zip"
```

>[!CAUTION]
>
>使用其他应用程序服务器（如JBoss）时，由于目标目录不可写，联机备份可能无法按预期工作。 在这种情况下，请联系支持人员。

>[!NOTE]
>
>还可以使用AEM[&#128279;](/help/sites-administering/jmx-console.md)提供的MBean 触发备份。

### 文件系统快照备份 {#filesystem-snapshot-backup}

此处介绍的过程特别适用于大型存储库。

>[!NOTE]
>
>如果要使用此备份方法，您的系统必须支持文件系统快照。 例如，对于Linux ，这意味着文件系统应放置在逻辑卷上。

1. 对部署了AEM的文件系统创建快照。

1. 装载文件系统快照。
1. 执行备份并卸载快照。

### AEM联机备份的工作原理 {#how-aem-online-backup-works}

AEM Online Backup由一系列内部操作组成，以确保正在备份的数据和正在创建的备份文件的完整性。 以下列出感兴趣的客户。

联机备份使用以下算法：

1. 创建zip文件时，第一步是创建或定位目标目录。

   * 如果备份到zip文件，则会创建临时目录。 目录名称以`backup.`开头并以`.temp`结尾；例如，`backup.f4d3.temp`。
   * 如果备份到目录，则使用目标路径中指定的名称。 可以使用现有目录，否则将创建新目录。

     备份启动时，在目标目录中创建一个名为`backupInProgress.txt`的空文件。 备份完成后，此文件将被删除。

1. 文件将从源目录复制到目标目录（或在创建zip文件时复制到临时目录）。 区段存储将在数据存储之前复制，以避免存储库损坏。 创建备份时，将忽略索引和缓存数据。 因此，备份中不包含来自`crx-quickstart/repository/cache`和`crx-quickstart/repository/index`的数据。 在创建zip文件时，进程的进度条指示符介于0%-70%之间；如果未创建zip文件，则进度条指示符介于0%-100%之间。

1. 如果备份到预先存在的目录，则删除目标目录中的“旧”文件。 旧文件是源目录中不存在的文件。

文件将分四个阶段复制到目标目录：

1. 在第一个复制阶段（创建zip文件时进度指示器0% - 63%，如果未创建zip文件，则进度指示器0% - 90%），所有文件都将在存储库正常运行时复制。 该过程分为两个阶段：

   * 阶段A — 复制除数据存储之外的所有内容（延迟）。
   * 阶段B — 仅复制数据存储（延迟）。

1. 在第二个复制阶段（创建zip文件时进度指示器63% - 65.8%，如果未创建zip文件，则进度指示器90% - 94%），将仅复制自第一个复制阶段启动以来在源目录中创建或修改的文件。 根据存储库的活动，文件数量可能会从完全没有文件到大量文件不等（因为第一个文件复制阶段通常需要的时间最长）。 复制过程类似于第一阶段（阶段A和阶段B延迟）。
1. 在第三个复制阶段（创建zip文件时进度指示器为65.8% - 68.6%，未创建zip文件时进度指示器为94% - 98%），将仅复制自第二个复制阶段启动以来在源目录中创建或修改的文件。 根据存储库的活动，可能没有要复制的文件，或者文件数量非常少（因为第二个文件复制阶段通常很快）。 复制过程与第二阶段（阶段A和阶段B）相似，但不会延迟。
1. 文件复制阶段1到3均在存储库运行时同时完成。 只复制自第三个复制阶段启动后在源目录中创建或修改的文件。 根据存储库的活动，可能没有要复制的文件，或者文件数量非常少（因为第二个文件复制阶段通常非常快）。 创建zip文件时进度指示器为68.6% - 70%；如果未创建zip文件，则进度指示器为98% - 100%。 复制过程类似于第三阶段。
1. 具体取决于目标：

   * 如果指定了zip文件，则现在将从临时目录创建该文件。 进度指示器70%-100%。 然后删除临时目录。
   * 如果目标是一个目录，则将删除名为`backupInProgress.txt`的空文件，以指示备份已完成。

## 恢复备份 {#restoring-the-backup}

您可以按如下方式恢复备份：

* 如果执行了文件系统快照备份，则只需还原系统的映像即可。
* 如果将备份创建为zip文件，只需将新文件夹中的内容解压缩，然后从该位置启动AEM。

## 包备份 {#package-backup}

要备份和还原内容，您可以使用包管理器之一，该管理器使用内容包格式来备份和还原内容。 包管理器在定义和管理包方面提供了更大的灵活性。

有关每种内容包格式的功能和权衡的详细信息，请参阅[如何使用包](/help/sites-administering/package-manager.md)。

### 备份范围 {#scope-of-backup}

使用包管理器或内容拉链备份节点时，CRX会保存以下信息：

* 所选树下的存储库内容。
* 用于备份内容的节点类型定义。
* 用于备份内容的命名空间定义。

备份时，AEM会丢失以下信息：

* 版本历史记录。
