---
title: Comments Essentials
seo-title: Comments Essentials
description: 注释组件概述
seo-description: 注释组件概述
uuid: 58b7bb58-f598-4bcb-93ae-b7795cab51cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 18f54a1c-52aa-414d-b494-1f19b5c10345
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Comments Essentials {#comments-essentials}

本页提供了使用评论系统（评论组件）的基本功能以及管理用户在成员发布评论或回复时生成的内容(UGC)的选项。

评论组件建立评论系统，使得每个单独的帖子由评论组件（单数）表示。 它是包含在页面上的评论系统。 注释系统将在被调用时创建单个注释。

## 客户端必备工具 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>是——在设计模式下可编辑 <i>属 </i>性</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.porting</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/commons/components/hbs/comments/comments.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>CSS</strong></td>
   <td> /libs/social/commons/components/hbs/comments/clientlibs/commentsystem.css</td>
  </tr>
  <tr>
   <td><strong> 属性</strong></td>
   <td> 请参阅 <a href="comments.md">使用注释</a></td>
  </tr>
 </tbody>
</table>

[客户端自定义](client-customize.md)

### 每页一个实例 {#one-instance-per-page}

分页以及使用URL进行缓存和链接需要每个注释系统都具有唯一的URL。 因此，每页只允许一个评论系统实例。

其他功能已包括评论系统。 这些是：

* [博客](blog-developer-basics.md)
* [日历](calendar-basics-for-developers.md)
* [文件库](essentials-file-library.md)
* [论坛](essentials-forum.md)
* [问题与解答](qna-essentials.md)
* [审核](reviews-basics.md)

### 旗标原因列表 {#flag-reason-list}

可以通过向应用程序添加flagreasonlist.hbs来自定义标记原因列表以覆盖中的内容

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

这适用于扩展注释系统的任何组件。

## 服务器端必备工具 {#essentials-for-server-side}

* [注释API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [注释端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 访问已发布的注释(UGC) {#accessing-posted-comments-ugc}

UGC应使用一种标准的仲裁方法进行仲裁。
请参阅 [审核用户生成的内容](moderate-ugc.md)。

自AEM 6.1 Communities起，对UGC使用公 [用商店](working-with-srp.md) ，包括以编程方式访问UGC，而不管选择的存储选项（如ASRP、MSRP或JSRP）。

**UGC在存储库中的位置和格式可能会发生更改，但不会发出警告**。

请参阅：

* [存储资源提供者概述](srp.md) -简介和存储库使用概述
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP实用程序方法和示例
* [使用SRP访问UGC](accessing-ugc-with-srp.md) —— 编码准则
* [SocialUtils重构](socialutils.md) -将已弃用的实用程序方法映射到当前SRP实用程序方法

