---
title: 将Adobe Analytics跟踪添加到组件
description: 将Adobe Analytics跟踪添加到组件
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: e6c1258c-81d5-48e4-bdf1-90d7cc13a22d
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 0%

---

# 将Adobe Analytics跟踪添加到组件{#adding-adobe-analytics-tracking-to-components}

## 在页面组件中包含Adobe Analytics模块 {#including-the-adobe-analytics-module-in-a-page-component}

页面模板组件(例如， `head.jsp, body.jsp`)需要JSP include来加载ContextHub和Adobe Analytics集成(它是Cloud Services的一部分)。 全部包括加载JavaScript文件。

ContextHub条目应直接包含在 `<head>` 标签中，而Cloud Services应包含在 `<head>` 并且早于 `</body>` 部分；例如：

```xml
<head>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub" />
...
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
...
</head>
<body>
...
    <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
</body>
```

此 `contexthub` 您插入到的脚本位于 `<head>` 元素将ContextHub功能添加到页面。

此 `cloudservices` 您在中添加的脚本 `<head>` 和 `<body>` 部分适用于添加到该页面的cloud services配置。 (如果页面使用多个Cloud Services配置，则必须仅包含ContextHub jsp和Cloud Servicesjsp一次。)

将Adobe Analytics框架添加到页面时， `cloudservices` 脚本会生成与Adobe Analytics相关的JavaScript和对客户端库的引用，类似于以下示例：

```xml
<div class="sitecatalyst cloudservice">
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/util.js"></script>
<script type="text/javascript" src="/content/geometrixx-outdoors/_jcr_content/analytics.sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/mac/mac-sc.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/plugins.js"></script>
<script type="text/javascript">
<!--
CQ_Analytics.Sitecatalyst.frameworkComponents = ['foundation/components/page'];
/**
 * Sets Adobe Analytics variables accordingly to mapped components. If <code>options</code>
 * object is provided only variables matching the options.componentPath are set.
 *
 * @param {Object} options Parameter object from CQ_Analytics.record() call. Optional.
 */
CQ_Analytics.Sitecatalyst.updateEvars = function(options) {
    this.frameworkMappings = [];
 this.frameworkMappings.push({scVar:"pageName",cqVar:"pagedata.title",resourceType:"foundation/components/page"});
    for (var i=0; i<this.frameworkMappings.length; i++){
  var m = this.frameworkMappings[i];
  if (!options || options.compatibility || (options.componentPath == m.resourceType)) {
   CQ_Analytics.Sitecatalyst.setEvar(m);
  }
    }
}

CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
 var collect = true;
    var lte = s.linkTrackEvents;
    s.pageName="content:geometrixx-outdoors:en";
    CQ_Analytics.Sitecatalyst.collect(collect);
    if (collect) {
  CQ_Analytics.Sitecatalyst.updateEvars();
     /************* DO NOT ALTER ANYTHING BELOW THIS LINE ! **************/
     var s_code=s.t();if(s_code)document.write(s_code);
     s.linkTrackEvents = lte;
     if(s.linkTrackVars.indexOf('events')==-1){delete s.events};
     $CQ(document).trigger("sitecatalystAfterCollect");
    }
});
//-->
</script>
<script type="text/javascript">
<!--
if(navigator.appVersion.indexOf('MSIE')>=0)document.write(unescape('%3C')+'\!-'+'-')
//-->
</script>
<noscript><img src="https://daydocumentation.112.2o7.net/b/ss/daydocumentation/1/H.25--NS/1380120772954?cdp=3&gn=content%3Ageometrixx-outdoors%3Aen" height="1" width="1" border="0" alt=""/></noscript>
<span data-tracking="{event:'pageView', values:{}, componentPath:'foundation/components/page'}"></span>
<div id="cq-analytics-texthint" style="background:white; padding:0 10px; display:none;">
 <h3 class="cq-texthint-placeholder">Component clientcontext is missing or misplaced.</h3>
</div>
<script type="text/javascript">
$CQ(function(){
 if( CQ_Analytics &&
  CQ_Analytics.ClientContextMgr &&
  !CQ_Analytics.ClientContextMgr.isConfigLoaded )
  {
   $CQ("#cq-analytics-texthint").show();
  }
});
</script>
</div>
```

所有AEM示例站点(如Geometrixx Outdoors)都包含此代码。

### sitecatalystAfterCollect事件 {#the-sitecatalystaftercollect-event}

此 `cloudservices` 脚本触发 `sitecatalystAfterCollect` 事件：

```
$CQ(document).trigger("sitecatalystAfterCollect");
```

触发此事件即表示页面跟踪已完成。 如果在此页面上执行其他跟踪操作，则应侦听此事件，而不是文档加载或文档就绪事件。 使用 `sitecatalystAfterCollect` 事件可避免冲突或其他不可预测的行为。

>[!NOTE]
>
>此 `/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js` 库中包含来自Adobe Analytics的代码 `s_code.js` 文件。

## 为自定义组件实施Adobe Analytics跟踪 {#implementing-adobe-analytics-tracking-for-custom-components}

启用您的AEM组件以与Adobe Analytics框架交互。 然后，配置框架，以便Adobe Analytics跟踪组件数据。

在编辑框架时，与Adobe Analytics框架交互的组件会显示在SideKick中。 将组件拖到框架中后，将显示组件属性，然后可以使用Adobe Analytics属性映射这些属性。 (请参阅 [设置基本跟踪的框架](/help/sites-administering/adobeanalytics-connect.md#creating-a-adobe-analytics-framework).)

当组件具有名为的子节点时，组件可以与Adobe Analytics框架进行交互 `analytics`. 此 `analytics` 节点具有以下属性：

* `cq:trackevents`：标识组件公开的CQ事件。 （请参阅自定义事件。）
* `cq:trackvars`：命名通过Adobe Analytics属性映射的CQ变量。
* `cq:componentName`：Sidekick中显示的组件的名称。
* `cq:componentGroup`：Sidekick中包含组件的组。

组件JSP中的代码会将JavaScript添加到触发跟踪的页面，并定义跟踪的数据。 JavaScript中使用的事件名称和数据名称必须匹配 `analytics` 节点属性。

* 使用data-tracking属性可在页面加载时跟踪事件数据。 (请参阅 [跟踪页面加载中的自定义事件](/help/sites-developing/extending-analytics.md#tracking-custom-events-on-page-load).)
* 使用CQ_Analytics.record函数可在用户与页面功能交互时跟踪事件数据。 (请参阅 [在页面加载后跟踪自定义事件](/help/sites-developing/extending-analytics.md#tracking-custom-events-after-page-load).)

当您使用这些数据跟踪方法时，Adobe Analytics集成模块会自动执行对Adobe Analytics的调用，以记录事件和数据。

### 示例：跟踪topnav点击量 {#example-tracking-topnav-clicks}

扩展Foundation Topnav组件，以便Adobe Analytics跟踪页面顶部的导航链接点击量。 单击导航链接时，Adobe Analytics会记录所单击的链接以及所单击的页面。

以下过程要求您已执行以下任务：

* 已创建CQ应用程序。
* 创建了Adobe Analytics配置和Adobe Analytics Framework。

#### 复制topnav组件 {#copy-the-topnav-component}

将topnav组件复制到CQ应用程序。 此过程要求您的应用程序在CRXDE Lite中设置。

1. 右键单击 `/libs/foundation/components/topnav` 节点，然后单击复制。
1. 右键单击应用程序文件夹下的“组件”文件夹，然后单击“粘贴”。
1. 单击全部保存。

#### 将topnav与Adobe Analytics框架集成 {#integrating-topnav-with-the-adobe-analytics-framework}

配置topnav组件并编辑JSP文件以定义跟踪事件和数据。

1. 右键单击topnav节点，然后单击“创建”>“创建节点”。 指定以下属性值，然后单击“确定”：

   * 名称: `analytics`
   * 类型: `nt:unstructured`

1. 将以下属性添加到Analytics节点，以便您可以命名跟踪事件：

   * 名称：cq：trackevents
   * 类型：字符串
   * 值： topnavClick

1. 将以下属性添加到Analytics节点，以便您可以将数据变量命名为：

   * 名称：cq：trackvars
   * 类型：字符串
   * 值： topnavTarget，topnavLocation

1. 将以下属性添加到Analytics节点以命名要Sidekick的组件：

   * 名称：cq：componentName
   * 类型：字符串
   * 值： topnav (tracking)

1. 将以下属性添加到Analytics节点以命名要Sidekick的组件组：

   * 名称：cq：componentGroup
   * 类型：字符串
   * 值：常规

1. 单击全部保存。
1. 打开 `topnav.jsp` 文件。
1. 在元素中，添加以下属性：

   ```xml
   onclick = "tracknav('<%= child.getPath() %>.html')"
   ```

1. 在页面底部，添加以下JavaScript代码：

   ```xml
   <script type="text/javascript">
       function tracknav(target) {
               if (CQ_Analytics.Sitecatalyst) {
                   CQ_Analytics.record({
                       event: 'topnavClick',
                       values: {
                           topnavTarget: target,
                           topnavLocation:'<%=currentPage.getPath() %>.html'
                       },
                       componentPath: '<%=resource.getResourceType()%>'
                   });
               }
       }
   </script>
   ```

1. 单击全部保存。

的内容 `topnav.jsp` 文件应如下所示：

```xml
<%@page session="false"%><%--
  Copyright 1997-2008 Day Management AG
  Barfuesserplatz 6, 4001 Basel, Switzerland
  All Rights Reserved.

  This software is the confidential and proprietary information of
  Day Management AG, ("Confidential Information"). You shall not
  disclose such Confidential Information and shall use it only in
  accordance with the terms of the license agreement you entered into
  with Day.

  ==============================================================================

  Top Navigation component

  Draws the top navigation

--%><%@include file="/libs/foundation/global.jsp"%><%
%><%@ page import="java.util.Iterator,
        com.day.text.Text,
        com.day.cq.wcm.api.PageFilter,
        com.day.cq.wcm.api.Page,
        com.day.cq.commons.Doctype,
        org.apache.commons.lang3.StringEscapeUtils" %><%

    // get starting point of navigation
    long absParent = currentStyle.get("absParent", 2L);
    String navstart = Text.getAbsoluteParent(currentPage.getPath(), (int) absParent);

    //if not deep enough take current node
    if (navstart.equals("")) navstart=currentPage.getPath();

    Resource rootRes = slingRequest.getResourceResolver().getResource(navstart);
    Page rootPage = rootRes == null ? null : rootRes.adaptTo(Page.class);
    String xs = Doctype.isXHTML(request) ? "/" : "";
    if (rootPage != null) {
        Iterator<Page> children = rootPage.listChildren(new PageFilter(request));
        while (children.hasNext()) {
            Page child = children.next();
            %><a onclick = "tracknav('<%= child.getPath() %>.html')"  href="<%= child.getPath() %>.html"><%
            %><img alt="<%= StringEscapeUtils.escapeXml(child.getTitle()) %>" src="<%= child.getPath() %>.navimage.png"<%= xs %>></a><%
        }
    }
%><script type="text/javascript">
    function tracknav(target) {
            if (CQ_Analytics.Sitecatalyst) {
                CQ_Analytics.record({
                    event: 'topnavClick',
                    values: {
                        topnavTarget:target,
                        topnavLocation:'<%=currentPage.getPath() %>.html'
                    },
                    componentPath: '<%=resource.getResourceType()%>'
                });
            }
    }
</script>
```

>[!NOTE]
>
>通常需要从ContextHub跟踪数据。 有关使用JavaScript获取此信息的信息，请参阅 [访问ContextHub中的值](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).

#### 将跟踪组件添加到Sidekick {#adding-the-tracking-component-to-sidekick}

将启用Adobe Analytics跟踪的组件添加到Sidekick，以便将其添加到框架中。

1. 从Adobe Analytics配置中打开Adobe Analytics框架。 ([http://localhost:4502/etc/cloudservices/sitecatalyst.html](http://localhost:4502/etc/cloudservices/sitecatalyst.html))
1. 在Sidekick上，单击“设计”按钮。

   ![设计按钮具有直角正方形。](assets/chlimage_1a.png)

1. 在链接跟踪配置区域中，单击配置继承。

   ![chlimage_1](assets/chlimage_1aa.png)

1. 在“允许的组件”列表中，选择“常规”部分中的topnav（跟踪） ，然后单击“确定”。
1. 展开Sidekick以进入编辑模式。 该组件现在可在“常规”组中使用。

#### 将topnav组件添加到框架 {#adding-the-topnav-component-to-your-framework}

将topnav组件拖动到Adobe Analytics框架，并将组件变量和事件映射到Adobe Analytics变量和事件。 (请参阅 [设置基本跟踪的框架](/help/sites-administering/adobeanalytics-connect.md).)

![chlimage_1-1](assets/chlimage_1-1a.png)

topnav组件现在已与Adobe Analytics框架集成。 将组件添加到页面时，单击顶部导航栏中的项目会导致将跟踪数据发送到Adobe Analytics。

### 将s.products数据发送到Adobe Analytics {#sending-s-products-data-to-adobe-analytics}

组件可以为发送到Adobe Analytics的s.products变量生成数据。 将组件设计为s.products变量的组成部分：

* 记录名为的值 `product` 的特定结构。
* 显示的数据成员 `product` 值，以便能够在Adobe Analytics框架中用Adobe Analytics变量对其进行映射。

Adobe Analytics s.products变量使用以下语法：

```
s.products="category;product;quantity;price;eventY={value}|eventZ={value};evarA={value}|evarB={value}"
```

Adobe Analytics集成模块构建 `s.products` 变量使用 `product` AEM组件生成的值。 此 `product` AEM组件生成的JavaScript中的值是具有以下结构的值数组：

```
"product": [{
    "category": "",
    "sku"     : "path to product node",
    "quantity": quantity,
    "price"   : price,
    "events   : {
      "eventName1": "eventValue1",
      "eventName_n": "eventValue_n"
    }
    "evars"   : {
      "eVarName1": "eVarValue1",
      "eVarName_n": "eVarValue_n"
    }
}]
```

当省略了数据项时 `product` 值，它将作为s.products中的空字符串发送。

>[!NOTE]
>
>当没有事件与产品值关联时，Adobe Analytics使用 `prodView` 事件。

此 `analytics` 组件的节点必须使用 `cq:trackvars` 属性：

* product.category
* product.sku
* product.quantity
* product.price
* product.events.eventName1
* product.events.eventName_n
* product.evars.eVarName1
* product.evars.eVarName_n

电子商务模块提供了多个用于生成s.products变量数据的组件。 例如， `submitorder` 组件([http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp](http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp))生成与以下示例类似的JavaScript：

```
<script type="text/javascript">
    function trackCartPurchase() {
        if (CQ_Analytics.Sitecatalyst) {
            CQ_Analytics.record({
                "event": ["productsCartPurchase"],
                "values": {
                    "product": [
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/1",
                            "quantity": 3,
                            "price"   : 179.7,
                            "evars"   : {
                                "childSku": "/path/to/prod/1/green/xs",
                                "size"    : "XS"
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/2",
                            "quantity": 10,
                            "price"   : 150,
                            "evars"   : {
                                "childSku": "/path/to/prod/2",
                                "size"    : ""
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/3",
                            "quantity": 2,
                            "price"   : 102,
                            "evars"   : {
                                "childSku": "/path/to/prod/3/m",
                                "size"    : "M"
                            }
                        }
                    ]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["discountRedemption"],
                "values": {
                    "discount": "/path/to/discount/1 - /path/to/discount/2",
                    "product" : [{
                        "category": "",
                        "sku"     : "Promotional Discount",
                        "events"  : {"discountRedemption": 20.00}
                    }]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["cartPurchase"],
                "values": {
                    "orderId"       : "00e40e2d-13a2-4a00-a8ee-01a9ebb0bf68",
                    "shippingMethod": "overnight",
                    "paymentMethod" : "Amex",
                    "billingState"  : "NY",
                    "billingZip"    : "10458",
                    "product"       : [{"category": "", "sku": "", "quantity": "", "price": ""}]
                },
                "componentPath": "commerce/components/submitorder"
            });
        }
        return true;
    }
</script>
```

#### 限制跟踪调用的大小 {#limiting-the-size-of-tracking-calls}

通常，Web浏览器会限制GET请求的大小。 由于CQ产品和SKU值是存储库路径，因此包含多个值的产品阵列可能会超过请求大小限制。 因此，组件应限制 `product` 每个的数组 `CQ_Analytics.record function`. 如果必须跟踪的项目数可能超过限制，请创建多个函数。

例如，电子商务 `submitorder` 组件限制的数量 `product` 调用中的项目数。 当购物车包含四个以上的产品时，将生成多个产品 `CQ_Analytics.record` 函数。
