---
title: 预填自适应表单域
seo-title: 预填自适应表单域
description: 使用现有数据预填自适应表单的字段。
seo-description: 使用自适应表单，用户可以使用其社交用户档案登录来预填表单中的基本信息。 本文介绍如何完成此操作。
uuid: 574de83a-7b5b-4a1f-ad37-b9717e5c14f1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 7139a0e6-0e37-477c-9e0b-aa356991d040
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2202'
ht-degree: 0%

---


# 预填自适应表单字段{#prefill-adaptive-form-fields}

## 简介 {#introduction}

您可以使用现有数据预填自适应表单的字段。 用户打开表单时，将预填这些字段的值。 要在自适应表单中预填数据，请以符合自适应表单数据结构预填格式的预填XML/JSON形式提供用户数据。

## 预填数据{#the-prefill-structure}的结构

自适应表单可以混合绑定和未绑定字段。 绑定字段是从“内容查找器”选项卡中拖动的字段，在字段编辑对话框中包含非空`bindRef`属性值。 未绑定字段将直接从Sidekick的组件浏览器中拖动，并且值`bindRef`为空。

您可以预填自适应表单的绑定和未绑定字段。 预填数据包含afBoundData和afUnBoundData部分，用于预填自适应表单的绑定和未绑定字段。 `afBoundData`部分包含绑定字段和面板的预填数据。 此数据必须与关联的表单模型模式兼容：

* 对于使用[XFA表单模板](../../forms/using/prepopulate-adaptive-form-fields.md)的自适应表单，请使用与XFA模板的数据模式兼容的预填XML。
* 对于使用[XML模式](#xml-schema-af)的自适应表单，请使用与XML模式结构兼容的预填XML。
* 对于使用[JSON模式](#json-schema-based-adaptive-forms)的自适应表单，请使用符合JSON模式的预填JSON。
* 对于使用FDM模式的自适应表单，请使用与FDM模式兼容的预填JSON。
* 对于没有表单模型](#adaptive-form-with-no-form-model)的自适应表单，没有绑定数据。 [每个字段都是未绑定字段，并使用未绑定的XML预填充。

### 示例预填XML结构{#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         . 
         .              
    </data>
  </afUnboundData>
</afData>
```

### 示例预填JSON结构{#sample-prefill-json-structure}

```javascript
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

对于具有相同绑定字段或未绑定字段且其名称相同的绑定字段，在XML标记或JSON对象中指定的数据将填充所有字段。 例如，表单中的两个字段将映射到预填数据中的名称`textbox`。 在运行时期间，如果第一个文本框字段包含“A”，则第二个文本框中会自动填写“A”。 此链接称为自适应表单域的实时链接。

### 使用XFA表单模板{#xfa-based-af}的自适应表单

基于XFA的自适应表单的预填XML和提交的XML的结构如下：

* **预填XML结构**:基于XFA的自适应表单的预填XML必须与XFA表单模板的数据模式兼容。要预填未绑定的字段，请将预填XML结构包含在`/afData/afBoundData`标签中。

* **已提交的XML结构**:当未使用预填充XML时，提交的XML包含包装器标签中绑定字段和未绑定字段 `afData` 的数据。如果使用预填XML，则提交的XML与预填XML的结构相同。 如果用`afData`根标签预填XML开始，则输出XML也具有相同的格式。 如果预填充XML没有`afData/afBoundData`包装器，而是直接从模式根标签（如`employeeData`）中开始，则提交的XML也会使用`employeeData`标签进行开始。

Prefill-Submit-Data-ContentPackage.zip

[获取包](assets/prefill-submit-data-contentpackage.zip)
含预填数据和已提交数据的FileSample

### 基于XML模式的自适应表单  {#xml-schema-af}

基于XML模式的自适应表单预填XML和提交XML的结构如下：

* **预填XML结构**:预填XML必须与关联的XML模式兼容。要预填未绑定字段，请将预填XML结构包含在/afData/afBoundData标签中。
* **已提交的XML结构**:如果未使用预填充XML，则提交的XML包含包装器标签中绑定字段和未绑定字段 `afData` 的数据。如果使用预填XML，则提交的XML与预填XML的结构相同。 如果XML开始预填`afData`根标签，则输出XML的格式相同。 如果预填充XML没有`afData/afBoundData`包装器，而是直接从`employeeData`等模式根标签中开始，则提交的XML也会使用`employeeData`标签进行开始。

```xml
<?xml version="1.0" encoding="utf-8" ?> 
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">
 
    <xs:element name="sample" type="SampleType"/>
         
    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

对于模型为XML模式的字段，数据预填到`afBoundData`标签中，如以下示例XML中所示。 它可用于使用一个或多个未绑定文本字段预填自适应表单。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>建议不要在绑定面板（具有非空`bindRef`的面板，该面板是通过从Sidekick或“数据源”选项卡拖动组件而创建的）中使用未绑定字段。 它可能导致这些未绑定字段的数据丢失。 此外，建议各字段的名称在表单中是唯一的，对于未绑定的字段尤为如此。

#### 没有afData和afBoundData包装器{#an-example-without-afdata-and-afbounddata-wrapper}的示例

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### 基于JSON模式的自适应表单{#json-schema-based-adaptive-forms}

对于基于JSON模式的自适应表单，预填JSON和提交JSON的结构如下所述。 有关详细信息，请参阅[使用JSON模式创建自适应表单](../../forms/using/adaptive-form-json-schema-form-model.md)。

* **预填JSON结构**:预填JSON必须与关联的JSON模式兼容。（可选）如果还要预填未绑定的字段，可将其打包到/afData/afBoundData对象中。
* **已提交的JSON结构**:如果未使用预填JSON，则提交的JSON包含afData包装器标记中绑定字段和未绑定字段的数据。如果使用预填JSON，则提交的JSON的结构与预填JSON的结构相同。 如果使用afData根对象预填JSON开始，则输出JSON的格式相同。 如果预填JSON没有afData/afBoundData包装器，而是直接从模式根对象（如用户）进行开始，则提交的JSON也会与用户对象开始。

```json
{
    "id": "https://some.site.somewhere/entry-schema#",
    "$schema": "https://json-schema.org/draft-04/schema#",
    "type": "object",
    "properties": {
        "address": {
            "type": "object",
            "properties": { 
    "name": {
     "type": "string"
    },
    "age": {
     "type": "integer"
}}}}}
```

对于使用JSON模式模型的字段，数据预填入afBoundData对象，如以下示例JSON中所示。 它可用于使用一个或多个未绑定文本字段预填自适应表单。 以下是包装`afData/afBoundData`的数据示例：

```json
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

下面是一个没有`afData/afBoundData`包装器的示例：

```json
{
 "user": {
  "address": {
   "city": "Noida",
   "country": "India"
}}}
```

>[!NOTE]
>
>建议在绑定面板中使用未绑定字段（通过从Sidekick或“数据源”选项卡拖动组件创建的具有非空bindRef的面板）**，因为它可能导致未绑定字段的数据丢失。**&#x200B;建议在表单中具有唯一的字段名称，尤其是对于未绑定的字段。

### 没有表单模型{#adaptive-form-with-no-form-model}的自适应表单

对于没有表单模型的自适应表单，所有字段的数据位于`<afUnboundData> tag`的`<data>`标记下。

还注意到：

为各个字段提交的用户数据的XML标签使用字段的名称生成。 因此，字段名称必须是唯一的。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## 使用Configuration Manager {#configuring-prefill-service-using-configuration-manager}配置预填服务

要启用预填服务，请在AEM Web控制台配置中指定默认预填服务配置。 使用以下步骤配置预填服务：

>[!NOTE]
>
>“预填服务配置”适用于自适应表单、HTML5表单和HTML5表单集。

1. 使用以下URL打开&#x200B;**[!UICONTROL Adobe Experience Manager Web控制台配置]**:\
   https://&lt;server>:&lt;port>/system/console/configMgr
1. 搜索并打开&#x200B;**[!UICONTROL 默认预填服务配置]**。

   ![预填配置](assets/prefill_config_new.png)

1. 输入&#x200B;**数据文件位置**&#x200B;的数据位置或正则表达式(常规表达式)。 有效数据文件位置的示例包括：

   * file:///C:/Users/public/Document/Prefill/。*
   * https://localhost:8000/somesamplexmlfile.xml

   >[!NOTE]
   >
   >默认情况下，允许通过crx文件预填所有类型的自适应Forms（XSD、XDP、JSON、FDM，且不基于表单模型）。 只允许对JSON和XML文件使用预填。

1. 现在已为表单配置预填服务。

   >[!NOTE]
   >
   >crx协议负责预填数据的安全，因此默认情况下允许使用。 使用通用正则表达式通过其他协议预填充可能会导致漏洞。 在配置中，指定用于保护数据的安全URL配置。

## 可重复面板{#the-curious-case-of-repeatable-panels}的奇特案例

通常，绑定(表单模式)和未绑定字段在同一自适应表单中创作，但以下是一些例外，以防绑定可重复：

* 对于使用XFA表单模板、XSD、JSON模式或FDM模式的自适应表单，不支持未绑定的可重复面板。
* 请勿在绑定的可重复面板中使用未绑定字段。

>[!NOTE]
>
>根据经验法则，如果绑定和未绑定字段与最终用户在未绑定字段中填写的数据交叉，则不要混合这些字段。 如果可能，您应修改模式或XFA表单模板并为未绑定字段添加一个条目，以便它也会被绑定，并且其数据与已提交数据中的其他字段一样可用。

## 支持预填用户数据{#supported-protocols-for-prefilling-user-data}的协议

在配置了有效正则表达式时，可以通过以下协议以预填数据格式预填自适应表单：

### crx://协议{#the-crx-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

指定的节点必须具有名为`jcr:data`的属性并保存数据。

### file://协议  {#the-file-protocol-nbsp}

```http
https://localhost:4502/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

引用的文件必须位于同一台服务器上。

### https://协议{#the-http-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://localhost:8000/somesamplexmlfile.xml
```

### service://协议{#the-service-protocol}

```http
https://localhost:4502/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

* SERVICE_NAME指OSGI预填服务的名称。 请参阅[创建并运行预填服务](../../forms/using/prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service)。
* IDENTIFIER指OSGI预填服务获取预填数据所需的任何元数据。 登录用户的标识符是可以使用的元数据示例。

>[!NOTE]
>
>不支持传递身份验证参数。

### 在slingRequest {#setting-data-attribute-in-slingrequest}中设置数据属性

您还可以在`slingRequest`中设置`data`属性，其中`data`属性是包含XML或JSON的字符串，如以下示例代码（示例为XML）所示：

```javascript
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

您可以编写一个包含所有数据的简单XML或JSON字符串，并在slingRequest中设置它。 您可以在呈示器JSP中为任何组件轻松完成此操作，您要在其中设置slingRequest数据属性的页面中包含这些组件。

例如，您希望页面具有特定类型标题的特定设计的位置。 为此，您可以编写自己的`header.jsp`，并将其包含在页面组件中并设置`data`属性。

另一个好示例是您希望通过Facebook、Twitter或LinkedIn等社交帐户在登录时预填数据的用例。 在这种情况下，您可以在`header.jsp`中包含一个简单的JSP，它从用户帐户中获取数据并设置数据参数。

prefill-page component.zip

[在页](assets/prefill-page-component.zip)
面组件中获取FileSample prefill.jsp

## AEM Forms自定义预填充服务{#aem-forms-custom-prefill-service}

您可以在场景中使用自定义预填服务，在场景中，您经常从预定义的源读取数据。 预填服务从定义的数据源读取数据，并用预填数据文件的内容预填自适应表单的字段。 它还可以帮助您将预填数据与自适应表单永久关联。

### 创建并运行预填服务{#create-and-run-a-prefill-service}

预填服务是OSGi服务，通过OSGi捆绑包进行打包。 您创建OSGi捆绑包，上传它并将其安装到AEM Forms捆绑包。 在开始创建捆绑包之前：

* [下载AEM Forms Client SDK](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)
* 下载样板程序包

* 将数据（预填数据）文件放在crx-repository中。 可以将文件放置在crx-repository的\contents文件夹中的任意位置。

[获取文件](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### 创建预填服务{#create-a-prefill-service}

样板文件包（示例预填充服务包）包含AEM Forms预填充服务的示例实现。 在代码编辑器中打开样板文件包。 例如，在Eclipse中打开样板项目进行编辑。 在代码编辑器中打开样板包后，请执行以下步骤以创建服务。

1. 打开src\main\java\com\adobe\test\Prefill.java文件进行编辑。
1. 在代码中，设置以下值：

   * `nodePath:` 指向crx-repository位置的节点路径变量包含数据（预填）文件的路径。例如，/content/prefilldata.xml
   * `label:` label参数指定服务的显示名称。例如，默认预填服务

1. 保存并关闭`Prefill.java`文件。
1. 将`AEM Forms Client SDK`包添加到样板项目的构建路径中。
1. 编译项目并为包创建.jar。

#### 开始并使用预填服务{#start-and-use-the-prefill-service}

要开始预填服务，请将JAR文件上载到AEM Forms Web Console，然后激活该服务。 现在，在自适应表单编辑器中显示的服务开始。 要将预填服务与自适应表单关联，请执行以下操作：

1. 在Forms编辑器中打开自适应表单，然后打开表单容器的“属性”面板。
1. 在“属性”控制台中，导航到AEM Forms容器>基本>预填服务。
1. 选择默认预填服务，然后单击&#x200B;**[!UICONTROL 保存]**。 服务与表单关联。

## 在客户端{#prefill-at-client}预填充数据

在您预填自适应表单时，AEM Forms服务器会将数据与自适应表单合并，并将填写的表单发送给您。 默认情况下，数据合并操作在服务器上进行。

您可以配置AEM Forms服务器以在客户端而不是服务器上执行数据合并操作。 它显着缩短了预填和渲染自适应表单所需的时间。 默认情况下，该功能处于禁用状态。 您可以从Configuration Manager或命令行中启用它。

* 要从配置管理器中启用或禁用：
   1. 打开AEM Configuration Manager。
   1. 找到并打开自适应表单和交互式通信Web渠道配置
   1. 启用Configuration.af.clientside.datamerge.enabled.name选项
* 要从命令行启用或禁用：
   * 要启用，请运行以下cURL命令：
      `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   * 要禁用，请运行以下cURL命令：
      `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`
   要充分利用客户端上的预填充数据，请更新预填充服务以返回[FileAttachmentMap](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html)和[CustomContext](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html)