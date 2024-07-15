---
title: 在Web应用程序中集成AEM Forms工作区组件
description: 如何在您自己的Web应用程序中重用AEM Forms工作区组件以使用功能并提供紧密集成。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: bb4a500d-c34f-4586-83f0-ad7ef69b4fb1
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 在Web应用程序中集成AEM Forms工作区组件 {#integrating-aem-forms-workspace-components-in-web-applications}

您可以在自己的Web应用程序中使用AEM Forms工作区[组件](/help/forms/using/description-reusable-components.md)。 以下实施示例使用安装在CRX™实例上的AEM Forms工作区开发包中的组件来创建Web应用程序。 自定义以下解决方案以满足您的特定需求。 示例实现在Web门户中重用`UserInfo`、`FilterList`和`TaskList`组件。

1. 在`https://'[server]:[port]'/lc/crx/de/`处登录CRXDE Lite环境。 确保您已安装AEM Forms Workspace开发包。
1. 创建路径`/apps/sampleApplication/wscomponents`。
1. 复制css、图像、js/libs、js/runtime和js/registry.js

   * 从 `/libs/ws`
   * 到`/apps/sampleApplication/wscomponents`。

1. 在/apps/sampleApplication/wscomponents/js文件夹内创建demomain.js文件。 将代码从/libs/ws/js/main.js复制到demomain.js中。
1. 在demomain.js中，删除用于初始化路由器的代码，然后添加以下代码：

   ```javascript
   require(['initializer','runtime/util/usersession'],
       function(initializer, UserSession) {
           UserSession.initialize(
               function() {
                   // Render all the global components
                   initializer.initGlobal();
               });
       });
   ```

1. 在/content下创建名称为`sampleApplication`的节点并键入`nt:unstructured`。 在此节点的属性中，添加类型为“字符串”且值为`sampleApplication`的`sling:resourceType`。 在此节点的访问控制列表中，添加一个允许jcr：read权限的`PERM_WORKSPACE_USER`条目。 此外，在`/apps/sampleApplication`的访问控制列表中，为`PERM_WORKSPACE_USER`添加一个允许jcr：read权限的项目。
1. 在`/apps/sampleApplication/wscomponents/js/registry.js`中，将模板值的路径从`/lc/libs/ws/`更新为`/lc/apps/sampleApplication/wscomponents/`。
1. 在位于`/apps/sampleApplication/GET.jsp`的门户主页JSP文件中，添加以下代码以在门户中包含所需的组件。

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   还包括AEM Forms工作区组件所需的CSS文件。

   >[!NOTE]
   >
   >在渲染时，每个组件都会添加到组件标记（具有类组件）。 确保主页包含这些标记。 请参阅AEM Forms工作区的`html.jsp`文件，以了解有关这些基本控件标记的更多信息。

1. 要自定义组件，您可以按如下方式扩展所需组件的现有视图：

   ```javascript
   define([
       'jquery',
       'underscore',
       'backbone',
       'runtime/views/userinfo'],
       function($, _, Backbone, UserInfo){
           var demoUserInfo = UserInfo.extend({
               //override the functions to customize the functionality
               render: function() {
                   UserInfo.prototype.render.call(this); // call the render function of the super class
                   …
                   //other tasks
                   …
               }
           });
           return demoUserInfo;
   });
   ```

1. 修改门户CSS以在您的门户上配置所需组件的布局、位置和样式。 例如，您希望将此门户的背景颜色保持为黑色以便更好地查看userInfo组件。 您可以通过更改`/apps/sampleApplication/wscomponents/css/style.css`中的背景颜色来完成此操作，如下所示：

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
