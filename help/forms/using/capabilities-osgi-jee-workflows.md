---
title: 以表单为中心的AEM工作流在OSGi和AEM FormsJEE工作流上的操作和功能
description: 以表单为中心的AEM工作流在OSGi和AEM FormsJEE工作流上的操作和功能
contentOwner: khsingh
translation-type: tm+mt
source-git-commit: dfa5a0dbfdd2c63ea0ec66d805e8b452baa3d0ac
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 22%

---


# OSGi和AEM FormsJEE工作流上以表单为中心的AEM工作流的操作和功能{#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## AEM收件箱和HTML工作区{#aem-inbox-and-html-workspace}

您可以使用AEM收件箱在OSGi上运行和监视以Forms为中心的AEM工作流。 而HTML Workspace允许您运行和监视AEM FormsJEE工作流。 下表帮助您了解AEM收件箱中针对OSGi上以Forms为中心的AEM工作流的各种重要操作，以及AEM FormsJEE工作流的HTML Workspace中的这些重要操作。

<table>
 <tbody>
  <tr>
   <td>操作</td>
   <td>AEM 收件箱</td>
   <td>HTML工作区</td>
  </tr>
  <tr>
   <td>启动进程、任务或表单应用程序<br /> </td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>提交任务</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>将任务分配给组</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>提交到多条路由</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>跟踪任务历史记录和任务摘要</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>电子邮件通知</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>重新分配任务</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>自适应表单的字段级附件</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>日历视图</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>任务级别注释</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>队列(共享的个人队列，来自队列的声明任务)</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>办公室外通知</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
    <tr>
   <td>自定义UI元素</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>将任务分配给多个用户</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
 </tbody>
</table>

## OSGi和AEM FormsJEE工作流上以表单为中心的AEM工作流{#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

OSGi和AEM FormsJEE工作流(JEE流程管理方面的AEM Forms)上以表单为中心的AEM工作流具有不同的功能集。 下表帮助您了解在OSGi上以表单为中心的AEM工作流和在JEE工作流上以AEM Forms为中心的OSGi中提供的重要功能：

<table>
 <tbody>
  <tr>
   <td>功能</td>
   <td>OSGi<br />上以表单为中心的AEM工作流 </td>
   <td>AEM Forms·吉工作流</td>
  </tr>
  <tr>
   <td>自适应表单</td>
   <td>支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>与其他AEM解决方案集成</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>潦草签名</td>
   <td>支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>自定义电子邮件模板</td>
   <td>支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>定义任务优先级</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>到期日后超时任务</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>工作流中的循环</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>动态选择被分派人 </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>使用自定义元数据</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>电子签名(Adobe Sign)</td>
   <td>支持<sup>[1]</sup></td>
   <td>支持<sup>[5]</sup></td>
  </tr>
  <tr>
   <td>管理任务和表单应用程序</td>
   <td>支持<sup>[2]</sup><br /> </td>
   <td>支持<sup>[2]</sup></td>
  </tr>
  <tr>
   <td>文档服务</td>
   <td>支持<sup>[3]</sup></td>
   <td>支持<sup>[3]</sup></td>
  </tr>
  <tr>
   <td>将完成的任务渲染为自适应表单或PDF文档</td>
   <td>支持</td>
   <td>支持 [4]</td>
  </tr>
  <tr>
   <td>与通信管理集成</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
   <tr>
   <td>网关，无等待 </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
   <tr>
   <td>用于存储数据的变量 </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>或，然后拆分</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>用户头像</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>在工作流结束时发送电子邮件</td>
   <td>支持<sup>[7]</sup></td>
   <td>支持</td>
  </tr>
  <tr>
   <td>从工作流调用Web服务</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>数字签名</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>重置按钮</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>工作流阶段</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>只读自适应表单</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>隐藏默认保存按钮</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>对工作流详细信息部分的精细控制</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>轮询／计划服务</td>
   <td>现成可用</td>
   <td>需要自定义实施</td>
  </tr>
  <tr>
   <td>自适应Forms应用程序</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>汇编程序服务</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>PDF Generator Service</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>表单服务</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>输出服务</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>文档保障</td>
   <td>支持</td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>执行脚本</td>
   <td>支持ECMAScript</td>
   <td>支持Java代码片段</td>
  </tr>
  <tr>
   <td>汇编程序</td>
   <td>支持</td>
   <td>支持</td>
  </tr>  
  <tr>
   <td>HTML5Forms，交互式PDF forms，表单集</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>进程报告</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>数字签名</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>起点类别</td>
   <td>不支持 </td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>批量任务批准 </td>
   <td>不支持 </td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>用自定义名称保存草稿</td>
   <td>不支持 </td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>使用现有进程数据<br />启动进程 </td>
   <td>不支持</td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>将起点另存为草稿</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>经理视图</td>
   <td>不支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>搜索模板</td>
   <td>不支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>与第三方应用程序集成</td>
   <td>不支持<sup>[6]</sup></td>
   <td>支持</td>
  </tr>
  <tr>
   <td>工作流应用程序或起点的任务级附件</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>提醒电子邮件</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>更改任务超时时的标题</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>关于任务委派和任务索赔的电子邮件</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>不相交组之间的委派</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>XSLT转换</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>动态任务优先级</td>
   <td>不支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>动态标题</td>
   <td>不支持</td>
   <td>不支持</td>
  </tr>
    <tr>
   <td>动态描述</td>
   <td>不支持</td>
   <td>不支持</td>
  </tr>
 </tbody>
</table>

1. 您可以在OSGi上使用以表单为中心的AEM工作流来签署已填写的自适应表单。 OSGi上以表单为中心的AEM工作流支持表单外签名。 不支持[形式签名](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience)体验。

1. 您需要访问AEM收件箱才能在AEM FormsOSGi上运行和监视以表单为中心的工作流，以及运行和监视AEM FormsJEE工作流的HTML Workspace。
1. 本地AEM Forms文档服务适用于OSGi上以表单为中心的AEM工作流和JEE工作流上的AEM Forms。 AEM Workflow在OSGi和AEM FormsJEE（流程管理）工作流上对以表单为中心的AEM工作流使用本机文档服务。
1. AEM FormsJEE工作流只能呈现自适应表单。 它不支持将自适应表单渲染为PDF文档。
1. AEM forms JEE工作流没有单独步骤用于Adobe Sign。 您需要为AEM forms JEE工作流启用Adobe Sign自适应表单。 有关详细信息，请参阅[Adobe Sign文档](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)。
1. 可以使用[调用表单数据模型服务](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p)步骤调用Web服务并从第三方应用程序发布或检索数据。
1. 您可以使用[发送电子邮件](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step)步骤发送电子邮件。

## AEM Inbox和AEM Forms应用程序功能之间的区别{#differences-between-aem-inbox-and-aem-forms-app-features}

启动以Forms为中心的工作流的两种主要方法是使用[AEM收件箱](../../forms/using/manage-applications-inbox.md)和AEM Forms应用程序。 但是，AEM Inbox和AEM Forms应用程序的功能不同。 AEM Inbox只能用于[以Forms为中心的工作流](../../forms/using/aem-forms-workflow.md)，而AEM Forms应用程序可用于以Forms为中心的工作流和流程管理。

下表列表了AEM Inbox和AEM Forms应用程序的功能：

<table>
 <tbody>
  <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>AEM 收件箱</strong></p> </td>
   <td><p><strong>AEM Forms 应用程序</strong></p> </td>
  </tr>
  <tr>
   <td><p>启动表单应用程序</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>提交任务</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>委派任务</p> </td>
   <td><p>支持</p> </td>
   <td><p>不支持</p> </td>
  </tr>
  <tr>
   <td><p>跟踪任务历史记录和任务摘要</p> </td>
   <td><p>支持</p> </td>
   <td><p>不支持</p> </td>
  </tr>
  <tr>
   <td><p>添加任务层附件</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>查看任务层附件</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>添加字段级附件</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>显示日历视图</p> </td>
   <td><p>支持</p> </td>
   <td><p>不支持</p> </td>
  </tr>
  <tr>
   <td><p>添加注释</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
 </tbody>
</table>

