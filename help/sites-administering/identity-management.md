---
title: Identity Management
seo-title: Identity Management
description: 了解AEM中的身份管理。
seo-description: Learn about identity management in AEM.
uuid: d9b83cd7-c47a-41a5-baa4-bbf385d13bfd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 994a5751-7267-4a61-9bc7-01440a256c65
docset: aem65
exl-id: acb5b235-523e-4c01-9bd2-0cc2049f88e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 7%

---

# Identity Management{#identity-management}

只有在您为网站的访客提供登录功能时，才能识别他们。 您可能希望提供登录功能的原因有多种：

* [AEM Communities](/help/communities/overview.md)站点访客需要登录才能向社区发布内容。
* [已关闭的用户组](/help/sites-administering/cug.md)

   您可能需要将对您网站（或网站部分）的访问权限限制为特定访客。

* [个性化](/help/sites-administering/personalization.md) 允许访客在访问您网站的某些方面进行配置。

登录（和注销）功能由 [帐户 **用户档案**](#profiles-and-user-accounts)，其中包含有关注册访客（用户）的其他信息。 登记和授权的实际过程可能不同：

* 从网站自行注册

   A [社区站点](/help/communities/sites-console.md) 可能配置为允许访客使用其Facebook或Twitter帐户自行注册或登录。

* 从网站申请注册

   对于封闭用户组，您可以允许访客请求注册，但通过工作流强制授权。

* 从创作环境中注册每个帐户

   如果您拥有少量用户档案（无论如何都需要授权），您可以决定直接注册每个用户档案。

为了允许访客注册，可使用一系列组件和表单来收集所需的标识信息，然后收集附加（通常是可选）的用户档案信息。 注册后，还应能够检查和更新他们提交的详细信息。

可以配置或开发其他功能：

* 配置所需的任何反向复制。
* 允许用户通过使用工作流开发表单来删除其配置文件。

>[!NOTE]
>
>配置文件中指定的信息也可用于通过向用户提供目标内容 [区段](/help/sites-administering/campaign-segmentation.md) 和 [促销活动](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

## 注册Forms {#registration-forms}

A [表单](/help/sites-authoring/default-components.md#form-component) 用于收集注册信息，然后生成新帐户和用户档案。

例如，用户可以使用Geometrixx页面请求新用户档案
`http://localhost:4502/content/geometrixx-outdoors/en/user/register.html`

![注册表](assets/registerform.png)

提交请求后，将打开用户档案页面，用户可在其中提供个人详细信息。

![profilepage](assets/profilepage.png)

此外，新帐户也会显示在 [“用户”控制台](/help/sites-administering/security.md).

## 登录 {#login}

登录组件可用于收集登录信息，然后激活登录过程。

这为访客提供了 **用户名** 和 **密码**，使用 **登录** 按钮，以在输入凭据时激活登录流程。

例如，用户可以使用 **登录** Geometrixx工具栏上的选项（使用页面）：

`http://localhost:4502/content/geometrixx-outdoors/en/user/sign-in.html`

![登录](assets/login.png)

## 注销 {#logging-out}

由于有登录机制，因此也需要注销机制。 此参数可用于 **注销** 选项。

## 查看和更新配置文件 {#viewing-and-updating-a-profile}

根据您的注册表，访客在其配置文件中可能已注册信息。 他们应该能够在以后的阶段查看和/或更新此内容。 这可以通过类似的形式完成；例如，在Geometrixx中：

```
http://localhost:4502/content/geometrixx-outdoors/en/user/profile.html
```

要查看用户档案的详细信息，请单击 **我的个人资料** 的右上角；例如， `admin` 帐户：
`http://localhost:4502/home/users/a/admin/profile.form.html/content/geometrixx-outdoors/en/user/profile.html.`

您可以使用 [客户端上下文](/help/sites-administering/client-context.md) （在创作环境中，且拥有足够的权限）：

1. 打开页面；例如Geometrixx页面：

   `http://localhost:4502/cf#/content/geometrixx/en.html`

1. 单击 **我的个人资料** 中。 您将看到您当前帐户的配置文件；例如，管理员。
1. 按 **control-alt-c** 打开客户端上下文。
1. 在Client Context的左上角，单击 **加载配置文件** 按钮。

   ![](do-not-localize/loadprofile.png)

1. 从对话框窗口的下拉列表中选择其他用户档案；例如， **艾莉森·帕克**.
1. 单击&#x200B;**确定**。
1. 再次单击 **我的个人资料**. 表单将更新Alison的详细信息。

   ![profilealison](assets/profilealison.png)

1. 您现在可以使用 **编辑配置文件** 或 **更改密码** 以更新详细信息。

## 向用户档案定义添加字段 {#adding-fields-to-the-profile-definition}

您可以向用户档案定义添加字段。 例如，向Geometrixx配置文件中添加“最喜爱的颜色”字段：

1. 从“网站”控制台中，导航到Geometrixx Outdoors站点>英语>用户>我的配置文件。
1. 双击 **我的个人资料** 页面进行编辑。
1. 在 **组件** sidekick的选项卡 **表单** 中。
1. 拖动 **下拉列表** 从sidekick到表单，位于 **关于我** 字段。
1. 双击 **下拉列表** 组件以打开用于配置的对话框，然后输入：

   * **元素名称** - `favoriteColor`
   * **标题** - `Favorite Color`
   * **项目**  — 添加多种颜色作为项目

   单击&#x200B;**确定**&#x200B;进行保存。

1. 关闭页面并返回到 **网站** 控制台并激活“我的配置文件”页面。

   下次查看配置文件时，您可以选择最喜爱的颜色：

   ![阿帕夫颜色](assets/aparkerfavcolour.png)

   字段将保存在 **个人资料** 相关用户帐户的一节：

   ![阿普克克德利特](assets/aparkercrxdelite.png)

## 用户档案状态 {#profile-states}

在许多用例中，需要了解用户（或其用户档案）是否位于 *特定状态* 或不。

这包括通过以下方式在用户配置文件中定义适当的属性：

* 对用户可见且可访问
* 为每个属性定义两个状态
* 允许在定义的两种状态之间切换

这可通过以下方式完成：

* [状态提供程序](#state-providers)

   用于管理特定资产的两种状态以及两种资产之间的过渡。

* [工作流](#workflows)

   管理与状态相关的操作。

可以定义多个状态；例如，在Geometrixx中，这包括：

* 在新闻稿或注释线程上订阅（或取消订阅）通知
* 添加和删除与朋友的连接

### 状态提供程序 {#state-providers}

状态提供程序管理相关属性的当前状态以及两个可能状态之间的转换。

状态提供程序作为组件进行实施，因此可以为您的项目自定义状态提供程序。 在Geometrixx中，这些参数包括：

* 取消订阅/订阅论坛主题
* 添加/删除好友

### 工作流 {#workflows}

状态提供程序管理配置文件属性及其状态。

需要一个工作流来实施与状态相关的操作。 例如，在订阅通知时，工作流将处理实际的订阅操作；从通知取消订阅时，工作流将处理从订阅列表中删除用户。

## 配置文件和用户帐户 {#profiles-and-user-accounts}

配置文件作为[用户帐户](/help/sites-administering/user-group-ac-admin.md).

配置文件可在 `/home/users/geometrixx`:

![chlimage_1-138](assets/chlimage_1-138.png)

在标准安装（创作或发布）中，每个人都有权读取所有用户的整个配置文件信息。 每个人都是“*内置组自动包含所有现有用户和组。 无法编辑成员列表*&quot;

这些访问权限由以下通配符ACL定义：

/home每个人允许jcr:read rep:glob = &#42;/profile&#42;

这允许：

* 论坛、评论或博客帖子，以显示相应用户档案中的信息（如图标或全名）
* geometrixx配置文件页面的链接

如果此类访问不适合您的安装，则可以更改这些默认设置。

可以使用 **[访问控制](/help/sites-administering/user-group-ac-admin.md#access-right-management)** 选项卡：

![aclmanager](assets/aclmanager.png)

## 个人资料组件 {#profile-components}

一系列配置文件组件也可用于定义网站的配置文件要求。

### 检查密码字段 {#checked-password-field}

此组件为您提供了两个字段。分别用于：

* 输入密码
* 确认密码已正确输入。

使用默认设置时组件将显示为：

![dc_profiles_checkedpassword](assets/dc_profiles_checkedpassword.png)

### 个人资料 - 头像照片 {#profile-avatar-photo}

此组件为用户提供了选择和上传头像照片文件的途径。

![dc_profiles_avatarphoto](assets/dc_profiles_avatarphoto.png)

### 个人资料 - 详细名称 {#profile-detailed-name}

此组件允许用户输入详细的名称。

![dc_profiles_detailedname](assets/dc_profiles_detailedname.png)

### 个人资料性别 {#profile-gender}

此组件允许用户输入其性别。

![dc_profiles_gender](assets/dc_profiles_gender.png)
