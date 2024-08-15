---
title: AEM 6.5中的存储元素
description: 了解AEM 6.5中可用的节点存储实施以及如何维护存储库。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
exl-id: 52437eb5-f9fb-4945-9950-5a1562fe878d
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: db7830895c8a2d1b7228dc4780296d43f15776df
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# AEM 6.5中的存储元素{#storage-elements-in-aem}

本文涵盖以下内容：

* [AEM 6中的存储概述](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [维护存储库](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM 6中的存储概述 {#overview-of-storage-in-aem}

AEM 6最重要的变化之一是存储库级别的创新。

目前，AEM6中有两种节点存储实现可用： Tar存储和MongoDB存储。

### Tar存储 {#tar-storage}

#### 使用Tar存储运行新安装的AEM实例 {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>区段节点存储的PID已从org.apache.jackrabbit.oak更改。将AEM 6早期版本中的&#x200B;**plugins**.segment.SegmentNodeStoreService更改为AEM 6.3中的org.apache.jackrabbit.oak.segment.SegmentNodeStoreService。确保进行了必要的配置调整，以便反映所做的更改。

默认情况下，AEM 6使用Tar存储来存储节点和二进制文件，并使用默认配置选项。 您可以通过执行以下操作手动配置其存储设置：

1. 下载AEM 6快速入门Jar并将其放入新文件夹中。
1. 通过运行以下命令解压缩AEM：

   `java -jar cq-quickstart-6.jar -unpack`

1. 在安装目录中创建名为`crx-quickstart\install`的文件夹。

1. 在新创建的文件夹中创建一个名为`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`的文件。

1. 编辑文件并设置配置选项。 以下选项可用于区段节点存储，它是AEM Tar存储实施的基础：

   * `repository.home`：存储各种存储库相关数据的存储库主目录的路径。 默认情况下，区段文件将存储在crx-quickstart/segmentstore目录下。
   * `tarmk.size`：区段的最大大小（以MB为单位）。 默认值为256 MB。

1. 启动AEM。

### Mongo存储 {#mongo-storage}

#### 使用Mongo Storage运行新安装的AEM实例 {#running-a-freshly-installed-aem-instance-with-mongo-storage}

可以按照以下过程将AEM 6配置为使用MongoDB存储运行：

1. 下载AEM 6快速入门jar并将其放入新文件夹中。
1. 通过运行以下命令解压缩AEM：

   `java -jar cq-quickstart-6.jar -unpack`

1. 确保已安装MongoDB并且正在运行`mongod`的实例。 有关详细信息，请参阅[安装MongoDB](https://docs.mongodb.org/manual/installation/)。
1. 在安装目录中创建名为`crx-quickstart\install`的文件夹。
1. 通过创建一个配置文件来配置节点存储，该配置文件具有您要在`crx-quickstart\install`目录中使用的配置的名称。

   Document Node Store (作为AEM MongoDB存储实现的基础)使用名为`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`的文件

1. 编辑文件并设置配置选项。 以下选项可供选择：

   * `mongouri`：连接到Mongo数据库所需的[MongoURI](https://docs.mongodb.org/manual/reference/connection-string/)。 默认值为`mongodb://localhost:27017`
   * `db`： Mongo数据库的名称。 默认情况下，新的AEM 6安装使用&#x200B;**aem-author**&#x200B;作为数据库名称。
   * `cache`：缓存大小（以MB为单位）。 此缓存大小分布在DocumentNodeStore中使用的各种缓存中。 默认值为256。
   * `changesSize`： Mongo中用于缓存差异输出的上限集合的大小（以MB为单位）。 默认值为256。
   * `customBlobStore`：布尔值，指示使用了自定义数据存储。 默认值为false。

1. 使用要使用的数据存储的PID创建配置文件，并编辑该文件以设置配置选项。 有关详细信息，请参阅[配置节点存储和数据存储](/help/sites-deploying/data-store-config.md)。

1. 通过运行以下命令，启动具有MongoDB存储后端的AEM 6 jar：

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   其中后端运行模式为&#x200B;**`-r`**，示例从MongoDB支持开始。

#### 禁用透明超大页面 {#disabling-transparent-huge-pages}

Red Hat® Linux®使用称为Transparent Great Pages (THP)的内存管理算法。 AEM执行细粒度读取和写入时，THP针对大型操作进行了优化。 因此，建议您在Tar和Mongo存储中禁用THP。 要禁用算法，请执行以下步骤：

1. 在您选择的文本编辑器中打开`/etc/grub.conf`文件。
1. 将以下行添加到&#x200B;**grub.conf**&#x200B;文件中：

   ```
   transparent_hugepage=never
   ```

1. 最后，通过运行以下命令，检查设置是否已生效：

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   如果禁用THP，上述命令的输出应为：

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>请查阅以下资源：
>
>* 有关Red Hat® Linux®上透明大页面的更多信息，请参阅Red Hat®客户门户中的以下文章： [如何在Red Hat Enterprise Linux 6、7和8中使用、监视和禁用透明大页面？](https://access.redhat.com/solutions/46111)
>* 有关Linux®优化提示，请参阅[性能优化](/help/sites-deploying/configuring-performance.md)。
>

## 维护存储库 {#maintaining-the-repository}

存储库的每次更新都会创建一个内容修订版本。 因此，存储库的大小会随着每次更新而增长。 为避免存储库增长失控，必须清理旧修订以释放磁盘资源。 此维护功能称为修订版清理。 修订清理机制通过从存储库中删除过时数据来回收磁盘空间。 有关修订清理的更多详细信息，请阅读[修订清理页面](/help/sites-deploying/revision-cleanup.md)。
