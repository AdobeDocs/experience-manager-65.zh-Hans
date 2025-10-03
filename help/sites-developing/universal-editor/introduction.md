---
title: 通用编辑器
description: 了解通用编辑器的灵活性，以及它如何帮助您在 AEM 6.5 中驱动 Headless 体验。
feature: Developing
role: Developer
exl-id: 7bdf1fcc-02b9-40bc-8605-e6508a84d249
source-git-commit: 9f91063e51aa599ef48967f832aa359ecf100fc2
workflow-type: ht
source-wordcount: '1183'
ht-degree: 100%

---


# 通用编辑器 {#universal-editor}

了解通用编辑器的灵活性，以及它如何帮助您在 AEM 6.5 中驱动 Headless 体验。

## 概述 {#overview}

通用编辑器是一个多功能可视化编辑器，是 Adobe Experience Manager Sites 的一部分。它使作者能够对任何 Headless 体验进行所见即所得（WYSIWYG）编辑。

* 作者可从通用编辑器的灵活性中受益，因为它为所有形式的 AEM Headless 内容提供相同、一致的可视化编辑体验。
* 开发人员同样能够从通用编辑器的多样性中获益，因为它还支持对实施的真正解耦。它允许开发人员使用他们选择的几乎任何框架或架构，而不会施加任何 SDK 或技术限制。

请参阅 [AEM as a Cloud Service 文档中有关通用编辑器的章节](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)，以了解更多详细信息。

## 架构 {#architecture}

通用编辑器是一项与 AEM 协同工作的服务，用于以 Headless 方式创作内容。

* 通用编辑器托管在 `https://experience.adobe.com/#/aem/editor/canvas` 中，可编辑由 AEM 6.5 渲染的页面。
* 通用编辑器通过 Dispatcher 从 AEM 作者实例中读取 AEM 页面。
* 运行在与 Dispatcher 相同的主机上的通用编辑器服务会将更改写回 AEM 作者实例。

![使用通用编辑器的创作流程](assets/author-flow.png)

## 要求 {#requirements}

通用编辑器受到以下环境支持：

* AEM 6.5
   * 支持本地部署和 AMS 托管。
* [AEM 6.5 LTS](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)
   * 支持本地部署和 AMS 托管。
* [AEM as a Cloud Service](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)

本文档重点介绍 AEM 6.5 对通用编辑器的支持。要在 AEM 6.5 中使用通用编辑器，您需要：

* 安装了服务包 23 或更高版本的 AEM 6.5
   * 服务包 21 和 22 也受支持，但需搭配[功能包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-6.5.21-universal-editor-1.0.0.zip)使用。
* 正确配置 Dispatcher

## 设置 {#setup}

要测试通用编辑器，您需要：

1. [设置本地通用编辑器服务。](#set-up-ue)
1. [调整 Dispatcher 以允许使用通用编辑器服务。](#update-dispatcher)

完成设置后，您即可[对应用程序进行接入配置，以使用通用编辑器。](#instrumentation)

### 配置服务 {#configure-services}

通用编辑器使用了若干需要额外配置的包。

#### 为 `login-token` cookie 设置 SameSite 属性。 {#samesite-attribute}

1. 打开配置管理器。
   * `http://<host>:<port>/system/console/configMgr`
1. 在列表中找到 **Adobe Granite 令牌身份验证处理程序**，并点击&#x200B;**更改配置值**。
1. 在对话框中，**将 login-token cookie 的 SameSite 属性**（`token.samesite.cookie.attr`）值修改为 `Partitioned`。
1. 单击&#x200B;**保存**。

#### 移除 `SAMEORIGIN` 标头中的 X-Frame 选项。 {#sameorigin}

1. 打开配置管理器。
   * `http://<host>:<port>/system/console/configMgr`
1. 在列表中找到 **Apache Sling Main Servlet**，并点击&#x200B;**编辑配置值**。
1. 如果存在，请从`X-Frame-Options=SAMEORIGIN` 附加响应标头&#x200B;**属性（**）中删除 `sling.additional.response.headers` 值。
1. 单击&#x200B;**保存**。

#### 配置 Adobe Granite 查询参数身份验证处理程序。 {#query-parameter}

1. 打开配置管理器。
   * `http://<host>:<port>/system/console/configMgr`
1. 在列表中找到 **Adobe Granite 查询参数身份验证处理程序**，并点击&#x200B;**编辑配置值**。
1. 在&#x200B;**路径**&#x200B;字段（`path`）中，添加 `/` 以启用。
   * 如果该字段为空，则会禁用此身份验证处理程序。
1. 单击&#x200B;**保存**。

#### 定义应为哪些内容路径或 `sling:resourceTypes` 打开通用编辑器。 {#paths}

1. 打开配置管理器。
   * `http://<host>:<port>/system/console/configMgr`
1. 在列表中找到&#x200B;**通用编辑器 URL 服务**，然后点击&#x200B;**编辑配置值**。
1. 定义应为哪些内容路径或 `sling:resourceTypes` 打开通用编辑器。
   * 在&#x200B;**通用编辑器打开映射**&#x200B;字段中，提供通用编辑器为其打开的路径。
   * 在通用编辑器打开的 **Sling:resourceTypes**&#x200B;字段中，提供通用编辑器直接打开的一个资源列表。
1. 单击&#x200B;**保存**。
1. 检查您的[外部化器配置](/help/sites-developing/externalizer.md)，确保至少已设置了本地、作者和发布三个环境，如下例所示。

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

完成这些配置步骤后，AEM 将按以下顺序为页面打开通用编辑器。

1. AEM 会检查 `Universal Editor Opening Mapping` 中的映射，如果内容位于那里定义的任何路径下，就会为其打开通用编辑器。
1. 如果内容不位于 `Universal Editor Opening Mapping` 中定义的路径下，AEM 会检查此内容的 `resourceType` 是否与通用编辑器打开的 **Sling:resourceTypes 中定义的类型匹配**，如果内容与其中一个类型匹配，就会在 `${author}${path}.html` 上为其打开通用编辑器。
1. 否则，AEM 就打开页面编辑器。

在 `Universal Editor Opening Mapping` 中，可使用以下变量来定义映射：

* `path`：要打开的资源的内容路径
* `localhost`：没有架构的用于 `localhost` 的外部化器条目，例如 `localhost:4502`
* `author`：没有架构的用于作者的外部化器条目，例如 `localhost:4502`
* `publish`：没有架构的用于发布的外部化器条目，例如 `localhost:4503`
* `preview`：没有架构的用于预览的外部化器条目，例如 `localhost:4504`
* `env`：`prod`、`stage`、`dev` 基于已定义的 Sling 运行模式
* `token`：`QueryTokenAuthenticationHandler` 需要查询令牌

映射示例：

* 打开 AEM 作者上 `/content/foo` 下的所有页面：
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * 这会打开 `https://localhost:4502/content/foo/x.html?login-token=<token>`
* 打开远程 NextJS 服务器上 `/content/bar` 下的所有页面，提供所有变量的信息
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * 这会打开 `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

### 设置通用编辑器服务 {#set-up-ue}

在更新并配置好 AEM 后，您可以为本地开发和测试搭建本地通用编辑器服务。

1. 安装 Node.js 版本 >=20。
1. 从[软件分发](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud/software-distribution/home)下载并解压最新的通用编辑器服务
1. 通过环境变量或 `.env` 文件配置通用编辑器服务。
   * [有关详细信息，请参阅 AEM as a Cloud Service 通用编辑器文档。](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * 请注意，如果需要重写内部 IP，可能需要使用 `UES_MAPPING` 选项。
1. 运行 `universal-editor-service.cjs`

### 更新 Dispatcher {#update-dispatcher}

在完成 AEM 配置并运行本地 Universal Editor Service 后，您需要[在 Dispatcher](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-dispatcher/using/dispatcher) 中允许该新服务的反向代理。

1. 修改作者实例的 vhost 文件以包含反向代理。

   ```html
   <IfModule mod_proxy.c>
    ProxyPass "/universal-editor" "http://localhost:8080"
    ProxyPassReverse "/universal-editor" "http://localhost:8080"
   </IfModule>
   ```

   >[!NOTE]
   >
   >默认端口为 8080。如果在[您的 `.env` 文件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)中通过 `UES_PORT` 参数更改了端口值，则必须在此处相应调整。

1. 重新启动 Apache。

## 对应用进行接入配置 {#instrumentation}

在更新 AEM 并运行本地通用编辑器服务后，您可以开始使用通用编辑器编辑 Headless 内容。

但是，您的应用程序必须进行接入配置才能充分利用通用编辑器。这需要在页面中添加元标记，以指示编辑器如何以及在何处对内容进行持久化。有关此接入配置的详细信息，请参阅 [AEM as a Cloud Service 的通用编辑器文档。](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)

请注意，在参考 AEM as a Cloud Service 的通用编辑器文档时，如果使用 AEM 6.5，则需进行以下调整：

* 元标记中的协议必须为 `aem65`，而不是 `aem`。

  ```html
  <meta name="urn:adobe:aue:system:aemconnection" content={`aem65:${getAuthorHost()}`}/>
  ```

* 必须通过元标记来声明通用编辑器服务的端点。

  ```html
  <meta name="urn:adobe:aue:config:service" content={`${getAuthorHost()}/universal-editor`}/>
  ```

* 在组件定义的 `plugins` 部分中，必须使用 `aem65` 而不是 `aem`。

>[!TIP]
>
>如需完整的开发人员入门指南，请参阅 AEM as a Cloud Service 文档中的[《面向 AEM 开发人员的通用编辑器概述》](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview)，同时注意本节中提到的针对 AEM 6.5 支持所需进行的调整。

## AEM 6.5 与 AEM as a Cloud Service 的差异 {#differences}

AEM 6.5 中的通用编辑器在整体上与 AEM as a Cloud Service 的工作方式相同，其中包括用户界面和大部分配置。但仍有一些差异需要注意。

* 在 6.5 中，通用编辑器仅支持 Headless 用例。
* 在 6.5 中，通用编辑器的设置略有不同（如当前文档[所述](#setup)）。
* 在 6.5 中，通用编辑器使用的资产选择器和内容片段选择器与 AEM as a Cloud Service 不同。
