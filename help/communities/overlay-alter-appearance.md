---
title: 更改外观
seo-title: Alter the Appearance
description: 修改脚本
seo-description: Modify the script
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# 更改外观 {#alter-the-appearance}

## 修改脚本 {#modify-the-script}

comment.hbs脚本负责为每个注释创建整体HTML。

要在每个已发布评论旁边不显示头像，请执行以下操作：

1. 复制 `comment.hbs`从 `libs`to `apps`

   1. 选择 `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. 选择 **[!UICONTROL 复制]**
   1. 选择 `/apps/social/commons/components/hbs/comments/comment`
   1. 选择 **[!UICONTROL 粘贴]**

1. 打开覆盖的 `comment.hbs`

   * 双击节点 `comment.hbs` in `/apps/social/commons/components/hbs/comments/comment folder`

1. 找到以下行，并删除或注释它们：

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

删除线条，或在线条周围设置 `<!--` 和 `-->` 去评论一下。 此外，还会添加字符“xxx”作为头像所在位置的视觉指示器。

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### 复制叠加 {#replicate-the-overlay}

使用复制工具将覆盖的评论组件推送到发布实例。

>[!NOTE]
>
>一种更为可靠的复制形式是在包管理器和 [激活](/help/sites-administering/package-manager.md#replicating-packages) 它。 可以导出和存档资源包。

在全局导航中，选择 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 复制]** 单击 **[!UICONTROL 激活树]**.

对于开始路径，输入 `/apps/social/commons` 选择 **[!UICONTROL 激活]**.

![verify-content-template](assets/verify-content-template.png)

### 查看结果 {#view-results}

如果您以管理员身份登录发布实例，例如以管理员/管理员身份登录https://localhost:4503/crx/de ，则可以验证覆盖的组件是否位于此处。

如果您注销，并重新登录为 `aaron.mcdonald@mailinator.com/password` 刷新页面后，您会发现发布的评论不再显示为头像，而是显示一个简单的“xxx”。

![create-template-component](assets/create-template-component.png)
