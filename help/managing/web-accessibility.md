---
title: Adobe Experience Manager（AEM）和 Web 无障碍指南
description: 介绍 Adobe Experience Manager（AEM）和 Web 无障碍指南
exl-id: db8785b9-09eb-444a-addc-74c520e710a9
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Developer, Leader, User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
    internal-label: Experience Manager 6.5
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c42c36cf-eeed-484a-8b39-a33a68192a07
    internal-label: Compliance
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 89%
---
# AEM 与 Web 无障碍指南{#aem-and-the-web-accessibility-guidelines}

出于许多社会、经济和法律动因，在设计 Web 内容时需要确保尽可能让任何目标受众都可以访问，不论他们是否是残障人士或受任何限制。 因此，通过 Adobe Experience Manager（AEM）实现 Web 无障碍，已成为优秀的 Web 设计一个日益重要的方面。

使用 AEM 创建无障碍网站和内容的影响包括：

* 管理员负责配置 AEM 以确保正确启用无障碍功能（无障碍功能）。

* 作者使用这些功能创建无障碍网站。

  创建无障碍内容是一个过程。 虽然 AEM 提供了一些功能，但内容作者需要确保遵循创建无障碍内容所要求的技术。

* 在实施网站设计时，模板开发人员还应注意到此类问题。

Adobe Experience Manager 符合[万维网联盟](#world-wide-web-consortium)提供的[指南](#wcag-accessibility-guidelines)。

>[!NOTE]
>
>有关更多详细信息，请参阅 [Adobe 解决方案的“无障碍合规性”报告](https://www.adobe.com/cn/accessibility/compliance.html)。

## 万维网联盟 {#world-wide-web-consortium}

[万维网联盟（W3C）](https://www.w3.org/) 是一个致力于开发 Web 标准的国际社区。 他们的 [Web 无障碍倡议（WAI）](https://www.w3.org/WAI/) 发布了 [Web 内容无障碍准则](#wcag-accessibility-guidelines)。

## Web 内容无障碍准则（WCAG）2.1 {#wcag-accessibility-guidelines}

为帮助 Web 设计人员和开发人员制作无障碍网站，[Web 无障碍倡议（WAI）](https://www.w3.org/WAI/) 于 2018 年 6 月发布了 [Web 内容无障碍准则（WCAG）2.1](https://www.w3.org/TR/WCAG/)。

WCAG 2.1 提供了[涵盖无障碍级别和如何符合这些级别的准则（包括相关成功标准）](https://www.w3.org/TR/WCAG/#conformance)。

## WCAG 2.1 和 AEM {#wcag-aem}

使用 Adobe Experience Manager，内容作者和/或网站所有者可以创建符合 WCAG 2.1 A 级和 AA 级成功标准的 Web 内容：

* [WCAG 2.1 快速入门指南](/help/managing/qg-wcag.md)中重点介绍了 WCAG 2.1 的特定方面。

* [创建无障碍内容](/help/sites-authoring/creating-accessible-content.md)详细介绍了这些内容与 AEM 的关系。

* [配置富文本编辑器以创建可访问的站点](/help/sites-administering/rte-accessible-content.md)
有关管理员如何配置AEM以生成无障碍内容的指南。

* [创建无障碍的自适应Forms](/help/forms/using/creating-accessible-adaptive-forms.md)
Adobe Experience Manager (AEM)包括多项特性和功能，可增强具有不同功能的用户使用自适应表单的可用性。 该解决方案还可帮助表单作者创建无障碍自适应表单。

>[!NOTE]
>
>在创建站点时，您应该大体上确定希望自己的站点符合哪个等级。

## Adobe 无障碍功能 {#accessibility-at-adobe}

有关其他信息，请访问 [Adobe 辅助功能资源中心。](https://www.adobe.com/cn/accessibility/)
