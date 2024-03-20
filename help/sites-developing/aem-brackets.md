---
title: AEM Brackets扩展
description: 了解如何使用Brackets的Adobe Experience Manager扩展。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 829d8256-b415-4a44-a353-455ac16950f3
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# AEM Brackets扩展{#aem-brackets-extension}

## 概述 {#overview}

AEM Brackets扩展提供了一个流畅的工作流，用于编辑AEM组件和客户端库，并利用了 [括号](https://brackets.io/) 代码编辑器，允许从代码编辑器访问Photoshop文件和图层。 扩展提供的轻松同步（不需要Maven或File Vault）提高了开发人员效率，并且还有助于掌握有限AEM知识的前端开发人员参与项目。 此扩展还为 [HTML模板语言(HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)这样可以降低JSP的复杂性，使组件开发更容易、更安全。

![chlimage_1-53](assets/chlimage_1-53a.png)

### 功能 {#features}

AEM Brackets扩展的主要功能包括：

* 将更改的文件自动同步到AEM开发实例。
* 手动双向同步文件和文件夹。
* 项目的完整内容包同步。
* 表达式和的HTL代码完成 `data-sly-*` 块语句。

此外，Brackets还为AEM前端开发人员提供了许多有用的功能：

* Photoshop文件支持从PSD文件中提取信息，如图层、测量、颜色、字体、文本等。
* 来自PSD的代码提示，可轻松地在代码中重用此提取的信息。
* CSS预处理程序支持，如LESS和SCSS。
* 以及数百种其他扩展，可满足更具体的需求。

## 安装 {#installation}

### 括号 {#brackets}

AEM Brackets扩展支持Brackets版本1.0或更高版本。

从下载最新的Brackets版本 [brackets.io](https://brackets.io/).

### 扩展 {#the-extension}

要安装扩展，请按照以下步骤操作：

1. 打开方括号。 在菜单中 **文件**，选择 **Extension Manager...**
1. 输入 **AEM** 在搜索栏中查找 **AEM Brackets扩展**.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. 单击 **安装**.
1. 关闭对话框，并在安装完成后Extension Manager。

## 快速入门 {#getting-started}

### 内容包项目 {#the-content-package-project}

安装扩展后，您可以通过使用Brackets从文件系统打开content-package文件夹来开始开发AEM组件。

项目必须至少包含：

1. a `jcr_root` 文件夹(例如， `myproject/jcr_root`)

1. a `filter.xml` 文件(例如， `myproject/META-INF/vault/filter.xml`)；以获取有关架构的更多详细信息 `filter.xml` 文件请参阅 [工作区筛选器定义](https://jackrabbit.apache.org/filevault/filter.html).

在括号中 **文件** 菜单，选择 **打开文件夹……** 然后选取 `jcr_root` 文件夹或父项目文件夹。

>[!NOTE]
>
>如果您没有自己的包含内容包的项目，则可以尝试 [HTL TodoMVC示例](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc). 在GitHub上，单击 **下载ZIP**，在本地提取文件，并按照以上说明，打开 `jcr_root` Brackets中的文件夹。 然后按照以下步骤设置 **项目设置**，最后通过将整个包上传到您的AEM开发实例 **导出内容包** 如完整内容包同步一节中进一步说明的那样。
>
>完成这些步骤后，您应该能够访问 `/content/todo.html` AEM开发实例上的URL，您可以开始在Brackets中修改代码，并了解在Web浏览器中刷新后，更改如何立即同步到AEM服务器。

### 项目设置 {#project-settings}

要将内容与AEM开发实例同步以及从中同步内容，您需要定义项目设置。 这可以通过转到 **AEM** 菜单和选择 **项目设置……**

![chlimage_1-55](assets/chlimage_1-55a.png)

通过“项目设置”，可定义以下内容：

1. 服务器URL(例如， `http://localhost:4502`)
1. 是否容忍没有有效HTTPS证书的服务器（除非需要，否则保持未选中状态）
1. 用于同步内容的用户名(例如， `admin`)
1. 用户的密码(例如， `admin`)

## 同步内容 {#synchronizing-content}

AEM Brackets扩展为文件和文件夹提供了以下类型的内容同步，这些同步由中定义的筛选规则允许 `filter.xml`：

### 已更改文件的自动同步 {#automated-synchronization-of-changed-files}

这只能将更改从Brackets同步到AEM实例，反之则不行。

### 手动双向同步 {#manual-bidirectional-synchronization}

在项目资源管理器中，通过右键单击任何文件或文件夹，以及 **导出到服务器** 或 **从服务器导入** 选项可供访问。

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>如果所选条目在 `jcr_root` 文件夹， **导出到服务器** 和 **从服务器导入** 上下文菜单条目被禁用。

### 完整内容包同步 {#full-content-package-synchronization}

在 **AEM** 菜单， **导出内容包** 或 **导入内容包** 选项允许您将整个项目与服务器同步。

![chlimage_1-57](assets/chlimage_1-57a.png)

### 同步状态 {#synchronization-status}

AEM Brackets扩展的Brackets窗口右侧的工具栏中提供了一个通知图标，用于指示上次同步的状态：

* 绿色 — 已成功同步所有文件
* 蓝色 — 正在进行同步操作
* 黄色 — 某些文件未同步
* 红色 — 未同步任何文件

单击通知图标会打开“同步状态报告”对话框，其中列出了每个已同步文件的所有状态。

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>仅限由以下项的筛选规则标记为包含的内容： `filter.xml` 将进行同步，无论使用的同步方法如何。
>
>此外， `.vltignore` 支持文件来阻止内容与存储库进行同步以及从存储库进行同步。

## 编辑HTL代码 {#editing-htl-code}

AEM Brackets扩展还提供了一些自动完成功能，以便于HTL属性和表达式的编写。

### 属性自动完成 {#attribute-auto-completion}

1. 在HTML属性中，键入 `sly`. 该属性会自动填写到 `data-sly-`.
1. 在下拉列表中选择HTL属性。

### 表达式自动完成 {#expression-auto-completion}

在表达式中 `${}`，常用变量名称会自动填写。

## 更多信息 {#more-information}

AEM Brackets扩展是一个开源项目，由 [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud) 组织，在Apache许可证版本2.0下：

* 代码存储库： [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Apache许可证，版本2.0： [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

Brackets代码编辑器也是一个开源项目，由 [Adobe Systems Incorporated](https://github.com/adobe) 组织：

* 代码存储库： [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

欢迎您投稿！
