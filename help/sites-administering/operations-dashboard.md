---
title: 操作功能板
description: 了解如何使用Adobe Experience Manager中的操作功能板。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: f9a88156-91a2-4c85-9bc9-8f23700c2cbd
feature: Operations
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: db7830895c8a2d1b7228dc4780296d43f15776df
workflow-type: tm+mt
source-wordcount: '5743'
ht-degree: 2%

---

# 操作功能板 {#operations-dashboard}

## 简介 {#introduction}

AEM 6中的操作仪表板可帮助系统操作员一目了然地监控AEM系统运行状况。 它还提供有关AEM相关方面的自动生成诊断信息，并可让您配置和运行自包含的维护自动化，从而显着减少项目操作和支持案例。 操作功能板可通过自定义运行状况检查和维护任务进行扩展。 此外，可通过JMX从外部监控工具访问操作仪表板数据。

**操作仪表板：**

* 是一键式系统状态，可帮助运营部门提高效率
* 在单个集中位置提供系统运行状况概述
* 缩短查找、分析和修复问题的时间
* 提供独立的维护自动化，帮助显着降低项目运营成本

通过从AEM欢迎屏幕转到&#x200B;**工具** - **操作**&#x200B;可访问该区域。

>[!NOTE]
>
>要能够访问操作仪表板，登录用户必须是“操作员”用户组的一部分。 有关详细信息，请参阅有关[用户、组和访问权限管理](/help/sites-administering/user-group-ac-admin.md)的文档。

## 健康报表 {#health-reports}

运行状况报告系统通过Sling运行状况检查提供有关AEM实例的运行状况的信息。 可通过OSGI、JMX、HTTP请求（通过JSON）或通过Touch UI完成此操作。 它提供某些可配置计数器的测量值和阈值，有时提供有关如何解决问题的信息。

它具有若干功能，如下所述。

## 运行状况检查 {#health-checks}

**运行状况报告**&#x200B;是一个卡片系统，用于指示特定产品区域的运行状况是好还是坏。 这些卡片是Sling运行状况检查的可视化图表，用于聚合来自JMX和其他源的数据，并再次将处理过的信息作为MBean显示。 也可以在&#x200B;**org.apache.sling.healthcheck**&#x200B;域下的[JMX Web控制台](/help/sites-administering/jmx-console.md)中检查这些MBean。

可通过AEM欢迎屏幕上的&#x200B;**工具** - **操作** - **运行状况报告**&#x200B;菜单或直接通过以下URL访问运行状况报告界面：

`https://<serveraddress>:port/libs/granite/operations/content/healthreports/healthreportlist.html`

![chlimage_1-116](assets/chlimage_1-116.png)

卡片系统可能会显示三种状态：**正常**、**警告**&#x200B;和&#x200B;**严重**。 状态是规则和阈值的结果，可以通过将鼠标悬停在信息卡上，然后单击操作栏中的齿轮图标来配置这些规则和阈值：

![chlimage_1-117](assets/chlimage_1-117.png)

### 运行状况检查类型 {#health-check-types}

AEM 6中有两种类型的运行状况检查：

1. 个人运行状况检查
1. 复合运行状况检查

**个人运行状况检查**&#x200B;是与状态卡相对应的单个运行状况检查。 可以使用规则或阈值配置各个运行状况检查，它们可以提供一个或多个提示和链接以解决已识别的运行状况问题。 让我们以“日志错误”检查为例：如果实例日志中存在ERROR条目，请在运行状况检查的详细信息页面上查找它们。 在页面顶部，您可以看到“诊断工具”部分中“日志消息”分析器的链接，该链接允许您更详细地分析这些错误并重新配置日志程序。

**复合运行状况检查**&#x200B;是汇总来自多个单独检查的信息的检查。

复合运行状况检查是通过&#x200B;**筛选标记**&#x200B;配置的。 实质上，具有相同过滤器标记的所有单次检查都分组为复合运行状况检查。 仅当所有其聚合的单项检查的状态均为OK时，复合运行状况检查的状态才为OK。

### 如何创建运行状况检查 {#how-to-create-health-checks}

在“操作”功能板中，您可以显示单个和复合运行状况检查的结果。

### 创建个人运行状况检查 {#creating-an-individual-health-check}

创建单个运行状况检查涉及两个步骤：实施Sling运行状况检查和在功能板的配置节点中添加运行状况检查条目。

1. 要创建Sling运行状况检查，请创建一个实施Sling运行状况检查接口的OSGI组件。 将此组件添加到捆绑包中。 组件的属性可完全标识运行状况检查。 安装组件后，将自动为运行状况检查创建JMX MBean。 有关详细信息，请参阅[Sling运行状况检查文档](https://sling.apache.org/documentation/bundles/sling-health-check-tool.html)。

   使用OSGI服务组件注释编写的Sling运行状况检查组件示例：

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
   >`MBEAN_NAME`属性定义为此运行状况检查生成的mbean的名称。

1. 创建运行状况检查后，必须创建新的配置节点，才能在操作功能板界面中访问该节点。 对于此步骤，需要知道运行状况检查的JMX Mbean名称（`MBEAN_NAME`属性）。 要为运行状况检查创建配置，请打开CRXDE并在以下路径下添加一个节点（类型为&#x200B;**nt：unstructured**）： `/apps/settings/granite/operations/hc`

   应在新节点上设置以下属性：

   * **名称：** `sling:resourceType`

      * **类型：** `String`
      * **值：** `granite/operations/components/mbean`

   * **名称：** `resource`

      * **类型：** `String`
      * **值：** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/exampleHealthCheck`

   >[!NOTE]
   >
   >上述资源路径按如下方式创建：如果运行状况检查的mbean名称为“test”，请将“test”添加到路径`/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck`的末尾
   >
   >因此，最终路径如下：
   >
   >`/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/test`

   >[!NOTE]
   >
   >确保`/apps/settings/granite/operations/hc`路径具有以下属性设置为true：
   >
   >
   >`sling:configCollectionInherit`
   >
   >`sling:configPropertyInherit`
   >
   >
   >此过程告知配置管理器将新配置与`/libs`中的现有配置合并。

### 创建复合运行状况检查 {#creating-a-composite-health-check}

复合运行状况检查的作用是聚合多个单独的运行状况检查，这些检查共享一组常用功能。 例如，安全复合运行状况检查将执行安全相关验证的所有单独运行状况检查分组。 创建复合检查的第一步是添加OSGI配置。 要使它显示在“操作仪表板”中，必须以简单检查的方式添加新配置节点。

1. 转到OSGI控制台中的Web配置管理器。 访问`https://serveraddress:port/system/console/configMgr`
1. 搜索名为&#x200B;**Apache Sling复合运行状况检查**&#x200B;的项目。 找到后，请注意已有两个配置可用：一个用于系统检查，另一个用于安全检查。
1. 通过按配置右侧的“+”按钮创建配置。 将显示一个新窗口，如下所示：

   ![chlimage_1-23](assets/chlimage_1-23.jpeg)

1. 创建配置并保存。 使用新配置创建Mbean。

   每个配置属性的用途如下：

   * **名称(hc.name)：**&#x200B;复合运行状况检查的名称。 建议使用有意义的名称。
   * **标记(hc.tags)：**&#x200B;此运行状况检查的标记。 如果此复合运行状况检查要作为另一个复合运行状况检查（例如，在运行状况检查的层次结构中）的一部分，请添加此复合与之相关的标记。
   * **MBean名称(hc.mbean.name)：**&#x200B;为此复合运行状况检查的JMX MBean指定的Mbean的名称。
   * **筛选标记(filter.tags)：**&#x200B;特定于复合运行状况检查的属性。 这些标记由复合聚合。 复合运行状况检查将在其组下聚合所有具有与此复合的任何过滤器标记匹配的标记的运行状况检查。 例如，具有筛选器标记&#x200B;**test**&#x200B;和&#x200B;**check**&#x200B;的组合运行状况检查聚合其标记属性(`hc.tags`)中具有任何&#x200B;**test**&#x200B;和&#x200B;**check**&#x200B;标记的所有单独和组合运行状况检查。

   >[!NOTE]
   >
   >为Apache Sling复合运行状况检查的每个新配置创建一个新的JMX Mbean。**

1. 最后，必须将已创建的复合运行状况检查条目添加到操作仪表板配置节点中。 此过程与单个运行状况检查的过程相同：必须在`/apps/settings/granite/operations/hc`下创建类型为&#x200B;**nt：unstructured**&#x200B;的节点。 节点的资源属性由OSGI配置中的&#x200B;**hc.mean.name**&#x200B;值定义。

   例如，如果您创建了配置并将&#x200B;**hc.mbean.name**&#x200B;值设置为&#x200B;**diskusage**，则配置节点如下所示：

   * **名称：** `Composite Health Check`

      * **类型：** `nt:unstructured`

   具有以下属性：

   * **名称：** `sling:resourceType`

      * **类型：** `String`
      * **值：** `granite/operations/components/mbean`

   * **名称：** `resource`

      * **类型：** `String`
      * **值：** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/diskusage`

   >[!NOTE]
   >
   >如果创建逻辑上属于复合检查的各个运行状况检查（默认情况下，该复合检查已存在于仪表板中），则会在相应的复合检查下自动捕获和分组这些运行状况检查。 因此，无需为这些检查创建配置节点。
   >
   >例如，如果您创建单独的安全运行状况检查，请为其分配“**安全**”标记，然后安装该标记。 它自动显示在“操作”操控板的“安全检查”复合检查下。

### AEM提供的运行状况检查 {#health-checks-provided-with-aem}

<table>
 <tbody>
  <tr>
   <td><strong>运行状况检查名称</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>查询性能</td>
   <td><p>此运行状况检查已在AEM 6.4</strong>中进行了简化<strong>，现在将检查最近重构的<code>Oak QueryStats</code> MBean，更具体而言是<code>SlowQueries </code>属性。 如果统计信息包含任何慢查询，则运行状况检查将返回警告。 否则，它会返回OK状态。<br /> </p> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueriesStatus%2Ctype%3DHealthCheck">org.apache.sling.healthcheck：name=queriesStatus，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>观察队列长度</td>
   <td><p>观察队列长度遍历所有事件侦听器和后台观察器，将其<code>queueSize </code>与其<code>maxQueueSize</code>进行比较，并：</p>
    <ul>
     <li>如果<code>queueSize</code>值超过<code>maxQueueSize</code>值（即事件将被删除时），则返回严重状态</li>
     <li>如果<code>queueSize</code>值超过<code>maxQueueSize * WARN_THRESHOLD</code>，则返回警告（默认值为0.75） </li>
    </ul> <p>每个队列的最大长度来自单独的配置(Oak和AEM)，并且无法通过此运行状况检查进行配置。 此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DObservationQueueLengthHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthcheck：name=ObservationQueueLengthHealthCheck，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>查询遍历限制</td>
   <td><p>查询遍历限制检查<code>QueryEngineSettings</code> MBean，更具体地说<code>LimitInMemory</code>和<code>LimitReads</code>属性，并返回以下状态：</p>
    <ul>
     <li>如果其中一个限制等于或大于 <code>Integer.MAX_VALUE</code></li>
     <li>如果其中一个限制小于10000(Oak中的推荐设置)，则返回警告状态</li>
     <li>如果无法检索<code>QueryEngineSettings</code>或任何限制，则返回“严重”状态</li>
    </ul> <p>此运行状况检查的Mbean是<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueryTraversalLimitsBundle%2Ctype%3DHealthCheck">org.apache.sling.healthcheck：name=queryTraversalLimitsBundle，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>同步的时钟</td>
   <td><p>此检查仅与<a href="https://github.com/apache/sling-old-svn-mirror/blob/4df9ab2d6592422889c71fa13afd453a10a5a626/bundles/extensions/discovery/oak/src/main/java/org/apache/sling/discovery/oak/SynchronizedClocksHealthCheck.java">文档节点存储群集</a>相关。 它会返回以下状态：</p>
    <ul>
     <li>当实例时钟不同步并超过预定义的低阈值时，返回警告状态</li>
     <li>当实例时钟不同步并超过预定义的高阈值时，返回严重状态</li>
    </ul> <p>此运行状况检查的Mbean是<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingDiscoveryOakSynchronizedClocks%2Ctype%3DHealthCheck">org.apache.sling.healthcheck：name=slingDiscoveryOakSynchronizedClocks，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>异步索引</td>
   <td><p>异步索引检查：</p>
    <ul>
     <li>如果至少有一个索引通道失败，则返回关键状态</li>
     <li>检查<code>lastIndexedTime</code>的所有索引通道并：
      <ul>
       <li>如果超过2小时前，则返回关键状态 </li>
       <li>如果时间介于2小时和45分钟之前，则返回警告状态 </li>
       <li>如果时间小于45分钟前，则返回“正常”状态 </li>
      </ul> </li>
     <li>如果不符合上述任何条件，则会返回“正常”状态</li>
    </ul> <p>“严重”和“警告”状态阈值均可配置。 此运行状况检查的Mbean是<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DasyncIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthcheck：name=asyncIndexHealthCheck，type=HealthCheck</a>。</p> <p><strong>注意： </strong>此运行状况检查在AEM 6.4中可用，并且已回溯到AEM 6.3.0.1。</p> </td>
  </tr>
  <tr>
   <td>大型 Lucene 索引</td>
   <td><p>此检查使用<code>Lucene Index Statistics</code> MBean公开的数据来识别大型索引并返回：</p>
    <ul>
     <li>如果索引中的文档超过10亿，则显示警告状态</li>
     <li>a如果索引中的文档超过15亿，则为严重状态</li>
    </ul> <p>阈值可配置，运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlargeIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthcheck：name=largeIndexHealthCheck，type=HealthCheck。</a></p> <p><strong>注意： </strong>此检查在AEM 6.4中可用，并且已回溯到AEM 6.3.2.0。</p> </td>
  </tr>
  <tr>
   <td>系统维护</td>
   <td><p>系统维护是一种复合检查，如果所有维护任务都按配置运行，则返回“正常”。 请记住：</p>
    <ul>
     <li>每个维护任务都附带一个关联的运行状况检查</li>
     <li>如果任务未添加到维护窗口，则其运行状况检查将返回“严重”</li>
     <li>配置“审核日志”和“工作流清除”维护任务，或将其从维护窗口中删除。 如果未配置，这些任务在首次尝试运行时将失败，因此“系统维护”检查会返回“严重”状态。</li>
     <li><strong>使用AEM 6.4</strong>时，还会检查<a href="/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks">Lucene二进制文件维护</a>任务</li>
     <li>在AEM 6.2及更低版本上，系统维护检查在启动后立即返回警告状态，因为任务从不运行。 从6.3开始，如果尚未到达第一个维护时段，它们会返回OK。</li>
    </ul> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsystemchecks%2Ctype%3DHealthCheck">org.apache.sling.healthcheck：name=systemchecks，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>复制队列</td>
   <td><p>此检查跨复制代理反复进行，并查看其队列。 对于队列顶部的项目，该检查会查看代理重试复制的次数。 如果代理重试的复制次数大于<code>numberOfRetriesAllowed</code>参数的值，则会返回警告。 <code>numberOfRetriesAllowed</code>参数可配置。 </p> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DreplicationQueue%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=replicationQueue，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>Sling 作业</td>
   <td>
    <div>
      Sling作业检查JobManager中排队的作业数，并将其与
     <code>maxNumQueueJobs</code>阈值，并且：
    </div>
    <ul>
     <li>如果队列中超过<code>maxNumQueueJobs</code>个，则返回“严重”</li>
     <li>如果存在早于1小时的长期运行活动作业，则返回“严重”</li>
     <li>如果存在已排队的作业，并且上次完成的作业时间早于1小时，则返回“严重”</li>
    </ul> <p>只能配置已排队作业的最大数量参数，其默认值为1000。</p> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingJobs%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=slingJobs，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>请求性能</td>
   <td><p>此检查检查<code>granite.request.metrics.timer</code> <a href="http://localhost:4502/system/console/slingmetrics" target="_blank">Sling量度</a>和：</p>
    <ul>
     <li>如果第75百分位值超过关键阈值（默认值为500毫秒），则返回“关键”</li>
     <li>如果第75百分位值超过警告阈值（默认值为200毫秒），则返回警告</li>
    </ul> <p>此运行状况检查的MBean为<em> </em><a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DrequestsStatus%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=requestsStatus，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>日志错误</td>
   <td><p>如果日志中有错误，此检查会返回警告状态。</p> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlogErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=logErrorHealthCheck，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>磁盘空间</td>
   <td><p>磁盘空间检查检查<code>FileStoreStats</code> MBean，检索节点存储的大小和节点存储分区上的可用磁盘空间量，并且：</p>
    <ul>
     <li>如果可用磁盘空间与存储库大小的比率小于警告阈值（默认值为10），则返回警告</li>
     <li>如果可用磁盘空间与存储库大小的比率小于关键阈值（默认值为2），则返回关键</li>
    </ul> <p>两个阈值均可配置。 该检查仅适用于具有区段存储的实例。</p> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DDiskSpaceHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=DiskSpaceHealthCheck，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>计划程序运行状况检查</td>
   <td><p>如果实例的Quartz作业运行时间超过60秒，则此检查会返回警告。 可以配置可接受的持续时间阈值。</p> <p>此运行状况检查的MBean是<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingCommonsSchedulerHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=slingCommonsSchedulerHealthCheck，type=HealthCheck</a><em>.</em></p> </td>
  </tr>
  <tr>
   <td>安全检查</td>
   <td><p>安全检查是一种组合检查，用于聚合多个安全相关检查的结果。 这些个人运行状况检查可解决<a href="/help/sites-administering/security-checklist.md">安全核对清单文档页面提供的安全核对清单中的不同问题。</a>该检查在启动实例时可用作安全冒烟测试。 </p> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsecuritychecks%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=securitychecks，type=HealthCheck</a></p> </td>
  </tr>
  <tr>
   <td>活动包</td>
   <td><p>活动包检查所有包的状态，并且：</p>
    <ul>
     <li>如果有任何捆绑包未处于活动状态或（从延迟激活开始），则返回警告状态</li>
     <li>它忽略忽略列表中的捆绑包状态</li>
    </ul> <p>ignore list参数是可配置的。</p> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DinactiveBundles%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=inactiveBundles，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>代码缓存检查</td>
   <td><p>运行状况检查验证多个JVM条件，这些条件可能会触发Java™ 7中存在的CodeCache错误：</p>
    <ul>
     <li>如果实例在Java™ 7上运行，并且启用了代码缓存刷新，则返回警告</li>
     <li>如果实例在Java™ 7上运行，并且保留的代码缓存大小小于最小阈值（默认值为90 MB），则返回警告</li>
    </ul> <p><code>minimum.code.cache.size</code>阈值可配置。 有关Bug的详细信息，请参阅<a href="https://bugs.java.com/bugdatabase/">，然后搜索Bug ID 8012547</a>。</p> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DcodeCacheHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=codeCacheHealthCheck，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>资源搜索路径错误</td>
   <td><p>检查路径<code>/apps/foundation/components/primary</code>中是否存在任何资源，并且：</p>
    <ul>
     <li>如果下有子节点，则返回警告 <code>/apps/foundation/components/primary</code></li>
    </ul> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DresourceSearchPathErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=resourceSearchPathErrorHealthCheck，type=HealthCheck</a>。</p> </td>
  </tr>
 </tbody>
</table>

### 运行状况检查配置 {#health-check-configuration}

默认情况下，对于现成的AEM实例，运行状况检查每60秒运行一次。

您可以使用[OSGi配置](/help/sites-deploying/configuring-osgi.md) **查询运行状况检查配置** (com.adobe.granite.queries.impl.hc.QueryHealthCheckMetrics)配置&#x200B;**Period**。

## 使用外部服务进行监控 {#monitoring-with-external-services}

可与外部技术或供应商集成。 有关相关详细信息，请参阅其文档。

## 诊断工具 {#diagnosis-tools}

操作仪表板还提供对诊断工具的访问权限，这些工具可帮助查找并排除来自运行状况检查仪表板的警告的根本原因，并为系统操作员提供重要的调试信息。

其最重要的特征包括：

* 日志消息分析器
* 访问栈和线程转储的功能
* 请求和查询性能分析器

您可以从AEM欢迎屏幕转到&#x200B;**工具 — 操作 — 诊断**&#x200B;来访问“诊断工具”屏幕。 您还可以通过直接访问以下URL来访问屏幕： `https://serveraddress:port/libs/granite/operations/content/diagnosis.html`

![chlimage_1-120](assets/chlimage_1-120.png)

### 日志消息 {#log-messages}

日志消息用户界面默认显示所有ERROR消息。 如果要显示更多日志消息，请使用适当的日志级别配置日志程序。

日志消息使用内存中的日志附加器，因此与日志文件无关。 另一个后果是，更改此UI中的日志级别不会更改记录到传统日志文件中的信息。 在此UI中添加和删除记录器仅影响内存记录器。 此外，更改记录器配置将反映在内存记录器的未来中。 已记录且不再相关的条目不会被删除，但将来不会记录类似的条目。

您可以通过从UI的左上角齿轮按钮提供记录器配置来配置记录的内容。 在那里，您可以添加、删除或更新记录器配置。 记录器配置由&#x200B;**日志级别** (WARN / INFO / DEBUG)和&#x200B;**筛选器名称**&#x200B;组成。 **筛选器名称**&#x200B;具有筛选要记录的日志消息源的角色。 或者，如果日志记录器应捕获指定级别的所有日志消息，则筛选器名称应为“**root**”。 设置记录器的级别将触发捕获级别等于或高于指定级别的所有消息。

示例：

* 如果您计划捕获所有&#x200B;**ERROR**&#x200B;消息，则无需配置。 默认情况下会捕获所有错误消息。
* 如果您计划捕获所有&#x200B;**ERROR**、**WARN**&#x200B;和&#x200B;**INFO**&#x200B;消息，则记录器名称应设置为“**root**”，记录器级别应设置为&#x200B;**INFO**。

* 如果您计划捕获来自特定包（例如com.adobe.granite）的所有消息，则应将记录器名称设置为“com.adobe.granite”。 而且，记录器级别设置为&#x200B;**DEBUG** （这样做会捕获所有&#x200B;**ERROR**、**WARN**、**INFO**&#x200B;和&#x200B;**DEBUG**&#x200B;消息），如下图所示。

![chlimage_1-121](assets/chlimage_1-121.png)

>[!NOTE]
>
>您不能通过指定的过滤器设置记录器名称以仅捕获错误消息。 默认情况下，将捕获所有ERROR消息。

>[!NOTE]
>
>日志消息用户界面不反映实际的错误日志。 除非在UI中配置其他类型的日志消息，否则只能看到错误消息。 有关如何显示特定日志消息的信息，请参阅以上说明。

>[!NOTE]
>
>诊断页面中的设置不会影响记录到日志文件的内容，反之亦然。 因此，尽管错误日志可能会捕获INFO消息，但您可能会在日志消息UI中看不到它们。 此外，通过UI，还可以捕获特定包中的DEBUG消息，而不会影响错误日志。 有关如何配置日志文件的详细信息，请参阅[日志记录](/help/sites-deploying/configure-logging.md)。

>[!NOTE]
>
>**使用AEM 6.4**，维护任务将以INFO级别中信息丰富的格式立即注销。 此工作流可让您更好地了解维护任务的状态。
>
>如果您使用第三方工具（如Splunk）来监控和响应维护任务活动，则可以使用以下log语句：

```
Log level: INFO
DATE+TIME [MaintanceLogger] Name=<MT_NAME>, Status=<MT_STATUS>, Time=<MT_TIME>, Error=<MT_ERROR>, Details=<MT_DETAILS>
```

### 请求性能 {#request-performance}

使用“请求性能”页可以分析处理的最慢的页面请求。 此页面上仅注册内容请求。 更具体地说，将捕获以下请求：

1. 请求访问`/content`下的资源
1. 请求访问`/etc/design`下的资源
1. 具有`".html"`扩展名的请求

![chlimage_1-122](assets/chlimage_1-122.png)

此时将显示页面：

* 发出请求的时间
* URL和请求方法
* 持续时间（以毫秒为单位）

默认情况下，会捕获最慢的20页请求，但可以在Configuration Manager中修改此限制。

### 查询性能 {#query-performance}

使用“查询性能”页可以分析系统执行的最慢查询。 此信息由JMX Mbean中的存储库提供。 在Jackrabbit中，`com.adobe.granite.QueryStat` JMX Mbean提供此信息，而在Oak存储库中，此信息由`org.apache.jackrabbit.oak.QueryStats.`提供

此时将显示页面：

* 进行查询的时间
* 查询的语言
* 发出查询的次数
* 查询的语句
* 持续时间（以毫秒为单位）

![chlimage_1-123](assets/chlimage_1-123.png)

### 说明查询 {#explain-query}

对于任何给定的查询，Oak会尝试根据&#x200B;**oak：index**&#x200B;节点下的存储库中定义的Oak索引找出最佳执行方式。 Oak可能会根据查询选择不同的索引。 了解Oak如何执行查询是优化查询的第一步。

Explain查询是一种用于说明Oak如何执行查询的工具。 通过从AEM欢迎屏幕转到&#x200B;**工具 — 操作 — 诊断**&#x200B;可访问该区域。 然后，单击&#x200B;**查询性能**&#x200B;并切换到&#x200B;**解释查询**&#x200B;选项卡。

**功能**

* 支持Xpath、JCR-SQL和JCR-SQL2查询语言
* 报告所提供的查询的实际执行时间
* 检测较慢的查询，并警告可能较慢的查询
* 报告用于执行查询的Oak索引
* 显示实际的Oak查询引擎说明
* 提供慢速查询和常用查询的点击加载列表

进入Explain查询UI后，输入查询，然后按&#x200B;**Explain**&#x200B;按钮：

![chlimage_1-124](assets/chlimage_1-124.png)

“查询说明”部分中的第一个条目是实际说明。 此说明显示了用于执行查询的索引类型。

第二个条目是执行计划。

在运行查询前勾选&#x200B;**包括执行时间**&#x200B;框也会显示查询运行的时间。 **包含节点数**&#x200B;选项报告节点数。 该报告提供了可用于优化应用程序或部署的索引的更多信息。

![chlimage_1-125](assets/chlimage_1-125.png)

### 索引管理器 {#the-index-manager}

索引管理器的目的是促进索引管理，如维护索引或查看索引的状态。

通过从“欢迎屏幕”转到**工具 — 操作 — 诊断**，然后单击&#x200B;**索引管理器**&#x200B;按钮可访问该区域。

也可以通过以下URL直接访问它： `https://serveraddress:port/libs/granite/operations/content/diagnosistools/indexManager.html`

![索引管理器](assets/index_manager.png)

UI可用于过滤表中的索引，方法是在屏幕左上角的搜索框中键入过滤条件。

### 下载状态ZIP {#download-status-zip}

此操作会触发下载zip文件，其中包含有关系统状态和配置的有用信息。 存档包含实例配置、包列表、OSGI、Sling量度和统计数据，这可能会导致产生大文件。 您可以使用&#x200B;**下载状态ZIP**&#x200B;窗口来减少大型状态文件的影响。 可从以下位置访问该窗口：**AEM >工具>操作>诊断>下载状态ZIP。**

从该窗口中，您可以选择要导出的内容（日志文件和/或线程转储）以及相对于当前日期包含在下载中的日志天数。

![download_status_zip](assets/download_status_zip.png)

### 下载线程转储 {#download-thread-dump}

此操作会触发下载zip文件，其中包含有关系统中存在的线程的信息。 提供了有关每个线程的信息，例如其状态、类加载器和栈栈跟踪。

### 下载栈转储 {#download-heap-dump}

您可以下载栈的快照以便稍后进行分析。 此操作会触发大型（数百MB）文件的下载。

## 自动维护任务 {#automated-maintenance-tasks}

在“自动维护任务”页面中，您可以查看和跟踪计划定期执行的建议维护任务。 这些任务与运行状况检查系统集成。 任务也可以从界面手动执行。

要转到操作功能板中的“维护”页面，请从AEM欢迎屏幕转到&#x200B;**工具 — 操作 — 功能板 — 维护**，或直接关注此链接：

`https://serveraddress:port/libs/granite/operations/content/maintenance.html`

“操作功能板”中提供了以下任务：

1. **修订清理**&#x200B;任务，位于&#x200B;**每日维护窗口**&#x200B;菜单下。
1. 位于&#x200B;**每日维护窗口**&#x200B;菜单下的&#x200B;**Lucene二进制文件清理**&#x200B;任务。
1. 位于&#x200B;**每周维护时段**&#x200B;菜单下的&#x200B;**工作流清除**&#x200B;任务。
1. **数据存储垃圾收集**&#x200B;任务，位于&#x200B;**每周维护时段**&#x200B;菜单下。
1. 位于&#x200B;**每周维护窗口**&#x200B;菜单下的&#x200B;**审核日志维护**&#x200B;任务。
1. 位于&#x200B;**每周维护时段**&#x200B;菜单下的&#x200B;**版本清除维护**&#x200B;任务。
1. **项目清除**&#x200B;维护任务，位于&#x200B;**每周维护时段**&#x200B;菜单下；使用&#x200B;**添加**&#x200B;选项。
1. 位于&#x200B;**每周维护时段**&#x200B;菜单下的&#x200B;**清除临时任务**&#x200B;维护任务；使用&#x200B;**添加**&#x200B;选项。

日常维护时段默认时间是凌晨2:00至凌晨5:00。配置为在每周维护窗口中运行的任务在星期六凌晨1:00到凌晨2:00之间运行。

您还可以通过按任意两个维护卡上的齿轮图标来配置时间安排：

![chlimage_1-126](assets/chlimage_1-126.png)

>[!NOTE]
>
>自AEM 6.1起，现有的维护窗口也可以配置为每月运行。

### 修订清理 {#revision-clean-up}

有关详细信息，请参阅[修订清理](/help/sites-deploying/revision-cleanup.md)。

### Lucene 二进制文件清理 {#lucene-binaries-cleanup}

通过使用Lucene二进制文件清理任务，您可以清除Lucene二进制文件并减少正在运行的数据存储大小要求。 每天回收Lucene的二进制流失，而不是早先依赖成功的[数据存储垃圾收集](/help/sites-administering/data-store-garbage-collection.md)运行。

尽管开发维护任务是为了减少Lucene相关的修订垃圾，但运行任务时普遍存在效率提高：

* 每周运行一次的数据存储垃圾收集任务可以更快地完成。
* 它也可能略微改善整体AEM性能。

您可以从&#x200B;**AEM > Tools > Operations > Maintenance > Daily Maintenance Window > Lucene Binaries Cleanup**&#x200B;访问Lucene二进制文件清理任务。

### 数据存储垃圾回收 {#data-store-garbage-collection}

有关数据存储垃圾收集的详细信息，请参阅专用的[数据存储垃圾收集](/help/sites-administering/data-store-garbage-collection.md)文档页面。

### 工作流清除 {#workflow-purge}

还可以从维护功能板中清除工作流。 要运行工作流清除任务，请执行以下操作：

1. 单击&#x200B;**每周维护时段**&#x200B;页面。
1. 在以下页面中，单击&#x200B;**工作流清除**&#x200B;信息卡中的&#x200B;**播放**。

>[!NOTE]
>
>有关工作流维护的详细信息，请参阅[管理工作流实例](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances)。

### 审核日志维护 {#audit-log-maintenance}

有关审核日志维护，请参阅[单独的文档页面。](/help/sites-administering/operations-audit-log.md)

### 版本清除 {#version-purge}

您可以计划版本清除维护任务，以自动删除旧版本。 此操作将手动使用[版本清除工具](/help/sites-deploying/version-purging.md)的需要降至最低。 您可以通过访问&#x200B;**Tools > Operations > Maintenance > Weekly Maintenance Window**&#x200B;并按照以下步骤来计划和配置版本清除任务：

1. 单击&#x200B;**添加**。
1. 从下拉菜单中选择&#x200B;**版本清除**。

   ![version_purge_maintenancetask](assets/version_purge_maintenancetask.png)

1. 要配置版本清除任务，请单击新创建的版本清除维护信息卡上的&#x200B;**齿轮**&#x200B;图标。

   ![version_purge_taskconfiguration](assets/version_purge_taskconfiguration.png)

**使用AEM 6.4**，您可以按如下方式停止“版本清除”维护任务：

* 自动 — 如果计划的维护窗口在任务完成之前关闭，则任务会自动停止。 当下一个维护窗口打开时，它将恢复。
* 手动 — 要手动停止任务，请在“版本清除”维护卡上单击&#x200B;**停止**&#x200B;图标。 在下次执行时，任务将安全地恢复。

>[!NOTE]
>
>停止维护任务意味着暂停其运行而不丢失已在进行的作业的跟踪。

>[!CAUTION]
>
>优化应经常运行版本清除任务的存储库大小。 当流量有限时，任务应安排在工作时间之外。

### 项目清除 {#project-purge}

<!--
Override the out-of-the-box Maintenance window configuration node under `/libs` by creating properties under the folder `/apps/settings/granite/operations/maintenance/granite_weekly`, `granite_daily` or `granite_monthly`. See the Maintenance Window table below for additional configuration details.

Enable the maintenance task by adding another node under the node above (name it `granite_ProjectPurgeTask`) with the appropriate properties. 
-->

在&#x200B;**Adobe项目清除配置** (com.adobe.cq.projects.purge.Scheduler)下配置OSGI属性。

### 临时任务清除 {#purge-of-ad-hoc-tasks}

<!--
Override the out-of-the-box Maintenance window configuration node under `/libs` by creating properties under the folder `/apps/settings/granite/operations/maintenance/granite_weekly`, `granite_daily` or `granite_monthly`.

See the Maintenance Window table below for additional configuration details. Enable the maintenance task by adding another node under the node above. Name it `granite_TaskPurgeTask`, with attribute `sling:resourceType` set to `granite/operations/components/maintenance/task` and attribute `granite.maintenance.name` set to `TaskPurge`. 
-->

在&#x200B;**临时任务清除** (`com.adobe.granite.taskmanagement.impl.purge.TaskPurgeMaintenanceTask`)下配置OSGI属性。

## 自定义维护任务 {#custom-maintenance-tasks}

自定义维护任务可以作为OSGi服务实施。 由于维护任务基础结构基于Apache Sling的作业处理，因此维护任务必须实施Java™接口` [org.apache.sling.event.jobs.consumer.JobExecutor](https://sling.apache.org/apidocs/sling7/org/apache/sling/event/jobs/consumer/JobExecutor.html)`。 此外，它必须声明若干服务注册属性以作为维护任务进行检测，如下所示：

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
   <td>布尔属性，定义用户是否可以停止任务。 如果任务声明它可停止，它必须在运行期间检查它是否被停止，然后相应地操作。 默认值为false。</td>
   <td>true</td>
   <td>可选</td>
  </tr>
  <tr>
   <td>granite.maintenance.mandatory</td>
   <td>布尔属性，定义任务是否为必需任务且必须定期运行。 如果任务是强制性的，但当前不在任何活动计划窗口中，则运行状况检查会报告此错误。 默认值为false。</td>
   <td>true</td>
   <td>可选</td>
  </tr>
  <tr>
   <td>granite.maintenance.name</td>
   <td>任务的唯一名称 — 该名称用于引用任务，只是简单名称。</td>
   <td>MyMaintenanceTask</td>
   <td>必填</td>
  </tr>
  <tr>
   <td>granite.maintenance.title</td>
   <td>为此任务显示的标题</td>
   <td>我的特别维护任务</td>
   <td>必填</td>
  </tr>
  <tr>
   <td>job.topics</td>
   <td>维护任务的唯一主题。<br /> Apache Sling作业处理将启动一个与此主题完全相同的作业来运行维护任务，当针对此主题注册任务时，该任务将运行。<br />主题必须以<i>com/adobe/granite/maintenance/job/</i>开头</td>
   <td>com/adobe/granite/maintenance/job/MyMaintenanceTask</td>
   <td>必填</td>
  </tr>
 </tbody>
</table>

除了上述服务属性之外，`JobConsumer`接口的`process()`方法必须通过添加应为维护任务执行的代码来实现。 提供的`JobExecutionContext`可用于输出状态信息，检查作业是否被用户停止并创建结果（成功或失败）。

对于不应在所有安装上运行维护任务的情况（例如，仅在发布实例上运行），您可以通过添加`@Component(policy=ConfigurationPolicy.REQUIRE)`使服务需要配置才能处于活动状态。 然后，您可以将相应的配置标记为依赖于存储库中的运行模式。 有关详细信息，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md#creating-the-configuration-in-the-repository)。

以下是自定义维护任务的示例，该任务从可配置的临时目录中删除过去24小时内修改过的文件：

src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java

<table>
 <tbody>
  <tr>
   <td><p> </p> <p><code>/*</code></p> <p><code> * #%L</code></p> <p><code> * sample-maintenance-task</code></p> <p><code> * %%</code></p> <p><code> * Copyright (C) 2014 Adobe</code></p> <p><code> * %%</code></p> <p><code> * Licensed under the Apache License, Version 2.0 (the "License");</code></p> <p><code> * you may not use this file except in compliance with the License.</code></p> <p><code> * You may obtain a copy of the License at</code></p> <p><code> * </code></p> <p><code> * <a href="https://www.apache.org/licenses/LICENSE-2.0">https://www.apache.org/licenses/LICENSE-2.0</a></code></p> <p><code> * </code></p> <p><code> * Unless required by applicable law or agreed to in writing, software</code></p> <p><code> * distributed under the License is distributed on an "AS IS" BASIS,</code></p> <p><code> * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.</code></p> <p><code> * See the License for the specific language governing permissions and</code></p> <p><code> * limitations under the License.</code></p> <p><code> * #L%</code></p> <p><code> */</code></p> <p><code> </code></p> <p><code>package com.adobe.granite.samples.maintenance.impl;</code></p> <p><code> </code></p> <p><code>import java.io.File;</code></p> <p><code>import java.util.Calendar;</code></p> <p><code>import java.util.Collection;</code></p> <p><code>import java.util.Map;</code></p> <p><code> </code></p> <p><code>import org.apache.commons.io.FileUtils;</code></p> <p><code>import org.apache.commons.io.filefilter.IOFileFilter;</code></p> <p><code>import org.apache.commons.io.filefilter.TrueFileFilter;</code></p> <p><code>import org.apache.felix.scr.annotations.Activate;</code></p> <p><code>import org.apache.felix.scr.annotations.Component;</code></p> <p><code>import org.apache.felix.scr.annotations.Properties;</code></p> <p><code>import org.apache.felix.scr.annotations.Property;</code></p> <p><code>import org.apache.felix.scr.annotations.Service;</code></p> <p><code>import org.apache.sling.commons.osgi.PropertiesUtil;</code></p> <p><code>import org.apache.sling.event.jobs.Job;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobConsumer;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionContext;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionResult;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutor;</code></p> <p><code>import org.slf4j.Logger;</code></p> <p><code>import org.slf4j.LoggerFactory;</code></p> <p><code> </code></p> <p><code>import com.adobe.granite.maintenance.MaintenanceConstants;</code></p> <p><code> </code></p> <p><code>@Component(metatype = true,</code></p> <p><code> label = "Delete Temp Files Maintenance Task",</code></p> <p><code> description = "Maintatence Task which deletes files from a configurable temporary directory which have been modified in the last 24 hours.")</code></p> <p><code>@Service</code></p> <p><code>@Properties({</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_NAME, value = "DeleteTempFilesTask", propertyPrivate = true),</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_TITLE, value = "Delete Temp Files", propertyPrivate = true),</code></p> <p><code> @Property(name = JobConsumer.PROPERTY_TOPICS, value = MaintenanceConstants.TASK_TOPIC_PREFIX</code></p> <p><code> + "DeleteTempFilesTask", propertyPrivate = true) })</code></p> <p><code>public class DeleteTempFilesTask implements JobExecutor {</code></p> <p><code> </code></p> <p><code> private static final Logger log = LoggerFactory.getLogger(DeleteTempFilesTask.class);</code></p> <p><code> </code></p> <p><code> @Property(label = "Temporary Directory", description="Temporary Directory. Defaults to the java.io.tmpdir system property.")</code></p> <p><code> private static final String PROP_TEMP_DIR = "temp.dir";</code></p> <p><code> </code></p> <p><code> private File tempDir;</code></p> <p><code> </code></p> <p><code> @Activate</code></p> <p><code> private void activate(Map&lt;string, object=""&gt; properties) {</code></p> <p><code> this.tempDir = new File(PropertiesUtil.toString(properties.get(PROP_TEMP_DIR),</code></p> <p><code> System.getProperty("java.io.tmpdir")));</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public JobExecutionResult process(Job job, JobExecutionContext context) {</code></p> <p><code> log.info("Deleting old temp files from {}.", tempDir.getAbsolutePath());</code></p> <p><code> Collection&lt;file&gt; files = FileUtils.listFiles(tempDir, new LastModifiedBeforeYesterdayFilter(),</code></p> <p><code> TrueFileFilter.INSTANCE);</code></p> <p><code> int counter = 0;</code></p> <p><code> for (File file : files) {</code></p> <p><code> log.debug("Deleting file {}.", file.getAbsolutePath());</code></p> <p><code> counter++;</code></p> <p><code> file.delete();</code></p> <p><code> // TODO - capture the output of delete() and do something useful with it</code></p> <p><code> }</code></p> <p><code> return context.result().message(String.format("Deleted %s files.", counter)).succeeded();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> /**</code></p> <p><code> * IOFileFilter which filters out files which have been modified in the last 24 hours.</code></p> <p><code> *</code></p> <p><code> */</code></p> <p><code> private static class LastModifiedBeforeYesterdayFilter implements IOFileFilter {</code></p> <p><code> </code></p> <p><code> private final long minTime;</code></p> <p><code> </code></p> <p><code> private LastModifiedBeforeYesterdayFilter() {</code></p> <p><code> Calendar cal = Calendar.getInstance();</code></p> <p><code> cal.add(Calendar.DATE, -1);</code></p> <p><code> this.minTime = cal.getTimeInMillis();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File dir, String name) {</code></p> <p><code> // this method is never actually called.</code></p> <p><code> return false;</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File file) {</code></p> <p><code> return file.lastModified() <= this.minTime;</code></p> <p><code> }</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code>}</code></p> <p><code>&lt;file&gt;&lt;/string,&gt;</code></p> <p> </p> </td>
  </tr>
 </tbody>
</table>

[experiencemanager-java-maintenancetask-sample](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample)- [src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample/blob/master/src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java)

部署服务后，该服务将显示在操作功能板UI中。 您可以将其添加到某个可用的维护计划中：

![chlimage_1-127](assets/chlimage_1-127.png)

此操作在/apps/granite/operations/config/maintenance/`schedule`/`taskname`处添加相应的资源。 如果任务依赖于运行模式，则必须在该节点上使用对此维护任务必须处于活动状态的运行模式值设置属性granite.operations.conditions.runmode。

## 系统概览 {#system-overview}

**系统概述仪表板**&#x200B;显示AEM实例的配置、硬件和运行状况的高级概述。 系统运行状况是透明的，所有信息都汇总在单个仪表板中。

>[!NOTE]
>
>您也可以[观看此视频](https://video.tv.adobe.com/v/21340)，了解系统概述仪表板的简介。

### 如何访问 {#how-to-access}

要访问系统概述仪表板，请导航到&#x200B;**工具>操作>系统概述**。

![system_overview_dashboard](assets/system_overview_dashboard.png)

### 系统概述仪表板说明 {#system-overview-dashboard-explained}

下表描述了“系统概述仪表板”中显示的所有信息。 当没有要显示的相关信息（例如，备份未进行，没有关键的运行状况检查）时，相应的部分将显示“没有条目”消息。

您还可以通过单击仪表板右上角的&#x200B;**下载**&#x200B;按钮，下载摘要仪表板信息的`JSON`文件。 `JSON`终结点为`/libs/granite/operations/content/systemoverview/export.json`，可以在`curl`脚本中使用它进行外部监视。

<table>
 <tbody>
  <tr>
   <td><strong>分区</strong></td>
   <td><strong>显示哪些信息</strong></td>
   <td><strong>什么时候重要</strong></td>
   <td><strong>链接到</strong></td>
  </tr>
  <tr>
   <td>运行状况检查</td>
   <td>
    <ul>
     <li>处于“严重”状态的检查列表</li>
     <li>处于警告状态的检查列表</li>
    </ul> </td>
   <td>以可视方式显示：<br />
    <ul>
     <li>严重检查的红色标记</li>
     <li>用于警告检查的橙色标记</li>
    </ul> </td>
   <td>
    <ul>
     <li>“运行状况报表”页面</li>
    </ul> </td>
  </tr>
  <tr>
   <td>维护任务</td>
   <td>
    <ul>
     <li>失败的任务列表</li>
     <li>当前正在运行的任务列表</li>
     <li>上次运行中成功的任务列表</li>
     <li>从未运行的任务列表</li>
     <li>未计划的任务列表</li>
    </ul> </td>
   <td><p>以可视方式指示：</p>
    <ul>
     <li>失败任务的红色标记</li>
     <li>用于运行任务的橙色标记（因为它们可能会影响性能）</li>
     <li>每个其他状态的灰色标记</li>
    </ul> </td>
   <td>
    <ul>
     <li>“维护任务”页</li>
    </ul> </td>
  </tr>
  <tr>
   <td>系统</td>
   <td>
    <ul>
     <li>操作系统和操作系统版本(例如，macOS X)</li>
     <li>从<a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/OperatingSystemMXBean.html#getSystemLoadAverage--">OperatingSystemMXBeanusable</a>检索到的系统平均负载</li>
     <li>磁盘空间（主目录所在的分区）</li>
     <li>最大栈，由<a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/MemoryMXBean.html#getHeapMemoryUsage--">MemoryMXBean</a>返回</li>
    </ul> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>实例</td>
   <td>
    <ul>
     <li>AEM版本</li>
     <li>运行模式列表</li>
     <li>启动实例的日期</li>
    </ul> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>存储库</td>
   <td>
    <ul>
     <li>Oak版本</li>
     <li>节点存储的类型（区段Tar或文档）
      <ul>
       <li>如果类型为文档，则显示文档存储的类型（RDB或Mongo）</li>
      </ul> </li>
     <li>如果有自定义数据存储：
      <ul>
       <li>对于文件数据存储，将显示路径</li>
       <li>对于S3数据存储，将显示S3存储段的名称</li>
       <li>对于共享的S3数据存储，将显示S3存储段的名称</li>
       <li>对于Azure数据存储，将显示容器</li>
      </ul> </li>
     <li>如果没有自定义外部数据存储，则会显示一条消息，指示此事实</li>
    </ul> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>分发代理</td>
   <td>
    <ul>
     <li>具有被阻止队列的代理列表</li>
     <li>错误配置的代理列表（“配置错误”）</li>
     <li>队列处理已暂停的代理列表</li>
     <li>空闲代理的列表</li>
     <li>正在运行的代理（当前正在处理条目）列表</li>
    </ul> </td>
   <td><p>以可视方式指示：</p>
    <ul>
     <li>红色标记表示被阻止的代理或配置错误</li>
     <li>用于暂停的试剂的橙色标记</li>
     <li>暂停、空闲或正在运行的代理的灰色标记<br /> </li>
    </ul> </td>
   <td>分发页面<br /> </td>
  </tr>
  <tr>
   <td>复制代理</td>
   <td>
    <ul>
     <li>具有被阻止队列的代理列表</li>
     <li>空闲代理的列表</li>
     <li>正在运行的代理（当前正在处理条目）列表</li>
    </ul> </td>
   <td><p>以可视方式显示：<br /> </p>
    <ul>
     <li>被阻止代理的红色标记</li>
     <li>暂停代理的灰色标记</li>
    </ul> </td>
   <td>复制页面</td>
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
     <li>工作流计数 — 给定状态（如果有）的工作流数量：
      <ul>
       <li>正在运行</li>
       <li>失败</li>
       <li>已暂停</li>
       <li>已中止</li>
      </ul> </li>
    </ul> <p>对于上面显示的每个状态，将执行查询，限制为400毫秒。 在400毫秒时，会显示截至该时间为止获得的条目数。</p> </td>
   <td><p>未解释：</p>
    <ul>
     <li>当存在处于意外状态的工作流和作业时，用户应进行调查。</li>
    </ul> </td>
   <td>工作流失败页面</td>
  </tr>
  <tr>
   <td>Sling 作业</td>
   <td><p>Sling作业计数 — 给定状态（如果有）的作业数：</p>
    <ul>
     <li>失败</li>
     <li>已排队</li>
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
   <td><p>预计数量：</p>
    <ul>
     <li>页</li>
     <li>资产</li>
     <li>标记</li>
     <li>可授权</li>
     <li>节点总数<br /> </li>
    </ul> <p>节点总数从nodeCounterMBean获得，其余统计信息从IndexInfoService获得。</p> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>备份</td>
   <td>显示“正在进行联机备份”（如果是）。</td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>索引</td>
   <td><p>显示：</p>
    <ul>
     <li>“正在编制索引”</li>
     <li>"正在进行查询"</li>
    </ul> <p>如果线程转储中存在索引或查询线程。</p> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>
