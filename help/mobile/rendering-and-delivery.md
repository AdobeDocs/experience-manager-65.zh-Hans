---
title: 呈现和交付
description: 了解如何通过Sling默认Servlet呈现Adobe Experience Manager内容以呈现JSON和其他格式。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: f0c543ae-33ed-40bb-9eb7-0dc3bdea69e0
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 6%

---

# 呈现和交付{#rendering-and-delivery}

{{ue-over-mobile}}

通过[Sling默认Servlet](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html)可轻松呈现Adobe Experience Manager (AEM)内容，以呈现[JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering)和其他格式。

这些开箱即用的渲染通常在存储库中导航，并按原样返回内容。

通过Sling，AEM还支持开发和部署自定义sling渲染器，以完全控制渲染的架构和内容。

Content Services默认呈现器填补了开箱即用的Sling默认设置和自定义开发之间的空白，允许在不进行开发的情况下自定义和控制呈现内容的许多方面。

下图显示了内容服务的渲染。

![chlimage_1-15](assets/chlimage_1-15.png)

## 请求JSON {#requesting-json}

使用&#x200B;**&lt;资源.caas[。&lt;EXPORT-CONFIG][。&lt;EXPORT-CONFIG].json**&#x200B;以请求JSON。

<table>
 <tbody>
  <tr>
   <td>资源</td>
   <td>/content/entities<br />或<br />下的实体资源是/content下的内容资源</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>可选</strong><br /> </p> <p>在/apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG<br /> <br />下找到的导出配置如果省略，则应用默认的导出配置 </p> </td>
  </tr>
  <tr>
   <td>DEPTH-INT</td>
   <td>在Sling渲染中使用的用于渲染子项的<strong>可选</strong><br /> <br />深度递归</td>
  </tr>
 </tbody>
</table>

## 创建导出配置 {#creating-export-configs}

可创建导出配置以自定义JSON渲染。

您可以在&#x200B;*/apps/mobileapps/caas/exportConfigs.*&#x200B;下创建一个配置节点。

| 节点名称 | 配置的名称（用于呈现选择器） |
|---|---|
| jcr:primaryType | nt:unstructured |

下表显示了“导出配置”的属性：

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>默认（如果，未设置）</strong></td>
   <td><strong>价值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>includecomponents</td>
   <td>String[]</td>
   <td>包括所有内容</td>
   <td>sling:resourceType</td>
   <td>从JSON导出中排除具有指定sling：resourceType的节点的详细信息</td>
  </tr>
  <tr>
   <td>excludecomponents</td>
   <td>String[]</td>
   <td>不排除任何内容</td>
   <td>sling:resourceType</td>
   <td>仅包含具有来自JSON导出的指定sling：resourceType的节点的详细信息</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>String[]</td>
   <td>不排除任何内容</td>
   <td>属性前缀</td>
   <td>从JSON导出中排除以指定前缀开头的属性</td>
  </tr>
  <tr>
   <td>excludeproperties</td>
   <td>String[]</td>
   <td>不排除任何内容</td>
   <td>属性名称</td>
   <td>从JSON导出中排除指定的属性</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>String[]</td>
   <td>包括所有内容</td>
   <td>属性名称</td>
   <td><p>如果excludePropertyPrefixes设置<br />，这将包含指定的属性，尽管这与要排除的前缀匹配，</p> <p>else（忽略排除属性）仅包括这些属性</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>String[]</td>
   <td>包括所有内容</td>
   <td>子名称</td>
   <td>从JSON导出中排除指定的子项</td>
  </tr>
  <tr>
   <td>excludechildren</td>
   <td>String[]<br /> <br /> </td>
   <td>不排除任何内容</td>
   <td>子名称</td>
   <td>从JSON导出中仅包括指定的子项，排除其他</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>String[]<br /> <br /> </td>
   <td>不重命名任何内容</td>
   <td>&lt;实际属性名称&gt;，&lt;替换属性名称&gt;</td>
   <td>使用替换重命名属性</td>
  </tr>
 </tbody>
</table>

### 资源类型导出覆盖 {#resource-type-export-overrides}

在&#x200B;*/apps/mobileapps/caas/exportConfigs下创建配置节点。*

| name | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

下表显示了这些属性：

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>默认（如果，未设置）</strong></td>
   <td><strong>价值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>&lt;选择器TO_INC&gt;</td>
   <td>String[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>对于以下sling资源类型，请勿返回默认的CaaS json导出。<br />通过将资源呈现为；<br /> &lt;RESOURCE&gt;返回客户json导出。&lt;SELECTOR_TO_INC&gt;.json </td>
  </tr>
 </tbody>
</table>

### 现有Content Services导出配置 {#existing-content-services-export-configs}

Content Services包括两种导出配置：

* 默认（未指定配置）
* 页面（渲染站点页面）

#### 默认导出配置 {#default-export-configuration}

如果在请求的URI中指定了配置，则会应用Content Services默认导出配置。

&lt;资源>.caas[。&lt;DEPTH-INT>].json

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td>excludeproperties</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>jcr：，sling：，cq：，oak：，pge-</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>jcr：text，text<br /> jcr：title，title<br /> jcr：description，description<br /> jcr：lastModified，lastModified<br /> cq：tags，tags<br /> cq：lastModified，lastModified</td>
  </tr>
  <tr>
   <td>includecomponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludecomponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludechildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>Sling JSON覆盖</td>
   <td>foundation/components/image<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### 页面导出配置 {#page-export-configuration}

此配置扩展了缺省设置，以包含子节点下的分组子节点。

&lt;SITE_PAGE>.caas.page[。&lt;DEPTH-INT>].json

### 其他资源 {#additional-resources}

请参阅以下资源，了解内容服务中的其他主题：

* [开发模型](/help/mobile/administer-mobile-apps.md)
* [创作内容服务](/help/mobile/develop-content-as-a-service.md)
* [管理内容服务](/help/mobile/developing-content-services.md)
