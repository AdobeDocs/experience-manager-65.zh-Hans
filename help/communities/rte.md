---
title: 富文本编辑器要点
description: 了解富文本编辑器的基础知识和功能，该编辑器允许您输入带有标记的文本。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 821e32f4-da8d-4bbb-936a-0844b8a24cdd
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 3%

---

# 富文本编辑器要点 {#rich-text-editor-essentials}

## 概述 {#overview}

富文本编辑器(RTE)允许您输入带标记的文本。

对于Communities组件，尽管与创作环境](../../help/sites-authoring/rich-text-editor.md)中的[富文本编辑器类似，但它会影响在发布环境中输入的文本。

![富文本编辑器](assets/rich-text-editor.png)

## 启用富文本编辑器 {#enabling-rich-text-editor}

可以启用允许用户生成内容(UGC)的社区组件以允许RTE。 如果该组件已添加到页面或包含在[函数](functions.md)中，则默认情况下可能会启用RTE，也可能不启用。

如果未启用，则只需进入[作者编辑模式](sites-console.md#authoring-site-content)，选择要编辑的组件，然后选中`Rich Text Editor`复选框即可。

RTE可用于以下Communities组件：

* [博客](blog-feature.md)
* [日程表](calendar.md)
* [评论](comments.md)
* [文件库](file-library.md)
* [论坛](forum.md)
* [消息](configure-messaging.md)
* [问题与解答](working-with-qna.md)
* [审核](reviews.md)

## 自定义 {#customization}

可以自定义富文本编辑器，因为实现基于[CKEditor](https://ckeditor.com/)。

Communities组件的当前配置位于`cq.social.  scf   clientlib`的存储库中的

`/libs/clientlibs/social/commons/scf/ckrte.js`

不建议修改cq.social.scf clientlib，因为未来的升级可能会覆盖任何编辑。

### 自定义示例：内联链接 {#example-customization-inline-links}

出于安全考虑，默认情况下，向成员显示的富文本图标集中不包含超链接选项。 当UGC中允许href时，恶意攻击的能力非常大。

要向工具栏添加超链接选项，请执行以下操作：

* 添加名为“`links`”的工具栏
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* 选择&#x200B;**[!UICONTROL 全部保存]**

#### /libs/clientlibs/social/commons/scf/ckrte.js {#libs-clientlibs-social-commons-scf-ckrte-js}

```
CKRte.prototype.config = {
    toolbar: [
        { name: "basicstyles",
           items: ["Bold", "Italic", "Underline", "NumberedList", "BulletedList", "Outdent", "Indent", "JustifyLeft", "JustifyCenter", "JustifyRight", "JustifyBlock", "TextColor"]
        },
        { name: 'links',
           items: [ 'Link','Unlink','Anchor' ]
        }
    ],
    autoParagraph: false,
    autoUpdateElement: false,
    removePlugins: "elementspath",
    resize_enabled: false
};
```
