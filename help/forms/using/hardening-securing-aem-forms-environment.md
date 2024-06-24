---
title: 在OSGi环境中强化和保护AEM表单
description: 了解在OSGi服务器上保护AEM Forms安全的建议和最佳实践。
topic-tags: Security
role: Admin,User
exl-id: 5da3cc59-4243-4098-b1e0-438304fcd0c5
solution: Experience Manager, Experience Manager Forms
feature: Document Security,Adaptive Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 0%

---

# 在OSGi环境中强化和保护AEM表单 {#hardening-and-securing-aem-forms-on-osgi-environment}

了解在OSGi服务器上保护AEM Forms安全的建议和最佳实践。

保护服务器环境对组织至关重要。 本文介绍了有关保护运行AEM Forms的服务器安全的建议和最佳实践。 这不是适用于您的操作系统的全面主机强化文档。 相反，本文介绍您应该实施的各种安全强化设置，以增强已部署应用程序的安全性。 但是，为确保应用程序服务器保持安全，除了本文中提供的建议外，您还应该实施安全监控、检测和响应过程。 本文档还包含保护PII（个人身份信息）安全的最佳实践和准则。

本文面向负责规划AEM Forms应用程序或基础架构开发和部署的顾问、安全专家、系统架构师和IT专业人员。 这些角色包括以下常见角色：

* IT和运营工程师必须在自己或客户组织中部署安全的Web应用程序和服务器。
* 架构师和规划师，负责为组织中的客户规划建筑工作。
* IT安全专家，他们专注于在其组织内跨平台提供安全保护。
* 需要客户和合作伙伴详细资源的Adobe和合作伙伴顾问。

下图显示了典型AEM Forms部署中使用的组件和协议，包括相应的防火墙拓扑：

![典型架构](assets/typical-architecture.png)

AEM Forms具有高度可自定义性，可以在许多不同的环境中工作。 某些建议可能不适用于您的组织。

## 安全传输层 {#secure-transport-layer}

传输层安全漏洞是任何面向Internet或面向Intranet的应用程序服务器的首要威胁之一。 本节将介绍增强网络主机抵御这些漏洞的过程。 它涉及网络分段、传输控制协议/Internet协议(TCP/IP)栈栈强化以及使用防火墙进行主机保护。

### 限制开放端点  {#limit-open-endpoints}

组织可以具有外部防火墙，以限制最终用户与AEM Forms发布场之间的访问。 组织还可以具有内部防火墙，以限制发布场和组织元素内的其他元素（例如，创作实例、处理实例、数据库）之间的访问。 允许防火墙为最终用户和组织元素内部启用对有限数量的AEM Forms URL的访问：

#### 配置外部防火墙  {#configure-external-firewall}

您可以配置外部防火墙，以允许特定AEM Forms URL访问Internet。 要填写或提交自适应表单、HTML5、通信管理信件或登录到AEM Forms服务器，需要访问这些URL：

<table> 
 <tbody>
  <tr>
   <td>组件</td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>自适应表单</td> 
   <td>
    <ul> 
     <li>/content/dam/formsanddocuments/AF_PATH/jcr：content</li> 
     <li>/etc/clientlibs/fd/</li> 
     <li>/content/forms/af/AF_PATH</li> 
     <li>/libs/granite/csrf/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>HTML5表单</td> 
   <td>
    <ul> 
     <li>/content/forms/formsets/profiles/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>通信管理 </td> 
   <td>
    <ul> 
     <li>/aem/forms/createcorrespondence* </li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Forms门户 </td> 
   <td>
    <ul> 
     <li>/content/forms/portal/</li> 
     <li>/libs/cq/ui/widgets*</li> 
     <li>/libs/cq/security/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td> AEM Forms 应用程序</td> 
   <td>
    <ul> 
     <li>/j_security_check*</li> 
     <li>/soap/services/AuthenticationManagerService</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

#### 配置内部防火墙  {#configure-internal-firewall}

您可以将内部防火墙配置为允许某些AEM Forms组件（例如，创作实例、处理实例、数据库）与发布场以及拓扑图中提到的其他内部组件进行通信：

<table> 
 <tbody>
  <tr>
   <td>主机<br /> </td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>Publish场（发布节点）</td> 
   <td>/bin/receive</td> 
  </tr>
  <tr>
   <td>处理服务器</td> 
   <td>/content/forms/fp/*</td> 
  </tr>
  <tr>
   <td>Forms Workflow附加服务器(JEE服务器上的AEM Forms)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### 设置存储库权限和访问控制列表(ACL) {#setup-repository-permissions-and-access-control-lists-acls}

默认情况下，发布节点上可用的资源可供所有人访问。 已为所有资源启用只读访问权限。 必须启用匿名访问。 如果您计划限制表单查看并仅向经过身份验证的用户提交访问权限，则使用通用组以允许仅经过身份验证的用户对发布节点上可用的资源具有只读访问权限。 以下位置/目录包含需要强化的forms资源（已验证用户的只读访问权限）：

* /content/&amp;ast；
* /etc.clientlibs/fd/&amp;ast；
* /libs/fd/&amp;ast；

## 安全地处理表单数据  {#securely-handle-forms-data}

AEM Forms将数据存储到预定义的位置和临时文件夹。 您应该保护数据安全，防止未经授权的使用。

### 设置临时文件夹的定期清理 {#setup-periodic-cleanup-of-temporary-folder}

为文件附件配置表单、验证或预览组件时，相应的数据将存储在位于/tmp/fd/的发布节点上。 定期清除数据。 您可以修改默认数据清除作业，使其更积极。 要修改计划清除数据的作业，请打开AEM Web控制台，打开AEM Forms临时存储清理任务，并修改Cron表达式。

在上述方案中，仅为经过身份验证的用户保存数据。 此外，使用访问控制列表(ACL)保护数据。 因此，修改数据清除是保护信息的额外步骤。

### 通过Forms Portal提交操作保存的安全数据 {#secure-data-saved-by-forms-portal-submit-action}

默认情况下，自适应表单的Forms Portal提交操作会将数据保存在发布节点的本地存储库中。 数据保存在/content/forms/fp中。 **建议不要将数据存储在发布实例上。**

您可以将存储服务配置为直接发送到处理群集，而无需在发布节点上本地保存任何内容。 处理群集位于专用防火墙后面的安全区域中，数据保持安全。

使用AEM DS设置服务的处理服务器的凭据将数据从发布节点发布到处理服务器。 使用对处理服务器的存储库具有读写访问权限的受限制的非管理用户的凭据。 有关更多信息，请参阅 [为草稿和提交配置存储服务](/help/forms/using/configuring-draft-submission-storage.md).

### 由表单数据模型(FDM)处理的安全数据 {#secure-data-handled-by-form-data-model-fdm}

使用具有最低所需权限的用户帐户为表单数据模型(FDM)配置数据源。 使用管理帐户可以向未授权用户提供元数据和架构实体的开放访问。\
数据集成还提供了授权FDM服务请求的方法。 您可以插入执行前和执行后授权机制来验证请求。 服务请求是在预填表单、提交表单和通过规则调用服务时生成的。

**预处理授权：** 您可以使用预处理授权在执行请求之前验证请求的真实性。 您可以使用输入、服务和请求详细信息来允许或停止执行请求。 如果停止执行，您可以返回数据集成异常OPERATION_ACCESS_DENIED。 您也可以在发送客户端请求以供执行之前对其进行修改。 例如，更改输入和添加其他信息。

**后处理授权：** 您可以使用后处理授权来验证和控制结果，然后再将结果返回给请求者。 您还可以过滤、修剪和向结果插入附加数据。

### 限制用户访问 {#limit-user-access}

创作、发布和处理实例需要一组不同的用户角色。 不要使用管理员凭据运行任何实例。

**在发布实例上：**

* 只有表单用户组的用户可以预览、创建草稿和提交表单。
* 只有cm-user-agent组的用户可以预览通信管理信件。
* 禁用所有非必要的匿名访问。

**在创作实例上：**

* 还有一组不同的预定义组，每个角色都具有特定权限。 将用户分配到组。

   * 表单 — 用户组的用户：

      * 可以创建、填写、发布和提交表单。
      * 无法创建基于XDP的自适应表单。
      * 无权为自适应表单编写脚本。
      * 无法导入XDP或任何包含XDP的包

   * 表单超级用户组的用户创建、填写、发布和提交所有类型的表单，编写自适应表单的脚本，导入包含XDP的包。
   * 模板作者和模板超级用户可以预览和创建模板。
   * fdm作者的用户可以创建和修改表单数据模型。
   * cm-user-agent组的用户可以创建、预览和发布通信管理信件。
   * 工作流编辑器组的用户可以创建收件箱应用程序和工作流模型。

**在处理作者时：**

* 对于远程保存和提交用例，请创建一个对crx-repository的content/form/fp路径具有读取、创建和修改权限的用户。
* 将用户添加到工作流 — 用户组，使用户能够使用AEM收件箱应用程序。

## AEM Forms环境的安全Intranet元素 {#secure-intranet-elements-of-an-aem-forms-environment}

通常，处理群集和Forms Workflow加载项(JEE上的AEM Forms)在防火墙后运行。 所以，这些被认为是安全的。 您仍然可以执行一些步骤来强化这些环境：

### 安全处理群集 {#secure-processing-cluster}

处理集群在创作模式下运行，但不将其用于开发活动。 不允许在处理集群的内容作者和表单用户组中包含普通用户。

### 使用AEM最佳实践来保护AEM Forms环境的安全 {#use-aem-best-practices-to-secure-an-aem-forms-environment}

本文档提供了特定于AEM Forms环境的说明。 您应该采取以确保在部署时基础AEM安装是安全的。 有关详细说明，请参阅 [AEM安全核对清单](/help/sites-administering/security-checklist.md) 文档。
