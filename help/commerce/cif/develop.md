---
title: 开发AEM Commerce
description: 了解如何使用AEM项目原型生成支持AEM的commerce项目。 了解如何构建项目并将其部署到本地开发环境。
topics: Commerce, Development
feature: Commerce Integration Framework
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 48479725-8b52-4ff2-a599-d20958b26ee6
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 3%

---

# 开发AEM Commerce {#develop}

根据适用于AEM的Commerce integration framework(CIF)开发AEM Commerce项目时，遵循与其他AEM项目相同的规则和最佳实践。 请先查看以下内容：

- [AEM 6.5 Developing 用户指南](/help/sites-developing/getting-started.md)
- [AEM核心概念](/help/sites-developing/the-basics.md)
- [AEM 开发 - 准则和最佳实践](/help/sites-developing/dev-guidelines-bestpractices.md)
- [如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md)

## AEM Commerce的本地开发 {#local}

建议使用本地开发环境来处理CIF项目。

>[!NOTE]
>
>以下说明可帮助您使用具有适用于AEM 6.5的CIF为AEM Commerce设置本地AEM开发环境。 如果您使用的是AEM as a Cloud Service，请参阅[AEM Commerceas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/home.html?lang=zh-Hans)文档。

适用于AEM 6.5 aka的AEM Commerce加载项。 CIF加载项也可用于本地开发，并作为AEM包提供。 可以从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下载它作为功能包。

### 所需的软件

下列内容应本地安装：

- 本地AEM 6.5
- [AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7或更高版本
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) （3.3.9或更高版本）
- [节点LTS](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### 访问CIF加载项

CIF加载项可从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下载，请搜索“AEM Commerce加载项”。

>[!TIP]
>
>确保始终使用最新的CIF加载项版本。

### 本地设置

对于使用CIF和AEM加载项进行本地CIF项目开发，请执行以下步骤：

1. 获取AEM 6.5版本并安装AEM 6.5 Service Pack。 需要AEM 6.5 Service Pack 7，但Adobe建议安装最后一个可用的Service Pack。

1. 解压缩AEM .jar以创建`crx-quickstart`文件夹，运行：

   ```bash
   java -jar <jar name> -unpack
   ```

1. 创建`crx-quickstart/install`文件夹

1. 将从软件分发门户下载的CIF附加组件所有包复制到`crx-quickstart/install`文件夹中。

>[!TIP]
>
>或者，也可以通过包管理器安装CIF附加组件包。

1. 启动AEM快速入门

通过OSGI控制台验证设置： `http://localhost:4502/system/console/osgi-installer`。 该列表应包含与CIF附加组件相关的包、内容包和OSGI配置。 确保所有捆绑包都已启动。

## 项目设置 {#project}

有两种方法可使用CIF启动AEM Commerce项目。

### 使用AEM项目原型

[AEM项目原型](https://github.com/adobe/aem-project-archetype)是引导预配置项目以开始使用CIF的主要工具。 CIF核心组件和所有必需的配置都可以在生成的项目中包含一个额外选项。

>[!TIP]
>
>使用[AEM Project Archetype 25或更高版本](https://github.com/adobe/aem-project-archetype/releases)生成项目。

有关如何生成AEM项目，请参阅AEM项目原型[使用说明](https://github.com/adobe/aem-project-archetype#usage)。 要将CIF包含在项目中，请使用`includeCommerce`选项。

例如：

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D aemVersion=6.5.5 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

CIF核心组件可以通过包括提供的`all`包在任何项目中使用，或通过使用CIF内容包和相关OSGi捆绑包在单个项目中使用。 要手动将CIF核心组件添加到项目，请使用以下依赖项：

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### 使用AEM Venia Reference Store

启动CIF项目的第二个选项是克隆并使用[AEM Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)。 AEM Venia Reference Store是一个示例参考店面应用程序，用于演示如何将CIF核心组件用于AEM。 它旨在作为一组最佳实践示例以及开发您自己的功能的潜在起点。

要开始使用Venia引用存储，只需克隆[Git存储库](https://github.com/adobe/aem-cif-guides-venia)并开始根据需要自定义项目。

>[!NOTE]
>
>Venia Reference Store项目包含AEM as a Cloud Service和AEM 6.5的两个生成配置文件。查看[项目readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md)以了解它们的使用方式。 对于AEM 6.5，使用`classic`配置文件。

### 将AEM连接到Commerce系统

要将您的项目连接到Commerce System，必须使用Commerce System的GraphQL端点配置AEM。

由[AEM项目原型](https://github.com/adobe/aem-project-archetype)或[AEM Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)生成的项目已包含必须调整的[默认配置](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)。

将`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`中`url`的值替换为项目使用的商务系统的GraphQL端点。

AEM Commerce加载项和CIF核心组件通过AEM服务器并直接通过浏览器连接到商务GraphQL端点。 默认情况下，客户端CIF核心组件和CIF附加组件创作工具连接到`/api/graphql`。 如果需要，可以通过CIFCloud Service配置来调整此设置（请参阅下文）。

CIF加载项提供了位于`/api/graphql`的GraphQL代理servlet。 如果您不打算使用本地AEM Dispatcher，则建议同时配置GraphQL代理servlet。

导航到http://localhost:4502/system/console/configMgr并为`Adobe CIF GraphQL Proxy Configuration`服务创建OSGI配置。 使用与上述用于GraphQL客户端的相同的GraphQL商务系统端点。

## 其他资源

- [AEM项目原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)
