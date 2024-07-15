---
title: 在摘要URL中获取任务变量
description: 如何重用有关任务的信息并生成摘要URL以摘要或描述任务。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# 在摘要URL中获取任务变量 {#getting-task-variables-in-summary-url}

摘要页面显示与任务相关的信息。 本文介绍了如何在摘要页面中重用与任务相关的信息。

在此示例业务流程中，员工提交休假申请表。 然后，申请表将转至员工的经理进行审批。

1. 为resourseType **Employees/PtoApplication**&#x200B;创建示例HTML渲染器(html.esp)。

   渲染器假定在节点上设置以下属性：

   * ename
   * empid
   * 原因
   * 持续时间

   >[!NOTE]
   >
   >此渲染器是摘要页面模板。

   此渲染器的以下示例代码包含在中：

   `apps/Employees/PtoApplication/html.esp`

   ```html
   <html>
     <body>
       <table>
       <tbody>
       <tr>
           <td>
               <h3>Employee Name: <%= currentNode.ename %></h3>
               <h3>Employee ID: <%= currentNode.eid %></h3>
               <h3>Leave duration: <%= currentNode.duration %> days</h3>
               <h3>Reason: <%= currentNode.reason %></h3>
           </td>
       </tr>
       </tbody>
       </table>
     </body>
   </html>
   ```

1. 修改编排，以从提交的表单数据中提取四个属性。 之后，在CRX中创建一个类型为&#x200B;**Employees/PtoApplication**&#x200B;的节点，并填充属性。

   1. 创建进程&#x200B;**创建PTO摘要**，并将其用作业务流程中&#x200B;**分配任务**&#x200B;操作之前的子进程。
   1. 将&#x200B;**employeeName**、**employeeID**、**ptoReason**、**totalDays**&#x200B;和&#x200B;**nodeName**&#x200B;定义为新进程中的输入变量。 这些变量将作为提交的表单数据传递。

      还定义在设置摘要URL时使用的输出变量&#x200B;**ptoNodePath**。

   1. 在&#x200B;**创建PTO摘要**&#x200B;进程中，使用&#x200B;**设置值**&#x200B;组件在&#x200B;**nodeProperty**(**nodeProps**)映射中设置输入详细信息。

      此映射中的键应与上一步中HTML渲染器中定义的键相同。

      此外，在映射中添加值为&#x200B;**Employees/PtoApplication**&#x200B;的&#x200B;**sling：resourceType**&#x200B;键。

   1. 在&#x200B;**创建PTO摘要**&#x200B;进程中使用&#x200B;**ContentRepositoryConnector**&#x200B;服务中的子进程&#x200B;**storeContent**。 此子进程将创建一个CRX节点。

      它需要三个输入变量：

      * **文件夹路径**：创建新CRX节点的路径。 将路径设置为&#x200B;**/内容**。
      * **节点名称**：将输入变量nodeName分配给此字段。 这是一个唯一的节点名称字符串。
      * **节点类型**：将该类型定义为&#x200B;**nt：unstructured**。 此进程的输出为nodePath。 nodePath是新创建节点的CRX路径。 ndoePath将成为&#x200B;**创建PTO**&#x200B;摘要过程的最终输出。

   1. 将提交的表单数据（**employeeName**、**employeeID**、**ptoReason**&#x200B;和&#x200B;**totalDays**）作为输入传递给新进程&#x200B;**创建PTO摘要**。 将输出作为&#x200B;**ptoSummaryNodePath**。

1. 将摘要URL定义为包含服务器详细信息以及&#x200B;**ptoSummaryNodePath**&#x200B;的XPath表达式。

   XPath： `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`。

在AEM Forms工作区中，打开任务时，摘要URL将访问CRX节点，并且HTML渲染器会显示摘要。

无需修改流程即可更改摘要布局。 HTML呈现器可正确显示摘要。
