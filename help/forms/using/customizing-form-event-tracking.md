---
title: 自定义表单事件跟踪
description: 如果用户在字段上花费的时间超过60秒，则会触发fieldvisit事件，并将字段的详细信息发送到Adobe SiteCatalyst。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: d0280a15-5d0d-49cf-bce9-ad1c40530eae
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 8a77756e8ba771c8de9950c2323bef8f23cc59b4
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---

# 自定义表单事件跟踪 {#customizing-form-event-tracking}

在支持Analytics的自适应表单中，现成可跟踪以下事件：

<table>
 <tbody>
  <tr>
   <th>事件</th>
   <th>可用变量</th>
  </tr>
  <tr>
   <td>渲染</td>
   <td>formName， formTitle， formInstance， source</td>
  </tr>
  <tr>
   <td>放弃</td>
   <td>formName、formTitle、formInstance、panelName、panelTitle</td>
  </tr>
  <tr>
   <td>保存</td>
   <td>formName， formTitle， formInstance， panelName， source</td>
  </tr>
  <tr>
   <td>提交</td>
   <td>formName， formTitle， formInstance， source</td>
  </tr>
  <tr>
   <td>错误</td>
   <td>formName、formTitle、fieldName、fieldTitle、panelTitle</td>
  </tr>
  <tr>
   <td>帮助</td>
   <td>formName、formTitle、fieldName、fieldTitle、panelTitle</td>
  </tr>
  <tr>
   <td>fieldVisit</td>
   <td>formName， formTitle， fieldName， fieldTitle， panelTitle<br /> </td>
  </tr>
  <tr>
   <td>panelVisit</td>
   <td>formName、formTitle、panelName、panelTitle</td>
  </tr>
 </tbody>
</table>

## 自定义字段访问事件超时 {#customizing-the-field-visit-event-timeout}

在默认的AEM表单设置中，如果用户在某个字段上花费超过60秒，则会触发`fieldvisit`事件并将该字段的详细信息发送到Adobe Analytics。 您可以在AEM配置控制台(/system/console/configMgr)的AEM Forms Analytics配置下自定义字段时间跟踪基线，以增加或减少超时限制。

## 自定义跟踪事件 {#customizing-the-tracking-events}

您可以修改`/libs/afanalytics/js/custom.js`文件中可用的`trackEvent`函数以自定义事件跟踪。 无论何时在自适应表单中发生正在跟踪的事件，都会调用`trackEvent`函数。 `trackEvent`函数接受两个参数： `eventName`和`variableValueMap`。

您可以计算&#x200B;*eventName*&#x200B;和&#x200B;*variableValueMap*&#x200B;参数的值以更改事件的跟踪行为。 例如，您可以选择在发生一定数量的错误事件后将信息发送到Analytics服务器。 您还可以选择执行以下任何自定义设置：

* 您可以在发送事件之前设置阈值时间。
* 您可以维护状态以决定操作，例如&#x200B;*fieldVisit*&#x200B;根据上一个事件的时间戳推送一个虚拟事件。
* 您可以使用`pushEvent`函数将事件发送到分析服务器&#x200B;*。*

* 您可以选择根本不将事件推送到Analytics服务器。

### 样本 {#sample}

在以下示例中，每个&#x200B;*fieldName*&#x200B;属性的&#x200B;*error*&#x200B;事件的状态都得到了维护。 仅当再次发生错误时，才会将该事件发送到Analytics服务器。

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## 自定义面板访问事件 {#customizing-the-panelvisit-event}

在默认的AEM Forms设置中，每60秒后，会检查包含自适应表单的窗口是否处于活动状态。 如果该窗口处于活动状态，则会向Adobe Analytics触发`panelVisit`事件。 它有助于确定文档或表单是否处于活动状态，并计算在相应表单或文档上花费的时间。

>[!NOTE]
>
>用于确定活动和计算逗留时间的事件名称为“panelVisit”。 此事件与上表中所列的面板访问事件不同。

您可以修改`/libs/afanalytics/js/custom.js`文件中可用的scheduleHeartBeatCheck函数，以定期更改或停止发送给Adobe Analytics的此事件。
