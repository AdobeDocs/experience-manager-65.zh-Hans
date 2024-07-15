---
title: 配置 ContextHub
description: 了解如何配置Adobe Experience Manager的Context Hub以个性化您的体验。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 61208bd5-475b-40be-ba00-31bbbc952adf
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 0%

---

# 配置 ContextHub {#configuring-contexthub}

ContextHub是一个用于存储、操作和呈现上下文数据的框架。 有关ContextHub的详细信息，请参阅[开发人员文档](/help/sites-developing/contexthub.md)。 ContextHub在触屏UI中替换了[Client Context](/help/sites-administering/client-context.md)。

配置[ContextHub](/help/sites-developing/contexthub.md)工具栏以控制它是否以预览模式显示、创建ContextHub存储以及使用触控优化UI添加UI模块。

## 禁用ContextHub {#disabling-contexthub}

默认情况下，AEM安装中会启用ContextHub。 可以禁用ContextHub以阻止其加载js/css和初始化。

<!--
There are two options to disable ContextHub:

* Edit the ContextHub's configuration and check the option **Disable ContextHub**

    1. In the rail click **Tools &gt; Sites &gt; ContextHub**
    1. Click the appropriate **Configuration Container**
    1. Select the **ContextHub Configuration** and click **Edit Selected Element**
    1. Click **Disable ContextHub** and click **Save**

or
-->

* 使用CRXDE Lite将`/libs/settings/cloudsettings/legacy/contexthub`下的属性`disabled`设置为&#x200B;**true**

>[!NOTE]
>
>[由于AEM 6.4中的存储库重组，](/help/sites-deploying/repository-restructuring.md) ContextHub配置的位置已从`/etc/cloudsettings`更改为：
>
>* `/libs/settings/cloudsettings`
>* `/conf/global/settings/cloudsettings`
>* `/conf/<tenant>/settings/cloudsettings`

## 显示和隐藏ContextHub UI {#showing-and-hiding-the-contexthub-ui}

将AdobeGranite ContextHub OSGi服务配置为在您的页面上显示或隐藏[ContextHub UI](/help/sites-authoring/ch-previewing.md)。 此服务的PID为`com.adobe.granite.contexthub.impl.ContextHubImpl.`

要配置服务，您可以使用[Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)或使用存储库中的[JCR节点](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)：

* **Web控制台：**&#x200B;要显示UI，请选择“显示UI”属性。 要隐藏UI，请清除隐藏UI属性。
* **JCR节点：**&#x200B;要显示UI，请将布尔值`com.adobe.granite.contexthub.show_ui`属性设置为`true`。 要隐藏UI，请将属性设置为`false`。

显示ContextHub UI时，它仅显示在AEM创作实例上的页面上。 UI未出现在发布实例的页面上。

## 添加ContextHub UI模式和模块 {#adding-contexthub-ui-modes-and-modules}

配置在预览模式下显示在ContextHub工具栏中的UI模式和模块：

* UI模式：相关模块组
* 模块：从存储中公开上下文数据并使作者能够处理上下文的小部件

UI模式在工具栏左侧显示为一系列图标。 选中后，UI模式的模块将显示在右侧。

![chlimage_1-319](assets/chlimage_1-319.png)

图标是来自[Coral UI图标库](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons)的引用。

### 添加UI模式 {#adding-a-ui-mode}

添加UI模式以分组相关的ContextHub模块。 在创建UI模式时，您需要提供显示在ContextHub工具栏中的标题和图标。

1. 在Experience Manager边栏中，单击工具>站点>上下文中心。
1. 单击默认配置容器。
1. 单击上下文中心配置。
1. 单击创建按钮，然后单击Context Hub UI模式。

   ![chlimage_1-320](assets/chlimage_1-320.png)

1. 提供以下属性的值：

   * 用户界面模式标题：标识用户界面模式的标题
   * 模式图标：要使用的[Coral UI图标](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons)的选择器，例如`coral-Icon--user`
   * 启用：选择此项可在ContextHub工具栏中显示UI模式

1. 单击“保存”。

### 添加UI模块 {#adding-a-ui-module}

将ContextHub UI模块添加到UI模式，以便该模块显示在ContextHub工具栏中，用于预览页面内容。 添加UI模块时，您将创建一个已在ContextHub中注册的模块类型实例。 要添加UI模块，您必须知道关联模块类型的名称。

AEM提供了一个基本UI模块类型以及多个示例UI模块类型，您可以基于这些类型构建UI模块。 下表提供了每种类型的简要说明。 有关开发自定义用户界面模块的信息，请参阅[创建ContextHub UI模块](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)。

UI模块属性包括一个详细配置，您可以在其中提供特定于模块的属性的值。 您以JSON格式提供详细配置。 表中的模块类型列提供了指向每个UI模块类型所需JSON代码信息的链接。

| 模块类型 | 描述 | 存储 |
|---|---|---|
| [contexthub.base](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) | 通用UI模块类型 | 在UI模块属性中配置 |
| [contexthub.browserinfo](/help/sites-developing/ch-samplemodules.md#contexthub-browserinfo-ui-module-type) | 显示有关浏览器的信息 | surferinfo |
| [contexthub.datetime](/help/sites-developing/ch-samplemodules.md#contexthub-datetime-ui-module-type) | 显示日期和时间信息 | 日期时间 |
| [contexthub.device](/help/sites-developing/ch-samplemodules.md#contexthub-device-ui-module-type) | 显示客户端设备 | 模拟器 |
| [contexthub.location](/help/sites-developing/ch-samplemodules.md#contexthub-location-ui-module-type) | 显示客户端的纬度和经度，以及地图上的位置。 允许您更改位置。 | 地理位置 |
| [contexthub.screen-orientation](/help/sites-developing/ch-samplemodules.md#contexthub-screen-orientation-ui-module-type) | 显示设备的屏幕方向（横向或纵向） | 模拟器 |
| [contexthub.tagcloud](/help/sites-developing/ch-samplemodules.md#contexthub-tagcloud-ui-module-type) | 显示有关页面标记的统计信息 | tagcloud |
| [granite.profile](/help/sites-developing/ch-samplemodules.md#granite-profile-ui-module-type) | 显示当前用户的配置文件信息，包括authorizableID、displayName和familyName。 可以更改displayName和familyName的值。 | 侧面像 |

1. 在Experience Manager边栏中，单击工具>站点> ContextHub。
1. 单击要向其添加UI模块的配置容器。
1. 单击或键入要将UI模块添加到其中的ContextHub配置。
1. 单击要向其中添加UI模块的UI模式。
1. 单击“创建”按钮，然后单击“ContextHub UI模块（通用）”。

   ![chlimage_1-321](assets/chlimage_1-321.png)

1. 提供以下属性的值：

   * 用户界面模块标题：标识用户界面模块的标题
   * 模块类型：模块类型
   * 已启用：选择此选项可在ContextHub工具栏中显示UI模块

1. （可选）要覆盖默认存储配置，请输入要配置UI模块的JSON对象。
1. 单击“保存”。

## 创建ContextHub存储 {#creating-a-contexthub-store}

创建Context Hub存储以保留用户数据并根据需要访问数据。 ContextHub存储基于已注册的存储候选项。 在创建存储时，需要存储候选注册到的storeType的值。 （请参阅[创建自定义商店候选](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)。）

### 详细存储配置 {#detailed-store-configuration}

在配置存储时，细节配置属性允许您提供特定于存储的属性的值。 该值基于存储的`init`函数的`config`参数。 因此，是否需要提供此值，以及此值的格式，取决于存储。

详细信息配置属性的值是JSON格式的`config`对象。

### 示例存储候选 {#sample-store-candidates}

AEM提供了以下存储候选项示例，您可以根据它们创建存储。

| 存储类型 | 描述 |
|---|---|
| [aem.segmentation](/help/sites-developing/ch-samplestores.md#aem-segmentation-sample-store-candidate) | 存储已解析和未解析的ContextHub区段。 自动从ContextHub SegmentManager检索区段 |
| [aem.resolvedsegments](/help/sites-developing/ch-samplestores.md#aem-resolvedsegments-sample-store-candidate) | 存储当前已解析的区段。 侦听ContextHub SegmentManager服务以自动更新存储 |
| [contexthub.geolocation](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) | 存储浏览器位置的纬度和经度。 |
| [contexthub.datetime](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) | 存储浏览器位置的当前日期、时间和季节 |
| [granite.emulators](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) | 为多个设备定义属性和功能，并检测当前的客户端设备 |
| [contexthub.generic-jsonp](/help/sites-developing/ch-samplestores.md#contexthub-generic-jsonp-sample-store-candidate) | 从JSONP服务检索和存储数据 |
| [granite.profile](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) | 存储当前用户的配置文件数据 |
| [contexthub.surferinfo](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) | 存储有关客户端的信息，如设备信息、浏览器类型和窗口方向 |
| [contexthub.tagcloud](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) | 存储页面标记和标记计数 |

1. 在Experience Manager边栏中，单击工具>站点> ContextHub。
1. 单击默认配置容器。
1. 单击Contexthub配置
1. 要添加存储，请单击“创建”图标，然后单击ContexHub存储配置。

   ![chlimage_1-322](assets/chlimage_1-322.png)

1. 提供基本配置属性的值，然后单击下一步：

   * **配置标题：**&#x200B;标识存储区的标题
   * **存储类型：**&#x200B;作为存储基础的存储候选的storeType属性的值
   * **必需：**&#x200B;选择
   * **已启用：**&#x200B;选择以启用存储

1. （可选）要覆盖默认存储配置，请在详细信息配置(JSON)框中输入JSON对象。
1. 单击“保存”。

## 示例：使用JSONP服务  {#example-using-a-jsonp-service}

此示例说明如何在UI模块中配置存储区并显示数据。 在此示例中，jsontest.com站点的MD5服务用作存储的数据源。 该服务以JSON格式返回给定字符串的MD5哈希代码。

contexthub.generic-jsonp存储已配置为存储服务调用`https://md5.jsontest.com/?text=%22text%20to%20md5%22`的数据。 该服务会返回以下数据，这些数据显示在UI模块中：

```xml
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### 创建contexthub.generic-jsonp存储 {#creating-a-contexthub-generic-jsonp-store}

Contexthub.generic-jsonp示例存储候选函数允许您从返回JSON数据的JSONP服务或Web服务中检索数据。 对于此存储候选项，请使用存储配置提供关于要使用的JSONP服务的详细信息。

`ContextHub.Store.JSONPStore` JavaScript类的[init](/help/sites-developing/contexthub-api.md#init-name-config)函数定义了一个初始化此商店候选的`config`对象。 `config`对象包含一个`service`对象，其中包含有关JSONP服务的详细信息。 要配置存储，请以JSON格式提供`service`对象作为详细信息配置属性的值。

要保存来自jsontest.com站点的MD5服务的数据，请使用[使用以下属性创建ContextHub存储区](/help/sites-developing/ch-configuring.md#creating-a-contexthub-store)中的过程：

* **配置标题：** md5
* **存储类型：** contexthub.generic-jsonp
* **必需：**&#x200B;选择
* **已启用：**&#x200B;选择
* **详细配置(JSON)：**

  ```xml
  {
   "service": {
   "jsonp": false,
   "timeout": 1000,
   "ttl": 1800000,
   "secure": false,
   "host": "md5.jsontest.com",
   "port": 80,
   "params":{
   "text":"text to md5"
       }
     }
   }
  ```

### 为md5数据添加UI模块 {#adding-a-ui-module-for-the-md-data}

将UI模块添加到ContextHub工具栏，以显示存储在示例md5存储中的数据。 在此示例中，contexthub.base模块用于生成以下UI模块：

![chlimage_1-323](assets/chlimage_1-323.png)

使用[添加UI模块](#adding-a-ui-module)中的过程将UI模块添加到现有UI模式，如示例Perona UI模式。 对于UI模块，请使用以下属性值：

* **UI模块标题：** MD5
* **模块类型：** contexthub.base
* **详细配置(JSON)：**

  ```xml
  {
   "icon": "coral-Icon--data",
   "title": "MD5 Converstion",
   "storeMapping": { "md5": "md5" },
   "template": "<p> {{md5.original}}</p>;
                <p>{{md5.md5}}</p>"
  }
  ```

## 调试Contexthub {#debugging-contexthub}

可以启用ContextHub的调试模式以进行疑难解答。 调试模式可通过ContextHub配置或CRXDE启用。

### 通过配置 {#via-the-configuration}

编辑ContextHub的配置并选中选项&#x200B;**调试**

1. 在边栏中，单击&#x200B;**工具>站点> ContextHub**
1. 单击默认&#x200B;**配置容器**
1. 选择&#x200B;**ContextHub配置**&#x200B;并单击&#x200B;**编辑所选元素**
1. 单击&#x200B;**调试**，然后单击&#x200B;**保存**

### 通过CRXDE {#via-crxde}

使用CRXDE Lite将属性`debug`设置为&#x200B;**true**，位于：

* `/conf/global/settings/cloudsettings`或
* `/conf/<tenant>/settings/cloudsettings`

>[!NOTE]
>
>对于ContextHub配置，仍位于其旧路径下，设置`debug property`的位置为`/libs/settings/cloudsettings/legacy/contexthub`。

### 静默模式 {#silent-mode}

静默模式会隐藏所有调试信息。 与可为每个ContextHub配置单独设置的普通调试选项不同，静默模式是一种全局设置，其优先于ContextHub配置级别上的任何调试设置。

这对于您根本不需要任何调试信息的发布实例非常有用。 由于它是全局设置，因此可通过OSGi启用。

1. 在`http://<host>:<port>/system/console/configMgr`处打开&#x200B;**Adobe Experience Manager Web控制台配置**
1. 搜索&#x200B;**AdobeGranite ContextHub**
1. 单击配置&#x200B;**AdobeGranite ContextHub**&#x200B;以编辑其属性
1. 选中选项&#x200B;**静默模式**&#x200B;并单击&#x200B;**保存**

## 升级后恢复ContextHub配置 {#recovering-contexthub-configurations-after-upgrading}

执行[升级到AEM](/help/sites-deploying/upgrade.md)时，会备份ContextHub配置并将其存储在安全位置。 在升级过程中，将安装默认ContextHub配置，并替换现有配置。 要保留所做的任何更改或添加，需要备份。

ContextHub配置存储在位于以下节点下名为`contexthub`的文件夹中：

* `/conf/global/settings/cloudsettings`
* `/conf/<tenant>/settings/cloudsettings`

升级后，备份存储在名为`contexthub`的文件夹下，该文件夹位于名为的节点下：

`/conf/global/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx`或
`/conf/<tenant>/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx`

节点名称的`yyyymmdd`部分是执行升级的日期。

要恢复ContextHub配置，请使用CRXDE Lite将`default-pre-upgrade_yyyymmdd_xxxxxx`节点下代表您的商店、UI模式和UI模块的节点复制到以下位置：

* `/conf/global/settings/cloudsettings`或
* `/conf/<tenant>/settings/cloudsettings`
