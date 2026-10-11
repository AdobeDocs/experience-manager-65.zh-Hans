---
title: OSGi 上的 AEM Forms 群组和权限
description: 将用户分配给组以在OSGi上管理Adobe Experience Manager (AEM) Forms
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: d802ac53-e3db-45ca-afcb-7e99d0bb7877
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
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
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 11%
---
# OSGi 上的 AEM Forms 群组和权限{#aem-forms-on-osgi-groups-and-privileges}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/forms-groups-privileges-tasks.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

您可以[创建组](/help/sites-administering/user-group-ac-admin.md#group-administration)并将策略和[用户](/help/sites-administering/user-group-ac-admin.md#user-administration)分配给Adobe Experience Manager (AEM)中的组。 这些策略控制属于组的用户的权限。

安装[AEM Forms附加组件包](../../forms/using/installing-configuring-aem-forms-osgi.md)后，本文中提到的组（如forms-users和forms-power-user）将自动可供分配。 下表列出了用户可基于组分配在OSGi上为AEM Forms执行的任务：

<table>
 <tbody>
  <tr>
   <td>组</td> 
   <td>任务</td> 
  </tr>
  <tr>
   <td>表单用户<sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>创建、预览、发布和提交自适应表单</li> 
     <li>创建、预览和发布交互式通信和文档片段</li> 
     <li>将资源上传到AEM实例</li> 
     <li>创建主题</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-users</td> 
   <td>
    <ul> 
     <li>创建、预览、发布和提交自适应表单</li> 
     <li>创建、预览和发布交互式通信和文档片段</li> 
     <li>使用代码编辑器创建自适应表单脚本</li> 
     <li>上传包括脚本的资源</li> 
     <li>创建主题</li> 
     <li>导入包含XDP的包</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>表单 — 提交 — 审阅者</td> 
   <td>
    <ul> 
     <li>审核提交</li> 
     <li>批准或拒绝提交</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>模板作者<sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>创建和预览自适应表单或交互式通信模板</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm-authors</p> </td> 
   <td>
    <ul> 
     <li>创建和修改表单数据模型</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>使用代理UI访问通信管理信件或交互式通信</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> 
     <li>创建收件箱应用程序</li> 
     <li>创建工作流模型</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>workflow-users</td> 
   <td>
    <ul> 
     <li>使用AEM收件箱应用程序<br /> <strong>注意： </strong>您必须分配有cm-agent-users和workflow-users组，才能访问AEM收件箱中的交互式通信代理UI。</li> 
     <li>管理工作流实例</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>fd-administrator</td> 
   <td>
    <ul> 
     <li>配置 PDF 生成器</li> 
     <li>配置Watched文件夹</li> 
     <li>管理工作流应用程序</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. 具有表单 — 用户组权限的用户无法编写自适应表单的脚本。
1. 具有模板作者组权限的用户无法编写模板的脚本。
