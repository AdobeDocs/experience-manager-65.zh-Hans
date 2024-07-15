---
title: 用于从自适应表单调用表单数据模型服务的API
description: 说明可用于从自适应表单字段中调用使用WSDL编写的Web服务的invokeWebServices API。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Adaptive Forms,Foundation Components
exl-id: cf037174-3153-486f-85b1-c974cd5a1ace
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 10%

---

# 用于从自适应表单调用表单数据模型服务的API {#api-to-invoke-form-data-model-service-from-adaptive-forms}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

## 概述 {#overview}

AEM Forms允许表单作者通过从自适应表单字段中调用在表单数据模型中配置的服务，进一步简化和增强表单填写体验。 要调用数据模型服务，您可以在可视编辑器中创建规则，或在[规则编辑器](/help/forms/using/rule-editor.md)的代码编辑器中使用`guidelib.dataIntegrationUtils.executeOperation` API指定JavaScript。

本文档侧重于使用`guidelib.dataIntegrationUtils.executeOperation` API编写JavaScript以调用服务。

## 使用API {#using-the-api}

`guidelib.dataIntegrationUtils.executeOperation` API从自适应表单字段中调用服务。 API语法如下：

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

`guidelib.dataIntegrationUtils.executeOperation` API的结构指定了有关服务操作的详细信息。 此结构的语法如下。

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

API结构指定了有关服务操作的以下详细信息。

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>用于指定表单数据模型标识符、操作标题和操作名称的结构</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>指定表单数据模型的存储库路径，包括其名称</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>指定要执行的服务操作的名称</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>将一个或多个表单对象映射到服务操作的输入参数</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>将一个或多个表单对象映射到服务操作的输出值以填充表单字段<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>基于服务操作的输入参数返回值。 它是用作回调函数的可选参数。<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>如果success回调函数无法根据输入参数显示输出值，则显示错误消息。 它是用作回调函数的可选参数。<br /> </td>
  </tr>
 </tbody>
</table>

## 用于调用服务的示例脚本 {#sample-script-to-invoke-a-service}

以下示例脚本使用`guidelib.dataIntegrationUtils.executeOperation` API调用在`employeeAccount`表单数据模型中配置的`getAccountById`服务操作。

`getAccountById`操作将`employeeID`表单字段中的值作为`empId`参数的输入，并返回相应员工的员工姓名、帐号和帐户余额。 输出值会填充到指定的表单字段中。 例如，`name`参数中的值在`fullName`表单元素中填充，在`account`表单元素中为`accountNumber`参数填充值。

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## 将API与回调函数结合使用 {#using-the-api-callback}

您还可以使用带有回调函数的`guidelib.dataIntegrationUtils.executeOperation` API调用表单数据模型服务。 API语法如下：

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

回调函数可以有`success`和`failure`回调函数。

### 包含成功和失败回调函数的示例脚本 {#callback-function-success-failure}

以下示例脚本使用`guidelib.dataIntegrationUtils.executeOperation` API调用在`employeeOrder`表单数据模型中配置的`GETOrder`服务操作。

`GETOrder`操作将`Order ID`表单字段中的值作为`orderId`参数的输入并返回`success`回调函数中的订货量值。  如果`success`回调函数未返回订单数量，`failure`回调函数将显示`Error occured`消息。

>[!NOTE]
>
>如果使用`success`回调函数，则指定的表单字段中不会填充输出值。

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
