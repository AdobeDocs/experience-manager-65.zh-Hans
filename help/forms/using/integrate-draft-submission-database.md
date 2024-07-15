---
title: 将草稿和提交组件与数据库集成的示例
description: 参考自定义数据和元数据服务的实施，以便将草稿和提交组件与数据库集成。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
exl-id: 2e4f8f51-df02-4bbb-99bb-30181facd1e0
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 1%

---

# 将草稿和提交组件与数据库集成的示例 {#sample-for-integrating-drafts-submissions-component-with-database}

## 示例概述 {#sample-overview}

AEM Forms portal草稿和提交组件允许用户将其表单另存为草稿，并稍后从任何设备提交。 此外，用户还可以在门户网站上查看他们提交的表单。 为了启用此功能，AEM Forms提供数据和元数据服务来存储表单中用户填写的数据以及与草稿和已提交表单关联的表单元数据。 默认情况下，此数据存储在CRX存储库中。 但是，当用户通过AEM发布实例（通常位于企业防火墙之外）与表单进行交互时，组织可能会希望自定义数据存储以便使其更加安全和可靠。

本文档中讨论的示例是自定义数据和元数据服务的参考实现，用于将草稿和提交组件与数据库集成。 示例实现中使用的数据库是&#x200B;**MySQL 5.6.24**。 但是，您可以将草稿和提交组件与您选择的任何数据库集成。

>[!NOTE]
>
>* 本文档中说明的示例和配置均基于MySQL 5.6.24，您必须将它们适当地替换为您的数据库系统。
>* 确保您已安装最新版本的AEM Forms附加组件包。 有关可用包的列表，请参阅[AEM Forms发行版](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)文章。
>* 示例包仅适用于自适应Forms提交操作。

## 设置和配置示例 {#set-up-and-configure-the-sample}

在所有创作和发布实例上执行以下步骤，以安装和配置示例：

1. 将以下&#x200B;**aem-fp-db-integration-sample-pkg-6.1.2.zip**&#x200B;包下载到您的文件系统。

   用于数据库集成的示例包

[获取文件](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. 转到https://[*host*]：[*port*]/crx/packmgr/上的AEM包管理器。
1. 单击&#x200B;**[!UICONTROL 上传包]**。

1. 浏览以选择&#x200B;**aem-fp-db-integration-sample-pkg-6.1.2.zip**&#x200B;包，然后单击&#x200B;**[!UICONTROL 确定]**。
1. 单击包旁边的&#x200B;**[!UICONTROL Install]**&#x200B;以安装包。
1. 转到&#x200B;**[!UICONTROL AEM Web控制台配置]**
页面位于https://[*主机*]：[*端口*]/system/console/configMgr。
1. 单击以在编辑模式下打开&#x200B;**[!UICONTROL Forms门户草稿和提交配置]**。

1. 按照下表所述指定属性的值：

   | **属性** | **描述** | **值** |
   |---|---|---|
   | Forms Portal草稿数据服务 | 草稿数据服务的标识符 | formsportal.sampledataservice |
   | Forms Portal草稿元数据服务 | 草稿元数据服务的标识符 | formsportal.samplemetadataservice |
   | Forms门户提交数据服务 | 提交数据服务的标识符 | formsportal.sampledataservice |
   | Forms门户提交元数据服务 | 提交元数据服务的标识符 | formsportal.samplemetadataservice |
   | Forms门户待处理签名数据服务 | 待处理签名数据服务的标识符 | formsportal.sampledataservice |
   | Forms Portal待处理签名元数据服务 | 待处理签名元数据服务的标识符 | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >服务的名称作为`aem.formsportal.impl.prop`键的值来解析，如下所示：

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   您可以更改数据和元数据表的名称。

   要为元数据表提供其他名称，请执行以下操作：

   * 在“Web控制台配置”中，找到并单击Forms Portal元数据服务示例实施。 您可以更改数据源、元数据/其他元数据表名的值。

   要为数据表提供不同的名称，请执行以下操作：

   * 在“Web控制台配置”中，找到并单击Forms Portal数据服务示例实施。 您可以更改数据源和数据表名称的值。

   >[!NOTE]
   >
   >如果更改表名称，请在表单门户配置中提供它们。

1. 保留其他配置不变，然后单击&#x200B;**[!UICONTROL 保存]**。

1. 可以通过Apache Sling Connection Pooled Data Source进行数据库连接。
1. 对于Apache Sling连接，在Web控制台配置的编辑模式下，查找并单击以打开&#x200B;**[!UICONTROL Apache Sling连接池化数据源]**。 按照下表所述指定属性的值：

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>价值</strong></td>
  </tr>
  <tr>
   <td>数据源名称</td>
   <td><p>用于从数据源池筛选驱动程序的数据源名称</p> <p><strong>注意： </strong><em>示例实现使用FormsPortal作为数据源名称。</em></p> </td>
  </tr>
  <tr>
   <td>JDBC驱动程序类</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>JDBC连接URI<br /> </td>
   <td>jdbc:mysql://[<em>主机</em>]：[<em>端口</em>]/[<em>架构名称</em>]</td>
  </tr>
  <tr>
   <td>用户名</td>
   <td>用于对数据库表进行身份验证和执行操作的用户名</td>
  </tr>
  <tr>
   <td>密码</td>
   <td>与用户名关联的密码</td>
  </tr>
  <tr>
   <td>事务隔离</td>
   <td>读取已提交</td>
  </tr>
  <tr>
   <td>最大活动连接数</td>
   <td>1000</td>
  </tr>
  <tr>
   <td>最大空闲连接数</td>
   <td>100</td>
  </tr>
  <tr>
   <td>最小空闲连接数</td>
   <td>10</td>
  </tr>
  <tr>
   <td>初始大小</td>
   <td>10</td>
  </tr>
  <tr>
   <td>最大等待</td>
   <td>100000</td>
  </tr>
  <tr>
   <td>借阅测试</td>
   <td>已选中</td>
  </tr>
  <tr>
   <td>空闲时测试</td>
   <td>已选中</td>
  </tr>
  <tr>
   <td>验证查询</td>
   <td>示例值为SELECT 1(mysql)，从dual(oracle)中选择1，选择1(MS Sql Server) (validationQuery)</td>
  </tr>
  <tr>
   <td>验证查询超时</td>
   <td>10000</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 示例中未提供用于MySQL的JDBC驱动程序。 请确保已为其配置并提供配置JDBC连接池所需的信息。
>* 将创作实例和发布实例指向使用同一数据库。 对于所有创作实例和发布实例，JDBC连接URI字段的值必须相同。

1. 保留其他配置不变，然后单击&#x200B;**[!UICONTROL 保存]**。

1. 如果数据库模式中已有表，请跳至下一步。

   否则，如果数据库模式中还没有表，请执行以下SQL语句，为数据库模式中的数据、元数据和其它元数据创建单独的表：

   >[!NOTE]
   >
   >创作实例和发布实例不需要不同的数据库。 在所有创作实例和发布实例上使用相同的数据库。

   数据表的&#x200B;**SQL语句**

   ```sql
   CREATE TABLE `data` (
   `owner` varchar(255) DEFAULT NULL,
   `data` longblob,
   `metadataId` varchar(45) DEFAULT NULL,
   `id` varchar(45) NOT NULL,
   PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   元数据表的&#x200B;**SQL语句**

   ```sql
   CREATE TABLE `metadata` (
   `formPath` varchar(1000) DEFAULT NULL,
   `formType` varchar(100) DEFAULT NULL,
   `description` text,
   `formName` varchar(255) DEFAULT NULL,
   `owner` varchar(255) DEFAULT NULL,
   `enableAnonymousSave` varchar(45) DEFAULT NULL,
   `renderPath` varchar(1000) DEFAULT NULL,
   `nodeType` varchar(45) DEFAULT NULL,
   `charset` varchar(45) DEFAULT NULL,
   `userdataID` varchar(45) DEFAULT NULL,
   `status` varchar(45) DEFAULT NULL,
   `formmodel` varchar(45) DEFAULT NULL,
   `markedForDeletion` varchar(45) DEFAULT NULL,
   `showDorClass` varchar(255) DEFAULT NULL,
   `sling:resourceType` varchar(1000) DEFAULT NULL,
   `attachmentList` longtext,
   `draftID` varchar(45) DEFAULT NULL,
   `submitID` varchar(45) DEFAULT NULL,
   `id` varchar(60) NOT NULL,
   `profile` varchar(255) DEFAULT NULL,
   `submitUrl` varchar(1000) DEFAULT NULL,
   `xdpRef` varchar(1000) DEFAULT NULL,
   `agreementId` varchar(255) DEFAULT NULL,
   `nextSigners` varchar(255) DEFAULT NULL,
   `eSignStatus` varchar(45) DEFAULT NULL,
   `pendingSignID` varchar(45) DEFAULT NULL,
   `agreementDataId` varchar(255) DEFAULT NULL,
   `enablePortalSubmit` varchar(45) DEFAULT NULL,
   `submitType` varchar(45) DEFAULT NULL,
   `dataType` varchar(45) DEFAULT NULL,
   `jcr:lastModified` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`id`),
   UNIQUE KEY `ID_UNIQUE` (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   用于additionalmetadatable **的** SQL语句

   ```sql
   CREATE TABLE `additionalmetadatatable` (
   `value` text,
   `key` varchar(255) NOT NULL,
   `id` varchar(60) NOT NULL,
   PRIMARY KEY (`id`,`key`),
   CONSTRAINT 'additionalmetadatatable_fk' FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   注释表的&#x200B;**SQL语句**

   ```sql
   CREATE TABLE `commenttable` (
   `commentId` varchar(255) DEFAULT NULL,
   `comment` text DEFAULT NULL,
   `ID` varchar(255) DEFAULT NULL,
   `commentowner` varchar(255) DEFAULT NULL,
   `time` varchar(255) DEFAULT NULL);
   ```

1. 如果数据库模式中已有表（数据、元数据和可添加的additionalmetadatable），请执行以下更改表查询：

   用于更改数据表的&#x200B;**SQL语句**

   ```sql
   ALTER TABLE `data` CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   用于更改元数据表的&#x200B;**SQL语句**

   ```sql
   ALTER TABLE metadata add markedForDeletion varchar(45) DEFAULT NULL
   ```

   >[!NOTE]
   >
   >如果您已运行ALTER TABLE元数据添加查询，并且表中存在marketforDeletion列，则该查询会失败。

   ```sql
   ALTER TABLE metadata add agreementId varchar(255) DEFAULT NULL,
   add nextSigners varchar(255) DEFAULT NULL,
   add eSignStatus varchar(45) DEFAULT NULL,
   add pendingSignID varchar(45) DEFAULT NULL,
   add agreementDataId varchar(255) DEFAULT NULL,
   add enablePortalSubmit varchar(45) DEFAULT NULL,
   add submitType varchar(45) DEFAULT NULL,
   add dataType varchar(45) DEFAULT NULL;
   ```

   ```sql
   ALTER TABLE `metadata` CHANGE `formPath` `formPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formType` `formType` VARCHAR(100) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `description` `description` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formName` `formName` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `renderPath` `renderPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `showDorClass` `showDorClass` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `sling:resourceType` `sling:resourceType` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `profile` `profile` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `submitUrl` `submitUrl` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `xdpRef` `xdpRef` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   用于更改additionalmetadatable表的&#x200B;**SQL语句**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

现在已配置示例实施，您可以在将所有数据和元数据存储在数据库中时，使用该实施列出草稿和提交内容。 现在，让我们看一下示例中如何配置数据和元数据服务。

## 安装mysql-connector-java-5.1.39-bin.jar文件 {#install-mysql-connector-java-bin-jar-file}

在所有创作实例和发布实例上执行以下步骤，安装mysql-connector-java-5.1.39-bin.jar文件：

1. 导航到`https://'[server]:[port]'/system/console/depfinder`并搜索com.mysql.jdbc包。
1. 在“导出方式”列中，检查包是否由任何捆绑导出。

   如果包未由任何捆绑包导出，请继续。

1. 导航到`https://'[server]:[port]'/system/console/bundles`并单击&#x200B;**[!UICONTROL 安装/更新]**。
1. 单击&#x200B;**[!UICONTROL 选择文件]**&#x200B;并浏览以选择mysql-connector-java-5.1.39-bin.jar文件。 此外，选中&#x200B;**[!UICONTROL 启动包]**&#x200B;和&#x200B;**[!UICONTROL 刷新包]**&#x200B;复选框。
1. 单击&#x200B;**[!UICONTROL 安装或更新]**。 完成后，重新启动服务器。
1. （*仅限Windows*）关闭操作系统的系统防火墙。

>[!NOTE]
>
> 建议使用“Ctrl + C”命令重新启动SDK。 使用替代方法（例如，停止Java进程）重新启动AEM SDK可能会导致AEM开发环境不一致。

## 表单门户数据和元数据服务的示例代码 {#sample-code-for-forms-portal-data-and-metadata-service}

以下zip包含数据和元数据服务接口的`FormsPortalSampleDataServiceImpl`和`FormsPortalSampleMetadataServiceImpl`（实现类）。 此外，它包含编译上述实现类所需的所有类。

[获取文件](assets/sample_package.zip)

## 验证文件名的长度  {#verify-length-of-the-file-name}

Forms Portal的数据库实施使用其他元数据表。 该表具有基于表的键和ID列的复合主键。 MySQL允许主键长度不超过255个字符。 您可以使用以下客户端验证脚本来验证附加到文件小部件的文件名的长度。 在附加文件时运行验证。 当文件名大于150（包括扩展名）时，以下过程中提供的脚本将显示一条消息。 您可以修改脚本以检查其是否包含其他字符数。

执行以下步骤以创建[客户端库](/help/sites-developing/clientlibs.md)并使用脚本：

1. 登录到CRXDE并导航到/etc/clientlibs/
1. 创建&#x200B;**cq：ClientLibraryFolder**&#x200B;类型的节点，并提供该节点的名称。 例如：`validation`。

   单击&#x200B;**[!UICONTROL 全部保存]**。

1. 右键单击节点，单击&#x200B;**[!UICONTROL 创建新文件]**，然后创建扩展名为.txt的文件。 例如，`js.txt`将以下代码添加到新创建的.txt文件中，然后单击&#x200B;**[!UICONTROL 全部保存]**。

   ```javascript
   #base=util
    util.js
   ```

   在上述代码中，`util`是文件夹的名称，是`util`文件夹中文件的`util.js`名称。 `util`文件夹和`util.js`文件是在后续步骤中创建的。

1. 右键单击在步骤2中创建的`cq:ClientLibraryFolder`节点，选择创建>创建文件夹。 创建名为`util`的文件夹。 单击&#x200B;**[!UICONTROL 全部保存]**。 右键单击`util`文件夹，选择“创建”>“创建文件”。 创建名为`util.js`的文件。 单击&#x200B;**[!UICONTROL 全部保存]**。

1. 将以下代码添加到util.js文件，然后单击&#x200B;**[!UICONTROL 全部保存]**。 代码验证文件名的长度。

   ```javascript
   /*
    * ADOBE CONFIDENTIAL
    * ___________________
    *
    * Copyright 2016 Adobe Systems Incorporated
    * All Rights Reserved.
    *
    * NOTICE:  All information contained herein is, and remains
    * the property of Adobe Systems Incorporated and its suppliers,
    * if any.  The intellectual and technical concepts contained
    * herein are proprietary to Adobe Systems Incorporated and its
    * suppliers and may be covered by U.S. and Foreign Patents,
    * patents in process, and are protected by trade secret or copyright law.
    * Dissemination of this information or reproduction of this material
    * is strictly forbidden unless prior written permission is obtained
    * from Adobe Systems Incorporated.
    *
    */
   (function () {
       var connectWithGuideBridge = function (gb) {
           gb.connect(function () {
               //For first time load
               window.guideBridge.on("elementValueChanged" , function(event, payload) {
           var component = payload.target; // Field whose value has changed
                   if(component.name == 'fileAttachment' && component.parent) {
                       var fileItems = $('#'+payload.target.parent.id).find(".guide-fu-fileItem");
                       for (i = 0;i<fileItems.length;i++) {
                           var filename = $(fileItems[i]).find(".guide-fu-fileName").text();
                           //check whether it is previously attached file or a newly  attached one
                           if(filename.length > 150 && filename.indexOf("fp.attach.jsp") < 0) {
                               window.alert("filename is larger than 150 : "+filename);
                                $(fileItems[i]).find(".guide-fu-fileClose.close").click();
                           }
                       }
                   }
   
      });
           });
       };
   
       if (window.guideBridge) {
           connectWithGuideBridge(window.guideBridge);
       } else {
           window.addEventListener("bridgeInitializeStart", function (event) {
               connectWithGuideBridge(event.detail.guideBridge);
           });
       }
   })();
   ```

   >[!NOTE]
   >
   >该脚本用于现成的附件小部件组件。 如果您自定义了现成的附件小组件，则请更改上述脚本以合并相应的更改。

1. 将以下属性添加到在步骤2中创建的文件夹，然后单击&#x200B;**[!UICONTROL 全部保存]**。

   * **[!UICONTROL 名称：]**&#x200B;类别

   * **[!UICONTROL 类型：]**&#x200B;字符串

   * **[!UICONTROL 值：]** fp.validation

   * **[!UICONTROL 多选项：]**&#x200B;已启用

1. 导航到`/libs/fd/af/runtime/clientlibs/guideRuntime`并将`fp.validation`值附加到嵌入属性。

1. 导航到/libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA并将`fp.validation`值附加到嵌入属性。

   >[!NOTE]
   >
   >如果您使用的是自定义客户端库，而不是guideRuntime和guideRuntimeWithXfa客户端库，请使用类别名称将在此过程中创建的客户端库嵌入到运行时加载的自定义库中。

1. 单击&#x200B;**[!UICONTROL 全部保存。]**&#x200B;现在，当文件名大于150（包括扩展名）字符时，会显示消息。
