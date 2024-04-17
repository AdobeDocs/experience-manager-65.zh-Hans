---
title: 安全性
description: 应用程序安全在开发阶段启动
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
solution: Experience Manager, Experience Manager Sites
feature: Developing,Security
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# 安全性{#security}

应用程序安全在开发阶段启动。 Adobe建议应用以下安全最佳实践。

## 使用请求会话 {#use-request-session}

按照最小权限原则，Adobe建议使用绑定到用户请求的会话和适当的访问控制来完成每次存储库访问。

## Protect抵御跨站点脚本(XSS) {#protect-against-cross-site-scripting-xss}

跨站点脚本(XSS)允许攻击者将代码注入其他用户查看的网页。 恶意Web用户可以利用此安全漏洞绕过访问控制。

AEM应用了在输出时筛选所有用户提供的内容的原则。 在开发和测试过程中，防御XSS都被列为最高优先事项。

AEM提供的XSS保护机制基于 [AntiSamy Java™库](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) 提供者 [OWASP(Open Web Application Security Project)](https://owasp.org/). 默认的AntiSamy配置位于

`/libs/cq/xssprotection/config.xml`

通过覆盖配置文件来调整此配置，使其符合您自己的安全需求非常重要。 官方 [AntiSamy文档](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) 为您提供实施安全要求所需的所有信息。

>[!NOTE]
>
>Adobe建议您始终使用访问XSS保护API [AEM提供的XSSAPI](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/xss/XSSAPI.html).

此外，Web应用程序防火墙，例如 [适用于Apache的mod_security](https://www.modsecurity.org)中，提供了对部署环境的安全性的可靠、集中控制，并防止了以前未检测到的跨站点脚本攻击。

## 访问Cloud Service信息 {#access-to-cloud-service-information}

>[!NOTE]
>
>Cloud Service信息的ACL和确保实例安全所需的OSGi设置作为 [生产就绪模式](/help/sites-administering/production-ready.md). 虽然这意味着您无需手动更改配置，但仍建议您在开始部署之前查看配置。

当您 [将AEM实例与Adobe Experience Cloud集成](/help/sites-administering/marketing-cloud.md)，您使用 [Cloud Service配置](/help/sites-developing/extending-cloud-config.md). 有关这些配置的信息以及收集的任何统计信息都存储在资料档案库中。 Adobe建议，如果使用此功能，应检查此信息的默认安全性是否符合您的要求。

webservicesupport模块将统计信息和配置信息写入以下位置：

`/etc/cloudservices`

具有默认权限：

* 创作环境： `read` 对象 `contributors`

* 发布环境： `read` 对象 `everyone`

## Protect抵御跨站点请求伪造攻击 {#protect-against-cross-site-request-forgery-attacks}

有关AEM用于缓解CSRF攻击的安全机制的更多信息，请参阅 [Sling引用过滤器](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 安全核对清单和 [CSRF保护框架文档](/help/sites-developing/csrf-protection.md).
