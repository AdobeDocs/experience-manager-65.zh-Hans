---
title: 内容片段模板
description: 创建内容片段时会选择模板，并为新片段提供基本结构、元素和变量
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 1b75721c-b223-41f0-88d9-bd855b529f31
solution: Experience Manager, Experience Manager Sites
feature: Developing,Content Fragments
role: Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 3%

---

# 内容片段模板{#content-fragment-templates}

>[!CAUTION]
>
>建议使用[内容片段模型](/help/assets/content-fragments/content-fragments-models.md)来创建所有新的内容片段。
>
>内容片段模型用于WKND中的所有示例。

>[!NOTE]
>
>在AEM 6.3之前，内容片段是基于模板而不是模型创建的。
>
>现已弃用内容片段模板。 它们仍可用于创建片段，但建议改用内容片段模型。 不会向片段模板中添加任何新功能，并且会在未来版本中删除这些功能。

创建内容片段时可以选择模板。 它们为新片段提供基本结构、元素和变量。 用于内容片段的模板受Granite配置管理器的约束。

现成的模板保存在下：

* `/libs/settings/dam/cfm/templates`

您可以在以下位置为内容片段创建特定于站点的模板：

* `/apps/settings/dam/cfm/templates`
用于覆盖现成模板或提供特定于客户的应用程序范围的模板的位置，这些模板在运行时不会进行扩展/更改。

* `/conf/global/settings/dam/cfm/templates`
运行时需要更改的全实例客户特定模板的位置。

优先顺序为（降序） `/conf`、`/apps`、`/libs`。

>[!CAUTION]
>
>您&#x200B;***必须***&#x200B;不更改`/libs`路径中的任何内容。
>
>这是因为下次升级实例时`/libs`的内容会被覆盖（在应用修补程序或功能包时很可能会被覆盖）。
>
>建议用于配置和其他更改的方法是：
>
>1. 在`/apps`下重新创建所需项（即`/libs`中存在的项）
>
>1. 在`/apps`中进行任何更改
>

模板的基本结构保存在下：

```xml
conf
  global
    settings
      dam
        cfm
          templates
            <template-name>
              ...
```

具体结构为：

```xml
+ <template-name>
    - jcr:primaryType
    - jcr:title
    - jcr:description
    - initialAssociatedContent
    - precreateElements
    - version
    + elements
        - jcr:primaryType
        + <element-name>
            - jcr:primaryType
            - jcr:title
            - defaultContent
            - initialContentType
            - name
        ... + other element definitions
    + variations
        - jcr:primaryType
        + <variation-name>
            - jcr:primaryType
            - jcr:title
            - jcr:description
            - name
        ... + other variation definitions
```

有关节点及其属性的更多详细信息包括：

* **模板**

  <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>价值</th>
    </tr>
    <tr>
     <td><code>&lt;<em>template-name</em>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>此节点是每个模板的根。 它是强制性的，应具有唯一名称。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必需<br /> </p> </td>
     <td>模板的标题（显示在<strong>创建片段</strong>向导中）。</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>可选</p> </td>
     <td>描述模板用途的文本（显示在<strong>创建片段</strong>向导中）。</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>可选</p> </td>
     <td>一个数组，其中包含指向集合的路径，默认情况下，这些路径应关联到新创建的内容片段。</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>必填</p> </td>
     <td><p><code>true</code>，如果在创建内容片段时应该创建表示内容片段的元素（主元素除外）的子资产；如果应该“动态”创建子资产，则为<em>false</em>。</p> <p><strong>注意</strong>：当前此参数必须设置为<code>true</code>。</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>必填</p> </td>
     <td><p>内容结构的版本；当前支持：</p> <p><strong>注意</strong>：当前此参数必须设置为<code>2</code>。<br /> </p> </td>
    </tr>
   </tbody>
  </table>

* **元素**

  <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>价值</th>
    </tr>
    <tr>
     <td><code>elements</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>必填</p> </td>
     <td><p>包含内容片段元素定义的节点。 它是强制性的，并且需要为<strong>Main</strong>元素至少包含一个子节点，但可以包含[1.n]个子节点。</p> <p>使用模板时，元素子分支复制到片段的模型子分支。</p> <p>第一个元素(在CRXDE Lite中查看)自动视为<i>main</i>元素；节点名称不相关，并且节点本身除了由主资源表示之外，不具有特殊意义；其他元素作为子资源处理。</p> </td>
    </tr>
   </tbody>
  </table>

* **元素名称**

  <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>价值</th>
    </tr>
    <tr>
     <td><code>&lt;<i>element-name</i>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>此节点定义一个元素。 它是强制性的，应具有唯一名称。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必填</p> </td>
     <td>元素的标题（显示在片段编辑器的元素选择器中）。</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>可选</p> <p>默认：“”</p> </td>
     <td>元素的初始内容；仅在<code>precreateElements</code><i> = </i><code>true</code>时使用</td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>可选</p> <p>默认： <code>text/html</code></p> </td>
     <td><p>元素的初始内容类型；仅在<code>precreateElements</code><i> = </i><code>true</code>时使用；当前支持：</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>必填</p> </td>
     <td>元素的内部名称；对于片段类型必须是唯一的。</td>
    </tr>
   </tbody>
  </table>

* **变体**

  <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>价值</th>
    </tr>
    <tr>
     <td><code>variations</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>可选</p> </td>
     <td>此可选节点包含内容片段的初始变体的定义。</td>
    </tr>
   </tbody>
  </table>

* **变量名称**

  <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>价值</th>
    </tr>
    <tr>
     <td><code>&lt;<i>variation-name</i>&gt;</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>如果存在变体节点，则此为必填字段</p> </td>
     <td><p>定义初始变量。<br />默认情况下，该变量会添加到内容片段的所有元素。</p> <p>变体的初始内容将与相应元素相同（请参阅<code class="code">defaultContent/
       initialContentType</code>）</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必填</p> </td>
     <td>变量的标题(显示在片段编辑器的<strong>变量</strong>选项卡中（左边栏）)。</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>可选</p> <p>默认：“”</p> </td>
     <td>提供变量<span>的描述的文本(显示在片段编辑器的<strong>变量</strong>选项卡中（左边栏）)。</code></td>
    </tr>
   </tbody>
  </table>
