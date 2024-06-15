---
title: 在自适应表单中创建和添加自定义函数
description: AEM Forms支持自定义函数，这些函数允许用户在规则编辑器中创建和使用自己的函数。
keywords: 添加自定义函数、使用自定义函数、创建自定义函数、在规则编辑器中使用自定义函数。
content-type: reference
feature: Adaptive Forms, Core Components
source-git-commit: f633fdfda531cc29ce6274e0367708cc4909a0cd
workflow-type: tm+mt
source-wordcount: '3385'
ht-degree: 2%

---

# 自适应核心组件中的自定义函数Forms

本文介绍了如何使用最新的自适应表单核心组件创建自定义函数，这些组件具有最新的功能，例如：
* 自定义函数的缓存功能
* 自定义函数的全局范围对象和字段对象支持
* 支持现代JavaScript功能，如let和arrow函数（ES10支持）

确保设置 [最新表单版本](https://github.com/adobe/aem-core-forms-components/tree/release/650) 使用AEM Forms核心组件环境中的“自定义函数”的最新功能。 </span>


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | 本文 |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/cn/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/create-and-use-custom-functions) |

## 简介

AEM Forms 6.5包括JavaScript函数，这些函数允许您使用规则编辑器定义复杂的业务规则。 虽然AEM Forms提供了多种现成的自定义函数，但许多用例需要定义您自己的自定义函数才能在多个表单中使用。 这些自定义函数允许根据特定要求处理输入的数据，从而增强表单的功能。 此外，它们允许根据预定义标准动态更改表单行为。

### 自定义函数的使用 {#uses-of-custom-function}

在自适应Forms核心组件中使用自定义函数的优点包括：


* **管理数据**：自定义函数管理和处理输入到表单字段中的数据。
* **数据处理**：自定义函数有助于处理输入到表单字段中的数据。
* **数据验证**：通过自定义函数，可对表单输入执行自定义检查并提供指定的错误消息。
* **动态行为**：自定义函数允许您根据特定条件控制表单的动态行为。 例如，您可以显示/隐藏字段、修改字段值或动态调整表单逻辑。
* **集成**：您可以使用自定义函数与外部API或服务集成。 它有助于从外部源获取数据，将数据发送到外部Rest端点，或根据外部事件执行自定义操作。

自定义函数本质上是添加到JavaScript文件中的客户端库。 创建自定义函数后，该函数即可在规则编辑器中供用户在自适应表单中选择。 自定义函数由规则编辑器中的JavaScript注释标识。

### 自定义函数支持的JavaScript注释 {#js-annotations}

**JavaScript注释为JavaScript代码提供元数据**. 它包括以特定符号开头的注释，例如， `/**` 和 `@`. 注释提供了有关代码中的函数、变量和其他元素的重要信息。 自适应表单支持自定义函数的以下JavaScript注释：

#### 名称

此 **名称** 用于在自适应表单的规则编辑器中标识自定义函数。 以下语法用于命名自定义函数：

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`

>[!NOTE]
>`[functionName]` 是函数的名称。 不允许使用空格。
>`<Function Name>` 是自适应Forms的规则编辑器中函数的显示名称。
>如果函数名称与函数本身的名称相同，则可以忽略 `[functionName]` 语法中的。

#### 参数

此 **参数** 是自定义函数使用的参数列表。 函数可以支持多个参数。 以下语法用于定义自定义函数中的参数：

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`

  `{type}` 表示参数类型。 允许的参数类型包括：

   * string：表示单个字符串值。
   * 数字：表示单个数值。
   * 布尔值：表示单个布尔值（true或false）。
   * 字符串[]：表示字符串值的数组。
   * 数字[]：表示数字值的数组。
   * 布尔型[]：表示布尔值的数组。
   * 日期：表示单个日期值。
   * 日期[]：表示日期值的数组。
   * array：表示包含各种类型值的泛型数组。
   * 对象：表示传递到自定义函数的表单对象，而不是直接传递其值。
   * 范围：表示全局对象，其中包含只读变量，如表单实例、目标字段实例以及在自定义函数中执行表单修改的方法。 此变量声明为JavaScript注释中的最后一个参数，对自适应表单的规则编辑器不可见。 scope参数可访问表单或组件的对象，以触发表单处理所需的规则或事件。 有关Globals对象及其使用方式的更多信息， [单击此处](/help/forms/using/create-and-use-custom-functions-core-components.md#field-and-global-scope-objects-in-custom-functions-support-field-and-global-objects)

参数类型为 **不区分大小写** 参数名称中不允许包含和空格。

`<Parameter Description>` 包含有关参数用途的详细信息。 它可以有多个单词。

<!--

**Optional Parameters**
By default, all parameters are mandatory. You can define a parameter as optional by either adding `=` after the parameter type or enclosing the parameter name in `[]`. Parameters defined as optional in JavaScript annotations are displayed as optional in the rule editor.
To define a variable as an optional parameter, you can use the any of the following syntaxes:
  
* `@param {type=} Input1`

In the above line of code, `Input1` is an optional parameter without any default value. To declare optional parameter with default value:

`@param {string=<value>} input1`
        
`input1` as an optional parameter with the default value set to `value`. 

* `@param {type} [Input1]`

In the above line of code, `Input1` is an optional parameter without any default value. To declare optional parameter with default value:

`@param {array} [input1=<value>]`

    `input1` is an optional parameter of array type with the default value set to `value`. 
    Ensure that the parameter type is enclosed in curly brackets {} and the parameter name is enclosed in square brackets []. 

Consider the following code snippet, where input2 is defined as an optional parameter:

```javascript

        /**
         * optional parameter function
         * @name OptionalParameterFunction
         * @param {string} input1 
         * @param {string=} input2 
         * @return {string}
        */
        function OptionalParameterFunction(input1, input2) {
        let result = "Result: ";
        result += input1;
        if (input2 !== null) {
            result += " " + input2;
        }
        return result;
        }
```

The following illustration displays using the `OptionalParameterFunction` csutom function in the rule editor:

![Optional or required parameters ](/help/forms/using/assets/optional-default-params.png)

You can save the rule without specifying a value for required parameters, but the rule is not executed and displays a warning message as:

![incomplete rule warning](/help/forms/using/assets/incomplete-rule.png)

When user leaves the optional parameter empty, then the "Undefined" value is passed to the custom function for the optional parameter.

To learn more about how to define optional parameters in JSDocs, [click here](https://jsdoc.app/tags-param).

-->

#### 返回类型

返回类型指定自定义函数在执行后返回的值的类型。 以下语法用于在自定义函数中定义退货类型：

* `@return {type}`
* `@returns {type}`
  `{type}` 表示函数的返回类型。 允许的返回类型包括：
* string：表示单个字符串值。
* 数字：表示单个数值。
* 布尔值：表示单个布尔值（true或false）。
* 字符串[]：表示字符串值的数组。
* 数字[]：表示数字值的数组。
* 布尔型[]：表示布尔值的数组。
* 日期：表示单个日期值。
* 日期[]：表示日期值的数组。
* array：表示包含各种类型值的泛型数组。
* 对象：表示表单对象，而不是直接表示其值。

返回类型不区分大小写。

#### 专用

声明为私有的自定义函数不会出现在自适应表单的规则编辑器的自定义函数列表中。 默认情况下，自定义函数是公用的。 将自定义函数声明为私有函数的语法为 `@private`.

<!--
#### Member

  Syntax: `@memberof namespace`
  Attaches a namespace to the function.
-->

<!--

#### This

   Syntax: `@this currentComponent`

   Use @this to refer to the Adaptive Form component on which the rule is written. 
  
   The following example is based on the field value. In the following example, the rule hides a field in the form. The `this` portion of `this.value` refers to underlying Adaptive Form component, on which the rule is written.

   ```
      /**
      * @function myTestFunction
      * @this currentComponent
      * @param {scope} scope in which code inside function will be executed.
      */
      myTestFunction = function (scope) {
         if(this.value == "O"){
               scope.age.visible = true;
         } else {
            scope.age.visible = false;
         }
      }

   ```

    >[!NOTE]
    >
    >Comments before custom function are used for summary. Summary can extend to multiple lines until a tag is encountered. Limit the size to a single for a concise description in the rule builder.

-->

<!--

## Function declaration supported types {#function-declaration-supported-types}

**Function Statement**

```javascript
function area(len) {
    return len*len;
}
```

This function is included without `jsdoc` comments.

**Function Expression**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Function Expression and Statement**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Function Declaration as Variable**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitation: custom function picks only the first function declaration from the variable list, if together. You can use function expression for every function declared.

**Function Declaration as Object**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```
-->

## 创建自定义函数时的准则 {#considerations}

要在规则编辑器中列出自定义函数，您可以使用以下任意格式：

### 包含或不包含jsdoc注释的函数语句

您可以创建包含或不包含jsdoc注释的自定义函数。

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```

如果用户没有向自定义函数添加任何JavaScript注释，则它按函数名称在规则编辑器中列出。 但是，建议包含JavaScript注释，以提高自定义函数的可读性。


### 具有必需JavaScript注释或注释的Arrow函数

您可以使用箭头函数语法创建自定义函数：

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} a parameter description
    * @param {string=} b parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
    /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;
    
```

如果用户没有将任何JavaScript注释添加到自定义函数，则该自定义函数不会列在自适应表单的规则编辑器中。

### 具有必需JavaScript注释或注释的函数表达式

要在自适应表单的规则编辑器中列出自定义函数，请以下列格式创建自定义函数：

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} input1 parameter description
    * @param {string=} input2 parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

如果用户没有将任何JavaScript注释添加到自定义函数，则该自定义函数不会列在自适应表单的规则编辑器中。

### 创建自定义函数的先决条件

在开始将自定义函数添加到自适应Forms之前，请确保在计算机上安装了以下软件：

* **纯文本编辑器(IDE)**：虽然任何纯文本编辑器都可以工作，但诸如Microsoft Visual Studio Code之类的集成开发环境(IDE)可提供高级功能以便更轻松地编辑。

* **Git：** 此版本控制系统是管理代码更改所必需的。 如果未安装，请从https://git-scm.com下载。


## 创建自定义功能 {#create-custom-function}

创建自定义函数的步骤包括：
1. [使用AEM项目原型创建客户端库并添加自定义函数](#create-client-library-archetype)
或者
   [通过CRXDE创建自定义函数](#create-add-custom-function)
1. [将客户端库添加到自适应表单](#add-client-library)
1. [在自适应表单中使用自定义函数](#use-custom-functions)


### 使用AEM项目原型创建客户端库{#create-client-library-archetype}

您可以通过向创建的项目添加客户端库来添加自定义函数 [使用AEM项目原型](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/archetype/using#getting-started).
如果您现有项目， <!--and have already the project structure as shown in the image below,--> 您可以直接添加 [自定义函数](#create-add-custom-function) 到您的本地项目。

<!--![custom fuction folder structure](assets/custom-library-folder-structure.png)-->

创建原型项目或使用现有项目后，请创建客户端库。 要创建客户端库，请执行以下步骤：

**添加客户端库文件夹**

要将新的客户端库文件夹添加到 [AEM项目目录]，请按照以下步骤操作：

1. 打开 [AEM项目目录] 在编辑器中。

   ![自定义函数文件夹结构](assets/custom-library-folder-structure.png)

1. 定位 `ui.apps`.
1. 添加新文件夹。 例如，添加一个名为的文件夹 `experience-league`.
1. 导航到 `/experience-league/` 文件夹并添加 `ClientLibraryFolder`. 例如，创建一个名为的客户端库文件夹 `customclientlibs`.

   位置为： `[AEM project directory]/ui.apps/src/main/content/jcr_root/apps/`

**将文件和文件夹添加到“客户端库”文件夹**

将以下内容添加到添加的客户端库文件夹：

* `.content.xml` 文件
* `js.txt` 文件
* `js` 文件夹

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. 在 `.content.xml` 添加以下代码行：

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > 您可以选择任意名称 `client library folder` 和 `categories` 属性。

1. 在 `js.txt` 添加以下代码行：

   ```javascript
         #base=js
       function.js
   ```

1. 在 `js` 文件夹，将javascript文件添加为 `function.js` 具体包括以下自定义函数：

   ```javascript
   /**
       * Calculates Age
       * @name calculateAge
       * @param {object} field
       * @return {string} 
   */
   
   function calculateAge(field) {
   var dob = new Date(field);
   var now = new Date();
   
   var age = now.getFullYear() - dob.getFullYear();
   var monthDiff = now.getMonth() - dob.getMonth();
   
   if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
   age--;
   }
   
   return age;
   }
   ```

1. 保存文件。

![自定义函数文件夹结构](assets/custom-function-added-files.png)

**在filter.xml中包含新文件夹**：

1. 导航至 `/ui.apps/src/main/content/META-INF/vault/filter.xml` 文件中的文件 [AEMaaCS项目目录].

1. 打开文件，并在末尾添加以下行：

   `<filter root="/apps/experience-league" />`
1. 保存文件。

   ![自定义函数筛选器xml](assets/custom-function-filterxml.png)

1. 按照中给出的步骤，将新创建的客户端库文件夹构建到您的AEM环境中 [“如何构建”部分](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype#how-to-build).

## 通过CRXDE创建和部署自定义函数{#create-add-custom-function}

如果您使用最新的AEM Forms和Forms加载项，则可以通过CRXDE创建自定义函数，以使用自定义函数的最新更新。 为此，请执行以下步骤：

<!--![custom fuction folder structure](assets/custom-library-folder-structure.png)-->


1. 登录 `http://server:port/crx/de/index.jsp#`.
1. 在 `/apps` 文件夹下创建一个文件夹。例如，创建一个名为的文件夹 `experience-league`.
1. 保存更改。
1. 导航到已创建的文件夹并创建节点类型 `cq:ClientLibraryFolder` 作为 `clientlibs`.
1. 导航到新创建的 `clientlibs` 文件夹并添加 `allowProxy` 和 `categories` 属性：

   ![自定义库节点属性](/help/forms/using/assets/customlibrary-catproperties.png)

   >[!NOTE]
   >
   > 您可以提供任意名称来取代 `customfunctionsdemo`.

1. 保存更改。

1. 创建名为的文件夹 `js` 在 `clientlibs` 文件夹。
1. 创建名为的JavaScript文件 `functions.js` 在 `js` 文件夹。
1. 创建名为的文件 `js.txt` 在 `clientlibs` 文件夹。
1. 保存更改。
创建的文件夹结构如下所示：

   ![创建的客户端库文件夹结构](/help/forms/using/assets/clientlibrary_folderstructure.png)
1. 双击 `functions.js` 文件以打开编辑器。 该文件包含自定义函数的代码。
让我们将以下代码添加到JavaScript文件中，以根据出生日期计算年龄(YYYY-MM-DD)。

   ```javascript
       /**
            * Calculates Age
            * @name calculateAge 
            * @return {string} 
       */
   
       function calculateAge(dateOfBirthString) {
       var dob = new Date(dateOfBirthString);
       var now = new Date();
   
       var age = now.getFullYear() - dob.getFullYear();
       var monthDiff = now.getMonth() - dob.getMonth();
   
       if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
       age--;
       }
   
       return age;
       }
   ```

1. 保存 `function.js`.
1. 导航到 `js.txt` 并添加以下代码：

   ```javascript
       #base=js
       functions.js
   ```

1. 保存 `js.txt` 文件。

您可以参考以下内容 [自定义函数](/help/forms/using/assets/customfunction.zip) 文件夹。 在您的AEM实例上下载并安装此文件夹。

现在，您可以通过添加客户端库在自适应表单中使用自定义函数。

## 在自适应表单中添加客户端库{#add-client-library}

将客户端库部署到AEM Forms环境后，请在自适应表单中使用其功能。 在自适应表单中添加客户端库

1. 在编辑模式下打开表单。 要在编辑模式下打开表单，请选择一个表单，然后选择 **[!UICONTROL 编辑]**.
1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性图标。 这将打开“自适应表单容器”对话框。
1. 打开 **[!UICONTROL 基本]** 选项卡并选择的名称 **[!UICONTROL 客户端库类别]** (在本例中，选择 `customfunctionscategory`)。

   ![添加自定义函数客户端库](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. 单击&#x200B;**[!UICONTROL 完成]**。

现在，您可以创建一个规则以在规则编辑器中使用自定义函数：

![添加自定义函数客户端库](/help/forms/using//assets/calculateage-customfunction.png)

现在，让我们了解如何使用 [AEM Forms 6.5中规则编辑器的调用服务](/help/forms/using/rule-editor-core-components.md#invoke-form-data-model-service-invoke)

## 在自适应表单中使用自定义函数 {#use-custom-functions}

在自适应表单中，您可以使用 [规则编辑器中的自定义函数](/help/forms/using/rule-editor-core-components.md).
让我们将以下代码添加到JavaScript文件(`Function.js` 文件)来基于出生日期计算年龄(YYYY-MM-DD)。 创建自定义函数为 `calculateAge()` ，以出生日期作为输入并返回年龄：

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

在上例中，当用户以(YYYY-MM-DD)格式输入出生日期时，自定义函数 `calculateAge` 将调用并返回年龄。

![在规则编辑器中计算Age自定义函数](/help/forms/using/assets/custom-function-calculate-age.png)

让我们预览表单，观察自定义函数如何通过规则编辑器实现：

![在规则编辑器表单预览中计算年龄自定义函数](/help/forms/using/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> 您可以参考以下内容 [自定义函数](/help/forms/using/assets/customfunctions.zip) 文件夹。 使用下载此文件夹并将其安装到您的AEM实例中 [包管理器](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager).

### 在自定义函数中支持异步函数 {#support-of-async-functions}

异步自定义函数未出现在规则编辑器列表中。 但是，可以在使用同步函数表达式创建的自定义函数中调用异步函数。

![同步和异步自定义函数](/help/forms/using/assets/workflow-for-sync-async-custom-fumction.png)

>[!NOTE]
>
> 在自定义函数中调用异步函数的优势在于，异步函数允许并行执行多个任务，并且自定义函数中使用了每个函数的结果。

查看以下代码，了解如何使用自定义函数调用异步函数：

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

在上述示例中，asyncFunction函数是 `asynchronous function`. 它执行异步操作，方法是 `GET` 请求给 `https://petstore.swagger.io/v2/store/inventory`. 它使用以下方式等待响应 `await`，使用将响应正文解析为JSON `response.json()`，然后返回数据。 此 `callAsyncFunction` 函数是一个同步自定义函数，可调用 `asyncFunction` 函数并在控制台中显示响应数据。 尽管 `callAsyncFunction` 函数是同步的，它调用异步asyncFunction函数并使用处理其结果 `then` 和 `catch` 语句。

要查看其是否有效，让我们添加一个按钮，并为按钮创建一个规则，该规则会在单击按钮时调用异步函数。

![创建异步函数的规则](/help/forms/using/assets/rule-for-async-funct.png)

请参阅下面的控制台窗口插图，以演示当用户单击 `Fetch` 按钮，自定义函数 `callAsyncFunction` 将调用，从而调用异步函数 `asyncFunction`. 在控制台窗口中Inspect以查看按钮单击时的响应：

![控制台窗口](/help/forms/using/assets/async-custom-funct-console.png)

让我们深入了解一下自定义函数的功能。

## 自定义函数的各种功能

您可以使用自定义函数向表单添加个性化功能。 这些函数支持各种功能，例如使用特定字段、使用全局字段或缓存。 这种灵活性允许您根据组织的要求自定义表单。

### 自定义函数中的字段和全局范围对象 {#support-field-and-global-objects}

字段对象是指表单中的单个组件或元素，例如文本字段和复选框。 全局对象包含只读变量，例如表单实例、目标字段实例以及在自定义函数中修改表单的方法。

>[!NOTE]
>
> 此 `param {scope} globals` 必须是最后一个参数，且不会显示在自适应表单的规则编辑器中。

<!-- Let us look at the following code snippet:

```JavaScript
   
    /**
    * updateDateTime
    * @name updateDateTime
    * @param {object} field
    * @param {scope} globals
    */
    function updateDateTime(field, globals) {
    // Accessing the Date object from the global scope
    var currentDate = new Date();
    // Formatting the date and time
    var formattedDateTime = currentDate.toLocaleString();
    // Updating the field value with the formatted date and time using setProperty.
    globals.functions.setProperty(field, {value: formattedDateTime});
    }
```

In the above code snippet, a custom function named `updateDateTime` takes parameters such as a field object and a global object. The field represents the textbox object where the formatted date and time value is displayed within the form. -->

让我们了解自定义函数如何在 `Contact Us` 使用不同用例的表单。

![联系我们表单](/help/forms/using/assets/contact-us-form.png)

#### **用例**：使用显示面板 `SetProperty` 规则

在自定义函数中添加以下代码，如 [create-custom-function](#create-custom-function) 部分，将表单字段设置为 `Required`.

```javascript
    
    /**
    * enablePanel
    * @name enablePanel
    * @param {object} field1
    * @param {object} field2
    * @param {scope} globals 
    */

    function enablePanel(field1,field2, globals)
    {
       if(globals.functions.validate(field1).length === 0)
       {
       globals.functions.setProperty(field2, {visible: true});
       }
    }
```

>[!NOTE]
>
> * 您可以使用中的可用属性配置字段属性 `[form-path]/jcr:content/guideContainer.model.json`.
> * 使用对表单进行的修改 `setProperty` globals对象的方法本质上是异步的，在执行自定义函数期间不会反映出来。

在此示例中，验证 `personaldetails` 单击按钮时会出现面板。 如果在面板、其他面板、 `feedback` 面板中，单击按钮后会变为可见。

让我们为 `Next` 按钮，用于验证 `personaldetails` 面板并将 `feedback`  用户单击 `Next` 按钮。

![设置属性](/help/forms/using/assets/custom-function-set-property.png)

请参阅下图以演示 `personaldetails` 单击 `Next` 按钮。 如果 `personaldetails` 经过验证， `feedback` 面板将变为可见。

![设置属性表单预览](/help/forms/using/assets/set-property-form-preview.png)

如果的字段中出现错误 `personaldetails` 面板中，单击 `Next` 按钮，以及 `feedback` 面板将保持不可见。

![设置属性表单预览](/help/forms/using/assets/set-property-panel.png)

#### **用例**：验证字段。

在自定义函数中添加以下代码，如 [create-custom-function](#create-custom-function) 部分，以验证字段。

```javascript
    /**
    * validateField
    * @name validateField
    * @param {object} field
    * @param {scope} globals
    */
    function validateField(field,globals)
    {
    
        globals.functions.validate(field);
    
    }   
```

>[!NOTE]
>
> 如果未在中传递参数 `validate()` 函数中，它验证表单。

在此示例中，自定义验证模式应用于 `contact` 字段。 用户需要输入以开头的电话号码 `10` 后接 `8` 数字。 如果用户输入的电话号码开头不是 `10` 或包含多于 `8` 数字，单击按钮时将显示验证错误消息：

![电子邮件地址验证模式](/help/forms/using/assets/custom-function-validation-pattern.png)

现在，下一步是为创建规则 `Next` 验证 `contact` 字段单击。

![验证模式](/help/forms/using/assets/custom-function-validate.png)

请参阅下图以演示，如果用户输入的电话号码开头不是 `10`，则字段级别会显示一条错误消息：

![电子邮件地址验证模式](/help/forms/using/assets/custom-function-validate-error-message.png)

如果用户输入有效的电话号码和 `personaldetails` 面板已经过验证， `feedback` 屏幕上会显示以下面板：

![电子邮件地址验证模式](/help/forms/using/assets/validate-form-preview-form.png)

#### **用例**：重置面板

在自定义函数中添加以下代码，如 [create-custom-function](#create-custom-function) 部分，以重置面板。

```javascript
    /**
    * resetField
    * @name  resetField
    * @param {string} input1
    * @param {object} field
    * @param {scope} globals 
    */
    function  resetField(field,globals)
    {
    
        globals.functions.reset(field);
    
    }
```

>[!NOTE]
>
> 如果未在中传递参数 `reset()` 函数中，它验证表单。

在此示例中， `personaldetails` 单击 `Clear` 按钮。 下一步是为创建规则 `Clear` 按钮上用于重置面板的按钮单击。

![清除按钮](/help/forms/using/assets/custom-function-reset-field.png)

请参阅下图以显示，如果用户单击 `clear` 按钮， `personaldetails` 面板重置：

![重置表单](assets/custom-function-reset-form.png)

#### **用例**：在字段级别显示自定义消息并将字段标记为无效

您可以使用 `markFieldAsInvalid()` 函数将字段定义为无效，并在字段级别设置自定义错误消息。 此 `fieldIdentifier` 值可以是 `fieldId`，或 `field qualifiedName`，或 `field dataRef`. 名为的对象的值 `option` 可以是 `{useId: true}`， `{useQualifiedName: true}`，或 `{useDataRef: true}`.
用于将字段标记为无效并设置自定义消息的语法包括：

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

在自定义函数中添加以下代码，如 [create-custom-function](#create-custom-function) 部分，以在字段级别启用自定义消息。

```javascript
    /**
    * customMessage
    * @name customMessage
    * @param {object} field
    * @param {scope} globals 
    */
    function customMessage(field, globals) {
    const minLength = 15;
    const comments = field.$value.trim();
    if (comments.length < minLength) {
        globals.functions.markFieldAsInvalid(field.$id, "Comments must be at least 15 characters long.", { useId: true });
    }
}
```

在此示例中，如果用户在“注释”文本框中输入的字符数少于15个，则会在字段级别显示自定义消息。

下一步是为创建规则 `comments` 字段：

![将字段标记为无效](/help/forms/using/assets/custom-function-invalid-field.png)

请观看下面的演示，了解如何在 `comments` 字段触发在字段级别显示自定义消息：

![将字段标记为无效预览表单](/help/forms/using/assets/custom-function-invalidfield-form.png)

如果用户在“评论”文本框中输入的字符超过15个，则验证该字段并提交表单：

![将字段标记为有效的预览表单](/help/forms/using/assets/custom-function-validfield-form.png)


#### **用例**：将更改的数据提交到服务器

以下代码行：
`globals.functions.submitForm(globals.functions.exportData(), false);` 用于在操作后提交表单数据。
* 第一个参数是要提交的数据。
* 第二个参数表示在提交之前是否验证表单。 它是 `optional` 并设置为 `true` 默认情况下。
* 第三个理由是 `contentType` ，此选项也是可选的，默认值为 `multipart/form-data`. 其他值可以是 `application/json` 和 `application/x-www-form-urlencoded`.

在自定义函数中添加以下代码，如 [create-custom-function](#create-custom-function) 部分，在服务器上提交操作数据：

```javascript
    /**
    * submitData
    * @name submitData
    * @param {object} field
    * @param {scope} globals 
    */
    function submitData(globals)
    {
    
    var data = globals.functions.exportData();
    if(!data.comments) {
    data.comments = 'NA';
    }
    console.log('After update:{}',data);
    globals.functions.submitForm(data, false);
    }
```

在此示例中，如果用户将 `comments` 文本框为空， `NA` 在提交表单时提交到服务器。

现在，为创建规则 `Submit` 提交数据的按钮：

![提交数据](/help/forms/using/assets/custom-function-submit-data.png)

请参阅图示 `console window` 以下说明，如果用户离开 `comments` 文本框为空，则值为 `NA` 在服务器上提交：

![在控制台窗口中提交数据](/help/forms/using/assets/custom-function-submit-data-form.png)

您还可以检查控制台窗口以查看提交到服务器的数据：

![控制台窗口中的Inspect数据](/help/forms/using/assets/custom-function-submit-data-console-data.png)

<!--

#### **Use Case**: Display form submission and failure messages for custom submit action 

Add the following line of code as explained in the [create-custom-function ](#create-custom-function) section, to customize the submission or failure message for form submissions and display the form submission messages in a modal box:

```javascript
/**
 * Handles the success response after a form submission.
 *
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitSuccessHandler(globals) {
    var event = globals.event;
    var submitSuccessResponse = event.payload.body;
    var form = globals.form;

    if (submitSuccessResponse) {
        if (submitSuccessResponse.redirectUrl) {
            window.location.href = encodeURI(submitSuccessResponse.redirectUrl);
        } else if (submitSuccessResponse.thankYouMessage) {
            showModal("success", submitSuccessResponse.thankYouMessage);
        }
    }
}

/**
 * Handles the error response after a form submission.
 *
 * @param {string} customSubmitErrorMessage - The custom error message.
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitErrorHandler(customSubmitErrorMessage, globals) {
    showModal("error", customSubmitErrorMessage);
}
function showModal(type, message) {
    // Remove any existing modals
    var existingModal = document.getElementById("modal");
    if (existingModal) {
        existingModal.remove();
    }

    // Create the modal dialog
    var modal = document.createElement("div");
    modal.setAttribute("id", "modal");
    modal.setAttribute("class", "modal");

    // Create the modal content
    var modalContent = document.createElement("div");
    modalContent.setAttribute("class", "modal-content");

    // Create the modal header
    var modalHeader = document.createElement("div");
    modalHeader.setAttribute("class", "modal-header");
    modalHeader.innerHTML = "<h2>" + (type === "success" ? "Thank You" : "Error") + "</h2>";

    // Create the modal body
    var modalBody = document.createElement("div");
    modalBody.setAttribute("class", "modal-body");
    modalBody.innerHTML = "<p class='" + type + "-message'>" + message + "</p>";

    // Create the modal footer
    var modalFooter = document.createElement("div");
    modalFooter.setAttribute("class", "modal-footer");

    // Create the close button
    var closeButton = document.createElement("button");
    closeButton.setAttribute("class", "close-button");
    closeButton.innerHTML = "Close";
    closeButton.onclick = function() {
        modal.remove();
    };

    // Append the elements to the modal content
    modalFooter.appendChild(closeButton);
    modalContent.appendChild(modalHeader);
    modalContent.appendChild(modalBody);
    modalContent.appendChild(modalFooter);

    // Append the modal content to the modal
    modal.appendChild(modalContent);

    // Append the modal to the document body
    document.body.appendChild(modal);
}
```

In this example, when the user uses the `customSubmitSuccessHandler` and `customSubmitErrorHandler` custom functions, the success and failure messages are displayed in a modal. The JavaScript function `showModal(type, message)` is used to dynamically create and display a modal dialog box on a screen.

Now, create a rule for successful form submission:

![Form submission success](/help/forms/using/assets/form-submission-success.png)

Refer to the illustration below to demonstrate that when the form is submitted successfully, the success message is displayed in a modal:

![Form submission success message](/help/forms/using/assets/form-submission-success-message.png )
 
Similarly, let us create a rule for failed form submissions:

![Form submission fail](/help/forms/using/assets/form-submission-fail.png)

Refer to the illustration below to demonstrate that when the form submission fails, the error message is displayed in a modal:

![Form submission fail message](/help/forms/using/assets/form-submission-fail-message.png )

To display form submission success and failure in a default manner, the `Default submit Form Success Handler` and `Default submit Form Error Handler` functions are available out of the box.

In case, the custom submit action fails to perform as expected in existing AEM projects or forms, refer to the [troubleshooting](#troubleshooting) section.

-->

## 对自定义函数的缓存支持

自适应Forms在规则编辑器中检索自定义函数列表时，为自定义函数实施缓存以增强响应时间。 消息为 `Fetched following custom functions list from cache` 显示在 `error.log` 文件。

![支持缓存的自定义函数](/help/forms/using/assets/custom-function-cache-error.png)

如果修改了自定义函数，缓存将失效，并且会进行解析。

## 疑难解答 {#troubleshooting}

* 用户需要确保 [核心组件和规范版本设置为最新版本](https://github.com/adobe/aem-core-forms-components/tree/release/650). 但是，对于现有AEM项目和表单，还需要执行其他步骤：

   * 对于AEM项目，用户应替换 `submitForm('custom:submitSuccess', 'custom:submitError')` 替换为 `submitForm()` 并部署该项目。

   * 对于现有表单，如果自定义提交处理程序无法正常运行，用户需要打开并保存 `submitForm` 规则 **提交** 按钮。 此操作替换中的现有规则 `submitForm('custom:submitSuccess', 'custom:submitError')` 替换为 `submitForm()` 在表格中。


* 如果包含自定义函数代码的JavaScript文件出错，则自定义函数将不会在自适应表单的规则编辑器中列出。 要检查自定义函数列表，您可以导航到 `error.log` 文件查找错误。 如果出现错误，自定义函数列表显示为空：

  ![错误日志文件](/help/forms/using/assets/custom-function-list-error-file.png)

  如果没有错误，则会获取自定义函数并显示在 `error.log` 文件。 消息为 `Fetched following custom functions list` 显示在 `error.log` 文件：

  ![使用正确的自定义函数创建错误日志文件](/help/forms/using/assets/custom-function-list-fetched-in-error.png)

## 注意事项

* 此 `parameter type` 和 `return type` 不支持 `None`.

* 自定义函数列表中不支持的函数包括：
   * 生成器函数
   * 异步/等待函数
   * 方法定义
   * 类方法
   * 默认参数
   * Rest参数


