---
title: Dynamic Media 限制
description: 了解创建图像集、旋转集或上传PDF时的最佳实践和强制的限制。 还了解Dynamic Media不支持的Web浏览器和操作系统组合。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Image Sets,Spin Sets,eCatalog
role: User
exl-id: e4d4059e-ac0b-42e7-910c-001310796574
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
  - id: d4b6216b-4a89-4ff0-8ac0-5a699ba23100
    internal-label: Images and videos
subfeature_v2:
  - id: c12bda38-aa1a-4647-b62e-42cd4537dac6
    internal-label: Dynamic Media Classic
  - id: e2dc1259-9034-40fc-a518-b92a34fe6642
    internal-label: Image sets
  - id: cb008a68-9156-4b10-9c66-391409a53067
    internal-label: Spin Sets
  - id: fb5874db-3110-450a-b647-a5c2ce139bef
    internal-label: eCatalog
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 8%
---
# Dynamic Media限制

以下部分介绍Dynamic Media中的限制。

本主题包含以下部分：

* [Dynamic Media对资产类型的最佳实践和强制限制](#best-practice-enforced-limits)
* [Dynamic Media不支持的Web浏览器和操作系统组合](#unsupported-browser-os)

## Dynamic Media对资产类型的最佳实践和强制限制 {#best-practice-enforced-limits}

在创建旋转集或图像集，或者上传PDF进行页面提取时，Adobe建议以下最佳实践并强制实施以下限制：

| 资源 — 限制类型 | 最佳实践 | 施加的限制 |
| --- | --- | --- |
| **图像** — 每个图像的智能裁剪数 | 5 | 100 |
| **所有集** — 每个集的重复资源数 | 无重复项 | 20‡ |
| **所有集** — 每个集的最大资源数 | 每组5至10个图像 | 1000 |
| **旋转集** — 每个2D集的最大行数/列数 | 每组12-18个图像 | 1000 |
| **PDF** — 考虑提取的PDF的最大页数 |  | 100（适用于所有PDF） |

‡最佳实践是在一个集中没有重复的资产。 单个资产的限制为20个重复项。 如果为该资产添加其他重复项（在该集中），请求将会产生错误或忽略重复项。
<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Dynamic Media不支持的Web浏览器和操作系统组合 {#unsupported-browser-os}

Dynamic Media不支持以下Web浏览器和操作系统的组合。

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1更新
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9小牛
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 Yosemite

## 停止对Secure Socket Layer 2.0和3.0以及Transport Layer Security 1.0和1.1的支持 {#tls}

<!--
CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022)
-->

自2024年4月30日起，Adobe Dynamic Media将停止支持以下内容：

* SSL（安全套接字层）2.0
* SSL 3.0
* TLS（传输层安全性）1.0 和 1.1
* TLS 1.2 中的以下弱密码：
  * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
  * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
  * `TLS_RSA_WITH_AES_256_GCM_SHA384`
  * `TLS_RSA_WITH_AES_256_CBC_SHA256`
  * `TLS_RSA_WITH_AES_256_CBC_SHA`
  * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
  * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
  * `TLS_RSA_WITH_AES_128_GCM_SHA256`
  * `TLS_RSA_WITH_AES_128_CBC_SHA256`
  * `TLS_RSA_WITH_AES_128_CBC_SHA`
  * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
  * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
  * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
  * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

