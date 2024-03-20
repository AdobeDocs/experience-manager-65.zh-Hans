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
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 2%

---

# 关于从Dynamic Media-Hybrid迁移到Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid是Dynamic Media与Adobe Experience Manager集成的旧版本。 混合版本最初在Adobe Experience Manager 6.1中引入。虽然Adobe继续支持混合模式，但它不是首选模式；首选使用Dynamic Media-Scene7模式。 混合模式也不支持智能裁切和全景图像等新功能，而Dynamic Media-Scene7则支持这些功能。

Dynamic Media-Hybrid与Dynamic Media-Scene7之间的其他主要区别包括：

* URL的结构。
* 视频摄取。
* 创建和存储图像演绎版。
* 云配置和凭据（配置）。

从Dynamic Media-Hybrid迁移到Dynamic Media-Scene7时，有两个选项可用。 第一个选项是仅在Experience Manager上预配Dynamic Media-Scene7的新实例。 第二个选项是将现有Dynamic Media — 混合实例迁移到Dynamic Media-Scene7。 此选项以表格形式概述了移动过程中要采取的步骤和注意事项。

>[!IMPORTANT]
>
>Adobe建议您不要在实时生产实例上将Dynamic Media-Hybrid实施迁移到Dynamic Media-Scene7。

## 选项1 — 在Experience Manager上预配Dynamic Media-Scene7的新实例 {#provision-new-dms7}

请考虑一下，只需在Adobe Experience Manager上通过新的预配置Dynamic Media-Scene7实例从头开始。 除了通过Dynamic MediaCloud Service摄取和处理资源外，还强烈建议对资源使用情况、工作流和组件进行Adobe审核。 通常，您可以使用较新的、现成可用的功能替换自定义组件和工作流。

## 选项2 — 将现有Dynamic Media — 混合实例迁移到Dynamic Media-Scene7 {#process-for-migrating}

| 步骤 | 任务 | 注意事项 |
|---|---|---|
| 1 | 克隆Dynamic Media — 混合创作实例。 | 维护现有的Dynamic Media — 混合创作实例以进行回退，直到此迁移过程中的其余步骤成功完成为止。 |
| 2 | 在Dynamic Media-Scene7模式下启动克隆的创作实例。 |  |
| 3 | 在Adobe Experience ManagerCloud Service中，使用Dynamic Media-Scene7凭据配置Dynamic Media。 | Adobe必须批准Dynamic Media-Scene7配置。 因此，您同时具有Adobe支持的Dynamic MediaM-Hybrid和Dynamic Media-Scene7环境，但这些环境仅在有限时间内可用。 |
| 4 | 创建迁移包，以便您可以根据需要摄取资源。<br>删除初始引入Dynamic Media-Hybrid期间创建的本地PTIFF。 | 如果所有资源当前在Dynamic Media — 混合实例中均可用，则克隆的已包含所有这些资源。 因此，不需要捆绑。 |
| 5 | 运行资源更新工作流，以便您可以将资源同步到Dynamic MediaCloud Service。 | Adobe建议分批执行更新工作流以允许压缩。 |
| 6 | 迁移查看器、图像和视频预设。 |  |
| 7 | 浏览每个受Web内容管理引用的资产，并更新其关联的URL。 |  |
| 8 | 迁移您要支持新Dynamic Media-Scene7模式的任何自定义工作流（手动更新）。 |  |
| 9 | 验证Web内容管理上传和配置。 |  |
| 10 | 验证后，获得禁用混合创作Dynamic Media的批准（作为回退进行维护）。 |  |
| 11 | 在成功使用Dynamic Media-Scene7大约一个月后，删除Dynamic Media-Hybrid Author实例。 |  |
