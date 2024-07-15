---
title: 更改外观
description: 了解如何编辑负责在Adobe Experience Manager Communities中为每个评论创建整体HTML的comment.hbs脚本。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# 更改外观 {#alter-the-appearance}

## 修改脚本 {#modify-the-script}

`comment.hbs`脚本负责为每个评论创建整体HTML。

要不在每个发布的评论旁边显示头像，请执行以下操作：

1. 将`comment.hbs`从`libs`复制到`apps`

   1. 选择`/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. 选择&#x200B;**[!UICONTROL 复制]**
   1. 选择`/apps/social/commons/components/hbs/comments/comment`
   1. 选择&#x200B;**[!UICONTROL 粘贴]**

1. 打开覆盖的`comment.hbs`

   * 双击`/apps/social/commons/components/hbs/comments/comment folder`中的节点`comment.hbs`

1. 查找以下行，然后将其删除或注释掉：

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

请删除这些行，或用`<!--`和`-->`将它们括起来，以便您将其注释掉。 此外，还将添加字符“xxx”作为显示头像位置的可视指示器。

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### 复制叠加 {#replicate-the-overlay}

使用复制工具将覆盖的注释组件推送到发布实例。

>[!NOTE]
>
>更可靠的复制形式是在包管理器中创建包并[激活](/help/sites-administering/package-manager.md#replicating-packages)。 可以导出和存档资源包。

从全局导航中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 复制]**，然后单击&#x200B;**[!UICONTROL 激活树]**。

对于起始路径，输入`/apps/social/commons`并选择&#x200B;**[!UICONTROL 激活]**。

![verify-content-template](assets/verify-content-template.png)

### 查看结果 {#view-results}

https://localhost:4503/crx/de如果您以管理员身份（例如，以admin/admin身份）登录发布实例，则可以验证是否存在覆盖的组件。

如果您注销然后以`aaron.mcdonald@mailinator.com/password`身份登录并刷新页面，则您发现显示的人像不会与发布的评论一起显示。 而是显示简单的“xxx”。

![create-template-component](assets/create-template-component.png)
