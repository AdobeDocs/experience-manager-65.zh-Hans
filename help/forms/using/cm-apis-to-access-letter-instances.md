---
title: 用于访问书信实例的API
description: 发现API并使用它们以编程方式访问AEM Forms环境中的信件实例。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: 9d43d9d4-5487-416c-b641-e807227ac056
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 1%

---

# 用于访问书信实例的API {#apis-to-access-letter-instances}

## 概述 {#overview}

使用通信管理的创建通信UI，您可以保存正在处理的信件实例草稿，并且存在已提交的信件实例。

通信管理为您提供API，您可以使用这些API构建列表界面以处理已提交的信件实例或草稿。 代理的API列表和打开的提交和草稿信件实例，以便代理可以继续处理草稿或提交的信件实例。

## 正在获取书信实例 {#fetching-letter-instances}

通信管理公开用于通过LetterInstanceService服务提取信件实例的API。

| 方法 | 描述 |
|--- |--- |
| getAllLetterInstances | 根据输入查询参数获取信件实例。 要获取所有信件实例，请将查询参数作为null传递。 |
| getLetterInstance | 根据书信实例ID获取指定的书信实例。 |
| letterInstanceExist | 检查给定名称是否存在LetterInstance。 |

>[!NOTE]
>
>LetterInstanceService是一种OSGI服务，可以在Java中使用@Reference检索其实例™
>类或sling.getService(LetterInstanceService)。 类)。

### 使用getAllLetterInstances {#using-nbsp-getallletterinstances}

以下API根据查询对象（已提交和草稿）查找书信实例。 如果查询对象为null，则返回所有信件实例。 此API返回[LetterInstanceVO](https://helpx.adobe.com/cn/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html)对象的列表，该列表可用于提取信件实例的附加信息。

**语法**： `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>参数</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>查询</td>
   <td>查询参数用于查找/筛选书信实例。 此处，查询仅支持对象的顶级属性/属性。 查询由语句组成，Statement对象中使用的“attributeName”应为Letter实例对象中属性的名称。<br /> </td>
  </tr>
 </tbody>
</table>

#### 示例1：提取SUBMITTED类型的所有信件实例 {#example-fetch-all-the-letter-instances-of-type-submitted}

以下代码返回已提交书信实例的列表。 要仅获取草稿，请将`LetterInstanceType.COMPLETE.name()`更改为`LetterInstanceType.DRAFT.name().`

```java
@Reference
LetterInstanceService letterInstanceService;
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

#### 示例2：提取用户提交的所有信件实例，信件实例类型为“草稿” {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

以下代码在同一查询中有多个语句，用于获取根据不同的条件过滤的结果，例如用户提交的信件实例（属性提交者）以及letterInstanceType类型为DRAFT。

```java
@Reference
LetterInstanceService letterInstanceService;

String submittedBy = "tglodman";
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);

Statement statementForSubmittedBy = new Statement();
statementForSubmittedBy .setAttributeName("submittedby");
statementForSubmittedBy .setOperator(Operator.EQUALS);
statementForSubmittedBy .setAttributeValue(submittedBy);
query.addStatement(statementForSubmittedBy );
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

### 使用getLetterInstance {#using-nbsp-getletterinstance}

获取由给定的书信实例ID标识的书信实例。 如果实例ID不匹配，则返回“ null ”。

**语法：** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### 正在验证LetterInstance是否存在 {#verifying-if-letterinstance-exist}

检查是否存在具有给定名称的书信实例

**语法**： `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **参数** | **描述** |
|---|---|
| 书信实例名称 | 要检查其是否存在的书信实例的名称。 |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## 打开书信实例 {#opening-letter-instances}

书信实例可以是已提交或草稿类型。 打开两种信件实例类型时，会显示不同的行为：

* 如果存在已提交信件实例，则会打开表示该信件实例的PDF。 服务器上保留的提交的书信实例还包含dataXML和已处理的XDP，这可用于完成并进一步自定义用例，如创建PDF/A。
* 如果存在草稿信件实例，则创建通信UI将重新加载到与创建草稿时完全相同的先前状态

### 打开草稿信件实例  {#opening-draft-letter-instance-nbsp}

CCR UI支持cmLetterInstanceId参数，该参数可用于重新加载书信。

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>重新加载通信时，不必指定cmLetterId或cmLetterName/State/Version，因为提交的数据已包含有关重新加载的通信的所有详细信息。 RandomNo用于避免浏览器缓存问题，您可以将时间戳用作随机数。

### 打开已提交的书信实例 {#opening-submitted-letter-instance}

可以使用书信实例ID直接打开提交的PDF：

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
