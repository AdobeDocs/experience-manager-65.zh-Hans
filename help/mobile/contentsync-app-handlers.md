---
title: 开箱即用的应用程序处理程序
description: 按照本页上的说明，了解带AEM的Adobe PhoneGap Enterprise的现成处理程序。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 0%

---

# 开箱即用的应用程序处理程序{#out-of-the-box-app-handlers}

{{ue-over-mobile}}

请参阅以下有关开发内容同步处理程序的准则：

* 处理程序必须实现&#x200B;*com.day.cq.contentsync.handler.ContentUpdateHandler*（直接或扩展具有此功能的类）
* 处理程序可以扩展&#x200B;*com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* 如果处理程序更新了ContentSync缓存，则只能报告true。 错误地报告为true将允许AEM创建更新。
* 仅当内容发生实际更改时，处理程序才应更新缓存。 如果不需要白色，请不要写入缓存，并避免不必要的更新创建。

## 开箱即用的处理程序 {#out-of-the-box-handlers}

下面列出了现成的应用程序处理程序：

**mobileapppages**&#x200B;呈现应用程序页面。

* ***类型 — 字符串*** - mobileapppages
* ***路径 — 字符串*** — 页面的路径
* ***扩展 — 字符串*** — 应在请求中使用的扩展。 对于页面，这几乎总是&#x200B;*html*，但其他仍可实现。

* ***选择器 — 字符串*** — 可选的选择器，用点分隔。 渲染页面的移动版本的常见示例为&#x200B;*touch*。

* ***deep - Boolean*** — 可确定是否也应包含子页面的可选布尔属性。 默认值为&#x200B;*true。*

* ***includeImages - Boolean*** — 用于确定是否应包含图像的可选布尔属性。 默认值为&#x200B;*true*。

   * 默认情况下，只考虑包含资源类型为foundation/components/image的图像组件。

* ***includeVideos — 布尔值*** — 可选布尔值属性确定是否应包含视频。 默认值为&#x200B;*true*。

* ***includeModifiedPagesOnly - Boolean*** — 如果为false或省略，则渲染所有页面并检查渲染中的更新。 如果为true，则根据对页面lastModified的更改进行差值。
* ***+重写（节点）***
  ***- relativeParentPath — 字符串*** — 写入所有其他相对路径的路径。

>[!NOTE]
>
>受此处理程序影响的图像和视频组件的资源类型通过配置&#x200B;*com.adobe.cq.mobile.platform.impl.contentsync.handler*&#x200B;的属性进行设置。*MobilePagesUpdateHandler OSGi服务*。

**mobilepageassets**&#x200B;收集应用程序页面资源。

**mobilecontentlisting**&#x200B;列出了ContentSync zip的内容。 设备上的客户端js使用此项来执行AEM应用程序所需的初始文件复制。

应该将此处理程序添加到任何AEM Apps ContentSync配置中。

* ***类型 — 字符串 — mobilecontentlisting***
* ***path*** — 字符串 — 保留为空，必须存在才能被视为有效的处理程序，但路径被推断为当前的ContentSync缓存。 此值将被忽略。
* ***targetRootDirectory* -**字符串 — 要作为此处理程序的内容更新的目标根添加到路径的前缀。
* ContentSync要执行此处理程序的&#x200B;***订单 — 长* -**订单。 此数字应设置为高于所有其他处理程序，如100。 它应在传统内容处理程序之后运行。

```xml
{
  "files": [
    "config.xml",
    "res/screens/ios/screen-ipad-portrait-2x.png",
    "res/screens/ios/screen-ipad-landscape.png",
    "res/screens/ios/screen-iphone-portrait-2x.png",
    "res/screens/ios/screen-iphone-landscape.png",
    "res/screens/ios/screen-iphone-portrait.png",
    "apps/weretail-app/components/splash-page/clientlibs.css",
    ...
    "pge-content-packages.json"
  ],
  "count": 382,
  "lastModified": 1422902754733
}
```

**mobilecontentpackageslisting**&#x200B;列出给定应用中的AEM内容包以及要向其发出更新请求的serverURL。 这用于设备上的客户端js请求内容更新

该处理程序应在AEM App Shell ContentSync配置（具有page-type=app-instance的节点）上使用

* ***类型 — 字符串 — mobilecontentpackageslisting***
* ***path **-**String*** — 应用程序Shell的路径（节点的pge-type=app-instance）。
* ***targetRootDirectory — 字符串*** — 要作为此处理程序的内容更新的目标根添加到路径的前缀。
* ***顺序 — ContentSync执行此处理程序的顺序为* -**。 此数字应设置为高于所有其他处理程序，如100。 它应在传统内容处理程序之后运行。

>[!NOTE]
>
>以下代码块不是精确的实施，应用作参考示例：

```xml
{
  "content": [
    {
      "name": "en",
      "title": "We Retail Mobile App - English",
      "type": "CONTENT",
      "path": "/content/phonegap/weretail-outdoors/en",
      "updatePath": "/content/phonegap/weretail/en/jcr:content/pge-app/app-config"
    },
    {
      "name": "shell",
      "title": "We Retail Mobile App",
      "type": "INSTANCE",
      "path": "/content/phonegap/weretail-outdoors/shell",
      "updatePath": "/content/phonegap/weretail/shell/jcr:content/pge-app/app-config"
    }
  ],
  "serverURL": "http://localhost:4503/"
}
```

**widgetconfig**&#x200B;包含更新的config.xml，它将通过命令中心所做的任何编辑与提供的config.xml合并在一起。 如果未包含此处理程序，则通过管理界面更改的任何应用程序详细信息将不会包含在缓存中。

此处理程序应在AEM App Shell ContentSync配置（pge-type=[app-instance]的节点）上使用。

* ***类型 — 字符串* - **widgetconfig
* ***path **-**String*** — 任何应用程序Shell子节点（pge-type=[app-instance]的节点）的路径。
* ***targetRootDirectory — 字符串*** — 要作为此处理程序的内容更新的目标根添加到路径的前缀。
* ***targetIconDirectory — 字符串*** — 用于放置应用程序图标的目录

**mobileADBMobileConfigJSON**&#x200B;如果配置了AMS cloudservice，则包含ADBMobileConfig.JSON文件。

在编译时使用此插件配置AMS插件以提供分析支持。

该处理程序应在AEM App Shell ContentSync配置（具有page-type=app-instance的节点）上使用

* ***类型 — 字符串*** - mobileADBMobileConfigJSON
* ***path - String*** — 应用程序shell的路径（具有pge-type=app-instance的节点或扩展/libs/mobileapps/core/components/instance的RT）
* ***targetRootDirectory — 字符串*** — 要作为此处理程序的内容更新的目标根添加到路径的前缀

**notificationsconfig**&#x200B;提取设备上所需的通知配置。 这些属性提取自与应用程序关联的相应推送服务云服务配置。

将提取云服务jcr：content节点中的非AEM属性，并将其添加到&#x200B;**pge-notifications-config.json** JSON文件中，以包含在应用程序内容的www根中。

AEM属性是使用“cq”、“sling”或“jcr”进行命名空间的属性。 可以使用content-sync配置节点上的“excludeProperties”属性排除其他属性。

* ***类型 — 字符串*** - notificationsconfig
* ***excludeProperties — 字符串[]*** — 要排除的属性

**contentsyncconfigcontent**&#x200B;从现有ContentSync配置收集内容。

* ***类型 — 字符串*** - contentsyncconfigcontent
* ***path — 字符串*** — 指向以下项之一的路径：

   * 其他ContentSync配置
   * 到内容包（将使用其phonegap-exportTemplate属性来查找其ContentSync配置）
   * 到移动设备资源（应用程序内容将位于该资源下，如果这些内容包的page-includeInBuild属性为true，则使用phonegap-exportTemplate查找其ContentSync配置）

* ***autoCreateFirstUpdateBeforeImport - Boolean*** — 如果为true，则在导入之前在目标配置中创建初始&#x200B;**更新**（如果一次不存在）

* ***autoFillBeforeImport — 布尔值*** — 如果为true，则在导入之前更新/填充目标配置
* ***configSuffix - String*** — 一个字符串，附加到在app-content的“phonegap-exportTemplate”属性上指示的路径。 这可用于区分不同的导出模板。 例如，此属性可设置为&#x200B;**&quot;-dev&quot;**&#x200B;以指示应使用&#x200B;*&quot;/../../../appconfig-dev&quot;*（相对于&#x200B;*&quot;/../../../appconfig&quot;*）。

**app-assets**&#x200B;包含与应用程序实例关联的所有资源。 此处理程序将包含在指定路径下找到的任何资产，以及由应用程序实例的appAssetPath属性引用的任何资产。

* ***类型 — 字符串*** — 应用程序资产

* ***path **-**String*** — 应用程序实例下存储应用程序资产的位置的路径

**mobileappoffers**&#x200B;已为Personalization用例引入新的内容同步处理程序以呈现目标内容。 “mobileappoffers”处理程序知道如何呈现由内容作者创建的关联目标选件。 mobileappoffers处理程序扩展了抽象页面更新处理程序，因此许多属性是相似的。 mobileappoffers处理程序的详细信息具有以下属性。

mobileappsoffers处理程序扩展mobileappspages处理程序并添加以下属性：

* ***locationRoot — 字符串*** — 指定移动应用程序的位置
* ***includePageTypes — 字符串*** — 默认为支持cq/personalization/components/teaserpage和cq/personalization/components/offerproxy
* ***选择器 — 字符串*** — 应设置为tandt
* ***路径 — 字符串*** — 营销活动品牌的路径

**mobileappconfig** mobileappconfig内容同步处理程序提供了一种将JSON数据插入MobileAppsConfig.json的方法。 要注册提供程序类，开发人员将在提供程序列表中添加其MobileAppsInfoProvider类。 该处理程序将对MobileAppsInfoProviders列表进行迭代，并允许提供程序将数据插入生成的json文件中。 此处理程序支持的属性列表包括：

* ***path **-**String*** — 包含pge-type=app-instance的应用程序实例节点或扩展/libs/mobileapps/core/components/instance的RT的路径
* ***提供程序 — 字符串*** `[]` — 完全限定的MobileAppsInfoProviders列表
* ***targetRootDirectory — 字符串*** — 要将MobileAppsConfig.json文件写入到的目录。
* **fileName - String** — 要将JSON写入到的文件的可选名称，默认为MobileAppsConfig.json

可能有多个mobileappconfig处理程序分别配置了写入不同JSON文件的唯一提供程序集。

### 测试内容同步处理程序 {#testing-content-sync-handlers}

**检查完整性的步骤**&#x200B;清除缓存

* 清除缓存
* 运行处理程序（更新了缓存）
* 再次运行您的处理程序（不应更新缓存）

**调试步骤**

* 运行配置
* 在设备上导出配置或查看
* 如果渲染失败，请检查缺少&#x200B;*样式/资产/库*&#x200B;或检查&#x200B;*样式/资产/库*&#x200B;的错误路径

**日志记录**&#x200B;通过包`com.day.cq.contentsync`上的OSGI日志记录器配置启用ContentSync调试日志记录这将允许您跟踪运行了哪些处理程序以及它们是否更新了缓存和报告更新了缓存。

## 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM为Adobe PhoneGap Enterprise创作](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>要开始进行AEM Mobile应用程序开发，请单击[此处](/help/mobile/getting-started-aem-mobile.md)。
