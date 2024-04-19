---
title: 在自适应表单中创建和添加自定义函数
description: AEM Forms支持自定义函数，这些函数允许用户在规则编辑器中创建和使用自己的函数。
keywords: 添加自定义函数、使用自定义函数、创建自定义函数、在规则编辑器中使用自定义函数。
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: a328b4a8-e8dd-42a0-b73b-94e76c7692a8
source-git-commit: a5b48f1f4072f3e10273ec90d6f505815fe584a3
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 5%

---


# 自适应Forms中的自定义函数（核心组件）

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/create-and-use-custom-functions) |
| AEM 6.5 | 本文 |

## 简介

AEM Forms 6.5引入了用于定义JavaScript函数的功能，这些函数可用于通过规则编辑器定义复杂的业务规则。 AEM Forms提供了许多现成的此类自定义函数，但您需要定义自己的自定义函数并在多个表单中使用它们。

自定义函数通过促进对输入数据的操作和处理来扩展表单的功能，以满足特定要求。 它们还支持根据预定义标准动态更改表单行为。
在自适应Forms中，您可以使用中的自定义函数 [自适应表单的规则编辑器](/help/forms/using/rule-editor.md) 创建表单字段的特定验证规则。
让我们了解自定义功能的使用，用户可以在其中输入电子邮件地址，您希望确保输入的电子邮件地址遵循特定格式（其中包含“@”符号和域名）。 创建自定义函数为“ValidateEmail”，该函数将电子邮件地址作为输入，如果有效，则返回true；否则返回false。

```javascript
function ValidateEmail(inputText)
{
    var email = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
    if(inputText.value.match(email))
        {
            alert("Valid email address!");
            return true;
        }
    else
    {
        alert("Invalid email address!");
        return false;
    }
}
```

在上述示例中，当用户尝试提交表单时，将调用自定义函数“ValidateEmail”以检查输入的电子邮件地址是否有效。

## 自定义函数的使用 {#uses-of-custom-function}

在自适应Forms中使用自定义函数的优点包括：

* **数据操作**：自定义函数处理并处理输入到表单字段中的数据。
* **数据验证**：通过自定义函数，可对表单输入执行自定义检查并提供指定的错误消息。
* **动态行为**：自定义函数允许您根据特定条件控制表单的动态行为。 例如，您可以显示/隐藏字段、修改字段值或动态调整表单逻辑。
* **集成**：您可以使用自定义函数与外部API或服务集成。 它有助于从外部源获取数据，将数据发送到外部Rest端点，或根据外部事件执行自定义操作。

## 支持的JS注释

请确保您编写的自定义函数附带 `jsdoc` 在上面，如果您需要自定义配置和描述。 有多种方法可以在中声明函数 `JavaScript,` 和注释可让您跟踪功能。 有关更多信息，请参阅 [usejsdoc.org](https://jsdoc.app/).

支持 `jsdoc` 标记：

* **私有**
语法： `@private`
专用函数未作为自定义函数包含在内。

* **名称**
语法： `@name funcName <Function Name>`
或者 `,` 您可以使用： `@function funcName <Function Name>` **或** `@func` `funcName <Function Name>`.
  `funcName` 是函数的名称（不允许有空格）。
  `<Function Name>` 是函数的显示名称。

* **会员**
语法： `@memberof namespace`
将命名空间附加到函数。

* **参数**
语法： `@param {type} name <Parameter Description>`
或者，您可以使用： `@argument` `{type} name <Parameter Description>` **或** `@arg` `{type}` `name <Parameter Description>`.
显示函数使用的参数。 一个函数可以有多个参数标记，每个参数按其出现顺序对应一个标记。
  `{type}` 表示参数类型。 允许的参数类型包括：

   1. 字符串
   2. 数字
   3. 布尔型
   4. 范围

  范围用于引用自适应表单的字段。 当表单使用延迟加载时，您可以使用 `scope` 以访问其字段。 在加载字段时或字段标记为全局时，您可以访问这些字段。

  所有其他参数类型均归入上述参数类型之一。 不支持无。 确保选择以上类型之一。 类型不区分大小写。 参数中不允许有空格 `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **返回类型**
语法： `@return {type}`
或者，您可以使用 `@returns {type}`.
添加有关函数的信息，例如其目标。
{type} 表示函数的返回类型。 允许的返回类型包括：

   1. 字符串
   1. 数字
   1. 布尔型

  所有其他退货类型均归入上述任一类型下。 不支持无。 确保选择以上类型之一。 返回类型不区分大小写。

* **此**
语法： `@this currentComponent`

  使用@this引用编写了规则的自适应表单组件。

  以下示例基于字段值。 在以下示例中，规则隐藏了表单中的字段。 此 `this` 部分 `this.value` 是指用于编写规则的底层自适应表单组件。

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
  >使用自定义函数之前的注释进行摘要。 在遇到标记之前，摘要可以扩展到多行。 将大小限制为单个，以便在规则生成器中提供简要说明。

## 函数声明支持的类型 {#function-declaration-supported-types}

**函数语句**

```javascript
function area(len) {
    return len*len;
}
```

此函数包含但不包含 `jsdoc` 注释。

**函数表达式**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**函数表达式和语句**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**函数声明作为变量**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

限制：自定义函数仅从变量列表中选取第一个函数声明（如果同时选取）。 您可以对每个声明的函数使用函数表达式。

**函数声明作为对象**

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

## 创建自定义函数 {#create-custom-function}

要创建自定义函数，请执行以下步骤：

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
1. 创建名为的JavaScript文件 `functions.js` 在 `js` 文件夹
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

您可以参考以下内容 [自定义函数](/help/forms/using/assets/customfunction.zip) 文件夹。 在AEM实例中下载并安装此文件夹。

现在，您可以通过添加客户端库在自适应表单中使用自定义函数。

## 在自适应表单中添加客户端库{#use-custom-function}

将客户端库部署到Forms CS环境后，请在自适应表单中使用其功能。 在自适应表单中添加客户端库

1. 在编辑模式下打开表单。 要在编辑模式下打开表单，请选择一个表单，然后选择 **[!UICONTROL 编辑]**.
1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性图标。 这将打开“自适应表单容器”对话框。
1. 打开 **[!UICONTROL 基本]** 选项卡并选择的名称 **[!UICONTROL 客户端库类别]** (在本例中，选择 `customfunctionscategory`)。

   ![添加自定义函数客户端库](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. 单击 **[!UICONTROL 完成]** .

现在，您可以创建一个规则以在规则编辑器中使用自定义函数：

![添加自定义函数客户端库](/help/forms/using//assets/calculateage-customfunction.png)

现在，让我们了解如何使用 [AEM Forms中的规则编辑器的调用服务](/help//forms/using/rule-editor.md).
