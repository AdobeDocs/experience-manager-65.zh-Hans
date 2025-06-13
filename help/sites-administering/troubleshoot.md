---
title: Adobe Experience Manager疑难解答
description: 了解如何对Adobe Experience Manager可能出现的一些问题进行故障诊断。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 2%

---

# Adobe Experience Manager疑难解答 {#troubleshooting-aem}

以下部分涵盖您在使用AEM (Adobe Experience Manager)时可能遇到的一些问题，以及有关如何解决这些问题的建议。

>[!NOTE]
>
>如果您正在排查AEM中的创作问题，请参阅[排查作者问题。](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>如果遇到问题，也值得检查实例（发行版和Service Pack）的[已知问题](/help/release-notes/release-notes.md)列表。

## 管理员疑难解答方案 {#troubleshooting-scenarios-for-administrators}

下表概述了管理员可以解决的问题：

<table>
 <tbody>
  <tr>
   <td><strong>角色</strong></td>
   <td><strong>问题 </strong></td>
  </tr>
  <tr>
   <td>系统管理员</td>
   <td><p>双击快速入门jar不起作用，或者使用其他程序（例如，存档管理器）打开jar文件</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> </td>
   <td><p>在CRX上运行的应用程序引发内存不足错误</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> </td>
   <td><p>双击AEM CM快速入门后，浏览器中不显示AEM欢迎屏幕</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> <p>管理员用户</p> </td>
   <td><p>创建线程转储</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> <p>管理员用户</p> </td>
   <td><p>检查未关闭的JCR会话</p> </td>
  </tr>
 </tbody>
</table>

## 安装问题 {#installation-issues}

有关以下故障排除方案的信息，请参阅[常见安装问题](/help/sites-deploying/troubleshooting.md#common-installation-issues)：

* 双击“快速入门”Jar对使用其他程序（如“存档管理器”）的JAR文件无效。
* 在CRX上运行的应用程序引发内存不足错误。
* 双击AEM快速入门后，浏览器中不显示AEM欢迎屏幕。

## 疑难解答分析方法 {#methods-for-troubleshooting-analysis}

### 创建线程转储 {#making-a-thread-dump}

线程转储是当前活动的所有Java™线程的列表。 如果AEM未正确响应，线程转储可以帮助您识别死锁或其他问题。

### 使用Sling线程转储器 {#using-sling-thread-dumper}

1. 打开&#x200B;**AEM Web控制台**；例如，在`https://localhost:4502/system/console/`。
1. 选择&#x200B;**Status**&#x200B;选项卡下的&#x200B;**Threads**。

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### 使用jstack（命令行） {#using-jstack-command-line}

1. 查找AEM Java™实例的PID（进程ID）。

   例如，您可以使用`ps -ef`或`jps`。

1. 运行：

   `jstack <pid>`

1. 显示线程转储。

>[!NOTE]
>
>您可以使用`>>`输出重定向将线程转储附加到日志文件：
>
>`jstack <pid> >> /path/to/logfile.log`

有关详细信息，请参阅[如何从JVM进行线程转储](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html)文档

### 检查未关闭的JCR会话 {#checking-for-unclosed-jcr-sessions}

在为AEM WCM开发功能时，可能会打开JCR会话（相当于打开数据库连接）。 如果打开的会话从未关闭，则您的系统可能会遇到以下症状：

* 系统变慢了。
* 您可以看到许多CacheManager： resizeAll条目（在日志文件中）；以下数字(size=&lt;x>)显示高速缓存数，每个会话打开多个高速缓存。
* 系统有时内存不足（在数小时、数天或数周后，具体取决于严重程度）。

要开始分析未关闭的会话，请参阅知识库文章[未关闭的资源解析程序](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23761)。

### 使用Adobe Experience Manager Web Console {#using-the-adobe-experience-manager-web-console}

OSGi捆绑包的状态还可以提供可能问题的早期指示。

1. 打开&#x200B;**AEM Web控制台**；例如，在`https://localhost:4502/system/console/`。
1. 选择&#x200B;**OSGI**&#x200B;选项卡下的&#x200B;**包**。
1. 检查：

   * 捆绑包的状态。 如果有任何组件处于非活动或未满足状态，请尝试停止并重新启动捆绑包。 如果问题仍然存在，请使用其他方法进行进一步调查。
   * 是否有任何捆绑包缺少依赖项。 单击单个捆绑包名称（它是一个链接），可以查看此类详细信息（以下示例没有任何问题）：

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
