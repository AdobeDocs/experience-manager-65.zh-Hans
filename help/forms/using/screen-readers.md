---
title: HTML5 Forms 的屏幕阅读器
description: 列出HTML5表单支持的屏幕阅读器。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: HTML5 Forms,Mobile Forms
exl-id: 07d20c2f-7d13-48ac-8d58-b367eb194558
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 3%
---
# HTML5 Forms 的屏幕阅读器 {#screen-readers-for-html-forms}

HTML5 forms组件将XFA表单模板渲染为HTML5格式。 所有支持HTML5的标准浏览器都可以呈现这些表单。 为了支持跨PDF和HTML5表单进行类似的数据捕获体验，PDF forms的布局保留在HTML5表单中。

HTML5 forms使用标准的HTML结构，从而允许将HTML的常规辅助工具与这些表单一起使用。 如果表单是根据可访问表单的最佳实践而设计的，则它可与任何受支持的屏幕阅读器配合使用。 此外，此类表单还支持键盘导航。

## 辅助功能标准 {#accessibility-standards}

HTML5 forms符合Section 508关于可访问性的规定，但存在已知例外。 有关详细信息，请参阅HTML5表单的[VPAT](https://www.adobe.com/content/dam/cc1/en/accessibility/compliance/pdfs/adobe-livecycle-es4-section-508-vpat-portfolio.pdf)。

## HTML5 Forms的认证屏幕阅读器 {#certified-screen-readers-for-html-forms}

* ® Windows上的JAWS 14.0
* macOS X和iPad上的Voicover

### 颌骨 {#jaws}

所有默认击键和快捷键均适用于HTML5表单。 有关使用JAWS的详细信息，请访问[https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp)。

### 配音 {#voiceover}

HTML5表单支持所有默认的“语音切换”按键和手势。 有关设置和使用VoiceOver的详细信息，请参阅[https://www.apple.com/accessibility/vision/](https://www.apple.com/accessibility/vision/)。

## 已知问题 {#known-issues}

* **（仅限Internal Explorer 9）**&#x200B;在HTML5表单中，按需加载页面（动态）。 按需页面加载导致屏幕阅读器的功能出现问题。 当屏幕阅读器的焦点位于页面的最后一个字段并且用户按下Tab键时，屏幕阅读器将焦点返回到表单上第一页的第一字段。
* **（仅限Internal Explorer 9）** HTML5窗体中的日期选取器控件无法通过键盘完全访问。 在日期选择器控件中，如果多次按向上/向下键，则日期选择器控件将关闭，并且焦点将移至下一个/最后一个字段。

* VoiceOver无法在iPad safari上的日期小部件上检测箭头键。
