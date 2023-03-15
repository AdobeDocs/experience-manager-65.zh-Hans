---
title: 投放 Dynamic Media 资源
description: 了解如何投放Dynamic Media资源
uuid: 23eddf83-34f5-4aae-8b81-d1cd7a098a7e
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e3b44330-d476-49c6-b7ba-079d0d60e500
docset: aem65
role: User, Admin
exl-id: 274af114-845a-46bd-b091-802cf589687a
feature: Asset Management,Renditions
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 13%

---

# 投放 Dynamic Media 资源{#delivering-dynamic-media-assets}

如何投放Dynamic Media资源（视频和图像）取决于网站的实施方式。

使用Dynamic Media，您有多个选项：

* 如果您的网站托管在Adobe Experience Manager上，那么您希望直接将Dynamic Media资源添加到您的页面。
* 如果您的网站不在Experience Manager中，则可以选择以下任一选项：

   * 将视频或图像嵌入到您的网站上。
   * 将URL链接到您的Web应用程序。当您希望将视频播放器作为弹出窗口或模式窗口投放时，请使用链接。
   * 如果您的网站是响应式的，您可以 [交付优化的图像](/help/assets/responsive-site.md).

>[!NOTE]
>
>智能成像可与您现有的图像预设配合使用，并在交付的最后毫秒内使用智能功能，以根据浏览器或网络连接速度进一步减小图像文件大小。 参见 [智能成像](/help/assets/imaging-faq.md) 了解更多信息。

有关更多信息，请参阅下列主题：

* [将Dynamic Media资源添加到网页](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [在网页上嵌入视频查看器或图像查看器](/help/assets/embed-code.md)
* [在 Dynamic Media 中激活热链接保护](/help/assets/hotlink-protection.md)
* [将 URL 关联到您的 Web 应用程序](/help/assets/linking-urls-to-yourwebapplication.md)
* [为响应式站点传送优化的图像](/help/assets/responsive-site.md)
* [HTTP2 内容交付](/help/assets/http2.md)
* [通过Dynamic Media Classic使CDN缓存失效](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [使用规则集转换 URL](/help/assets/using-rulesets-to-transform-urls.md)


## Dynamic Media资源的HTTP/2交付 {#http-delivery-of-dynamic-media-assets}

Experience Manager现在支持通过HTTP/2交付所有Dynamic Media内容（图像和视频）。 即，图像或视频的已发布URL或嵌入代码可与接受托管资产的任何应用程序集成。 随后，该已发布的资产将通过HTTP/2协议进行交付。 这种交付方法改进了浏览器和服务器的通信方式，从而可以为所有Dynamic Media资源提供更好的响应和加载时间。

要了解更多信息，请参阅 [HTTP/2内容交付常见问题解答](/help/sites-administering/scene7-http2faq.md).
