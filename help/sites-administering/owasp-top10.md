---
title: OWASP前10名
description: 了解AEM如何处理前十大OWASP安全风险。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# OWASP前10名{#owasp-top}

[开放Web应用程序安全项目](https://owasp.org/) (OWASP)维护了一个列表，列出了[十大Web应用程序安全风险](https://owasp.org/www-project-top-ten/)。

下面列出了这些术语，并解释了CRX如何处理这些术语。

## 1.注射 {#injection}

* SQL — 设计禁止：默认存储库设置既不包含也不需要传统数据库，所有数据都存储在内容存储库中。 所有访问仅限于经过身份验证的用户，并且只能通过JCR API执行。 仅搜索查询支持SQL (SELECT)。 此外，SQL提供值绑定支持。
* LDAP — 无法进行LDAP注入，因为身份验证模块会过滤输入并使用绑定方法执行用户导入。
* OS — 没有从应用程序内执行shell。

## 2.跨站点脚本(XSS) {#cross-site-scripting-xss}

一般缓解做法是使用基于[OWASP编码器](https://owasp.org/www-project-java-encoder/)和[AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project)的服务器端XSS保护库对用户生成的内容的所有输出进行编码。

XSS是测试和开发期间的首要任务，发现的任何问题通常都会立即得到解决。

## 3.身份验证和会话管理中断 {#broken-authentication-and-session-management}

AEM使用可靠的身份验证技术，依赖于[Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html)和[Apache Sling](https://sling.apache.org/)。 AEM中未使用浏览器/HTTP会话。

## 4.不安全的直接对象引用 {#insecure-direct-object-references}

对数据对象的所有访问都由存储库进行调解，因此受基于角色的访问控制的限制。

## 5.跨站点请求伪造(CSRF) {#cross-site-request-forgery-csrf}

通过自动将加密令牌注入所有表单和AJAX请求并在服务器上验证每个POST的此令牌，可缓解跨站点请求伪造(CSRF)。

此外，AEM附带基于反向链接标头的过滤器，该过滤器可以配置为&#x200B;*仅*&#x200B;允许来自特定主机的POST请求（在列表中定义）。

## 6.安全配置错误 {#security-misconfiguration}

无法保证所有软件的配置始终正确。 但是，Adobe努力提供尽可能多的指导，并使配置尽可能简单。 此外，AEM还随附[集成的安全运行状况检查](/help/sites-administering/operations-dashboard.md)，帮助您一目了然地监视安全配置。

查看[安全核对清单](/help/sites-administering/security-checklist.md)以了解详细信息，其中提供了逐步强化说明。

## 7.不安全的加密存储 {#insecure-cryptographic-storage}

密码将作为加密哈希存储在用户节点中。 默认情况下，此类节点仅可由管理员和用户自己读取。

使用FIPS 140-2认证的加密库以加密形式存储诸如第三方凭据之类的敏感数据。

## 8.无法限制URL访问 {#failure-to-restrict-url-access}

存储库允许通过访问控制条目为任何给定路径上的任何给定用户或组设置[细粒度权限（由JCR指定）](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html)。 存储库强制执行访问限制。

## 9.传输层保护不足 {#insufficient-transport-layer-protection}

通过服务器配置减轻（例如，仅使用HTTPS）。

## 10.未验证的重定向和转发 {#unvalidated-redirects-and-forwards}

通过限制所有重定向到用户提供的目标的操作来缓解此问题。
