---
title: 全局文档存储目录
seo-title: 全局文档存储目录
description: 全局文档存储(GDS)目录是用于存储进程中使用的长寿命文件的目录。
seo-description: 全局文档存储(GDS)目录是用于存储进程中使用的长寿命文件的目录。
uuid: 7681672c-a0dc-4445-8004-1b1e2ed3d301
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a33b8834-6e39-47eb-a53b-0982d32e80ad
translation-type: tm+mt
source-git-commit: 215ba1cb3e98954418b844849c812c9ba6cf572b

---


# 全局文档存储目录{#global-document-storage-directory}

全 *局文档存储(GDS)* (Global Document Storage, GDS)目录是用于存储进程中使用的长寿命文件的目录。 这些文件包括PDF、策略和表单模板。 长期使用的文件是许多AEM表单部署的整体状态的关键部分。 如果某些或所有长期文档丢失或损坏，表单服务器可能会变得不稳定。 异步作业调用的输入文档也存储在GDS目录中，并且必须可用于处理请求。 务必考虑承载GDS目录的文件系统的可靠性。 根据您的服务质量和服务级别需要，使用独立磁盘冗余阵列(RAID)或其他技术。

长期使用的文件可能包含敏感的用户信息。 当通过使用AEM表单API或用户界面访问此信息时，可能需要特殊凭据。 通过操作系统正确保护GDS目录非常重要。 只有用于运行应用程序服务器的管理员帐户才应具有对GDS目录的读／写访问权限。

除了为GDS选择安全、高度可用的目录外，您还可以选择在数据库中启用文档存储。 请注意，即使将AEM表单数据库用于文档存储，AEM表单仍需要GDS目录。 (请参 [阅将数据库用于文档存储时的备份选项](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage)。)

AEM表单应用程序数据驻留在GDS目录和AEM表单数据库中。 下表介绍了数据及其位置。

<table>
 <thead>
  <tr>
   <th><p>AEM表单数据</p></th>
   <th><p>数据库</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>应用程序数据（用户、角色、进程、策略、端点、事件等）。</p></td>
   <td><p>是</p></td>
   <td><p>否</p></td>
  </tr>
  <tr>
   <td><p>已部署的服务容器</p></td>
   <td><p>是</p></td>
   <td><p>否</p></td>
  </tr>
  <tr>
   <td><p>文档管理器 </p></td>
   <td><p>否</p></td>
   <td><p>是</p></td>
  </tr>
  <tr>
   <td><p>表单存储库</p></td>
   <td><p>是</p></td>
   <td><p>否</p></td>
  </tr>
  <tr>
   <td><p>系统配置</p></td>
   <td><p>是</p></td>
   <td><p>否</p></td>
  </tr>
  <tr>
   <td><p>监视文件夹</p></td>
   <td><p>否</p></td>
   <td><p>是</p></td>
  </tr>
 </tbody>
</table>

## 配置GDS目录 {#configuring-the-gds-directory}

在AEM表单安装过程中，可以手动配置GDS目录的位置。 如果安装过程中位置设置保持为空，则位置默认为应用程序服务器安装下的目录，如下所示：

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/[server]/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/[server]/DocumentStorage`

## 更改默认GDS位置 {#change-the-default-gds-location}

在AEM表单安装完成后，您可以在管理控制台中更改GDS位置。 您必须手动重新定位数据以完成该过程。

>[!NOTE]
>
>以下方式迁移数据，否则会发生数据丢失。

1. 登录到管理控制台，然后单击设置>核心系统设置>配置。
1. 在“全局文档存储目录”框中，输入新GDS目录的完整路径，然后单击“确定”。
1. 立即关闭应用程序服务器。
1. 将所有文件从旧GDS目录移至新位置，同时保留内部目录结构。
1. 重新启动应用程序服务器。

## 关于部署文件 {#about-deployment-files}

AEM表单由两种类型的部署文件组成，即服务容器和Java 2 Platform, Enterprise Edition(J2EE)EAR文件。 EAR文件由包含AEM表单核心功能的标准J2EE应用程序捆绑包组成。 特定于应用程序服务器的EAR文件如下：

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

实施AEM表单涉及将组合的EAR文件和支持文件部署到计划运行AEM表单解决方案的应用程序服务器。 如果您配置并组装了多个模块，可部署的模块将打包在可部署的EAR文件中。 要部署这些文件，请将它们复制到 *[appserver主]*&#x200B;页\server\all\deploy directory。

模块和AEM表单存档文件打包在JAR文件中。 由于它们不是J2EE类型文件，因此不会部署到应用程序服务器。 而是将它们复制到GDS目录中，并且对其位置的引用存储在AEM表单数据库中。 因此，必须在群集的所有节点之间共享GDS目录。 所有节点都必须有权访问DSC的中央存储目录。

>[!NOTE]
>
>在部署服务容器之前，请确保已创建并配置GDS目录。 (请参 [阅配置GDS目录](global-document-storage-directory.md#configuring-the-gds-directory))

