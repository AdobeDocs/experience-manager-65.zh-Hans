---
title: 操作仪表板
seo-title: 操作仪表板
description: 了解如何使用“操作”仪表板。
seo-description: 了解如何使用“操作”仪表板。
uuid: ef24813f-a7a8-4b26-a496-6f2a0d9efef6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: b210f5d7-1d68-49ee-ade7-667c6ab11d2b
docset: aem65
exl-id: f9a88156-91a2-4c85-9bc9-8f23700c2cbd
feature: Operations
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '6199'
ht-degree: 2%

---

# 操作仪表板{#operations-dashboard}

## 简介 {#introduction}

AEM 6中的操作仪表板可帮助系统操作员一目了然地监控AEM系统运行状况。 它还提供有关AEM相关方面的自动生成的诊断信息，并允许配置和运行自包含的维护自动化，以显着减少项目操作和支持案例。 “操作”仪表板可通过自定义运行状况检查和维护任务进行扩展。 此外，操作仪表板数据可以通过JMX从外部监视工具访问。

**操作仪表板:**

* 是一键式系统状态，可帮助运营部门提高效率
* 在一个集中的位置提供系统运行状况概述
* 缩短查找、分析和修复问题的时间
* 提供自带的维护自动化功能，有助于显着降低项目运营成本

可以从AEM欢迎屏幕转至&#x200B;**Tools** - **Operations**&#x200B;访问它。

>[!NOTE]
>
>要能够访问“操作”仪表板，登录用户必须是“操作员”用户组的一部分。 有关详细信息，请参阅[用户、组和访问权限管理](/help/sites-administering/user-group-ac-admin.md)的相关文档。

## 健康报表 {#health-reports}

运行状况报告系统通过Sling运行状况检查提供有关AEM实例运行状况的信息。 这可以通过OSGI、JMX、HTTP请求（通过JSON）或通过触屏UI来完成。 它优惠某些可配置计数器的度量值和阈值，在某些情况下，它将优惠有关如何解决该问题的信息。

它具有以下几个功能。

## 运行状况检查 {#health-checks}

**运行状况报告**&#x200B;是一个卡系统，表明特定产品区域的运行状况良好或不良。 这些卡是Sling运行状况检查的可视化，它将来自JMX和其他源的数据聚合，并再次将处理的信息显示为MBean。 这些MBean还可以在[JMX Web控制台](/help/sites-administering/jmx-console.md)中的&#x200B;**org.apache.sling.healthcheck**&#x200B;域下进行检查。

运行状况报告界面可通过AEM欢迎屏幕上的&#x200B;**工具** - **操作** - **运行状况报告**&#x200B;菜单访问，或直接通过以下URL访问：

`https://<serveraddress>:port/libs/granite/operations/content/healthreports/healthreportlist.html`

![chlimage_1-116](assets/chlimage_1-116.png)

卡系统显示三种可能的状态：**确定**、**警告**&#x200B;和&#x200B;**关键**。 这些状态是规则和阈值的结果，可以通过将鼠标悬停在卡上并单击操作栏中的齿轮图标来配置规则和阈值：

![chlimage_1-117](assets/chlimage_1-117.png)

### 运行状况检查类型{#health-check-types}

AEM 6中有两种类型的运行状况检查：

1. 个人运行状况检查
1. 综合运行状况检查

**单个运行状况检查**&#x200B;是与状态卡对应的单个运行状况检查。 单个运行状况检查可以配置规则或阈值，并且它们可以提供一个或多个提示和链接来解决已识别的运行状况问题。 让我们以“日志错误”检查为例：如果实例日志中有ERROR项，您将在运行状况检查的详细信息页面上找到它们。 在页面顶部，您将在“诊断工具”部分看到指向“日志消息”分析器的链接，该链接使您能够更详细地分析这些错误并重新配置日志程序。

**复合运行状况检查**&#x200B;是一个检查，它聚合了多个单独检查中的信息。

综合运行状况检查是使用&#x200B;**过滤器标签**&#x200B;来配置的。 本质上，具有相同过滤器标签的所有单个检查都将分组为复合运行状况检查。 仅当聚合的所有单个检查都具有“OK”状态时，“Composite Health Check”（综合运行状况检查）才会具有“OK”状态。

### 如何创建运行状况检查{#how-to-create-health-checks}

在“操作”仪表板中，您可以直观地显示单个运行状况检查和复合运行状况检查的结果。

### 创建单个运行状况检查{#creating-an-individual-health-check}

创建单个运行状况检查涉及两个步骤：实施Sling运行状况检查，并在仪表板的配置节点中添加运行状况检查项。

1. 要创建Sling运行状况检查，您需要创建一个实现Sling HealthCheck界面的OSGI组件。 您将将此组件添加到捆绑包中。 组件的属性将完全标识运行状况检查。 安装该组件后，将自动为运行状况检查创建JMX MBean。 有关详细信息，请参阅[Sling运行状况检查文档](https://sling.apache.org/documentation/bundles/sling-health-check-tool.html)。

   Sling运行状况检查组件示例（使用OSGI服务组件注释编写）：

   ```java
   @Component(service = HealthCheck.class,
   property = {
       HealthCheck.NAME + "=Example Check",
       HealthCheck.TAGS + "=example",
       HealthCheck.TAGS + "=test",
       HealthCheck.MBEAN_NAME + "=exampleHealthCheckMBean"
   })
    public class ExampleHealthCheck implements HealthCheck {
       @Override
       public Result execute() {
           // health check code
       }
    }
   ```

   >[!NOTE]
   >
   >`MBEAN_NAME`属性定义将为此运行状况检查生成的mbean的名称。

1. 创建运行状况检查后，需要创建新的配置节点，以便在“操作”仪表板界面中访问该节点。 对于此步骤，必须知道运行状况检查的JMX Mbean名称（`MBEAN_NAME`属性）。 要为运行状况检查创建配置，请打开CRXDE并在以下路径下添加新节点（类型为&#x200B;**nt:unstructured**）：`/apps/settings/granite/operations/hc`

   应在新节点上设置以下属性：

   * **名称:** `sling:resourceType`

      * **类型:** `String`
      * **值：** `granite/operations/components/mbean`
   * **名称:** `resource`

      * **类型:** `String`
      * **值：** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/exampleHealthCheck`

   >[!NOTE]
   >
   >上面的资源路径如下所示：如果运行状况检查的mbean名称为“test”，则在路径`/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck`的末尾添加“test”
   >
   >因此，最终的路径将是：
   >
   >`/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/test`

   >[!NOTE]
   >
   >确保`/apps/settings/granite/operations/hc`路径的以下属性设置为true:
   >
   >
   >`sling:configCollectionInherit`
   >
   >`sling:configPropertyInherit`
   >
   >
   >这将告诉配置管理器将新配置与`/libs`的现有配置合并。

### 创建复合运行状况检查{#creating-a-composite-health-check}

“复合运行状况检查”的角色是聚合多个共享一组常见功能的独立运行状况检查。 例如，“安全复合运行状况检查”将执行与安全相关的验证的所有单个运行状况检查组合在一起。 创建复合检查的第一步是添加新的OSGI配置。 要在“操作”仪表板中显示该节点，需要添加一个新的配置节点，这与我们为简单检查所做的相同。

1. 转到OSGI控制台中的Web配置管理器。 可通过访问`https://serveraddress:port/system/console/configMgr`
1. 搜索名为&#x200B;**Apache Sling Composite Health Check**&#x200B;的条目。 找到它后，请注意已有两种可用配置：一个用于系统检查，另一个用于安全检查。
1. 通过按配置右侧的“+”按钮创建新配置。 将显示一个新窗口，如下所示：

   ![chlimage_1-23](assets/chlimage_1-23.jpeg)

1. 创建配置并保存。 将使用新配置创建Mbean。

   每个配置属性的用途如下：

   * **名称(hc.name):** 复合运行状况检查的名称。建议使用有意义的名称。
   * **标记(hc.tags)：此** 运行状况检查的标记。如果此复合运行状况检查旨在成为另一个复合运行状况检查的一部分（例如，在运行状况检查的层次结构中），请添加此复合所关联的标记。
   * **MBean名称(hc.mbean.name):** 将给此复合运行状况检查的JMX MBean的Mbean的名称。
   * **过滤器标签(filter.tags):** 这是特定于复合运行状况检查的属性。这些是合成应聚合的标记。 复合运行状况检查将在其组下聚合所有具有任何与此复合的任何过滤器标签匹配的标签的运行状况检查。 例如，具有过滤器标签&#x200B;**test**&#x200B;和&#x200B;**check**&#x200B;的复合健康检查将聚合其标签属性(`hc.tags`)中具有任何&#x200B;**test**&#x200B;和&#x200B;**check**&#x200B;标签的所有个人和复合健康检查。

   >[!NOTE]
   >
   >将为Apache Sling Composite运行状况检查的每个新配置创建一个新的JMX Mbean。**

1. 最后，需要在“操作”仪表板配置节点中添加刚刚创建的复合运行状况检查项。 此过程与单个运行状况检查的过程相同：需要在`/apps/settings/granite/operations/hc`下创建类型为&#x200B;**nt:unstructured**&#x200B;的节点。 节点的资源属性将由OSGI配置中的&#x200B;**hc.mean.name**&#x200B;值定义。

   例如，如果您创建了配置并将&#x200B;**hc.mbean.name**&#x200B;值设置为&#x200B;**diskusage**，则配置节点将如下所示：

   * **名称:** `Composite Health Check`

      * **类型:** `nt:unstructured`

   具有以下属性：

   * **名称:** `sling:resourceType`

      * **类型:** `String`
      * **值：** `granite/operations/components/mbean`
   * **名称:** `resource`

      * **类型:** `String`
      * **值：** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/diskusage`

   >[!NOTE]
   >
   >如果您创建逻辑上属于复合检查的各个运行状况检查(默认情况下，该复合检查已存在于仪表板中)，它们将自动捕获并分组在相应的复合检查下。 因此，无需为这些检查创建新的配置节点。
   >
   >例如，如果您创建了单个安全运行状况检查，您只需为它分配“**security**”标签，它就已安装，它将自动显示在“操作”仪表板的“安全检查”复合检查下。

### 随AEM {#health-checks-provided-with-aem}提供的运行状况检查

<table>
 <tbody>
  <tr>
   <td><strong>zHealthcheck名称</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>查询性能</td>
   <td><p>在AEM 6.4</strong>中，此运行状况检查已简化<strong>，现在检查最近重构的<code>Oak QueryStats</code> MBean，更具体地说是<code>SlowQueries </code>属性。 如果统计数据包含任何慢速查询，运行状况检查将返回警告。 否则，返回“确定”状态。<br /> </strong></p> <p>此运行状况检查的MBean是<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueriesStatus%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=querysStatus，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>观察队列长度</td>
   <td><p>观察队列长度迭代所有事件监听器和后台观察器，将其<code>queueSize </code>与其<code>maxQueueSize</code>进行比较，并：</p>
    <ul>
     <li>如果<code>queueSize</code>值超过<code>maxQueueSize</code>值(即删除事件时)，则返回关键状态</li>
     <li>如果<code>queueSize</code>值位于<code>maxQueueSize * WARN_THRESHOLD</code>上方（默认值为0.75），则返回警告 </li>
    </ul> <p>每个队列的最大长度来自不同的配置(Oak和AEM)，不能通过此运行状况检查进行配置。 此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DObservationQueueLengthHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=OvertationQueueLengthHealthCheck，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>查询遍历限制</td>
   <td><p>查询遍历限制检查<code>QueryEngineSettings</code> MBean，更确切地说是<code>LimitInMemory</code>和<code>LimitReads</code>属性，并返回以下状态：</p>
    <ul>
     <li>如果其中一个限制等于或高于 <code>Integer.MAX_VALUE</code></li>
     <li>如果其中一个限制低于10000（Oak的推荐设置），则返回“警告”状态</li>
     <li>如果无法检索<code>QueryEngineSettings</code>或任何限制，则返回“严重”状态</li>
    </ul> <p>此运行状况检查的Mbean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueryTraversalLimitsBundle%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=queryTraveralLimitsBundle，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>同步的时钟</td>
   <td><p>此检查仅与<a href="https://github.com/apache/sling-old-svn-mirror/blob/4df9ab2d6592422889c71fa13afd453a10a5a626/bundles/extensions/discovery/oak/src/main/java/org/apache/sling/discovery/oak/SynchronizedClocksHealthCheck.java">文档nodestore群集</a>相关。 它返回以下状态：</p>
    <ul>
     <li>当实例时钟不同步并超过预定义的低阈值时，返回“警告”状态</li>
     <li>当实例时钟不同步并超过预定义的高阈值时，返回“关键”状态</li>
    </ul> <p>此运行状况检查的Mbean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingDiscoveryOakSynchronizedClocks%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=slingDiscoveryOakSynchronizedCloks，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>异步索引</td>
   <td><p>异步索引检查：</p>
    <ul>
     <li>返回至少一个索引通道失败时的关键状态</li>
     <li>检查<code>lastIndexedTime</code>的所有索引通道和：
      <ul>
       <li>如果超过2小时前返回关键状态 </li>
       <li>如果在2小时到45分钟之前，则返回警告状态 </li>
       <li>如果45分钟前不到，则返回“确定”状态 </li>
      </ul> </li>
     <li>如果未满足这些条件，则返回“确定”状态</li>
    </ul> <p>“严重”和“警告”状态阈值都可配置。 此运行状况检查的Mbean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DasyncIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=asyncIndexHealthCheck，type=HealthCheck</a>。</p> <p><strong>注意： </strong>此运行状况检查可在AEM 6.4中使用，并已支持到AEM 6.3.0.1。</p> </td>
  </tr>
  <tr>
   <td>大型 Lucene 索引</td>
   <td><p>此检查使用<code>Lucene Index Statistics</code> MBean公开的数据来标识大索引并返回：</p>
    <ul>
     <li>如果有10亿以上文档的指数</li>
     <li>a如果有一个指数超过15亿文档</li>
    </ul> <p>可以配置阈值，运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlargeIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=largeIndexHealthCheck，type=HealthCheck。</a></p> <p><strong>注意： </strong>此检查在AEM 6.4中可用，并已支持到AEM 6.3.2.0。</p> </td>
  </tr>
  <tr>
   <td>系统维护</td>
   <td><p>系统维护是一个复合检查，如果所有维护任务都按配置运行，则返回“确定”。 请记住：</p>
    <ul>
     <li>每个维护任务都附带相关的运行状况检查</li>
     <li>如果任务未添加到维护窗口，其运行状况检查将返回“关键”</li>
     <li>您需要配置“审核日志”和“工作流清除”维护任务，或以其他方式从维护窗口中删除它们。 如果未配置，这些任务将在第一次尝试运行时失败，因此系统维护检查将返回“严重”状态。</li>
     <li><strong>对于AEM 6.4</strong>，还会检查Lucene二进制文 <a href="/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks">件维护任</a> 务</li>
     <li>在AEM 6.2和更低版本上，系统维护检查会在启动后立即返回“警告”状态，因为任务从不运行。 从6.3开始，如果尚未到达第一个维护窗口，他们将返回“OK（确定）”。</li>
    </ul> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsystemchecks%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=systemchecks，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>复制队列</td>
   <td><p>此检查重复复制代理并查看其队列。 对于队列顶部的项，检查将查看代理重试复制的次数。 如果代理重试的复制次数超过<code>numberOfRetriesAllowed</code>参数的值，则会返回警告。 可配置<code>numberOfRetriesAllowed</code>参数。 </p> <p>此运行状况检查的MBean是<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DreplicationQueue%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=replicationQueue，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>Sling 作业</td>
   <td>
    <div>
      Sling Jobs会检查在JobManager中排队的作业数，并将其与
     <code>maxNumQueueJobs</code>阈值和：
    </div>
    <ul>
     <li>如果队列中的<code>maxNumQueueJobs</code>以上，则返回关键</li>
     <li>如果存在运行时间长于1小时的活动作业，则返回关键</li>
     <li>如果存在排队的作业，且上次完成的作业时间大于1小时，则返回关键</li>
    </ul> <p>只能配置排队作业参数的最大数量，其默认值为1000。</p> <p>此运行状况检查的MBean是<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingJobs%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=slingJobs，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>请求性能</td>
   <td><p>此检查查看<code>granite.request.metrics.timer</code> <a href="http://localhost:4502/system/console/slingmetrics" target="_blank">Sling量度</a>和：</p>
    <ul>
     <li>如果第75百分点值超过临界阈值（默认值为500毫秒），则返回临界值</li>
     <li>返回当第75百分点值超过警告阈值时发出警告（默认值为200毫秒）</li>
    </ul> <p>此运行状况检查的MBean为<em> </em><a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DrequestsStatus%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=requestsStatus，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>日志错误</td>
   <td><p>如果日志中有错误，此检查将返回“警告”状态。</p> <p>此运行状况检查的MBean是<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlogErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=logErrorHealthCheck，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>磁盘空间</td>
   <td><p>磁盘空间检查会查看<code>FileStoreStats</code> MBean，检索节点存储的大小和节点存储分区上的可用磁盘空间量，并：</p>
    <ul>
     <li>如果可用磁盘空间与存储库大小的比率小于警告阈值（默认值为10），则返回警告</li>
     <li>如果可用磁盘空间与存储库大小的比率小于关键阈值（默认值为2），则返回关键</li>
    </ul> <p>这两个阈值都可配置。 此检查仅适用于具有区段存储的实例。</p> <p>此运行状况检查的MBean是<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DDiskSpaceHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=DiskSpaceHealthCheck，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>计划程序运行状况检查</td>
   <td><p>如果实例的Quartz作业运行时间超过60秒，则此检查将返回警告。 可配置可接受的持续时间阈值。</p> <p>此运行状况检查的MBean是<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingCommonsSchedulerHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=slingCommonsSchedulerHealthCheck，type=HealthCheck</a><em>。</em></p> </td>
  </tr>
  <tr>
   <td>安全检查</td>
   <td><p>“安全”检查是一个组合，它聚合多个与安全相关的检查的结果。 这些单独的运行状况检查解决了与<a href="/help/sites-administering/security-checklist.md">安全清单文档页上提供的安全清单不同的问题。</a> 在启动实例时，该检查可用作安全烟雾测试。 </p> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsecuritychecks%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=securitychecks，type=HealthCheck</a></p> </td>
  </tr>
  <tr>
   <td>活动包</td>
   <td><p>活动包检查所有包的状态，并：</p>
    <ul>
     <li>返回“警告”状态(如果任何包不活动，或(以延迟激活开始)</li>
     <li>它忽略忽略忽略列表中的包状态</li>
    </ul> <p>可以配置忽略列表参数。</p> <p>此运行状况检查的MBean是<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DinactiveBundles%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=inactiveBundles，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>代码缓存检查</td>
   <td><p>这是运行状况检查，它验证若干JVM条件，这些JVM条件可触发Java 7中存在的CodeCache错误：</p>
    <ul>
     <li>返回在启用代码缓存刷新的Java 7上运行实例时发出警告</li>
     <li>返回警告，如果实例在Java 7上运行，且保留代码缓存大小小于最小阈值（默认值为90MB）</li>
    </ul> <p>可配置<code>minimum.code.cache.size</code>阈值。 有关此错误的详细信息，请<a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547">检查</a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547"></a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547"></a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547">此页</a>。</p> <p>此运行状况检查的MBean是<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DcodeCacheHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=codeCacheHealthCheck，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>资源搜索路径错误</td>
   <td><p>检查路径<code>/apps/foundation/components/primary</code>中是否有任何资源，并：</p>
    <ul>
     <li>返回在子节点位于 <code>/apps/foundation/components/primary</code></li>
    </ul> <p>此运行状况检查的MBean是<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DresourceSearchPathErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=resourceSearchPathErrorHealthCheck，type=HealthCheck</a>。</p> </td>
  </tr>
 </tbody>
</table>

## 使用Nagios {#monitoring-with-nagios}进行监视

运行状况检查仪表板可以通过Granite JMX Mbeans与Nagios集成。 以下示例说明如何在运行AEM的服务器上添加显示已使用内存的检查。

1. 在监视服务器上安装和安装Nagios。
1. 然后，安装Nagios Remote Plugin Executor(NRPE)。

   >[!NOTE]
   >
   >有关如何在系统上安装Nagios和NRPE的详细信息，请查阅[Nagios文档](https://library.nagios.com/library/products/nagioscore/manuals/)。

1. 为AEM服务器添加主机定义。 这可以通过Nagios XI Web界面使用配置管理器来完成：

   1. 打开浏览器并指向Nagios服务器。
   1. 按顶部菜单中的&#x200B;**配置**&#x200B;按钮。
   1. 在左窗格中，按&#x200B;**高级配置**&#x200B;下的&#x200B;**核心配置管理器**。
   1. 按&#x200B;**监视**&#x200B;部分下的&#x200B;**主机**&#x200B;链接。
   1. 添加主机定义：

   ![chlimage_1-118](assets/chlimage_1-118.png)

   以下是主机配置文件的示例，如果您使用的是Nagios Core:

   ```xml
   define host {
      address 192.168.0.5
      max_check_attempts 3
      check_period 24x7
      check-command check-host-alive
      contacts admin
      notification_interval 60
      notification_period 24x7
   }
   ```

1. 在AEM服务器上安装Nagios和NRPE。
1. 在两台服务器上安装[check_http_json](https://github.com/phrawzty/check_http_json)插件。
1. 在两台服务器上定义通用JSON check命令：

   ```xml
   define command{
   
       command_name    check_http_json-int
   
       command_line    /usr/lib/nagios/plugins/check_http_json --user "$ARG1$" --pass "$ARG2$" -u 'https://$HOSTNAME$:$ARG3$/$ARG4$' -e '$ARG5$' -w '$ARG6$' -c '$ARG7$'
   
   }
   ```

1. 在AEM服务器上为已用内存添加服务：

   ```xml
   define service {
   
       use generic-service
   
       host_name my.remote.host
   
       service_description AEM Author Used Memory
   
       check_command  check_http_json-int!<cq-user>!<cq-password>!<cq-port>!system/sling/monitoring/mbeans/java/lang/Memory.infinity.json!{noname}.mbean:attributes.HeapMemoryUsage.mbean:attributes.used.mbean:value!<warn-threshold-in-bytes>!<critical-threshold-in-bytes>
   
       }
   ```

1. 检查您的Nagios仪表板以了解新创建的服务：

   ![chlimage_1-119](assets/chlimage_1-119.png)

## 诊断工具{#diagnosis-tools}

操作仪表板还提供对诊断工具的访问，这些工具可以帮助查找和排除来自运行状况检查仪表板的警告的根本原因，并为系统操作员提供重要的调试信息。

其最重要的功能包括：

* 日志消息分析器
* 能够访问堆和线程转储
* 请求和查询性能分析器

可从AEM欢迎屏幕转至&#x200B;**工具 — 操作 — 诊断**，进入诊断工具屏幕。 您还可以通过直接访问以下URL来访问屏幕：`https://serveraddress:port/libs/granite/operations/content/diagnosis.html`

![chlimage_1-120](assets/chlimage_1-120.png)

### 日志消息{#log-messages}

默认情况下，日志消息用户界面将显示所有ERROR消息。 如果要显示更多日志消息，您需要配置具有相应日志级别的记录器。

日志消息使用内存日志附加器，因此与日志文件无关。 另一个结果是更改此UI中的日志级别不会更改传统日志文件中记录的信息。 在此UI中添加和删除记录器将仅影响内存记录器。 另外，请注意，更改记录器配置将反映在内存记录器的将来 — 不删除已记录且不再相关的条目，但类似条目将来不会记录。

您可以通过在UI中从左上角的齿轮按钮提供记录器配置来配置记录器。 您可以在此处添加、删除或更新记录器配置。 记录器配置由&#x200B;**日志级别**(WARN / INFO / DEBUG)和&#x200B;**过滤器名称**&#x200B;组成。 **筛选器名称**&#x200B;具有筛选日志消息源的角色。 或者，如果记录器应捕获指定级别的所有日志消息，则过滤器名称应为“**root**”。 设置记录器的级别将触发所有消息的捕获，其级别等于或高于指定的级别。

示例：

* 如果您计划捕获所有&#x200B;**ERROR**&#x200B;消息 — 不需要配置。 默认情况下会捕获所有ERROR消息。
* 如果计划捕获所有&#x200B;**ERROR**、**WARN**&#x200B;和&#x200B;**INFO**&#x200B;消息，应将记录器名称设置为：&quot;**root**&quot;，记录器级别为：**信息**。

* 如果您计划捕获来自某个包的所有消息（例如com.adobe.granite） — 应将记录器名称设置为：“com.adobe.granite”和记录器级别：**DEBUG**（这将捕获所有&#x200B;**ERROR**、**WARN**、**INFO**&#x200B;和&#x200B;**DEBUG**&#x200B;消息），如下图所示。

![chlimage_1-121](assets/chlimage_1-121.png)

>[!NOTE]
>
>无法设置记录器名称以通过指定的过滤器仅捕获ERROR消息。 默认情况下，将捕获所有ERROR消息。

>[!NOTE]
>
>日志消息用户界面不反映实际错误日志。 除非您在UI中配置其他类型的日志消息，否则只会显示错误消息。 有关如何显示特定日志消息的信息，请参阅上面的说明。

>[!NOTE]
>
>诊断页面中的设置不会影响记录到日志文件的内容，反之亦然。 因此，尽管错误日志可能会捕获INFO消息，但您可能在日志消息UI中看不到这些消息。 此外，通过UI，可以从某些包中捕获DEBUG消息，而不会影响错误日志。 有关如何配置日志文件的详细信息，请参阅[日志记录](/help/sites-deploying/configure-logging.md)。

>[!NOTE]
>
>**在AEM 6.4中**，维护任务将以INFO级别的更多富信息格式从开箱即用。这使得能够更好地查看维护任务的状态。
>
>如果您使用第三方工具（如Splunk）来监视和响应维护任务活动，则可以使用以下日志语句：

```
Log level: INFO
DATE+TIME [MaintanceLogger] Name=<MT_NAME>, Status=<MT_STATUS>, Time=<MT_TIME>, Error=<MT_ERROR>, Details=<MT_DETAILS>
```

### 请求性能{#request-performance}

“请求性能”页允许分析处理的最慢页面请求。 此页面上只会注册内容请求。 具体而言，将捕获以下请求：

1. 访问`/content`下的资源的请求
1. 访问`/etc/design`下的资源的请求
1. 具有`".html"`扩展的请求

![chlimage_1-122](assets/chlimage_1-122.png)

此时将显示页面：

* 发出请求的时间
* URL和请求方法
* 持续时间（以毫秒为单位）

默认情况下，捕获最慢的20个页面请求，但可以在配置管理器中修改此限制。

### 查询性能{#query-performance}

“查询性能”页允许分析系统执行的最慢查询。 此信息由JMX Mbean中的存储库提供。 在Jackrabbit中，`com.adobe.granite.QueryStat` JMX Mbean提供此信息，而在Oak存储库中，它由`org.apache.jackrabbit.oak.QueryStats.`提供

此时将显示页面：

* 创建查询的时间
* 查询语
* 发布查询的次数
* 查询
* 持续时间（以毫秒为单位）

![chlimage_1-123](assets/chlimage_1-123.png)

### 说明查询 {#explain-query}

对于任何给定查询,Oak都会尝试根据存储库中&#x200B;**oak:index**&#x200B;节点下定义的Oak索引找出最佳执行方式。 根据查询,Oak可以选择不同的索引。 了解Oak如何执行查询是优化查询的第一步。

“解释查询”是一个工具，用于解释Oak如何执行查询。 可以通过从AEM欢迎屏幕转至&#x200B;**工具 — 操作 — 诊断**，然后单击&#x200B;**查询性能**&#x200B;并切换至&#x200B;**说明查询**&#x200B;选项卡来访问它。

**功能**

* 支持Xpath、JCR-SQL和JCR-SQL2查询语言
* 报告提供查询的实际执行时间
* 检测慢速查询并警告可能慢速的查询
* 报告用于执行查询的Oak索引
* 显示实际Oak查询引擎说明
* 提供慢速和常用查询的点击加载列表

进入解释查询UI后，只需输入查询并按&#x200B;**说明**&#x200B;按钮即可使用：

![chlimage_1-124](assets/chlimage_1-124.png)

“查询说明”部分中的第一个条目是实际说明。 说明将显示用于执行查询的索引类型。

第二个条目是执行计划。

在运行查询之前，按&#x200B;**包含执行时间**&#x200B;框键还将显示查询的执行时间，以便提供可用于优化应用程序或部署的索引的详细信息。

![chlimage_1-125](assets/chlimage_1-125.png)

### 索引管理器{#the-index-manager}

索引管理器的目的是促进索引管理，如维护索引或查看索引的状态。

可从欢迎屏幕转至**工具 — 操作 — 诊断**，然后单击&#x200B;**索引管理器**&#x200B;按钮访问。

也可以通过以下URL直接访问它：`https://serveraddress:port/libs/granite/operations/content/diagnosistools/indexManager.html`

![screen-shot_2019-06-18at154754](assets/screen-shot_2019-06-18at154754.png)

UI可用于通过在屏幕左上角的搜索框中键入筛选条件来筛选表中的索引。

### 下载状态ZIP {#download-status-zip}

这将触发下载包含系统状态和配置的有用信息的zip文件。 存档包含实例配置、捆绑包列表、OSGI、Sling量度和统计信息，这可能导致大文件。 您可以使用&#x200B;**下载状态ZIP**&#x200B;窗口来减少大型状态文件的影响。 该窗口可从以下位置访问：**AEM >工具>操作>诊断>下载状态ZIP。**

在此窗口中，您可以选择要导出的内容（日志文件和线程转储）以及下载中包含的相对于当前日期的日志天数。

![download_status_zip](assets/download_status_zip.png)

### 下载线程转储{#download-thread-dump}

这将触发下载包含系统中线程相关信息的zip文件。 提供了有关每个线程的信息，如其状态、类加载器和堆栈跟踪。

### 下载堆转储{#download-heap-dump}

您还可以下载堆的快照，以便在以后分析它。 请注意，这将触发以数百兆字节顺序下载的大型文件。

## 自动维护任务{#automated-maintenance-tasks}

“自动维护任务”页是您可以视图和跟踪计划定期执行的推荐维护任务的位置。 任务与运行状况检查系统集成。 也可以从接口手动执行任务。

要转到“操作”仪表板中的“维护”页，您需要从AEM欢迎屏幕转至&#x200B;**工具 — 操作 — 仪表板 — 维护**，或直接遵循以下链接：

`https://serveraddress:port/libs/granite/operations/content/maintenance.html`

“操作”仪表板中提供了以下任务:

1. 位于&#x200B;**每日维护窗口**&#x200B;菜单下的&#x200B;**修订清理**&#x200B;任务。
1. **Lucene二进制文件清理**&#x200B;任务，位于&#x200B;**每日维护窗口**&#x200B;菜单下。
1. 位于&#x200B;**每周维护窗口**&#x200B;菜单下的&#x200B;**工作流清除**&#x200B;任务。
1. **数据存储垃圾收集**&#x200B;任务，位于&#x200B;**每周维护窗口**&#x200B;菜单下。
1. **审核日志维护**&#x200B;任务，位于&#x200B;**每周维护窗口**&#x200B;菜单下。
1. **版本清除维护**&#x200B;任务，位于&#x200B;**每周维护窗口**&#x200B;菜单下。

每日维护窗口的默认时间是凌晨2点到5点。 配置为在每周维护窗口中运行的任务将在星期六的上午1点到凌晨2点之间执行。

您还可以通过按任意两个维护卡上的齿轮图标来配置时间：

![chlimage_1-126](assets/chlimage_1-126.png)

>[!NOTE]
>
>自AEM 6.1起，还可以将现有维护窗口配置为每月运行。

### 修订清理 {#revision-clean-up}

有关执行修订清理的详细信息，请参阅此专用文章](/help/sites-deploying/revision-cleanup.md)。[

### Lucene 二进制文件清理 {#lucene-binaries-cleanup}

通过使用Lucene二进制文件清理任务，可以清除lucene二进制文件并减少运行中的数据存储大小要求。 这是因为Lucene的二进制服务器服务器服务器服务器将每天重新申请，而不是以前对成功运行[数据存储垃圾收集](/help/sites-administering/data-store-garbage-collection.md)的依赖性。

虽然开发维护任务是为了减少与Lucene相关的修改垃圾，但运行任务时总体效率有所提高：

* 每周执行数据存储垃圾收集任务将更快地完成
* 它还可能略微提高AEM的整体性能

您可以从以下位置访问Lucene二进制文件清理任务:**AEM >工具>操作>维护>每日维护窗口> Lucene二进制文件清理**。

### 数据存储垃圾收集 {#data-store-garbage-collection}

有关数据存储垃圾收集的详细信息，请参阅专用的[文档页面](/help/sites-administering/data-store-garbage-collection.md)。

### 工作流清除{#workflow-purge}

工作流也可以从维护仪表板中清除。 要运行“工作流清除”任务，您需要：

1. 单击&#x200B;**每周维护窗口**&#x200B;页。
1. 在下一页中，单击&#x200B;**工作流清除**&#x200B;卡中的&#x200B;**播放**&#x200B;按钮。

>[!NOTE]
>
>有关工作流维护的详细信息，请参阅[此页](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances)。

### 审核日志维护{#audit-log-maintenance}

有关“审核日志维护”，请参阅[单独的文档页。](/help/sites-administering/operations-audit-log.md)

### 版本清除 {#version-purge}

您可以计划“版本清除”维护任务，以自动删除旧版本。 因此，这使手动使用[版本清除工具](/help/sites-deploying/version-purging.md)的需要降至最低。 您可以访问&#x200B;**“工具”>“操作”>“维护”>“每周维护窗口”**&#x200B;并执行以下步骤来计划和配置“版本清除”任务:

1. 单击&#x200B;**添加**&#x200B;按钮。
1. 从下拉菜单中选择&#x200B;**版本清除**。

   ![version_purge_maintenancetask](assets/version_purge_maintenancetask.png)

1. 要配置“版本清除”任务，请单击新创建的“版本清除”维护卡上的&#x200B;**gears**&#x200B;图标。

   ![version_purge_taskconfiguration](assets/version_purge_taskconfiguration.png)

**在AEM 6.4中**，您可以按如下方式停止版本清除维护任务:

* 自动 — 如果计划的维护窗口在任务完成之前关闭，则任务会自动停止。 在下一个维护窗口打开时，它将恢复。
* 手动 — 要手动停止任务，请在“版本清除”维护卡上单击&#x200B;**停止**&#x200B;图标。 下次执行时，任务将安全地恢复。

>[!NOTE]
>
>停止维护任务意味着暂停其执行，而不丢失对已在进行的作业的跟踪。

>[!CAUTION]
>
>为了优化存储库大小，您应经常运行版本清除任务。 任务应在业务时间以外安排，当流量有限时。

## 自定义维护任务{#custom-maintenance-tasks}

自定义维护任务可以作为OSGi服务实现。 由于维护任务基础架构基于Apache Sling的作业处理，因此维护任务必须实现java接口` [org.apache.sling.event.jobs.consumer.JobExecutor](https://sling.apache.org/apidocs/sling7/org/apache/sling/event/jobs/consumer/JobExecutor.html)`。 此外，它必须声明若干服务注册属性作为维护任务进行检测，如下所示：

<table>
 <tbody>
  <tr>
   <td><strong>服务属性名称</strong><br /> </td>
   <td><strong>描述</strong></td>
   <td><strong>示例</strong><br /> </td>
   <td><strong>类型</strong></td>
  </tr>
  <tr>
   <td>granite.maintenance.isStoppable</td>
   <td>布尔属性，用于定义用户是否可以停止任务。 如果任务声明其可停止，则必须在执行过程中检查其是否已停止，然后相应地执行。 默认值为false。</td>
   <td>true</td>
   <td>可选</td>
  </tr>
  <tr>
   <td>granite.maintenance.mandatory</td>
   <td>布尔属性，用于定义任务是否为必需，并且必须定期运行。 如果任务是必需的，但当前不在任何活动计划窗口中，运行状况检查会将此报告为错误。 默认值为false。</td>
   <td>true</td>
   <td>可选</td>
  </tr>
  <tr>
   <td>granite.maintenance.name</td>
   <td>任务的唯一名称 — 此名称用于引用任务。 这通常是一个简单的名称。</td>
   <td>MyMaintenanceTask</td>
   <td>必填</td>
  </tr>
  <tr>
   <td>granite.maintenance.title</td>
   <td>为此任务显示的标题</td>
   <td>我的特殊维护任务</td>
   <td>必填</td>
  </tr>
  <tr>
   <td>job.topics</td>
   <td>这是维护任务的一个独特主题。<br /> Apache Sling作业处理将开始具有此主题的作业以执行维护任务，并在为此主题注册任务时执行。<br /> 主题必须与 <i>com/adobe/granite/maintenance/job/开始</i></td>
   <td>com/adobe/granite/maintenance/job/MyMaintenanceTask</td>
   <td>必填</td>
  </tr>
 </tbody>
</table>

除了上述服务属性，`JobConsumer`接口的`process()`方法还需要通过添加应为维护任务执行的代码来实现。 提供的`JobExecutionContext`可用于输出状态信息、检查用户是否停止了作业并创建结果（成功或失败）。

如果维护任务不应在所有安装上运行（例如，仅在发布实例上运行），则可以通过添加`@Component(policy=ConfigurationPolicy.REQUIRE)`使服务需要配置才能处于活动状态。 然后，您可以根据配置在存储库中标记为运行模式。 有关详细信息，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md#creating-the-configuration-in-the-repository)。

以下是自定义维护任务的示例，该自定义维护操作从过去24小时内修改过的可配置临时目录中删除文件：

src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java

<table>
 <tbody>
  <tr>
   <td><p> </p> <p><code>/*</code></p> <p><code> * #%L</code></p> <p><code> * sample-maintenance-task</code></p> <p><code> * %%</code></p> <p><code> * Copyright (C) 2014 Adobe</code></p> <p><code> * %%</code></p> <p><code> * Licensed under the Apache License, Version 2.0 (the "License");</code></p> <p><code> * you may not use this file except in compliance with the License.</code></p> <p><code> * You may obtain a copy of the License at</code></p> <p><code> * </code></p> <p><code> * <a href="https://www.apache.org/licenses/LICENSE-2.0">https://www.apache.org/licenses/LICENSE-2.0</a></code></p> <p><code> * </code></p> <p><code> * Unless required by applicable law or agreed to in writing, software</code></p> <p><code> * distributed under the License is distributed on an "AS IS" BASIS,</code></p> <p><code> * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.</code></p> <p><code> * See the License for the specific language governing permissions and</code></p> <p><code> * limitations under the License.</code></p> <p><code> * #L%</code></p> <p><code> */</code></p> <p><code> </code></p> <p><code>package com.adobe.granite.samples.maintenance.impl;</code></p> <p><code> </code></p> <p><code>import java.io.File;</code></p> <p><code>import java.util.Calendar;</code></p> <p><code>import java.util.Collection;</code></p> <p><code>import java.util.Map;</code></p> <p><code> </code></p> <p><code>import org.apache.commons.io.FileUtils;</code></p> <p><code>import org.apache.commons.io.filefilter.IOFileFilter;</code></p> <p><code>import org.apache.commons.io.filefilter.TrueFileFilter;</code></p> <p><code>import org.apache.felix.scr.annotations.Activate;</code></p> <p><code>import org.apache.felix.scr.annotations.Component;</code></p> <p><code>import org.apache.felix.scr.annotations.Properties;</code></p> <p><code>import org.apache.felix.scr.annotations.Property;</code></p> <p><code>import org.apache.felix.scr.annotations.Service;</code></p> <p><code>import org.apache.sling.commons.osgi.PropertiesUtil;</code></p> <p><code>import org.apache.sling.event.jobs.Job;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobConsumer;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionContext;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionResult;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutor;</code></p> <p><code>import org.slf4j.Logger;</code></p> <p><code>import org.slf4j.LoggerFactory;</code></p> <p><code> </code></p> <p><code>import com.adobe.granite.maintenance.MaintenanceConstants;</code></p> <p><code> </code></p> <p><code>@Component(metatype = true,</code></p> <p><code> label = "Delete Temp Files Maintenance Task",</code></p> <p><code> description = "Maintatence Task which deletes files from a configurable temporary directory which have been modified in the last 24 hours.")</code></p> <p><code>@Service</code></p> <p><code>@Properties({</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_NAME, value = "DeleteTempFilesTask", propertyPrivate = true),</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_TITLE, value = "Delete Temp Files", propertyPrivate = true),</code></p> <p><code> @Property(name = JobConsumer.PROPERTY_TOPICS, value = MaintenanceConstants.TASK_TOPIC_PREFIX</code></p> <p><code> + "DeleteTempFilesTask", propertyPrivate = true) })</code></p> <p><code>public class DeleteTempFilesTask implements JobExecutor {</code></p> <p><code> </code></p> <p><code> private static final Logger log = LoggerFactory.getLogger(DeleteTempFilesTask.class);</code></p> <p><code> </code></p> <p><code> @Property(label = "Temporary Directory", description="Temporary Directory. Defaults to the java.io.tmpdir system property.")</code></p> <p><code> private static final String PROP_TEMP_DIR = "temp.dir";</code></p> <p><code> </code></p> <p><code> private File tempDir;</code></p> <p><code> </code></p> <p><code> @Activate</code></p> <p><code> private void activate(Map&lt;string, object=""&gt; properties) {</code></p> <p><code> this.tempDir = new File(PropertiesUtil.toString(properties.get(PROP_TEMP_DIR),</code></p> <p><code> System.getProperty("java.io.tmpdir")));</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public JobExecutionResult process(Job job, JobExecutionContext context) {</code></p> <p><code> log.info("Deleting old temp files from {}.", tempDir.getAbsolutePath());</code></p> <p><code> Collection&lt;file&gt; files = FileUtils.listFiles(tempDir, new LastModifiedBeforeYesterdayFilter(),</code></p> <p><code> TrueFileFilter.INSTANCE);</code></p> <p><code> int counter = 0;</code></p> <p><code> for (File file : files) {</code></p> <p><code> log.debug("Deleting file {}.", file.getAbsolutePath());</code></p> <p><code> counter++;</code></p> <p><code> file.delete();</code></p> <p><code> // TODO - capture the output of delete() and do something useful with it</code></p> <p><code> }</code></p> <p><code> return context.result().message(String.format("Deleted %s files.", counter)).succeeded();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> /**</code></p> <p><code> * IOFileFilter which filters out files which have been modified in the last 24 hours.</code></p> <p><code> *</code></p> <p><code> */</code></p> <p><code> private static class LastModifiedBeforeYesterdayFilter implements IOFileFilter {</code></p> <p><code> </code></p> <p><code> private final long minTime;</code></p> <p><code> </code></p> <p><code> private LastModifiedBeforeYesterdayFilter() {</code></p> <p><code> Calendar cal = Calendar.getInstance();</code></p> <p><code> cal.add(Calendar.DATE, -1);</code></p> <p><code> this.minTime = cal.getTimeInMillis();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File dir, String name) {</code></p> <p><code> // this method is never actually called.</code></p> <p><code> return false;</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File file) {</code></p> <p><code> return file.lastModified() <= this.minTime;</code></p> <p><code> }</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code>}</code></p> <p><code>&lt;file&gt;&lt;/string,&gt;</code></p> <p> </p> </td>
  </tr>
 </tbody>
</table>

[experiencemanager-java-maintenancetask-sample](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample)- [src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample/blob/master/src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java)

部署服务后，它会暴露在“操作”仪表板UI中。 您可以将其添加到可用的维护计划之一：

![chlimage_1-127](assets/chlimage_1-127.png)

这将在/apps/granite/operations/config/maintenance/`schedule`/`taskname`添加相应的资源。 如果任务与运行模式相关，则需要在该节点上设置granite.operations.conditions.runmode属性，并设置运行模式的值，这些值对于此维护任务需要处于活动状态。

## 系统概览 {#system-overview}

**系统概述仪表板**&#x200B;显示AEM实例的配置、硬件和运行状况的高级概述。 这意味着系统运行状况是透明的，所有信息都会聚集到一个仪表板中。

>[!NOTE]
>
>您还可以[观看此视频](https://video.tv.adobe.com/v/21340)，了解“系统概述”仪表板的简介。

### 如何访问{#how-to-access}

要访问“系统概述”仪表板，请导航到&#x200B;**“工具”>“操作”>“系统概述”**。

![system_overview_仪表板](assets/system_overview_dashboard.png)

### 系统概述仪表板说明{#system-overview-dashboard-explained}

下表描述了“系统概述”仪表板中显示的所有信息。 请记住，当没有要显示的相关信息（例如，备份未进行，没有关键的运行状况检查）时，相应部分将显示“无条目”消息。

您还可以通过单击仪表板右上角的&#x200B;**下载**&#x200B;按钮来下载汇总仪表板信息的`JSON`文件。`JSON`端点是`/libs/granite/operations/content/systemoverview/export.json`，可在`curl`脚本中用于外部监视。

<table>
 <tbody>
  <tr>
   <td><strong>区域</strong></td>
   <td><strong>显示哪些信息</strong></td>
   <td><strong>什么时候至关重要</strong></td>
   <td><strong>链接到</strong></td>
  </tr>
  <tr>
   <td>运行状况检查</td>
   <td>
    <ul>
     <li>处于“关键”状态的检查列表</li>
     <li>处于“警告”状态的检查列表</li>
    </ul> </td>
   <td>可视指示：<br />
    <ul>
     <li>关键检查的红色标签</li>
     <li>用于警告检查的橙色标签</li>
    </ul> </td>
   <td>
    <ul>
     <li>运行状况报告页</li>
    </ul> </td>
  </tr>
  <tr>
   <td>维护任务</td>
   <td>
    <ul>
     <li>一列表失败的任务</li>
     <li>当前运行的列表任务</li>
     <li>在上次运行中成功的列表任务</li>
     <li>一列表从未运行的任务</li>
     <li>未计划的列表任务</li>
    </ul> </td>
   <td><p>以可视方式指示：</p>
    <ul>
     <li>失败任务的红色标记</li>
     <li>用于运行任务的橙色标签（因为它们可能影响性能）</li>
     <li>其他所有状态的灰色标签</li>
    </ul> </td>
   <td>
    <ul>
     <li>维护任务页</li>
    </ul> </td>
  </tr>
  <tr>
   <td>系统</td>
   <td>
    <ul>
     <li>操作系统和操作系统版本（例如Mac OS X）</li>
     <li>系统负载平均值，从<a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/OperatingSystemMXBean.html#getSystemLoadAverage--">OperatingSystemMXBeanusable</a>检索</li>
     <li>磁盘空间（在主目录所在的分区上）</li>
     <li>最大堆，由<a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/MemoryMXBean.html#getHeapMemoryUsage--">MemoryMXBean</a>返回</li>
    </ul> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>实例</td>
   <td>
    <ul>
     <li>AEM版本</li>
     <li>列表运行模式</li>
     <li>实例启动的日期</li>
    </ul> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>存储库</td>
   <td>
    <ul>
     <li>Oak版</li>
     <li>节点存储的类型(区段Tar或文档)
      <ul>
       <li>如果类型为文档，则显示文档存储的类型（RDB或Mongo）</li>
      </ul> </li>
     <li>如果存在自定义数据存储：
      <ul>
       <li>对于文件数据存储区，将显示路径</li>
       <li>对于S3数据存储，将显示S3存储桶的名称</li>
       <li>对于共享的S3数据存储，将显示S3存储桶的名称</li>
       <li>对于Azure容器存储，将显示</li>
      </ul> </li>
     <li>如果没有自定义外部数据存储，则显示指示此事实的消息</li>
    </ul> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>分发代理</td>
   <td>
    <ul>
     <li>具有被阻止队列的代理的列表</li>
     <li>列表配置错误的代理（“配置错误”）</li>
     <li>暂停队列处理的代理列表</li>
     <li>一列表空闲代理</li>
     <li>运行代理的列表（当前正在处理条目）</li>
    </ul> </td>
   <td><p>以可视方式指示：</p>
    <ul>
     <li>被阻止的代理或配置错误的红色标记</li>
     <li>暂停的代理的橙色标签</li>
     <li>暂停、空闲或运行代理的灰色标记<br /> </li>
    </ul> </td>
   <td>分发页<br /> </td>
  </tr>
  <tr>
   <td>复制代理</td>
   <td>
    <ul>
     <li>具有被阻止队列的代理的列表</li>
     <li>一列表空闲代理</li>
     <li>运行代理的列表（当前正在处理条目）</li>
    </ul> </td>
   <td><p>可视指示：<br /> </p>
    <ul>
     <li>被阻止的代理的红色标签</li>
     <li>暂停代理的灰色标记</li>
    </ul> </td>
   <td>复制页</td>
  </tr>
  <tr>
   <td>工作流</td>
   <td>
    <ul>
     <li>工作流作业：
      <ul>
       <li>失败的工作流作业数（如果有）</li>
       <li>已取消的工作流作业数（如果有）</li>
      </ul> </li>
    </ul>
    <ul>
     <li>工作流计数 — 处于给定状态的工作流数（如果有）：
      <ul>
       <li>运行</li>
       <li>失败</li>
       <li>暂停</li>
       <li>中止</li>
      </ul> </li>
    </ul> <p>对于以上显示的每种状态，将执行查询，限制为400毫秒。 在400毫秒时，将显示到该点为止获取的条目数。</p> </td>
   <td><p>未解释：</p>
    <ul>
     <li>当工作流和作业处于意外状态时，用户应进行调查。</li>
    </ul> </td>
   <td>“工作流失败”页</td>
  </tr>
  <tr>
   <td>Sling 作业</td>
   <td><p>Sling作业计数 — 处于给定状态的作业数（如果有）：</p>
    <ul>
     <li>失败</li>
     <li>排队</li>
     <li>已取消</li>
     <li>活动</li>
    </ul> </td>
   <td><p>未解释：</p>
    <ul>
     <li>当存在处于意外状态或计数较高的作业时，用户应进行调查。</li>
    </ul> </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>预计节点计数</td>
   <td><p>估计数：</p>
    <ul>
     <li>页</li>
     <li>资产</li>
     <li>标记</li>
     <li>可授权</li>
     <li>节点总数<br /> </li>
    </ul> <p>节点总数从nodeCounterMBean获取，其余统计信息则从IndexInfoService获取。</p> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>备份</td>
   <td>如果出现这种情况，则显示“正在进行联机备份”。</td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>索引</td>
   <td><p>显示:</p>
    <ul>
     <li>"正在进行索引"</li>
     <li>"正在进行查询"</li>
    </ul> <p>如果线程转储中存在索引或查询线程。</p> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>
