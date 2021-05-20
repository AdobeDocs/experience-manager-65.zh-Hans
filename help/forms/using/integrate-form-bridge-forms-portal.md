---
title: 将表单桥与HTML5表单的自定义门户集成
seo-title: 将表单桥与HTML5表单的自定义门户集成
description: 您可以使用FormBridge API从HTML页面获取或设置表单字段的值并提交表单。
seo-description: 您可以使用FormBridge API从HTML页面获取或设置表单字段的值并提交表单。
uuid: c8911f82-1a25-47a5-9a06-19b5dce74a2c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bd9bf095-d74d-458c-afe7-fab04050849d
docset: aem65
feature: 移动设备表单
exl-id: 89118bb8-6ec8-4048-b3d6-5c73a9eea33e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# 将表单桥与HTML5表单的自定义门户集成{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge是一个HTML5表单桥API，允许您与表单进行交互。 有关FormBridge API引用，请参阅[FormBridge API引用](/help/forms/using/form-bridge-apis.md)。

您可以使用FormBridge API从HTML页面获取或设置表单字段的值并提交表单。 例如，您可以使用API来构建类似于向导的体验。

现有的HTML应用程序可以利用FormBridge API与表单进行交互，并将其嵌入到HTML页面中。 您可以使用以下步骤来使用表单桥API设置字段的值。

## 将HTML5表单集成到网页{#integrating-html-forms-to-a-web-page}

1. **选择用户档案或创建用户档案**

   1. 在CRX DE界面中，导航到：`https://'[server]:[port]'/crx/de`。
   1. 使用管理员凭据登录。
   1. 创建用户档案或选择现有用户档案。

      有关如何创建配置文件的详细信息，请参阅[创建新配置文件](/help/forms/using/custom-profile.md)。

1. **修改HTML配置文件**

   在配置文件渲染器中包含XFA运行时、XFA区域设置库和XFA表单HTML代码片段，设计网页，并将表单放入网页内。

   例如，使用以下代码片段创建一个包含两个输入字段和一个表单的应用程序，以演示表单与外部应用程序之间的交互。

   ```xml
   <%@ page session="false"
                  contentType="text/html; charset=utf-8"%><%
   %><%@ taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
   %><!DOCTYPE html>
   <html manifest="${param.offlineSpec}">
       <head>
          <cq:include script="formRuntime.jsp"/>
           <!-- Portal Scripts and Styles -->
          <cq:include script="portalheader.jsp"/>
       </head>
       <body>
           <div id="leftdiv" >
               <div id="leftdivcontentarea">
                   <!-- Portal Body -->
                 <cq:include script="portalbody.jsp"/>
               </div>
           </div>
           <div id="rightdiv">
               <div id="formBody">
               <cq:include script="config.jsp"/>
               <!-- Form body -->
               <cq:include script="formBody.jsp"/>
               <!  --To assist in page transitions -- add navigation, based on scrolling -->
               <cq:include  script="../nav/scroll/nav_footer.jsp"/>
               <cq:include script="footer.jsp"/>
               </div>
           </div>
       </body>
   </html>
   ```

   >[!NOTE]
   >
   >**行9**&#x200B;包含用于CSS样式和JavaScript文件的其他JSP引用，以设计页面。
   >
   >
   >**行18**&#x200B;上的&lt;div id=&quot;rightdiv&quot;>标记包含XFA表单的HTML代码段。
   页面的样式设置为两个容器：**left**&#x200B;和&#x200B;**right**。 正确的容器具有表单。 左侧容器有两个输入字段和外部HTML页面的一部分。
   以下屏幕快照显示了表单在浏览器中的显示方式。

   ![门户](assets/portal.jpg)

   左侧是&#x200B;**HTML页面**&#x200B;的一部分。 包含字段的右侧是&#x200B;**xfa窗体**。

1. **访问页面中的表单字段**

   下面是一个示例脚本，您可以添加该脚本以在表单字段中设置值。

   例如，如果要使用字段&#x200B;**名字**&#x200B;和&#x200B;**姓氏**&#x200B;中的值设置&#x200B;**EmployeeName**，请调用&#x200B;**window.formBridge.setFieldValue**&#x200B;函数。

   同样，您也可以通过调用&#x200B;**window.formBridge.getFieldValue** API来读取值。

   ```javascript
   $(function() {
               $(".input").blur(function() {
                   window.formBridge.setFieldValue(
                               'xfa.form.form1.#subform[0].EmployeeName',
                                $("#lname").val()+' '+$("#fname").val()
                              )
                   });
           });
   ```
