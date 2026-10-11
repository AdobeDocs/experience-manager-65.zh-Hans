---
title: 帮助管理员启动并运行的最佳实践
description: 查找由Adobe工程和咨询团队编译的最佳实践，帮助管理员启动和运行。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 576d87c8-cc96-45a0-b3cf-defb440babbb
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 13%
---
# 最佳做法{#best-practices}

最佳实践描述如何以尽可能高效和最有效的方式开发、管理或使用AEM。 这一不断增加的主题列表包括AEM中的多个领域。

以下区域提供了有关最佳实践的文档：

* [Assets](#assets)
* [Sites](#sites)

有关创作、部署和维护或开发的最佳实践，请参阅以下内容之一：

* [创作最佳做法](/help/sites-authoring/best-practices.md)
* [开发最佳做法](/help/sites-developing/best-practices.md)
* [部署最佳实践](/help/sites-deploying/best-practices.md)

下面的表格中介绍了特定文档并将其链接到该文档。

## Assets {#assets}

以下主题介绍了有关Assets的最佳实践，包括Dynamic Media功能和Dynamic Media Classic集成：

<table>
 <tbody>
  <tr>
   <td>Assets周围不同区域的最佳实践，用于增强负载下的系统稳定性和性能</td>
   <td><a href="/help/assets/best-practices-for-assets.md">用于资产的最佳实践</a></td>
   <td>包含指向Assets周围不同区域的最佳实践指南的链接。 查看这些文档后，您将拥有构建和管理企业资产管理系统的知识和工具。</td>
  </tr>
  <tr>
   <td>如何组织内容（文件夹层次结构）</td>
   <td><a href="/help/assets/organize-assets.md">文件管理最佳实践</a></td>
   <td>大多数处理配置文件是基于文件夹的，因为视频、元数据、图像处理始终应用于文件夹。 此最佳实践文档介绍如何定义和设置文件夹层次结构，因为层次结构对如何处理内容有显着影响。 </td>
  </tr>
  <tr>
   <td>集成Scene7和AEM</td>
   <td><a href="/help/sites-administering/scene7.md#best-practices-for-integrating-scene-with-aem">将Scene7与AEM集成的最佳实践</a></td>
   <td><p>描述何时启用轮询导入程序、如何测试您的集成，以及何时使用内容浏览器而不是直接上传到Assets。</p> </td>
  </tr>
  <tr>
   <td>图像预设选项</td>
   <td>了解<a href="/help/assets/managing-image-presets.md#understanding-image-presets">图像预设</a>和<a href="/help/assets/managing-image-presets.md#image-preset-options">图像预设最佳实践</a></td>
   <td>作为有关<a href="/help/assets/managing-image-presets.md">管理图像预设</a>的文档的一部分，这些主题描述了什么是图像预设以及有关选择图像预设选项的最佳实践。</td>
  </tr>
  <tr>
   <td>Dynamic Media与Scene7直接集成</td>
   <td><a href="/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media">Scene7/AEM集成与Dynamic Media集成</a></td>
   <td>描述何时最好使用Dynamic Media解决方案、何时将S7与AEM集成或者何时同时使用二者。</td>
  </tr>
 </tbody>
</table>

## Sites {#sites}

管理和创作网站内容有一些最佳实践，如下所示：

<table>
 <tbody>
  <tr>
   <td>GDPR合规性</td>
   <td><a href="/help/sites-administering/gdpr-compliance-sites.md">AEM Sites GDPR合规性</a></td>
   <td>欧盟《通用数据保护条例》关于数据隐私权的规定自 2018 年 5 月起正式生效。 AEM Sites符合GDPR。 此页面将指导客户完成在 AEM Sites 中处理 GDPR 请求的过程。 它描述了私有数据的存储位置，以及如何手动或使用代码移除私有数据。</td>
  </tr>
  <tr>
   <td>为您的实例定义默认UI。</td>
   <td><p><a href="/help/sites-authoring/select-ui.md#configuring-the-default-ui-for-your-instance">为实例配置默认UI</a></p> </td>
   <td>AEM具有两个UI：触控优化和Classic。 本节详细介绍如何为实例定义默认UI。</td>
  </tr>
  <tr>
   <td>多站点管理</td>
   <td><a href="/help/sites-administering/msm-best-practices.md">MSM 最佳做法</a></td>
   <td>使用MSM自动进行内容部署的最佳实践。 </td>
  </tr>
  <tr>
   <td>翻译内容</td>
   <td><a href="/help/sites-administering/tc-bp.md">翻译最佳做法</a></td>
   <td>规划和实施多语言站点的最佳实践。</td>
  </tr>
  <tr>
   <td>用户管理</td>
   <td><a href="/help/sites-administering/security.md#best-practices">权限和权限最佳实践</a></td>
   <td>描述使用权限和特权时的最佳实践 </td>
  </tr>
  <tr>
   <td>工作流</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md#configuration">工作流最佳实践 — 配置</a></td>
   <td>借助工作流，您可以自动执行Adobe Experience Manager (AEM)活动，并且可以显示在AEM环境中发生的大量处理，因此强烈建议仔细规划和配置工作流实施。</td>
  </tr>
 </tbody>
</table>
