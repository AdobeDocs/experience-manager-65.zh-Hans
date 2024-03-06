---
title: AEM Forms工作区JSON对象说明
description: 有关LiveCycleAEM Forms Workspace中使用的JSON JavaScript对象的概念信息，以进行自定义、扩展、修改和重用。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: f837a2b3-4650-4261-84c6-291bb2a46dc7
source-git-commit: 970e0a97d531d4cbae76119960972e54ef65dda0
workflow-type: tm+mt
source-wordcount: '2144'
ht-degree: 8%

---

# AEM Forms工作区JSON对象说明 {#aem-forms-workspace-json-object-description}

下面介绍了AEM Forms工作区中使用的JSON对象。

1. 类别

   类别显示在工作区的启动进程选项卡中。 这些类别用于对起点进行分类。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>name</td>
   <td>周五</td>
   <td>类别名称</td>
  </tr>
  <tr>
   <td>id</td>
   <td>周五</td>
   <td>类别Id<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>描述<br type="_moz" /> </td>
   <td>周五</td>
   <td>类别描述<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentOid<br type="_moz" /> </td>
   <td>周五</td>
   <td>包含父类别的OID<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>起始点列表<br type="_moz" /> </td>
   <td>周二</td>
   <td>包含某个类别中存在的所有起点的列表</td>
  </tr>
  <tr>
   <td>categorylist</td>
   <td>周二</td>
   <td>包含类别的直接子类别的列表<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>所有“起点”和“收藏”都是在客户端定义的类别。 收藏类别包含用户标记为收藏的所有起点。 “所有起点”类别包含所有起点。

1. 起点

   启动点用于在调用时从工作区启动进程。

   | **属性** | **仅限客户端** | **评论** |
   |---|---|---|
   | categoryId | 周五 | 它包含起点所属类别的ID。 |
   | 说明 | 周五 | 它包含对起点的描述。 |
   | name | 周五 | 它包含起点的名称。 |
   | serializedImageTicket | 周五 | 它包含与起点对应的图像票证。 此图像票证用在起点的imageUrl字段中，用于从服务器获取起点的图像。 |
   | serviceName | 周五 | 它包含起点服务的名称。 |
   | startpointId | 周五 | 它包含起点ID。 |
   | isFavorite | 周二 | 指示起点是否为常用起点。 如果起点为最喜爱则为真，否则为假。 |
   | isDefaultImage | 周二 | 表示是否为进程指定了图像。 如果没有与进程关联的图像，则为true，否则为false。 |
   | 任务 | 周二 | 它包含调用起点时创建的任务。 |
   | imageUrl | 周二 | 它包含对应于起点的图像的URL。 |

1. 任务

   任务被分配给用户/组，并包括可以使用数据填充的用户界面 — 表单或指南（已弃用）。 当用户被分配任务时，将为他们提供完成和提交的表单或指南。

<table>
 <tbody>
  <tr>
   <td>属性<br /> </td>
   <td>仅限客户端<br /> </td>
   <td>评论<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>周五</td>
   <td>当任务为LC8任务时，任务类为“LC8”，否则为“标准”。<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>周五</td>
   <td>它包含任务完成时的时间戳。<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>周五</td>
   <td>它包含可向其咨询任务的组的ID。 它是在设计过程中设置的。<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>周五</td>
   <td>它包含创建任务时的时间戳。<br /> </td>
  </tr>
  <tr>
   <td>creationId<br /> </td>
   <td>周五</td>
   <td>它包含创建任务的用户的ID。<br /> </td>
  </tr>
  <tr>
   <td>当前工作<br /> </td>
   <td>周五</td>
   <td>它包含有关当前任务分配的详细信息。<br /> </td>
  </tr>
  <tr>
   <td>截止日期<br /> </td>
   <td>周五</td>
   <td>它包含任务到达截止日期的时间戳。<br /> </td>
  </tr>
  <tr>
   <td>描述<br /> </td>
   <td>周五</td>
   <td>它包含任务的描述。<br /> </td>
  </tr>
  <tr>
   <td>显示名称<br /> </td>
   <td>周五</td>
   <td>它包含任务的显示名称。<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>周五</td>
   <td>它包含任务可转发到的组的ID。 它是在设计过程中设置的。<br /> </td>
  </tr>
  <tr>
   <td>说明<br /> </td>
   <td>周五</td>
   <td>它包含任务的说明。<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>周五</td>
   <td>如果任务被锁定，则为True。<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>周五</td>
   <td>如果必须打开任务表单才能完成任务，则为True。<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>周五</td>
   <td>如果为true，则在打开任务时，表单首次会进入全屏。<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>周五</td>
   <td>如果为true，则必须选择路由以完成任务。<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>周五</td>
   <td>如果为true，则显示附件。<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>周五</td>
   <td>如果为true，则从起始点创建任务。<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>周五</td>
   <td>如果任务在工作区中可见，则为True。<br /> </td>
  </tr>
  <tr>
   <td>nextReminder<br /> </td>
   <td>周五</td>
   <td>下一个提醒的时间戳。<br /> </td>
  </tr>
  <tr>
   <td>优先级<br /> </td>
   <td>周五</td>
   <td>它包含任务的优先级。<br /> 1 =最高优先级<br /> 2 =高优先级<br /> 3 =普通优先级<br /> 4 =低优先级<br /> 5 =最低优先级<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>周五</td>
   <td>任务所属的进程实例的ID。<br /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br /> </td>
   <td>周五</td>
   <td>任务的进程实例的状态。<br /> </td>
  </tr>
  <tr>
   <td>提醒计数<br /> </td>
   <td>周五</td>
   <td>它包含任务的提醒计数。<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>周五</td>
   <td>它包含与任务关联的路由列表。 用户可以通过从路由列表中选择路由中的任何一条来完成该任务。<br /> </td>
  </tr>
  <tr>
   <td>选定路由<br /> </td>
   <td>周五</td>
   <td>它包含任务完成时选择的路由的名称。<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>周五</td>
   <td>它包含与任务对应的图像票证。 此图像票证用于任务的imageUrl字段中，以从服务器获取任务的图像。<br /> <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>周五</td>
   <td>它包含用于任务的服务的名称。<br /> </td>
  </tr>
  <tr>
   <td>服务标题<br /> </td>
   <td>周五</td>
   <td>它包含用于任务的服务的标题。<br /> </td>
  </tr>
  <tr>
   <td>状态<br /> </td>
   <td>周五</td>
   <td>1 =已创建（从起始点创建任务。）<br /> 2 =创建并保存（从起始点创建并保存任务。）<br /> 3 =已分配（任务在流程启动后分配给用户。）<br /> 4 =已分配和保存（任务已分配和保存。）<br /> 100 =已完成（任务已完成。）<br /> 101 =已截止（任务已达到截止日期。）<br /> 102 =已终止<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>周五</td>
   <td>它包含流程设计期间任务集的名称。<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>周五</td>
   <td>它包含任务摘要url。<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>周五</td>
   <td>它是任务的访问控制列表。<br /> </td>
  </tr>
  <tr>
   <td>taskid<br /> </td>
   <td>周五</td>
   <td>任务的ID。<br /> </td>
  </tr>
  <tr>
   <td>updatetime<br /> </td>
   <td>周五</td>
   <td>上次更新任务的时间戳。<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>周二</td>
   <td>它包含任务的表单URL。<br /> </td>
  </tr>
  <tr>
   <td>任务表单类型<br /> </td>
   <td>周二</td>
   <td>它包含任务表单类型。 使用此字段，任务在客户端上呈现为pdf for、swf表单等。<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>周二</td>
   <td>如果为true，则路由操作在工作区中可见。<br /> </td>
  </tr>
  <tr>
   <td>showACLActions<br /> </td>
   <td>周二</td>
   <td>如果为true，则转发、咨询、共享等操作在工作区中可见。<br /> </td>
  </tr>
  <tr>
   <td>supportsoffline<br /> </td>
   <td>周二</td>
   <td>如果为true，则可以将表单脱机。 这仅适用于PDF表单。<br /> </td>
  </tr>
  <tr>
   <td>supportssave<br /> </td>
   <td>周二</td>
   <td>如果为true，则用户可以保存任务。<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>周二</td>
   <td>此对象包含用于通过Reader提交PDF表单的选项，以防PDF表单不包含提交按钮。<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>周二</td>
   <td>表示是否为进程指定了图像。 如果没有与进程关联的图像，则为true，否则为false。<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>周二</td>
   <td>它包含在任务详细信息的“历史记录”选项卡中使用的任务列表。<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>周二</td>
   <td>如果登录用户是任务的所有者，则为True。<br /> </td>
  </tr>
  <tr>
   <td>可用命令<br /> </td>
   <td>周二</td>
   <td>它包含可对任务执行的所有操作。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>周二</td>
   <td>它包含可用于任务的所有路由操作。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>周二</td>
   <td>它包含forward 、 share和consult等命令（如果可用于任务）。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>周二</td>
   <td>它包含lock、unlock、absout、return、claim等可用命令。<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>周二</td>
   <td>它包含有关任务的进程实例的信息。<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>它包含进程变量的对象数组（如果存在）。<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>周二</td>
   <td>它包含任务的进程实例的待处理任务列表。<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>周二</td>
   <td>它是一个对象数组。 每个对象都包含有关路由及其相应确认消息（如果存在）的详细信息。<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>周二</td>
   <td>它是任务表单数据的URL。<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>周二</td>
   <td>这是第三方应用程序表单的配置。<br /> </td>
  </tr>
  <tr>
   <td>已提交<br /> </td>
   <td>周二</td>
   <td>如果提交任务，则为True。<br /> </td>
  </tr>
  <tr>
   <td>附件<br /> </td>
   <td>周二</td>
   <td>任务的附件列表。<br /> </td>
  </tr>
  <tr>
   <td>指定任务<br /> </td>
   <td>周二</td>
   <td>任务的分配列表。<br /> </td>
  </tr>
 </tbody>
</table>

1. 过滤器

   过滤器基本上是用户或组的队列。 将任务分配给用户/组后，该任务将添加到相应的队列中。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>isDefault <br type="_moz" /> </td>
   <td>周五</td>
   <td>如果队列是登录用户的默认队列，则为true，否则为false。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>name<br type="_moz" /> </td>
   <td>周五</td>
   <td>队列所有者的名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>qid</td>
   <td>周五</td>
   <td>队列的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>类型</td>
   <td>周五</td>
   <td>它包含队列的类型。<br /> 0 — 用户队列。<br /> 1. 共享队列。<br /> 2. 组队列。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>查询</td>
   <td>周二</td>
   <td>这包含与筛选器关联的查询。 此查询用于从完整任务列表中搜索任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>任务</td>
   <td>周二</td>
   <td>它包含属于某个过滤器的所有任务的列表。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 外出

   您可以管理“不在办公室”日程安排，并在您不在时控制分配给您的任务流。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong><br type="_moz" /> </td>
   <td><strong>仅限客户端</strong><br type="_moz" /> </td>
   <td><strong>评论</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>日期范围<br type="_moz" /> </td>
   <td>周五</td>
   <td>它包含用户的外出时间表的数组对象。 在每个计划对象中，startDate字段包含计划的开始日期，而dendDate字段包含计划的结束日期。 如果计划中的endDate为null，则表示用户尚未计划外出计划的结束日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDecision<br type="_moz" /> </td>
   <td>周五</td>
   <td>如果用户不在办公室，则没有主指定，则为True。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>周五</td>
   <td>如果用户不在办公室，则为真。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDegine<br type="_moz" /> </td>
   <td>周五</td>
   <td>它包含由用户分配为主指定用户的详细信息。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDesignates<br type="_moz" /> </td>
   <td>周五</td>
   <td>它包含用于特定于进程的“不在办公室”指定的对象数组。 在每个特定于进程的指定对象中，processName包含进程的名称，如果没有为相应的进程分配用户，则isNotDesigned为true；如果没有为相应的进程分配用户的其他详细信息，则userDesigned为null。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>进程<br type="_moz" /> </td>
   <td>周二</td>
   <td>它包含用户可用的所有进程的列表。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>周二</td>
   <td>它包含最初获取的用户的初始外出设置。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>周二</td>
   <td>它包含已修改的“外出”设置。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>周二</td>
   <td>它包含由登录用户搜索直到日期的用户的列表。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 流程实例

   当通过工作区或工作台调用流程时，将创建一个流程实例。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>描述<br type="_moz" /> </td>
   <td>周五</td>
   <td>流程实例描述<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>发起者</td>
   <td>周五</td>
   <td>进程实例的启动器名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>周五</td>
   <td>进程实例的发起者的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>周五</td>
   <td>流程完成时的时间戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>周五</td>
   <td>进程实例的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>周五</td>
   <td>0 =已启动<br /> 1 =正在运行<br /> 2 =完成<br /> 3 =正在完成<br /> 4 =已终止<br /> 5 =正在终止<br /> 6 =已暂停<br /> 7 =暂停<br /> 8 =取消暂停<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processname<br type="_moz" /> </td>
   <td>周五</td>
   <td>进程的名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>周五</td>
   <td>进程启动时的时间戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>周五</td>
   <td>流程变量的对象数组。 每个进程变量对象包含进程变量名称、进程变量值和进程变量类型。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>任务列表<br type="_moz" /> </td>
   <td>周二</td>
   <td>此进程实例生成的任务。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 进程名称

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>processMajorVersion<br type="_moz" /> </td>
   <td>周五</td>
   <td>进程的主要版本。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>周五</td>
   <td>进程的次要版本。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processname<br type="_moz" /> </td>
   <td>周五</td>
   <td>进程的名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>进程标题<br type="_moz" /> </td>
   <td>周五</td>
   <td>进程的标题。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceList<br type="_moz" /> </td>
   <td>周二</td>
   <td>此进程的进程实例列表。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任务分配对象

   任务分配对象包含有关任务分配的信息。 以下是任务分配的属性。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>assignmentCreateTime<br type="_moz" /> </td>
   <td>周五</td>
   <td>创建此任务分配时的时间戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentType<br type="_moz" /> </td>
   <td>周五</td>
   <td>0 =初始分配<br /> 1 =转发（任务已转发到任务的当前所有者。）<br /> 2 =已返回（任务已由任务的先前所有者返回到任务的当前所有者。）<br /> 3 =已声明（任务已由任务的当前所有者声明。）<br /> 4 =提升（在提升后，任务已分配给任务的当前所有者。）<br /> 5 =管理员已分配（任务已由管理员分配给任务的当前所有者。）<br /> 6 =已咨询（已咨询任务当前所有者。）<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentUpdateTime<br type="_moz" /> </td>
   <td>周五</td>
   <td>更新此任务分配时的时间戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>周五</td>
   <td>任务当前所有者的队列ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwner<br type="_moz" /> </td>
   <td>周五</td>
   <td>任务的当前所有者的名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>周五</td>
   <td>任务的当前所有者的ID。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任务ACL对象

   任务ACL对象包含有关任务的转发、共享、咨询等权限的信息。 以下是任务ACL的属性。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>canAddAttachments<br type="_moz" /> </td>
   <td>周五</td>
   <td>如果为true，则可以将附件添加到任务中。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>周五</td>
   <td>如果为true，则可以将注释添加到任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>周五</td>
   <td>如果为true，则可以声明任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>周五</td>
   <td>如果为true，则可查阅任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>周五</td>
   <td>如果为true，则可以转发任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>周五</td>
   <td>如果为true，则任务可以共享。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任务附件

   可以将附件添加到任务中。 附件可以是“附件”和“注释”类型。 以下是附件对象的属性。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>creationDate<br type="_moz" /> </td>
   <td>周五</td>
   <td>创建附件时的时间戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorId<br type="_moz" /> </td>
   <td>周五</td>
   <td>添加附件的用户的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorName<br type="_moz" /> </td>
   <td>周五</td>
   <td>添加附件的用户的名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>描述<br type="_moz" /> </td>
   <td>周五</td>
   <td>附件的描述。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>文件名<br type="_moz" /> </td>
   <td>周五</td>
   <td>附件的名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>id<br type="_moz" /> </td>
   <td>周五</td>
   <td>附件的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastModifiedDate<br type="_moz" /> </td>
   <td>周五</td>
   <td>上次修改附件时的时间戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>注释已扩展<br type="_moz" /> </td>
   <td>周五</td>
   <td>如果为true，则注释为扩展（长）注释。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>权限<br type="_moz" /> </td>
   <td>周五</td>
   <td>与附件关联的权限。 allowRead字段用于读取权限，allowWrite用于写入权限，allowDelete用于删除权限。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>大小<br type="_moz" /> </td>
   <td>周五</td>
   <td>附件大小（以字节为单位）。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskid<br type="_moz" /> </td>
   <td>周五</td>
   <td>向其中添加附件的任务的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>type<br type="_moz" /> </td>
   <td>周五</td>
   <td>“类型”是文件的附件，“类型”是注释的注释。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>周二</td>
   <td>根据用户的UI设置，该日期包含附件创建日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>周二</td>
   <td>格式化的附件说明。 用于显示AEM Forms工作区附件描述中出现的特殊字符。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>格式化的文件名<br type="_moz" /> </td>
   <td>周二</td>
   <td>格式化的附件名称。 用于显示AEM Forms工作区附件名称中存在的特殊字符。 这仅适用于注释。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 用户

   以下是用户对象的属性。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>地址<br type="_moz" /> </td>
   <td>周五</td>
   <td>用户的地址。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>周五</td>
   <td>用户的常用名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>描述<br type="_moz" /> </td>
   <td>周五</td>
   <td>用户的描述。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMembership<br type="_moz" /> </td>
   <td>周五</td>
   <td>用户组的列表。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>显示名称<br type="_moz" /> </td>
   <td>周五</td>
   <td>用户的显示名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>电子邮件<br type="_moz" /> </td>
   <td>周五</td>
   <td>用户的电子邮件ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>周五</td>
   <td>如果用户不在办公室，则为真。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>姓氏<br type="_moz" /> </td>
   <td>周五</td>
   <td>用户的姓氏。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>名字<br type="_moz" /> </td>
   <td>周五</td>
   <td>用户的名字。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>oid<br type="_moz" /> </td>
   <td>周五</td>
   <td>用户的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>org<br type="_moz" /> </td>
   <td>周五</td>
   <td>用户的组织名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>邮政地址<br type="_moz" /> </td>
   <td>周五</td>
   <td>用户的邮政地址。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>电话<br type="_moz" /> </td>
   <td>周五</td>
   <td>用户的联系电话。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephonenumber<br type="_moz" /> </td>
   <td>周五</td>
   <td>用户的联系电话。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userid<br type="_moz" /> </td>
   <td>周五</td>
   <td>用户的登录ID。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
