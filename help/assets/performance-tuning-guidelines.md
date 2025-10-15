---
title: 性能调整 [!DNL Assets]
description: 有关 [!DNL Experience Manager] 配置、更改硬件、软件和网络组件的建议和指导，以消除瓶颈并优化 [!DNL Experience Manager Assets]的性能。
contentOwner: AG
mini-toc-levels: 1
role: Architect, Admin
feature: Asset Management
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
solution: Experience Manager, Experience Manager Assets
source-git-commit: f8588ef353bd08b41202350072728d80ee51f565
workflow-type: tm+mt
source-wordcount: '2729'
ht-degree: 0%

---

<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] 性能优化指南 {#assets-performance-tuning-guide}

[!DNL Experience Manager Assets]安装程序包含多个硬件、软件和网络组件。 根据您的部署方案，可能需要对硬件、软件和网络组件进行特定的配置更改以消除性能瓶颈。

此外，确定并遵守某些硬件和软件优化准则有助于奠定坚实的基础，使您的[!DNL Experience Manager Assets]部署能够满足有关性能、可扩展性和可靠性的期望。

[!DNL Experience Manager Assets]中的性能不佳可能会影响用户在交互性能、资产处理、下载速度和其他方面的体验。

事实上，在为任何项目建立目标指标之前，您必须先执行性能优化这项基本任务。

下面是一些关键重点领域，在这些领域中，您可以发现并修复性能问题，以免它们对用户造成影响。

## 平台 {#platform}

虽然Experience Manager在多种平台上均受支持，但Adobe发现它最大程度地支持了Linux®和Windows上的本机工具，这有助于优化性能和简化实施。 理想情况下，您应该部署64位操作系统以满足[!DNL Experience Manager Assets]部署的高内存要求。 与任何Experience Manager部署一样，您应尽可能实施TarMK。 虽然TarMK不能扩展至超过单个创作实例，但发现其性能优于MongoMK。 您可以添加TarMK卸载实例以提高[!DNL Experience Manager Assets]部署的工作流处理能力。

### 临时文件夹 {#temp-folder}

要缩短资产上传时间，请为Java临时目录使用高性能存储。 在Linux®和Windows上，可以使用RAM驱动器或固态硬盘。 在基于云的环境中，可以使用等效的高速存储类型。 例如，在Amazon EC2中，[临时驱动器](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html)可用于临时文件夹。

假定服务器具有足够的内存，请配置RAM驱动器。 在Linux®上，运行以下命令创建8 GB RAM驱动器：

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

在Windows操作系统上，使用第三方驱动程序创建RAM驱动器，或者只使用高性能存储（如SSD）。

高性能临时卷就绪后，设置JVM参数`-Djava.io.tmpdir`。 例如，可以将下面的JVM参数添加到`CQ_JVM_OPTS`的`bin/start`脚本中的[!DNL Experience Manager]变量：

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java配置 {#java-configuration}

### Java版本 {#java-version}

Adobe建议在Java 8上部署[!DNL Experience Manager Assets]以获得最佳性能。

<!-- TBD: Link to the latest official word around Java.
-->

### JVM参数 {#jvm-parameters}

设置以下JVM参数：

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## 数据存储和内存配置 {#data-store-and-memory-configuration}

### 文件数据存储配置 {#file-data-store-configuration}

建议所有[!DNL Experience Manager Assets]用户将数据存储与区段存储分开。 此外，配置`maxCachedBinarySize`和`cacheSizeInMB`参数可以帮助最大化性能。 将`maxCachedBinarySize`设置为缓存中可容纳的最小文件大小。 指定用于`cacheSizeInMB`内数据存储的内存中缓存的大小。 Adobe建议将此值设置为栈总大小的2-10%。 但是，负载/性能测试可以帮助确定理想的设置。

### 配置缓冲图像缓存的最大大小 {#configure-the-maximum-size-of-the-buffered-image-cache}

将大量资产上传到[!DNL Adobe Experience Manager]时，为允许内存消耗意外达到峰值，并防止JVM因OutOfMemoryErrors而失败，请减小缓冲图像缓存的最大配置大小。 例如，您的系统最大栈(- `Xmx`param)为5 GB，Oak BlobCache设置为1 GB，文档缓存设置为2 GB。 在这种情况下，缓冲缓存将占用最大1.25 GB和内存，这样将仅留下0.75 GB内存用于意外峰值。

在OSGi Web控制台中配置缓冲缓存大小。 在`https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`，以字节为单位设置属性`cq.dam.image.cache.max.memory`。 例如，1073741824为1 GB(1024 x 1024 x 1024 = 1 GB)。

从Experience Manager 6.1 SP1开始，如果您使用`sling:osgiConfig`节点配置此属性，请确保将数据类型设置为“长”。

### 共享的数据存储 {#shared-data-stores}

在大规模实施中，实施S3或共享文件数据存储区有助于节省磁盘空间并提高网络吞吐量。 有关使用共享数据存储的利弊的更多信息，请参阅[Assets大小调整指南](/help/assets/assets-sizing-guide.md)。

### S3数据存储 {#s-data-store}

以下S3数据存储配置(`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`)帮助Adobe将12.8 TB的二进制大对象(BLOB)从现有文件数据存储提取到客户站点的S3数据存储中：

```conf
accessKey=<snip>
 secretKey=<snip>
 s3Bucket=<snip>
 s3Region=us-standard
 s3EndPoint=<a href="https://s3.amazonaws.com/">s3.amazonaws.com</a>
 connectionTimeout=120000
 socketTimeout=120000
 maxConnections=80
 writeThreads=60
 concurrentUploadsThreads=30
 asyncUploadLimit=30
 maxErrorRetry=1000
 path=/opt/author/crx-quickstart/repository/datastore
 s3RenameKeys=false
 s3Encryption=SSE_S3
 proactiveCaching=true
 uploadRetries=1000
 migrateFailuresCount=400
```

## 网络优化 {#network-optimization}

Adobe建议启用HTTPS，因为许多公司都有会侦听HTTP流量的防火墙，这会给上载和损坏文件带来不利影响。 对于大型文件上传，请确保用户与网络有有线连接，因为WiFi网络会快速饱和。 有关识别网络瓶颈的指南，请参阅[Assets大小调整指南](/help/assets/assets-sizing-guide.md)。 若要通过分析网络拓扑评估网络性能，请参阅[Assets网络注意事项](/help/assets/assets-network-considerations.md)。

您的网络优化策略主要取决于[!DNL Experience Manager]实例的可用带宽量和负载。 常用配置选项（包括防火墙或代理）有助于提高网络性能。 请牢记以下要点：

* 根据实例类型（小、中、大），请确保您有足够的网络带宽来实施Experience Manager实例。 如果[!DNL Experience Manager]托管在AWS上，则充足的带宽分配尤其重要。
* 如果您的[!DNL Experience Manager]实例托管在AWS上，则可以通过使用通用缩放策略受益。 如果用户需要高负载，请放大实例。 在中/低负载时将其缩小。
* HTTPS：大多数用户都设有拦截HTTP流量的防火墙，这可能会在上传操作期间对文件上传产生不利影响，甚至导致文件损坏。
* 大文件上传：确保用户有有线网络连接（WiFi连接快速饱和）。

## 工作流 {#workflows}

### 瞬态工作流 {#transient-workflows}

请尽可能将[!UICONTROL DAM更新资产]工作流设置为“临时”。 该设置显着减少了处理工作流所需的开销，因为在这种情况下，工作流不需要经过正常的跟踪和存档过程。

1. 在`/miscadmin`处的[!DNL Experience Manager]部署中导航到`https://[aem_server]:[port]/miscadmin`。

1. 展开&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]** > **[!UICONTROL dam]**。

1. 打开&#x200B;**[!UICONTROL DAM更新资产]**。 从浮动工具面板切换到&#x200B;**[!UICONTROL 页面]**&#x200B;选项卡，然后单击&#x200B;**[!UICONTROL 页面属性]**。

1. 选择&#x200B;**[!UICONTROL 临时工作流]**，然后单击&#x200B;**[!UICONTROL 确定]**。

   >[!NOTE]
   >
   >某些功能不支持临时工作流。 如果[!DNL Assets]部署需要这些功能，请勿配置临时工作流。

如果无法使用临时工作流，请定期运行工作流清除以删除存档的[!UICONTROL DAM更新资产]工作流，以确保系统性能不会降低。

通常，每周执行清除工作流。 但是，在资源密集型场景中（如在大规模资产摄取期间），您可以更频繁地执行该操作。

要配置工作流清除，请通过OSGi控制台添加新的Adobe Granite工作流清除配置。 接下来，在每周维护时段中配置和计划工作流。

如果清除时间过长，则会超时。 因此，您应确保清除作业完成，以避免由于工作流数量过多而导致清除工作流无法完成的情况。

例如，在执行大量非临时工作流（创建工作流实例节点）后，您可以临时执行[ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html)。 它立即删除多余的已完成工作流实例，而不是等待Adobe Granite工作流清除计划程序运行。

### 最大并行作业数 {#maximum-parallel-jobs}

默认情况下，[!DNL Experience Manager]运行的最大并行作业数等于服务器上的处理器数。 此设置的问题在于，在负载较重期间，所有处理器都被[!UICONTROL DAM更新资产]工作流占用，从而减慢UI响应并阻止[!DNL Experience Manager]运行其他可保护服务器性能和稳定性的进程。 最好通过执行以下步骤，将此值设置为服务器上可用处理器的一半：

1. 在[!DNL Experience Manager]作者中，访问`https://[aem_server]:[port]/system/console/slingevent`。

1. 单击与您的实施相关的每个工作流队列上的&#x200B;**[!UICONTROL 编辑]**，例如&#x200B;**[!UICONTROL Granite Transient Workflow队列]**。

1. 更新&#x200B;**[!UICONTROL 最大并行作业]**&#x200B;的值，然后单击&#x200B;**[!UICONTROL 保存]**。

首先，将队列设置为一半可用处理器是一种可行的解决方案。 但是，您可能必须增加或减少此数量才能达到最大吞吐量，并根据环境对其进行调整。 临时和非临时工作流以及其他进程（如外部工作流）有单独的队列。 如果多个队列设置为50%的处理器同时处于活动状态，则系统可能会快速过载。 在用户实施中，大量使用的队列差异很大。 因此，您可能必须仔细配置这些服务器才能在不牺牲服务器稳定性的情况下实现最高效率。

### DAM更新资产配置 {#dam-update-asset-configuration}

[!UICONTROL DAM更新资产]工作流包含为任务配置的整套步骤，例如生成Dynamic Media PTIFF和[!DNL Adobe InDesign Server]集成。 但是，大多数用户可能不需要执行其中的多个步骤。 Adobe建议您创建[!UICONTROL DAM更新资产]工作流模型的自定义副本，并删除任何不必要的步骤。 在这种情况下，请更新[!UICONTROL DAM更新资产]的启动器，以指向新模型。

集中运行[!UICONTROL DAM更新资产]工作流可能会急剧增加文件数据存储的大小。 Adobe的实验结果表明，如果在8小时内执行约5500个工作流，则数据存储大小可以增加约400 GB。

这是临时增加，运行数据存储垃圾收集任务后，数据存储将恢复到其原始大小。

通常，数据存储垃圾收集任务与其他计划的维护任务一起每周运行。

如果磁盘空间有限并且集中运行[!UICONTROL DAM更新资产]工作流，请考虑更频繁地计划垃圾收集任务。

#### 运行时呈现版本 {#runtime-rendition-generation}

客户在其网站中使用各种大小和格式的图像，或将其分发给业务合作伙伴。 由于每个演绎版都会增加资源在存储库中的占用空间，因此Adobe建议谨慎使用此功能。 要减少处理和存储图像所需的资源量，您可以在运行时生成这些图像，而不是在摄取期间生成为演绎版。

许多Sites客户都实施一个图像servlet，该图像服务可在请求图像时调整其大小和裁剪图像，这会对发布实例施加额外的负载。 但是，只要可以缓存这些图像，就可以缓解挑战。

另一种方法是使用Dynamic Media技术完全放弃图像操作。 此外，您可以部署一个不仅从[!DNL Experience Manager]基础结构接管节目生成职责的Brand Portal，还可以接管整个发布层。

#### ImageMagick {#imagemagick}

如果您自定义[!UICONTROL DAM更新资产]工作流以使用ImageMagick生成演绎版，Adobe建议您修改位于`policy.xml`的`/etc/ImageMagick/`文件。 默认情况下，ImageMagick使用OS卷上的全部可用磁盘空间和可用内存。 在`policymap`的`policy.xml`部分中进行以下配置更改以限制这些资源。

```xml
<policymap>
  <!-- <policy domain="system" name="precision" value="6"/> -->
  <policy domain="resource" name="temporary-path" value="/ephemeral0/imagemagick_tmp"/>
  <policy domain="resource" name="memory" value="1000MiB"/>
  <policy domain="resource" name="map" value="1000MiB"/>
  <!-- <policy domain="resource" name="area" value="1gb"/> -->
  <policy domain="resource" name="disk" value="10000MiB"/>
  <!-- <policy domain="resource" name="file" value="768"/> -->
  <policy domain="resource" name="thread" value="1"/>
  <policy domain="resource" name="throttle" value="50"/>
  <!-- <policy domain="resource" name="time" value="3600"/> -->
</policymap>
```

此外，将`configure.xml`文件中ImageMagick的临时文件夹的路径（或通过设置环境变量`MAGICK_TEMPORARY_PATH`）设置为具有足够空间和IOPS的磁盘分区。

>[!CAUTION]
>
>如果ImageMagick使用所有可用磁盘空间，错误配置可能会使服务器不稳定。 使用ImageMagick处理大型文件所需的策略更改可能会影响[!DNL Experience Manager]性能。 有关详细信息，请参阅[安装和配置ImageMagick](/help/assets/best-practices-for-imagemagick.md)。

>[!NOTE]
>
>ImageMagick `policy.xml`和`configure.xml`文件在`/usr/lib64/ImageMagick-&#42;/config/`中可用，而不是`/etc/ImageMagick/`。 有关配置文件的位置，请参阅ImageMagick文档（`https://www.imagemagick.org/script/resources.php`网站）。

如果您在Adobe Managed Services (AMS)上使用[!DNL Experience Manager]，如果您计划处理大量大型PSD或PSB文件，请联系Adobe客户支持。 与Adobe客户支持代表合作，为您的AMS部署实施这些最佳实践，并为Adobe的专有格式选择最佳工具和模型。 [!DNL Experience Manager]不能处理超过30000 x 23000像素的超高分辨率PSB文件。

### XMP写回 {#xmp-writeback}

每当在[!DNL Experience Manager]中修改元数据时，XMP写回都会更新原始资源，这会导致以下情况：

* 资源本身已修改
* 将创建资源的版本
* [!UICONTROL DAM更新资产]已针对该资产运行

列出的结果消耗了相当多的资源。 因此，Adobe建议在不需要时禁用XMP写回。 有关详细信息，请参阅[XMP写回](/help/assets/xmp-writeback.md)。

如果选中运行工作流标志，则导入大量元数据可能会导致资源密集的XMP写回活动。 在使用精益服务器期间规划此类导入，以便不影响其他用户的性能。

## 复制 {#replication}

将资产复制到大量发布实例时（例如，在Sites实施中），Adobe建议您使用链复制。 在这种情况下，创作实例将复制到单个发布实例，然后复制到其他发布实例，从而释放创作实例。

### 配置链复制 {#configure-chain-replication}

1. 选择要用于链接复制的发布实例
1. 在该发布实例上添加指向其他发布实例的复制代理
1. 在每个复制代理上，在“触发器”选项卡上启用“接收时”

>[!NOTE]
>
>Adobe不建议自动激活资源。 但是，如有必要，Adobe建议将此作为工作流的最后步骤，通常是DAM更新资产。

## 搜索索引 {#search-indexes}

安装[最新的Service Pack](/help/release-notes/release-notes.md)和与性能相关的修补程序，因为这些程序通常包括系统索引更新。 有关某些索引优化，请参阅[性能优化提示](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/assets/administer/performance-tuning-guidelines)。

为经常运行的查询创建自定义索引。 有关详细信息，请参阅用于分析慢查询[的](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html)方法和[自定义索引](/help/sites-deploying/queries-and-indexing.md)。 有关查询和索引最佳实践的其他见解，请参阅[查询和索引最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

### Lucene索引配置 {#lucene-index-configurations}

可以对Oak索引配置进行一些优化，以帮助提高[!DNL Experience Manager Assets]性能。 更新索引配置以缩短重新索引时间：

1. 打开CRXDe `/crx/de/index.jsp`并以管理用户身份登录。
1. 浏览到`/oak:index/lucene`。
1. 添加值为`String[]`、`excludedPaths`和`/var`的`/etc/workflow/instances`属性`/etc/replication`。
1. 浏览到`/oak:index/damAssetLucene`。 添加值为`String[]`的`includedPaths`属性`/content/dam`。 保存更改。

如果您的用户不需要对资源执行全文搜索，例如在PDF文档中搜索文本，则禁用它。 您可以通过禁用全文索引来提高索引性能。 要禁用[!DNL Apache Lucene]文本提取，请执行以下步骤：

1. 在[!DNL Experience Manager]界面中，访问[!UICONTROL 包管理器]。
1. 上载并安装位于[disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip)的包。

### 猜测总数 {#guess-total}

在创建可生成大型结果集的查询时，请使用`guessTotal`参数以避免在运行这些查询时占用大量内存。

## 已知问题 {#known-issues}

### 大文件 {#large-files}

存在与[!DNL Experience Manager]中的大文件相关的两个主要已知问题。 当文件大小大于2 GB时，冷备用同步可能会出现内存不足的情况。 在某些情况下，它会阻止备用同步运行。 在其他情况下，它会导致主实例崩溃。 此方案适用于[!DNL Experience Manager]中大于2GB的任何文件，包括内容包。

同样，当文件在使用共享S3数据存储时达到2 GB时，可能需要一些时间才能将文件从缓存完全保存到文件系统。 因此，在使用无二进制复制时，可能会在复制完成之前未保留二进制数据。 这种情况可能导致问题，特别是在数据可用性很重要的情况下。

## 性能测试 {#performance-testing}

对于每个[!DNL Experience Manager]部署，建立一个可以快速发现并解决瓶颈的性能测试机制。 以下是需要重点关注的一些关键领域。

### 网络测试 {#network-testing}

对于客户的所有网络性能问题，请执行以下任务：

* 测试客户网络中的网络性能
* 在Adobe网络内测试网络性能。 对于AMS客户，请与您的CSE合作，从Adobe网络中进行测试。
* 从另一个接入点测试网络性能
* 使用网络基准测试工具
* 针对Dispatcher进行测试

### [!DNL Experience Manager]部署测试 {#aem-deployment-testing}

要通过高效的CPU利用率和负载共享将延迟降至最低并实现高吞吐量，请定期监控[!DNL Experience Manager]部署的性能。 特别是：

* 针对[!DNL Experience Manager]部署运行负载测试。
* 监控上传性能和UI响应性。

## [!DNL Experience Manager Assets]性能核对清单和资产管理任务的影响 {#checklist}

* 启用HTTPS以绕过任何公司HTTP流量探查器。
* 使用有线连接上传大量资产。
* 在Java 8上部署。
* 设置最佳JVM参数。
* 配置文件系统数据存储或S3数据存储。
* 禁用子资源生成。 如果启用，AEM的工作流会为多页面资源中的每个页面创建一个单独的资源。 其中每个页面都是单独的资产，会占用额外的磁盘空间，需要进行版本控制和额外的工作流处理。 如果您不需要单独的页面，请禁用子资产生成和页面提取活动。
* 启用临时工作流。
* 调整Granite工作流队列以限制并发作业。
* 配置[!DNL ImageMagick]以限制资源消耗。
* 从[!UICONTROL DAM更新资产]工作流中删除不必要的步骤。
* 配置工作流和版本清除。
* 使用最新的Service Pack和修补程序优化索引。 请联系Adobe客户支持，获取任何可能提供的其他索引优化。
* 使用guessTotal优化查询性能。
* 如果将[!DNL Experience Manager]配置为从文件内容中检测文件类型(通过在&#x200B;**[!UICONTROL AEM Web Console]**&#x200B;中启用&#x200B;**[!UICONTROL Day CQ DAM Mime Type Service]**)，请在非高峰时间批量上传许多文件，因为它占用大量资源。
