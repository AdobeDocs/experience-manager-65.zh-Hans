---
title: 通过内容同步处理移动设备
description: 按照本页了解Content Sync。 在Adobe Experience Manager (AEM)中创作的页面可用作应用程序内容，即使设备处于离线状态也是如此。 此外，由于AEM页面基于Web标准，因此它们可以跨平台工作，使您能够将其嵌入任何本机包装器中。 此策略可减少开发工作量，并让您轻松更新应用程序内容。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: a6e59334-09e2-4bb8-b445-1868035da556
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '2950'
ht-degree: 0%

---

# 通过内容同步处理移动设备{#mobile-with-content-sync}

{{ue-over-mobile}}

使用Content Sync将内容打包，以便能够在本机移动设备应用程序中使用。 在Adobe Experience Manager (AEM)中创作的页面可用作应用程序内容，即使设备处于离线状态也是如此。 此外，由于AEM页面基于Web标准，因此它们可以跨平台工作，使您能够将其嵌入任何本机包装器中。 此策略可减少开发工作量，并让您轻松更新应用程序内容。

内容同步框架将创建一个包含Web内容的存档文件。 内容可以是简单页面、图像和PDF文件或整个Web应用程序中的任意内容。 内容同步API提供了从移动应用程序或构建进程访问存档文件的权限，以便可以检索内容并将其包含在应用程序中。

以下一系列步骤展示了Content Sync的典型用例：

1. AEM开发人员创建了一个内容同步配置，用于指定要包含的内容。
1. 内容同步框架收集和缓存内容。
1. 在移动设备上，启动移动设备应用程序并从服务器请求内容，该内容以ZIP文件形式交付。
1. 客户端将ZIP内容解压缩到本地文件系统。 ZIP文件中的文件夹结构模拟客户端（例如，浏览器）通常从服务器请求的路径。
1. 客户端在嵌入式浏览器中打开内容，或以其他方式使用内容。
1. 稍后，客户端从服务器请求更新内容。 内容同步框架提供增量更新以减少下载大小和时间，由于带宽或数据量有限，这对于移动设备可能非常重要。

## 开发内容同步处理程序 {#developing-the-content-sync-handlers}

开发内容同步处理程序的一些指导原则如下所示：

* 处理程序必须实现&#x200B;*com.day.cq.contentsync.handler.ContentUpdateHandler*（直接或扩展具有此功能的类）
* 处理程序可以扩展&#x200B;*com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* 如果处理程序更新ContentSync缓存，则只能报告true。 如果错误地报告true，则AEM会在实际没有发生更新时创建更新。
* 仅当内容发生更改时，处理程序才应更新缓存。 如果不需要白色，请勿写入缓存。 这会导致创建不必要的更新。

>[!NOTE]
>
>通过包&#x200B;*com.day.cq.contentsync*&#x200B;上的OSGI记录器配置启用&#x200B;*ContentSync调试记录*。 这样，您就可以跟踪运行了哪些处理程序，以及这些处理程序是否更新了缓存和报告更新了缓存。

## 配置内容同步内容 {#configuring-the-content-sync-content}

创建内容同步配置以指定交付给客户端的ZIP文件的内容。 您可以创建任意数量的内容同步配置。 每个配置都有一个名称用于标识。

要创建内容同步配置，请向存储库中添加`cq:ContentSyncConfig`节点，并将`sling:resourceType`属性设置为`contentsync/config`。 `cq:ContentSyncConfig`节点可以位于存储库中的任意位置，但是AEM发布实例上的用户必须能够访问该节点。 因此，您应在`/content`下添加节点。

要指定内容同步ZIP文件的内容，请将子节点添加到cq：ContentSyncConfig节点。 每个子节点的以下属性标识要包含的内容项，以及在添加内容项时如何对其进行处理：

* `path`：内容的位置。
* `type`：用于处理内容的配置类型的名称。 有几种类型可用，在&#x200B;*配置类型*&#x200B;一节中有介绍。

有关详细信息，请参阅&#x200B;*示例内容同步配置*。

创建内容同步配置后，该配置将显示在内容同步控制台中。

>[!NOTE]
>
>内容同步框架不检查资产依赖项和设计相关文件是否包含在内容同步包中。 确保在ZIP文件中包含所有必需的文件。

### 配置对内容同步下载的访问权限 {#configuring-access-to-content-sync-downloads}

指定可以从内容同步下载的用户或组。 您可以配置可以从所有内容同步缓存下载的默认用户或组，也可以覆盖默认用户或组，并配置特定内容同步配置的访问权限。

安装AEM后，管理员组的成员可以默认从Content Sync下载。

#### 设置内容同步下载的默认访问权限 {#setting-the-default-access-for-content-sync-downloads}

Day CQ Content Sync Manager服务控制对Content Sync的访问。 配置此服务以指定默认情况下可从Content Sync下载的用户或组。

如果您正在[使用Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)配置服务，请键入用户或组的名称作为“可授权回退缓存”属性的值。

如果您在存储库[&#128279;](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)中进行配置，请使用以下有关服务的信息：

* PID： com.day.cq.contentsync.impl.ContentSyncManagerImpl
* 属性名称： contentsync.fallback.authorizable

#### 覆盖内容同步缓存的下载访问权限 {#overriding-download-access-for-a-content-sync-cache}

要配置特定内容同步配置的下载访问权限，请将以下属性添加到`cq:ContentSyncConfig`节点：

* 名称：可授权
* 类型：字符串
* 值：可下载的用户或组的名称。

例如，您的应用程序允许用户直接从Content Sync安装更新。 要允许所有用户下载更新，请将可授权属性的值设置为`everyone`。

如果`cq:ContentSyncConfig`节点没有可授权属性，则为Day CQ内容同步管理器服务的回退缓存可授权属性配置的默认用户或组将确定可以下载的用户。

### 配置用户以更新内容同步缓存 {#configuring-the-user-for-updating-a-content-sync-cache}

当用户对内容同步缓存执行更新时，特定用户帐户代表用户执行操作。 默认情况下，匿名用户会更新所有Content Sync缓存。

您可以覆盖默认用户，并指定更新特定内容同步缓存的用户或组。

要覆盖默认用户，请通过将以下属性添加到cq：ContentSyncConfig节点来指定用户或组，以更新特定内容同步配置：

* 名称：`updateuser`
* 类型：`String`
* 值：可执行更新的用户或组的名称。

如果`cq:ContentSyncConfig`节点没有`updateuser`属性，则默认`anonymous`用户将更新缓存。

### 配置类型 {#configuration-types}

处理范围从呈现简单的JSON到完全呈现页面（包括其引用的资产）。 此部分列出了可用的配置类型及其特定参数：

**复制** — 复制文件和文件夹。

* **path** — 如果路径指向单个文件，则仅复制该文件。 如果它指向一个文件夹（其中包括页面节点），则会复制下面的所有文件和文件夹。

**内容**&#x200B;使用标准[Sling请求处理](/help/sites-developing/the-basics.md#sling-request-processing)呈现内容。

* **path** — 应为输出的资源的路径。
* **扩展** — 应在请求中使用的扩展。 常见示例为&#x200B;*html*&#x200B;和&#x200B;*json*，但任何其他扩展都是可能的。

* **选择器** — 可选的选择器，用点分隔。 常见的示例有&#x200B;*touch* （用于呈现页面的移动版本）或&#x200B;*infinity* （用于JSON输出）。

**clientlib** — 打包JavaScript或CSS客户端库。

* **path** — 客户端库根的路径。
* **扩展** — 客户端库的类型。 此时应将此项设置为&#x200B;*js*&#x200B;或&#x200B;*css*。

**资源**

收集资源的原始演绎版。

* **path** - /content/dam下的资产文件夹的路径。

**图像** — 收集图像。

* **path** — 图像资源的路径。

图像类型用于在zip文件中包含We Retail徽标。

**页面** — 呈现AEM页面并收集引用的资源。

* **path** — 页面的路径。
* **扩展** — 应在请求中使用的扩展。 对于页面，这几乎总是&#x200B;*html*，但其他仍可实现。

* **选择器** — 可选的选择器，用点分隔。 渲染页面的移动版本的常见示例为&#x200B;*touch*。

* **deep** — 可确定是否也应包含子页面的可选布尔属性。 默认值为&#x200B;*true。*

* **includeImages** — 确定是否应包含图像的可选布尔属性。 默认值为&#x200B;*true*。

  默认情况下，只考虑包含资源类型为foundation/components/image的图像组件。 您可以通过在Web控制台中配置&#x200B;**Day CQ WCM页面更新处理程序**&#x200B;来添加更多资源类型。

**rewrite** - rewrite节点定义如何在导出的页面中重写链接。 重写的链接可以指向zip文件中包含的文件或服务器上的资源。

`rewrite`节点必须位于`page`节点的下方。

`rewrite`节点可以具有以下一个或多个属性：

* `clientlibs`：重写clientlibs路径。

* `images`：重写图像路径。
* `links`：重写链接路径。

每个属性都可以具有以下值之一：

* `REWRITE_RELATIVE`：用相对位置重写文件系统上的页面.html文件的路径。

* `REWRITE_EXTERNAL`：使用AEM [外部化器服务](/help/sites-developing/externalizer.md)，通过指向服务器上的资源重写路径。

名为&#x200B;**PathRewriterTransformerFactory**&#x200B;的AEM服务允许您配置将重写的特定html属性。 该服务可以在Web控制台中进行配置，并且具有`rewrite`节点的每个属性的配置： `clientlibs`、`images`和`links`。

此功能是在AEM 5.5中添加的。

### 示例内容同步配置 {#example-content-sync-configuration}

以下列表显示了Content Sync的配置示例。

```xml
+ weretail_go [cq:ContentSyncConfig]
  - sling:resourceType = "contentsync/config"

  + etc.designs.default [nt:unstructured]
    - path = "/etc/designs/default"
    - type = "copy"

  + etc.designs.mobile [nt:unstructured]
    - path = "/etc/designs/mobile"
    - type = "copy"

  + events.plist [nt:unstructured]
    - path = "/content/weretail_mobile/en/events/jcr:content/par/events"
    - type = "content"
    - extension = "plist"

  + events.touch.html [nt:unstructured]
    - path = "/content/weretail_mobile/en/events"
    - type = "pages"
    - extension = "html"
    - selector = "touch"

  + logo [nt:unstructured]
    - path = "/etc/designs/mobile/jcr:content/mobilecontentpage/logo"
    - type = "logo"

  + manifest [nt:unstructured]
    - indexPage = "/content/weretail_mobile/en/events.touch.html"
    - metadataPlist = "/content/weretail_mobile/en/events/_jcr_content/par/events.plist"

  + ...
```

**etc.designs.default和etc.designs.mobile** — 配置的前两个条目显而易见。 由于您即将包含多个移动设备页面，因此需要/etc/designs下的相关设计文件。 由于无需额外处理，因此只需复制即可。

**events.plist** — 此条目有点特殊。 如简介中所述，应用程序应提供包含事件位置标记的地图视图。 必要的位置信息将作为单独的文件以PLIST格式提供。 要使此功能正常工作，在索引页上使用的事件列表组件具有一个名为plist.jsp的脚本。 当使用`.plist`扩展请求组件的资源时，将运行此脚本。 与往常一样，在path属性中给定组件路径，并将类型设置为content，因为您希望使用[Sling请求处理](/help/sites-developing/the-basics.md#sling-request-processing)。

**events.touch.html** — 接下来是应用程序中显示的实际页面。 path属性设置为事件的根页面。 该页面下的所有事件页面也将被包含，因为deep属性默认为true。 您可以将页面用作配置类型，以便纳入任何可能从页面上的图像或下载组件引用的图像或其他文件。 此外，设置触摸选择器将会为我们提供页面的移动设备版本。 功能包中的配置包含更多此类条目，但为了简单起见，此处未包含这些条目。

**徽标** — 徽标配置类型目前尚未提及，它不属于内置类型。 但是，内容同步框架在某种程度上是可扩展的，本节将介绍这方面的一个示例。

**manifest** — 通常希望在zip文件中包含某种元数据，例如内容的起始页。 但是，对此类信息进行硬编码会妨碍您以后轻松更改这些信息。 内容同步框架支持此用例，方法是查找配置中的清单节点，该节点由名称标识并且不需要配置类型。 在该特定节点上定义的每个属性都会添加到文件中，该文件也称为清单并驻留在zip文件的根中。

在本例中，事件列表页面应该是初始页面。 此信息在&#x200B;**indexPage**&#x200B;属性中提供，因此可以随时轻松更改。 第二个属性定义&#x200B;*events.plist*&#x200B;文件的路径。 正如您稍后看到的，客户端应用程序现在可以读取清单并根据清单执行操作。

设置配置后，可以使用浏览器或任何其他HTTP客户端下载内容，或者，如果您正在为iOS进行开发，则可以使用专用的WAppKitSync客户端库。 下载位置由配置的路径和&#x200B;*.zip*&#x200B;扩展组成，例如，使用本地AEM实例时： *http://localhost:4502/content/weretail_go.zip*

### 内容同步控制台 {#the-content-sync-console}

内容同步控制台列出了存储库中的所有内容同步配置（类型为`cq:ContentSyncConfig`的所有节点），对于每个配置，您可以执行以下操作：

* 更新缓存。
* 清除缓存。
* 下载完整的zip文件。
* 下载当前日期与特定日期和时间的差异zip文件。

它对于开发和故障诊断非常有用。

可在以下位置访问该控制台：

`http://localhost:4502/libs/cq/contentsync/content/console.html`

它如下所示：

![chlimage_1-50](assets/chlimage_1-50.png)

### 扩展内容同步框架 {#extending-the-content-sync-framework}

尽管配置选项的数量已经非常多，但可能并不涵盖特定用例的所有要求。 此部分介绍Content Sync框架的扩展点以及如何创建自定义配置类型。

对于每个配置类型，都有一个&#x200B;*内容更新处理程序*，它是为该特定类型注册的OSGi组件工厂。 这些处理程序收集和处理内容，并将其添加到由内容同步框架维护的缓存中。 实现以下接口或抽象基类：

* `com.day.cq.contentsync.handler.ContentUpdateHandler` — 所有更新处理程序都必须实施的接口
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` — 使用Sling简化资源渲染的抽象类

将类注册为OSGi组件工厂，并将其部署在捆绑包的OSGi容器中。 可以使用[Maven SCR插件](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/apache-felix-maven-scr-plugin-use.html)通过JavaDoc标记或注释来完成此操作。 以下示例显示了JavaDoc版本：

```java
/*
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/customtype"
 */
public class CustomTypeUpdateHandler implements ContentUpdateHandler {
    // add your code here
}

/*
 * @scr.component metatype="no" inherit="true"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/othertype"
 */
public class OtherTypeUpdateHandler extends AbstractSlingResourceUpdateHandler {
    // add your code here
}
```

请注意，*factory*&#x200B;定义包含公共接口和用斜杠分隔的自定义类型。 此策略允许内容同步框架在识别配置条目中的自定义类型时查找和创建自定义类的实例。 下一部分提供了自定义更新处理程序的具体示例。

>[!CAUTION]
>
>基于AbstractSlingResourceUpdateHandler基类进行构建时，必须添加&#x200B;*inherit*&#x200B;定义。 否则，OSGi容器将不会设置基类中声明的必需引用。

### 实施自定义更新处理程序 {#implementing-a-custom-update-handler}

每个We.Retail Mobile页面的左上角都有一个应当包含在zip文件中的徽标。 但是，对于缓存优化，AEM不引用图像文件在存储库中的实际位置，这会阻止我们仅使用&#x200B;**副本**&#x200B;配置类型。 您必须提供我们自己的&#x200B;**徽标**&#x200B;配置类型，以便在AEM请求的位置提供图像。 以下代码列表显示了徽标更新处理程序的完整实施：

#### LogoUpdateHandler.java {#logoupdatehandler-java}

```java
package com.day.cq.wcm.apps.weretail.impl;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.day.cq.commons.jcr.JcrUtil;
import com.day.cq.contentsync.config.ConfigEntry;
import com.day.cq.contentsync.handler.ContentUpdateHandler;
import com.day.cq.wcm.foundation.Image;
import com.day.text.Text;

/**
 * The <code>LogoUpdateHandler</code> is used to update the content sync cache
 * with a page logo added using a logo component.
 *
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/logo"
 */
public class LogoUpdateHandler implements ContentUpdateHandler {

    private static final Logger log = LoggerFactory.getLogger(LogoUpdateHandler.class);

    /** @scr.reference policy="static" */
    protected JcrResourceResolverFactory resolverFactory;

    public boolean updateCacheEntry(ConfigEntry configEntry, Long lastUpdated, String configCacheRoot, Session admin, Session session) {
        ResourceResolver resolver = resolverFactory.getResourceResolver(admin);
        Resource resource = resolver.getResource(configEntry.getContentPath());

        Image img = new Image(resource);
        img.setItemName(Image.NN_FILE, "image");
        img.setItemName(Image.PN_REFERENCE, "imageReference");
        img.setSelector("img");

        try {
            if(img.getLastModified() == null || lastUpdated < img.getLastModified().getTime().getTime()) {
                String src = img.getSrc();
                String parentPath = configCacheRoot + Text.getRelativeParent(src, 1);

                Node parent = JcrUtil.createPath(parentPath, "sling:Folder", admin);
                Node image = resolver.getResource(resource.getPath() + "/image").adaptTo(Node.class);
                JcrUtil.copy(image, parent, Text.getName(src));

                admin.save();

                return true;
            }
        } catch (RepositoryException e) {
            log.error("Unexpected error while updating logo: ", e);
        }

        return false;
    }
}
```

`LogoUpdateHandler`类实现`ContentUpdateHandler`接口的`updateCacheEntry(ConfigEntry, Long, String, Session, Session)`方法，该方法接受多个参数：

* 一个`ConfigEntry`实例，它提供对调用此处理程序的配置条目及其属性的访问权限。
* 一个`lastUpdated`时间戳，指示内容同步上次更新其缓存的时间。 处理程序不应更新在该时间戳之后未修改的内容。
* 指定缓存根路径的`configCacheRoot`参数。 所有更新的文件都必须存储在此路径下方，才能添加到zip文件中。
* 用于所有与缓存相关的存储库操作的管理会话。
* 用户会话，可用于在特定用户的上下文中更新内容，从而提供个性化内容。

要实施自定义处理程序，请首先根据配置条目中提供的资源创建Image类的实例。 此过程与页面上实际的徽标组件所执行的操作相同。 它确保图像的目标路径与页面中引用的路径相同。

接下来，检查自上次更新以来是否修改了资源。 自定义实施应避免对缓存进行不必要的更新，如果未做任何更改，则返回false。 如果修改了资源，请将映像复制到相对于缓存根目录的预期目标位置。 最后，返回`true`以向框架指示缓存已更新。

## 使用客户端上的内容 {#using-the-content-on-the-client}

要在由内容同步提供的移动应用程序中使用内容，必须通过HTTP或HTTPS连接请求内容。 因此，检索的内容（打包在ZIP文件中）可以被提取并存储在移动设备本地。 内容不仅是指数据，而且是指逻辑，即完整的Web应用程序；因此，即使没有网络连接，移动用户也可以执行检索到的Web应用程序和相应的数据。

内容同步以智能方式交付内容：仅交付自上次成功交付数据同步后发生的数据更改，因此减少了数据传输所需的时间。 在首次运行应用程序时，会请求自1970年1月1日以来的数据更改，而稍后仅请求自上次成功同步以来更改的数据。 AEM使用iOS的客户端通信框架来简化数据通信和传输，因此，只需最少的本机代码即可启用基于iOS的Web应用程序。

所有传输的数据都可提取到相同的目录结构中，提取数据时不需要执行额外的步骤（例如，依赖关系检查）。 如果存在iOS，则所有数据都会存储在iOS应用程序的Documents文件夹内的子文件夹中。

基于iOS的AEM Mobile应用程序的典型执行路径：

* 用户在iOS设备上启动应用程序。
* 应用程序尝试连接到AEM后端，并请求自上次运行以来数据发生更改。
* 服务器检索有问题的数据并将它们压缩到一个文件中。
* 数据将返回到客户端设备，并提取到文档文件夹中。
* UIWebView组件启动/刷新。

如果以前无法建立连接，则会显示下载的数据。

### 其他资源 {#additional-resources}

要了解管理员和作者的角色和责任，请参阅以下资源：

* [为AEM Mobile On-demand Services创作AEM内容](/help/mobile/mobile-apps-ondemand.md)
* [管理内容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
