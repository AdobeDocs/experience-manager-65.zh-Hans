---
title: AEM Content and Commerce 快速入门
description: 了解如何部署AEM内容和Commerce项目。
topics: Commerce
feature: Commerce Integration Framework
exl-id: 92b964f8-6672-4f76-8a9f-5782c3ceb83f
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 3%

---

# AEM Content and Commerce 快速入门 {#start}

要开始使用AEM Content和Commerce，您需要安装适用于AEM 6.5的AEM Content和Commerce加载项。

## 最低软件要求

需要[AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7或更高版本。

## 入门培训 {#onboarding}

AEM Content和Commerce的入门培训分为两步：

1. 安装适用于AEM 6.5的AEM Content and Commerce加载项

2. 将AEM与您的Commerce解决方案连接

### 安装适用于AEM 6.5的AEM Content and Commerce加载项 {#install-add-on}

从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)门户下载并安装适用于AEM 6.5的AEM Commerce加载项。

启动并安装所需的AEM 6.5 Service Pack。 我们建议安装最后一个可用的Service Pack。

>[!NOTE]
>
>这将由CSE为AEM Managed Service客户完成。

### 将AEM连接到您的Commerce系统 {#connect}

AEM可以连接到任何具有AEM的GraphQL端点可访问的commerce system。 这些端点通常公开可用，或者可以通过专用VPN或本地连接进行连接，具体取决于各个项目设置。

可选地，可以提供身份验证标头以使用需要身份验证的其他CIF功能。

必须调整由[AEM项目原型](https://github.com/adobe/aem-project-archetype)和已包含在[默认配置](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)中的[AEM Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)生成的项目。

将`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`中`url`的值替换为商务系统的GraphQL端点。 此配置可通过OSGI控制台或通过项目部署OSGI配置来完成。 使用不同的AEM运行模式支持用于暂存和生产系统的不同配置。

AEM Content和Commerce附加组件以及CIF核心组件同时使用AEM服务器端和客户端连接。 客户端CIF核心组件和CIF附加创作工具默认连接到`/api/graphql`。 如果需要，可以通过CIFCloud Service配置调整此设置（请参阅下文）。

CIF加载项提供了位于`/api/graphql`的GraphQL代理servlet，可以选择将其用于[本地开发](develop.md)。 对于生产部署，强烈建议通过AEM Dispatcher或其他网络层（如CDN）设置商务GraphQL端点的反向代理。

## 配置存储和目录 {#catalog}

加载项和[CIF核心组件](https://github.com/adobe/aem-core-cif-components)可用于连接到不同商务商店（或商店视图等）的多个AEM网站结构。 默认情况下，CIF加载项使用默认配置进行部署，该默认配置连接到Adobe Commerce的默认存储和目录。

可以按照以下步骤通过CIFCloud Service配置为项目调整此配置：

1. 在AEM中，转到“工具”>“Cloud Service”>“CIF配置”

2. 选择要更改的商务配置

3. 通过操作栏打开配置属性

![CIFCloud Service配置](/help/commerce/cif/assets/cif-cloud-service-config.png)

可以配置以下属性：

- GraphQL客户端 — 为商务后端通信选择配置的GraphQL客户端。 这通常应保留为默认值。
- 存储视图 — 存储视图标识符。 如果为空，则使用默认存储视图。
- GraphQL代理路径 — AEM中的GraphQL代理用于向商务后端GraphQL端点代理请求的URL路径。

  >[!NOTE]
  >
  >在大多数设置中，不能更改默认值`/api/graphql`。 只有未使用所提供的GraphQL代理的高级设置才应更改此设置。

- 启用目录UID支持 — 在商业后端GraphQL调用中启用对UID而不是ID的支持。

  >[!NOTE]
  >
  >Adobe Commerce 2.4.2中引入了对UID的支持。仅当您的Commerce后端支持版本2.4.2或更高版本的GraphQL架构时，才启用此功能。

- 目录根类别标识符 — 商店目录根的标识符（UID或ID）

  >[!CAUTION]
  >
  >从CIF核心组件版本2.0.0开始，删除了`id`的支持并将其替换为`uid`。 如果您的项目使用CIF核心组件版本2.0.0，则必须启用目录UID支持，并使用有效的类别UID作为“目录根类别标识符”。

以上所示的配置仅供参考。 项目应提供自己的配置。

有关使用多个AEM网站结构与不同商业目录组合的更复杂的设置，请参阅[Commerce多商店设置](configuring/multi-store-setup.md)教程。

## 其他资源 {#additional-resources}

- [AEM项目原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)
- [Commerce多商店设置](configuring/multi-store-setup.md)
