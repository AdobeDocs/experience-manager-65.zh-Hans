---
title: 创建已关闭的用户组
description: 了解如何创建已关闭的用户组。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 1%

---

# 创建已关闭的用户组{#creating-a-closed-user-group}

封闭用户组(CUG)用于限制对已发布Internet站点内特定页面的访问。 此类页面要求分配的成员登录并提供安全凭据。

要在网站中配置此类区域，您可以：

* [创建实际的已关闭用户组并分配成员](#creating-the-user-group-to-be-used)。

* [将此组应用于所需的页面](#applying-your-closed-user-group-to-content-pages)，并选择（或创建）登录页面以供CUG的成员使用；将CUG应用于内容页面时也指定了该登录页面。

* [创建指向受保护区域](#linking-to-the-cug-pages)内至少一个页面的某种形式的链接，否则该链接将不可见。

* [配置Dispatcher](#configure-dispatcher-for-cugs)（如果正在使用中）。

>[!CAUTION]
>
>创建封闭用户组(CUG)时应当始终考虑性能。
>
>尽管CUG中的用户和组数量不受限制，但页面上的CUG数量过高可能会降低渲染性能。
>
>在进行性能测试时，应始终考虑CUG的影响。

## 创建要使用的用户组 {#creating-the-user-group-to-be-used}

要创建已关闭的用户组，请执行以下操作：

1. 从AEM homescreen转到&#x200B;**Tools - Security**。

   >[!NOTE]
   >
   >有关创建和配置用户和组的完整信息，请参阅[管理用户和组](/help/sites-administering/security.md#managing-users-and-groups)。

1. 从下一个屏幕中选择&#x200B;**组**&#x200B;信息卡。

   ![screenshot_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. 按右上角的&#x200B;**创建**&#x200B;按钮创建组。
1. 命名您的新组；例如，`cug_access`。

   ![screenshot_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. 转到&#x200B;**成员**&#x200B;选项卡，将所需用户分配给此组。

   ![screenshot_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. 激活您分配给CUG的任何用户；在本例中，为`cug_access`的所有成员。
1. 激活已关闭的用户组，使其在发布环境中可用；在本例中，`cug_access`。

## 将已关闭的用户组应用于内容页面 {#applying-your-closed-user-group-to-content-pages}

要将CUG应用到一个或多个页面，请执行以下操作：

1. 导航到要分配给CUG的受限制部分的根页面。
1. 通过单击页面的缩略图并选择顶部工具栏中的&#x200B;**属性**&#x200B;来选择页面。

   ![screenshot_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. 在以下窗口中，打开&#x200B;**高级**&#x200B;选项卡。

1. 向下滚动到&#x200B;**身份验证要求**&#x200B;部分。

   1. 激活&#x200B;**启用**&#x200B;复选框。

   1. 添加您的&#x200B;**登录页面**的路径。
这是可选操作，如果留空，则使用标准登录页面。

   已添加![CUG](assets/cug-authentication-requirement.png)

1. 接下来，转到&#x200B;**权限**&#x200B;选项卡并选择&#x200B;**编辑已关闭的用户组**。

   ![screenshot_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[!NOTE]
   >
   >“权限”选项卡中的 CUG 无法从 Blueprint 转出到 Live Copy。在配置Live Copy时对此进行规划。
   >
   >有关详细信息，请参阅[此页面](closed-user-groups.md#aem-livecopy)。

1. 将打开&#x200B;**编辑已关闭的用户组**&#x200B;对话框。 您可以在此搜索并选择您的CUG，然后通过&#x200B;**保存**&#x200B;确认组选择。

   该组将被添加到列表中；例如，组&#x200B;**cug_access**。

   已添加![CUG](assets/cug-added.png)

1. 通过&#x200B;**保存并关闭**&#x200B;确认更改。

>[!NOTE]
>
>有关发布环境中用户档案以及提供登录和退出表单的信息，请参阅[Identity Management](/help/sites-administering/identity-management.md)。

## 链接到CUG页面 {#linking-to-the-cug-pages}

由于指向CUG页面的任何链接的目标对匿名用户不可见，因此linkchecker将删除此类链接。

要避免出现这种情况，建议您创建指向CUG区域内的页面的无保护重定向页面。 然后呈现导航条目，而不会导致linkchecker出现任何问题。 仅当实际访问重定向页面时，用户才会在CUG区域中被重定向 — 在成功提供其登录凭据之后。

## 为CUG配置Dispatcher {#configure-dispatcher-for-cugs}

如果您使用的是Dispatcher，则需要使用以下属性定义Dispatcher场：

* [virtualhosts](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts)：与CUG应用于的页面的路径匹配。
* \sessionmanagement：请参见下文。
* [cache](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache)： CUG所应用文件的专用缓存目录。

### 为CUG配置Dispatcher会话管理 {#configuring-dispatcher-session-management-for-cugs}

在dispatcher.any文件](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement)中为CUG配置[会话管理。 在请求访问CUG页面时使用的身份验证处理程序决定了如何配置会话管理。

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>当Dispatcher场启用了会话管理时，不会缓存场处理的所有页面。 要缓存超出CUG的页面，请在dispatcher.any中创建第二个场
>处理非CUG页面。

1. 通过定义`/directory`配置[/sessionmanagement](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement)；例如：

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. 将[/allowAuthorized](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#caching-when-authentication-is-used)设置为`0`。
