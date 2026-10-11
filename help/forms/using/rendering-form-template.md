---
title: 为 HTML5 Forms 渲染表单模板
description: HTML5表单配置文件与配置文件渲染关联。 配置文件渲染器是JSP页，负责通过调用HTML OSGi服务来生成表单的Forms表示形式。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: HTML5 Forms,Mobile Forms
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 3%
---
# 为 HTML5 Forms 渲染表单模板 {#rendering-form-template-for-html-forms}

## 渲染端点 {#render-endpoint}

HTML5表单具有&#x200B;**配置文件**&#x200B;的概念，这些配置文件公开为REST端点以启用表单模板的移动设备渲染。 这些配置文件已关联&#x200B;**配置文件渲染器**。 它们是JSP页，负责通过调用HTML OSGi服务来生成Forms表单表示形式。 “配置文件”节点的JCR路径决定了渲染端点的URL。 表单的默认渲染端点指向“default”配置文件，如下所示：

https://<*主机*>：<*端口*>/content/xfaforms/profiles/default.html?contentRoot=<*包含表单xdp*>&template=<*名称xdp*>的文件夹路径

例如，`http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

对于自定义配置文件，端点会相应地更改。 例如，名为hrforms的自定义用户档案的端点为：

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

如果您的模板驻留在名为FormSubmission的应用程序的AEM存储库中，则URI为：

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## 渲染参数 {#render-parameters}

将表单渲染为HTML时支持的请求参数包括：

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
   <td>此参数指定模板和相关资源所在的路径。 此路径可以是服务器文件系统路径或存储库路径、http或ftp路径。<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>此参数指定将表单数据xml发布到的URL。<br /> </td>
  </tr>
 </tbody>
</table>

### 将数据与表单模板合并 {#merge-data-with-form-template}

| 参数 | 描述 |
|---|---|
| dataRef | 此参数指定与模板合并的数据文件的&#x200B;**绝对路径**。 此参数可以是一个指向rest服务的URL，该服务以xml格式返回数据。 |
| 数据 | 此参数指定与模板合并的UTF-8编码数据字节。 如果指定此参数，HTML5表单将忽略dataRef参数。 |

### 传递渲染参数 {#passing-the-render-parameter}

HTML5 Forms支持三种传递渲染参数的方法。 您可以通过URL、键值对和配置文件节点传递参数。 在渲染参数中，键值对具有最高的优先级，其后是配置文件节点。 URL请求参数的优先级最低。

* **URL请求参数**：您可以在URL中指定渲染参数。 在URL请求参数中，这些参数对于最终用户可见。 例如，以下提交URL在URL中包含模板参数： `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **SetAttribute请求参数**：您可以将渲染参数指定为键值对。 在SetAttribute请求参数中，最终用户看不到这些参数。 您可以将请求从任何其他JSP转发到HTML5表单配置文件渲染器JSP，并在请求对象上使用&#x200B;*setAttribute*&#x200B;传递所有渲染参数。 此方法具有最高优先权。

* **配置文件节点请求参数：**&#x200B;您可以将渲染参数指定为配置文件节点的节点属性。 在配置文件节点请求参数中，最终用户看不到这些参数。 配置文件节点是发送请求的节点。 要将参数指定为节点属性，请使用CRXDE lite。

### 提交参数 {#submit-parameters}

HTML5 forms提交数据；在AEM服务器上执行服务器端脚本和Web服务。 有关用于在AEM服务器上执行服务器端脚本和Web服务的参数的详细信息，请参阅[HTML5表单服务代理](/help/forms/using/service-proxy.md)。
