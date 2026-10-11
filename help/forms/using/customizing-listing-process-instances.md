---
title: 自定义流程实例列表
description: 如何在AEM Forms工作区中自定义流程实例中显示的属性。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b27ffe92-8491-43a0-bf42-613eb39a606e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 8%
---
# 自定义流程实例列表 {#customizing-the-listing-of-process-instances}

流程实例列表显示在AEM Forms工作区的“跟踪”选项卡中。

在流程实例列表中，对于每个流程实例，AEM Forms工作区显示该实例的一些属性。 以下属性适用于每个流程实例。 这些属性作为属性存储在流程实例组件模型中，并可用于其视图和模板。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>说明</td>
   <td>流程实例的描述。</td>
  </tr>
  <tr>
   <td>发起者</td>
   <td>进程实例的启动器名称。</td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>进程实例的发起者的ID。</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>进程完成时的时间戳。</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>进程实例的ID。</td>
  </tr>
  <tr>
   <td>processInstanceStatus</td>
   <td>0 =已启动<br /> 1 =正在运行<br /> 2 =完成<br /> 3 =正在完成<br /> 4 =已终止<br /> 5 =正在终止<br /> 6 =已暂停<br /> 7 =正在暂停<br /> 8 =正在取消暂停</td>
  </tr>
  <tr>
   <td>processname</td>
   <td>进程的名称。</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>进程启动时的时间戳。</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>流程变量的对象数组。 每个进程变量对象都包含<strong>name</strong> （进程变量的名称）、<strong>value</strong> （进程变量的值）和<strong>类型</strong> （进程变量的类型）。</td>
  </tr>
 </tbody>
</table>

**示例：**

要在进程实例信息卡中显示进程实例的`description`属性，请执行以下步骤。

1. 按照[通用步骤自定义AEM Forms工作区](/help/forms/using/generic-steps-html-workspace-customization.md)。
1. 执行以下操作：

   1. 如果/libs/ws/js/runtime/templates/processinstance.html不存在，请将其复制到/apps/ws/js/runtime/templates/ 。 单击&#x200B;**全部保存**。
   1. 添加进程描述div，类= &#39;processDescription&#39; inprocessinstance.html。

   ```jsp
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. 执行以下操作：

   1. 打开/apps/ws/js/registry.js进行编辑。
   1. 搜索并将`text!/lc/libs/ws/js/runtime/templates/processinstance.html`替换为&#x200B;`text!/lc/`**应用**/ws/js/runtime/templates/processinstance.html。

1. 通过如下方式在样式表/apps/ws/css/newStyle.css中添加条目，上述更改可能需要更新CSS文件：

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement and user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
