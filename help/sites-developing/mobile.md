---
title: 为移动设备创建站点
seo-title: Creating Sites for Mobile Devices
description: 创建移动站点与创建标准站点类似，因为它还涉及创建模板和组件
seo-description: Creating a mobile site is similar to creating a standard site as it also involves creating templates and components
uuid: 6b19042c-03f1-4e33-970e-475f9fb8c5fb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 0aabfb0a-ef9c-4b06-b698-61cad101c3c1
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
exl-id: 21b2037a-685a-441d-aecd-865884253e03
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3840'
ht-degree: 1%

---

# 为移动设备创建站点{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

创建移动站点与创建标准站点类似，因为它还涉及创建模板和组件。 有关创建模板和组件的更多详细信息，请参阅以下页面： [模板](/help/sites-developing/templates.md), [组件](/help/sites-developing/components.md) 和 [开发入门AEM Sites](/help/sites-developing/getting-started.md). 主要区别在于在网站中启用AEM内置移动功能。 它是通过创建依赖于移动页面组件的模板来实现的。

您还应考虑使用 [响应式设计](/help/sites-developing/responsive.md)，创建一个可容纳多种屏幕大小的网站。

要开始，您可以查看 **We.Retail移动设备演示网站** 中的“隐藏主体”(A)。

要创建移动站点，请按如下步骤继续操作：

1. 创建页面组件：

   * 设置 `sling:resourceSuperType` 属性 `wcm/mobile/components/page`
这样，组件就依赖于移动页面组件。

   * 创建 `body.jsp` 具有项目特定逻辑。

1. 创建页面模板：

   * 设置 `sling:resourceType` 属性添加到新创建的页面组件。
   * 设置 `allowedPaths` 属性。

1. 为网站创建设计页面。
1. 在 `/content` 节点：

   * 设置 `cq:allowedTemplates` 属性。
   * 设置 `cq:designPath` 属性。

1. 在站点根页面的页面属性中，在 **移动设备** 选项卡。
1. 使用新模板创建网站页面。

移动页面组件( `/libs/wcm/mobile/components/page`):

* 添加 **移动设备** 选项卡。
* 通过 `head.jsp`，它会从请求中检索当前移动设备组，如果找到设备组，则会使用 `drawHead()` 方法，包括设备组的关联模拟器init组件（仅在创作模式下）和设备组的呈现CSS。

>[!NOTE]
>
>移动站点的根页面需要位于节点层次结构的1级，建议位于/content节点下。

## 使用多站点管理器创建移动站点 {#creating-a-mobile-site-with-the-multi-site-manager}

使用多站点管理器(MSM)从标准站点创建移动Live Copy。 标准网站会自动转换为移动网站：移动站点具有移动站点的所有功能（例如，在模拟器中编辑），并且可以与标准站点同步进行管理。 请参阅章节 [为不同渠道创建Live Copy](/help/sites-administering/msm.md) （在“多站点管理器”页面中）。

## 服务器端移动API {#server-side-mobile-api}

包含移动类的Java包包括：

* [com.day.cq.wcm.mobile.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html)  — 定义MobileConstants。
* [com.day.cq.wcm.mobile.api.device](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html)  — 定义设备、设备组和设备组列表。
* [com.day.cq.wcm.mobile.api.device.capability](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html)  — 定义DeviceCapability。
* [com.day.cq.wcm.mobile.api.wurfl](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/api/package-summary.html)  — 定义WurflQueryEngine。
* [com.day.cq.wcm.mobile.core](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/core/package-summary.html)  — 定义MobileUtil，它提供了围绕WCM Mobile的各种实用工具方法。

### 移动设备组件 {#mobile-components}

的 **We.Retail移动设备演示网站** 使用下面的移动设备组件 `/libs/foundation/components`:

<table>
 <tbody>
  <tr>
   <td>名称</td>
   <td>组</td>
   <td>特征</td>
  </tr>
  <tr>
   <td>mobilefooter</td>
   <td>隐藏</td>
   <td> — 页脚</td>
  </tr>
  <tr>
   <td>mobileimage</td>
   <td>移动设备</td>
   <td> — 基于图像基础组件<br />  — 如果设备能够<br /> </td>
  </tr>
  <tr>
   <td>mobilelist</td>
   <td>移动设备</td>
   <td> — 基于列表基础组件<br /> - listitem_teaser.jsp在设备可用时呈现图像<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>隐藏</td>
   <td> — 基于徽标基础组件<br />  — 如果设备能够<br /> </td>
  </tr>
  <tr>
   <td>mobilereference</td>
   <td>移动设备</td>
   <td><p> — 类似于引用基础组件</p> <p> — 将文本时间组件映射到mobiletextimage 1，将图像组件映射到mobileimage 1</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>移动设备</td>
   <td> — 基于文本时间基础组件<br />  — 如果设备能够</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>隐藏</td>
   <td><p> — 基于topnav foundation组件</p> <p> — 仅渲染文本</p> </td>
  </tr>
 </tbody>
</table>

#### 创建移动设备组件 {#creating-a-mobile-component}

AEM移动框架允许开发对发出请求的设备敏感的组件。 以下代码示例显示了如何在组件jsp中使用AEM移动API，特别是如何：

* 从请求中获取设备：
   `Device device = slingRequest.adaptTo(Device.class);`

* 获取设备组：
   `DeviceGroup deviceGroup = device.getDeviceGroup();`

* 获取设备组功能：
   `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* 获取设备属性（WURFL数据库中的原始功能键/值）：
   `Map<String,String> deviceAttributes = device.getAttributes();`

* 获取设备用户代理：
   `String userAgent = device.getUserAgent();`

* 从当前页面获取设备组列表（作者分配给站点的设备组）：
   `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* 检查设备组是否支持图像
   `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
或者

...   `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>在jsp中， `slingRequest` 可通过 `<sling:defineObjects>` 标记和 `currentPage` 到 `<cq:defineObjects>` 标记。

### 模拟器 {#emulators}

基于模拟器的创作为作者提供了创建面向移动设备客户端的内容页面的方法。 移动内容创作遵循与就地所见即所得(WYSIWYG)编辑相同的原则。 为了让作者感知移动设备上的页面外观，可使用设备模拟器编辑移动内容页面。

移动设备模拟器基于通用的模拟器框架。 有关更多详细信息，请参阅 [模拟器](/help/sites-developing/emulators.md) 页面。

设备模拟器会在页面上显示移动设备，而常规的编辑（parsys、组件）则发生在设备的屏幕中。 设备模拟器取决于为站点配置的设备组。 可以将多个模拟器分配给设备组。 然后，内容页面上会提供所有模拟器。 默认情况下，将显示分配给站点的第一个设备组的第一个模拟器。 可以通过页面顶部的模拟器轮播或通过Sidekick的编辑按钮来切换模拟器。

**创建模拟器**

要创建模拟器，请参阅 [创建自定义移动设备模拟器](/help/sites-developing/emulators.md) 部分。

**移动仿真器的主要特性**

* 设备组由一个或多个模拟器之一组成：设备组配置页面，例如/etc/mobile/groups/touch，包含 `emulators` 属性 `jcr:content` 节点。
注意：虽然同一模拟器可能属于多个设备组，但这没有太大意义。

* 通过设备组的配置对话框， `emulators` 属性会使用所需模拟器的路径进行设置。 例如：`/libs/wcm/mobile/components/emulators/iPhone4`。

* 模拟器组件(例如， `/libs/wcm/mobile/components/emulators/iPhone4`)扩展基本的移动模拟器组件( `/libs/wcm/mobile/components/emulators/base`)。

* 在配置设备组时，可以选择扩展基本移动模拟器的每个组件。 因此，可以轻松创建或扩展自定义模拟器。
* 在编辑模式下的请求时，将使用模拟器实施来呈现页面。
* 当页面的模板依赖于移动页面组件时，模拟器功能会自动集成到页面中(通过 `head.jsp` )。

### 设备组 {#device-groups}

移动设备组根据设备功能提供移动设备的分段。 设备组提供了在创作实例上基于模拟器进行创作以及在发布实例上正确呈现内容所需的信息：作者向移动设备页面添加内容并将其发布后，即可在发布实例中请求该页面。 在该视图中，内容页面将使用配置的一个设备组呈现，而不是模拟器编辑视图。 设备组的选择基于 [移动设备检测](#devicedetection). 然后，匹配设备组提供必要的样式信息。

设备组定义为以下内容页面 `/etc/mobile/devices` 并使用 **移动设备组** 模板。 设备组模板用作内容页面形式的设备组定义的配置模板。 其主要特点是：

* 位置: `/libs/wcm/mobile/templates/devicegroup`
* 允许的路径： `/etc/mobile/groups/*`
* 页面组件: `wcm/mobile/components/devicegroup`

#### 将设备组分配给您的网站 {#assigning-device-groups-to-your-site}

在创建移动设备网站时，您需要将设备组分配给您的网站。 AEM根据设备的HTML和JavaScript渲染功能提供了三个设备组：

* **功能** 手机，适用于Sony Ericsson W800等功能设备，支持基本HTML，但不支持图像和JavaScript。
* **智能** 手机，适用于支持基本HTML和图像的Blackberry等设备，但不支持JavaScript。

* **触控** 手机，适用于完全支持HTML、图像、JavaScript和设备旋转的iPad等设备。

由于模拟器可以与设备组关联(请参阅 [创建设备组](#creating-a-device-group))，则将设备组分配给站点后，作者可以在与设备组关联的模拟器之间进行选择，以编辑页面。

要将设备组分配给您的网站，请执行以下操作：

1. 在您的浏览器中，转到 **Siteadmin** 控制台。
1. 在下面打开移动设备站点的根页面 **网站**.
1. 打开页面属性。
1. 选择 **移动设备** 选项卡：

   * 定义设备组。
   * 单击&#x200B;**确定**。

>[!NOTE]
>
>为网站定义设备组后，网站的所有页面都会继承这些设备组。

#### 设备组筛选器 {#device-group-filters}

设备组筛选器定义了用于确定设备是否属于该组的基于功能的标准。 在创建设备组时，您可以选择用于评估设备的过滤器。

在AEM收到来自设备的HTTP请求时，与组关联的每个过滤器都会将设备功能与特定条件进行比较。 当设备具有过滤器所需的所有功能时，设备会被视为属于组。 功能从WURFL™数据库中检索。

设备组可以使用零个或多个过滤器进行功能检测。 此外，过滤器可以与多个设备组一起使用。 AEM提供了一个默认过滤器，用于确定设备是否具有为组选择的功能：

* CSS
* JPG和PNG图像
* JavaScript
* 设备旋转

如果设备组不使用过滤器，则为该组配置的选定功能是设备所需的唯一功能。

有关更多信息，请参阅 [创建设备组过滤器](/help/sites-developing/groupfilters.md).

#### 创建设备组 {#creating-a-device-group}

当安装的AEM组不符合您的要求时，请创建设备组。

1. 在您的浏览器中，转到 **工具** 控制台。
1. 在下面创建新页面 **工具** > **移动设备** > **设备组**. 在 **创建页面** 对话框：

   * 作为 **标题** enter `Special Phones`.

   * 作为 **名称** enter `special`.

   * 选择 **移动设备组模板**.
   * 单击&#x200B;**创建**。

1. 在CRXDE中，添加 **static.css** 文件，其中包含设备组的样式位于 `/etc/mobile/groups/special` 节点。

1. 打开 **特殊电话** 页面。
1. 要配置设备组，请单击 **编辑** 按钮 **设置**.
在 **常规** 选项卡：

   * **标题**:移动设备组的名称。
   * **描述**:群组的描述。
   * **User-Agent**:与设备匹配的用户代理字符串。 它是可选的，可以是正则表达式。 示例: `BlackBerryZ10`
   * **功能**:定义组是否可以处理图像、CSS、JavaScript或设备旋转。
   * **最小屏幕宽度**&#x200B;和&#x200B;**高度**
   * **禁用模拟器**:可在内容编辑期间启用/禁用模拟器。

   在 **模拟器** 选项卡：

   * **模拟器**:选择分配给此设备组的模拟器。

   在 **过滤器** 选项卡：

   * 要添加过滤器，请单击添加项目，然后从下拉列表中选择一个过滤器。
   * 将按过滤器的显示顺序进行评估。 当设备不符合过滤器的条件时，将不会评估列表中的后续过滤器。



1. 单击确定。

移动设备组配置对话框如下所示：

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### 每个设备组的自定义CSS {#custom-css-per-device-group}

如前所述，可以将自定义CSS与设备组页面相关联，这与设计页面的CSS非常相似。此CSS用于影响页面内容在创作和发布时的设备组特定呈现。随后，将自动包含此CSS:

* 在此设备组使用的每个模拟器的创作实例页面上。
* 在发布实例的页面中，如果请求的用户代理与此特定设备组中的移动设备匹配，则为。

## 服务器端设备检测 {#server-side-device-detection}

使用过滤器和设备规范库来确定执行HTTP请求的设备的功能。

### 开发设备组过滤器 {#develop-device-group-filters}

创建设备组筛选器以定义一组设备功能要求。 根据需要创建任意数量的过滤器，以定位所需的设备功能组。

设计过滤器，以便您能够使用它们的组合来定义功能组。 通常，不同设备组的功能会重叠。 因此，您可以将一些过滤器与多个设备组定义结合使用。

创建过滤器后，可以在组配置中使用该过滤器。

有关信息，请转到 [创建设备组过滤器](/help/sites-developing/groupfilters.md).

### 使用WURFL™数据库 {#using-the-wurfl-database}

AEM使用截断版本的 [沃夫尔](https://wurfl.sourceforge.net/)™数据库，根据设备的用户代理查询设备功能，如屏幕分辨率或javascript支持。

WURFL™数据库的XML代码表示为下面的节点 `/var/mobile/devicespecs` 通过解析 `wurfl.xml`文件位置 `/libs/wcm/mobile/devicespecs/wurfl.xml.` 向节点的扩展是在 `cq-mobile-core` 包启动。

设备功能将存储为节点属性，节点表示设备型号。 您可以使用查询检索设备或用户代理的功能。

随着WURFL™数据库的不断发展，您可能需要对其进行定制或替换。 要更新移动设备数据库，您可以使用以下选项：

* 如果您拥有允许此用途的许可证，请将文件替换为最新版本。 请参阅安装其他WURFL数据库。
* 使用AEM中提供的版本，并配置与用户代理字符串匹配并指向现有WURFL™设备的正则表达式。 请参阅 [添加基于正则表达式的用户代理匹配](#adding-a-regexp-based-user-agent-matching).

#### 测试用户代理到WURFL™功能的映射 {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

当设备访问您的移动设备网站时， AEM会检测到设备，根据其功能将其映射到设备组，并发送与设备组对应的页面查看。 匹配设备组提供必要的样式信息。 可以在移动设备用户代理测试页面上测试这些映射：

`https://localhost:4502/etc/mobile/useragent-test.html`

#### 安装不同的WURFL™数据库 {#installing-a-different-wurfl-database}

随AEM一起安装的截断的WURFL™数据库是2011年8月30日之前发布的版本。 如果您的WURFL版本是在2011年8月30日之后发布的，请确保您的使用符合您的许可证。

安装WURFL™数据库：

1. 在CRXDE Lite中，创建以下文件夹： `/apps/wcm/mobile/devicespecs`
1. 将WURFL™文件复制到文件夹中。
1. 将文件重命名为 `wurfl.xml`.

AEM自动解析 `wurfl.xml` 文件并更新以下节点 `/var/mobile/devicespecs`.

>[!NOTE]
>
>启用完整WURFL™数据库后，解析和激活可能需要几分钟时间。 您可以查看日志以获取进度信息。

#### 添加基于正则表达式的用户代理匹配 {#adding-a-regexp-based-user-agent-matching}

在/apps/wcm/mobile/devicesecps/wurfl/regexp下添加用户代理作为正则表达式，以指向现有WURFL™设备类型。

1. 在 **CRXDE Lite**，在/apps/wcm/mobile/devicespecs/regexp下创建一个节点，例如apple_ipad_ver1。
1. 将以下属性添加到节点：

   * **regexp**:定义用户代理的正则表达式，例如：.&#42;Mozilla。&#42;iPad.&#42;AppleWebKit。&#42;Safari。&#42;
   * **deviceId**:wurfl.xml中定义的设备ID，例如：apple_ipad_ver1

上述配置使User-Agent与提供的正则表达式匹配的设备（如果存在）被映射到apple_ipad_ver1 WURFL™设备ID。

## 客户端设备检测 {#client-side-device-detection}

本节介绍如何使用AEM的设备客户端检测来优化页面渲染或为客户端提供替代网站版本。

AEM支持基于 `BrowserMap`. `BrowserMap` 作为客户端库在AEM中发运，位于 `/etc/clientlibs/browsermap`.

`BrowserMap` 为您提供了三种策略，您可以使用这些策略向客户提供替代网站，这些策略按以下顺序使用：

1. [备用链接](#providing-alternate-links)
1. [特定于设备组的URL](#definingdevicegroupspecificurl)
1. [基于选择器的URL](#defining-selector-based-urls)

>[!NOTE]
>
>有关客户端库集成的更多信息，请阅读 [使用客户端HTML库](/help/sites-developing/clientlibs.md) 中。

### 提供备用链接 {#providing-alternate-links}

的 `PageVariantsProvider` OSGi服务能够为属于同一系列的站点生成备用链接。 为了配置服务要考虑的站点， `cq:siteVariant` 节点必须添加到 `jcr:content` 节点。

的 `cq:siteVariant` 节点需要具有以下属性：

* `cq:childNodesMapTo`  — 确定子节点将映射到的链接元素的属性；建议以这种方式组织网站内容，以便根节点的子节点代表全局网站语言变体的根(例如， `/content/mysite/en`, `/content/mysite/de`)，在这种情况下， `cq:childNodesMapTo` 应该 `hreflang`;
* `cq:variantDomain`  — 指示内容 `Externalizer` 域将用于生成页面变体绝对URL;如果未设置此值，则将使用相对链接生成页面变体；
* `cq:variantFamily`  — 指示此网站属于哪个网站系列；同一网站的多个特定设备表示应属于同一家族；
* `media`  — 存储链接元素的媒体属性值；建议使用 `BrowserMap` 注册 `DeviceGroups`，以便 `BrowserMap` 库可以自动将客户端转发到网站的正确变体。

#### PageVariantsProvider和Externalizer {#pagevariantsprovider-and-externalizer}

当 `cq:variantDomain` 属性 `cq:siteVariant` 节点不为空， `PageVariantsProvider` 服务将使用此值作为配置的域来生成绝对链接 `Externalizer` 服务。 确保配置 `Externalizer` 服务来反映您的设置。

>[!NOTE]
>
>使用AEM时，可通过多种方法来管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解更多详细信息和建议的实践。

### 定义设备组特定URL {#defining-a-device-group-specific-url}

如果您不想使用备用链接，则可以为每个链接配置全局URL `DeviceGroup`. 我们建议创建您自己的客户端库，该库嵌入 `browsermap.standard` 客户端库，但重新定义了设备组。

BrowserMap的设计方式是，通过创建同名的新设备组并将其添加到 `BrowserMap` 对象。

>[!NOTE]
>
>有关更多详细信息，请阅读 [自定义BrowserMap](#creatingacustomisedbrowsermap) 中。

### 定义基于选择器的URL {#defining-selector-based-urls}

如果没有采用任何以前的机制来指明 `BrowserMap`，然后选择将使用 `DeviceGroups` 将添加到 `URL`s，在这种情况下，您应提供自己的Servlet来处理请求。

例如，设备浏览 `www.example.com/index.html` 标识为 `smartphone` 由BrowserMap转发到 `www.example.com/index.smartphone.html.`

### 在您的页面上使用BrowserMap {#using-browsermap-on-your-pages}

要在页面中使用标准的BrowserMap客户端库，您必须包含 `/libs/wcm/core/browsermap/browsermap.jsp` 使用 `cq:include`标记 `head` 中。

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

除了添加 `BrowserMap` 您的 `JSP` 文件，则还必须添加 `cq:deviceIdentificationMode` 字符串属性设置为 `client-side` 到 `jcr:content` 节点。

### 覆盖BrowserMap的默认行为 {#overriding-browsermap-s-default-behaviour}

如果您希望自定义 `BrowserMap`  — 通过覆盖 `DeviceGroups` 或添加更多探测器 — 则您应创建自己的客户端库，在该库中嵌入 `browsermap.standard`客户端库。

此外，您还必须手动调用 `BrowserMap.forwardRequest()` 方法 `JavaScript` 代码。

>[!NOTE]
>
>有关客户端库集成的更多信息，请阅读 [使用客户端HTML库](/help/sites-developing/clientlibs.md) 中。

创建自定义后 `BrowserMap` 客户端库中，我们建议使用以下方法：

1. 创建 `browsermap.jsp` 文件

   ```xml
   <%@include file="/libs/foundation/global.jsp" %>
   <%@ taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
   <%@ page import="
       com.day.cq.wcm.api.variants.PageVariant,
       com.day.cq.wcm.api.variants.PageVariantsProvider,
       com.day.cq.wcm.api.devicedetection.DeviceIdentificationMode,
       com.day.cq.wcm.api.WCMMode"
   %>
   <%
       final PageVariantsProvider p = sling.getService(PageVariantsProvider.class);
       if(p == null) {
           throw new IllegalStateException("Missing PageVariantsProvider service");
       }
       for(PageVariant v : p.getVariants(currentPage, slingRequest)) {
           final String curVar = v.getAttributes().get("data-current-variant");
           String media = v.getAttributes().get("media");
           if (media != null) {
               media = media.replaceAll(" ", "");
           }
   %>
       <link
           rel="alternate"
           data-cq-role="site.variant"
           title="<%= xssAPI.encodeForHTMLAttr(v.getTitle()) %>"
           hreflang="<%= xssAPI.encodeForHTMLAttr(v.getAttributes().get("hreflang")) %>"
           media="<%= xssAPI.encodeForHTMLAttr(media) %>"
           href="<%= xssAPI.getValidHref(v.getURL()) %>"
           <% if(curVar != null) { %> data-current-variant="<%= curVar %>"<% } %>
       />
   <%
       }
       Boolean browserMapEnabled = true;
       final DeviceIdentificationMode dim = sling.getService(DeviceIdentificationMode.class);
       String[] selectors  = slingRequest.getRequestPathInfo().getSelectors();
       boolean isPortletRequest = false;
       for (int i = 0; i < selectors.length; i++) {
           if ("portlet".equals(selectors[i])) {
               isPortletRequest = true;
               break;
           }
       }
       if (isPortletRequest) {
           log.debug("Request was made by a portlet container - BrowserMap will not be embedded");
       } else {
           final WCMMode wcmMode = WCMMode.fromRequest(slingRequest);
           boolean shouldIncludeClientLib = false;
           if (WCMMode.EDIT != wcmMode && WCMMode.PREVIEW != wcmMode && WCMMode.DESIGN != wcmMode) {
               if (dim != null) {
                   final String mode = dim.getDeviceIdentificationModeForPage(currentPage);
                   shouldIncludeClientLib = DeviceIdentificationMode.CLIENT_SIDE.equals(mode);
                   if (shouldIncludeClientLib) {
                       browserMapEnabled = (Boolean) request.getAttribute("browsermap.enabled");
                       if (browserMapEnabled == null) {
                           browserMapEnabled = true;
                       }
                   }
               }
           }
   %>
           <c:if test="<%= !browserMapEnabled %>">
               <meta name="browsermap.enabled" content="false">
           </c:if>
           <c:if test="<%= shouldIncludeClientLib %>">
               <meta name="viewport" content="width=device-width, initial-scale=1.0">
               <cq:includeClientLib categories="browsermap.custom"/>
           </c:if>
   <%
       }
   %>
   ```

1. 包括 `broswermap.jsp` 文件。

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### 从某些页面中排除BrowserMap {#excluding-browsermap-from-certain-pages}

如果要从某些您不需要客户端检测的页面中排除BrowserMap库，可以添加请求属性：

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

这将使 `/libs/wcm/core/browsermap/browsermap.jsp` 脚本，以向将要生成 `BrowserMap` 不执行任何检测：

```xml
<meta name="browsermap.enabled" content="false">
```

### 测试网站的特定版本 {#testing-a-specific-version-of-a-web-site}

通常，BrowserMap脚本会始终将访客重定向到最合适的网站版本，通常会根据需要将访客重定向到桌面或移动设备网站。

您可以通过添加 `device` 参数。 以下URL将呈现Geometrixx Outdoors网站的移动版本。

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>的 `wcmmode` 参数设置为 `disabled` 以模拟发布实例的行为。

过期设备值存储在Cookie中，因此您无需添加 `device` 参数 `URL`.

因此，您需要调用相同的 `URL` 和 `device` 设置为 `browser` 以返回到网站的桌面版本。

>[!NOTE]
>
>BrowserMap将覆盖的设备值存储在名为 `BMAP_device`. 删除此Cookie将确保CQ根据您当前的设备（如桌面或移动设备）提供相应版本的网站。

## 移动设备请求处理 {#mobile-request-processing}

AEM处理由属于触控设备组的移动设备发出的请求，如下所示：

1. iPad向AEM发布实例发送请求，例如 `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEM确定所请求页面的网站是否为移动网站（通过检查是否为第一级页面） `/content/geometrixx_mobile` 扩展移动页面组件)。 如果是：
1. AEM会根据请求标头中的用户代理来查找设备功能。
1. AEM将设备功能映射到设备组并设置 `touch` 作为设备组选择器。
1. AEM将请求重定向到 `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. AEM将响应发送至iPad:

   * `products.touch.html` 是按常规方式呈现的，平易近人。
   * 渲染组件使用选择器来调整演示文稿。
   * AEM会自动将移动设备选择器添加到页面中的所有内部链接。

### 统计数据 {#statistics}

您可以获取有关移动设备向AEM服务器发出的请求数的一些统计信息。 可以划分请求数：

* 每个设备组和设备
* 每年、月和日

要查看统计信息，请执行以下操作：

1. 转到 **工具** 控制台。
1. 打开 **设备统计** 下面的页面 **工具** > **移动设备**.
1. 单击链接可查看特定年份、月份或日期的统计资料。

的 **统计** 页面如下所示：

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>的 **统计** 页面是在移动设备首次访问AEM并检测到时创建的。 在此之前，它不可用。

如果需要在统计信息中生成条目，可以按如下方式继续操作：

1. 使用移动设备或模拟器(例如，在Firefox上的https://chrispederick.com/work/user-agent-switcher/)。
1. 通过禁用创作模式(例如：
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

的 **统计** 页面现已可用。

### 支持“发送链接到朋友”链接的页面缓存 {#supporting-page-caching-for-send-link-to-a-friend-links}

移动设备页面通常可在Dispatcher上访问，因为设备组呈现的页面在页面URL中由设备组选择器进行区分，例如 `/content/mobilepage.touch.html`. 不会缓存对没有选择器的移动页面的请求，就像在本例中，设备检测操作并最终重定向到匹配的设备组（或“不匹配”）一样。 链接重写器会处理通过设备组选择器呈现的移动页面，该重写器会重写页面中的所有链接，以同时包含设备组选择器，从而阻止对已限定页面上的每次点击执行设备检测。

因此，您可能会遇到以下情况：

用户Alice将被重定向到 `coolpage.feature.html`，并将该URL发送给朋友Bob，该朋友Bob使用位于 `touch` 设备组。

如果 `coolpage.feature.html` 来自前端缓存，AEM将无法分析请求以找出移动选择器与新用户代理不匹配，并且Bob获得错误的表示形式。

要解决此问题，您可以在页面上包含一个简单的选择UI，最终用户可以在该UI中覆盖由AEM选择的设备组。 在上例中，页面上的链接（或图标）允许最终用户切换到 `coolpage.touch.html` 如果他认为他的设备足够用。
