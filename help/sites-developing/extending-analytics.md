---
title: 扩展事件跟踪
description: AEM Analytics允许您跟踪用户在您网站上的交互
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: a71d20e6-0321-4afb-95fe-6de8b7b37245
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# 扩展事件跟踪{#extending-event-tracking}

AEM Analytics允许您跟踪用户在您网站上的交互。 作为开发人员，您可能需要：

* 跟踪访客与您的组件交互的方式。 这可以用完成 [自定义事件。](#custom-events)
* [访问ContextHub中的值](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).
* [添加记录回调](#adding-record-callbacks).

>[!NOTE]
>
>这些信息基本上是通用的，但它使用 [Adobe Analytics](/help/sites-administering/adobeanalytics.md) 以了解具体示例。
>
>有关开发组件和对话框的一般信息，请参见 [开发组件](/help/sites-developing/components.md).

## 自定义事件 {#custom-events}

自定义事件可跟踪依赖于页面上特定组件可用性的任何内容。 这还包括特定于模板的事件，因为页面组件会被视为另一个组件。

### 在页面加载时跟踪自定义事件 {#tracking-custom-events-on-page-load}

这可以使用伪属性来完成 `data-tracking` （对于向后兼容性，仍支持older record属性）。 您可以将其添加到任何HTML标记中。

的语法 `data-tracking` 是

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

您可以将任意数量的键值对作为第二个参数（称为有效负载）传递。

示例可能如下所示：

```xml
<span data-tracking="{event:'blogEntryView',
                                values:{
                                   'blogEntryContentType': 'blog',
                                   'blogEntryUniqueID': '<%= xssAPI.encodeForJSString(entry.getId()) %>',
                                   'blogEntryTitle': '<%= xssAPI.encodeForJSString(entry.getTitle()) %>',
                                   'blogEntryAuthor':'<%= xssAPI.encodeForJSString(entry.getAuthor()) %>',
                                   'blogEntryPageLanguage':'<%= currentPage.getLanguage(true) %>'
                                },
                                componentPath:'myapp/component/mycomponent'}">
</span>
```

在页面加载时，全部 `data-tracking` 属性将被收集并添加到ContextHub的事件存储中，可在其中映射到Adobe Analytics事件。 Adobe Analytics不会跟踪未映射的事件。 请参阅 [正在连接到Adobe Analytics](/help/sites-administering/adobeanalytics.md) 以了解有关映射事件的更多详细信息。

### 在页面加载后跟踪自定义事件 {#tracking-custom-events-after-page-load}

要跟踪加载页面后发生的事件（如用户交互），请使用 `CQ_Analytics.record` JavaScript函数：

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

位置

* `events` 是字符串或字符串数组（用于多个事件）。

* `values` 包含要跟踪的所有值
* `collect` 是可选的，将返回一个包含事件和数据对象的数组。
* `options` 是可选的并包含链接跟踪选项，如HTML元素 `obj` 和 ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`.

* `componentPath` 是必需属性，建议将其设置为 `<%=resource.getResourceType()%>`

例如，使用以下定义，用户单击 **跳转到顶部** 链接将导致两个事件， `jumptop` 和 `headlineclick`，将被触发：

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## 访问ContextHub中的值 {#accessing-values-in-the-contexthub}

ContextHub JavaScript API具有 `getStore(name)` 返回指定存储（如果可用）的函数。 商店有 `getItem(key)` 返回指定键值（如果可用）的函数。 使用 `getKeys()` 函数可以检索特定存储的已定义键的数组。

通过使用，绑定一个函数，可以通知您存储上的值发生了更改 `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)` 函数。

要接收有关ContextHub初始可用性的通知，最佳方式是使用 `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);` 函数。

**ContextHub的其他事件：**

所有商店都准备就绪：

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

存储特定：

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>另请参阅完整的 [ContextHub API参考](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## 添加记录回调 {#adding-record-callbacks}

使用函数注册回调之前和之后 `CQ_Analytics.registerBeforeCallback(callback,rank)` 和 `CQ_Analytics.registerAfterCallback(callback,rank)`.

这两个函数都将函数作为第一个参数，并将排名作为第二个参数，这指定了执行回调的顺序。

如果回调返回false，则不会执行执行链中后续的回调。
