---
title: 文档安全 |处理用户数据
seo-title: Document Security | Handling user data
description: 文档安全 |处理用户数据
uuid: 1624a465-8b0c-4347-a53f-1118bfa6e18f
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 898268cb-4426-421f-8f63-d75bd85cb57f
role: Admin
exl-id: 00c01a12-1180-4f35-9179-461bf177c787
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# 文档安全 |处理用户数据 {#document-security-handling-user-data}

AEM Forms文档安全允许您创建、存储预定义的安全设置并将其应用于文档。 它确保只有授权用户才能使用文档。 您可以使用策略保护文档。 策略是包含安全设置和授权用户列表的信息集合。 您可以将策略应用于一个或多个文档，并授权在AEM Forms JEE用户管理中添加的用户。

<!-- Fix broken link For more information about how document security works, see AEM Forms JEE administration help. -->

## 用户数据和数据存储 {#user-data-and-data-stores}

文档安全存储与受保护文档相关的策略和数据，包括数据库中的用户数据，如My Sql、My Sql、MS SQL Server和IBM DB2。 此外，在用户管理中存储策略中授权用户的数据。 有关存储在用户管理中的数据的信息，请参阅 [Forms用户管理：处理用户数据](/help/forms/using/user-management-handling-user-data.md).

下表映射文档安全在数据库表中组织数据的方式。

<table>
 <tbody>
  <tr>
   <td>数据库表</td>
   <td>描述</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalKeyEntity</code></td>
   <td>存储有关用户的主键的信息。 这些键用于脱机文档安全工作流。</td>
  </tr>
  <tr>
   <td><code>EdcAuditEntity</code></td>
   <td>存储有关审核事件（如用户事件、文档事件和策略事件）的信息。</td>
  </tr>
  <tr>
   <td><p><code>EdcLicenseEntity</code></p> </td>
   <td>存储受保护文档的记录。 它存储每个受保护文档的许可证详细信息。</td>
  </tr>
  <tr>
   <td><p><code>EdcDocumentEntity</code></p> </td>
   <td>存储系统中创建的每个许可证的文档名称。</td>
  </tr>
  <tr>
   <td><p><code>EdcRevokationEntity</code></p> </td>
   <td>存储有关撤销和恢复受保护文档的信息。</td>
  </tr>
  <tr>
   <td><code>EdcMyPolicyListEntity</code></td>
   <td>存储有关可以创建个人策略的用户的信息，这些策略显示在“策略”页面的“我的策略”选项卡下。 </td>
  </tr>
  <tr>
   <td><code>EdcPolicyEntity</code></td>
   <td>存储有关策略的信息。 每个策略都对应于此表中的一行。</td>
  </tr>
  <tr>
   <td><code>EdcPolicyXmlEntity</code></td>
   <td>存储活动策略的XML文件。 策略XML<sup> </sup>包含对与策略关联的用户的主ID的引用。 策略XML存储为Blob对象。</td>
  </tr>
  <tr>
   <td><code>EdcPolicyArchiveEntity</code></td>
   <td>存储有关已存档策略的信息。 存档的策略包含其作为Blob对象存储的策略XML。</td>
  </tr>
  <tr>
   <td><p><code>EdcPolicySetPrincipalEntity</code></p> <p><code>EdcPolicySetPrincipalEnt</code> (Oracle和MS SQL数据库)</p> </td>
   <td>存储策略集和用户之间的映射。</td>
  </tr>
  <tr>
   <td><code>EdcInvitedUserEntity</code></td>
   <td>存储有关受邀用户的信息。</td>
  </tr>
 </tbody>
</table>

## 访问和删除用户数据 {#access-and-delete-user-data}

您可以访问和导出数据库中用户的文档安全数据，如果需要，请永久删除该数据。

要从数据库导出或删除用户数据，您需要使用数据库客户端连接到数据库，并根据用户的一些个人身份信息查找主ID。 例如，要使用登录ID检索用户的主体ID，请运行以下 `select` 命令。

在 `select` 命令，替换 `<user_login_id>` ，其登录ID是您要从 `EdcPrincipalUserEntity` 数据库表。

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

知道主体ID后，即可导出或删除用户数据。

### 导出用户数据 {#export-user-data}

运行以下数据库命令，从数据库表导出主体ID的用户数据。 在 `select` 命令，替换 `<principal_id>` 具有要导出其数据的用户的主体ID。

>[!NOTE]
>
>以下命令使用My SQL和IBM DB2数据库中的数据库表名。 在Oracle和MS SQL数据库上运行这些命令时，请替换 `EdcPolicySetPrincipalEntity` with `EdcPolicySetPrincipalEnt` 中。

```sql
Select * from EdcPrincipalKeyEntity where principalid = '<principal_id>';

Select * from EdcLicenseEntity where publisherId = '<principal_id>';

Select * from EdcDocumentEntity where id in (Select documentid from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcRevokationEntity where licenseid in (Select id from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcMyPolicyListEntity where principalId = '<principal_id>';

Select * from edcpolicyentity where policyownerId = '<principal_id>';

Select * from edcpolicyxmlentity where policyidref in (Select id from edcpolicyentity where policyownerId = '<principal_id>');

Select * from edcpolicyarchiveentity where policyownerId = '<principal_id>';

Select * from edcpolicysetprincipalentity where principalId = '<principal_id>';

Select * from edcinviteduserentity where principalId = '<principal_id>';
```

>[!NOTE]
>
>要从 `EdcAuditEntity` 表，使用 [EventManager.exportEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) 采用的API [EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) 作为参数，以根据 `principalId`, `policyId`或 `licenseId`.

要获取系统中某个用户的完整数据，必须从用户管理数据库访问和导出数据。 有关更多信息，请参阅 [Forms用户管理：处理用户数据](/help/forms/using/user-management-handling-user-data.md).

### 删除用户数据 {#delete-user-data}

执行以下操作，以从数据库表中删除主体ID的文档安全数据。

1. 关闭AEM Forms服务器。
1. 运行以下数据库命令，从数据库表中删除主ID的数据，以确保文档安全。 在 `Delete` 命令，替换 `<principal_id>` 具有要删除其数据的用户的主体ID。

   ```sql
   Delete from EdcPrincipalKeyEntity where principalid = '<principal_id>';
   
   Delete from EdcMyPolicyListEntity where principalId = '<principal_id>';
   
   Delete from edcpolicyarchiveentity where policyownerId = '<principal_id>';
   
   Delete from edcpolicysetprincipalentity where principalId = '<principal_id>';
   
   Delete from edcinviteduserentity where principalId = '<principal_id>';
   ```

   >[!NOTE]
   >
   >从 `EdcAuditEntity` 表，使用 [EventManager.deleteEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) 采用的API [EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) 作为删除基于 `principalId`, `policyId`或 `licenseId`.

1. 活动和存档的策略XML文件存储在 `EdcPolicyXmlEntity` 和 `EdcPolicyArchiveEntity` 数据库表。 要从这些表中删除用户的数据，请执行以下操作：

   1. 在 `EdcPolicyXMLEntity` 或 `EdcPolicyArchiveEntity` 表并提取XML文件。 XML文件与下面所示的文件类似。
   1. 编辑XML文件以删除主体ID的blob。
   1. 对另一个文件重复步骤1和2。

   >[!NOTE]
   >
   >您必须删除 `Principal` 主ID或策略XML的标记可能已损坏或无法使用。

   ```xml
   <ns2:Principal PrincipalNameType="USER">
       <ns2:PrincipalDomain>OID</ns2:PrincipalDomain>
       <ns2:PrincipalName>56F33FEB-098A-1036-A651-00000A2A2656</ns2:PrincipalName>
   </ns2:Principal>
   </ns2:PolicyEntry>
       <ns2:Property PropertyName="isCertified">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">false</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="encryptionAlgorithm">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">AES128</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="AccessDeniedErrorMessage">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string"></ns2:PropertyValue>
       </ns2:Property>
   <ns2:PolicyEntry>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.onlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.copy" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.offlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.accessible" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.editNotes" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.edit" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.fillAndSign" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printHigh" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printLow" Access="ALLOW"/>
   ```

   除了直接从 `EdcPolicyXmlEntity` 表格中，还有两种方法可以实现此目的：

   **使用管理控制台**

   1. 以管理员身份登录Forms JEE管理控制台，网址为https://[*服务器*]:[*端口*]/adminui。
   1. 导航到 **[!UICONTROL 服务>文档安全>策略集]**.
   1. 打开策略集，并从策略中删除用户。

   **使用文档安全网页**

   具有创建个人策略权限的文档安全用户可以从其策略中删除用户数据。 为此，请执行以下操作：

   1. 具有个人策略的用户可登录其文档安全网页： https://[*服务器*]:[*端口*]/edc.
   1. 导航到 **[!UICONTROL 服务>文档安全>我的策略]**.
   1. 打开策略并从策略中删除用户。

   >[!NOTE]
   >
   >管理员可以在 **[!UICONTROL 服务>文档安全>我的策略]** 使用管理控制台。

1. 从用户管理数据库中删除主体ID的数据。 有关详细步骤，请参阅 [Forms用户管理 |处理用户数据](/help/forms/using/user-management-handling-user-data.md).
1. 启动AEM Forms服务器。
