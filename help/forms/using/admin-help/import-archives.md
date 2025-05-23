---
title: 导入和管理存档
description: 了解如何导入和管理存档。 存档导入并管理在Workbench中创建的LCA。 您可以导入、配置、使用和删除存档。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0c15677a-ee17-425e-a261-fb3ae8688eb2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '1450'
ht-degree: 0%

---

# 导入和管理存档 {#import-and-manage-archives}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

使用“存档”选项卡导入和管理在Workbench中创建的LCA。

## 导入存档 {#import-an-archive}

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“应用程序管理”，然后单击“存档”选项卡。
1. 单击“导入”。
1. 单击“浏览”找到要导入的存档，然后单击“预览”。
1. 查看将随归档文件一起安装的资源和对象的列表。 由于没有可用的撤消功能，请确保与现有资源、对象和服务配置没有冲突。

   如果选择导入服务配置，则AEM Forms将导入LCA中进程使用的所有进程配置文件（端点、安全配置文件和服务配置参数）。

1. 单击“导入”。
1. 查看导入结果，然后单击跳过配置以完成导入过程，或单击配置配置归档文件。

   >[!NOTE]
   >
   >如果单击“跳过配置”，可以稍后配置归档文件。

1. 如果单击“配置”，将显示“配置端点”页，您可以在其中进行所需的任何更改：

   * 要重命名端点或编辑其说明，请单击它。
   * 要添加任务管理器端点，请单击“添加任务管理器”。 有关任务管理器设置的详细信息，请参阅[配置任务管理器端点](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)。
   * 要添加观察文件夹端点，请单击“添加WatchedFolder”。 有关观察文件夹设置的详细信息，请参阅[观察文件夹终结点设置](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)。
   * 要添加电子邮件端点，请单击“添加电子邮件”。 有关电子邮件设置的详细信息，请参阅[电子邮件终结点设置](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)。
   * 要添加EJB端点，请单击添加EJB并指定端点的名称和说明。
   * 要添加SOAP端点，请单击添加SOAP并指定端点的名称和描述。
   * 要添加远程处理端点，请单击“添加远程处理”。 有关远程设置的详细信息，请参阅[远程终结点设置](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)。
   * 要添加REST端点，请单击添加REST并指定端点的名称和描述。 请注意添加REST端点页面上显示的REST调用URL。
   * 要删除端点，请选中该端点旁边的复选框，然后单击“删除”。

1. 单击“下一步”。
1. 如果LCA中的进程或服务具有配置参数，则会显示“配置参数”页，您可以在此配置服务参数并单击下一步。
1. 在“配置安全性概要文件”页上，根据需要进行任何更改：

   * **需要呼叫者进行身份验证：**&#x200B;此设置指示是否可以使用或不使用凭据调用该服务。

     如果显示&#x200B;*当前需要呼叫者来验证*，则必须对服务的呼叫者进行验证并且必须授权该呼叫者的用户主体来调用该服务；否则，将拒绝调用尝试。 要删除验证需要，请单击“允许未验证的呼叫者”。

     如果显示&#x200B;*不需要呼叫者来验证*，则不需要对服务的呼叫者进行验证。 由于没有授权检查，因此服务的调用将始终成功。 要要求身份验证，请单击“要求呼叫者进行身份验证”。

   * **运行方式：**&#x200B;指定服务调用后使用的运行时标识。 要更改此选项，请单击“更改”。 从以下选项中进行选择：

     **未指定：**&#x200B;使用默认行为。

     **Invoker：**&#x200B;与调用服务的用户使用相同的标识。

     **系统：**&#x200B;以完全权限运行服务。 这是长期进程的默认设置。

     **命名用户：**&#x200B;允许您以特定用户身份运行服务。 这是短期进程的默认设置。 选择此选项时，单击选择用户以显示“选择承担者”页，在该页中可以搜索和选择用户。

   * 要将承担者添加到安全性配置文件，请单击“添加承担者”，然后选择要作为承担者添加的用户或组。 单击“下一步” ，然后选择要分配给此主体的权限：

     **INVOKE_PERM：**&#x200B;调用服务上的所有操作

     **MODIFY_CONFIG_PERM：**&#x200B;修改服务的配置

     **SUPERVISOR_PERM：**&#x200B;查看从进程创建的服务的进程实例数据

     **START_STOP_PERM：**&#x200B;启动和停止服务

     **ADD_REMOVE_ENDPOINTS_PERM：**&#x200B;添加、删除和修改服务的端点

     **CREATE_VERSION_PERM：**&#x200B;创建服务的版本

     **DELETE_版本_PERM：**&#x200B;要删除服务的版本

     **MODIFY_VERSION_PERM：**&#x200B;修改服务的版本

     **READ_PERM：**&#x200B;查看服务

     单击Finished将承担者添加到安全配置文件中。

1. 单击“已完成”以完成配置。

## 配置作为归档文件一部分的AEM表单 {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“应用程序管理”，然后单击“存档”选项卡。
1. 在“归档文件管理”页上，选择要配置的归档文件。
1. 在“查看存档”页上，选择突出显示的存档资源。
1. 配置导入的流程存档文件。

## 使用配置向导配置作为归档文件一部分的AEM表单 {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“应用程序管理”，然后单击“存档”选项卡。
1. 单击要配置的存档文件旁边的配置。
1. 此时将显示“配置端点”页，您可以在此进行所需的任何更改：

   * 要重命名端点或编辑其说明，请单击它。
   * 要添加任务管理器端点，请单击“添加任务管理器”。 有关任务管理器设置的详细信息，请参阅[配置任务管理器端点](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)。
   * 要添加观察文件夹端点，请单击“添加WatchedFolder”。 有关观察文件夹设置的详细信息，请参阅[观察文件夹终结点设置](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)。
   * 要添加电子邮件端点，请单击“添加电子邮件”。 有关电子邮件设置的详细信息，请参阅[电子邮件终结点设置](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)。
   * 要添加EJB端点，请单击添加EJB并指定端点的名称和说明。
   * 要添加SOAP端点，请单击添加SOAP并指定端点的名称和描述。
   * 要添加远程处理端点，请单击“添加远程处理”。 有关远程设置的详细信息，请参阅[远程终结点设置](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)。
   * 要添加REST端点，请单击添加REST并指定端点的名称和描述。 请注意添加REST端点页面上显示的REST调用URL。
   * 要删除端点，请选中该端点旁边的复选框，然后单击“删除”。

1. 单击“下一步”。
1. 如果LCA中的进程或服务具有配置参数，则会显示“配置参数”页，您可以在此配置服务参数并单击下一步。
1. 在“配置安全性概要文件”页上，您可以进行所需的任何更改：

   * **需要呼叫者进行身份验证：**&#x200B;此设置指示是否可以使用或不使用凭据调用该服务。

     如果显示&#x200B;*当前需要呼叫者来验证*，则必须对服务的呼叫者进行验证并且必须授权该呼叫者的用户主体来调用该服务；否则，将拒绝调用尝试。 要删除验证需要，请单击“允许未验证的呼叫者”。

     如果显示&#x200B;*不需要呼叫者来验证*，则服务的呼叫者可能会接受验证，也可能不接受验证。 由于没有授权检查，因此服务的调用将始终成功。 要要求身份验证，请单击“要求呼叫者进行身份验证”。

   * **运行方式：**&#x200B;指定服务调用后使用的运行时标识。 要更改此选项，请单击“更改”。 从以下选项中进行选择：

     **未指定：**&#x200B;使用默认行为。

     **Invoker：**&#x200B;与调用服务的用户使用相同的标识。

     **系统：**&#x200B;以完全权限运行服务。 这是长期进程的默认设置。

     **命名用户：**&#x200B;允许您以特定用户身份运行服务。 这是短期进程的默认设置。 选择此选项时，单击选择用户以显示“选择承担者”页，在该页中可以搜索和选择用户。

   * 要将承担者添加到安全性配置文件，请单击“添加承担者”，然后选择要作为承担者添加的用户或组。 单击“下一步” ，然后选择要分配给此主体的权限：

     **INVOKE_PERM：**&#x200B;调用服务上的所有操作

     **MODIFY_CONFIG_PERM：**&#x200B;修改服务的配置

     **SUPERVISOR_PERM：**&#x200B;查看从进程创建的服务的进程实例数据

     **START_STOP_PERM：**&#x200B;启动和停止服务

     **ADD_REMOVE_ENDPOINTS_PERM：**&#x200B;添加、删除和修改服务的端点

     **CREATE_VERSION_PERM：**&#x200B;创建服务的版本

     **DELETE_版本_PERM：**&#x200B;要删除服务的版本

     **MODIFY_VERSION_PERM：**&#x200B;修改服务的版本

     **READ_PERM：**&#x200B;查看服务

     单击Finished将承担者添加到安全配置文件中。

## 删除存档 {#remove-an-archive}

>[!NOTE]
>
>要删除包含存储在第三方存储库( EMC Documentum Content Server 、 IBM FileNet Content Manager或IBM Content Manager )中的资产的存档，还必须使用Workbench从存储库中删除资产文件。

1. 在管理控制台中，单击服务>应用程序和服务>存档管理。
1. 在“归档文件管理”页中，选中要删除的归档文件的复选框，然后单击“删除”。
