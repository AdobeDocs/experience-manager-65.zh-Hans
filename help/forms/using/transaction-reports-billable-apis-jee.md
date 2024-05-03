---
title: 交易报告AEM Forms on JEE的可计费API。
description: 作为AEM Forms on JEE的交易入账的所有API的列表。
topic-tags: forms-manager
feature: Transaction Reports
exl-id: dbb22369-c0a2-4cf6-b01b-096b4de13a14
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 3%

---

# 适用于AEM Forms on JEE的Transaction Reporting Billable API {#transaction-reports-billable-apis}

JEE上的AEM Forms提供了多个API来提交、处理和渲染文档。 某些API作为交易入账，而其他API则作为自由使用。 本文档提供作为交易入账的所有API的列表。 以下是一些使用计费API的常见方案：

* 将文档从一种格式转换为另一种格式
* 拼合动态PDF文档
* 将交互式PDF文档与另一个PDF文档合并

计费API不考虑页数、文档或表单的长度或渲染文档的最终格式。
<!--

* **Forms Submitted:** When data is submitted from any type of form created with AEM Forms and the data is submitted to any data storage repository or database is considered form submission. For example, submitting an HTML5 Form, PDF Forms are accounted as forms submitted. Each form in a form set is considered a submission. For example, if a form set has 5 forms, when the form set is submitted, transaction reporting service counts it as 5 submissions.

* **Documents Rendered:** Generating a document by combining a template and data, digitally signing or certifying a document, using a billable document services API for document services, or converting a document from one format to another are accounted as documents rendered.

-->

以下是JEE可计费API列表。 查找列表 [在OSGi上为AEM Forms设置可记帐API](/help/forms/using/transaction-reports-billable-apis.md).

## 可记帐文档服务API {#billable-document-services-apis}

### 生成PDF服务 {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
  </tr>
   <tr>
   <td><a>CreatePDF</a></td>
   <td>按照支持的文件类型创建Adobe PDF。</td>
   <td>转化<br /> </td>
  </tr>
  <tr>
   <td><a>CreatePDF3</a></td>
   <td>按照支持的文件类型创建Adobe PDF。 </td>
   <td>转化<br /> </td>
  </tr>
  <tr>
   <td><a> HtmlToPDF</a></td>
   <td>将HTML文件转换为Adobe PDF。 </td>
   <td>转化<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF</a></td>
   <td>将PDF导出到支持的文件类型。 </td>
   <td>转化<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF2</a></td>
   <td><p>将PDF导出到支持的文件类型。</p> </td>
   <td>转化<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF3</a></td>
   <td>将PDF导出到支持的文件类型。</td>
   <td>转化<br /> </td>
  </tr>
  <tr>
   <td><a>HtmlFileToPDF</a></td>
   <td>将HTML文件转换为PDF。</td>
   <td>转化<br /> </td>
  </tr>
  <tr>
   <td><a>HtmlToPDF2</a></td>
   <td>将HTML文件转换为PDF。</td>
   <td>转化<br /> </td>
  </tr>
  <tr>
   <td><a>优化PDF</a></td>
   <td>优化PDF以通过去除不必要的元数据而减小文件大小，同时不影响质量。</td>
   <td>转化<br /> </td>
  </tr>
 </tbody>
</table>

### DocAssurance服务 {#DocAssurance-Service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
  </tr>
  <tr>
   <td><a>签名/认证</a><br /> </td>
   <td>此API使您能够保护文档。 您可以使用该API来签名和认证PDF文档。</td>
   <td>转化</td>
  </tr>
 </tbody>
</table>


### Distiller服务 {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
  </tr>
  <tr>
  <tr>
   <td><a>CreatePDF</a></td>
   <td>从支持的文件类型创建Adobe PDF。</td>
   <td>转化</td>
  </tr>
  <tr>
   <td><a>CreatePDF2</a></td>
   <td>从支持的文件类型创建Adobe PDF。</td>
   <td>转化</td>
  </tr>
 </tbody>
</table>

<!--

### Document of Record Service (DoR Service) {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">render</a></td>
   <td>Invokes the specified render method to generate a document of record using provided parameters.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### 输出服务 {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
  </tr>
  <tr>
   <td><a>generateoutput</a></td>
   <td>合并数据和模板以创建PDF文档。</td>
   <td>已渲染的文档</td>
  </tr>
  <tr>
   <td><a>generatePDFOutput</a></td>
   <td>合并数据和模板以创建PDF文档。</td>
   <td>已渲染的文档</td>
  </tr>
  <tr>
   <td><a>generatePDFOutput2</a></td>
   <td>合并数据和模板以创建PDF文档。</td>
   <td>已渲染的文档</td>
  </tr>
  <tr>
   <td><a>generatePrintedOutput</a></td>
   <td>将XDP和PDF文档转换为PostScript (PS)、Printer Command Language (PCL)和ZPL文件格式。 </td>
   <td>已渲染的文档</td>
  </tr>
  <tr>
   <td><a>generatePrintedOutput2</a></td>
   <td>将XDP和PDF文档转换为PostScript (PS)、Printer Command Language (PCL)和ZPL文件格式。 </td>
   <td>已渲染的文档</td>
  </tr>
  <tr>
   <td><a>transformPDF</a></td>
   <td>将一组XDP和PDF文档转换为一组PostScript (PS)、打印机命令语言(PCL)和ZPL文件格式。 </td>
   <td>文档转换</td>
  </tr>
 </tbody>
</table>

<!-- ### Forms Service {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Renders PDF Form from XDP templates. The XDP templates are created in Forms Designer.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extracts data from a PDF Form or XDP templates</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### 转换PDF服务 {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
  </tr>
  <tr>
   <td><a>toImage2</a></td>
   <td>将PDF文档转换为图像文档的列表。 支持的图像格式为JPEG、JPEG2K、PNG和TIFF。</td>
   <td>文档转换</td>
  </tr>
  <tr>
   <td><a>toPS2</a></td>
   <td>使用选项规范中指定的选项将FlatPDF文件转换为PostScript格式。</td>
   <td>文档转换</td>
  </tr>
  <tr>
   <td><a>toSWF</a></td>
   <td>使用选项规范中指定的选项将平面PDF文件转换为SWF格式。</td>
   <td>文档转换</td>
  </tr>
 </tbody>
</table>

### 条形码Forms服务 {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
  </tr>
  <tr>
   <td><a>解码</a></td>
   <td>解码Document对象中的所有条形码，并返回包含从条形码检索的数据的org.w3c.dom.Document对象。</td>
   <td>文档转换</td>
  </tr>
 </tbody>
</table>

### 汇编程序服务 {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
  </tr>
  <tr>
   <td><a>调用</a></td>
   <td>执行指定的DDX文档并返回包含结果文档的AssemblerResult对象。 </td>
   <td>文档转换</td>
  </tr>
  <tr>
   <td><a>invokeDDX</a></td>
   <td>执行指定的DDX文档并返回包含结果文档的AssemblerResult对象。 </td>
   <td>文档转换</td>
  </tr>
  <tr>
   <td><a>invokeOneDocument</a></td>
   <td>使用指定的选项将指定的文档转换为PDF/A。</td>
   <td>文档转换</td>
  </tr>
  <tr>
   <td><a>invokeDDXOneDocument</a></td>
   <td>使用指定的选项将指定的文档转换为PDF/A。</td>
   <td>文档转换</td>
  </tr>
  <tr>
   <td><a>toPDFA</a></td>
   <td>使用指定的选项将指定的文档转换为PDF/A。</td>
   <td>文档转换</td>
  </tr>
 </tbody>
</table>

当您执行以下一个或多个操作时，调用API的使用情况计为事务：
1. 从非PDF格式转换为PDF格式。 例如，从XDP格式到PDF格式的转换。<!-- catering to both interactive and non-interactive forms of communication, and the conversion from Word to PDF.-->
1. 从PDF格式转换为PDF/A格式。
1. 从PDF格式转换为非PDF格式。 示例包括从PDF到图像的转换或从PDF到文本的转换。

>[!NOTE]
>
>* 汇编器服务的调用API可以在内部调用另一个服务的可计费API，具体取决于输入。 所以， `invoke API` 可计为无、单个或多个交易。 计算的事务数取决于输入和调用的内部API。
>* 使用汇编程序服务生成的单个PDF文档 `invoke` 和 `invokeDDX`，可计为无、单个或多个交易。 计算事务处理的数量取决于提供的 <!--DDX--> 代码。

<!--
### PDF Utility Service  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a>convertPDFtoXDP</a></td>
   <td>Converts a PDF document into an XDP file. For a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the AcroForm dictionary.</td>
   <td>Documents Conversion</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

## 计费数据捕获API {#billable-data-capture-apis}

<!--All the submission events of Forms, HTML5 Forms, and form set are accounted as transactions. By default, submission of a PDF Form is not accounted as a transaction. Use the provided [transaction recorder API](record-transaction-custom-implementation.md) to record a PDF Forms submission as a transaction.-->

<!--
### Adaptive Forms {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an adaptive form</td>
   <td>Submits an adaptive form to configured submit action. </td>
   <td>Forms Submitted</td>
   <td>
    <ul>
     <li>Successful submissions account for single or two transactions. The number of transactions counted depends upon the type of submit action used for submission. For example, sending PDF through email submit action accounts for two counts of transactions. One transaction for form submission and another for PDF generated using the Document of Record (DOR) service. </li>
     <li>Using the adaptive form within an adaptive form (Adaptive form formset) accounts only single transaction. You can have any number of adaptive forms within an adaptive form.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

-->

<!--### HTML5 Forms {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an HTML5 Form</td>
   <td>Submits an HTML5 Form to submit URL configured in the form.</td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### Forms {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>描述</td>
   <td>交易报告类别</td>
  </tr>
  <tr>
   <td>exportData</td>
   <td>提交表单。</td>
   <td>已提交的表单</td>
  </tr>
  <tr>
   <td>exportData2</td>
   <td>提交表单。</td>
   <td>已提交的表单</td>
  </tr>
  <tr>
   <td>renderForm</td>
   <td>提交表单。</td>
   <td>Forms已呈现</td>
  </tr>
  <tr>
   <td>renderHTMLForm</td>
   <td>提交表单。</td>
   <td>Forms已呈现</td>
  </tr>
  <tr>
   <td>renderHTMLForm2</td>
   <td>提交表单。</td>
   <td>Forms已呈现</td>
  </tr>
  <tr>
   <td>renderPDFForm</td>
   <td>提交表单。</td>
   <td>Forms已呈现</td>
  </tr>
  <tr>
   <td>renderPDFForm2</td>
   <td>提交表单。</td>
   <td>Forms已呈现</td>
  </tr>
  <tr>
   <td>renderPDFFormWithUsageRights</td>
   <td>提交表单。</td>
   <td>Forms已呈现</td>
  </tr>
 </tbody>
</table>

<!-- ## Billable Interactive Communication and Form-centric AEM Workflows on OSGi APIs {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

Assign task and document services steps of Form-centric AEM Workflows on OSGi and all the renditions of interactive communication and are accounted as transactions. Previewing an interactive communication on the author instance and previewing on the publish instance using Agent UI are not accounted as transactions. If a workflow step accounts a transaction and the workflow fails to complete, the transaction count is not reversed.

<!--

### Interactive Communication - Web Channel {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Rendering a web channel</td>
   <td>Opens the web version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Interactive Communication - Print Channel {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> (convert to PDF)</td>
   <td>Generates the PDF version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

-->


<!--
### Form-centric AEM Workflows on OSGi  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>Use case</p> </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an Assign Task step</td>
   <td>Forms Submitted</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Submitting a workflow application startpoint </td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
  <tr>
   <td>Submitting an interactive communication (Print Channel) from the Agent UI to a workflow</td>
   <td>Documents Rendered</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->


<!--

WILL ADD THIS ONE - 

## Recording billable APIs as transactions for custom code {#recording-billable-apis-as-transactions-for-custom-code}

Actions like submitting a PDF Form, using Agent UI to preview an interactive communication, using non-standard form submission, and custom implementations are not accounted as transactions. AEM Forms provides an API to record such actions as transactions. You can call the API from your custom implementations to [record a transaction](/help/forms/using/record-transaction-custom-implementation.md).

## Related Articles {#related-articles}

* [Transaction Reports Overview](../../forms/using/transaction-reports-overview.md)
* [Viewing and Understanding a Transaction Reports](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Record a transaction for custom implementations](/help/forms/using/record-transaction-custom-implementation.md)

-->

## 相关文章

* [在JEE上启用和查看AEM Forms的交易报告](/help/forms/using/transaction-report-overview-jee.md)
* [为JEE上的AEM Forms的自定义组件API记录事务](/help/forms/using/record-transaction-custom-component-jee.md)
