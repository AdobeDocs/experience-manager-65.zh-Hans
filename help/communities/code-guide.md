---
title: 编码准则
description: Communities开发人员指南、提示和技巧
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

---

# 编码准则 {#coding-guidelines}

## 指南、提示和技巧 {#guidelines-tips-and-tricks}

使用AEM Communities已经从严重依赖Java Server Pages发展到灵活选择模板脚本语言，因为这种语言的业务逻辑、样式和页面内容彼此不同。

在使用用户生成的内容(UGC)方面更大的灵活性是通过SocialResourceProvider API，这消除了对于为部署选择了哪个[SRP](srp.md)选项的感知。

以下是AEM Communities开发人员的各种编码准则和最佳实践：

### 代码 {#code}

* [使用SRP访问UGC](accessing-ugc-with-srp.md) — 如何避免编写仅当UGC存储在JCR (JSRP)中时才有效的应用程序。
* [SocialUtils重构](socialutils.md) — 用于替换SocialUtils的SRP的实用工具方法。
* [命名约定](naming-conventions.md) — 自定义Java类的命名约定。

### 脚本 {#scripts}

* [侧载社区组件](sideloading.md) — 如何在页面加载后动态添加组件。
* [富文本编辑器软件包](rte.md) — 如何自定义提供给成员用于发布内容的富文本UI。

### IDE {#ide}

* [使用Maven for Communities](maven.md) — 如何包含Communities API jar。
* [SocialUtils重构](socialutils.md) — 用于替换SocialUtils的SRP的实用工具方法。
