---
title: 信件和互动式通信的后处理
description: 通信管理中的信件后处理允许您创建AEM和Forms后处理过程（如打印和电子邮件），并将它们与您的信件集成。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 91ee4422-99c1-4907-a507-5968c6984f28
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# 信件和互动式通信的后处理{#post-processing-of-letters-and-interactive-communications}

## 后处理 {#post-processing}

代理可以关联并执行信件和交互式通信的后处理工作流。 可以在信件模板的“属性”视图中选择要执行的后处理。 您可以将后处理设置为电子邮件、打印、传真或存档最终信件。

![后处理](assets/ppoverview.png)

要将帖子流程与信件或交互式通信关联，您首先需要设置帖子流程。 可以对提交的信件执行两种类型的工作流：

1. **Forms Workflow：** 这些是AEM Forms on JEE流程管理工作流。 设置说明 [Forms Workflow](#formsworkflow).

1. **AEM工作流：** AEM工作流还可用作已提交信件的发布流程。 设置说明 [AEM Workflow](../../forms/using/aem-forms-workflow.md).

## 表单工作流 {#formsworkflow}

1. 在AEM中，使用以下URL打开服务器的Adobe Experience Manager Web控制台配置： `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![配置管理器](assets/2configmanager-1.png)

1. 在此页面中，找到AEM Forms客户端SDK配置，然后单击该配置以展开它。
1. 在服务器URL中，输入JEE服务器上AEM Forms的名称和登录详细信息，然后单击 **保存**.

   ![输入LiveCycle服务器的名称](assets/1cofigmanager.png)

1. 指定用户名和密码。
1. 确保已将sun.util.calendar添加到反序列化防火墙配置中。

   列入允许列表转到“反序列化防火墙配置”，在“包前缀的类”下，添加sun.util.calendar。

1. 现在，您的服务器已映射，并且在创建信件时，可在AEM用户界面中使用AEM Forms on JEE中的发布流程。

   ![创建已列出后处理的信件屏幕](assets/0configmanager.png)

1. 要验证进程/服务，请复制进程名称并返回到Adobe Experience Manager Web控制台配置页面> AEM Forms客户端SDK配置，然后将进程添加为新服务。

   例如，如果Letter的“属性”页中的下拉列表将进程名称显示为Forms Workflow-> ValidCCPostProcess/SaveXML，则添加服务名称为 `ValidCCPostProcess/SaveXML`.

1. 要使用AEM Forms on JEE工作流进行后期处理，请设置必要的参数和输出。 参数的默认值如下所示。

   转到Adobe Experience Manager Web控制台配置页面> **[!UICONTROL 通信管理配置]** 并设置以下参数：

   1. **inPDFDoc(文档参数PDF)：** 作为输入的PDF文档。 此输入包含渲染的字母作为输入。 指示的参数名称是可配置的。 可以从配置的通信管理配置中配置它们。
   1. **inXMLDoc（XML数据参数）：** XML文档作为输入。 此输入包含用户以XML形式输入的数据。
   1. **inXDPDoc（XDP文档参数）：** XML文档作为输入。 此输入包含基础布局(XDP)。
   1. **inAttachmentDocs（“附件文档”参数）：** 列表输入参数。 此输入包含作为输入的所有附件。
   1. **redirectURL（重定向URL输出）：** 指示要重定向到的url的输出类型。

   您的表单工作流必须具有PDF的文档参数或XML数据参数作为输入，且名称与中指定的名称相同 **[!UICONTROL 通信管理配置]**. 要使流程在后处理下拉列表中列出，需要此字段。

## 发布实例上的设置 {#settings-on-the-publish-instance}

1. 登录 `https://localhost:publishport/aem/forms`.
1. 导航到 **[!UICONTROL 字母]** 查看发布实例上可用的已发布书信。
1. 配置AEM DS设置。 请参阅 [配置AEM DS设置](../../forms/using/configuring-the-processing-server-url.md).

>[!NOTE]
>
>使用Forms或AEM工作流时，在从发布服务器进行任何提交之前，必须配置DS设置服务。 否则，表格提交将失败。

## 书信实例检索 {#letter-instances-retrieval}

通过使用LetterInstanceService中定义的以下API，可以进一步处理保存的信件实例，例如检索信件实例和删除信件实例。

<table>
 <tbody>
  <tr>
   <td><strong>服务器端API</strong></td>
   <td><strong>操作名称</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><p>公共LetterInstanceVO</p> <p>getLetterInstance(String letterInstanceId)</p> <p>引发ICCException； </p> </td>
   <td>getLetterInstance</td>
   <td>获取指定的书信实例 </td>
  </tr>
  <tr>
   <td>公共void deleteLetterInstance(String letterInstanceId)引发ICCException； </td>
   <td>deleteLetterInstance </td>
   <td>已删除指定的书信实例 </td>
  </tr>
  <tr>
   <td>List getAllLetterInstances(Query)引发ICCException； </td>
   <td>getAllLetterInstances </td>
   <td>此API根据输入查询参数获取书信实例。 要获取所有信件实例，可将查询参数作为null传递。<br /> </td>
  </tr>
  <tr>
   <td>公共布尔值letterInstanceExists（字符串letterInstanceName）引发ICCException； </td>
   <td>letterInstanceExist </td>
   <td>检查给定名称是否存在书信实例 </td>
  </tr>
 </tbody>
</table>

## 将后处理与信件关联 {#associating-a-post-process-with-a-letter}

在CCR用户界面中，完成以下步骤以将后处理与信件相关联：

1. 将鼠标悬停在信件上并选择 **查看属性**.
1. 选择&#x200B;**编辑**。
1. 在基本属性中，使用后处理下拉列表，选择要与信件关联的后处理。 下拉列表中列出了AEM和Forms相关的发布流程。
1. 选择&#x200B;**保存**。
1. 使用后处理配置书信后，发布书信，并（可选）在发布实例上指定AEM DS设置服务中的处理URL。 这样可以确保在处理实例上运行后处理。

## 重新加载草稿书信实例  {#reloaddraft}

可以使用以下URL在用户界面中重新加载草稿信件实例：

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstanceID：已提交书信实例的唯一ID。

有关保存草稿信件的更多信息，请参阅 [保存草稿和提交信件实例](../../forms/using/create-correspondence.md#savingdrafts).
