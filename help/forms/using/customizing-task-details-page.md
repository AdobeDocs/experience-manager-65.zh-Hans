---
title: 自定义任务详细信息页面
description: 如何在AEM Forms工作区中自定义“任务详细信息”页面，以修改显示的关于任务的默认信息。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 48c24442-22d2-4d1a-9462-0aba78340281
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 自定义任务详细信息页面 {#customizing-the-task-details-page}

任务详细信息页面包含有关任务及其流程的信息。 但是，您可以自定义“任务详细信息”页面来添加或删除信息。

可以将以下信息添加到任务详细信息页面：

* 任务的JSON对象中的可用信息([AEM Forms工作区JSON对象描述](/help/forms/using/html-workspace-json-object-description.md)中的任务部分)
* 进程实例的JSON对象中的可用信息([AEM Forms工作区JSON对象说明](/help/forms/using/html-workspace-json-object-description.md)中的进程实例部分)

要自定义任务详细信息页面，请执行以下操作：

1. 执行[AEM Forms工作区自定义的一般步骤。](/help/forms/using/generic-steps-html-workspace-customization.md)
1. 要显示任何其他信息，请将相应的键值对添加到`translation.json`文件中`todo`block > `details`block > `app`block > [`required`block]。

   [`required`块]引用了可用的块，例如任务信息的任务块、进程信息的进程块和挂起任务信息的当前挂起任务块。

   例如，要在任务详细信息页面中添加有关“需要路由选择”的信息，您可以在任务块中添加以下键值对：

   ```json
   "todo" : {
       .
       .
       .
       "details" : {
           .
           .
           "task" : {
               .
               .
               "RouteSelectionRequired" : "Route Selection Required"
           }
       }
   }
   ```

   >[!NOTE]
   >
   >为所有支持的语言添加相应的键值对。

1. 将`/libs/ws/js/runtime/templates/taskdetails.html`复制到`/apps/ws/js/runtime/templates/taskdetails.html`。

   将新信息添加到`/apps/ws/js/runtime/templates/taskdetails.html`。 例如：

   ```css
   <div class="detailsContainer">
       .
       .
       <ul>
           .
           .
           <li>
               <label for="routeSelectionRequired" title="<%= $.t('todo.details.task.RouteSelectionRequired')%>"><%= $.t('todo.details.task.RouteSelectionRequired')%></label>
               <div>
                   <span id="routeSelectionRequired"><%= isRouteSelectionRequired != null ? isRouteSelectionRequired : ''%></span>
               </div>
           </li>
           .
           .
       </ul>
   </div>
   ```

1. 打开/apps/ws/js/registry.js进行编辑。

   搜索并将`text!/lc/libs/ws/js/runtime/templates/taskdetails.html`替换为`text!/lc/apps/ws/js/runtime/templates/taskdetails.html`。

>[!NOTE]
>
>若要使用在AEM Forms工作区的&#x200B;**启动进程**&#x200B;选项卡中创建的任务自定义任务详细信息页面，请将新信息添加到`/apps/ws/js/runtime/templates/startprocess.html`。
>
>要为详细信息页面中添加的信息添加新样式，请使用[Workspace自定义](changing-locale-user-interface.md)中的&#x200B;*用户界面更改*&#x200B;部分修改CSS文件。
