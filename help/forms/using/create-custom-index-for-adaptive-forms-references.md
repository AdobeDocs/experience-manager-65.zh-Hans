---
title: 创建自适应表单引用的自定义索引
description: 了解如何在AEM Forms中为自适应表单引用查询创建标记的Lucene索引，以在发布体验片段时避免遍历查询。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, Developer
source-git-commit: 9240de61985dc32f17593f416e5d054cadb8a392
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 1%
---

# 为自适应表单引用创建自定义索引 {#create-custom-index-for-adaptive-forms-references}

创建带标记的Lucene索引以避免在Adobe Experience Manager (AEM) Forms解析自适应表单引用时遍历查询。 如果没有合适的索引，发布包含自适应表单引用的体验片段可能会在日志中生成`Traversal query (query without index)`警告。

在AEM Forms 6.5.24.0及更高版本中，引用查询使用`aemformsAFReferences`索引标记。 这些发行版本包括查询更改，但必须使用该标记创建自定义索引。 本文介绍了如何定义和部署索引。

对于AEM Forms 6.5 LTS，请参阅[在AEM Forms 6.5 LTS中为自适应表单引用创建自定义索引](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65-lts/content/forms/install-aem-forms/configure-aem-forms/create-custom-index-for-adaptive-forms-references)。

## 先决条件 {#prerequisites}

在开始之前，请确保您具有：

* AEM Forms 6.5.24.0或更高版本，并安装了相应的Forms加载项。
* 在创作实例的`/oak:index`下创建索引的访问权限。
* 具有`ui.apps`模块的AEM项目（如果您通过内容包部署索引），或者访问CRXDE Lite作为开发替代方案。

在将索引部署到生产环境之前，请在开发或暂存环境中测试该索引。 [在大型存储库上生成索引可能需要一些时间](/help/sites-deploying/queries-and-indexing.md#configuring-the-indexes)。

## 定义自定义索引 {#define-the-custom-index}

在`/oak:index/customAFReferenceLuceneIndex-1`处创建索引。 您可以选择其他索引节点名称，但请保持`aemformsAFReferences`标记不变，以便Forms引用查询可以选择该索引。

使用以下定义。 它在`/content`下的`nt:unstructured`节点上索引`sling:resourceType`。

```json
{
  "jcr:primaryType": "oak:QueryIndexDefinition",
  "selectionPolicy": "tag",
  "compatVersion": 2,
  "includedPaths": ["/content"],
  "queryPaths": ["/content"],
  "tags": ["aemformsAFReferences"],
  "type": "lucene",
  "async": ["async"],
  "evaluatePathRestrictions": true,
  "reindex": false,
  "indexRules": {
    "jcr:primaryType": "nt:unstructured",
    "nt:unstructured": {
      "jcr:primaryType": "nt:unstructured",
      "properties": {
        "jcr:primaryType": "nt:unstructured",
        "resourceType": {
          "jcr:primaryType": "nt:unstructured",
          "propertyIndex": true,
          "name": "sling:resourceType"
        }
      }
    }
  }
}
```

不添加`analyzed=true`。 引用查询使用属性限制而不是全文`contains`条件，因此不需要设置。

## 使用内容包部署索引 {#deploy-the-index-with-a-content-package}

使用内容包进行生产部署。

1. 在您的AEM项目的`ui.apps`模块中，创建`ui.apps/src/main/content/jcr_root/_oak_index/customAFReferenceLuceneIndex-1/`。
1. 在该目录中使用以下定义创建`.content.xml`：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:oak="http://jackrabbit.apache.org/oak/ns/1.0"
             xmlns:jcr="http://www.jcp.org/jcr/1.0"
             xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
             jcr:primaryType="oak:QueryIndexDefinition"
             async="[async]"
             compatVersion="{Long}2"
             evaluatePathRestrictions="{Boolean}true"
             includedPaths="[/content]"
             queryPaths="[/content]"
             reindex="{Boolean}false"
             selectionPolicy="tag"
             tags="[aemformsAFReferences]"
             type="lucene">
       <indexRules jcr:primaryType="nt:unstructured">
           <nt:unstructured jcr:primaryType="nt:unstructured">
               <properties jcr:primaryType="nt:unstructured">
                   <resourceType jcr:primaryType="nt:unstructured"
                                 name="sling:resourceType"
                                 propertyIndex="{Boolean}true"/>
               </properties>
           </nt:unstructured>
       </indexRules>
   </jcr:root>
   ```

1. 在`ui.apps/src/main/content/META-INF/vault/filter.xml`中的现有`workspaceFilter`元素中添加以下筛选器。 保持项目的其他筛选器不变。

   ```xml
   <filter root="/oak:index/customAFReferenceLuceneIndex-1"/>
   ```

1. 使用现有的生成配置生成项目，并在创作实例上安装生成的内容包。 有关包上载和安装说明，请参阅[包管理器](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system)。
1. 确认`/oak:index/customAFReferenceLuceneIndex-1`存在。 在检查查询计划之前，允许完成异步索引。

如果选择不同的索引名称，请在目录、筛选器和存储库路径中一致地使用该名称。

## 使用CRXDE Lite创建索引 {#create-the-index-with-crxde-lite}

在开发环境中使用此替代方法，而不是内容包方法。

创建索引节点时，请使用以下属性：

| 属性 | 类型 | 价值 |
| --- | --- | --- |
| `selectionPolicy` | 字符串 | `tag` |
| `compatVersion` | 长 | `2` |
| `includedPaths` | `String[]` | `/content` |
| `queryPaths` | `String[]` | `/content` |
| `tags` | `String[]` | `aemformsAFReferences` |
| `type` | 字符串 | `lucene` |
| `async` | `String[]` | `async` |
| `evaluatePathRestrictions` | 布尔值 | `true` |
| `reindex` | 布尔值 | `false` |

`String[]`表示多值字符串属性，即使它只包含一个值。

1. 打开 `http://localhost:4502/crx/de/index.jsp`。 将主机和端口替换为创作实例的主机和端口。
1. 导航到 `/oak:index`。 右键单击该节点并选择[!UICONTROL 创建] > [!UICONTROL 创建节点]。
1. 创建类型为`oak:QueryIndexDefinition`的`customAFReferenceLuceneIndex-1`。
1. 将上表中的属性添加到索引节点。
1. 在索引节点下，创建以下子节点层次结构。 将每个子节点的类型设置为`nt:unstructured`：

   ```text
   indexRules
       nt:unstructured
           properties
               resourceType
   ```

1. 在`resourceType`上，添加值为`sling:resourceType`的`name` （字符串）和值为`true`的`propertyIndex` （布尔值）。
1. 选择[!UICONTROL 全部保存]并允许异步索引完成。

## 验证查询是否使用索引 {#verify-that-the-query-uses-the-index}

检查查询计划，确认参考查询选择您的自定义索引。

1. 确认异步索引已完成。 使用[索引管理器](/help/sites-administering/operations-dashboard.md#the-index-manager)检查索引状态。
1. 打开[!UICONTROL 工具] > [!UICONTROL 操作] > [!UICONTROL 诊断] > [!UICONTROL 查询性能]并选择[!UICONTROL 说明查询]。 选择XPath查询语言并输入：

   ```text
   /jcr:root/content//element(*, nt:unstructured)[
     (@sling:resourceType = 'fd/af/components/aemform'
     or jcr:like(@sling:resourceType, '%components/aemformscontainer%')
     or jcr:like(@sling:resourceType, '%components/adaptiveForm/fragment%'))]
   option (index tag aemformsAFReferences)
   ```

1. 选择[!UICONTROL 说明]。 确认计划使用`lucene:customAFReferenceLuceneIndex-1`和`/oak:index/customAFReferenceLuceneIndex-1`或您选择的索引名称作为查询的分支而不是遍历计划。 有关详细信息，请参阅[说明查询](/help/sites-administering/operations-dashboard.md#explain-query)。
1. 重复产生警告的体验片段发布操作。 检查`error.log`以了解来自`com.adobe.aem.formsndocuments.publish.AssetReferenceProvider.resolvePathsToFindReferences`的新遍历警告。

如果计划未选择自定义索引，请根据以上示例检查标记、`indexRules`层次结构和`sling:resourceType`属性定义。 有关进一步的诊断，请参阅[Oak索引疑难解答](/help/sites-deploying/troubleshooting-oak-indexes.md)。

## 相关任务 {#related-tasks}

有关查询性能和索引配置的更多信息，请参阅：

* [Oak查询和索引](/help/sites-deploying/queries-and-indexing.md)
* [有关查询和索引的最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [排查查询速度缓慢的问题](/help/sites-developing/troubleshooting-slow-queries.md)
