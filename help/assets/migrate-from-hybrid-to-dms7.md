---
title: 从Dynamic Media — 混合模式迁移到Dynamic Media - S7模式
description: 了解如何将Dynamic Media — 混合模式实例迁移到Dynamic Media - S7模式
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Scene7 Mode,Hybrid Mode
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
subfeature_v2:
  - id: ee69dd13-2aba-4eb0-912b-399e82368d73
    internal-label: Scene7 mode
  - id: cf50b0d2-df62-495c-a741-4fa0284ca4fc
    internal-label: Hybrid mode
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 2%
---
# 关于从Dynamic Media-Hybrid移动到Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid是Dynamic Media与Adobe Experience Manager集成的旧版本。 混合版本最初在Adobe Experience Manager 6.1中引入。 虽然Adobe继续支持混合模式，但它不是首选模式；首选使用的模式是Dynamic Media-Scene7 。 混合模式也不支持智能裁切和全景图像等新功能，而Dynamic Media-Scene7则支持这些功能。

Dynamic Media-Hybrid和Dynamic Media-Scene7之间的其他关键区别包括：

* URL的结构。
* 视频摄取。
* 创建和存储图像演绎版。
* 云配置和凭据（配置）。

从Dynamic Media-Hybrid移动到Dynamic Media-Scene7时，有两个选项可用。 第一个选项是仅在Experience Manager上预配Dynamic Media-Scene7的新实例。 第二个选项是将现有Dynamic Media-Hybrid实例迁移到Dynamic Media-Scene7。 此选项以表格形式概述了移动过程中要采取的步骤和注意事项。

>[!IMPORTANT]
>
>Adobe建议您不要在实时生产实例上将Dynamic Media-Hybrid实施迁移到Dynamic Media-Scene7。

## 选项1 — 在Experience Manager上预配Dynamic Media-Scene7的新实例 {#provision-new-dms7}

只需考虑在Adobe Experience Manager上新建一个已配置的Dynamic Media-Scene7实例即可。 除了通过Dynamic Media Cloud Service摄取和处理资源外，还强烈建议使用Adobe审核资源使用情况、工作流和组件。 通常，您可以使用较新的、现成可用的功能替换自定义组件和工作流。

## 选项2 — 将现有Dynamic Media-Hybrid实例迁移到Dynamic Media-Scene7 {#process-for-migrating}

| 步骤 | 任务 | 注意事项 |
|---|---|---|
| 1 | 克隆Dynamic Media混合创作实例。 | 维护现有的Dynamic Media-Hybrid创作实例以进行回退，直到此迁移过程中的其余步骤成功完成为止。 |
| 2 | 在Dynamic Media-Scene7模式下启动克隆的创作实例。 |  |
| 3 | 在Adobe Experience Manager云服务中，使用Dynamic Media-Scene7凭据配置Dynamic Media 。 | Adobe必须批准Dynamic Media-Scene7配置。 因此，您同时具有Adobe支持的Dynamic MediaM-Hybrid和Dynamic Media-Scene7环境，但时间有限。 |
| 4 | 创建迁移包，以便您可以根据需要摄取资源。<br>删除初始引入Dynamic Media-Hybrid期间创建的本地PTIFF。 | 如果Dynamic Media-Hybrid实例中的所有资源当前均可用，则克隆的已包含所有这些资源。 因此，不需要捆绑。 |
| 5 | 运行资源更新工作流，以便您可以将资源同步到Dynamic Media Cloud Service。 | Adobe建议分批执行更新工作流以允许压缩。 |
| 6 | 迁移查看器、图像和视频预设。 |  |
| 7 | 浏览每个受Web内容管理引用的资产，并更新其关联的URL。 |  |
| 8 | 迁移您要支持新Dynamic Media-Scene7模式的任何自定义工作流（手动更新）。 |  |
| 9 | 验证Web内容管理上传和配置。 |  |
| 10 | 验证后，获得禁用动态媒体混合创作（作为回退进行维护）的批准。 |  |
| 11 | 成功使用Dynamic Media-Scene7大约一个月后，删除Dynamic Media-Hybrid创作实例。 |  |
