---
title: 开发工具
description: 要开发JCR、Apache Sling或Adobe Experience Manager应用程序，可以使用多个工具集。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 97310ed5-f8fb-416c-8a66-68f652abeaa0
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 17%
---
# 开发工具{#development-tools}

要开发JCR、Apache Sling或Adobe Experience Manager (AEM)应用程序，可以使用以下工具集：

* 由[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)和WebDAV组成的集。 CRXDE Lite已嵌入到CRX/AEM中，使您能够在该浏览器中执行标准开发任务。 使用CRXDE Lite，您可以在日志记录和与SVN集成时创建和编辑文件(如.jsp和.java)、文件夹、模板、组件、对话框、节点、属性和捆绑包。

  在以下情况下，建议您使用CRXDE Lite：无法直接访问CRX/AEM服务器；通过扩展或修改现成组件和Java™捆绑包来开发应用程序；不需要专用调试器、代码完成和语法高亮显示。

* 一组包含以下内容：
  * 集成开发环境。 例如，[Eclipse](/help/sites-developing/howto-projects-eclipse.md)或[IntelliJ](/help/sites-developing/ht-intellij.md)。
  * 构建工具。 例如，[Apache Maven](/help/sites-developing/ht-projects-maven.md)。
  * FileVault ，由Adobe开发，用于将存储库映射到文件系统（版本控制系统）。 例如，Subversion。
  * 错误跟踪器系统。 例如，Jira。
  * 一种中央依赖性管理系统。 例如，Apache Archiva。
  * 以及构建自动化系统。 例如，Apache Continuum。

  通过此设置，您可以将应用程序（内容、代码、配置）完全集成到任何开发环境和流程中。 不同元素之间的链接是通过FileVault表示存储库的文件系统，因为前面提到的所有开发工具都可以处理文件。

## 集成开发环境的扩展 {#extensions-for-integrated-development-environments}

Adobe发布了以下扩展：

* [AEM Eclipse扩展](/help/sites-developing/aem-eclipse.md)
* [AEM Brackets 扩展](/help/sites-developing/aem-brackets.md)

### 其他工具 {#other-tools}

AEM附带了其他有助于开发的工具：

* [对话框编辑器](/help/sites-developing/dialog-editor.md)
* [使用 Translator 管理词典](/help/sites-developing/i18n-translator.md)
* [使用 Maven 管理包](/help/sites-developing/vlt-mavenplugin.md)
* [如何使用 Eclipse 开发 AEM 项目](/help/sites-developing/howto-projects-eclipse.md)
* [如何使用 Apache Maven 构建 AEM 项目](/help/sites-developing/ht-projects-maven.md)
* [如何使用 IntelliJ IDEA 开发 AEM 项目](/help/sites-developing/ht-intellij.md)
* [如何使用 VLT 工具](/help/sites-developing/ht-vlttool.md)
* [如何使用代理服务器工具](/help/sites-developing/ht-proxy-server.md)
* [AEM 现代化工具](/help/sites-developing/modernization-tools.md)
* [AEM Repo 工具](/help/sites-developing/aem-repo-tool.md)

有助于创建新项目的工具：

* [AEM 项目原型模板](https://github.com/adobe/aem-project-archetype)
* [AEM Lazybone模板](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>以下教程可能对启动新的AEM项目有帮助：
>[AEM Sites快速入门第1部分 — 项目设置](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
