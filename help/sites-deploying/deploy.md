---
title: 部署和维护
description: 了解如何开始安装AEM。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '1779'
ht-degree: 3%

---

# 部署和维护{#deploying-and-maintaining}

在此页中，您可以找到：

* [基本概念](#basic-concepts)

   * [什么是AEM？](#what-is-aem)
   * [典型部署](#typical-deployment-scenarios)

      * [内部部署](#on-premise)
      * [使用Cloud Manager的Managed Services](#managed-services-using-cloud-manager)

* [快速入门](#getting-started)

   * [先决条件](#prerequisites)
   * [获取软件](#getting-the-software)
   * [默认本地安装](#default-local-install)
   * [创作和发布安装](#author-and-publish-installs)
   * [解压缩的安装目录](#unpacked-install-directory)
   * [启动和停止](#starting-and-stopping)

熟悉这些基础知识后，您便可以在以下子页面中找到更高级和详细的信息：

* [技术要求](/help/sites-deploying/technical-requirements.md)
* [建议的部署](/help/sites-deploying/recommended-deploys.md)
* [自定义独立安装](/help/sites-deploying/custom-standalone-install.md)
* [应用程序服务器安装](/help/sites-deploying/application-server-install.md)
* [疑难解答](/help/sites-deploying/troubleshooting.md)
* [命令行启动和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [配置 ](/help/sites-deploying/configuring.md)
* [升级到AEM 6.5](/help/sites-deploying/upgrade.md)
* [电子商务](/help/commerce/cif-classic/deploying/ecommerce.md)
* [配置操作方法文章](/help/sites-deploying/ht-deploy.md)
* [Web 控制台](/help/sites-deploying/web-console.md)
* [排查复制问题](/help/sites-deploying/troubleshoot-rep.md)
* [最佳实践](/help/sites-deploying/best-practices.md)
* [部署社区](/help/communities/deploy-communities.md)
* [AEM平台简介](/help/sites-deploying/platform.md)
* [性能准则](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile快速入门](/help/mobile/getting-started-aem-mobile.md)
* [什么是AEM Screens？](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html)

## 基本概念 {#basic-concepts}

### 什么是AEM？ {#what-is-aem}

Adobe Experience Manager是一个基于Web的客户端 — 服务器系统，用于构建、管理和部署商业网站及相关服务。 它将多个基础架构级别和应用程序级别的功能合并到一个集成软件包中。

在基础架构级别，AEM提供以下功能：

* **Web应用程序服务器**： AEM可以独立模式部署（包括集成的Jetty Web服务器），也可以部署为第三方应用程序服务器中的Web应用程序。
* **Web应用程序框架**： AEM集成了Sling Web应用程序框架，该框架简化了RESTful、面向内容的Web应用程序的编写。
* **内容存储库**： AEM包含一个Java™内容存储库(JCR)，这是一种专门针对非结构化数据和半结构化数据而设计的分层数据库。 存储库不仅存储面向用户的内容，还存储应用程序使用的所有代码、模板和内部数据。

在此基础上，AEM还提供了若干应用程序级别的功能，用于管理：

* **网站**
* **移动设备应用程序**
* **数字出版物**
* **Forms和文档**
* **数字Assets**
* **社区**
* **联机Commerce**

最后，客户可以使用这些基础架构和应用程序级别的构建块，通过构建自己的应用程序来创建自定义解决方案。

AEM服务器基于&#x200B;**Java**，并且在支持该平台的大多数操作系统上运行。 所有客户端与AEM的交互均通过&#x200B;**Web浏览器**&#x200B;完成。

>[!NOTE]
>
>AEM 6.5 QuickStart中提供的自适应Forms功能仅供探索和评估之用。 由于自适应表单功能需要适当的许可，因此必须获得 AEM Forms 的有效许可证才能作生产用途。

### 典型部署方案 {#typical-deployment-scenarios}

在AEM术语中，“实例”是在服务器上运行的AEM的副本。 AEM安装通常至少涉及两个实例，通常在不同计算机上运行：

* **作者**：用于创建、上载和编辑内容以及管理网站的AEM实例。 内容准备好上线后，即会复制到发布实例。
* **发布**：一个向公众提供已发布内容的AEM实例。

这些实例在安装软件方面是相同的。 它们仅通过配置进行区分。 此外，大多数安装都使用Dispatcher：

* **Dispatcher**：通过AEM Dispatcher模块增强的静态Web服务器(Apache httpd®Microsoft、IIS等)。 它缓存由发布实例生成的网页以提高性能。

虽然此设置提供了许多高级选项和说明，但大多数部署的核心是创作、发布和Dispatcher的基本模式。 让我们从简单的设置开始。 随后将讨论高级部署选项。

以下各节描述了这两种情况：

* **内部部署**：在您的公司环境中部署并管理AEM。

* **Managed Services — 适用于Adobe Experience Manager的Cloud Manager**：由Adobe Managed Services部署和管理的AEM。

### 内部部署 {#on-premise}

您可以在公司环境中的服务器上安装AEM。 典型安装实例包括：开发、测试和发布环境。 有关如何获取AEM软件以便在本地安装的基本详细信息，请参阅[快速入门](/help/sites-deploying/deploy.md#getting%20started)。

若要了解有关典型内部部署的更多信息，请参阅[推荐的部署](/help/sites-deploying/recommended-deploys.md)。

### 使用Cloud Manager的Managed Services {#managed-services-using-cloud-manager}

AEM Managed Services是数字体验管理的完整解决方案。 它提供了云中体验交付解决方案的优势，同时保留了内部部署的所有控制、安全和自定义优势。 AEM Managed Services通过在云中部署并借鉴Adobe的最佳实践和支持，使客户能够更快地启动。 组织和企业用户可以在最短的时间内吸引客户、提高市场份额并专注于创建创新的营销活动，同时减轻IT负担。

通过AEM Managed Services，客户可以实现以下优势：

**加快上市时间：**&#x200B;利用Adobe Managed Services的灵活云基础架构，组织可以快速规划、启动和优化成功的数字体验。 Adobe无需额外资金、硬件或软件即可管理云架构，而Adobe的客户解决方案工程师可协助完成AEM架构、配置、连接到后端应用程序的自定义操作以及上线最佳实践。

**更高的性能：**&#x200B;通过四个服务可用性选项（99.5%、99.9%、99.95%和99.99%），为您的企业提供可靠的数字体验。 此外，它还支持自动备份和多模式灾难恢复模式，以帮助确保可靠性和应急管理。

**优化的IT成本：**&#x200B;主动指导和专业知识可帮助组织及时了解最新版本的AEM。 Adobe Platinum维护和支持自动包含在AMS Enterprise/Basic的新部署中，提供技术专业知识和操作经验以帮助企业维护其任务关键型应用程序。 免费的基本Analytics或Target功能可提供附加价值，尤其是对于分析和个性化需求有限的中端市场组织。

**最高安全性：**&#x200B;通过在受限访问设施、防火墙系统后面或虚拟专用云中托管客户应用程序，确保企业级物理、网络和数据安全性。 它包括具有强健的数据存储加密、防病毒和数据隔离的单租户虚拟机。

**Cloud Manager**： Cloud Manager是Adobe Experience Manager Managed Services产品的一部分，它是一个自助服务门户，进一步使组织能够在云中自行管理Adobe Experience Manager。 它包含一流的持续集成和持续交付(CI/CD)管道，使IT团队和实施合作伙伴能够在不影响性能或安全性的情况下加速自定义项或更新的交付。 Cloud Manager仅适用于Adobe Managed Service客户。

要了解有关Cloud Manger及其资源的更多信息，请参阅&#x200B;[**Cloud Manager用户指南**](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)。

## 快速入门 {#getting-started}

### 先决条件 {#prerequisites}

虽然生产实例在运行官方支持的操作系统的专用计算机上运行（请参阅[技术要求](/help/sites-deploying/technical-requirements.md)），但Experience Manager服务器实际上将在支持&#x200B;[**Java™ Standard Edition 8**](https://www.oracle.com/java/technologies/downloads/#java8)的任何系统上运行。

为了熟悉和开发AEM，通常使用安装在运行Apple OS X或Microsoft®Windows或Linux®桌面版本的本地计算机上的实例。

在客户端，AEM可与桌面和平板电脑操作系统上的所有现代浏览器(**Microsoft® Edge**、**Internet Explorer** 11、**Chrome **51+** **、**Firefox **47+、**Safari** 8+)配合使用。 有关详细信息，请参阅[支持的客户端平台](/help/sites-deploying/technical-requirements.md#supported-client-platforms)。

### 获取软件 {#getting-the-software}

持有有效维护和支持合同的客户应该已收到一封包含代码的邮件通知，并能够从&#x200B;[**Adobe授权网站**](https://licensing.adobe.com/)下载AEM。 业务合作伙伴可以从&#x200B;[**spphelp@adobe.com**](mailto:spphelp@adobe.com)&#x200B;请求下载访问权限。

AEM软件包有两种形式：

* **cq-quickstart-6.5.0.jar：**&#x200B;独立的可执行文件&#x200B;*jar*，其中包含运行所需的一切。

* **cq-quickstart-6.5.0.war：**&#x200B;在第三方应用程序服务器中部署的&#x200B;*war*&#x200B;文件。

在以下部分中，我们介绍了&#x200B;**独立安装**。 有关在应用程序服务器中安装AEM的详细信息，请参阅[应用程序服务器安装](/help/sites-deploying/application-server-install.md)。

### 默认本地安装 {#default-local-install}

1. 在本地计算机上创建一个安装目录。 例如：

   UNIX®安装位置： **/opt/aem**

   Windows安装位置： **`C:\Program Files\aem`**

   同样，将示例实例直接安装在桌面上的文件夹中也很常见。 无论如何，Adobe通常将此位置称为：

   `<aem-install>`

   *文件目录的路径只能包含美国ASCII字符。*

1. 将&#x200B;**jar**&#x200B;和&#x200B;**license**&#x200B;文件放置在此目录中：

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   如果您未提供`license.properties`文件，AEM会将您的浏览器重定向到启动时的&#x200B;**欢迎**&#x200B;屏幕，您可以在其中输入许可证密钥。 如果您还没有许可证密钥，则需要向Adobe请求有效的许可证密钥。

1. 要在GUI环境中启动实例，请双击&#x200B;**`cq-quickstart-6.5.0.jar`**&#x200B;文件。

   或者，您可以从命令行启动AEM：

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM需要几分钟时间来解压缩jar文件、安装自身并启动。 上述过程会导致：

* **AEM作者**&#x200B;实例
* 正在&#x200B;**localhost**&#x200B;上运行
* 在端口&#x200B;**4502**&#x200B;上

要访问该实例，请将浏览器指向：

**`https://localhost:4502`**

创作实例中的结果将自动配置为连接到&#x200B;**`localhost:4503`**&#x200B;上的&#x200B;**发布实例**。

### 创作和发布安装 {#author-and-publish-installs}

只需在首次启动`jar`文件之前重命名该文件，即可更改默认安装（**`localhost:4502`**&#x200B;上的&#x200B;**作者**&#x200B;实例）。 命名模式为：

**`cq-<instance-type>-p<port-number>.jar`**

例如，将文件重命名为

**`cq-author-p4502.jar`**

然后启动它，将在&#x200B;**`localhost:4502`**&#x200B;上运行创作实例。

同样，重命名和启动文件

**`cq-publish-p4503.jar`**

结果发布实例在&#x200B;**`localhost:4503`**&#x200B;上运行。

例如，您需要在中安装这两个实例

`<aem-install>/author`和

**`<aem-install>/publish`**

有关自定义安装的更多详细信息，请参阅以下内容：

* [自定义独立安装](/help/sites-deploying/custom-standalone-install.md)
* [运行模式](/help/sites-deploying/configure-runmodes.md)

### 解压缩的安装目录 {#unpacked-install-directory}

首次启动快速入门jar时，它会将其自身解压缩到名为`crx-quickstart`的新子目录下的同一目录中。 您应该拥有以下权限：

```xml
<aem-install>/
    license.properties
    cq-quickstart-6.5.0.jar
    crx-quickstart/
        app/
        bin/
        conf/
        launchpad/
        logs/
        metrics/
        monitoring/
        opt/
        repository/
        threaddumps/
        eula-de_DE.html
        eula-en_US.html
        eula-fr_FR.html
        eula-ja_JP.html
        readme.txt
```

如果实例是从UI安装的，则将自动打开一个浏览器窗口，并且还会打开一个桌面应用程序窗口，其中显示实例的主机和端口以及一个开/关开关：

![启动屏幕](assets/screen_shot_.png)

### 启动和停止 {#starting-and-stopping}

当AEM自行解压缩并首次启动后，双击安装目录中的jar文件即可启动实例，它不会重新安装。

若要从GUI停止实例，请单击桌面应用程序窗口上的&#x200B;**打开/关闭**&#x200B;开关。

您还可以从命令行停止和启动AEM。 假设您已经首次安装实例，**命令行脚本**&#x200B;如下所示：

**`<aem-install>/crx-quickstart/bin/`**

此文件夹包含以下UNIX® bash shell脚本：

* **`start`**：启动实例
* `stop`：停止实例
* **`status`**：报告实例的状态
* **`quickstart`**：用于配置启动信息（如有必要）。

还有等效的&#x200B;**`bat`**&#x200B;个用于Windows的文件。 有关更多详细信息，请参阅：

* [命令行启动和停止](/help/sites-deploying/command-line-start-and-stop.md)

AEM启动，并自动将Web浏览器重定向到相应的页面（通常是登录页面）；例如：

`https://localhost:4502/`

![登录屏幕](assets/screen_shot_2019-04-08at83533am.png)

登录后，您可以访问AEM。 有关详细信息，请参阅以下内容，具体取决于您的角色：

* [创作](/help/sites-authoring/first-steps.md)
* [管理 ](/help/sites-administering/home.md)
* [开发](/help/sites-developing/getting-started.md)
* [管理](/help/managing/best-practices.md)

## 高级部署 {#advanced-deployment}

通过上部分，您应该能够很好地了解AEM安装的基础知识。 但是，安装AEM的完整生产系统可能会涉及更大的复杂性。 有关高级安装的完整介绍，请参阅以下子页面：

* [技术要求](/help/sites-deploying/technical-requirements.md)
* [建议的部署](/help/sites-deploying/recommended-deploys.md)
* [自定义独立安装](/help/sites-deploying/custom-standalone-install.md)
* [应用程序服务器安装](/help/sites-deploying/application-server-install.md)
* [疑难解答](/help/sites-deploying/troubleshooting.md)
* [命令行启动和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [配置 ](/help/sites-deploying/configuring.md)
* [升级到AEM 6.5](/help/sites-deploying/upgrade.md)
* [电子商务](/help/commerce/cif-classic/deploying/ecommerce.md)
* [配置操作方法文章](/help/sites-deploying/ht-deploy.md)
* [Web 控制台](/help/sites-deploying/web-console.md)
* [排查复制问题](/help/sites-deploying/troubleshoot-rep.md)
* [最佳实践](/help/sites-deploying/best-practices.md)
* [部署社区](/help/communities/deploy-communities.md)
* [AEM平台简介](/help/sites-deploying/platform.md)
* [性能准则](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile快速入门](/help/mobile/getting-started-aem-mobile.md)
* [什么是AEM Screens？](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html)
