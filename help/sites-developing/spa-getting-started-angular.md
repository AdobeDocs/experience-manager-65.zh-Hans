---
title: AEM中SPA快速入门——角度
seo-title: AEM中SPA快速入门——角度
description: 本文介绍了一个范例SPA应用程序，介绍了它的组合方式，并允许您使用Angular框架快速启动并运行自己的SPA。
seo-description: 本文介绍了一个范例SPA应用程序，介绍了它的组合方式，并允许您使用Angular框架快速启动并运行自己的SPA。
uuid: d3d2fa63-68c8-4a48-8c8d-045f4f8db937
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9cdd7648-d67e-414d-aedf-a5687da39326
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# AEM中SPA快速入门——角度{#getting-started-with-spas-in-aem-angular}

单页应用程序(SPA)可以为网站用户提供引人入胜的体验。 开发人员希望能够使用SPA框架构建站点，而作者希望在AEM内为使用SPA框架构建的站点无缝编辑内容。

SPA创作功能为在AEM中支持SPA提供了全面的解决方案。 本文介绍Angular框架上简化的SPA应用程序，并解释它的组合方式，使您能快速启动并运行自己的SPA。

>[!NOTE]
>
>本文基于角框架。 有关React框架的相应文档，请参阅AEM [中SPA快速入门- React](/help/sites-developing/spa-getting-started-react.md)。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染（例如“反应”或“角度”）的项目，建议使用SPA编辑器解决方案。

## 简介 {#introduction}

本文概括了简单SPA的基本功能，以及使您的SPA运行所需的最低限度。

有关SPA在AEM中工作方式的更多详细信息，请参阅以下文档：

* [SPA简介和演练](/help/sites-developing/spa-walkthrough.md)
* [SPA创作简介](/help/sites-developing/spa-overview.md)
* [SPA Blueprint](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>要能够在SPA中创作内容，内容必须存储在AEM中并由内容模型公开。
>
>如果AEM之外开发的SPA不遵守内容模型合同，则此SPA将不可授权。

本文档将介绍简化的SPA的结构并说明其工作方式，以便您将这一理解应用于您自己的SPA。

## 依赖关系、配置和构建 {#dependencies-configuration-and-building}

除了期望的角度依赖关系外，示例SPA还可以利用其他库来提高SPA的创建效率。

### 依赖关系 {#dependencies}

文 `package.json` 件定义了整个SPA包的要求。 此处列出所需的最低AEM依赖关系。

```
"dependencies": {
  "@adobe/cq-angular-editable-components": "~1.0.3",
  "@adobe/cq-spa-component-mapping": "~1.0.3",
  "@adobe/cq-spa-page-model-manager": "~1.0.4"
}
```

利用 `aem-clientlib-generator` 该工具，可以在构建过程中自动创建客户端库。

`"aem-clientlib-generator": "^1.4.1",`

有关该功能的更多详细信息，请 [单击此处](https://github.com/wcm-io-frontend/aem-clientlib-generator)。

>[!CAUTION]
>
>所需的最低版 `aem-clientlib-generator` 本为1.4.1。

在文 `aem-clientlib-generator` 件中配置了以 `clientlib.config.js` 下内容。

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-angular-app/clientlibs",

    libs: {
        name: "my-angular-app",
        allowProxy: true,
        categories: ["my-angular-app"],
        embed: ["my-angular-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### 正在生成 {#building}

实际构建应用程序除了 [aem-clientlib](https://webpack.js.org/) -generator用于自动创建客户端库外，还利用Webpack进行转换。 因此，build命令将类似于：

`"build": "ng build --build-optimizer=false && clientlib",`

构建后，包即可上传到AEM实例。

### Maven Archetype for SPA Starter Kit {#maven-archetype-for-spa-starter-kit}

Adobe建议利用 [Maven Archetype for SPA Starter Kit](https://github.com/adobe/aem-spa-project-archetype) ，帮助您开始您自己的AEM SPA项目。

## 应用程序结构 {#application-structure}

如前所述，包括依赖关系和构建应用程序将留给您一个可上传到AEM实例的工作SPA包。

本文档的下一节将介绍AEM中SPA的结构、驱动应用程序的重要文件以及它们如何协同工作。

以简化的图像组件为例，但应用程序的所有组件都基于相同的概念。

### app.module.ts {#app-module-ts}

SPA的入口点是此处显示的 `app.module.ts` 文件，该文件经过简化，可专注于重要内容。

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/cq-angular-editable-components';
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  imports: [ BrowserModule.withServerTransition({ appId: 'my-angular-app' }),
    SpaAngularEditableComponentsModule,
    AppRoutingModule,
    BrowserTransferStateModule ],
  providers: ...,
  declarations: [ ... ],
  entryComponents: [ ... ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

文 `app.module.ts` 件是应用程序的起始点，它包含初始项目配置并用于引导应 `AppComponent` 用程序。

#### 静态实例化 {#static-instantiation}

当使用组件模板静态实例化组件时，必须将值从模型传递到组件的属性。 模型中的值作为属性传递，以便以后作为组件属性可用。

### app.component.ts {#app-component-ts}

引导 `app.module.ts` 完 `AppComponent`成后，它便可以初始化应用程序，该应用程序以简化版本显示，以专注于重要内容。

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/cq-spa-page-model-manager';
import { Constants } from "@adobe/cq-angular-editable-components";

@Component({
  selector: 'app-root',
  template: `
    <router-outlet></router-outlet>
  `
})

export class AppComponent {
  items;
  itemsOrder;
  path;

  constructor() {
    ModelManager.initialize().then(this.updateData.bind(this));
  }

  private updateData(model) {
    this.path = model[Constants.PATH_PROP];
    this.items = model[Constants.ITEMS_PROP];
    this.itemsOrder = model[Constants.ITEMS_ORDER_PROP];
  }
}
```

### main-content.component.ts {#main-content-component-ts}

通过处理页面，将调用 `app.component.ts` 列 `main-content.component.ts` 在此处的简化版本中。

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/cq-angular-editable-components";

@Component({
  selector: 'app-main',
  template: `
    <aem-page class="structure-page" [attr.data-cq-page-path]="path" [cqPath]="path" [cqItems]="items" [cqItemsOrder]="itemsOrder" ></aem-page>
  `
})

export class MainContentComponent {
  items;
  itemsOrder;
  path;

  constructor( private route: ActivatedRoute,
    private modelManagerService: ModelManagerService) {
    this.modelManagerService.getData({ path: this.route.snapshot.data.path }).then((data) => {
      this.path = data[Constants.PATH_PROP];
      this.items = data[Constants.ITEMS_PROP];
      this.itemsOrder = data[Constants.ITEMS_ORDER_PROP];
    });
  }
}
```

收 `MainComponent` 集页面模型的JSON表示形式并处理内容以包装／装饰页面的每个元素。 有关该工具的更 `Page` 多详细信息，请参阅文 [档SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501)。

### image.component.ts {#image-component-ts}

它 `Page` 由组件组成。 摄取JSON后，可 `Page` 以处理这些组件，如 `image.component.ts` 下所示。

```
/// image.component.ts
import { Component, Input } from '@angular/core';

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function(cqModel) {
        return !cqModel || !cqModel.src || cqModel.src.trim().length < 1;
    }
};

@Component({
  selector: 'app-image',
  templateUrl: './image.component.html',
})

export class ImageComponent {
  @Input() src: string;
  @Input() alt: string;
  @Input() title: string;
}

MapTo('my-angular-app/components/image')(ImageComponent, ImageEditConfig);
```

AEM中SPA的核心思想是将SPA组件映射到AEM组件，并在内容被修改时更新组件（反之亦然）。 有关此通信模 [型的摘要，请参阅文档](/help/sites-developing/spa-overview.md) SPA编辑器概述。

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

该方 `MapTo` 法将SPA组件映射到AEM组件。 它支持使用单个字符串或字符串数组。

`ImageEditConfig` 是一个配置对象，它通过为编辑器提供生成占位符所需的元数据来帮助启用组件的创作功能

如果没有内容，则标签将作为占位符提供以表示空内容。

#### 动态传递的属性 {#dynamically-passed-properties}

来自模型的数据会作为组件的属性动态传递。

### image.component.html {#image-component-html}

最后，可以在中渲染图像 `image.component.html`。

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## 在SPA组件之间共享信息 {#sharing-information-between-spa-components}

单页应用程序中的组件需要定期共享信息。 有几种建议的方法可以这样做，其复杂性的顺序如下所示。

* **** 选项1:将逻辑集中化并广播到必要的组件，例如，将util类用作纯面向对象的解决方案。
* **** 选项2:使用状态库（如NgRx）共享组件状态。
* **** 选项3:通过自定义和扩展容器组件来利用对象层次结构。

## 后续步骤 {#next-steps}

有关创建您自己的SPA的分步指南，请参阅AEM SPA [编辑器入门- WKND事件教程](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)。

有关如何组织自己为AEM开发SPA的更多信息，请参阅为AEM开 [发SPA文章](/help/sites-developing/spa-architecture.md)。

有关动态模型到组件映射以及它在AEM中在SPA中的工作方式的更多详细信息，请参阅SPA的 [动态模型到组件映射文章](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

如果您希望在AEM中为React或Angular之外的框架实施SPA，或只是希望深入了解AEM的SPA SDK的工作方式，请参阅 [SPA Blueprint文章](/help/sites-developing/spa-blueprint.md) 。
