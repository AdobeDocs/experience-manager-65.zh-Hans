---
title: 在任务摘要窗格中显示信息
description: 在AEM Forms工作区中，可以将“任务摘要”窗格配置为摘要任务或显示任何其他网页。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 在任务摘要窗格中显示信息 {#displaying-information-in-the-task-summary-pane}

在AEM Forms工作区中打开任务时，“任务摘要”窗格会显示任务的摘要。 这项与任务相关的附加信息为AEM Forms工作区的最终用户增添了更多价值。

AEM Forms工作区允许您在“任务摘要”窗格中显示自己选择的网页。 可以使用Workbench创建进程以显示“任务摘要”窗格。

1. 在Workbench中创建分配任务流程。 有关分配任务操作的更多详细信息，请参阅[Workbench帮助](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/)中的服务参考主题。

   >[!NOTE]
   >
   >如果存在TaskSummary URL，则默认情况下会打开Task Summary视图，而不是Form视图。 在这种情况下，即使用户在分配任务中启用了“以最大化模式打开表单”选项，该表单也不会以最大化模式打开。

1. 配置任务摘要URL字段。 您可以指定文本值、模板、变量或XPath表达式。
1. 下面是在“任务摘要”页面上显示信息的示例。

   * 登录到`https://'[server]:[port]'/lc/crx/de`上的CRXDE Lite环境。
   * `Create a node`**SampleSummary** ` under `/content` with type `nt：unstructured`. In the properties of this node, add `sling：resourceType` of type String and value `SampleSummary`. In the Access Control List of this node, add an entry for `PERM_WORKSPACE_USER` allowing `jcr：read` privileges.`
   * `/apps`下的&#x200B;`Create a folder`**SampleSummary**。 在`/apps/SampleSummary`的访问控制列表中，添加允许`jcr:readprivileges`的`PERM_WORKSPACE_USER`条目。
   * `Create a file `html.esp` at `/apps/SampleSummary`. For example, add the following lines in `html.esp`.`

   ```html
   <html>
       <body>
           <h1>Sample Summary</h1>
           <br/>
           <p>Hello Sir!
               <br/>
               This is sample summary page for this task.
           </p>
       </body>
   </html>
   ```

   * 在分配任务步骤中将任务摘要URL的值设置为`/lc/content/SampleSummary.html`。
   * 在AEM Forms工作区中打开与此分配任务步骤关联的任务时，`/apps/SampleSummary`处的`html.esp`在任务摘要窗格中呈现。
