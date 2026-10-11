---
title: 自适应Forms、HTML5表单和AEM Forms的常见问题解答(FAQ)
description: 有关自适应Forms、HTML5表单和AEM Forms的布局、脚本支持和范围的常见问题解答(FAQ)。
docset: aem65
exl-id: 19a6e431-de66-4d5c-924f-f9c1a195390c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
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
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 4%
---
# 常见问题解答（FAQ） {#frequently-asked-questions-faq}

1. 为什么中的条形码和签名字段未显示在我的HTML 5表单中？

   回答：条形码和签名字段在HTML或移动设备场景中无关。 这些字段显示为非交互区域。 但是，AEM Forms Designer提供了一个新的签名涂写字段，该字段可用于代替签名字段。 还可以添加用于条形码的[自定义构件](../../forms/using/custom-widgets.md)并将其集成。
