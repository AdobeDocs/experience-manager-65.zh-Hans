---
title: Adobe Experience Manager 6.5中的Dynamic Media存储库重组
description: 了解如何进行必要的更改，以迁移到Experience Manager 6.5 for Dynamic Media中的新存储库结构。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 4e736924-74ea-431a-be19-1c4ff022f464
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 835ee49e-9248-5578-a60a-15c097807178
    internal-label: Upgrading
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 3%
---
# Adobe Experience Manager 6.5中的Dynamic Media存储库重组 {#dynamic-media-repository-restructuring-in-aem}

如Adobe Experience Manager 6.5](/help/sites-deploying/repository-restructuring.md)中的父[存储库重构页面中所述，升级到Experience Manager 6.5的客户应使用此页面评估与影响Dynamic Media的存储库更改相关的工作量。 在Experience Manager 6.5升级过程中，有些更改需要您尽心尽力，而其他更改则可能会推迟到将来升级时再进行。

**在将来升级之前**

* [自定义自适应视频编码配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Dynamic Media (DMS7)云配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Dynamic Media（DM混合）Cloud Service配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Dynamic Media - YouTube Cloud Service配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [杂项](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## 在将来升级之前 {#prior-to-upgrade}

### 自定义自适应视频编码配置  {#custom-adaptive-video-encoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>您可以运行以下迁移脚本以迁移到新位置：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>或者，您也可以在Experience Manager UI中编辑配置，并将更改保存到新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media (DMS7)云配置 {#dynamic-media-dms-cloud-configuration}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>客户可以在以下位置运行迁移脚本：<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>重新启动Dynamic Media OSGi捆绑包。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### Dynamic Media（DM混合）Cloud Service配置 {#cloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>您可以运行下面的迁移脚本以与最新模型保持一致：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media - YouTube Cloud Service配置  {#youtubecloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/cloudservices/youtube</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>1. 从YouTube<br /> 2取消发布所有视频。 使用新的TouchUI（从<code>/conf</code>）创建YouTube配置，包括从旧位置<br /> 3复制所有渠道。 将所有视频发布回YouTube。</p> <p>此工作流可生成新的YouTube URL。 如果您在创建TouchUI YouTube配置之前没有取消发布，则您将在属性下列出多个YouTube URL，因为如果有机会，重新创建的渠道会再次发布。 此功能意味着您的“属性”下列出了无用的URL。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 杂项 {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/dam/imageserver/macros</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>客户可以运行以下迁移脚本。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>或者，您也可以在Experience Manager UI中编辑配置，并将更改保存到新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/dam/presets/analytics</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>客户可以运行以下迁移脚本。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>
