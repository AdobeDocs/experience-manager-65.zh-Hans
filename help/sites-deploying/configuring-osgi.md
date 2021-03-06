---
title: 配置OSGi
seo-title: 配置OSGi
description: OSGi是Adobe Experience Manager(AEM)技术堆栈中的一个基本元素。 它用于控制AEM的复合包及其配置。 本文详细介绍了如何管理此类包的配置设置。
seo-description: OSGi是Adobe Experience Manager(AEM)技术堆栈中的一个基本元素。 它用于控制AEM的复合包及其配置。 本文详细介绍了如何管理此类包的配置设置。
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
feature: 配置
exl-id: 5ecd09a3-c4be-4361-9816-03106435346f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2014'
ht-degree: 0%

---

# 配置OSGi{#configuring-osgi}

[](https://www.osgi.org/) OSG是Adobe Experience Manager(AEM)技术堆栈中的一个基本元素。它用于控制AEM的复合包及其配置。

OSGi &quot;*提供了标准化基元，它允许应用程序从可重用的小组件和协作组件构建。 这些组件可以组合成应用程序并部署*&quot;。

这样可以轻松管理包，因为可以单独停止、安装和启动包。 互依关系会自动处理。 每个OSGi组件（请参阅[OSGi规范](https://www.osgi.org/Specifications/HomePage)）都包含在各种包中的一个包中。

您可以通过以下任一方式管理此类包的配置设置：

* 使用[Adobe CQ Web控制台](#osgi-configuration-with-the-web-console)
* 使用[配置文件](#osgi-configuration-with-configuration-files)
* 在存储库](#osgi-configuration-in-the-repository)中配置[content-nodes(`sling:OsgiConfig`)

虽然存在细微差异，但可以使用任一方法，主要与[运行模式](/help/sites-deploying/configure-runmodes.md)有关：

* [Adobe CQ Web控制台](#osgi-configuration-with-the-web-console)

   * Web控制台是OSGi配置的标准界面。 它提供了用于编辑各种属性的UI，在这些属性中，可以从预定义列表中选择可能的值。

      因此，这是最简单的方法。

   * 使用Web控制台进行的任何配置都将立即应用并适用于当前实例，而与当前运行模式无关，也与后续对运行模式所做的任何更改无关。

* [配置文件](#osgi-configuration-with-configuration-files)

   * 包含在Web控制台中定义的设置。
   * 可以包含在内容包中，以供在其他实例上使用。

* [存储库中的内容节点(sling:osgiConfig)](#osgi-configuration-in-the-repository)

   * 这需要使用CRXDE Lite进行手动配置。
   * 由于`sling:OsgiConfig`节点的命名约定，您可以将配置绑定到特定的[运行模式](/help/sites-deploying/configure-runmodes.md)。 您甚至可以在同一存储库中保存多个运行模式的配置。
   * 立即应用任何适当的配置（取决于运行模式）。

无论您使用哪种方法，所有这些配置方法：

* 确保复制或复制存储库内容会重新创建相同的配置。
* 允许您将配置签出到FileVault或Subversion;安全或进一步更新。
* 可以保存在包中，以便在设置其他实例时使用。
* 允许您使用脚本执行配置转出以传播配置详细信息。

>[!NOTE]
>
>某些重要设置的详细信息列在[OSGi配置设置下。](/help/sites-deploying/osgi-configuration-settings.md)

## 使用Web控制台{#osgi-configuration-with-the-web-console}进行OSGi配置

AEM中的[Web控制台](/help/sites-deploying/web-console.md)提供了用于配置包的标准化界面。 **Configuration**&#x200B;选项卡用于配置OSGi包，因此是配置AEM系统参数的基础机制。

所做的任何更改都会立即应用于相关的OSGi配置，无需重新启动。

>[!NOTE]
>
>在Web控制台中所做的更改将作为[配置文件](#osgi-configuration-with-configuration-files)保存在存储库中。 这些组件可以包含在内容包中，以供在进一步安装中重复使用。

>[!NOTE]
>
>在Web控制台中，任何提及默认设置的描述都与Sling默认值相关。
>
>Adobe Experience Manager有其自己的默认值，因此默认设置可能与控制台中记录的默认值不同。

要使用Web控制台更新配置，请执行以下操作：

1. 通过以下任一方式访问Web控制台的&#x200B;**Configuration**&#x200B;选项卡：

   * 从&#x200B;**工具 — >操作**&#x200B;菜单上的链接打开Web控制台。 登录控制台后，您可以使用下拉菜单：

      **OSGi >**

   * 直接URL;例如：

      `http://localhost:4502/system/console/configMgr`
   将显示一个列表。

1. 通过以下任一方式选择要配置的包：

   * 单击该包的&#x200B;**编辑**&#x200B;图标
   * 单击包的&#x200B;**名称**

1. 此时将打开一个对话框。您可以在此处根据需要进行编辑；例如，将&#x200B;**日志级别**&#x200B;设置为`INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >更新将作为[配置文件](#osgi-configuration-with-configuration-files)保存在存储库中。 要在之后找到这些标识（例如，要包含在内容包中以供在其他实例上使用），您应记下永久标识(`PID`)。

1. 单击&#x200B;**保存**。

   您所做的更改会立即应用于正在运行的系统的相关OSGi配置，无需重新启动。

   >[!NOTE]
   >
   >您现在可以找到相关的[配置文件](#osgi-configuration-with-configuration-files);例如，包含在内容包中以供在其他实例上使用。

## 配置文件{#osgi-configuration-with-configuration-files}的OSGi配置

使用Web控制台进行的配置更改将作为配置文件(`.config`)保留在存储库中，位于：

`/apps`

这些文件包可以包含在内容包中，并可在其他实例上重复使用。

>[!NOTE]
>
>配置文件的格式非常具体 — 有关完整的详细信息，请参阅[Sling Apache文档](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format)。
>
>因此，建议通过在Web控制台中进行实际更改来创建和维护配置文件。

Web控制台不显示您所做的更改已保存在存储库中的位置，但可以轻松找到这些更改：

1. 在Web控制台中通过[进行初始更改来创建配置文件](#osgi-configuration-with-the-web-console)。
1. 打开CRXDE Lite。
1. 在&#x200B;**工具**&#x200B;菜单中，选择&#x200B;**查询……** 。
1. 提交&#x200B;**Type** `SQL`的查询，以搜索已更新配置的PID。

   例如，**Apache Felix OSGi管理控制台**&#x200B;具有以下的永久标识(PID):

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   因此SQL查询可以是：

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. 将显示配置文件节点。

   对于上例：

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >您可以打开此文件以查看您所做的更改，但为避免键入错误，建议使用控制台进行实际更改。

1. 您现在可以构建包含此节点的内容包，并根据需要在其他实例中使用。

## 存储库{#osgi-configuration-in-the-repository}中的OSGi配置

除了使用Web控制台之外，您还可以在存储库中定义配置详细信息。 这样，您就可以轻松配置不同的运行模式。

这些配置是通过在存储库中创建`sling:OsgiConfig`节点进行的，以供系统引用。 这些节点将镜像OSGi配置，并与它们形成用户界面。 要更新配置数据，请更新节点属性。

如果修改存储库中的配置数据，则所做的更改会立即应用于相关OSGi配置，就像更改是使用Web控制台进行的一样，并进行相应的验证和一致性检查。 这也适用于将配置从`/libs/`复制到`/apps/`的操作。

由于同一配置参数可以位于多个位置，因此系统：

* 搜索类型为`sling:OsgiConfig`的所有节点
* 根据服务名称过滤
* 根据运行模式筛选

>[!NOTE]
>
>另请阅读[如何仅为特定实例定义基于存储库的配置](https://helpx.adobe.com/experience-manager/kb/RunModeDependentConfigAndInstall.html)。

### 向存储库{#adding-a-new-configuration-to-the-repository}添加新配置

#### {#what-you-need-to-know}需要了解的内容

要向存储库添加新配置，您需要了解以下信息：

1. 服务的&#x200B;**永久标识**(PID)。

   引用Web控制台中的&#x200B;**Configurations**&#x200B;字段。 该名称在包名称后面的方括号中显示（或在页面底部的&#x200B;**配置信息**&#x200B;中）。

   例如，创建一个节点`com.day.cq.wcm.core.impl.VersionManagerImpl.`以配置&#x200B;**AEM WCM版本管理器**。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 是否需要特定的[运行模式](/help/sites-deploying/configure-runmodes.md)。 创建文件夹：

   * `config`  — 用于所有运行模式
   * `config.author`  — 对于创作环境
   * `config.publish`  — 对于发布环境
   * `config.<run-mode>`  — 酌情

1. 是否需要&#x200B;**配置**&#x200B;或&#x200B;**工厂配置**。
1. 要配置的各个参数；包括需要重新创建的任何现有参数定义。

   在Web控制台中引用单个参数字段。 每个参数的名称都用方括号括起来。

   例如，创建属性
   `versionmanager.createVersionOnActivation` 配置激活 **时创建版本**。

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. `/libs`中是否已存在配置？ 要列出实例中的所有配置，请使用CRXDE Lite中的&#x200B;**Query**&#x200B;工具提交以下SQL查询：

   `select * from sling:OsgiConfig`

   如果是，则此配置可复制到` /apps/<yourProject>/`，然后在新位置中进行自定义。

#### 在存储库{#creating-the-configuration-in-the-repository}中创建配置

要将新配置实际添加到存储库，请执行以下操作：

1. 使用CRXDE Lite导航到：

   ` /apps/<yourProject>`

1. 如果尚未存在，请创建`config`文件夹(`sling:Folder`):

   * `config`  — 适用于所有运行模式
   * `config.<run-mode>`  — 特定于特定运行模式

1. 在此文件夹下，创建一个节点：

   * 类型: `sling:OsgiConfig`
   * 名称：持久身份(PID);

      例如，AEM Version Manager使用`com.day.cq.wcm.core.impl.VersionManagerImpl`
   >[!NOTE]
   >
   >在进行工厂配置时，将`-<identifier>`附加到该名称。
   >
   >如下所示：`org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >其中`<identifier>`被替换为您（必须）输入用来标识实例的自由文本（您不能忽略此信息）；例如：
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. 对于要配置的每个参数，在此节点上创建一个属性：

   * 名称：Web控制台中显示的参数名称；字段描述末尾的括号中显示该名称。 例如，对于`Create Version on Activation`，使用`versionmanager.createVersionOnActivation`
   * 类型：酌情。
   * 值：。

   您只需为要配置的参数创建属性，其他参数仍将采用AEM设置的默认值。

1. 保存所有更改。

   通过重新启动服务来更新节点后，会立即应用更改（与在Web控制台中所做的更改一样）。

>[!CAUTION]
>
>不得更改`/libs`路径中的任何内容。

>[!CAUTION]
>
>配置的完整路径必须正确，才能在启动时读取。

## 配置详细信息{#configuration-details}

### 启动时的分辨率顺序{#resolution-order-at-startup}

使用以下优先顺序：

1. `/apps/*/config...`下的存储库节点，类型为`sling:OsgiConfig`或属性文件。

1. `/libs/*/config...`下类型为`sling:OsgiConfig`的存储库节点。 （现成定义）。

1. 来自`<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`的任何`.config`文件。 在本地文件系统上。

这意味着`/libs`中的通用配置可能会被`/apps`中的项目特定配置掩盖。

### 运行时的分辨率顺序{#resolution-order-at-runtime}

在系统运行时所做的配置更改会通过修改的配置触发重新加载。

然后，将按以下优先顺序应用：

1. 在Web控制台中修改配置将立即生效，因为它在运行时具有优先权。
1. 在`/apps`中修改配置将立即生效。
1. 在`/libs`中修改配置将立即生效，除非该配置被`/apps`中的配置掩盖。

### 多运行模式的分辨率{#resolution-of-multiple-run-modes}

对于特定于运行模式的配置，可以组合多种运行模式。 例如，您可以按以下样式创建配置文件夹：

`/apps/*/config.<runmode1>.<runmode2>/`

如果所有运行模式都与启动时定义的运行模式匹配，则将应用此类文件夹中的配置。

例如，如果以运行模式`author,dev,emea`启动实例，则将应用`/apps/*/config.emea`、`/apps/*/config.author.dev/`和`/apps/*/config.author.emea.dev/`中的配置节点，而不应用`/apps/*/config.author.asean/`和`/config/author.dev.emea.noldap/`中的配置节点。

如果同一PID的多个配置适用，则应用匹配运行模式数目最多的配置。

例如，如果实例是以运行模式`author,dev,emea`启动的，则`/apps/*/config.author/`和`/apps/*/config.emea.author/`都定义了
`com.day.cq.wcm.core.impl.VersionManagerImpl`，将应用`/apps/*/config.emea.author/`中的配置。

此规则的粒度处于PID级别。
您不能在`/apps/*/config.author/`中为同一PID定义某些属性，而在`/apps/*/config.emea.author/`中为同一PID定义更多特定属性。
具有最大匹配运行模式数的配置将对整个PID有效。

### 标准配置{#standard-configurations}

以下列表显示了存储库中可用配置的一小部分（在标准安装中）：

* 作者 — AEM WCM过滤器：

   `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* 发布 — AEM WCM过滤器：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* 发布 — AEM WCM页面统计信息：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>由于这些配置位于`/libs`中，因此在自定义之前，不得直接编辑这些配置，而是将其复制到应用程序区域(`/apps`)。

要列出实例中的所有配置节点，请使用CRXDE Lite中的&#x200B;**Query**&#x200B;功能提交以下SQL查询：

`select * from sling:OsgiConfig`

### 配置持久性{#configuration-persistence}

* 如果通过Web控制台更改配置，则该配置（通常）会写入存储库中，具体位置为：

   `/apps/{somewhere}`

   * 默认情况下， `{somewhere}`为`system/config`，因此配置将写入

      `/apps/system/config`

   * 但是，如果您正在编辑最初来自存储库其他位置的配置：例如：

      /libs/foo/config/someconfig

      然后，将更新后的配置写在原始位置下；例如：

      `/apps/foo/config/someconfig`

* 由`admin`更改的设置保存在`*.config`文件下：

   ```
      /crx-quickstart/launchpad/config
   ```

   * 这是OSGi配置管理员的专用数据区域，包含`admin`指定的所有配置详细信息，无论这些配置详细信息是如何进入系统的。
   * 这是实施详细信息，您绝不能直接编辑此目录。
   * 但是，了解这些配置文件的位置以便可以获取备份和/或多个安装的副本是有用的：

      * Apache Felix OSGi管理控制台

         `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * CRX Sling客户端存储库

         `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>您必须&#x200B;***从不***&#x200B;编辑以下文件夹或文件：
>
>`/crx-quickstart/launchpad/config`
