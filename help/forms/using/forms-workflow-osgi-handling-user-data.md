---
title: OSGi上以Forms为中心的工作流 |处理用户数据
seo-title: OSGi上以Forms为中心的工作流 |处理用户数据
description: OSGi上以Forms为中心的工作流 |处理用户数据
uuid: 6eefbe84-6496-4bf8-b065-212aa50cd074
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f400560-8152-4d07-a946-e514e9b9cedf
role: Admin
exl-id: fd0e17d7-c3e9-4dec-ad26-ed96a1881f42
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 0%

---

# OSGi上以Forms为中心的工作流 |处理用户数据 {#forms-centric-workflows-on-osgi-handling-user-data}

以Forms为中心的AEM工作流使您能够自动处理以Forms为中心的真实业务流程。 工作流由一系列步骤组成，这些步骤按关联工作流模型中指定的顺序执行。 每个步骤都执行特定操作，如将任务分配给用户或发送电子邮件。 工作流可以与存储库、用户帐户和服务中的资产进行交互。 因此，工作流可以协调涉及任何方面的复杂Experience Manager。

可以通过以下任一方法触发或启动以表单为中心的工作流：

* 从AEM收件箱提交应用程序
* 从AEM [!DNL Forms]应用程序提交应用程序
* 提交自适应表单
* 使用监视文件夹
* 提交交互式通信或信件

有关以Forms为中心的AEM工作流和功能的更多信息，请参阅OSGi](/help/forms/using/aem-forms-workflow.md)上以Forms为中心的工作流。[

## 用户数据和数据存储 {#user-data-and-data-stores}

触发工作流时，将自动为工作流实例生成有效负载。 每个工作流实例都会分配一个唯一的实例ID和关联的有效负载ID。 有效负载包含与工作流实例关联的用户和表单数据的存储库位置。 此外，工作流实例的草稿和历史数据也存储在AEM存储库中。

工作流实例的有效负荷、草稿和历史记录所在的默认存储库位置如下所示：

>[!NOTE]
>
>在创建工作流或应用程序时，您可以配置不同的位置来存储负载、草稿和历史数据。 要识别工作流或应用程序存储数据的位置，请查看工作流。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><b>AEM 6.4 [!DNL Forms]</b></td>
   <td><b>AEM 6.3 [!DNL Forms]</b></td>
  </tr>
  <tr>
   <td><strong>工作流<br />实例</strong></td>
   <td>/var/workflow/instances/[server_id]/&lt;日期&gt;/[workflow-instance]/</td>
   <td>/etc/workflow/instances/[server_id]/[date]/[workflow-instance]/</td>
  </tr>
  <tr>
   <td><strong>有效负荷</strong></td>
   <td>/var/fd/dashboard/payload/[server_id]/[date]/<br /> [payload_id]/</td>
   <td>/etc/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td>
  </tr>
  <tr>
   <td><strong>草稿</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td>
  </tr>
  <tr>
   <td><strong>历史</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
  </tr>
 </tbody>
</table>

## 访问和删除用户数据 {#access-and-delete-user-data}

您可以从存储库中的工作流实例中访问和删除用户数据。 要实现此目的，您必须知道与用户关联的工作流实例的实例ID。 您可以使用启动工作流实例的用户的用户名或工作流实例的当前代理人的用户名来查找工作流实例的实例ID。

但是，在以下情况下，在识别与启动器关联的工作流时，您无法识别或结果可能不明确：

* **通过已监视文件夹触发的工作流**:如果工作流是由已监视的文件夹触发的，则无法使用其启动器来识别工作流实例。在这种情况下，用户信息在存储的数据中进行编码。
* **从发布AEM实例启动的工作流**:从AEM发布实例提交自适应表单、交互式通信或信件时，所有工作流实例都使用服务用户创建。在这些情况下，不会在工作流实例数据中捕获登录用户的用户名。

### 访问用户数据 {#access}

要识别和访问为工作流实例存储的用户数据，请执行以下步骤：

1. 在AEM创作实例上，转到`https://'[server]:[port]'/crx/de`，然后导航到&#x200B;**[!UICONTROL 工具>查询]**。

   从&#x200B;**[!UICONTROL 类型]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL SQL2]**。

1. 根据可用信息，执行以下查询之一：

   * 如果工作流启动器已知，请执行以下操作：

   `SELECT &ast; FROM [cq:Workflow] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[initiator]='*initiator-ID*'`

   * 如果您要查找其数据的用户是当前工作流代理人，请执行以下操作：

   `SELECT &ast; FROM [cq:WorkItem] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[assignee]='*assignee-id*'`

   该查询返回指定工作流启动器或当前工作流代理人的所有工作流实例的位置。

   例如，以下查询从工作流启动器为`srose`的`/var/workflow/instances`节点返回两个工作流实例路径。

   ![工作流实例](assets/workflow-instance.png)

1. 转到查询返回的工作流实例路径。 状态属性显示工作流实例的当前状态。

   ![状态](assets/status.png)

1. 在工作流实例节点中，导航到`data/payload/`。 `path`属性存储工作流实例的有效负载路径。 您可以导航到访问有效负载中存储的数据的路径。

   ![payload-path](assets/payload-path.png)

1. 导航到工作流实例的草稿和历史记录位置。

   例如：

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/draft/`

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/history/`

1. 对步骤2中查询返回的所有工作流实例重复步骤3 - 5。

   >[!NOTE]
   >
   >AEM [!DNL Forms]应用程序还以离线模式存储数据。 工作流实例的数据可能存储在单个设备上的本地，并在应用程序与服务器同步时被提交到[!DNL Forms]服务器。

### 删除用户数据 {#delete-user-data}

您必须是AEM管理员，才能通过执行以下步骤从工作流实例中删除用户数据：

1. 按照[访问用户数据](/help/forms/using/forms-workflow-osgi-handling-user-data.md#access)中的说明操作，并注意以下事项：

   * 与用户关联的工作流实例的路径
   * 工作流实例的状态
   * 工作流实例的负载路径
   * 工作流实例的草稿和历史记录路径

1. 对于&#x200B;**RUNNING**、**SUSPED**&#x200B;或&#x200B;**STALE**&#x200B;状态中的工作流实例执行此步骤：

   1. 转到`https://'[server]:[port]'/aem/start.html` ，然后使用管理员凭据登录。
   1. 导航到&#x200B;**[!UICONTROL 工具>工作流>实例]**。
   1. 为用户选择相关的工作流实例，然后点按&#x200B;**[!UICONTROL 终止]**&#x200B;以终止正在运行的实例。

      有关使用工作流实例的更多信息，请参阅[管理工作流实例](/help/sites-administering/workflows-administering.md)。

1. 转到[!DNL CRXDE Lite]控制台，导航到工作流实例的有效负载路径，然后删除`payload`节点。
1. 导航到工作流实例的草稿路径，并删除`draft`节点。
1. 导航到工作流实例的历史记录路径，并删除`history`节点。
1. 导航到工作流实例的工作流实例路径，并删除该工作流的`[workflow-instance-ID]`节点。

   >[!NOTE]
   >
   >删除工作流实例节点将删除所有工作流参与者的工作流实例。

1. 对于为用户标识的所有工作流实例，重复步骤2 - 6。
1. 识别并删除工作流参与者的AEM [!DNL Forms]应用程序发件箱中的离线草稿和提交数据，以避免向服务器提交任何数据。

您还可以使用API访问和删除节点和属性。 有关更多信息，请参阅以下文档。

* [如何以编程方式访问AEM JCR](/help/sites-developing/access-jcr.md)
* [删除节点和属性](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.9%20Removing%20Nodes%20and%20Properties)
* [API参考](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/overview-summary.html)
