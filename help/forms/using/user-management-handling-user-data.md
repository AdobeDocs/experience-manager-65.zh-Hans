---
title: Forms用户管理 |处理用户数据
seo-title: Forms用户管理 |处理用户数据
description: Forms用户管理 |处理用户数据
uuid: 2b76b69f-6f3a-4f1a-a2a4-d39f5e529f75
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a88fc933-f1af-4798-b72f-10e7b0d2fd11
role: Admin
exl-id: eeeab5d1-073a-4e13-a781-391dfe70bb37
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---

# Forms用户管理 |处理用户数据 {#forms-user-management-handling-user-data}

用户管理是AEM Forms JEE组件，它允许创建、管理和授权AEM Forms用户访问AEM Forms。 用户管理使用域作为获取用户信息的目录。 支持以下域类型：

**本地域**:此类域未连接到第三方存储系统。用户和组而是在本地创建，并驻留在用户管理数据库中。 密码存储在本地，并使用本地数据库完成身份验证。

**混合域**:此类域未连接到第三方存储系统。用户和组而是在本地创建，并驻留在用户管理数据库中。 与本地域不同，混合域使用外部身份验证提供程序，该提供程序可以是LDAP、Kerberos、SAML或自定义身份验证提供程序。

**企业域**:由位于第三方存储系统（如LDAP目录）中的用户和组组成。用户管理不写入第三方存储系统。 用户管理而是将用户和组信息与用户管理数据库同步。 企业域还使用外部身份验证提供程序，该提供程序可以是LDAP、Kerberos、SAML或自定义身份验证提供程序。

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## 用户数据和数据存储 {#user-data-and-data-stores}

用户管理将用户数据存储在数据库中，如My Sql 、Oracle、MS SQL Server和IBM DB2。 此外，任何在AEM作者的Forms应用程序(`https://'[server]:[port]'lc`)中至少登录过一次的用户，都会在AEM存储库中创建该用户。 因此，用户管理存储在以下数据存储中：

* 数据库
* AEM存储库
* 第三方存储，如LDAP目录

>[!NOTE]
>
>存储在第三方存储中的数据不在本文档的范围之内。 直接联系第三方供应商以管理此类存储中的用户数据。

### 数据库 {#database}

用户管理将用户数据存储在以下数据库表中：

<table>
 <tbody>
  <tr>
   <td>数据库表</td>
   <td>描述</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalEntity</code></td>
   <td><p>存储有关主实体的信息。 主体可以是用户、组或角色。</p> <p> </p> </td>
  </tr>
  <tr>
   <td><code>EdcPrincipalUserEntity</code></td>
   <td>存储用户的个人身份信息(PII)。 它包含一个适用于来自本地、企业和混合域的每个用户的条目。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>(Oracle和MS SQL数据库)</p> </td>
   <td>仅存储本地用户的数据。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>(Oracle和MS SQL数据库)</p> </td>
   <td>包含来自本地、企业和混合域的所有用户条目。 它包含用户电子邮件ID。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code> (Oracle和MS SQL数据库)</p> </td>
   <td>存储用户和组之间的映射。</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>存储用户和组的角色和主体之间的映射。</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>存储用户和组的主权限和权限之间的映射。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code> (Oracle和MS SQL数据库)</p> </td>
   <td>存储与主体对应的旧属性值和新属性值。<br /> </td>
  </tr>
 </tbody>
</table>

### AEM存储库 {#aem-repository}

对于在`https://'[server]:[port]'lc`下至少访问过Forms应用程序一次的用户，用户管理数据也存储在AEM存储库中。

## 访问和删除用户数据 {#access-and-delete-user-data}

您可以访问和导出用户管理数据库和AEM存储库中用户的用户管理数据，并根据需要永久删除该数据。

### 数据库 {#database-1}

要从用户管理数据库导出或删除用户数据，您需要使用数据库客户端连接到数据库，并根据用户的某些PII查找主ID。 例如，要使用登录ID检索用户的主ID，请在数据库中运行以下`select`命令。

在`select`命令中，将`<user_login_id>`替换为您要检索其主ID的用户的登录ID。

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

知道主体ID后，即可导出或删除用户数据。

#### 导出用户数据 {#export-user-data}

运行以下数据库命令，从数据库表中导出主体ID的用户管理数据。 在`select`命令中，将`<principal_id>`替换为要导出其数据的用户的主ID。

>[!NOTE]
>
>以下命令使用My SQL和IBM DB2数据库中的数据库表名。 在Oracle和MS SQL数据库上运行这些命令时，请替换命令中的以下表名：
>
>* 将`EdcPrincipalLocalAccountEntity`替换为`EdcPrincipalLocalAccount`
   >
   >
* 将`EdcPrincipalEmailAliasEntity`替换为`EdcPrincipalEmailAliasEn`
   >
   >
* 将`EdcPrincipalMappingEntity`替换为`EdcPrincipalMappingEntit`
   >
   >
* 将`EdcPrincipalGrpCtmntEntity`替换为`EdcPrincipalGrpCtmntEnti`

>



```sql
Select * from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (Select id from EDCPRINCIPALENTITY where id='<principal_id>'));

Select * from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalEntity where id='<principal_id>';
```

#### 删除用户数据 {#delete-user-data}

执行以下操作，以从数据库表中删除主体ID的用户管理数据。

1. 如[删除用户数据](/help/forms/using/user-management-handling-user-data.md#delete-aem)中所述，从AEM存储库中删除用户数据（如果适用）。
1. 关闭AEM Forms服务器。
1. 运行以下数据库命令，从数据库表中删除主体ID的用户管理数据。 在`Delete`命令中，将`<principal_id>`替换为要删除其数据的用户的主ID。

   ```sql
   Delete from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (select id from EdcPrincipalEntity where id='<principal_id>'));
   
   Delete from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalEntity where id='<principal_id>';
   ```

1. 启动AEM Forms服务器。

### AEM存储库 {#aem-repository-1}

Forms JEE用户在AEM存储库中拥有其数据(如果他们至少访问了AEM Forms创作实例之一)。 您可以从AEM存储库访问和删除其用户数据。

#### 访问用户数据 {#access-user-data}

要查看在AEM存储库中创建的用户，请使用AEM管理员凭据登录`https://'[server]:[port]'/lc/useradmin`。 请注意，URL中的`server`和`port`是AEM创作实例的。 在此，您可以使用用户名搜索用户。 双击某个用户可查看该用户的属性、权限和群组等信息。 用户的`Path`属性指定在AEM存储库中创建的用户节点的路径。

#### 删除用户数据 {#delete-aem}

要删除用户，请执行以下操作：

1. 转到具有AEM管理员凭据的`https://'[server]:[port]'/lc/useradmin`。
1. 搜索用户，然后双击用户名以打开用户属性。 复制`Path`属性。
1. 转到位于`https://'[server]:[port]'/lc/crx/de/index.jsp`的AEM CRX DELite，然后导航或搜索用户路径。
1. 删除路径，然后单击&#x200B;**[!UICONTROL Save All]**&#x200B;以从AEM存储库中永久删除用户。
