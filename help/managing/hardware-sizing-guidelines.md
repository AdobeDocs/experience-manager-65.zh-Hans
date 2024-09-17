---
title: 硬件大小调整准则
description: 这些大小调整指南提供了部署AEM项目所需硬件资源的大致情况。
exl-id: 5837ef4f-d4e0-49d7-a671-87d5547e0d98
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Developer,Leader
source-git-commit: 9eeba0532a9eddb668b8488218c0570ca2241439
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 0%

---

# 硬件大小调整准则{#hardware-sizing-guidelines}

这些大小调整指南提供了部署AEM项目所需硬件资源的大致情况。 规模估计取决于项目的体系结构、解决方案的复杂性、预期流量和项目要求。 本指南可帮助您确定特定解决方案的硬件需求，或查找硬件需求的上下限估计。

要考虑的基本因素包括（按此顺序）：

* **网络速度**

   * 网络延迟
   * 可用带宽

* **计算速度**

   * 缓存效率
   * 预期流量
   * 模板、应用程序和组件的复杂性
   * 并发作者
   * 创作操作的复杂性（简单内容编辑、MSM转出等）

* **I/O性能**

   * 文件或数据库存储的性能和效率

* **硬盘**

   * 至少比存储库大小大两到三倍

* **内存**

   * 网站的大小（内容对象、页面和用户的数量）
   * 同时处于活动状态的用户/会话数

## 架构 {#architecture}

典型的AEM设置包括创作环境和发布环境。 这些环境对底层硬件大小和系统配置有不同的要求。 有关这两个环境的详细注意事项，请参见[创作环境](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations)和[发布环境](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations)部分。

在典型项目设置中，您有多个环境可在其上暂存项目阶段：

* **开发环境**
开发新功能或进行重大更改。 最佳实践是为每个开发人员使用开发环境（在其个人系统上本地安装）。

* **创作测试环境**
验证更改。 测试环境的数量因项目要求而异（例如，QA、集成测试或用户验收测试不同）。

* **Publish测试环境**
主要用于测试Social Collaboration用例和/或作者与多个发布实例之间的交互。

* **创作生产环境**
供作者编辑内容。

* **Publish生产环境**
用于提供已发布的内容。

此外，环境可能有所不同，从运行AEM的单服务器系统和应用程序服务器，到高度扩展的多服务器、多CPU群集实例集。 Adobe建议您为每个生产系统使用单独的计算机，并且不要在这些计算机上运行其他应用程序。

## 一般硬件大小调整注意事项 {#generic-hardware-sizing-considerations}

以下各节提供了有关如何计算硬件需求的指导，其中将考虑各种因素。 对于大型系统，Adobe建议您在参考配置上执行一组简单的内部基准测试。

性能优化是一项基本任务，在完成特定项目的基准测试之前需要执行这项任务。 在执行任何基准测试并将其结果用于任何硬件大小计算之前，请确保应用[性能优化文档](/help/sites-deploying/configuring-performance.md)中提供的建议。

高级用例的硬件规模要求需要基于对项目的详细性能评估。 需要卓越硬件资源的高级用例的特性包括以下组合：

* 高内容有效负荷/吞吐量
* 广泛使用自定义代码、自定义工作流或第三方软件库
* 与不受支持的外部系统集成

## 磁盘空间/硬盘 {#disk-space-hard-drive}

所需的磁盘空间在很大程度上取决于Web应用程序的卷和类型。 计算时应考虑以下因素：

* 页面、资产和其他存储库存储的实体（如工作流、配置文件等）的数量和大小。
* 估计的内容更改频率，从而创建内容版本
* 将生成的DAM资源演绎版数量
* 随着时间的推移，内容的总体增长

在“联机”和“脱机”版本清理期间，会持续监视磁盘空间。 如果可用磁盘空间下降到临界值以下，则该过程将取消。 关键值是存储库当前磁盘占用空间的25%，无法对其进行配置。 Adobe建议磁盘大小至少比存储库大小（包括预计增长量）大两到三倍。

考虑设置独立磁盘冗余阵列（例如RAID10）以实现数据冗余。

### 虚拟化 {#virtualization}

AEM在虚拟化环境中运行良好，但可能存在CPU或I/O等无法直接等同于物理硬件的因素。 建议选择更高的I/O速度（通常），因为这是关键因素。 设定环境基准对于准确了解所需资源是必不可少的。

### AEM实例的并行化 {#parallelization-of-aem-instances}

**安全失败**

一个防故障的网站至少部署在两个独立的系统上。 如果一个系统发生故障，另一个系统可以接管并补偿系统故障。

**系统资源可扩展性**

当所有系统都在运行时，可以增强计算性能。 这种额外性能不一定与群集节点数量成线性关系，因为这种关系在很大程度上取决于技术环境。 有关详细信息，请参阅[群集文档](/help/sites-deploying/recommended-deploys.md)。

根据特定Web项目的基本要求和具体用例，估计需要多少簇节点：

* 从故障安全的角度来看，必须根据群集节点恢复所需的时间来确定所有环境的严重故障程度以及故障补偿时间。
* 在可扩展性方面，写操作次数基本上是最重要的因素。 可以为仅访问系统的操作建立负载平衡，以处理读取操作；有关详细信息，请参阅[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans)。

### 硬件Recommendations {#hardware-recommendations}

通常，您可以按照为发布环境推荐的方式，对创作环境使用相同的硬件。 通常，创作系统上的网站流量较低，但缓存效率也较低。 但是，这里的基本因素是并行工作的作者数量以及对系统采取的操作类型。 一般来说，（创作环境的）AEM聚类在缩放读取操作方面最有效；换句话说，AEM聚类与执行基本编辑操作的作者一起缩放效果较好。

## 其他特定于用例的计算 {#additional-use-case-specific-calculations}

除了计算默认Web应用程序外，还请考虑以下用例的特定因素。 计算值将添加到默认计算中。

### Assets特定的注意事项 {#assets-specific-considerations}

广泛处理数字资产需要优化的硬件资源，最相关的因素是图像大小和已处理图像的峰值吞吐量。

分配至少16GB的栈并将[!UICONTROL DAM更新资产]工作流配置为使用[Camera Raw包](/help/assets/camera-raw.md)摄取原始图像。

>[!NOTE]
>
>较高的图像吞吐量意味着计算资源必须能够跟上系统I/O的速度，反之亦然。 例如，如果通过导入图像来启动工作流，则通过WebDAV上传许多图像可能会导致工作流积压。
>
>为TarPM、数据存储和搜索索引使用单独的磁盘有助于优化系统I/O行为（但是，通常将搜索索引保留在本地是有意义的）。

>[!NOTE]
>
>另请参阅[Assets性能指南](/help/sites-deploying/assets-performance-sizing.md)。

### 多站点管理器 {#multi-site-manager}

在创作环境中使用AEM MSM时的资源消耗在很大程度上取决于特定用例。 基本因素包括：

* 活动副本数
* 转出的周期
* 要转出的内容树大小
* 转出操作的已连接功能

使用具有代表性的内容摘录测试计划的用例，可以帮助您更好地了解资源消耗。 如果使用计划吞吐量推断结果，则可以评估AEM MSM所需的其他资源。

此外，还应说明并行工作的作者。 如果AEM MSM用例消耗的资源多于计划的资源，则他们会感觉到性能副作用。

### AEM Communities大小调整注意事项 {#aem-communities-sizing-considerations}

包含AEM Communities功能的AEM站点（社区站点）会在发布环境中与站点访客（成员）进行高级别的交互。

社区站点的规模调整考虑因素取决于社区成员预期的交互，以及页面内容的最佳性能是否更加重要。

用户生成的内容(UGC)提交的成员与页面内容分开存储。 虽然AEM平台使用将站点内容从创作复制到发布的节点存储区，但AEM Communities使用单个通用存储区来存储从未复制的UGC。

对于UGC存储，需要选择一个影响所选部署的存储资源提供程序(SRP)。
请参阅

* [社区内容存储](/help/communities/working-with-srp.md)
* [推荐的社区拓扑](/help/communities/topologies.md)
