---
title: HTML5表单的渲染表单模板
seo-title: HTML5表单的渲染表单模板
description: HTML5表单用户档案与用户档案渲染相关联。 用户档案呈现是JSP页，负责通过调用Forms OSGi服务生成表单的HTML表示形式。
seo-description: HTML5表单用户档案与用户档案渲染相关联。 用户档案呈现是JSP页，负责通过调用Forms OSGi服务生成表单的HTML表示形式。
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: 移动设备表单
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---


# HTML5表单的渲染表单模板{#rendering-form-template-for-html-forms}

## 渲染端点{#render-endpoint}

HTML5表单的概念为&#x200B;**用户档案**，它们作为REST端点公开，以启用表单模板的移动渲染。 这些用户档案具有关联的&#x200B;**用户档案渲染器**。 它们是JSP页，负责通过调用Forms OSGi服务生成表单的HTML表示形式。 用户档案节点的JCR路径决定渲染端点的URL。 指向“default”用户档案的表单的默认渲染端点如下所示：

https://&lt;*host*>:&lt;*port*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*包含xdp*>&amp;template=*xdp*&#x200B;名称的文件夹路径

例如，`http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

对于自定义用户档案，端点会相应地更改。 例如，具有hrforms名称的自定义用户档案的终点是：

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

如果您的模板位于名为FormSubmission的应用程序中的AEM存储库中，则URI为：

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## 渲染参数{#render-parameters}

以HTML形式呈现表单时支持的请求参数有：

<table>
 <tbody>
  <tr>
   <th><strong>参数 </strong></th>
   <th><strong>描述</strong></th>
  </tr>
  <tr>
   <td>模板<br /> </td>
   <td>此参数指定模板文件的名称。<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>此参数指定模板和关联资源所在的路径。 此路径可以是服务器文件系统路径、存储库路径、http或ftp路径。<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>此参数指定将表单数据xml发布到的url。<br /> </td>
  </tr>
 </tbody>
</table>

### 将数据与表单模板{#merge-data-with-form-template}合并

| 参数 | 描述 |
|---|---|
| dataRef | 此参数指定与模板合并的数据文件的&#x200B;**绝对路径**。 此参数可以是返回xml格式数据的rest服务的URL。 |
| 数据 | 此参数指定与模板合并的UTF-8编码数据字节。 如果指定此参数，则HTML5表单将忽略dataRef参数。 |

### 传递渲染参数{#passing-the-render-parameter}

HTML5表单支持三种传递渲染参数的方法。 您可以通过URL、键值对和用户档案节点传递参数。 在render参数中，键值对具有最高的优先级，后跟用户档案节点。 URL请求参数的优先级最低。

* **URL请求参数**:您可以在URL中指定渲染参数。在URL请求参数中，参数对最终用户可见。 例如，以下提交URL在URL中包含模板参数：`http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **SetAttribute请求参数**:可以将渲染参数指定为键值对。在SetAttribute请求参数中，参数对最终用户不可见。 您可以将任何其他JSP的请求转发到HTML5表单用户档案呈示器JSP，并在请求对象上使用&#x200B;*setAttribute*&#x200B;传递所有呈现参数。 此方法具有最高优先级。

* **用户档案节点请求参** 数：可以将渲染参数指定为用户档案节点的节点属性。在用户档案节点请求参数中，参数对最终用户不可见。 用户档案节点是发送请求的节点。 要将参数指定为节点属性，请使用CRXDE lite。

### 提交参数{#submit-parameters}

HTML5表单提交数据；在AEM服务器上执行服务器端脚本和web服务。 有关在AEM服务器上执行服务器端脚本和Web服务的参数的详细信息，请参阅[HTML5 forms Service Proxy](/help/forms/using/service-proxy.md)。
