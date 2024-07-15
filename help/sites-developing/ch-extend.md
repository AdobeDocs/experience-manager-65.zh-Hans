---
title: 扩展 ContextHub
description: 当提供的ContextHub存储和模块不符合您的解决方案要求时，定义这些存储和模块的新类型
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 41898fa7-a369-4c63-8ccb-69eb3fa146a1
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# 扩展 ContextHub{#extending-contexthub}

在提供的ContextHub存储和模块不符合您的解决方案要求时，定义新类型的ContextHub存储和模块。

## 创建自定义商店候选 {#creating-custom-store-candidates}

ContextHub存储是从已注册的存储候选区创建的。 要创建自定义商店，请创建并注册商店候选商店。

包含创建和注册商店候选的代码的JavaScript文件必须包含在[客户端库文件夹](/help/sites-developing/clientlibs.md#creating-client-library-folders)中。 文件夹的类别必须符合以下模式：

```xml
contexthub.store.[storeType]
```

类别的`[storeType]`部分是在其中注册存储候选项的`storeType`。 （请参阅[注册ContextHub存储候选项](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)）。 例如，对于`contexthub.mystore`的storeType，客户端库文件夹的类别必须为`contexthub.store.contexthub.mystore`。

### 创建ContextHub存储候选 {#creating-a-contexthub-store-candidate}

若要创建商店候选，请使用[`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent)函数扩展一个基础商店：

* [&#39;ContextHub.Store.PersistedStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [&#39;ContextHub.Store.SessionStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [&#39;ContextHub.Store.JSONPStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [&#39;ContextHub.Store.PersistedJSONPStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

每个基存储区扩展[`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core)存储。

以下示例创建`ContextHub.Store.PersistedStore`存储候选的最简单扩展：

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

实际上，您的自定义商店候选者定义了其他功能或覆盖商店的初始配置。 `/libs/granite/contexthub/components/stores`下的存储库中安装了多个[示例存储候选项](/help/sites-developing/ch-samplestores.md)。 要学习这些示例，请使用CRXDE Lite打开JavaScript文件。

### 注册ContextHub存储候选 {#registering-a-contexthub-store-candidate}

注册存储候选项，以将其与ContextHub框架集成并允许从中创建存储。 要注册存储候选，请使用`ContextHub.Utils.storeCandidates`类的[`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)函数。

注册候选商店时，需提供商店类型的名称。 从候选项创建存储时，可以使用存储类型标识存储所基于的候选项。

注册候选商店时，需指定其优先级。 当使用与已注册的存储候选相同的存储类型来注册存储候选时，使用具有较高优先级的候选。 因此，您可以使用新实施覆盖现有商店候选。

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

通常只需要一个候选，并且优先级可以设置为`0`。 但是，如果您感兴趣，可以了解[更多高级注册，](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)，这允许根据JavaScript条件(`applies`)和候选优先级选择少数商店实现之一。

## 创建ContextHub UI模块类型 {#creating-contexthub-ui-module-types}

当随ContextHub](/help/sites-developing/ch-samplemodules.md)安装的[模块类型不符合您的要求时，创建自定义UI模块类型。 要创建UI模块类型，请通过扩展`ContextHub.UI.BaseModuleRenderer`类并在`ContextHub.UI`中注册来创建UI模块渲染器。

要创建UI模块渲染器，请创建包含用于渲染UI模块的逻辑的`Class`对象。 类至少必须执行以下操作：

* 扩展`ContextHub.UI.BaseModuleRenderer`类。 此类是所有UI模块渲染器的基本实现。 `Class`对象定义了一个名为`extend`的属性，您使用该属性将此类命名为正在扩展的类。

* 提供默认配置。 创建`defaultConfig`属性。 此属性是一个对象，其中包含为[`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) UI模块定义的属性以及您需要的任何其他属性。

`ContextHub.UI.BaseModuleRenderer`的源位于/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js。 要注册渲染器，请使用`ContextHub.UI`类的[`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender)方法。 提供模块类型的名称。 当管理员基于此渲染器创建UI模块时，他们会指定此名称。

在自动执行的匿名函数中创建并注册renderer类。 以下示例基于contexthub.browserinfo UI模块的源代码。 此UI模块是`ContextHub.UI.BaseModuleRenderer`类的简单扩展。

```xml
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

包含创建和注册渲染程序的代码的JavaScript文件必须包含在[客户端库文件夹](/help/sites-developing/clientlibs.md#creating-client-library-folders)中。 文件夹的类别必须符合以下模式：

```xml
contexthub.module.[moduleType]
```

类别的`[moduleType]`部分是在其中注册了模块渲染器的`moduleType`。 例如，对于`contexthub.browserinfo`的`moduleType`，客户端库文件夹的类别必须为`contexthub.module.contexthub.browserinfo`。
