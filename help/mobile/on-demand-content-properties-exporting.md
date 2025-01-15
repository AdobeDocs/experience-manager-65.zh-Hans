---
title: 使用内容属性导出内容
description: 以下页面显示了应用程序属性和节点。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: db1c33c9-8539-436d-b4d0-3d5e6fd688ed
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 3%

---

# 使用内容属性导出内容{#using-content-properties-to-export-content}

{{ue-over-mobile}}

在AEM中，应用表示为&#x200B;*cq：Pages*。

除了下面显示的表示支持属性的集成的其他属性之外，它们还共享在任何&#x200B;*cq：Page*&#x200B;中找到的相同公共属性。

## 应用程序属性 {#app-properties}

下表显示了&#x200B;**应用程序属性和节点**。

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>dps-cloudConfig</td>
   <td>String：Path</td>
   <td><p>配置的Mobile On-DemandCloud Service的路径。 用于AEM Mobile到Mobile On-Demand操作（API调用）</p> <p>当作者选择将Mobile On-DemandCloud Service与应用程序关联时，可以通过“管理连接”拼贴配置此关联。</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>String：Path</td>
   <td><p>应用程序导出配置的路径。 导出配置是一个包含2个子ContentSync导出配置模板的文件夹；</p> <p><i>dps-article</i>： ContentSync导出配置以导出文章内容</p> <p><i>dps-HTMLResources</i>： ContentSync导出配置以导出应用程序/文章共享资源</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>字符串</td>
   <td><p>此应用程序链接/绑定的Mobile On-Demand项目的ID/URI。</p> <p>当作者从关联的Mobile On-DemandCloud Service的可用项目列表中选择项目时，可通过“管理连接”拼贴配置此关联。</p> </td>
  </tr>
  <tr>
   <td>dps-projectTitle</td>
   <td>字符串</td>
   <td>应用程序标题。</td>
  </tr>
  <tr>
   <td>dps-resourceType</td>
   <td>字符串</td>
   <td>内容类型。</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploaded</td>
   <td>日期</td>
   <td>上次将共享资源从AEM上传到AEM Mobile的日期。</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>String：userid</td>
   <td>执行了上次将共享资源请求从AEM上传到AEM Mobile的用户的ID。</td>
  </tr>
  <tr>
   <td>pge-dashboard-config</td>
   <td>String：Path</td>
   <td>仪表板配置的路径。 路径可以根据需要重定向到自定义仪表板配置。</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>String：Path</td>
   <td><p>属于或扩展<i>mobileapps/core/components/instance的cq：Component的路径。</i></p> <p>这会在应用程序目录中提供状态和渲染。</p> </td>
  </tr>
 </tbody>
</table>

您可以使用&#x200B;***内容属性***&#x200B;创建内容。 有关创建和导出文章和共享资源，请参阅以下资源：

* [内容属性](/help/mobile/content-properties.md)
* [创建文章导出配置](/help/mobile/creating-article-export-configuration.md)
* [创建共享资源导出配置](/help/mobile/creating-shared-resources-export-configuration.md)
