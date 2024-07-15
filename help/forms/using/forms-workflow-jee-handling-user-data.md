---
title: Forms JEE工作流 | 处理用户数据
description: 了解如何使用AEM Forms JEE工作流设计、创建和管理业务流程。
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
exl-id: 847fa303-8d1e-4a17-b90d-5f9da5ca2d77
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---

# Forms JEE工作流 | 处理用户数据 {#forms-jee-workflows-handling-user-data}

AEM Forms JEE工作流提供了用于设计、创建和管理业务流程的工具。 工作流进程包含一系列按指定顺序执行的步骤。 每个步骤都会执行特定操作，例如向用户分配任务或发送电子邮件。 进程可与资产、用户帐户和服务进行交互，并且可以使用以下任意方法触发：

* 从AEM Forms Workspace启动流程
* 使用SOAP或RESTful服务
* 提交自适应表单
* 使用观察文件夹
* 使用电子邮件

有关创建AEM Forms JEE工作流进程的更多信息，请参阅[Workbench帮助](https://www.adobe.com/go/learn_aemforms_workbench_65)。

## 用户数据和数据存储 {#user-data-and-data-stores}

当流程被触发并进展时，它会捕获有关流程参与者的数据、参与者在表单中输入的与流程相关联的数据，以及添加到表单中的附件。 该数据存储在AEM Forms JEE服务器数据库中，如果进行了配置，一些数据（如附件）将存储在Global Document Storage (GDS)目录中。 GDS目录可以在共享文件系统或数据库上配置。

## 访问和删除用户数据 {#access-and-delete-user-data}

触发流程时，将生成唯一的流程实例ID和长生命周期调用ID，并将其与流程实例关联。 您可以根据长时间的调用ID访问和删除流程实例的数据。 您可以使用已提交任务的进程发起者或进程参与者的用户名来推算进程实例的长时间调用ID。

但是，在以下情形中，您无法识别启动器的进程实例ID：

* **通过观察文件夹触发的进程**：如果进程是由观察文件夹触发的，则无法使用进程实例的启动器识别该进程。 在此情况下，在存储的数据中对用户信息进行编码。
* **从发布AEM实例启动的进程**：从AEM发布实例触发的所有进程实例不捕获有关发起程序的信息。 但是，用户数据可捕获在与进程关联的表单中，该表单存储在工作流变量中。
* **通过电子邮件启动的进程**：发件人的电子邮件ID被捕获为`tb_job_instance`数据库表的不透明blob列中的属性，无法直接查询该属性。

### 在工作流发起者或参与者已知时标识流程实例ID {#initiator-participant}

执行以下步骤，以便您能够为工作流发起者或参与者标识流程实例ID：

1. 在AEM Forms Server数据库中执行以下命令，从`edcprincipalentity`数据库表中检索工作流发起人或参与者的主体ID。

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   查询返回指定`user_ID`的主体ID。

1. （**对于工作流启动器**）执行以下命令以从`tb_task`数据库表中检索与启动器的主体ID关联的所有任务。

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   查询返回由指定的`initiator`_ `principal_id`启动的任务。 任务分为两种类型：

   * **已完成的任务**：这些任务已提交，并在`process_instance_id`字段中显示字母数字值。 记下已提交任务的所有流程实例ID，并继续这些步骤。
   * **任务已启动但未完成**：这些任务已启动但尚未提交。 这些任务的`process_instance_id`字段中的值为&#x200B;**0** （零）。 在这种情况下，请记下相应的任务ID并查看[处理孤立任务](#orphan)。

1. （**对于工作流参与者**）执行以下命令以从`tb_assignment`数据库表中检索与发起者的进程参与者主体ID关联的进程实例ID。

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   查询将返回与参与者关联的所有进程（包括参与者未提交任何任务的进程）的实例ID。

   记下已提交任务的所有流程实例ID，并继续这些步骤。

   对于`process_instance_id`为0 （零）的孤立任务或任务，请记下相应的任务ID并查看[处理孤立任务](#orphan)。

1. 按照[根据流程实例ID从工作流实例中清除用户数据](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge)部分中的说明进行操作，以便您可以删除已识别流程实例ID的用户数据。

### 在用户数据存储在原始变量中时识别流程实例ID {#primitive}

可以设计一个工作流，以便在变量中捕获用户数据，并将该变量存储为数据库中的blob。 在这种情况下，仅当用户数据存储在以下基元类型变量之一中时，才能查询用户数据：

* **字符串**：包含用户ID或作为子字符串，可以使用SQL进行查询。
* **数值**：直接包含用户ID。
* **XML**：将用户ID作为子字符串包含在作为文本列存储在数据库中的文本中，并且可以像字符串一样进行查询。

执行以下步骤，以便确定在原始类型变量中存储数据的工作流是否包含用户的数据：

1. 执行以下数据库命令：

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   查询返回指定应用程序(`app_name`)和工作流(`workflow_name`)的`tb_<number>`格式的表名。

   >[!NOTE]
   >
   >如果工作流嵌套在应用程序内的子文件夹中，`name`属性的值可能会很复杂。 请确保您指定了工作流的确切完整路径，该路径可从`omd_object_type`数据库表中获取。

1. 查看`tb_<number>`表架构。 该表包含存储指定工作流的用户数据的变量。 表中的变量对应于工作流中的变量。

   识别并记下与包含用户ID的工作流变量对应的变量。 如果所标识的变量为基元类型，则可以运行查询以确定与用户ID关联的工作流实例。

1. 执行以下数据库命令。 在此命令中，`user_var`是包含用户ID的原始类型变量。

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   查询返回与指定`user_ID`关联的所有进程实例ID。

1. 按照[根据流程实例ID从工作流实例中清除用户数据](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge)部分中的说明进行操作，以便您可以删除已识别流程实例ID的用户数据。

### 根据流程实例ID从工作流实例中清除用户数据 {#purge}

现在，您已标识与用户关联的流程实例ID，请执行以下操作以从相应的流程实例中删除用户数据。

1. 运行以下命令，以便您可以从`tb_process_instance`表中检索进程实例的长生命周期调用ID和状态。

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   查询返回指定`process_instance_id`的长期调用ID和状态。

1. 使用具有正确连接设置的`ServiceClientFactory`实例创建公共`ProcessManager`客户端(`com.adobe.idp.workflow.client.ProcessManager`)的实例。

   有关详细信息，请参阅[类ProcessManager](https://helpx.adobe.com/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html)的Java™ API引用。

1. 检查工作流实例的状态。 如果状态不是2 (COMPLETE)或4 (TERMINATED)，请首先通过调用以下方法终止实例：

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`。

1. 通过调用以下方法清除工作流实例：

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   `purgeProcessInstance`方法会从AEM Forms Server数据库和GDS（如果已配置）中完全删除指定调用ID的所有数据。

### 处理孤立任务 {#orphan}

孤立任务是指包含进程已启动但尚未提交的任务。 在这种情况下，`process_instance_id`为&#x200B;**0** （零）。 因此，无法使用进程实例ID跟踪为孤立任务存储的用户数据。 但是，您可以使用孤立任务的任务ID跟踪它。 您可以按照[中所述从`tb_task`表中为用户标识任务ID。如果工作流发起者或参与者已知，请标识进程实例ID](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant)。

获得任务ID后，请执行以下操作以从GDS和数据库中清除具有孤立任务的关联文件和数据。

1. 在AEM Forms Server数据库上运行以下命令，以便您可以检索已标识任务ID的ID。

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   该查询返回ID列表。 对于结果中返回的每个ID (`fd_id`)，创建会话ID字符串的列表，如下所示：

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. 根据GDS指向文件系统还是数据库，执行以下步骤之一：

   1. 文件系统&#x200B;**中的** GDS

      在GDS文件系统中：

      1. 搜索具有以下会话ID字符串作为扩展名的文件：

      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`

      具有这些扩展名的文件是标记文件。 它们与文件名一起以下列格式存储：

      `<file_name_guid>.session<session_id_string>`

      1. 从文件系统中删除所有标记文件以及文件名完全为`<file_name_guid>`的其他文件。

   1. 数据库&#x200B;**中的** GDS

      为每个会话ID执行以下命令：

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```

1. 运行以下命令，以便您可以从AEM Forms Server数据库中删除任务ID的数据：

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```
