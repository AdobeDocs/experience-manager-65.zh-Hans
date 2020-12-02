---
title: 复制疑难解答
seo-title: 复制疑难解答
description: 本文提供了有关如何解决复制问题的信息。
seo-description: 本文提供了有关如何解决复制问题的信息。
uuid: 1662bf60-b000-4eb2-8834-c6da607128fe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 0d055be7-7189-4587-8c7c-2ce34e22a6ad
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 0%

---


# 复制故障排除{#troubleshooting-replication}

本页提供有关如何解决复制问题的信息。

## 问题{#problem}

复制（非反向复制）因某种原因失败。

## 分辨率 {#resolution}

复制失败有多种原因。 本文阐述了在分析这些问题时可能采取的方法。

**单击激活按钮时，复制是否会被触发？如果不是，则执行以下操作：**

1. 转到/crx/explorer并以管理员身份登录。
1. 打开“内容浏览器”
1. 查看节点/bin/replicate或/bin/replicate.json是否存在。 如果节点存在，则删除该节点并保存。

**复制是否正在复制代理队列中排队？**

请转到/etc/replication/agents.author.html，然后单击复制代理进行检查，以检查此问题。

**如果一个代理队列或几个代理队列被卡住：**

1. 队列是否显示&#x200B;**blocked**&#x200B;状态？ 如果是，则发布实例未运行或完全无响应？ 检查发布实例以查看其错误（即检查日志，并查看是否存在OutOfMemory错误或其他问题）。 然后，如果速度通常比较慢，则进行线程转储并分析。
1. 队列状态是否显示&#x200B;**队列处于活动状态- # pending**? 基本上，复制作业可能会卡在套接字读取中，等待发布实例或调度程序做出响应。 这可能意味着发布实例或调度程序处于高负载状态或卡在锁中。 从作者处获取线程转储，并在此情况下发布。

   * 在线程转储分析器中，从作者打开线程转储，检查复制代理的sling事件作业是否卡在socketRead中。
   * 在线程转储分析器中从发布打开线程转储，分析可能导致发布实例不响应的原因。 您应当看到名称中带有/bin/receivePOST的线程，即从作者处接收复制的线程。

**如果所有代理队列都卡住**

1. 由于存储库损坏或某些其他问题，某段内容可能无法在/var/replication/data下序列化。 检查logs/error.log中是否有相关错误。 要清除错误的复制项，请执行以下操作：

   1. 转到https://&lt;host>:&lt;port>/crx/de并以管理员用户身份登录。
   1. 单击顶部菜单中的“工具”。
   1. 单击放大镜按钮。
   1. 选择“XPath”作为类型。
   1. 在“查询”框中，输入@slingevent:created的此查询/jcr:root/var/eventing/jobs//element(*,slingevent:Job)顺序
   1. 单击“搜索”
   1. 在结果中，最热门的项目是最新的sling事件作业。 单击每个副本，找到与队列顶部显示的内容匹配的卡住的复制。

1. sling事件框架作业队列可能有问题。 尝试在/system/console中重新启动org.apache.sling.事件包。
1. 可能是作业处理完全关闭。 您可以在Felix Console下的Sling Eventing选项卡中检查该设置。 检查它是否显示- Apache Sling Eventing(JOB PROCESSING IS DISABLED!)

   * 如果是，则检查Felix控制台的“配置”选项卡下的Apache Sling作业事件处理程序。 可能是未选中“已启用作业处理”复选框。 如果已选中，但仍显示“作业处理已禁用”，则请检查/apps/system/config下是否存在正在禁用作业处理的任何叠加。 尝试为jobmanager.enabled创建一个osgi:config节点，将布尔值设置为true，然后重新检查激活是否启动以及队列中没有更多作业。

1. DefaultJobManager配置也可能进入不一致状态。 当某人通过OSGiconsole手动修改“Apache Sling作业事件处理程序”配置时（例如，禁用并重新启用“已启用作业处理”属性并保存配置），会发生这种情况。

   * 此时，存储在crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config的DefaultJobManager配置将进入不一致状态。 即使“Apache Sling作业事件处理程序”属性显示“已启用作业处理”处于选中状态，当您导航到Sling事件选项卡时，也会显示消息- JOB PROCESSING IS DISABLED，且复制不工作。
   * 要解决此问题，您需要导航到OSGi控制台的“配置”页并删除“Apache Sling作业事件处理程序”配置。 然后重新启动群集的主控节点，使配置恢复到一致状态。 这应该可以修复问题，复制将再次开始工作。

**创建replication.log**

有时，将所有复制日志记录设置为在DEBUG级别的单独日志文件中会非常有用。 要执行此操作：

1. 转到https://host:port/system/console/configMgr并以管理员身份登录。
1. 查找Apache Sling Logging Logger工厂，并通过单击工厂配置右侧的&#x200B;**+**&#x200B;按钮创建一个实例。 这将创建新的日志记录记录器。
1. 设置如下配置：

   * 日志级别：调试
   * 日志文件路径：logs/replication.log
   * 类别:com.day.cq.replication

1. 如果您怀疑此问题与sling事件／作业有关，则还可以在类别:org.apache.sling.事件下添加此java包

## 暂停复制代理队列{#pausing-replication-agent-queue}

有时，它可能适合暂停复制队列以减少创作系统上的负载，而不禁用它。 目前，只有通过临时配置无效端口才能实现此操作。 从5.4开始，您可以看到复制代理队列中的暂停按钮有一些限制

1. 状态不会持久，这意味着如果重新启动服务器或复制捆绑包被循环使用，它将返回运行状态。
1. 暂停的空闲时间较短(在没有其他线程复制的活动后1小时，OOB为空)，而不是更长的时间。 因为吊具有避免空闲线的功能。 基本上，检查作业队列线程是否已使用较长时间，如果这样，它将启动清理循环。 由于清理周期，它会停止线程，因此暂停的设置会丢失。 由于作业被保留，因此会启动一个新线程来处理没有暂停配置详细信息的队列。 由于此队列变为运行状态。

## 用户激活{#page-permissions-are-not-replicated-on-user-activation}上未复制页面权限

页面权限不会复制，因为它们存储在授予访问权限的节点下，而不存储在用户下。

一般情况下，页面权限不应从作者复制到发布，默认情况下不应复制。 这是因为这两个环境的访问权限应不同。 因此，建议在发布时单独配置ACL（与作者分开配置）。

## 将命名空间信息从作者复制到发布{#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}时，复制队列被阻止

在某些情况下，当尝试将命名空间信息从创作实例复制到发布实例时，复制队列会被阻止。 这是因为复制用户没有`jcr:namespaceManagement`权限。 要避免此问题，请确保：

* 复制用户（如[传输](/help/sites-deploying/replication.md#replication-agents-configuration-parameters)选项卡>用户下配置）也存在于发布实例中。
* 用户在安装内容的路径上具有读写权限。
* 用户在存储库级别具有`jcr:namespaceManagement`权限。 您可以按如下方式授予权限：

1. 以管理员身份登录到CRX/DE(`https://localhost:4502/crx/de/index.jsp`)。
1. 单击&#x200B;**访问控制**&#x200B;选项卡。
1. 选择&#x200B;**存储库**。
1. 单击&#x200B;**添加条目**（加号图标）。
1. 输入用户的名称。
1. 从权限列表中选择`jcr:namespaceManagement`。
1. 单击确定。

