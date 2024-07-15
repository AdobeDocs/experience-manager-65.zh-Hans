---
title: 叠加
description: Adobe Experience Manager使用叠加原理来让您扩展和自定义控制台和其他功能。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 1%

---

# 叠加{#overlays}

Adobe Experience Manager (AEM)（以及之前的CQ）长期以来使用叠加原理来允许您扩展和自定义[控制台](/help/sites-developing/customizing-consoles-touch.md)和其他功能（例如，[页面创作](/help/sites-developing/customizing-page-authoring-touch.md)）。

“叠加”是在许多上下文中使用的术语。 在此上下文中(扩展AEM)，叠加意味着采用预定义功能并将您自己的定义强加于此预定义功能之上（以自定义标准功能）。

在标准实例中，预定义功能保存在`/libs`下，建议在`/apps`分支下定义叠加（自定义项）。 AEM使用搜索路径查找资源，首先搜索`/apps`分支，然后搜索`/libs`分支（可以配置[搜索路径](#configuring-the-search-paths)）。 此机制意味着您的叠加（以及其中定义的自定义项）具有优先级。

自AEM 6.0起，对叠加的实施和使用方式进行了更改：

* AEM 6.0及更高版本 — 适用于[Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)相关的叠加图（即支持触摸的UI）

   * 方法

      * 在`/apps`下重新构建相应的`/libs`结构。

        这不需要1:1的副本，使用[Sling资源合并器](/help/sites-developing/sling-resource-merger.md)交叉引用所需的原始定义。 Sling资源合并器提供访问资源并将其与差异（差异）机制合并的服务。

      * 在`/apps`下，进行任何更改。

   * 优点

      * 对`/libs`下的更改更可靠。
      * 仅重新定义所需的内容。

* AEM 6.0之前的非Granite叠加和叠加

   * 方法

      * 将内容从`/libs`复制到`/apps`

        复制整个子分支，包括资产。

      * 在`/apps`下，进行任何更改。

   * 缺点

      * 虽然当某些内容在`/libs`下更改时，您的更改不会丢失，但您可能必须重新创建在`/apps`下的叠加中发生的某些更改。

>[!CAUTION]
>
>[Sling资源合并器](/help/sites-developing/sling-resource-merger.md)和相关方法只能与[Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)一起使用。 这意味着创建具有框架结构的叠加仅适用于支持触摸的标准用户界面。
>
>其他区域（包括经典UI）的叠加包括复制相应的节点和整个子结构，然后进行所需的更改。

叠加是进行许多更改的推荐方法，例如[配置控制台](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console)或[向侧面板中的资产浏览器创建选择类别](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser)（在创作页面时使用）。 它们必须是：

* ***不要*&#x200B;在`/libs`分支&#x200B;**中进行更改
您所做的任何更改都可能会丢失，因为每当您：

   * 在实例上升级
   * 应用修补程序
   * 安装功能包

* 它们将您的更改集中在一个位置；您可以更轻松地跟踪、迁移、备份或调试更改（如有必要）。

## 配置搜索路径 {#configuring-the-search-paths}

对于叠加图，交付的资源是检索到的资源和属性的汇总，具体取决于可以定义的搜索路径：

* 在&#x200B;**Apache Sling Resource Resolver Factory**&#x200B;的[OSGi配置](/help/sites-deploying/configuring-osgi.md)中定义的资源&#x200B;**解析程序搜索路径**。

   * 搜索路径的自上而下顺序指示其各自的优先级。
   * 在标准安装中，主默认值是`/apps`，`/libs` — 因此`/apps`的内容具有比`/libs`更高的优先级（即&#x200B;*覆盖*）。

* 两个服务用户需要对脚本存储位置具有JCR：READ访问权限。 这些用户是： components-search-service(由com.day.cq.wcm.coreto用于访问/缓存组件)和sling-scripting（由org.apache.sling.servlets.resolver用于查找servlet）。
* 还必须根据脚本放置位置（本示例中位于/etc、/libs或/apps下）来配置以下配置。

  ```
  PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
  resource.resolver.searchpath=["/etc","/apps","/libs"]
  resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
  ```

* 最后，还必须配置Servlet解析程序（在本例中，还要添加/etc）

  ```
  PID = org.apache.sling.servlets.resolver.SlingServletResolver
  servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
  ```

## 使用示例 {#example-of-usage}

在以下情况下介绍了一些示例：

* [自定义控制台](/help/sites-developing/customizing-consoles-touch.md)
* [自定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md)
