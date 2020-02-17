---
title: 控制对受策略保护的文档的访问
seo-title: 控制对受策略保护的文档的访问
description: 了解如何查看、管理和控制对受策略保护的文档的访问。
seo-description: 了解如何查看、管理和控制对受策略保护的文档的访问。
uuid: 2d9f95e9-e4ee-47e2-988e-a191d1d1d264
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f34058c3-384a-4b73-a386-5bc9125acbf8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 控制对受策略保护的文档的访问 {#controlling-access-to-policy-protected-documents}

无论您分发受策略保护的文档的范围有多广，您都可以控制接收人使用这些文档的方式。

使用“文档”页面，您可以执行以下任务：

* 搜索并查看受策略保护的文档的详细信息。 您可以查看有关文档名称、发布者名称、策略名称和应用策略的日期的信息。 如果删除了保护文档的策略，您还可以在策略名称下看到已删除的策略ID。 用户可以查看和管理自己受策略保护的文档。 管理员可以查看和管理所有受策略保护的文档。
* 更改应用于文档的策略的详细信息。 用户可以编辑自己的策略，管理员可以编辑共享策略和个人策略，策略集协调员可以编辑他们具有权限的策略集中的共享策略。 您可以直接从“文档详细信息”页面访问与文档关联的策略。
* 撤销并恢复对受策略保护的文档的访问权。 管理员可以撤销和恢复对任何文档的访问权。 策略集协调员（有权管理文档）可以撤消和恢复对使用共享策略的受策略保护文档从其策略集中的访问权限。 如果用户创建了保护文档的策略，或者策略是允许此功能的共享策略，则用户可以撤销对受策略保护文档的访问权。
* 切换应用于文档的策略。 如果将策略应用到文档的用户创建了策略，或者策略是启用此功能的共享策略，则可以切换该策略。 策略集协调员可以从其策略集切换策略。 管理员可以切换应用于任何文档的策略。

当文档受策略保护并且您撤销访问权限或切换所应用的策略时，这些更改将生效，如下所示：

* 如果文档处于联机状态，则更改将立即应用，除非用户打开了文档。 在这种情况下，用户必须关闭文档，更改才能生效。
* 如果收件人脱机使用文档（例如，在笔记本电脑上），则更改将在收件人下次通过打开任何受策略保护的文档与文档安全同步时生效。

## 查看有关文档的信息 {#view-information-about-a-document}

对于“文档”页面上列出的每个文档，您都可以看到文档名称、发布者名称、策略名称和文档受保护的日期。 如果已删除保护文档的策略，则策略ID将列在“策略名称”下。

您还可以在“文档详细信息”页面上查看有关特定文档的更多详细信息（如下所述）:

>[!NOTE]
>
>必须使用“文档详细信息”页上的“策略名称”链接来访问在Microsoft outlook中为附加到电子邮件的文档收件人自动生成的策略。 这些策略不显示在策略页面上。

**** 文档名称：所选文档的名称。

**** 文档ID:当将策略应用于文档时，文档安全性分配的唯一标识符。 文档安全性使用此编号跟踪文档。

**** 文档状态：文档的状态（例如，活动或已吊销。）

**** 发布者：将策略附加到文档的用户的名称。

**** 策略名称：用于保护文档的策略的名称。 您可以单击该名称以打开策略。 您必须使用此链接访问Acrobat为附加到Outlook电子邮件的文档收件人生成的策略。 这些策略不显示在“策略”页面上。

**** 策略类型：应用于文档的策略类型。

**** 发布日期：对文档应用策略的日期。

**** 相关小版本：如果文档有相关小版本，则此项目也会显示在列表中。 单击链接可查看文档的相关小版本列表。

用户可以查看有关其受保护文档的信息。 管理员可以查看有关任何用户已使用策略保护的文档的信息。 策略集协调员可以查看有关受策略保护的文档的信息（来自其策略集）。

1. 在文档安全页面上，单击“文档”。
1. 在文档列表中，单击相应的文档。 此时将打开“文档详细信息”页面，其中显示有关文档的详细信息。 本页还提供了用于撤销文档访问、切换策略和查看与本文档相关的事件的选项。

## 查看文档的相关小版本 {#view-related-iterations-for-a-document}

如果启用了跟踪相关小版本，则可以跟踪不同用户保存的文档版本。 此功能仅受某些应用程序（如PTC Pro/ENGINEER Wildfire）支持。

当多个用户协作并保存同一文档的不同版本时，此功能非常有用。 文档安全可以跟踪各种迭代；因此，您可以轻松查看不同版本的文档信息。

如果启用了此功能，您可以从“文档”页面查看文档的相关小版本。

1. 查看文档的“文档详细信息”页面。 (请参 [阅查看有关文档的信息](controlling-access-policy-protected-documents.md#view-information-about-a-document)。)
1. 单击“查看相关小版本”(View Related Iterations)。 只有在启用了该功能时，此选项才可用。 此时将显示相关小版本的列表。 对于每个小版本，您可以查看以下信息：

   * **** 小版本：文件名。 它可能与原始文件名不同，并且其末尾附加有版本号。
   * **** 发布者：原始文档的发布者。
   * **** 创建者：保存小版本的用户。
   * **** 创建日期：保存小版本的日期和时间。
   * **** 政策：保护小版本的策略。 不同的迭代可能受不同策略的保护。

1. 要显示该小版本的“文档详细信息”(Document Detail)页，请单击小版本的文件名。

## 撤销和恢复对文档的访问 {#revoking-and-reinstating-access-to-documents}

您可以撤销和恢复对受策略保护的文档的访问权：

**** 用户：可以撤销或恢复对其使用自己的个人策略保护的文档的访问权，或者对于已为应用策略的用户启用了撤销功能的共享策略的访问权。 无法撤销对文档或切换策略的访问权限的用户需要联系管理员。

**** 管理员：可以撤销或恢复对任何受策略保护的文档（包括受个人或共享策略保护的文档）的访问权限。 如果管理员撤销了对使用共享策略保护的文档的访问权限，则只有管理员可以恢复该文档的访问权限。

**** 策略集协调员：可以撤销或恢复策略集保护的文档的访问权限。

当您撤销或恢复文档访问权限时，更改将在以下时间生效：

* 如果文档处于联机状态并关闭状态，则更改将在收件人下次通过打开受策略保护的文档与文档安全同步时生效。
* 如果文档处于联机状态并打开，则更改将在收件人关闭文档时生效。
* 如果文档处于脱机状态（在使用时没有Internet连接，如在笔记本电脑上），则更改将在收件人下次与文档安全性同步时生效。

**撤销对受策略保护的文档的访问权**

1. 在文档安全页面上，单击“文档”。
1. 选中相应文档旁边的复选框，然后单击“撤销”。 您可以一次撤销对多个文档的访问权。
1. 选择要向在文档被撤销后尝试打开文档的用户显示的消息：

   * **** 一般信息：指示作者已吊销文档
   * **** 文档终止：指示作者终止了文档
   * **修订文档**:指示作者修改了文档

1. （可选）如果文档有较新版本，请输入该URL，然后单击“测试”以验证该URL。
1. 单击“确定”，然后再次单击“确定”以返回到“文档”页面。

**恢复文档访问权限**

1. 在文档安全页面上，单击“文档”。
1. 在文档列表中，单击相应的文档。
1. 单击“取消撤销”，然后单击“确定”。

## 切换应用于文档的策略 {#switch-a-policy-that-is-applied-to-a-document}

用户、策略集协调员和管理员可以切换应用于受策略保护的文档的策略（一次只能对文档应用一个策略）。 如果用户创建了策略或策略是启用了此功能的共享策略，则用户可以切换应用于其自己受策略保护的文档的策略。 否则，管理员或策略集协调员必须切换策略。 管理员可以切换任何用户受策略保护的文档的策略。 策略集协调员可以从其策略集切换策略。

切换策略时，新策略将按如下方式实施：

* 如果文档处于联机状态并关闭状态，则更改将在收件人下次通过联机打开任何受策略保护的文档与文档安全同步时生效。
* 如果文档处于联机状态并打开，则更改将在用户关闭文档时生效。
* 如果文档处于脱机状态（在使用中没有活动的因特网或网络连接，例如在笔记本电脑上），则当用户下次通过联机打开受策略保护的文档与文档安全同步时，将应用更改。

>[!NOTE]
>
>要允许匿名访问当前没有此访问权限的受策略保护的文档，请删除客户端应用程序中的现有策略，然后应用允许匿名访问的策略。 如果切换策略，用户仍必须登录才能访问文档。

1. 在文档安全页面上，单击“文档”。
1. 在文档列表中，单击相应的文档。
1. 单击“切换策略”。 将显示最多100个策略的列表。
1. 如果未显示所需的策略，请从“查找”列表中选择策略名称或策略ID，键入名称或ID，然后单击“查找”。
1. 单击列表中的新策略。
1. 单击“切换策略”，然后单击“确定”返回到“文档”页面。

## 搜索文档 {#search-for-a-document}

您可以使用列表中可用的日期范围标准和搜索条件的组合，在“文档”页面上搜索文档。 这些条件包括文档名称、策略名称或所有文档。

某些其他搜索选项仅对管理员可用：

**** 文档ID:应用策略时，文档安全性为文档分配的唯一ID编号。

**** 文档名称：文档的名称。

**** 发布者名称：将策略附加到文档的用户的名称。 您可以从所有域或指定的域中选择用户。

**** 策略ID:附加到文档的策略的ID编号。

**** 策略名称：附加到文档的策略的名称。

**** 所有文档：所有受管理员和用户保护的文档。 使用“所有文档”选项搜索可能会返回一长串文档。

1. 在文档安全页面上，单击“文档”。
1. 在“查找”列表中，选择所需的搜索条件。

   可以将条件指定为文档ID、文档名称、发布者名称、策略ID、策略名称或所有文档。

   如果指定发布者名称，请单击“通讯簿”图标并指定要搜索用户的域，然后单击“确定”返回到“文档”搜索页面。

1. （可选）在“日期”列表中，选择日期范围选项。 如果选择“自定义日期”，请在出现的框中键入日期的yyyy/mm/dd格式，或使用日期选取器指定日期范围：

   * 单击日历以打开日期选取器。
   * 使用箭头查找年份和月份。
   * 单击日历上月的某天。
   * 单击确定以关闭日期选取器。

1. 单击“查找”。

## 对文档列表排序 {#sort-the-document-list}

可以按列标题对文档列表进行排序。 列标题旁边的三角形图标指示当前用于排序的列。 向上指向的三角形表示升序，而向下指向的三角形表示降序。

1. 在文档安全页面上，单击“文档”。
1. 单击相应的列标题。
1. 要更改排序顺序，请再次单击列。

## 向受策略保护的文档添加封面 {#add-cover-page-to-policy-protected-documents}

对于大多数非Adobe PDF查看器，如果打开文档安全保护文档，则第一页将显示为空白页面，或应用程序在不打开文档的情况下中止。

您可以使用页面0（包装器文档）支持允许非Adobe PDF查看器打开受保护的文档并显示文档中的封面。

>[!NOTE]
>
>在Adobe Reader/Acrobat或Mobile Reader中查看此类文档（包含第0页）时，默认情况下会打开受保护的文档。

**向受策略保护的文档添加封面**

在工作台中使用以下进程：

**** 使用封面保护文档：使用指定的策略保护PDF文档，并向文档添加封面

**** 提取受保护的文档：从包含封面的PDF文档中提取受策略保护的PDF文档

使用以下文档安全API:

****`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` protectDocumentWithCoverPage:使用指定的策略保护给定的PDF，并返回包含封面的文档和作为附件&#x200B;**extractProtectedDocument的受保护文**&#x200B;档：提取受保护的文档，该文档是包含封面的文档中的一个附件。 可以使用protectDocumentWithCoverPage方法创建包含封面的文档`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`