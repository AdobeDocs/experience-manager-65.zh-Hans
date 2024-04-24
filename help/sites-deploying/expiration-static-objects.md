---
title: 静态对象过期
description: 了解如何配置Adobe Experience Manager以使静态对象在合理的时间段内不会过期。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: bfd5441c-19cc-4fa8-b597-b1221465f75d
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# 静态对象过期{#expiration-of-static-objects}

静态对象（例如图标）不会更改。 因此，系统应配置为它们不会过期（在合理的时间段内），从而减少不必要的流量。

这将产生以下影响：

* 从服务器基础架构卸载请求。
* 提高页面加载的性能，因为浏览器会在浏览器缓存中缓存对象。

过期时间由HTTP标准有关文件的“过期时间”来指定(例如，参阅以下文档的第14.21章： [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) “超文本传输协议 — HTTP 1.1”)。 此标准使用标头来允许客户端缓存对象，直到它们被视为过时；此类对象将缓存指定的时间量，而不会对原始服务器进行任何状态检查。

>[!NOTE]
>
>此配置独立于（并且不适用于）Dispatcher。
>
>Dispatcher的用途是将数据缓存到Adobe Experience Manager (AEM)之前。

所有非动态且不会随时间变化的文件都可以并且应该缓存。 Apache HTTPD服务器的配置可能类似于以下内容之一，具体取决于环境：

>[!CAUTION]
>
>在定义将对象视为最新对象的时段时，请务必小心。 就这样 *在指定的时间段到期之前不检查*，客户端最终可能从缓存中显示旧内容。

1. **对于创作实例：**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /libs>
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType text/javascript "access plus 1 month"
     ExpiresByType image/png "access plus 1 month"
     ExpiresByType image/gif "access plus 1 month"
   </Location>
   ```

   这允许中间缓存（例如浏览器缓存）存储CSS、JavaScript、PNG和GIF文件一个月，直到它们过期为止。 这意味着它们不需要从AEM或Web服务器请求，但可以保留在浏览器缓存中。

   网站的其他部分不应缓存在创作实例上，因为它们随时可能更改。

1. **对于发布实例：**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /content>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   <Location /etc/designs>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   ```

   这允许中间缓存（例如，浏览器缓存）将CSS、JavaScript、PNG和GIF文件存储长达一天的客户端缓存中。 尽管此示例说明了以下所有内容的全局设置 `/content` 和 `/etc/designs`，您应该使其更加细化。

   根据站点更新的频率，您还可以考虑缓存HTML页面。 一个合理的时间段应该是一小时：

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

配置静态对象后，扫描 `request.log`，在选择包含此类对象的页面时，用来确认没有向静态对象发出（不必要的）请求。
