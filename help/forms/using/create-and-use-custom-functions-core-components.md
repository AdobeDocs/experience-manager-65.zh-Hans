---
title: 在自适应表单中创建和添加自定义函数
description: AEM Forms支持自定义函数，这些函数允许用户在规则编辑器中创建和使用自己的函数。
keywords: 添加自定义函数、使用自定义函数、创建自定义函数、在规则编辑器中使用自定义函数。
content-type: reference
feature: Adaptive Forms, Core Components
role: Admin, User, Developer
exl-id: 00073e3a-f1b5-4c42-9fea-4a14b8a22c81
source-git-commit: 7f1283898cbeebdedb7bdea6f0a8d9db567617ee
workflow-type: tm+mt
source-wordcount: '3385'
ht-degree: 2%

---

# 自适应核心组件中的自定义函数Forms

本文介绍了如何使用最新的自适应表单核心组件创建自定义函数，这些组件具有最新的功能，例如：

* 自定义函数的缓存功能
* 自定义函数的全局范围对象和字段对象支持
* 支持现代JavaScript功能，如左键和箭头功能（支持ES10）

请确保在AEM Forms核心组件环境中设置[最新表单版本](https://github.com/adobe/aem-core-forms-components/tree/release/650)以使用自定义函数中的最新功能。</span>


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | 本文 |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/cn/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/create-and-use-custom-functions) |

## 简介

AEM Forms 6.5包括JavaScript函数，这些函数允许您使用规则编辑器定义复杂的业务规则。 虽然AEM Forms提供了多种现成的自定义函数，但许多用例需要定义您自己的自定义函数才能在多个表单中使用。 这些自定义函数允许根据特定要求处理输入的数据，从而增强表单的功能。 此外，它们允许根据预定义标准动态更改表单行为。

### 自定义函数的使用 {#uses-of-custom-function}

在自适应Forms核心组件中使用自定义函数的优点包括：


* **管理数据**：自定义函数管理并处理输入到表单字段中的数据。
* **正在处理数据**：自定义函数可帮助处理输入到表单字段中的数据。
* **数据验证**：自定义函数允许您对表单输入执行自定义检查并提供指定的错误消息。
* **动态行为**：自定义函数允许您根据特定条件控制表单的动态行为。 例如，您可以显示/隐藏字段、修改字段值或动态调整表单逻辑。
* **集成**：您可以使用自定义函数与外部API或服务集成。 它有助于从外部源获取数据，将数据发送到外部Rest端点，或根据外部事件执行自定义操作。

自定义函数本质上是添加到JavaScript文件中的客户端库。 创建自定义函数后，该函数即可在规则编辑器中供用户在自适应表单中选择。 自定义函数由规则编辑器中的JavaScript注释标识。

### 自定义函数支持的JavaScript批注 {#js-annotations}

**JavaScript注释为JavaScript代码**&#x200B;提供元数据。 它包含以特定符号（例如，`/**`和`@`）开头的注释。 注释提供了有关代码中的函数、变量和其他元素的重要信息。 自适应表单支持自定义函数的以下JavaScript注释：

#### 名称

**Name**&#x200B;用于标识自适应表单的规则编辑器中的自定义函数。 以下语法用于命名自定义函数：

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`

>[!NOTE]
>`[functionName]`是函数的名称。 不允许使用空格。
>`<Function Name>` 是自适应Forms的规则编辑器中函数的显示名称。
>如果函数名称与函数本身的名称相同，则可以在语法中省略`[functionName]`。

#### 参数

**参数**&#x200B;是自定义函数使用的参数列表。 函数可以支持多个参数。 以下语法用于定义自定义函数中的参数：

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`

  `{type}`表示参数类型。 允许的参数类型包括：

   * string：表示单个字符串值。
   * 数字：表示单个数值。
   * 布尔值：表示单个布尔值（true或false）。
   * string[]：表示字符串值的数组。
   * number[]：表示数值的数组。
   * 布尔值[]：表示布尔值的数组。
   * 日期：表示单个日期值。
   * date[]：表示日期值的数组。
   * array：表示包含各种类型值的泛型数组。
   * 对象：表示传递到自定义函数的表单对象，而不是直接传递其值。
   * 范围：表示全局对象，其中包含只读变量，如表单实例、目标字段实例以及在自定义函数中执行表单修改的方法。 此变量声明为JavaScript注释中的最后一个参数，对自适应表单的规则编辑器不可见。 scope参数可访问表单或组件的对象，以触发表单处理所需的规则或事件。 有关Globals对象及其使用方法的详细信息，[单击此处](/help/forms/using/create-and-use-custom-functions-core-components.md#field-and-global-scope-objects-in-custom-functions-support-field-and-global-objects)

参数类型为&#x200B;**不区分大小写**，参数名称中不允许有空格。

`<Parameter Description>`包含有关参数用途的详细信息。 它可以有多个单词。

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
  `{type}`表示函数的返回类型。 允许的返回类型包括：
* string：表示单个字符串值。
* 数字：表示单个数值。
* 布尔值：表示单个布尔值（true或false）。
* string[]：表示字符串值的数组。
* number[]：表示数值的数组。
* 布尔值[]：表示布尔值的数组。
* 日期：表示单个日期值。
* date[]：表示日期值的数组。
* array：表示包含各种类型值的泛型数组。
* 对象：表示表单对象，而不是直接表示其值。

返回类型不区分大小写。

#### 专用

声明为私有的自定义函数不会出现在自适应表单的规则编辑器的自定义函数列表中。 默认情况下，自定义函数是公用的。 将自定义函数声明为private的语法为`@private`。

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

如果用户没有将任何JavaScript注释添加到自定义函数，则它按函数名称在规则编辑器中列出。 但是，建议包含JavaScript注释，以提高自定义函数的可读性。


### 带有强制JavaScript注释或注释的Arrow函数

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

### 带有必需JavaScript注释或注释的函数表达式

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

* **纯文本编辑器(IDE)**：虽然任何纯文本编辑器都可以工作，但诸如Microsoft Visual Studio Code之类的集成开发环境(IDE)可提供高级功能，以便于编辑。

* **Git：**&#x200B;管理代码更改需要此版本控制系统。 如果未安装，请从https://git-scm.com下载。


## 创建自定义功能 {#create-custom-function}

创建自定义函数的步骤包括：
1. [使用AEM项目原型创建客户端库并添加自定义函数](#create-client-library-archetype)
或者
   [通过CRXDE创建自定义函数](#create-add-custom-function)
1. [将客户端库添加到自适应表单](#add-client-library)
1. [在自适应表单中使用自定义函数](#use-custom-functions)


### 使用AEM项目原型创建客户端库{#create-client-library-archetype}

您可以向使用AEM项目原型](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/archetype/using#getting-started)创建的项目[中添加客户端库，从而添加自定义函数。
如果您现有项目<!--and have already the project structure as shown in the image below,-->，则可以直接将[自定义函数](#create-add-custom-function)添加到本地项目。

<!--![custom fuction folder structure](assets/custom-library-folder-structure.png)-->

创建原型项目或使用现有项目后，请创建客户端库。 要创建客户端库，请执行以下步骤：

**添加客户端库文件夹**

要将新的客户端库文件夹添加到[AEM项目目录]，请执行以下步骤：

1. 在编辑器中打开[AEM项目目录]。

   ![自定义函数文件夹结构](assets/custom-library-folder-structure.png)

1. 找到`ui.apps`。
1. 添加新文件夹。 例如，添加名为`experience-league`的文件夹。
1. 导航到`/experience-league/`文件夹并添加`ClientLibraryFolder`。 例如，创建一个名为`customclientlibs`的客户端库文件夹。

   位置为： `[AEM project directory]/ui.apps/src/main/content/jcr_root/apps/`

**将文件和文件夹添加到客户端库文件夹**

将以下内容添加到添加的客户端库文件夹：

* `.content.xml`文件
* `js.txt`文件
* `js`文件夹

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. 在`.content.xml`中，添加以下代码行：

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > 您可以为`client library folder`和`categories`属性选择任意名称。

1. 在`js.txt`中，添加以下代码行：

   ```javascript
         #base=js
       function.js
   ```

1. 在`js`文件夹中，将javascript文件添加为`function.js`，其中包含自定义函数：

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

1. 导航到[AEMaaCS项目目录]中的`/ui.apps/src/main/content/META-INF/vault/filter.xml`文件。

1. 打开文件，并在末尾添加以下行：

   `<filter root="/apps/experience-league" />`
1. 保存文件。

   ![自定义函数筛选器xml](assets/custom-function-filterxml.png)

1. 按照[如何生成部分](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype#how-to-build)中给出的步骤将新创建的客户端库文件夹生成到您的AEM环境。

## 通过CRXDE创建和部署自定义函数{#create-add-custom-function}

如果您使用最新的AEM Forms和Forms加载项，则可以通过CRXDE创建自定义函数，以使用自定义函数的最新更新。 为此，请执行以下步骤：

<!--![custom fuction folder structure](assets/custom-library-folder-structure.png)-->


1. 登录`http://server:port/crx/de/index.jsp#`。
1. 在 `/apps` 文件夹下创建一个文件夹。例如，创建名为`experience-league`的文件夹。
1. 保存更改。
1. 导航到已创建的文件夹，并创建类型为`cq:ClientLibraryFolder`的节点作为`clientlibs`。
1. 导航到新创建的`clientlibs`文件夹并添加`allowProxy`和`categories`属性：

   ![自定义库节点属性](/help/forms/using/assets/customlibrary-catproperties.png)

   >[!NOTE]
   >
   > 您可以提供任意名称来取代`customfunctionsdemo`。

1. 保存更改。

1. 在`clientlibs`文件夹下创建名为`js`的文件夹。
1. 在`js`文件夹下创建名为`functions.js`的JavaScript文件。
1. 在`clientlibs`文件夹下创建名为`js.txt`的文件。
1. 保存更改。
创建的文件夹结构如下所示：

   ![创建的客户端库文件夹结构](/help/forms/using/assets/clientlibrary_folderstructure.png)
1. 双击`functions.js`文件以打开编辑器。 该文件包含自定义函数的代码。
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

1. 保存`function.js`。
1. 导航到`js.txt`并添加以下代码：

   ```javascript
       #base=js
       functions.js
   ```

1. 保存 `js.txt` 文件。

您可以引用以下[自定义函数](/help/forms/using/assets/customfunction.zip)文件夹。 在您的AEM实例上下载并安装此文件夹。

现在，您可以通过添加客户端库在自适应表单中使用自定义函数。

## 在自适应表单中添加客户端库{#add-client-library}

将客户端库部署到AEM Forms环境后，请在自适应表单中使用其功能。 在自适应表单中添加客户端库

1. 在编辑模式下打开表单。 若要在编辑模式下打开表单，请选择一个表单，然后选择&#x200B;**[!UICONTROL 编辑]**。
1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性图标。 这将打开“自适应表单容器”对话框。
1. 打开&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡，并从下拉列表中选择&#x200B;**[!UICONTROL 客户端库类别]**&#x200B;的名称（在本例中，选择`customfunctionscategory`）。

   ![正在添加自定义函数客户端库](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. 单击&#x200B;**[!UICONTROL 完成]**。

现在，您可以创建一个规则以在规则编辑器中使用自定义函数：

![正在添加自定义函数客户端库](/help/forms/using//assets/calculateage-customfunction.png)

现在，让我们了解如何在AEM Forms 6.5](/help/forms/using/rule-editor-core-components.md#invoke-form-data-model-service-invoke)中使用[规则编辑器的调用服务来配置和使用自定义函数

## 在自适应表单中使用自定义函数 {#use-custom-functions}

在自适应表单中，您可以在规则编辑器](/help/forms/using/rule-editor-core-components.md)中使用[自定义函数。
让我们将以下代码添加到JavaScript文件（`Function.js`文件）中，以根据出生日期(YYYY-MM-DD)计算年龄。 创建自定义函数作为`calculateAge()`，它将出生日期作为输入并返回年龄：

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

在上例中，当用户以(YYYY-MM-DD)格式输入出生日期时，将调用自定义函数`calculateAge`并返回年龄。

![在规则编辑器中计算Age自定义函数](/help/forms/using/assets/custom-function-calculate-age.png)

让我们预览表单，观察自定义函数如何通过规则编辑器实现：

![在规则编辑器表单预览中计算Age自定义函数](/help/forms/using/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> 您可以引用以下[自定义函数](/help/forms/using/assets/customfunctions.zip)文件夹。 使用[包管理器](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager)在AEM实例中下载并安装此文件夹。

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

在上述示例中，asyncFunction函数是`asynchronous function`。 它通过向`https://petstore.swagger.io/v2/store/inventory`发出`GET`请求来执行异步操作。 它使用`await`等待响应，使用`response.json()`将响应正文解析为JSON，然后返回数据。 `callAsyncFunction`函数是一个同步自定义函数，它调用`asyncFunction`函数并在控制台中显示响应数据。 虽然`callAsyncFunction`函数是同步的，但它调用异步asyncFunction函数并使用`then`和`catch`语句处理其结果。

要查看其是否有效，让我们添加一个按钮，并为按钮创建一个规则，该规则会在单击按钮时调用异步函数。

![为异步函数创建规则](/help/forms/using/assets/rule-for-async-funct.png)

请参考控制台窗口的插图以演示当用户单击`Fetch`按钮时，将调用自定义函数`callAsyncFunction`，进而调用异步函数`asyncFunction`。 在控制台窗口中Inspect以查看按钮单击时的响应：

![控制台窗口](/help/forms/using/assets/async-custom-funct-console.png)

让我们深入了解一下自定义函数的功能。

## 自定义函数的各种功能

您可以使用自定义函数向表单添加个性化功能。 这些函数支持各种功能，例如使用特定字段、使用全局字段或缓存。 这种灵活性允许您根据组织的要求自定义表单。

### 自定义函数中的字段和全局范围对象 {#support-field-and-global-objects}

字段对象是指表单中的单个组件或元素，例如文本字段和复选框。 全局对象包含只读变量，例如表单实例、目标字段实例以及在自定义函数中修改表单的方法。

>[!NOTE]
>
> `param {scope} globals`必须是最后一个参数，它不会显示在自适应表单的规则编辑器中。

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

让我们了解自定义函数如何在`Contact Us`表单的帮助下使用字段和全局对象，该表单使用不同的用例。

![与我们联系表单](/help/forms/using/assets/contact-us-form.png)

#### **用例**：使用`SetProperty`规则显示面板

将以下代码添加到[create-custom-function](#create-custom-function)部分中说明的自定义函数中，以将表单字段设置为`Required`。

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
> * 您可以使用位于`[form-path]/jcr:content/guideContainer.model.json`中的可用属性配置字段属性。
> * 使用Globals对象的`setProperty`方法对该表单进行的修改是异步的，在执行自定义函数期间不会反映这些修改。

在此示例中，`personaldetails`面板的验证是在单击按钮时进行的。 如果在面板中未检测到错误，则单击按钮后，另一个面板（`feedback`面板）将变为可见。

让我们为`Next`按钮创建一个规则，该规则将验证`personaldetails`面板，并在用户单击`Next`按钮时使`feedback`面板可见。

![设置属性](/help/forms/using/assets/custom-function-set-property.png)

请参阅下图以演示单击`Next`按钮时验证`personaldetails`面板的位置。 如果`personaldetails`中的所有字段都已验证，`feedback`面板将变为可见。

![设置属性表单预览](/help/forms/using/assets/set-property-form-preview.png)

如果`personaldetails`面板的字段中存在错误，则单击`Next`按钮时会在字段级别显示这些错误，并且`feedback`面板将保持不可见。

![设置属性表单预览](/help/forms/using/assets/set-property-panel.png)

#### **用例**：验证字段。

按照[create-custom-function](#create-custom-function)部分中的说明，在自定义函数中添加以下代码以验证字段。

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
> 如果未在`validate()`函数中传递任何参数，它将验证表单。

在此示例中，自定义验证模式应用于`contact`字段。 用户需要输入以`10`开头后接`8`位数的电话号码。 如果用户输入的电话号码不以`10`开头或包含多或少`8`位数，则单击该按钮时将显示验证错误消息：

![电子邮件地址验证模式](/help/forms/using/assets/custom-function-validation-pattern.png)

现在，下一步是为`Next`按钮创建一个规则，以验证单击按钮时的`contact`字段。

![验证模式](/help/forms/using/assets/custom-function-validate.png)

请参阅下图以演示，如果用户输入的电话号码不是以`10`开头，则在字段级别将显示错误消息：

![电子邮件地址验证模式](/help/forms/using/assets/custom-function-validate-error-message.png)

如果用户输入有效的电话号码并且验证`personaldetails`面板中的所有字段，屏幕上会显示`feedback`面板：

![电子邮件地址验证模式](/help/forms/using/assets/validate-form-preview-form.png)

#### **用例**：重置面板

按照[create-custom-function](#create-custom-function)部分中的说明，在自定义函数中添加以下代码以重置面板。

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
> 如果未在`reset()`函数中传递任何参数，它将验证表单。

在此示例中，`personaldetails`面板在单击`Clear`按钮时重置。 下一步是为`Clear`按钮创建一个规则，该规则将在单击按钮时重置面板。

![清除按钮](/help/forms/using/assets/custom-function-reset-field.png)

请参阅下图以显示，如果用户单击`clear`按钮，`personaldetails`面板将重置：

![重置表单](assets/custom-function-reset-form.png)

#### **用例**：在字段级别显示自定义消息并将字段标记为无效

您可以使用`markFieldAsInvalid()`函数将字段定义为无效，并在字段级别设置自定义错误消息。 `fieldIdentifier`值可以是`fieldId`、`field qualifiedName`或`field dataRef`。 名为`option`的对象的值可以是`{useId: true}`、`{useQualifiedName: true}`或`{useDataRef: true}`。
用于将字段标记为无效并设置自定义消息的语法包括：

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

按照[create-custom-function](#create-custom-function)部分中的说明，在自定义函数中添加以下代码，以在字段级别启用自定义消息。

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

下一步是为`comments`字段创建规则：

![将字段标记为无效](/help/forms/using/assets/custom-function-invalid-field.png)

请参阅下面的演示，说明在`comments`字段中输入负反馈会触发字段级别的自定义消息显示：

![将字段标记为无效的预览表单](/help/forms/using/assets/custom-function-invalidfield-form.png)

如果用户在“评论”文本框中输入的字符超过15个，则验证该字段并提交表单：

![将字段标记为有效的预览表单](/help/forms/using/assets/custom-function-validfield-form.png)


#### **用例**：将更改的数据提交到服务器

以下代码行：
`globals.functions.submitForm(globals.functions.exportData(), false);`用于在操作后提交表单数据。
* 第一个参数是要提交的数据。
* 第二个参数表示在提交之前是否验证表单。 它是`optional`，默认设置为`true`。
* 第三个参数是提交的`contentType`，该参数也是可选的，默认值是`multipart/form-data`。 其他值可以是`application/json`和`application/x-www-form-urlencoded`。

按照[create-custom-function](#create-custom-function)部分中的说明，在自定义函数中添加以下代码，以在服务器上提交操作数据：

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

在此示例中，如果用户将`comments`文本框留空，则`NA`在提交表单时提交给服务器。

现在，为提交数据的`Submit`按钮创建规则：

![提交数据](/help/forms/using/assets/custom-function-submit-data.png)

请参阅以下`console window`的图示，以演示如果用户将`comments`文本框留空，则在服务器上提交值为`NA`：

![在控制台窗口提交数据](/help/forms/using/assets/custom-function-submit-data-form.png)

您还可以检查控制台窗口以查看提交到服务器的数据：

在控制台窗口![Inspect数据](/help/forms/using/assets/custom-function-submit-data-console-data.png)

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

自适应Forms在规则编辑器中检索自定义函数列表时，为自定义函数实施缓存以增强响应时间。 `error.log`文件中显示一条消息，名称为`Fetched following custom functions list from cache`。

支持缓存的![自定义函数](/help/forms/using/assets/custom-function-cache-error.png)

如果修改了自定义函数，缓存将失效，并且会进行解析。

## 疑难解答 {#troubleshooting}

* 用户需要确保[核心组件和规范版本设置为最新版本](https://github.com/adobe/aem-core-forms-components/tree/release/650)。 但是，对于现有AEM项目和表单，还需要执行其他步骤：

   * 对于AEM项目，用户应使用`submitForm()`替换`submitForm('custom:submitSuccess', 'custom:submitError')`的所有实例并部署该项目。

   * 对于现有表单，如果自定义提交处理程序无法正常运行，用户需要使用规则编辑器在&#x200B;**提交**&#x200B;按钮上打开并保存`submitForm`规则。 此操作将`submitForm('custom:submitSuccess', 'custom:submitError')`中的现有规则替换为表单中的`submitForm()`。


* 如果包含自定义函数代码的JavaScript文件出错，则自定义函数不会列在自适应表单的规则编辑器中。 要检查自定义函数列表，您可以导航到`error.log`文件以查找错误。 如果出现错误，自定义函数列表显示为空：

  ![错误日志文件](/help/forms/using/assets/custom-function-list-error-file.png)

  如果没有错误，则会获取自定义函数并显示在`error.log`文件中。 `error.log`文件中显示一条消息，名称为`Fetched following custom functions list`：

  使用正确的自定义函数![错误日志文件](/help/forms/using/assets/custom-function-list-fetched-in-error.png)

## 注意事项

* `parameter type`和`return type`不支持`None`。

* 自定义函数列表中不支持的函数包括：
   * 生成器函数
   * 异步/等待函数
   * 方法定义
   * 类方法
   * 默认参数
   * Rest参数
