---
title: 已监视文件夹AEM Forms
seo-title: Watched folder in AEM Forms
description: 管理员可以将文件夹置于监视中，并在文件置于监视的文件夹中时启动工作流、服务或脚本操作。
seo-description: An administrator can put a folder on watch and start a workflow, service, or script operation when a file is placed in the folder being watched.
uuid: 39eac0fd-8212-46ff-b75d-8b4320d448a9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: db38972c-be3f-49fd-8cc1-45b16ed244af
docset: aem65
exl-id: fbf5c7c3-cb01-4fda-8e5d-11d56792d4bf
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '7149'
ht-degree: 0%

---

# 已监视文件夹AEM Forms{#watched-folder-in-aem-forms}

管理员可以配置网络文件夹（称为“监视文件夹”），以便当用户在“监视文件夹”中放置文件(如PDF文件)时，会启动预配置的工作流、服务或脚本操作来处理添加的文件。 服务执行指定操作后，会将结果文件保存在指定的输出文件夹中。 有关工作流、服务和脚本的更多信息，请参阅 [处理文件的各种方法](#variousmethodsforprocessingfiles).

## 创建监视文件夹 {#create-a-watched-folder}

您可以使用以下方法之一在文件系统上创建监视文件夹：

* 在配置“监视文件夹”配置节点的属性时，在folderPath属性中键入父目录的完整路径，并附加要创建的“监视文件夹”的名称，如以下示例所示： `C:/MyPDFs/MyWatchedFolder`
的 
`MyWatchedFolder`文件夹不存在，AEM Forms会尝试在指定路径下创建文件夹。

* 在配置“监视文件夹”端点之前，在文件系统上创建文件夹，然后在folderPath属性中提供完整路径。 有关folderPath属性的详细信息，请参阅 [已监视文件夹属性](#watchedfolderproperties).

>[!NOTE]
>
>在群集环境中，用作监视文件夹的文件夹必须在文件系统或网络上可访问、可写和共享。 群集的每个应用程序服务器实例都必须有权访问同一共享文件夹。 在Windows上，在所有服务器上创建一个映射的网络驱动器，并在folderPath属性中指定映射的网络驱动器的路径。

## 创建监视文件夹配置节点 {#create-watched-folder-configuration-node}

要配置监视文件夹，请创建监视文件夹配置节点。 执行以下步骤以创建配置节点：

1. 以管理员身份登录到CRX-DE lite，然后导航到/etc/fd/watchfolder/config文件夹。

1. 创建类型的节点 `nt:unstructured`. 例如，watchedfolder

   >[!NOTE]
   >
   >“监视文件夹”节点名称不能包含空格和特殊字符。

1. 将以下属性添加到节点：

   * `folderPath`
   * `inputProcessorType`
   * `inputProcessorId`
   * `outputFilePattern`

   有关支持属性的完整列表，请参阅 [已监视文件夹属性](#watchedfolderproperties).

1. 单击 **全部保存**. 创建节点并保存属性后。 的 `input`, `result`, `failure`, `preserve`和 `stage`文件夹是在 `folderPath` 属性。

   扫描作业在定义的时间间隔内开始扫描“监视文件夹”。

## 已监视文件夹属性 {#watchedfolderproperties}

您可以为已监视文件夹配置以下属性。

* **folderPath（字符串）**:要按定义的时间间隔扫描的文件夹的路径。 对于群集环境，文件夹必须位于共享位置，所有服务器都具有对服务器的完全访问权限。 它是强制属性。
* **inputProcessorType（字符串）**:要启动的进程的类型。 您可以指定工作流、脚本或服务。 它是强制属性。
* **inputProcessorId（字符串）**:inputProcessorId属性的行为基于为inputProcessorType属性指定的值。 它是强制属性。 下表详细列出了inputProcessorType属性的所有可能值以及inputProcessorType属性的相应条件：

   * 对于工作流，指定要执行的工作流模型。 例如， /etc/workflow/models/&lt;workflow_name>/jcr:content/model
   * 对于脚本，指定要执行的脚本的JCR路径。 例如， /etc/fd/watchfolder/test/testScript.ecma
   * 对于服务，请指定用于查找OSGi服务的过滤器。 该服务将注册为com.adobe.aemfd.watchfolder.service.api.ContentProcessor Interface的实现。

* **runModes（字符串）**:用于工作流执行的允许运行模式的逗号分隔列表。 以下是一些示例：

   * 作者

   * 发布

   * 作者，发布

   * 发布，创作

>[!NOTE]
>
>如果托管监视文件夹的服务器没有任何指定的运行模式，则无论服务器上的运行模式如何，监视文件夹都将始终激活。

* **outputFilePattern（字符串）**:输出文件的模式。 您可以指定文件夹或文件模式。 如果指定了文件夹模式，则输出文件的名称将如工作流中所述。 如果指定了文件模式，则输出文件的名称如文件模式中所述。 [文件和文件夹模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) 还可以为输出文件指定目录结构。 它是强制属性。

* **stageFileExpirationDuration（长，默认–1）**:在输入文件/文件夹（已被拾取以进行处理）之前等待的秒数，应视为已超时并标记为失败。 仅当此属性的值为正数时，才会激活此过期机制。

>[!NOTE]
>
>即使使用此机制将输入标记为已超时，它仍可能在后台处理，但所花费的时间比预期的要多。 如果在超时机制启动之前已使用输入内容，则处理过程甚至可能在稍后继续完成，并将输出转储到结果文件夹中。 如果在超时前未使用内容，则在稍后尝试使用内容时，处理很可能会出错，并且此错误也将记录在同一输入的失败文件夹中。 另一方面，如果对输入的处理从未因间歇性作业/工作流失火而激活（这是过期机制要解决的情况），则当然不会发生这两种情况。 因此，对于因超时而标记为失败的失败文件夹中的任何条目（查找格式为“File not processed after ampied time， marking as failure！”的消息） 在失败日志中)，建议扫描结果文件夹（以及失败文件夹本身，以查找同一输入的另一个条目），以检查之前描述的任何可能性是否实际发生。

* **deleteExpiredStageFileOnlyWhenThrottled（布尔值，默认为true）：** 过期机制是否应仅在监视文件夹被限制时激活。 该机制对于受限制的监视文件夹更相关，因为在未处理状态（由于间歇性作业/工作流失火）中存在的少量文件在启用限制时可能会阻塞整个批次的处理。 如果此属性保持为true（默认），则不会为未限制的监视文件夹激活过期机制。 如果属性保留为false，则只要stageFileExpirationDuration属性是正数，机制将始终激活。

* **pollInterval(Long)**:扫描监视文件夹以进行输入的间隔，以秒为单位。 除非启用“限制”设置，否则轮询间隔应大于处理平均作业的时间；否则，系统可能会变得过载。 默认值为 5。有关其他信息，请参阅批量大小说明。 轮询间隔的值必须大于或等于1。
* **excludeFilePattern（字符串）**:分号(;)分隔的模式列表，已监视文件夹使用这些模式确定要扫描和选取的文件和文件夹。 不会扫描任何具有此模式的文件或文件夹进行处理。 当输入的文件夹包含多个文件时，此设置非常有用。 文件夹的内容可以复制到一个名称由“监视文件夹”选取的文件夹中。 这会阻止监视文件夹在将文件夹完全复制到输入文件夹之前提取待处理的文件夹。 默认值为null。
您可以使用 [文件模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) 要排除：

   * 具有特定文件扩展名的文件；例如， &#42;.dat， &#42;.xml， .pdf， &#42;.&#42;
   * 具有特定名称的文件；例如，数据&#42; 将排除名为data1、data2等的文件和文件夹。
   * 名称和扩展名中具有复合表达式的文件，如以下示例所示：

      * 数据[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
      * &#42;。[dD][Aa]&#39;port&#39;
      * &#42;。[Xx][Mm][Ll]

有关文件模式的更多信息，请参阅 [关于文件模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

* **includeFilePattern（字符串）**:分号(;)分隔的模式列表，已监视文件夹使用这些模式确定要扫描和选取的文件夹和文件。 例如，如果输入IncludeFilePattern&#42;，所有与输入匹配的文件和文件夹&#42; 被接走。 这包括名为input1、input2等的文件和文件夹。 默认值为 &#42; 和指示所有文件和文件夹。 您可以使用文件模式包括：

   * 具有特定文件扩展名的文件；例如， &#42;.dat， &#42;.xml， .pdf， &#42;.&#42;
   * 具有特定名称的文件；例如，数据。&#42; 将包含名为data1、data2等的文件和文件夹。

* 名称和扩展名中具有复合表达式的文件，如以下示例所示：

   * 数据[0-9][0-9][0-9].[dD][aA]&#39;port&#39;

      * &#42;。[dD][Aa]&#39;port&#39;
      * &#42;。[Xx][Mm][Ll]

有关文件模式的更多信息，请参阅 [关于文件模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)

* **waitTime(Long)**:文件夹或文件创建后，在扫描之前等待的时间（以毫秒为单位）。 例如，如果等待时间为3,600,000毫秒（一小时），而文件是在一分钟前创建的，则此文件将在59分钟或更久之后被提取。 默认值为 0。此设置有助于确保文件或文件夹已完全复制到输入文件夹。 例如，如果要处理大文件，并且需要10分钟才能下载该文件，请将等待时间设置为10&#42;60 &#42;1000毫秒。 如果文件未保持10分钟，则阻止“已监视文件夹”扫描文件。
* **purgeDuration(Long)**:结果文件夹中的文件和文件夹如果比此值旧，则会清除它们。 此值以天为单位。 此设置有助于确保结果文件夹不会变满。 值为–1天表示从不删除结果文件夹。 默认值为–1。
* **resultFolderName（字符串）**:保存结果的文件夹。 如果结果未显示在此文件夹中，请检查失败文件夹。 只读文件不会处理，而是保存在失败文件夹中。 此值可以是具有以下文件模式的绝对路径或相对路径：

   * %F =文件名前缀
   * %E =文件扩展名
   * %Y =年（满）
   * %y =年（最后两位）
   * %M =月
   * %D =每月的某天
   * %d =每年的某天
   * %H =小时（24小时制）
   * %h =小时（12小时制）
   * %m =分钟
   * %s =秒
   * %l =毫秒
   * %R =随机数（介于0和9之间）
   * %P =进程ID或作业ID

   例如，如果在2009年7月17日晚上8点，并且您指定了C:/Test/WF0/failure/%Y/%M/%D/%H/，则结果文件夹为C:/Test/WF0/failure/2009/07/17/20

   如果路径不是绝对路径，而是相对路径，则会在“监视文件夹”内创建文件夹。 默认值为result/%Y/%M/%D/，这是监视文件夹内的结果文件夹。 有关文件模式的更多信息，请参阅 [关于文件模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

>[!NOTE]
>
>结果文件夹的大小越小，“监视的文件夹”的性能就越好。 例如，如果监视文件夹的估计负载每小时为1000个文件，请尝试诸如result/%Y%M%D%H之类的模式，以便每小时创建一个新子文件夹。 如果负载较小（例如，每天1000个文件），则可以使用诸如result/%Y%M%D之类的模式。

* **failureFolderName（字符串）**:保存失败文件的文件夹。 此位置始终相对于已监视文件夹。 可以使用文件模式，如“结果文件夹”中所述。 只读文件不会处理，而是保存在失败文件夹中。 默认值为failure/%Y/%M/%D/。
* **preserveFolderName（字符串）：** 成功处理后文件的存储位置。 路径可以是绝对路径、相对路径或空目录路径。 可以使用文件模式，如“结果文件夹”中所述。 默认值为preserve/%Y/%M/%D/。
* **batchSize(Long)**:每次扫描要选取的文件或文件夹数。 用于防止系统过载；一次扫描过多文件可能会导致崩溃。 默认值为 2。

   “投票间隔”和“批量大小”设置决定“监视文件夹”在每次扫描中接收的文件数。 监视文件夹使用石英线程池扫描输入文件夹。 线程池与其他服务共享。 如果扫描间隔较小，则线程会经常扫描输入文件夹。 如果文件经常被放入“监视文件夹”中，则扫描间隔应保持较小。 如果文件不常被删除，请使用较大的扫描间隔，以便其他服务可以使用线程。

   如果删除的文件量很大，请使批处理大小变大。 例如，如果监视文件夹端点启动的服务每分钟可处理700个文件，并且用户以相同的速率将文件放入输入文件夹，则将“批量大小”设置为350，将“投票间隔”设置为30秒可帮助监视文件夹性能，而不会太频繁地扫描监视文件夹。

   将文件放入监视文件夹后，会在输入中列出文件，如果每秒进行扫描，会降低性能。 增加扫描间隔可以提高性能。 如果要删除的文件量较小，请相应地调整“批处理大小”和“轮询间隔”。 例如，如果每秒删除10个文件，请尝试将pollInterval设置为1秒，将批量大小设置为10

* **throttleOn（布尔值）**:选择此选项后，将限制AEM Forms在任何给定时间处理的已监视文件夹作业的数量。 最大作业数由批量大小值确定。 默认值为true。 (请参阅 [关于限制](../../forms/using/watched-folder-in-aem-forms.md#p-about-throttling-p).)

* **overwriteDuplicateFilename（布尔值）**:设置为True时，将覆盖结果文件夹和保留文件夹中的文件。 当设置为False时，名称将使用带数字索引后缀的文件和文件夹。 默认值为False。
* **preserveOnFailure（布尔值）**:在无法对服务执行操作时保留输入文件。 默认值为true。
* **inputFilePattern（字符串）**:指定监视文件夹的输入文件模式。 创建文允许列表件。
* **异步（布尔值）**:将调用类型标识为异步或同步。 默认值为true（异步）。 文件处理是一项消耗资源的任务，请将异步标志的值保持为true，以防止阻塞扫描作业的主线程。 在群集环境中，必须保持标志为true，才能对在可用服务器上处理的文件进行负载平衡。 如果标记为false，则扫描作业会尝试在其自身线程中按顺序对每个顶级文件/文件夹执行处理。 在没有特定原因（例如，基于工作流的单服务器设置处理）的情况下，请勿将标记设置为false。

>[!NOTE]
>
>根据设计，工作流是异步的。 即使将值设置为false，工作流也会在异步模式下启动。

* **已启用（布尔值）**:停用并激活已监视文件夹的扫描。 将enabled设置为true，以开始扫描“监视文件夹”。 默认值为true。
* **payloadMapperFilter:** 将文件夹配置为监视文件夹后，会在监视文件夹中创建文件夹结构。 该结构具有文件夹，用于提供输入、接收输出（结果）、保存故障数据、保留长寿命进程的数据以及保存各个阶段的数据。 已监视文件夹的文件夹结构可以用作以Forms为中心的工作流的有效负载。 有效负载映射器允许您定义有效负载的结构，该结构使用监视文件夹进行输入、输出和处理。 例如，如果您使用默认映射器，它会将“监视文件夹”的内容与 [负载]\输入和 [负载]\output文件夹。 提供了两个现成的有效负载映射器实施。 如果您没有 [自定义实施](../../forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter)，使用一个现成的实施：

   * **默认映射器：** 使用默认有效负载映射器将已监视文件夹的输入和输出内容保留在有效负载中单独的输入和输出文件夹中。 此外，在工作流的有效负荷路径中，使用 [负载]/input/和 [负载]/output路径来检索和保存内容。

   * **简单的基于文件的有效负载映射器：** 使用基于简单文件的有效负载映射器将输入和输出内容直接保留在有效负载文件夹中。 它不会创建任何额外的层次结构，如默认映射器。

### 自定义配置参数 {#custom-configuration-parameters}

除了上面列出的监视文件夹配置属性外，您还可以指定自定义配置参数。 自定义参数将传递到文件处理代码。 它允许代码根据参数的值更改其行为。 要指定参数，请执行以下操作：

1. 登录到CRXDE-Lite，然后导航到“监视文件夹”配置节点。
1. 添加属性参数。&lt;property_name> 到“监视文件夹”配置节点。 属性的类型只能是Boolean、Date、Decimal、Double、Long和String。 您可以指定单值和多值属性。

>[!NOTE]
>
>如果属性的数据类型为Double，则在此类属性的值中指定一个小数点。 对于所有属性，其中数据类型为Double，且值中未指定小数点，则类型将转换为Long。

这些属性将作为Map类型的不可更改映射传递&lt;string object=&quot;&quot;> 到处理代码。 处理代码可以是ECMAScript、工作流或服务。 为属性提供的值在映射中以键值对的形式提供。 键是属性的名称，值是属性的值。 有关自定义配置参数的更多信息，请参阅下图：

![具有必需属性的监视文件夹配置节点示例、一些可选属性和一些配置参数](assets/custom-configuration-parameters.png)

具有必需属性的监视文件夹配置节点示例、一些可选属性和一些配置参数。

#### 工作流程的可变变量 {#mutable-variables-for-workflows}

您可以为基于工作流的文件处理方法创建可变变量。 这些变量用作在工作流步骤之间流动的数据的容器。 要创建此类变量，请执行以下操作：

1. 登录到CRXDE-Lite，然后导航到“监视文件夹”配置节点。

1. 添加属性workflow.var。&lt;variable_name> 到“监视文件夹”配置节点。

   属性的类型只能是Boolean、Date、Decimal、Double、Long和String。 还支持多值属性。 对于多值属性，可用于工作流步骤的值是指定类型的数组。

   >[!NOTE]
   >
   >如果属性的数据类型为Double，则在此类属性的值中指定一个小数点。 对于所有属性，其中数据类型为Double，且值中未指定小数点，则类型将转换为Long。

>[!NOTE]
>
>JCR规范要求属性具有默认值。 默认值可用于工作流处理步骤。 因此，请指定适当的默认值。

![custom-configuration-parameters2](assets/custom-configuration-parameters2.png)

## 处理文件的各种方法 {#variousmethodsforprocessingfiles}

您可以启动工作流、服务或脚本以处理位于监视文件夹中的文档。

### 使用服务处理已监视文件夹的文件   {#using-a-service-to-process-files-of-a-watched-folder-nbsp}

服务是 `com.adobe.aemfd.watchfolder.service.api.ContentProcessor` 界面。 它已在OSGi中注册，并带有一些自定义属性。 实施的自定义属性使其具有唯一性，并有助于识别实施。

#### ContentProcessor界面的自定义实施 {#custom-implementation-of-the-contentprocessor-interface}

自定义实施接受处理上下文（com.adobe.aemfd.watchfolder.service.api.ProcessorContext类型的对象），从上下文中读取输入文档和配置参数，处理输入，并将输出添加回上下文。 ProcessorContext具有以下API:

* **getWatchFolderId**:返回已监视文件夹的ID。
* **getInputMap**:返回映射类型的映射。 映射的键是输入文件的文件名和包含文件内容的文档对象。 使用getinputMap API读取输入文件。
* **getConfigParameters**:返回“映射”类型的不可变映射。 该映射包含监视文件夹的配置参数。

* **setResult**:ContentProcessor实施使用API将输出文档写入结果文件夹。 您可以为setResult API的输出文件提供名称。 API可能会根据指定的输出文件夹/文件模式选择使用或忽略提供的文件。 如果指定了文件夹模式，则输出文件的名称将如工作流中所述。 如果指定了文件模式，则输出文件的名称如文件模式中所述。

例如，以下代码是ContentProcessor界面的自定义实现，具有自定义foo=bar属性。

```java
@Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
@Service(value = {OutputWriter.class, ContentProcessor.class})
@Property(name = "foo", value = "bar")
public class OutputWriter implements ContentProcessor {
```

While [配置监视文件夹](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p)，如果将inputProcessorId属性指定为(foo=bar)，将inputProcessorType属性指定为Service，则上述服务（自定义实施）将用于处理“监视文件夹”的输入文件。

以下示例也是ContentProcessor界面的自定义实现。 在示例中，服务接受输入文件，将文件复制到临时位置，并返回包含文件内容的文档对象。 文档对象的内容将保存到结果文件夹中。 结果文件夹的物理路径在 [监视文件夹配置节点](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

```java
@Component(immediate = true)
@Service(value = ContentProcessor.class)
@Property(name = "serviceSelector", value = "testProcessor1")
public class TestContentProcessor1 implements ContentProcessor {
    @Override
    public void processInputs(ProcessorContext context) throws Exception {
        Map.Entry<String, Document> e = context.getInputMap().entrySet().iterator().next();
        File f = new File((String) context.getConfigParameters().get("tempDir"),
                context.getConfigParameters().get("outPrefix") + e.getKey());
        e.getValue().copyToFile(f);
        context.setResult(f.getName(), new Document(f, true));
    }
}
```

### 使用脚本处理已监视文件夹的文件 {#using-scripts-to-process-files-of-a-watched-folder}

脚本是ECMAScript投诉自定义代码，编写用于处理置于监视文件夹中的文档。 脚本表示为JCR节点。 除了标准ECMAScript变量（日志、sling等）之外，脚本还具有一个变量processorContext。 变量的类型为ProcessorContext。 ProcessorContext具有以下API:

* **getWatchFolderId**:返回已监视文件夹的ID。
* **getInputMap**:返回映射类型的映射。 映射的键是输入文件的文件名和包含文件内容的文档对象。 使用getinputMap API读取输入文件。
* **getConfigParameters**:返回“映射”类型的不可变映射。 该映射包含监视文件夹的配置参数。
* **setResult**:ContentProcessor实施使用API将输出文档写入结果文件夹。 您可以为setResult API的输出文件提供名称。 API可能会根据指定的输出文件夹/文件模式选择使用或忽略提供的文件。 如果指定了文件夹模式，则输出文件的名称将如工作流中所述。 如果指定了文件模式，则输出文件的名称如文件模式中所述。

以下代码是一个ECMAScript示例。 它接受输入文件，将文件复制到临时位置，并返回包含文件内容的文档对象。 文档对象的内容将保存到结果文件夹中。 结果文件夹的物理路径在 [监视文件夹配置节点](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

>[!NOTE]
>
>输出文件夹和文件名前缀取决于“监视文件夹”配置参数。

```java
var inputMap = processorContext.getInputMap();
var params = processorContext.getConfigParameters();
var entry = inputMap.entrySet().iterator().next();
var tempFile = new Packages.java.io.File(params.get("tempDir"), params.get("outPrefix") + entry.getKey());
entry.getValue().copyToFile(tempFile);
processorContext.setResult(tempFile.getName(), new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true));
```

#### 脚本位置和安全注意事项 {#location-of-scripts-and-security-considerations}

默认情况下，会提供一个容器文件夹(/etc/fd/watchfolder/scripts)，客户可以在其中放置其脚本，且watch-folder框架使用的默认服务用户具有从此位置读取脚本的必要权限。

如果您计划将脚本放置在自定义位置，则默认服务用户可能没有对自定义位置的读取权限。 对于此类情景，请执行以下步骤以为自定义位置提供必要的权限：

1. 以编程方式或通过控制台https://&#39;创建系统用户[服务器]:[端口]“/crx/explorer”。 您还可以使用现有系统用户。 在此处与系统用户合作，而不是与普通用户合作非常重要。
1. 在存储脚本的自定义位置上为新创建或现有系统用户提供读取权限。 您可以有多个自定义位置。 至少为所有自定义位置提供读取权限。
1. 在Felix配置控制台(/system/console/configMgr)中，找到watch-folders的服务用户映射。 此映射类似于“映射：adobe-aemds-core-watch-folder=...&#39;。
1. 单击映射。 对于条目“adobe-aemds-core-watch-folder:scripts=fd-service”，将fd-service更改为自定义系统用户的ID。 单击保存。

现在，您可以使用配置的自定义位置来保存脚本。

### 使用工作流处理已监视文件夹的文件 {#using-a-workflow-to-process-files-of-a-watched-folder}

工作流可让您自动执行Experience Manager活动。 工作流由一系列按特定顺序执行的步骤组成。 每个步骤都会执行不同的活动，例如激活页面或发送电子邮件消息。 工作流可以与存储库、用户帐户和Experience Manager服务中的资产进行交互。 因此，工作流可以协调复杂的工作。

* 在创建工作流之前，请考虑以下几点：
* 步骤的输出必须可用于所有后续步骤。
这些步骤必须能够更新（甚至删除）由先前步骤生成的现有输出。
* 可变变量用于在各个步骤之间流动自定义动态数据。

请执行以下步骤以使用工作流处理文件：

1. 创建的实施 `com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextProcessor` 界面。 它类似于为服务创建的实施。

   >[!NOTE]
   >
   >您可以在ECMAScript中完全创建完整的实施。

1. 在工作流的步骤中，找到com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService类型的OSGi服务，然后使用以下参数调用该服务的execute()方法。

   * WorkflowContextProcessor界面的自定义实施
   * workItem
   * workflowSession
   * 元数据

如果您使用Java编程语言来实施工作流，则AEM工作流引擎会为workItem、workflowSession和元数据变量提供值。 这些变量将作为参数传递给自定义WorkflowProcess实施的execute()方法。

如果您使用ECMAScript来实施工作流，则AEM工作流引擎会为graniteWorkItem、graniteWorkflowSession和元数据变量提供值。 这些变量将作为参数传递到WorkflowContextService.execute()方法。

processWorkflowContext()的参数是com.adobe.aemfd.watchfolder.workflow.api.WorkflowContext类型的对象。 WorkflowContext界面具有以下API，以便于考虑上述特定于工作流的注意事项：

* getWorkItem:返回WorkItem变量的值。 变量将被传递到WorkflowContextService.execute()方法。
* getWorkflowSession:返回WorkflowSession变量的值。 变量将被传递到WorkflowContextService.execute()方法。
* getMetadata:返回元数据变量的值。 变量将被传递到WorkflowContextService.execute()方法。
* getCommittedVariables:返回表示按先前步骤设置的变量的只读对象映射。 如果在以前的任何步骤中未修改变量，则会返回在配置“监视文件夹”期间指定的默认值。
* getCommittedResults:返回只读文档映射。 该映射表示由前一步骤生成的输出文件。
* setVariable:WorkflowContextProcessor实施使用变量来处理表示在步骤之间流动的自定义动态数据的变量。 变量的名称和类型与在 [配置监视文件夹](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p). 要更改变量的值，请使用非空值调用setVariable API。 要删除变量，请调用值为null的setVariable()。

还提供以下ProcessorContext API:

* getWatchFolderId:返回已监视文件夹的ID。
* getInputMap:返回Map类型的映射&lt;string document=&quot;&quot;>. 映射的键是输入文件的文件名和包含文件内容的文档对象。 使用getinputMap API读取输入文件。
* getConfigParameters:返回类型为“映射”的不可变映射&lt;string object=&quot;&quot;>. 该映射包含监视文件夹的配置参数。
* setResult:ContentProcessor实施使用API将输出文档写入结果文件夹。 您可以为setResult API的输出文件提供名称。 API可能会根据指定的输出文件夹/文件模式选择使用或忽略提供的文件。 如果指定了文件夹模式，则输出文件的名称将如工作流中所述。 如果指定了文件模式，则输出文件的名称如文件模式中所述

在工作流中使用setResult API时，请考虑以下事项：

* 要添加有助于整个工作流输出的新输出文档，请调用setResult API，其中的文件名未用作上一步中的输出文件名。
* 要更新上一步生成的输出，请使用上一步已使用的文件名调用setResult API。
* 要删除由上一步生成的输出，请调用setResult ，其中的文件名已由上一步使用，并且为null作为内容。

>[!NOTE]
>
>在任何其他方案中调用内容为null的setResult API时，都会导致错误。

以下示例作为工作流步骤进行实施。 在此示例中，ECMAscript使用变量stepCount跟踪当前工作流实例中调用步骤的次数。
输出文件夹的名称是当前步骤号、原始文件名和在outPrefix参数中指定的前缀的组合。

ECMAScript获取工作流上下文服务的引用并创建WorkflowContextProcessor接口的实现。 WorkflowContextProcessor实施接受输入文件，将文件复制到临时位置，并返回表示复制文件的文档。 根据布尔变量purgePrevious的值，当前步骤将删除上次在当前工作流实例中启动该步骤时由同一步骤生成的输出。 最后，调用wfSvc.execute方法来执行WorkflowContextProcessor实现。 输出文档的内容将保存在“监视文件夹”配置节点中所述物理路径的结果文件夹中。

```javascript
log.error("Watch-folder workflow script called for step: " + graniteWorkItem.getNode().getTitle());
var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
// Custom WorkflowContextProcessor implementation which defines the processWorkflowContext() method purely in JS
var impl = { processWorkflowContext: function (wfContext) {
    var wfId = wfContext.getWatchFolderId();
    var inputMap = wfContext.getInputMap();
    var paramMap = wfContext.getConfigParameters();
    var preResults = wfContext.getCommittedResults();
    var preVars = wfContext.getCommittedVariables();
    log.info("WF ID: " + wfId); // workflowId of type String
    log.info("Inputs: " + inputMap); // Input map of type Map<String, Document>
    log.info("Params: " + paramMap); // Config params of type Map<String, Object>
    log.info("Old results: " + preResults);
    log.info("Old variables: " + preVars);
    var currStepNumber = new Packages.java.lang.Long(new Packages.java.lang.Long(preVars.get("stepCount")).longValue() + 1);
    log.info("Current step number: " + currStepNumber);
    wfContext.setVariable("stepCount", currStepNumber);
    var entry = inputMap.entrySet().iterator().next();
    var tempFile = new Packages.java.io.File(paramMap.get("tempDir"), paramMap.get("outPrefix") + "STEP-" + currStepNumber + "-" + entry.getKey());
    entry.getValue().copyToFile(tempFile);
    var fName = tempFile.getName();
    var outDoc = new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true);
    wfContext.setResult(tempFile.getName(), outDoc);
    var prevStepOutName = paramMap.get("outPrefix") + "STEP-" + (currStepNumber - 1) + "-" + entry.getKey();
    if (preResults.containsKey(prevStepOutName) && paramMap.get("purgePrevious").booleanValue()) {
        log.info("Purging previous step output " + prevStepOutName);
        wfContext.setResult(prevStepOutName, null);
    }
} }
wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
log.info("Exiting workflow script!")
```

### 创建负载映射器过滤器，将已监视文件夹的结构映射到工作流的负载 {#create-payload-mapper-filter-to-map-structure-of-a-watched-folder-to-the-payload-of-a-workflow}

创建监视文件夹时，它会在监视的文件夹中创建文件夹结构。 文件夹结构具有暂存、结果、保留、输入和失败文件夹。 文件夹结构可用作工作流的输入有效负荷，并接受来自工作流的输出。 它还可以列出故障点（如果有）。

如果有效负载的结构与监视文件夹的结构不同，则可以编写自定义脚本以将监视文件夹的结构映射到有效负载。 这种脚本称为负载映射器过滤器。 开箱即用地，AEM Forms提供了有效负载映射器过滤器，用于将已监视文件夹的结构映射到有效负载。

#### 创建自定义有效负载映射器过滤器 {#creating-a-custom-payload-mapper-filter}

1. 下载 [Adobe客户端SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/).
1. 在基于Maven的项目的生成路径中设置客户端SDK。 要开始，您可以在选择的IDE中下载并打开以下基于Maven的项目。
1. 编辑示例包中可用的有效负载映射器过滤器代码，以满足您的要求。
1. 使用maven创建自定义有效负载映射器筛选器的包。
1. 使用 [AEM包控制台](https://localhost:4502/system/console/bundles) 来安装包。

   现在，自定义负载映射器过滤器列在AEM监视文件夹UI中。 您可以将其用于工作流。

   以下示例代码为相对于有效负载保存的文件实施基于文件的简单映射器。 您可以使用它开始操作。

   ```java
   package com.adobe.aemfd.watchfolder.workflow;
   import com.adobe.aemfd.docmanager.Document;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.PayloadMapper;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowExecutionContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowInitializationContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowVariable;
   import com.adobe.granite.workflow.exec.Workflow;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.ResourceResolver;
   import javax.jcr.Binary;
   import javax.jcr.Node;
   import java.util.Collection;
   import java.util.HashMap;
   import java.util.Map;
   @Component(immediate = true)
   @Service(value = PayloadMapper.class)
   public class SimpleFileBasedPayloadMapper implements PayloadMapper {
   @Override
   public Node createPayload(WorkflowInitializationContext wfInitCtxt, Node stagingFolder, String uniquePayloadName,
   Map<String, Binary> inputs, Collection<WorkflowVariable> variableDefs) throws Exception {
   Node dirNode = stagingFolder.addNode(uniquePayloadName, "sling:Folder");
   for (Map.Entry<String, Binary> bins: inputs.entrySet()) {
   Node fileNode = dirNode.addNode(bins.getKey(), "nt:file");
   Node resNode = fileNode.addNode ("jcr:content", "nt:resource");
   resNode.setProperty("jcr:data", bins.getValue());
   }
   return dirNode;
   }
   @Override
   public Map<String, Document> getInputs(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload, ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public void setOutput(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   String fileName, Binary contents, int outputMode) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getIntermediateOutputs(WorkflowInitializationContext wfInitCtxt,
   WorkflowExecutionContext wfExecCtxt, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getFinalOutputs(WorkflowInitializationContext wfInitCtxt, Workflow workflow, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   Map<String, Object> params = wfInitCtxt.getConfigParameters();
   Map<String, Document> result = new HashMap<String, Document>();
   for (Map.Entry<String, Object> me: params.entrySet()) {
   String key = me.getKey();
   if (key.startsWith("pm.outfile.")) {
   String fName = (String) me.getValue();
   Document d = new Document(payload.getPath() + "/" + fName, resourceResolver);
   result.put(fName, d);
   }
   }
   return result;
   }
   @Override
   public void setVariable(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   WorkflowVariable variable) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Object> getVariables(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   }
   ```

## 用户如何与已监视文件夹交互 {#how-users-interact-with-a-watched-folder}

对于监视文件夹端点，用户可以通过将输入文件或文件夹从其桌面复制或拖动到监视文件夹来开始文件处理操作。 文件按到达顺序处理。

对于“监视文件夹”端点，如果作业只需要一个输入文件，则用户可以将该文件复制到“监视文件夹”的根目录。

如果作业包含多个输入文件，则用户必须在“监视文件夹”层次结构之外创建一个包含所有必需文件的文件夹。 此新文件夹应包括输入文件（如果进程需要，还可选择包含DDX文件）。 作业文件夹构建完成后，用户会将其复制到监视文件夹的输入文件夹中。

>[!NOTE]
>
>确保应用程序服务器已删除对监视文件夹中文件的访问权限。 如果AEM Forms在扫描文件后无法从输入文件夹中删除文件，则关联的进程将无限期地启动。

## 有关已监视文件夹的其他信息 {#additional-information-about-the-watched-folders}

### 关于限制 {#about-throttling}

为监视文件夹端点启用限制后，它将限制在任何给定时间处理的监视文件夹作业的数量。 最大作业数由批量大小值确定，也可在“监视文件夹”端点中进行配置。 达到限制限制时，不会轮询“监视文件夹”输入目录中的传入文档。 在完成其他监视文件夹作业并进行另一次轮询尝试之前，文档也会保留在输入目录中。 对于同步处理，在单次轮询中处理的所有作业都将计入限制，即使这些作业在单个线程中连续处理也是如此。

>[!NOTE]
>
>限制不随群集扩展。 启用限制后，集群作为一个整体将不会在任何给定时间处理超过“批处理大小”中指定的作业数。 此限制是群集范围的，并非群集中每个节点的特定限制。 例如，如果批量大小为2，则在一个节点处理两个作业时可以达到限制限制，而其他节点不会轮询输入目录直到完成其中一个作业为止。

#### 节流的工作原理 {#how-throttling-works}

“监视文件夹”在每个pollInterval中扫描输入文件夹，选取批量大小中指定的文件数，并为每个文件调用目标服务。 例如，如果批处理大小为4，则监视文件夹在每次扫描时都会选取四个文件，创建四个调用请求，并调用目标服务。 在完成这些请求之前，如果调用“已监视文件夹”，则无论前四个作业是否完成，都会再次启动四个作业。

限制会阻止监视文件夹在前一个作业未完成时调用新作业。 已监视文件夹检测正在进行的作业，并根据批处理大小减去正在进行的作业来处理新作业。 例如，在第二次调用中，如果已完成的作业数仅为三个，并且一个作业仍在进行中，则“监视文件夹”仅会再调用三个作业。

* “已监视文件夹”依赖于暂存文件夹中存在的文件数，以确定正在进行的作业数。 如果文件在暂存文件夹中保持未处理，则“已监视文件夹”不会再调用任何作业。 例如，如果批量大小为4，并且3个作业停止，则“监视文件夹”在后续调用中只调用一个作业。 存在多种情况，可能导致暂存文件夹中的文件保持未处理状态。 当作业停止时，管理员可以在“进程管理”(Process Management)管理页上终止该进程，以便“已监视文件夹”(Watched Folder)将文件移出暂存文件夹。
* 如果AEM Forms服务器在“监视文件夹”调用作业之前关闭，则管理员可以将文件移出暂存文件夹。 有关信息，请参阅 [故障点和恢复](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).
* 如果AEM Forms服务器正在运行，但当作业管理器服务回调时“监视文件夹”未运行（服务未按顺序启动时发生），则管理员可以将文件移出暂存文件夹。 有关信息，请参阅 [故障点和恢复](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).

### 故障点和恢复故障点和恢复 {#failure-points-and-recoveryfailure-points-and-recovery}

在每个轮询事件中，“监视文件夹”会锁定输入文件夹，将与包含文件模式匹配的文件移动到暂存文件夹，然后解锁输入文件夹。 需要锁定，以便两个线程不会选取同一组文件并处理它们两次。 如果pollInterval较小且批处理大小较大，则发生这种情况的可能性会增加。 将文件移到暂存文件夹后，将解锁输入文件夹，以便其他线程可以扫描该文件夹。 此步骤有助于提供高吞吐量，因为在一个线程处理文件时，其他线程可以扫描。

将文件移到暂存文件夹后，将为每个文件创建调用请求并调用目标服务。 有时，监视文件夹无法恢复暂存文件夹中的文件：

* 如果服务器在“监视文件夹”可以创建调用请求之前关闭，则暂存文件夹中的文件将保留在暂存文件夹中，且无法恢复。

* 如果“监视文件夹”已成功为stage文件夹中的每个文件创建调用请求，并且服务器崩溃，则基于调用类型有两种行为：

   * **同步**:如果“已监视文件夹”配置为同步调用服务，则暂存文件夹中的所有文件在暂存文件夹中都将保留未处理。
   * **异步**:在这种情况下，“已监视文件夹”依赖于作业管理器服务。 如果作业管理器服务调用回监视文件夹，则根据调用结果将暂存文件夹中的文件移动到保留或失败文件夹中。 如果作业管理器服务未回调“已监视文件夹”，则这些文件将在暂存文件夹中保持未处理状态。 当作业管理器回调时，监视文件夹未运行时，会发生这种情况。

#### 恢复暂存文件夹中未处理的源文件 {#recover-unprocessed-source-files-in-the-stage-folder}

当“监视文件夹”无法处理暂存文件夹中的源文件时，您可以恢复未处理的文件。

1. 重新启动应用程序服务器或节点。

1. 停止监视文件夹处理新的输入文件。 如果跳过此步骤，将很难确定哪些文件在暂存文件夹中未处理。 要阻止监视文件夹处理新的输入文件，请执行以下任务之一：

   * 将“监视文件夹”的includeFilePattern属性更改为与任何新输入文件都不匹配的内容（例如，输入NOMATCH）。
   * 暂停创建新输入文件的进程。

   等待AEM Forms恢复并处理所有文件。 大多数文件都应该恢复，任何新的输入文件都应正确处理。 等待监视文件夹恢复和处理文件的时长取决于要调用的操作长度和要恢复的文件数量。

1. 确定无法处理的文件。 如果您等待了适当的时间并完成了上一步，并且暂存文件夹中仍有未处理的文件，请转到下一步。

   >[!NOTE]
   >
   >您可以查看暂存目录中文件的日期和时间戳。 根据文件数量和正常处理时间，您可以确定哪些文件的旧版本足以被视为卡住。

1. 将未处理的文件从暂存目录复制到输入目录。

1. 如果阻止监视文件夹在步骤2中处理新的输入文件，请将“包含文件模式”更改为其上一个值，或重新启用您禁用的进程。

### 将监视文件夹链在一起 {#chain-watched-folders-together}

监视文件夹可以链接在一起，以便一个监视文件夹的结果文档是下一个监视文件夹的输入文档。 每个已监视文件夹都可以调用其他服务。 通过以此方式配置监视文件夹，可以调用多项服务。 例如，一个监视文件夹可以将PDF文件转换为Adobe PostScript®，另一个监视文件夹可以将PostScript文件转换为PDF/A格式。 为此，只需将您第一个端点定义的监视文件夹的结果文件夹设置为指向由第二个端点定义的监视文件夹的输入文件夹即可。

第一次转换的输出将转到\path\result。 第二次转换的输入是\path\result，第二次转换的输出将转到\path\result\result （或第二次转换的“结果文件夹”框中定义的目录）。

### 文件和文件夹模式 {#file-and-folder-patterns}

管理员可以指定可调用服务的文件类型。 可以为每个监视文件夹建立多个文件模式。 文件模式可以是以下文件属性之一：

* 具有特定文件名扩展名的文件；例如， &#42;.dat， &#42;.xml， .pdf， &#42;.&#42;
* 具有特定名称的文件；例如，数据。&#42;
* 名称和扩展名中具有复合表达式的文件，如以下示例所示：

   * 数据[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
   * &#42;。[dD][Aa]&#39;port&#39;
   * &#42;。[Xx][Mm][Ll]

* 管理员可以定义要在其中存储结果的输出文件夹的文件模式。 对于输出文件夹（结果、保留和失败），管理员可以指定以下任何文件模式：
* %Y =年（满）
* %y =年（最后两位）
* %M =月，
* %D =月中某天，
* %d =每年的某天，
* %h =小时，
* %m =分钟，
* %s =秒，
* %R = 0-9之间的随机数
* %J =作业名称

例如，结果文件夹的路径可能为C:\Adobe\Adobe LiveCycle ES4\BarcodedForms\%y\%m\%d。

输出参数映射还可以指定其他模式，例如：

* %F =源文件名
* %E =源文件扩展名

如果输出参数映射模式以“File.separator”（路径分隔符）结尾，则会创建一个文件夹并将内容复制到该文件夹中。 如果模式不以“File.separator”结尾，则使用该名称创建内容（结果文件或文件夹）。

## 将PDF生成器与监视文件夹结合使用 {#using-pdf-generator-with-a-watched-folder}

您可以配置“监视文件夹”以启动工作流、服务或脚本以处理输入文件。 在以下部分中，我们将配置一个监视文件夹以启动ECMAScript。 ECMAScript将使用PDF生成器将Microsoft Word(.docx)文档转换为PDF文档。

执行以下步骤以使用PDF生成器配置监视文件夹：

1. [创建ECMAScript](../../forms/using/watched-folder-in-aem-forms.md#p-create-an-ecmascript-p)
1. [创建工作流](../../forms/using/watched-folder-in-aem-forms.md#p-create-a-workflow-p)
1. [配置监视文件夹](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p)

### 创建ECMAScript {#create-an-ecmascript}

ECMAScript将使用PDF生成器的createPDF API将Microsoft Word(.docx)文档转换为PDF文档。 执行以下步骤以创建脚本：

1. 在浏览器窗口中打开CRXDE lite。 URL为https://&#39;[服务器]:[端口]&#39;/crx/de.

1. 导航到/etc/workflow/scripts并创建一个名为PDFG的文件夹。

1. 在PDFG文件夹中，创建一个名为pdfg-openOffice-sample.ecma的文件，并将以下代码添加到该文件：

   ```javascript
   var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
   // Custom ContentProcessor implementation which defines the processInputs() method purely in JS
   var impl = { processWorkflowContext: function (wrkfContext) {
   
     //  var logger = Packages.org.slf4j.LoggerFactory.getLogger("cmb-mergeandprint-sample.ecma");
                   var inputMap=wrkfContext.getInputMap();
   
                   var distiller = sling.getService(com.adobe.pdfg.service.api.DistillerService);
                   var generatePDF = sling.getService(com.adobe.pdfg.service.api.GeneratePDFService);
                   var pdfgConfig = sling.getService(com.adobe.pdfg.service.api.PDFGConfigService);
       var result = new Packages.java.util.HashMap();
       var entry = inputMap.entrySet().iterator().next();
       var pdfgOut = generatePDF.createPDF(entry.getValue(), ".docx", "Standard OpenOffice", "Standard", "No Security", null, null);
                   var convertedDoc = pdfgOut.get("ConvertedDoc");
   //   logger.info("SuccessFully saved the document to Ouput Node");
       wrkfContext.setResult(entry.getKey().substring(0, entry.getKey().lastIndexOf('.'))+".pdf",convertedDoc); // Ownership flag set to true for auto temp-file deletion.
   
   } }
   
   wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
   ```

1. 保存并关闭文件。

### 创建工作流 {#create-a-workflow}

1. 在浏览器窗口中打开AEM工作流UI。
   <https://[servername>]:&#39;port&#39;/workflow

1. 在“模型”(Models)视图中，单击 **新建**. 在“新建工作流”对话框中，指定 **标题**，然后单击 **确定**.

   ![create-a-workflow-pdf](assets/create-a-workflow-pdf.png)

1. 选择新创建的工作流并单击 **编辑**. 工作流将在新窗口中打开。

1. 删除默认的工作流步骤。 将流程步骤从Sidekick拖放到工作流。

   ![create-a-workflow-pdf2](assets/create-a-workflow-pdf2.png)

1. 右键单击“流程”步骤并选择 **编辑**. 此时将出现“步骤属性”(Step Properties)窗口。

1. 在“进程”选项卡中，选择ECMAScript。 例如，在中创建的pdfg-openOffice-sample.ecma脚本 [创建ECMAScript](#p-create-an-ecmascript-p). 启用 **处理程序高级** 选项并单击 **确定**.

   ![create-a-workflow3-pdf](assets/create-a-workflow3-pdf.png)

### 配置监视文件夹 {#configure-the-watched-folder}

1. 在浏览器窗口中打开CRXDE lite。 https://&#39;[服务器]:[端口]&#39;/crx/de/

1. 导航到/etc/fd/watchfolder/config/文件夹并创建nt:unstructured类型的节点。

   ![configure-the-watched-folder-pdf](assets/configure-the-watched-folder-pdf.png)

1. 将以下属性添加到节点：

   * folderPath（字符串）：要按定义的时间间隔扫描的文件夹的路径。 文件夹必须位于共享位置，所有服务器都具有对服务器的完全访问权限。
inputProcessorType（字符串）：要启动的进程的类型。 在本教程中，指定工作流。

   * inputProcessorId（字符串）：inputProcessorId属性的行为基于为inputProcessorType属性指定的值。 在本例中，inputProcessorType属性的值是workflow。 因此，对于inputProcessorId属性，请指定PDFG工作流的以下路径：/etc/workflow/models/pdfg/jcr:content/model

   * outputFilePattern(String):输出文件的模式。 您可以指定文件夹或文件模式。 如果指定了文件夹模式，则输出文件的名称将如工作流中所述。 如果指定了文件模式，则输出文件的名称如文件模式中所述。
   除了上述必需属性之外，“已监视文件夹”还支持一些可选属性。 有关可选属性的完整列表和说明，请参阅 [已监视文件夹属性](#watchedfolderproperties).

## 已知问题 {#watched-folder-known-issues}

在JEE上启动AEM 6.5 Forms时，文件会在JBoss完全启动且文件无法处理之前开始处理。 要避免此问题，请在启动JBoss之前清除所有已监视文件夹。
