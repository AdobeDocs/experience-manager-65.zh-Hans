---
title: 模拟器
description: AEM使作者能够在模拟最终用户查看页面的环境的模拟器中查看页面
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
exl-id: 009b7e2c-ac37-4acc-a656-0a34d3853dfd
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---

# 模拟器{#emulators}

{{ue-over-mobile}}

Adobe Experience Manager (AEM)允许作者在模拟最终用户查看页面的环境的模拟器中查看页面，例如在移动设备上或电子邮件客户端中。

AEM模拟器框架：

* 在模拟的用户界面(UI)中提供内容创作，例如，移动设备或电子邮件客户端（用于创作新闻稿）。
* 根据模拟的UI调整页面内容。
* 允许创建自定义模拟器。

>[!CAUTION]
>
>仅经典UI支持此功能。

## 模拟器特性 {#emulators-characteristics}

模拟器：

* 基于ExtJS。
* 对页面DOM运行。
* 其外观通过CSS进行调节。
* 支持插件（例如，移动设备旋转插件）。
* 仅对作者有效。
* 其基组件位于`/libs/wcm/emulator/components/base`。

### 模拟器如何转换内容 {#how-the-emulator-transforms-the-content}

模拟器通过将HTML主体内容封装到模拟器DIV中来工作。 例如，以下html代码：

```xml
<body>
<div id="wrapper" class="page mobilecontentpage ">
    <div class="topnav mobiletopnav">
    ...
    </div>
    ...
</div>
</body>
```

在模拟器启动后，将转换为以下html代码：

```xml
<body>
 <div id="cq-emulator-toolbar">
 ...
 </div>
 <div id="cq-emulator-wrapper">
  <div id="cq-emulator-device">
   <div class=" android vertical" id="cq-emulator">
    ...
    <div class=" android vertical" id="cq-emulator-content">
     ...
     <div id="wrapper" class="page mobilecontentpage">
     ...
     </div>
     ...
    </div>
   </div>
  </div>
 </div>
 ...
</body>
```

添加了两个div标记：

* id为`cq-emulator`的div将模拟器作为整体保存并

* id为`cq-emulator-content`的div，表示页面内容所在的设备的视区/屏幕/内容区域。

新的CSS类也分配给新的模拟器div：它们表示当前模拟器的名称。

模拟器的插件可以进一步扩展分配的CSS类的列表，如旋转插件的示例，根据当前设备旋转插入“垂直”或“水平”类。

这样，可以通过具有与模拟器div的ID和CSS类相对应的CSS类来控制模拟器的完整外观。

>[!NOTE]
>
>建议项目HTML将正文内容包装在一个div中，就像上面的示例一样。 如果正文内容包含多个标记，则可能会产生不可预测的结果。

### 移动模拟器 {#mobile-emulators}

现有的移动仿真器：

* 位于/libs/wcm/mobile/components/emulators下。
* 可通过JSON servlet在以下位置获取：

  http://localhost:4502/bin/wcm/mobile/emulators.json

当页面组件依赖于移动页面组件(`/libs/wcm/mobile/components/page`)时，模拟器功能通过以下机制自动集成到页面中：

* 移动设备页面组件`head.jsp`包括设备组的关联模拟器init组件（仅在创作模式下）以及设备组的渲染CSS，具体方式为：

  `deviceGroup.drawHead(pageContext);`

* 方法`DeviceGroup.drawHead(pageContext)`包含仿真器的init组件，即调用仿真器组件的`init.html.jsp`。 如果模拟器组件没有自己的`init.html.jsp`，并且依赖于Mobile基础模拟器(`wcm/mobile/components/emulators/base)`)，则调用Mobile基础模拟器的init脚本(`/libs/wcm/mobile/components/emulators/base/init.html.jsp`)。

* 移动基础仿真器的init脚本通过JavaScript定义：

   * 为页面定义的所有模拟器的配置(emulatorConfigs)
   * 模拟器管理器通过以下方式将模拟器的功能集成到页面中：

     `emulatorMgr.launch(config)`；

     通过以下方式定义模拟器管理器：

     `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### 创建自定义移动模拟器 {#creating-a-custom-mobile-emulator}

要创建自定义移动设备模拟器，请执行以下操作：

1. 在`/apps/myapp/components/emulators`下创建组件`myemulator` （节点类型： `cq:Component`）。

1. 将`sling:resourceSuperType`属性设置为`/libs/wcm/mobile/components/emulators/base`

1. 为模拟器外观定义类别为`cq.wcm.mobile.emulator`的CSS客户端库：名称= `css`，节点类型= `cq:ClientLibrary`

   例如，您可以引用节点`/libs/wcm/mobile/components/emulators/iPhone/css`

1. 如果需要，可定义JS客户端库，例如，以定义特定插件：名称= js，节点类型= cq：ClientLibrary

   例如，您可以引用节点`/libs/wcm/mobile/components/emulators/base/js`

1. 如果模拟器支持由插件定义的特定功能（如触控滚动），请在模拟器下创建配置节点：名称= `cq:emulatorConfig`，节点类型= `nt:unstructured`，并添加定义插件的属性：

   * 名称= `canRotate`，类型= `Boolean`，值= `true`：包含旋转功能。

   * 名称= `touchScrolling`，类型= `Boolean`，值= `true`：包含触控滚动功能。

   通过定义您自己的插件，可以添加更多功能。
