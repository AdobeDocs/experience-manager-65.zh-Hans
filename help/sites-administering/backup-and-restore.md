---
title: 备份和恢复
seo-title: 备份和恢复
description: 了解如何备份和恢复AEM内容。
seo-description: 了解如何备份和恢复AEM内容。
uuid: 446a466f-f508-4430-9e50-42cd4463760e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: eb8bbb85-ca2f-4877-8ee0-bb1ee8b7d8de
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# 备份和恢复{#backup-and-restore}

在AEM中，有两种备份和恢复存储库内容的方法：

* 您可以创建存储库的外部备份并将其存储在安全位置。 如果存储库出现故障，您可以将其恢复到以前的状态。
* 您可以创建存储库内容的内部版本。 这些版本与内容一起存储在存储库中，因此您可以快速恢复已更改或删除的节点和树。

## 常规 {#general}

此处介绍的方法适用于系统备份和恢复。

如果您需要备份和／或恢复丢失的少量内容，则不一定需要恢复系统：

* 您可以通过包从其他系统获取数据
* 或者，在临时系统上恢复备份，创建一个内容包并在缺少此内容的系统上部署它。

有关详细信息，请参 [阅下面的包备份](/help/sites-administering/backup-and-restore.md#package-backup) 。

## 计时 {#timing}

请勿与数据存储垃圾收集并行运行备份，因为这可能会损害两个进程的结果。

## 脱机备份 {#offline-backup}

您始终可以执行脱机备份。 这需要AEM停机，但与在线备份相比，在所需时间方面会非常有效。

在大多数情况下，您将使用文件系统快照创建存储的只读副本。 要创建脱机备份，请执行以下步骤：

* 停止应用程序
* 制作快照备份
* 启动应用程序

由于快照备份通常只需几秒钟，因此整个停机时间不到几分钟。

## 联机备份 {#online-backup}

此备份方法可创建整个存储库的备份，包括在其下部部署的任何应用程序，如AEM。 备份包括内容、版本历史、配置、软件、修补程序、自定义应用程序、日志文件、搜索索引等。 如果您使用群集，并且共享文件夹是 `crx-quickstart` （物理上或使用软链接）的子目录，则也会备份共享目录。

您可以在以后恢复整个存储库（和任何应用程序）。

此方法作为“热”或“联机”备份运行，因此可在存储库运行时执行它。 因此，在备份运行时，存储库可用。 此方法适用于默认的基于Tar存储的存储库实例。

创建备份时，您有以下选项：

* 使用AEM的集成备份工具备份到目录。
* 使用文件系统快照备份到目录

无论如何，备份都会创建存储库的映像（或快照）。 然后，系统备份代理应确保将此映像实际传输到专用备份系统（磁带机）。

>[!NOTE]
>
>如果对具有自定义Blobstore配置的AEM实例使用AEM联机备份功能，则建议将数据存储的路径配置为“ `crx-quickstart`”目录外，然后单独备份数据存储。

>[!CAUTION]
>
>联机备份只备份文件系统。 如果将存储库内容和／或存储库文件存储在数据库中，则该数据库需要单独备份。 如果您正在将AEM与MongoDB结合使用，请参阅有关如何使用 [MongoDB本机备份工具的文档](https://docs.mongodb.org/manual/tutorial/backup-with-mongodump/)。

### AEM Online Backup {#aem-online-backup}

存储库的联机备份允许您创建、下载和删除备份文件。 它是“热”或“联机”备份功能，因此可以在读写模式下正常使用存储库时执行。

>[!CAUTION]
>
>请勿将AEM联机备份与 [Datastore Garbage Collection或Revision Cleanup](/help/sites-administering/data-store-garbage-collection.md) 同时 [运行](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)。 它会对系统性能产生负面影响。

启动备份时，可指定 **Target Path** （目标路径）和／或 **Delay（延迟）**。

**目标路径** 备份文件通常保存在快速启动jar文件(.jar)所在文件夹的父文件夹中。 例如，如果您的AEM jar文件位于/InstallationKits/AEM下，则备份将在/InstallationKits下生成。 您还可以将目标指定到您选择的位置。

如果 **TargetPath是目录** ，则会在此目录中创建存储库的图像。 如果同一目录被多次（或始终）用于存储备份，

* 在TargetPath中对存储库中的已修改文件进行相应修改
* 已删除的存储库中的文件将在TargetPath中删除
* 在存储库中创建的文件是在TargetPath中创建的

>[!NOTE]
>
>如果 **TargetPath设置为扩展名为******.zip的文件名，则存储库将备份到临时目录，然后压缩该临时目录的内容并存储在ZIP文件中。
>
>这种方法不受欢迎，因为
>
>* 在备份过程中，它需要额外的磁盘存储（临时目录加上zip文件）
>* 压缩过程由存储库完成，并可能影响其性能。
>* 它会延迟备份过程。
>* 最高可配备Java 1.6 java只能创建大小高达4GB的ZIP文件。
>
>
如果需要创建ZIP作为备份格式，您应该备份到目录，然后使用压缩程序创建zip文件。

**延迟** ：指示时间延迟（以毫秒为单位），以便不影响存储库性能。 默认情况下，存储库备份以全速运行。 您可以降低创建联机备份的速度，这样不会降低其他任务的速度。

使用非常大的延迟时，请确保联机备份不超过24小时。 如果已这样做，请放弃此备份，因为它可能不包含所有二进制文件。
1毫秒的延迟通常导致10%的CPU使用，10毫秒的延迟通常导致不到3%的CPU使用。 总延迟（以秒为单位）可以按如下方式估计：存储库大小(MB)，乘以毫秒的延迟，再除以2（如果使用zip选项），或除以4（备份到目录时）。 这意味着备份到200 MB存储库的目录（延迟时间为1毫秒）会使备份时间增加约50秒。

>[!NOTE]
>
>有关 [该过程的内部详细信息](#how-aem-online-backup-works) ，请参阅AEM在线备份的工作方式。

创建备份：

1. 以管理员身份登录到AEM。

1. 转到工 **具——操作——备份。**
1. 单击&#x200B;**创建**。将打开备份控制台。

   ![chlimage_1-1](assets/chlimage_1-1a.png)

1. 在备份控制台上，指定 **[Target Path](#aem-online-backup)**and**[ Delay](#aem-online-backup)**。

   ![chlimage_1-2](assets/chlimage_1-2a.png)

   >[!NOTE]
   >
   >备份控制台也可通过以下方式使用：
   >
   >
   >` https://<*hostname*>:<*port-number*>/libs/granite/backup/content/admin.html`

1. 单 **击保存**，进度栏将指示备份进度。

   >[!NOTE]
   >
   >您可 **以随时取消** 正在运行的备份。

1. 备份完成后，备份窗口中会列出zip文件。

   ![chlimage_1-3](assets/chlimage_1-3a.png)

   >[!NOTE]
   >
   >可以使用控制台删除不再需要的备份文件。 在左窗格中选择备份文件，然后单击“删 **除”**。

   >[!NOTE]
   >
   >如果您已备份到目录：备份过程完成后，AEM将不会写入目标目录。

### 自动化AEM在线备份 {#automating-aem-online-backup}

如果可能，应当在系统上负载很小时运行联机备份，例如在上午。

使用或HTTP客户端可以自 `wget` 动执行 `curl` 备份。 下面显示了如何使用curl自动备份的示例。

#### 备份到默认的Target目录 {#backing-up-to-the-default-target-directory}

>[!CAUTION]
>
>在以下示例中，可能需要为您 `curl` 的实例配置命令中的各种参数；例如，主机名( `localhost`)、端口( `4502`)、管理员密码( `xyz`)和文件名( `backup.zip`)。

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=backup.zip
```

备份文件／目录在服务器上创建，该文件夹位于包含该文件夹的父文件夹 `crx-quickstart` 中（与使用浏览器创建备份时相同）。 例如，如果您已在目录中安装AEM `/InstallationKits/crx-quickstart/`，则将在目录中创建备 `/InstallationKits` 份。

curl命令会立即返回，因此您必须监视此目录以查看zip文件的准备时间。 在创建备份时，可以看到临时目录（其名称基于最终的zip文件的名称），最后将压缩该目录。 例如：

* 生成的zip文件的名称： `backup.zip`
* 临时目录的名称： `backup.f4d5.temp`

#### 备份到非默认Target目录 {#backing-up-to-a-non-default-target-directory}

通常，备份文件／目录是在包含该文件夹的文件夹的父文件夹中的服务器上创建 `crx-quickstart` 的。

如果要将备份（按任一排序）保存到其他位置，可以在命令中将绝对路径“”设 `target` 置为参数 `curl` 。

例如，要在目录 `backupJune.zip` 中生成 `/Backups/2012`:

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=/Backups/2012/backupJune.zip"
```

>[!CAUTION]
>
>使用其他应用程序服务器（如JBoss）时，联机备份可能无法按预期工作，因为目标目录不可写。 在这种情况下，请联系支持部门。

>[!NOTE]
>
>还可以使用AEM提 [供的MBean触发备份](/help/sites-administering/jmx-console.md)。

### 文件系统快照备份 {#filesystem-snapshot-backup}

此处描述的过程特别适用于大型存储库。

>[!NOTE]
>
>如果要使用此备份方法，则系统必须支持文件系统快照。 例如，对于Linux，这意味着您的文件系统应放在逻辑卷上。

1. 执行已部署的文件系统AEM的快照。

1. 装载文件系统快照。
1. 执行备份并卸载快照。

### AEM Online backup的工作原理 {#how-aem-online-backup-works}

AEM联机备份由一系列内部操作组成，这些操作可确保备份数据和创建备份文件的完整性。 下面列出了相关信息。

联机备份使用以下算法：

1. 创建zip文件时，第一步是创建或定位目标目录。

   * 如果备份到zip文件，则会创建临时目录。 目录名称以开头 `backup.` 和结尾为 `.temp`;例如 `backup.f4d3.temp`,
   * 如果备份到目录，则使用在目标路径中指定的名称。 可以使用现有目录，否则将创建新目录。

      备份启动时， `backupInProgress.txt` 目标目录中会创建一个名为空的文件。 备份完成后，将删除此文件。

1. 文件将从源目录复制到目标目录（或创建zip文件时的临时目录）。 在数据存储之前复制区段存储区，以避免存储库损坏。 创建备份时，将忽略索引和缓存数据。 因此，备份中不 `crx-quickstart/repository/cache` 包括 `crx-quickstart/repository/index` 来自和来自的数据。 创建zip文件时，进程的进度栏指示符在0%到70%之间；如果未创建zip文件，则为0%到100%。

1. 如果备份到预先存在的目录，则目标目录中的“旧”文件将被删除。 旧文件是源目录中不存在的文件。

文件分四个阶段复制到目标目录：

1. 在第一个复制阶段（创建zip文件时进度指示符0% - 63%，如果未创建zip文件，则为0% - 90%），在存储库正常运行时复制所有文件。 该过程分为两个阶段：

   * 阶段A —— 复制除数据存储之外的所有内容（有延迟）。
   * 阶段B —— 仅复制数据存储（有延迟）。

1. 在第二个复制阶段（创建zip文件时进度指示符为63% - 65.8%，如果未创建zip文件，则为90% - 94%），仅复制自启动第一个复制阶段以来在源目录中创建或修改的文件。 根据存储库的活动，这可能范围从根本没有文件到大量文件（因为第一个文件复制阶段通常需要很长时间）。 复制过程与第一阶段类似（具有延迟的阶段A和阶段B）。
1. 在第三个复制阶段（创建zip文件时进度指示符为65.8% - 68.6%；如果未创建zip文件，则为94% - 98%），仅复制自第二个复制阶段启动以来在源目录中创建或修改的文件。 根据存储库的活动，可能没有要复制的文件，或者只有很少的文件（因为第二个文件复制阶段通常很快）。 复制过程与第二阶段类似——阶段A和阶段B，但没有延迟。
1. 文件复制阶段1到3在存储库运行时可同时完成。 仅复制自启动第三个复制阶段以来在源目录中创建或修改的文件。 根据存储库的活动，可能没有要复制的文件，或者非常少的文件（因为第二个文件复制阶段通常非常快）。 创建zip文件时，进度指示器为68.6% - 70%；如果未创建zip文件，进度指示器为98% - 100%。 复制过程与第三阶段类似。
1. 具体取决于目标：

   * 如果指定了zip文件，则现在从临时目录创建该文件。 进度指标70%-100%。 随后将删除临时目录。
   * 如果目标是目录，则删除名为的空文 `backupInProgress.txt` 件以指示备份已完成。

## 恢复备份 {#restoring-the-backup}

可以按如下方式恢复备份：

* 如果执行文件系统快照备份，您只需恢复系统映像。
* 如果您将备份创建为zip文件，只需将内容解压缩到新文件夹中，然后从该位置启动AEM。

## 包备份 {#package-backup}

要备份和恢复内容，您可以使用包管理器之一，它使用内容包格式备份和恢复内容。 包管理器在定义和管理包方面提供了更大的灵活性。

有关这些单独的内容包格式的功能和权衡的详细信息，请参 [阅如何使用包](/help/sites-administering/package-manager.md)。

### 备份范围 {#scope-of-backup}

当您使用“包管理器”或“内容拉链”备份节点时，CRX会保存以下信息：

* 您选择的树下的存储库内容。
* 用于备份内容的节点类型定义。
* 用于备份内容的命名空间定义。

备份时，AEM会丢失以下信息：

* 版本历史记录。

