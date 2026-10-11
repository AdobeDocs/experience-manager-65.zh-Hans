---
title: 编码误区
description: 为AEM开发时要避免的常见编码陷阱
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 4%
---
# 编码误区{#code-pitfalls}

## 避免Java代码中的Sling绑定 {#avoid-sling-bindings-in-java-code}

在90%的情况下，使用Sling绑定是不合适访问服务的方式。 您应该改用&#x200B;*@Reference*&#x200B;或&#x200B;*@Inject*&#x200B;注释。

## 避免Java代码中的Thread.interrupt {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt*&#x200B;很危险，因为它可以在错误时间调用时关闭文件，包括Lucene文件和永久缓存文件。

## 避免将Java同步与ReadWriteLocks混合使用 {#avoid-mixing-java-synchronization-with-readwritelocks}

这可能导致争用情况，在这种情况下，代码将最终死锁。
