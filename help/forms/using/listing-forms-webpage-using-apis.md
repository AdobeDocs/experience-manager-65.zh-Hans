---
title: 使用API在网页上列出表单
seo-title: 使用API在网页上列出表单
description: 以编程方式查询Forms Manager以检索已过滤的表单列表并显示在您自己的网页上。
seo-description: 以编程方式查询Forms Manager以检索已过滤的表单列表并显示在您自己的网页上。
uuid: e51cb2d4-816f-4e6d-a081-51e4999b00ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 515ceaf6-c132-4e1a-b3c6-5d2c1ccffa7c
translation-type: tm+mt
source-git-commit: db69c393fc44ca2fcb30f9fcb0c5ca456ba35ed5

---


# 使用API在网页上列出表单 {#listing-forms-on-a-web-page-using-apis}

AEM Forms提供基于REST的搜索API,Web开发人员可以使用它查询和检索一组满足搜索条件的表单。 您可以使用API根据各种筛选器搜索表单。 响应对象包含表单属性、属性和渲染表单的端点。

要使用REST API搜索表单，请使用下面描述的查询参数将GET请 `https://[server]:[port]/libs/fd/fm/content/manage.json` 求发送到服务器。

## Query parameters {#query-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>属性名称<br /> </strong></td>
   <td><strong>描述<br /> </strong></td>
  </tr>
  <tr>
   <td>函数<br /> </td>
   <td><p>指定要调用的函数。 要搜索表单，请将属性的 <code>func </code>值设置为 <code>searchForms</code>。</p> <p>例如， <code class="code">
       URLParameterBuilder entityBuilder=new URLParameterBuilder ();
       entityBuilder.add("func", "searchForms");</code></p> <p><strong></strong> 注意：此 <em>参数为必填。</em><br /> </p> </td>
  </tr>
  <tr>
   <td>appPath<br /> </td>
   <td><p>指定用于搜索表单的应用程序路径。 默认情况下，appPath属性搜索所有在根节点级别可用的应用程序。<br /> </p> <p>您可以在单个搜索查询中指定多个应用程序路径。 用竖线(|)字符分隔多个路径。 </p> </td>
  </tr>
  <tr>
   <td>cutPoints<br /> </td>
   <td><p>指定要与资产一起提取的属性。 可以使用星号(*)同时获取所有属性。 使用管道(|)运算符指定多个属性。 </p> <p>例如， <code>cutPoints=propertyName1|propertyName2|propertyName3</code></p> <p><strong>注意</strong>: </p>
    <ul>
     <li><em>始终获取id、路径和名称等属性。 </em></li>
     <li><em>每个资产都有不同的属性集。 formUrl、pdfUrl和guideUrl等属性不取决于自定义点属性。 这些属性取决于资产类型，并相应地获取。 </em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>relation<br /> </td>
   <td>指定要与搜索结果一起提取的相关资产。 您可以选择以下选项之一来获取相关资产：
    <ul>
     <li><strong>NO_RELATION</strong>:请勿提取相关资产。</li>
     <li><strong>立即</strong>:获取与搜索结果直接相关的资产。</li>
     <li><strong>全部</strong>:提取直接和间接相关资产。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>maxSize</td>
   <td>指定要获取的最大表单数。</td>
  </tr>
  <tr>
   <td>偏移</td>
   <td>指定要从开始跳过的表单数。</td>
  </tr>
  <tr>
   <td>returnCount</td>
   <td>指定是否返回与给定条件匹配的搜索结果。 </td>
  </tr>
  <tr>
   <td>语句</td>
   <td><p>指定语句列表。 查询将在JSON格式中指定的语句列表中执行。 </p> <p>例如，</p> <p><code class="code">JSONArray statementArray=new JSONArray();
       JSONObject statement=new JSONObject();
       statement.put("name", "title");
       statement.put("value", "SimpleSurveyAF");
       statement.put("operator", "EQ"); statementArray.put(statement);</code></p> <p>在上例中， </p>
    <ul>
     <li><strong>name</strong>:指定要搜索的属性的名称。</li>
     <li><strong>value</strong>:指定要搜索的属性的值。</li>
     <li><strong>operator</strong>:指定搜索时要应用的运算符。 支持以下运算符：
      <ul>
       <li>EQ —— 等于 </li>
       <li>NEQ —— 不等于</li>
       <li>GT —— 大于</li>
       <li>LT —— 小于</li>
       <li>GTEQ —— 大于或等于</li>
       <li>LTEQ —— 小于或等于</li>
       <li>CONTAINS —— 如果B是A的一部分，则A包含B</li>
       <li>全文——全文搜索</li>
       <li>STARTSWITH —— 如果B是A的开头部分，则A以B开头</li>
       <li>ENDSWITH —— 如果B是A的结束部分，则A以B结束</li>
       <li>LIKE —— 实现LIKE运算符</li>
       <li>AND —— 合并多个语句</li>
      </ul> <p><strong></strong> 注意： <em>GT、LT、GTEQ和LTEQ算子适用于线性类型的属性，如LONG、DOUBLE和DATE。</em></p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>排序<br /> </td>
   <td><p>指定搜索结果的顺序条件。 标准以JSON格式定义。 可以对多个字段上的搜索结果进行排序。 结果按字段在查询中显示的顺序排序。</p> <p>例如，</p> <p>要检索按标题属性按升序排序的查询结果，请添加以下参数： </p> <p><code class="code">JSONArray orderingsArray=new JSONArray();
       JSONObject orderings=new JSONObject();
       orderings.put("name", "title");
       orderings.put("criteria", "ASC");
       orderingsArray.put(orderings);
       entityBuilder.add("orderings", orderingsArray.toString());</code></p>
    <ul>
     <li><strong>name</strong>:指定用于对搜索结果排序的属性名称。</li>
     <li><strong>条件</strong>:指定结果的顺序。 order属性接受以下值：
      <ul>
       <li>ASC —— 使用ASC按升序排列结果。<br /> </li>
       <li>DES —— 使用DES按降序排列结果。</li>
      </ul> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>includeXdp</td>
   <td>指定是否检索二进制内容。 该属 <code>includeXdp</code> 性适用于类型、类型 <code>FORM</code>和 <code>PDFFORM</code>类型的资产 <code>PRINTFORM</code>。</td>
  </tr>
  <tr>
   <td>assetType</td>
   <td>指定要从所有已发布资产中检索的资产类型。 使用管道(|)运算符指定多个资产类型。 有效的资产类型包括FORM、PDFFORM、PRINTFORM、RESOURCE和GUIDE。</td>
  </tr>
 </tbody>
</table>

## 示例请求 {#sample-request}

```
func : searchForms
appPath : /content/dam/formsanddocuments/MyApplication23
cutPoints : title|description|author|status|creationDate|lastModifiedDate|activationDate|expiryDate|tags|allowedRenderFormat|formmodel
relation : NO_RELATION
includeXdp : false
maxSize : 10
offset : 0
returnCount : true
statements: [{"name":"name","value":"*Claim.xdp","operator":"CONTAINS"},
                {"name":"","value":"Expense","operator":"FULLTEXT"},
                {"name":"description","value":"ABCD*","operator":"CONTAINS"},
                {"name":"status","value":"false","operator":"EQ"},
                {"name":"lastModifiedDate","value":"01/09/2013","operator":"GTEQ"},
                {"name":"lastModifiedDate","value":"01/18/2013","operator":"LTEQ"}]
orderings:[{"name" :“lastModifiedDate“:”order”:”ASC”}]
```

## 示例响应 {#sample-response}

```
[
{"resultCount":2},
    {"assetType":"FORM","name":"ExpenseClaim.xdp","id":"509fa2d5-e3c9-407b-b8dc-fa0ba08eb0ce",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDEFGIJK","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"5477a127-8bbf-4cec-8f81-2689e5cb4a15",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/Image.gif","resourceSize":0}],
       "status":false,"creationDate":1358429845623,"lastModifiedDate":1358429846771},
{"assetType":"FORM","name":"ExpenseClaim.xdp","id":"4312239b-b666-4d36-95bc-641b3a39ddd4",
       "path":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDefghijklm","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"118a2e3f-7097-4d8c-85d1-651306de284a",
       "path":"/content/dam/formsanddocuments/MyApplication23/Image.gif","resourceSize":0}],"status":false,
       "creationDate":1358429856690,"lastModifiedDate":1358430109023}
]
```

## 相关文章

* [启用表单门户组件](/help/forms/using/enabling-forms-portal-components.md)
* [创建表单门户页面](/help/forms/using/creating-form-portal-page.md)
* [使用API在网页上列出表单](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交组件](/help/forms/using/draft-submission-component.md)
* [自定义草稿和已提交表单的存储](/help/forms/using/draft-submission-component.md)
* [将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自定义表单门户组件的模板](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在门户上发布表单的简介](/help/forms/using/introduction-publishing-forms.md)