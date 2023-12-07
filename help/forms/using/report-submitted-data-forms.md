---
title: 用于处理表单门户上提交的表单的API
description: AEM Forms提供了API，您可以使用这些API在Forms Portal中查询已提交的表单数据并对其执行操作。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish, developer-reference
feature: Forms Portal
exl-id: a685889e-5d24-471c-926d-dbb096792bc8
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 4%

---

# 用于处理表单门户上提交的表单的API {#apis-to-work-with-submitted-forms-on-forms-portal}

AEM Forms提供了可用于查询通过表单门户提交的表单数据的API。 此外，您可以使用本文档中介绍的API发布注释或更新已提交表单的属性。

>[!NOTE]
>
>必须将调用API的用户添加到审阅人组，如中所述 [将提交审阅人关联到表单](/help/forms/using/adding-reviewers-form.md).

## GET/content/forms/portal/submission.review.json？func=getFormsForSubmissionReview {#get-content-forms-portal-submission-review-json-func-getformsforsubmissionreview-br}

返回所有符合条件的表单的列表。

### URL参数 {#url-parameters}

此API不需要其他参数。

### 响应 {#response}

响应对象包含一个JSON数组，其中包含表单名称及其存储库路径。 响应的结构如下：

```json
[
 {formName: "<form name>",
 formPath: "<path to the form>" },
 {.....},
 ......]
```

### 示例 {#example}

**请求URL**

```http
https://[host]:[port]/content/forms/portal/submission.review.json?func=getFormsForSubmissionReview
```

**响应**

```json
[{"formPath":"/content/dam/formsanddocuments/forms-review/form2","formName":"form2"},{"formPath":"/content/dam/formsanddocuments/forms-review/form1","formName":"form1"}]
```

## GET/content/forms/portal/submission.review.json？func=getAllSubmissions {#get-content-forms-portal-submission-review-json-func-getallsubmissions}

返回所有已提交表单的详细信息。 但是，您可以使用URL参数来限制结果。

### URL参数 {#url-parameters-1}

在请求URL中指定以下参数：

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>formPath</code></td>
   <td>指定表单所在的CRX存储库路径。 如果不指定表单路径，则会返回空响应。<br /> </td>
  </tr>
  <tr>
   <td><code>offset</code><br /> （可选）</td>
   <td>指定结果集索引中的起点。 默认值为 <strong>0</strong>.</td>
  </tr>
  <tr>
   <td><code>limit</code><br /> （可选）</td>
   <td>限制结果的数量。 默认值为 <strong>30</strong>.</td>
  </tr>
  <tr>
   <td><code>orderby</code> <br /> （可选）</td>
   <td>指定用于排序结果的属性。 默认值为 <strong>jcr：lastModified</strong>，根据上次修改时间对结果进行排序。</td>
  </tr>
  <tr>
   <td><code>sort</code> <br /> （可选）</td>
   <td>指定排序结果的顺序。 默认值为 <strong>desc</strong>，按降序对结果进行排序。 您可以指定 <code>asc</code> 以对结果进行升序排序。</td>
  </tr>
  <tr>
   <td><code>cutPoints</code> <br /> （可选）</td>
   <td>指定要包含在结果中的表单属性的逗号分隔列表。 默认属性为：<br /> <code>formName</code>， <code>formPath</code>， <code>submitID</code>， <code>formType</code>， <code>jcr:lastModified</code>， <code>owner</code></td>
  </tr>
  <tr>
   <td><code>search</code> <br /> （可选）</td>
   <td>在表单属性中搜索指定的值并返回具有匹配值的表单。 默认值为 <strong>“”</strong>.</td>
  </tr>
 </tbody>
</table>

### 响应 {#response-1}

响应对象包含一个JSON数组，该数组包含指定表单的详细信息。 响应的结构如下：

```json
{
 total: "<total number of submissions>",
 items: [{ formName: "<name of the form>", formPath: "<path to the form>", owner: "<owner of the form>"},
 ....]}
```

### 示例 {#example-1}

**请求URL**

```http
https://[host]:[port]/content/forms/portal/submission.review.json?func=getAllSubmissions&formPath=/content/dam/formsanddocuments/forms-review/form2
```

**响应**

```json
{"total":1,"items":[{"formName":"form2","formPath":"/content/dam/formsanddocuments/forms-review/form2","submitID":"1403037413508500","formType":"af","jcr:lastModified":"2015-11-05T17:52:32.243+05:30","owner":"admin"}]}
```

## POST/content/forms/portal/submission.review.json？func=addComment {#post-content-forms-portal-submission-review-json-func-addcomment-br}

向指定的提交实例添加注释。

### URL参数 {#url-parameters-2}

在请求URL中指定以下参数：

| 参数 | 描述 |
|---|---|
| `submitID` | 指定与提交实例关联的元数据ID。 |
| `Comment` | 指定要添加到指定提交实例的注释文本。 |

### 响应 {#response-2}

在成功发布评论时返回评论ID。

### 示例 {#example-2}

**请求URL**

```http
https://[host:'port'/content/forms/portal/submission.review.json?func=addComment&submitID=1403037413508500&comment=API+test+comment
```

**响应**

```java
1403873422601300
```

## GET/content/forms/portal/submission.review.json？func=getComments   {#get-content-forms-portal-submission-review-json-func-getcomments-nbsp}

返回在指定提交实例上发布的所有评论。

### URL参数 {#url-parameters-3}

在请求URL中指定以下参数：

| 参数 | 描述 |
|---|---|
| `submitID` | 指定提交实例的元数据ID。 |

### 响应 {#response-3}

响应对象包含一个JSON数组，该数组包含与指定提交ID关联的所有注释。 响应的结构如下：

```json
[{
 owner: "<name of the commenter>",
 comment: "<comment text>",
 time: "<time when the comment was posted>"},
 { }......]
```

### 示例 {#example-3}

**请求URL**

```http
https://[host]:'port'/content/forms/portal/submission.review.json?func=getComments&submitID=1403037413508500
```

**响应**

```java
[{"owner":"fr1","comment":"API test comment","time":1446726988250}]
```

## POST/content/forms/portal/submission.review.json？func=updateSubmission {#post-content-forms-portal-submission-review-json-func-updatesubmission-br}

更新指定提交的表单实例的指定属性的值。

### URL参数 {#url-parameters-4}

在请求URL中指定以下参数：

| 参数 | 描述 |
|---|---|
| `submitID` | 指定与提交实例关联的元数据ID。 |
| `property` | 指定要更新的表单属性。 |
| `value` | 指定要更新的表单属性的值。 |

### 响应 {#response-4}

返回包含有关所发布更新的信息的JSON对象。

### 示例 {#example-4}

**请求URL**

```http
https://[host]:'port'/content/forms/portal/submission.review.json?func=updateSubmission&submitID=1403037413508500&value=sample_value&property=some_new_prop
```

**响应**

```json
{"formName":"form2","owner":"admin","jcr:lastModified":1446727516593,"path":"/content/forms/fp/admin/submit/metadata/1403037413508500.html","submitID":"1403037413508500","status":"submitted"}
```
