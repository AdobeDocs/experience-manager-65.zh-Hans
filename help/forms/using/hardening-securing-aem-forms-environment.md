---
title: 在OSGi环境上强化和保护AEM表单
seo-title: 在OSGi环境上强化和保护AEM表单
description: 了解在OSGi服务器上保护AEM Forms的建议和最佳实践。
seo-description: 了解在OSGi服务器上保护AEM Forms的建议和最佳实践。
uuid: abca7e7c-38c3-44f5-8d8a-4615cfce26c6
topic-tags: Security
discoiquuid: b1bd04bf-0d6d-4e6b-8c7c-eafd1a24b5fe
role: 管理员
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1464'
ht-degree: 0%

---


# 在OSGi环境{#hardening-and-securing-aem-forms-on-osgi-environment}上加固和保护AEM表单

了解在OSGi服务器上保护AEM Forms的建议和最佳实践。

保护服务器环境对组织至关重要。 本文描述了保护运行AEM Forms的服务器的建议和最佳实践。 这不是针对您的操作系统的全面的主机强化文档。 相反，本文描述了您应实施的各种安全强化设置，以增强已部署应用程序的安全性。 但是，为了确保应用程序服务器保持安全，除了本文中提供的建议之外，您还应实施安全监控、检测和响应程序。 该文档还包含保护PII（个人身份信息）的最佳实践和指南。

本文面向负责规划AEM Forms应用程序或基础架构开发和部署的顾问、安全专家、系统架构师和IT专业人士。 这些角色包括以下常见角色：

* IT和运营部门的工程师，他们必须在自己或客户组织中部署安全的Web应用程序和服务器。
* 负责为组织中的客户规划建筑工作的架构师和规划师。
* IT安全专家，他们专注于在组织内跨平台提供安全性。
* 来自Adobe和合作伙伴的顾问，他们需要为客户和合作伙伴提供详细的资源。

下图显示了典型AEM Forms部署中使用的组件和协议，包括相应的防火墙拓扑：

![典型体系结构](assets/typical-architecture.png)

AEM Forms可高度自定义，可在多种不同的环境中工作。 某些建议可能不适用于您的组织。

## 安全传输层{#secure-transport-layer}

传输层安全漏洞是任何面向Internet或面向Intranet的应用程序服务器面临的首要威胁之一。 本节介绍针对这些漏洞强化网络上的主机的过程。 它解决了网络分段、传输控制协议/因特网协议(TCP/IP)栈加固以及使用防火墙保护主机的问题。

### 限制开放端点{#limit-open-endpoints}

组织可以具有外部防火墙来限制最终用户与AEM Forms发布场之间的访问。 组织还可以具有内部防火墙，以限制发布场与组织元素中的其他元素（例如，作者实例、处理实例、数据库）之间的访问。 允许防火墙允许最终用户和组织元素中访问有限数量的AEM Forms URL:

#### 配置外部防火墙{#configure-external-firewall}

您可以配置外部防火墙，以允许特定AEM Forms URL访问Internet。 要填写或提交自适应表单、HTML5、通信管理信件或登录AEM Forms服务器，需要访问以下URL:

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
     <li>/content/dam/formsanddocuments/AF_PATH/jcr:content</li> 
     <li>/etc/clientlibs/fd/</li> 
     <li>/content/forms/af/AF_PATH</li> 
     <li>/libs/granite/csrf/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>HTML5 表单</td> 
   <td>
    <ul> 
     <li>/content/forms/formsets/用户档案/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>通信管理 </td> 
   <td>
    <ul> 
     <li>/aem/forms/createcorresponsements* </li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Forms Portal </td> 
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

#### 配置内部防火墙{#configure-internal-firewall}

您可以配置内部防火墙，以允许某些AEM Forms组件（例如，作者实例、处理实例、数据库）与发布场和拓扑图中提到的其他内部组件进行通信：

<table> 
 <tbody>
  <tr>
   <td>主机<br /> </td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>发布场（发布节点）</td> 
   <td>/bin/receive</td> 
  </tr>
  <tr>
   <td>处理服务器</td> 
   <td>/content/forms/fp/*</td> 
  </tr>
  <tr>
   <td>Forms Workflow加载项服务器(JEE服务器上的AEM Forms)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### 设置存储库权限和访问控制列表(ACL){#setup-repository-permissions-and-access-control-lists-acls}

默认情况下，每个人都可以访问发布节点上可用的资产。 对所有资产启用只读访问。 需要启用匿名访问。 如果您计划限制表单视图并仅向经过身份验证的用户提交访问权限，则使用通用组仅允许经过身份验证的用户对发布节点上可用的资产具有只读访问权限。 以下位置/目录包含需要强化的表单资源（对经过身份验证的用户具有只读访问权限）：

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## 安全地处理表单数据{#securely-handle-forms-data}

AEM Forms会将数据存储到预定义的位置和临时文件夹。 您应保护数据，以防未经授权的使用。

### 设置临时文件夹{#setup-periodic-cleanup-of-temporary-folder}的定期清理

为文件附件、验证或预览组件配置表单时，相应的数据会存储在位于/tmp/fd/的发布节点上。 数据会定期清除。 您可以将默认数据清除作业修改为更具攻击性。 要修改计划清除数据的作业，请打开AEM Web Console，打开AEM Forms临时存储清除任务，然后修改Cron表达式。

在上述情况下，数据仅保存给经过身份验证的用户。 此外，访问控制列表(ACL)保护数据。 因此，修改数据清除是保护信息的额外步骤。

### 保护表单门户提交操作{#secure-data-saved-by-forms-portal-submit-action}保存的数据

默认情况下，自适应表单的表单门户提交操作会将数据保存到发布节点的本地存储库中。 数据保存在/content/forms/fp。 **不建议在发布实例上存储数据。**

您可以配置存储服务以通过线向处理群集发送，而无需在发布节点上本地保存任何内容。 处理群集驻留在专用防火墙后的安全区域中，数据保持安全。

使用AEM DS设置服务的处理服务器凭据将数据从发布节点发布到处理服务器。 建议使用具有对处理服务器存储库的读写访问权限的受限非管理用户的凭据。 有关详细信息，请参阅[配置草稿和提交的存储服务](/help/forms/using/configuring-draft-submission-storage.md)。

### 通过表单数据模型(FDM){#secure-data-handled-by-form-data-model-fdm}处理的安全数据

使用具有最低所需权限的用户帐户为表单数据模型(FDM)配置数据源。 使用管理帐户可以为未经授权的用户提供对元数据和模式实体的开放访问。\
数据集成还提供了对FDM服务请求授权的方法。 您可以插入执行前和执行后授权机制来验证请求。 在预填表单、提交表单和通过规则调用服务时生成服务请求。

**预处理授权：** 您可以在执行请求之前使用预处理授权来验证请求的真实性。您可以使用输入、服务和请求详细信息来允许或停止执行请求。 如果停止执行，则可以返回数据集成异常OPERATION_ACCESS_DENIED。 您还可以在发送客户端请求以执行之前对其进行修改。 例如，更改输入并添加其他信息。

**流程后授权：** 在将结果返回给请求者之前，您可以使用流程后授权来验证和控制结果。您还可以过滤、修剪和插入其他数据到结果。

### 限制用户访问{#limit-user-access}

创作、发布和处理实例需要一组不同的用户角色。 请勿使用管理员凭据运行任何实例。

**在发布实例上：**

* 只有表单用户组的用户才能预览、创建草稿和提交表单。
* 只有cm-user-agent组的用户才能预览通信管理信件。
* 禁用所有非必要的匿名访问。

**在作者实例中：**

* 有一组预定义用户组，每个人物具有特定权限。 将用户分配到组。

   * 表单用户组的用户：

      * 可以创建、填写、发布和提交表单。
      * 无法创建基于XDP的自适应表单。
      * 没有编写自适应表单脚本的权限。
      * 无法导入XDP或包含XDP的任何包
   * 表单用户 — 高级用户组创建、填写、发布和提交所有类型的表单，为自适应表单编写脚本，导入包含XDP的包。
   * 模板作者和模板权限用户的用户可以预览和创建模板。
   * fdm-authors的用户可以创建和修改表单数据模型。
   * cm-user-agent组的用户可以创建、预览和发布通信管理信件。
   * 工作流编辑器组的用户可以创建收件箱应用程序和工作流模型。


**处理作者时：**

* 对于远程保存和提交用例，请创建具有crx-repository的content/form/fp路径上的读取、创建和修改权限的用户。
* 将用户添加到工作流用户组，以使用户能够使用AEM收件箱应用程序。

## AEM Forms环境{#secure-intranet-elements-of-an-aem-forms-environment}的安全内部网元素

通常，处理群集和Forms Workflow加载项(JEE上的AEM Forms)在防火墙后运行。 因此，这些都被认为是安全的。 您仍可以执行一些步骤来强化这些环境:

### 安全处理群集{#secure-processing-cluster}

处理群集在创作模式下运行，但不将其用于开发活动。 不允许将普通用户包含在处理群集的内容作者和表单用户组中。

### 使用AEM最佳做法保护AEM Forms环境{#use-aem-best-practices-to-secure-an-aem-forms-environment}

此文档提供特定于AEM Forms 环境的说明。 您应确保在部署时基础AEM安装是安全的。 有关详细说明，请参阅[AEM安全核对清单](/help/sites-administering/security-checklist.md)文档。
