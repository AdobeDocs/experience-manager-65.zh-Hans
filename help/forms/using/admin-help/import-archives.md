---
title: 导入和管理存档
seo-title: 导入和管理存档
description: 了解如何导入和管理存档。
seo-description: 了解如何导入和管理存档。
uuid: aa1613dd-6350-49a7-9643-44365e2acdcc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b6f6463a-2ae4-43d2-8d16-cc20a954e50e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 导入和管理存档 {#import-and-manage-archives}

使用存档选项卡可导入和管理在Workbench中创建的LCA。

## 导入存档 {#import-an-archive}

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“应用程序管理”，然后单击存档选项卡。
1. 单击导入。
1. 单击“浏览”以找到要导入的存档，然后单击“预览”。
1. 查看将随存档一起安装的资源和对象列表。 确保与现有资源、对象和服务配置不发生冲突，因为没有可用的撤消功能。

   如果选择导入服务配置，AEM表单将导入LCA中进程使用的所有进程配置文件（端点、安全配置文件和服务配置参数）。

1. 单击导入。
1. 查看导入结果，然后单击跳过配置以完成导入过程，或单击配置以配置存档。

   >[!NOTE]
   >
   >如果单击“跳过配置”，则可以稍后配置存档。

1. 如果单击配置，将显示配置端点页面，您可以在该页面中进行所需的任何更改：

   * 要重命名端点或编辑其说明，请单击该端点。
   * 要添加任务管理器端点，请单击“添加任务管理器”。 有关任务管理器设置的详细信息，请参阅配 [置任务管理器端点](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)。
   * 要添加监视文件夹端点，请单击“添加监视文件夹”。 有关“监视文件夹”设置的详细信息，请参阅“监视 [文件夹端点设置”](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)。
   * 要添加电子邮件端点，请单击“添加电子邮件”。 有关“电子邮件”设置的详细信息，请参阅“电 [子邮件端点设置”](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)。
   * 要添加EJB端点，请单击“添加EJB”，然后指定端点的名称和说明。
   * 要添加SOAP端点，请单击“添加SOAP”，然后指定端点的名称和说明。
   * 要添加远程处理端点，请单击“添加远程处理”。 有关“远程处理”设置的详细信息，请参 [阅“远程处理”端点设置](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)。
   * 要添加REST端点，请单击“添加REST”，然后指定端点的名称和说明。 请注意“添加REST端点”页面上显示的REST调用URL。
   * 要删除端点，请选中该端点旁边的复选框，然后单击“删除”。

1. 单击下一步。
1. 如果LCA中的进程或服务具有配置参数，则会显示“配置参数”页，在该页中，您可以配置服务参数并单击“下一步”。
1. 在“配置安全性配置文件”页面上，进行所需的任何更改：

   * **** 要求调用方进行身份验证：此设置指示是否可以使用凭据调用该服务。

      如果 *显示调用方当前需要进行身份验证* ，则必须对服务调用方进行身份验证，并且必须授权该调用方的用户主体调用该服务；否则，将拒绝调用尝试。 要删除验证需要，请单击“允许未验证的调用者”。

      如果 *不需要调用者进行身份验证* ，则无需对服务的调用者进行身份验证。 由于没有授权检查，服务的调用将始终成功。 要要求身份验证，请单击“要求调用方进行身份验证”。

   * **** 运行方式：指定在调用服务后由服务使用的运行时标识。 要更改此选项，请单击“更改”。 从以下选项中进行选择：

      **** 未指定：使用默认行为。

      **** 调用者：使用与调用服务的用户相同的标识。

      **** 系统：以完全权限运行服务。 这是长期进程的默认设置。

      **** 指定用户：允许您以特定用户身份运行服务。 这是短时间进程的默认设置。 选择此选项后，单击选择用户以显示“选择主体”页，在该页可以搜索和选择用户。

   * 要向安全配置文件添加主体，请单击“添加主体”，然后选择要添加为主体的用户或用户组。 单击“下一步”，然后选择要分配给此主体的权限：

      **** INVOKE_PERM:调用服务上的所有操作

      **** MODIFY_CONFIG_PERM:修改服务的配置

      **** SUPERVISOR_PERM:查看从进程创建的服务的进程实例数据

      **** START_STOP_PERM:启动和停止服务

      **** ADD_REMOVE_ENDPOINTS_PERM:添加、删除和修改服务的端点

      **** CREATE_VERSION_PERM:创建服务的新版本

      **** DELETE_VERSION_PERM:删除服务的某个版本

      **** MODIFY_VERSION_PERM:修改服务版本

      **** READ_PERM:查看服务

      单击完成以将主体添加到安全配置文件。

1. 单击完成以完成配置。

## 配置作为归档文件一部分的AEM表单 {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“应用程序管理”，然后单击存档选项卡。
1. 在“存档管理”页面上，选择要配置的存档文件。
1. 在“查看存档”页面上，选择高亮显示的存档资源。
1. 配置导入的进程存档文件。

## 使用配置向导配置作为归档文件一部分的AEM表单 {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“应用程序管理”，然后单击存档选项卡。
1. 单击要配置的存档文件旁边的配置。
1. 此时将显示“配置端点”页，您可以在该页中进行所需的任何更改：

   * 要重命名端点或编辑其说明，请单击该端点。
   * 要添加任务管理器端点，请单击“添加任务管理器”。 有关任务管理器设置的详细信息，请参阅配 [置任务管理器端点](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)。
   * 要添加监视文件夹端点，请单击“添加监视文件夹”。 有关“监视文件夹”设置的详细信息，请参阅“监视 [文件夹端点设置”](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)。
   * 要添加电子邮件端点，请单击“添加电子邮件”。 有关“电子邮件”设置的详细信息，请参阅“电 [子邮件端点设置”](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)。
   * 要添加EJB端点，请单击“添加EJB”，然后指定端点的名称和说明。
   * 要添加SOAP端点，请单击“添加SOAP”，然后指定端点的名称和说明。
   * 要添加远程处理端点，请单击“添加远程处理”。 有关“远程处理”设置的详细信息，请参 [阅“远程处理”端点设置](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)。
   * 要添加REST端点，请单击“添加REST”，然后指定端点的名称和说明。 请注意“添加REST端点”页面上显示的REST调用URL。
   * 要删除端点，请选中该端点旁边的复选框，然后单击“删除”。

1. 单击下一步。
1. 如果LCA中的进程或服务具有配置参数，则会显示“配置参数”页，在该页中，您可以配置服务参数并单击“下一步”。
1. 在“配置安全性配置文件”页面上，您可以进行所需的任何更改：

   * **** 要求调用方进行身份验证：此设置指示是否可以使用凭据调用该服务。

      如果 *显示调用方当前需要进行身份验证* ，则必须对服务调用方进行身份验证，并且必须授权该调用方的用户主体调用该服务；否则，将拒绝调用尝试。 要删除验证需要，请单击“允许未验证的调用者”。

      如果 *不需要呼叫者进行身份验证* ，则服务的呼叫者可能进行身份验证，也可能不进行身份验证。 由于没有授权检查，服务的调用将始终成功。 要要求身份验证，请单击“要求调用方进行身份验证”。

   * **** 运行方式：指定在调用服务后由服务使用的运行时标识。 要更改此选项，请单击“更改”。 从以下选项中进行选择：

      **** 未指定：使用默认行为。

      **** 调用者：使用与调用服务的用户相同的标识。

      **** 系统：以完全权限运行服务。 这是长期进程的默认设置。

      **** 指定用户：允许您以特定用户身份运行服务。 这是短时间进程的默认设置。 选择此选项后，单击选择用户以显示“选择主体”页，在该页可以搜索和选择用户。

   * 要向安全配置文件添加主体，请单击“添加主体”，然后选择要添加为主体的用户或用户组。 单击“下一步”，然后选择要分配给此主体的权限：

      **** INVOKE_PERM:调用服务上的所有操作

      **** MODIFY_CONFIG_PERM:修改服务的配置

      **** SUPERVISOR_PERM:查看从进程创建的服务的进程实例数据

      **** START_STOP_PERM:启动和停止服务

      **** ADD_REMOVE_ENDPOINTS_PERM:添加、删除和修改服务的端点

      **** CREATE_VERSION_PERM:创建服务的新版本

      **** DELETE_VERSION_PERM:删除服务的某个版本

      **** MODIFY_VERSION_PERM:修改服务版本

      **** READ_PERM:查看服务

      单击完成以将主体添加到安全配置文件。

## 删除存档 {#remove-an-archive}

>[!NOTE]
>
>要删除包含存储在第三方存储库（EMC Documentum Content Server、IBM FileNet Content Manager或IBM Content Manager）中的资产的存档，您还必须使用Workbench从存储库中删除资产文件。

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“存档管理”。
1. 在“存档管理”页面上，选中要删除的存档的复选框，然后单击“删除”。

