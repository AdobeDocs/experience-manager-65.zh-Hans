---
title: 将Create Correspondence UI与您的自定义门户集成
seo-title: 将Create Correspondence UI与您的自定义门户集成
description: 了解如何将创建通信UI与自定义门户集成
seo-description: 了解如何将创建通信UI与自定义门户集成
uuid: 68ef5bf2-b271-4c44-8840-6c495069164d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 0d3bb98e-7139-4d8e-b110-6ebd11debda1
docset: aem65
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 4%

---


# 将Create Correspondence UI与自定义门户{#integrating-create-correspondence-ui-with-your-custom-portal}集成

## 概述 {#overview}

本文详细介绍了如何将创建通信解决方案与您的环境集成。

## 基于URL的调用{#url-based-invocation}

从自定义门户调用Create Correspondence应用程序的一种方法是使用以下请求参数准备URL:

* 字母模板的标识符（使用cmLetterId参数）。

* 从所需数据源获取的XML数据的URL（使用cmDataUrl参数）。

例如，自定义门户会将URL准备为\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`，可能是门户上链接的href。

>[!NOTE]
>
>以这种方式调用是不安全的，因为通过在URL中显示相同（明显可见）的参数作为GET请求传递。

>[!NOTE]
>
>在调用Create Corresponence应用程序之前，请保存并上传数据，以在给定的dataURL上调用Create Corresponence UI。 这可以从自定义门户本身或通过其他后端进程完成。

## 基于内联数据的调用{#inline-data-based-invocation}

调用“创建通信”应用程序的另一种（也是更安全的）方法是直接点击https://&#39;[server]:[port]&#39;/[contextPath]/aem/forms/createcorrespondence.html上的URL，同时发送参数和数据以作为POST请求调用“创建通信”应用程序（将它们隐藏在最终用户面前）。 这也意味着您现在可以随行传递Create Correndence应用程序的XML数据（作为同一请求的一部分，使用cmData参数），这在以前的方法中是不可能的/理想的。

### 用于指定字母{#parameters-for-specifying-letter}的参数

| **名称** | **类型** | **描述** |
|---|---|---|
| cmLetterInstanceId | 字符串 | 字母实例的标识符。 |
| cmLetterId | 字符串 | Letter模板的名称。 |

表中的参数顺序指定用于加载字母的参数的首选项。

### 用于指定XML数据源{#parameters-for-specifying-the-xml-data-source}的参数

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td> 
   <td><strong>类型</strong></td> 
   <td><strong>描述</strong></td> 
  </tr>
  <tr>
   <td>cmDataUrl<br /> </td> 
   <td>URL</td> 
   <td>使用基本协议（如cq、ftp、http或文件）从源文件获取XML数据。<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>字符串</td> 
   <td>使用Letter实例中可用的xml数据。</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>布尔型</td> 
   <td>重用数据字典中附加的测试数据。</td> 
  </tr>
 </tbody>
</table>

表中的参数顺序指定用于加载XML数据的参数的首选项。

### 其他参数{#other-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td> 
   <td><strong>类型</strong></td> 
   <td><strong>描述</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>布尔型</td> 
   <td>如果在预览模式<br />中打开字母，则为true </td> 
  </tr>
  <tr>
   <td>随机</td> 
   <td>时间戳</td> 
   <td>解决浏览器缓存问题。</td> 
  </tr>
 </tbody>
</table>

如果您对cmDataURL使用http或cq协议，则http/cq的URL应可匿名访问。
