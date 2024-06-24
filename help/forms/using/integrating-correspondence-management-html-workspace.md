---
title: 在AEM Forms工作区中集成第三方应用程序
description: 在AEM Forms工作区中集成第三方应用程序，例如通信管理。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 39a3f7db-549f-47f3-8d4f-42d583a4532d
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# 在AEM Forms工作区中集成第三方应用程序{#integrating-third-party-applications-in-aem-forms-workspace}

AEM Forms工作区支持管理表单和文档的任务分配和完成活动。 这些表单和文档可以是以XDP、PDF、HTML或Flex格式呈现的XDP Forms、Flex®表单或指南（已弃用）。

这些功能得到了进一步增强。 AEM Forms现在支持与第三方应用程序协作，这些应用程序支持类似于AEM Forms工作区的功能。 此功能的共同部分是任务分配和后续审批的工作流。 AEM Forms为AEM Forms企业用户提供单一的统一体验，因此可通过AEM Forms工作区处理所支持应用程序的所有此类任务分配或批准。

例如，让我们将通信管理视为与AEM Forms工作区集成的示例候选项。 通信管理具有“信件”的概念，可以渲染信件并允许执行操作。

## 创建相应的管理资源 {#create-correspondence-management-assets}

首先，创建一个在AEM Forms工作区中呈现的示例通信管理模板。 有关更多详细信息，请参阅 [创建书信模板](../../forms/using/create-letter.md).

访问其URL处的通信管理模板，以验证是否可以成功呈现通信管理模板。 URL的模式与 `https://'[server]:[port]'/lc/content/cm/createcorrespondence.html?cmLetterId=encodedLetterId&cmUseTestData=1&cmPreview=0;`

位置 `encodedLetterId` 是URL编码的字母ID。 在Workbench中为工作区任务定义渲染进程时，请指定相同的书信ID。

## 创建任务以在AEM Workspace中呈现和提交书信 {#create-a-task-to-render-and-submit-a-letter-in-aem-workspace}

在执行这些步骤之前，请确保您是以下组的成员：

* cm-agent-users
* 工作区用户

有关更多信息，请参阅 [添加和配置用户](/help/forms/using/admin-help/adding-configuring-users.md).

使用以下步骤可创建任务以在AEM Workspace中呈现和提交书信：

1. 启动Workbench 以管理员身份登录到localhost。
1. 单击“文件”>“新建”>“应用程序”。 在应用程序名称字段中，输入 `CMDemoSample` 然后单击“Finish（完成）”。
1. 选择 `CMDemoSample/1.0` 并右键单击 `NewProcess`. 在名称字段中，输入 `CMRenderer` 然后单击“Finish（完成）”。
1. 拖动起点活动选取器并对其进行配置：

   1. 在演示文稿数据中，选择使用CRX资源。

      ![useacrxasset](assets/useacrxasset.png)

   1. 浏览资产。 在选择表单资产对话框中，字母选项卡列出服务器上的所有字母。

      ![书信选项卡](assets/letter_tab_new.png)

   1. 选择相应的书信并单击 **确定**.

1. 单击管理操作配置文件。 此时将显示“管理操作配置文件”对话框。 确保正确选择呈现进程和提交进程。
1. 要打开带有数据XML文件的信件，请在“准备数据流程”中浏览并选择适当的数据文件。
1. 单击“确定”。
1. 定义起点输出和任务附件的变量。 定义的变量包含“起始点输出”和“任务附件”数据。
1. （可选）要在工作流中添加其他用户，请拖动活动选取器并对其进行配置，然后将其分配给用户。 编写自定义包装器（下面给出一个示例）或下载并安装DSC（下面给出一个示例）以提取信件模板、起点输出和任务附件。

   下面列出了一个自定义包装器示例：

   ```javascript
   public LetterInstanceInfo getLetterInstanceInfo(Document dataXML) throws Exception {
   try {
   if(dataXML == null)
   throw new Exception("dataXML is missing");
   
   CoreService coreService = getRemoteCoreService();
   if (coreService == null)
   throw new Exception("Unable to retrive service. Please verify connection details.");
   Map<String, Object> result = coreService.getLetterInstanceInfo(IOUtils.toString(dataXML.getInputStream(), "UTF-8"));
   LetterInstanceInfo letterInstanceInfo = new LetterInstanceInfo();
   
   List<Document> attachmentDocs = new ArrayList<Document>();
   List<byte[]> attachments = (List<byte[]>)result.get(CoreService.ATTACHMENT_KEY);
   if (attachments != null){
   for (byte[] attachment : attachments)
   { attachmentDocs.add(new Document(attachment)); }
   
   }
   letterInstanceInfo.setLetterAttachments(attachmentDocs);
   
   byte[] updateLayout = (byte[])result.get(CoreService.LAYOUT_TEMPLATE_KEY);
   if (updateLayout != null)
   { letterInstanceInfo.setLetterTemplate(new Document(updateLayout)); }
   
   else
   { throw new Exception("template bytes missing while getting Letter instance Info."); }
   
   return letterInstanceInfo;
   } catch (Exception e)
   { throw new Exception(e); }
   
   }
   ```

   [获取文件](assets/dscsample.zip)
下载DSC：上面附加的DSCSample.zip文件中提供了示例DSC。 下载并解压缩DSCSample.zip文件。 在使用DSC服务之前，必须对其进行配置。 请参阅 [配置DSC服务](../../forms/using/add-action-button-in-create-correspondence-ui.md#p-configure-the-dsc-service-p).

   在“定义活动”对话框中，选择相应的活动（如getLetterInstanceInfo），然后单击 **确定**.

1. 部署应用程序。 如果出现提示，请签入并保存资产。
1. 登录AEM表单工作区，网址为https://&#39;[服务器]：[端口]&#39;/lc/content/ws.
1. 打开您已添加的任务CMRenderer。 此时将出现“通信管理”信件。

   ![cminworkspace](assets/cminworkspace.png)

1. 填写所需数据并提交信件。 窗口关闭。 在此流程中，任务被分配到步骤9的工作流中指定的用户。

   >[!NOTE]
   >
   >在填写信件中的所有必需变量之前，不会启用提交按钮。
