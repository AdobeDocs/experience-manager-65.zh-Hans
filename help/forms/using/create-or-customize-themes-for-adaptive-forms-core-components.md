---
title: 如何创建或自定义自适应表单主题？
description: 了解如何使用BEM规范创建或自定义自适应Forms核心组件的主题
keywords: 创建自适应表单核心组件主题，创建新主题，自定义主题，上传新主题，在表单中使用主题，删除主题，在AEM 6.5表单中创建主题
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms,Core Components
exl-id: 9f9b35a3-0479-4179-9fad-994a482c96b6
solution: Experience Manager, Experience Manager Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1939'
ht-degree: 5%

---

# 创建或自定义自适应表单主题 {#introduction-to-theme}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html) |
| AEM 6.5 | 本文 |


<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

在AEM Forms 6.5中，主题是一个AEM客户端库，可使用它定义自适应表单的样式（外观）。 主题包含组件和面板的样式详细信息。 样式包括背景颜色、状态颜色、透明度、对齐方式和大小等属性。在应用主题时，指定的样式会反映在相应的组件上。主题是独立管理的，无需引用自适应表单，并且可在多个自适应Forms中重复使用。

## 可用主题 {#available-theme}

AEM 6.5环境为基于核心组件的自适应Forms提供了以下列出的主题：

* [画布主题](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND 主题](https://github.com/adobe/aem-forms-theme-wknd)
* [画架主题](https://github.com/adobe/aem-forms-theme-easel)
* [FSI主题](https://github.com/adobe/aem-forms-theme-fsi)
* [医疗保健主题](https://github.com/adobe/aem-forms-theme-healthcare)
* [公共主题](https://github.com/adobe/aem-forms-theme-public)
* [制造主题](https://github.com/adobe/aem-forms-theme-manufacturing)

## 了解主题的结构 {#understanding-structure-of-theme}

主题是一个包，其中包含定义自适应Forms样式的CSS文件、JavaScript文件和资源（如图标）。 自适应表单主题遵循特定的组织，由以下组件组成：

* `src/theme.scss`：此文件夹包含对整个主题具有广泛影响的CSS文件。 它用作定义和管理主题样式和行为的集中位置。 通过编辑此文件，您可以做出在整个主题中普遍应用的更改，从而影响自适应Forms和AEM Sites页面的外观和功能。

* `src/site`：此文件夹包含应用于整个AEM站点页面的CSS文件。 这些文件由代码和样式组成，这些代码和样式会影响AEM站点页面的整体功能和布局。 此处所做的任何修改都会反映在网站的所有页面中。

* `src/components`：此文件夹中的CSS文件是为单个AEM核心组件设计的。 组件的每个专用文件夹都包含一个`.scss`文件，该文件在自适应表单中为该特定组件设置样式。 例如，`/src/components/button/_button.scss`文件包含自适应Forms按钮组件的样式信息。

  ![画布主题结构](/help/forms/using/assets/component-based-theme-folder-structure.png)

* `src/resources`：此文件夹包含静态文件，如图标、徽标和字体。 这些资源用于增强主题的可视化元素和总体设计。

## 创建主题

AEM Forms 6.5为基于核心组件的自适应Forms提供了以下列出的主题。

* [画布主题](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND 主题](https://github.com/adobe/aem-forms-theme-wknd)
* [画架主题](https://github.com/adobe/aem-forms-theme-easel)
* [公共主题](https://github.com/adobe/aem-forms-theme-public)
* [制造主题](https://github.com/adobe/aem-forms-theme-manufacturing)

您可以[自定义其中的任何主题以创建主题](#customize-a-theme-core-components)。

## 自定义主题 {#customize-a-theme-core-components-based-adaptive-forms}

自定义主题是指修改和个性化主题外观的过程。 自定义主题时，您可以更改其设计元素、布局、颜色、排版规则，有时还会更改底层代码。 这样，您就可以为网站或应用程序创建独一无二的定制外观，同时保持主题提供的基本结构和功能。

>[!NOTE]
>
> * 使用包管理器在所有Author和Publish实例上部署主题。
> * 主题客户端库与任何其他包一样，通过包管理器导入或导出。

### 自定义主题的先决条件 {#prerequisites}

* 为您的环境[启用自适应Forms核心组件](/help/forms/using/enable-adaptive-forms-core-components.md)。

* 安装[Apache Maven的最新版本。](https://maven.apache.org/download.cgi) Apache Maven是常用于Java™项目的生成自动化工具。 安装最新版本可确保您具有主题自定义所需的依赖项。

* 了解如何在Adobe Experience Manager[&#128279;](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html)中创建客户端库。 AEM提供了客户端库，这使您可以在存储库中存储客户端代码，将其整理到不同类别中，并定义何时以及如何向客户端提供每种类别的代码。

* 安装纯文本编辑器。 例如，Microsoft® Visual Studio Code。 使用Microsoft等纯文本编辑器®Visual Studio Code为编辑和修改主题文件提供了用户友好的环境。

* 确保AEM Forms环境已启动并正在运行。

### 自定义主题的注意事项 {#consideration}

* 请确保您使用[在您的环境中启用自适应Forms核心组件](/help/forms/using/enable-adaptive-forms-core-components.md)的Archetype项目来自定义主题。

* 发布自适应表单时，不会在Publish实例上自动发布客户端库。 确保手动将在自适应表单中引用的客户端库发布到Publish环境。

* Adobe建议不要更改客户端库的类名。

### 自定义主题 {#customize-a-theme-core-components}

创建或自定义主题是一个多步骤过程。 按照列出的顺序执行步骤，以创建/自定义主题：

1. [克隆主题](#clone-git-repo-of-theme)
1. [自定义主题的外观](#customize-the-theme)
1. [为本地部署准备主题](#generate-the-clientlib)
1. [在本地环境中部署主题](#deploy-the-theme-on-a-local-environment)
1. [在生产环境中部署主题](#5-deploy-a-theme-on-your-production-environment)

<!--
 ![Theme Customization workflow](/help/forms/using/assets/custom-theme-steps.png)
-->

文档中提供的示例基于&#x200B;**画布**&#x200B;主题，但您可以克隆任何主题并使用相同的说明对其进行自定义。 这些说明适用于任何主题，允许您根据特定需求修改主题。

#### 1.克隆主题的Git存储库 {#clone-git-repo-of-theme}

要克隆基于核心组件的自适应Forms的主题，请选择以下主题之一：

* [画布主题](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND 主题](https://github.com/adobe/aem-forms-theme-wknd)
* [画架主题](https://github.com/adobe/aem-forms-theme-easel)

执行以下说明以克隆主题：

1. 在本地开发环境中打开命令提示符或终端窗口。

1. 运行`git clone`命令以克隆主题。

   ```
      git clone [Path of Git Repository of the theme]
   ```

   将主题&rbrack;的Git存储库的&lbrack;路径替换为主题的相应Git存储库的实际URL

   例如，要克隆画布主题，请执行以下命令：

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

1. 选择&#x200B;**信任父文件夹中所有文件的作者**，并单击&#x200B;**是的，我信任作者**。

成功执行命令后，`aem-forms-theme-canvas`文件夹中提供了计算机上主题的本地副本。

#### 2.自定义主题 {#customize-the-theme}

您可以灵活地自定义各个组件，或使用主题的全局变量进行主题级别的更改。 修改全局变量会对所有单个组件产生级联效果。 例如，您可以使用全局变量更改自适应表单中所有组件的边框颜色，或为行动号召(CTA)按钮应用生动的填充颜色。 您可以：

* [设置主题级别样式](#theme-customization-global-level)

* [设置组件级别样式](#component-based-customization)

##### 设置主题级别样式 {#theme-customization-global-level}

`variable.scss`文件包含主题的全局变量。 通过更新这些变量，您可以在主题级别进行与样式相关的更改。 要应用主题级别的样式，请执行以下步骤：

1. 打开`<your-theme-sources>/src/site/_variables.scss`文件进行编辑。
1. 更改任何属性的值。 例如，缺省错误颜色为红色。 要将错误颜色从红色更改为蓝色，请更改`$error`变量的颜色十六进制代码。 例如：`$error: #196ee5`。

   ![示例：错误颜色设置为蓝色](/help/forms/using/assets/theme-level-changes.png)

1. 保存并关闭该文件。


同样，您可以使用`variable.scss`文件设置字体系列和类型、主题和字体颜色、字体大小、主题间距、错误图标、主题边框样式以及影响多个自适应表单组件的更多变量。

##### 设置组件级别样式 {#component-based-customization}

您还可以选择自定义特定自适应表单核心组件（如按钮、复选框、容器、页脚等）的字体、颜色、大小及其他CSS属性。 通过编辑与特定组件关联的CSS文件，您可以将其样式与组织的品牌保持一致。 要自定义组件的样式，请执行以下步骤：

1. 打开文件`<your-theme-sources>/src/components/<component>/<component.scss>`进行编辑。 例如，要更改按钮组件的字体颜色，请打开`<your-theme-sources>/src/components/button/button.scss`文件。
1. 根据您的要求更改任意的值。 例如，要将鼠标悬停时按钮组件的颜色更改为绿色，请将`cmp-adaptiveform-button__widget:hover`类中`color: $white`属性的值更改为十六进制代码#12b453或任何其他绿色阴影。 最终代码如下所示：

   ```
    .cmp-adaptiveform-button__widget:hover {
    background: $dark-gray;
    color: #12b453;
    }
   ```


1. 保存并关闭该文件。

<!--

   ![Example: Hover color set to green](/help/forms/using/assets/button-customization.png)

-->

>[!NOTE]
>
> 在主题和组件级别定义样式时，在组件级别定义的样式优先。

#### 3.准备好部署主题 {#generate-the-clientlib}

要将主题部署到AEM实例，需要将其转换为客户端库。 按照以下步骤将主题转换为客户端库：

1. 打开命令提示符或终端窗口。
1. 导航到`<your-theme-sources>`文件夹。 例如，`C:\aem-forms-theme-canvas`
1. 运行以下命令：

   ```
      npm run create-clientlib --category=adaptiveform.theme.[yourtheme]
   ```

   将`[yourtheme]`替换为自定义主题的名称。 例如，如果自定义主题的名称为`customcanvastheme`，请运行以下命令

   ```
       npm run create-clientlib --category=adaptiveform.theme.customcanvastheme
   ```

   成功执行该命令后，将在`themerepo\theme-clientlibs\[yourtheme]`处创建一个客户端库文件夹。

   ![客户端库生成](/help/forms/using/assets/clientlib_created.png)


   ![客户端库位置](/help/forms/using/assets/adaptiveform.theme.easel.png)

#### 4.将主题部署在本地环境中 {#deploy-the-theme-on-a-local-environment}

要将主题部署到本地开发或测试环境，请执行以下步骤：

1. 将上一部分中创建的客户端库复制到原型项目中，路径如下：

   `/ui.apps/src/main/content/jcr_root/apps/[AEM Archetype Project Folder]/clientlibs/<yourtheme>`

1. 打开命令提示符或终端。
1. 导航到AEM Archetype项目的根目录，该项目用于启用自适应表单核心组件。
1. 运行以下命令以在您的环境中部署自定义主题：

   `mvn clean install`

   ![客户端库生成](/help/forms/using/assets/mvndeploy.png)

<!--

#### 5. Test the theme with a local Adaptive Form {#test-the-theme-with-a-local-adaptive-form}

To apply and test the customized theme with an Adaptive Form:

**Apply theme while creating an Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Select **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Click **Create** > **Adaptive Forms**. The wizard for creating Adaptive Form opens.

1. Select the core component template in the **Source** tab.
1. Select the theme in the **Style** tab.
1. Click **Create**.

An Adaptive Form with the selected theme is created. 

**Apply theme to an existing Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Select **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Select an Adaptive Form and click Properties. 

1. For the **Theme Client Library** option, select the theme. 

1. Click **Save & Close**.

The selected theme is applied to the Adaptive Form. 
-->

#### 5.在生产环境中部署主题 {#deploy-theme}

在本地开发环境中成功测试主题后，您可以继续将主题部署到生产环境，包括创作实例和Publish实例。 按照以下步骤在生产环境中部署主题：

1. 登录到您的AEM环境。
1. 打开包管理器。 默认URL为`https://localhost:4502/crx/packmgr/index.jsp`。
1. 单击&#x200B;**上传包**，然后单击&#x200B;**浏览**。
1. 导航到`[AEM Archetype Project Folder]\all\target[appid].all-[version].zip`并选择。 单击&#x200B;**打开**。
1. 单击“安装”。 在所有生产环境中重复该步骤。


安装包后，该主题可供选择。

![主题客户端库](/help/forms/using/assets/themeclientlibrary.png)

>[!NOTE]
>
>
> 如果您在访问发布实例的登录对话框以通过包管理器安装包时遇到困难，请尝试通过以下URL登录： `http://[Publish Server URL]:[PORT]/system/console`。 这允许访问Publish实例，允许您继续安装过程。

## 将主题应用于自适应表单 {#using-theme-in-adaptive-form}

将主题应用于自适应表单的步骤如下：

1. 登录到本地AEM创作实例。
1. 在 Experience Manager 登录页面上输入您的凭据。选择&#x200B;**Adobe Experience Manager** > **Forms** > **Forms和文档**。
1. 单击&#x200B;**创建** > **自适应Forms**。
1. 选择自适应Forms核心组件模板，然后单击&#x200B;**下一步**。 出现&#x200B;**添加属性**
1. 为自适应表单指定&#x200B;**Name**。


   >[!NOTE]
   >
   > * 默认情况下，选择`adaptiveform.theme.canvas3`主题。
   > * 您可以从&#x200B;**主题客户端库**&#x200B;下拉菜单中选择其他主题。

1. 单击&#x200B;**创建**。

创建自适应表单时，自适应表单主题用作自适应表单模板的一部分来定义样式。

## 删除主题 {#delete-a-theme}

要删除不使用的或不需要的主题，请执行以下操作：

1. 登录您的创作实例。
1. 打开`http://[Publish Server URL]:[PORT]/crx/de/index.jsp`
1. 导航到 `apps/[AEM Archetype Project Folder]/clientlibs/[yourtheme]`。
1. 删除主题文件夹并保存更改。


## 常见问题解答 {#faq}

**问：**&#x200B;在全局级别和组件级别的主题文件夹中进行自定义时，哪个自定义项优先？

**Ans：**&#x200B;在主题和组件级别上同时定义样式时，在组件级别上定义的样式优先。

**问：**&#x200B;如果自定义主题在&#x200B;**[!UICONTROL 主题客户端库]**&#x200B;中不可见，应该执行哪些步骤？

**Ans：**&#x200B;如果您的自定义主题未出现在&#x200B;**[!UICONTROL 主题客户端库]**&#x200B;下拉列表中，请按照以下步骤操作：

1. 导航到将自定义主题客户端库添加到的位置。 建议的路径为`/ui.apps/src/main/content/jcr_root/apps[AEM Archetype Project Folder]/clientlibs/<yourtheme>`。

1. 打开`.content.xml`文件并包含以下元数据：

   ```
       formstheme:true
       allowproxy:true
   ```

1. 保存文件并重新部署主题。

## 另请参阅

* [创建基于核心组件的自适应表单](create-an-adaptive-form-core-components.md)
* [使用规则编辑器向表单添加动态行为](rule-editor.md)
* [创建或自定义基于核心组件的自适应Forms的主题](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [为基于核心组件的自适应Forms创建模板](template-editor.md)
* [创建自适应表单或将其添加到AEM Sites页面或体验片段](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [示例主题模板和表单数据模型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)
