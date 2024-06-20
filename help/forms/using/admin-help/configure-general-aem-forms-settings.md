---
title: AEM Forms常规设置
description: 了解如何在管理控制台中配置有助于提高系统性能的“核心配置”页面设置。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: e1519477-b5a8-4947-8597-26b945a3b819
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 0%

---

# AEM Forms常规设置 {#general-aem-forms-settings}

管理控制台中的“核心配置”页面提供了有助于提高系统性能的设置。 配置或更新这些设置后，重新启动应用程序服务器。

>[!NOTE]
>
> 建议使用“Ctrl + C”命令重新启动SDK。 使用替代方法（例如，停止Java进程）重新启动AEM SDK可能会导致AEM开发环境不一致。

有关启用安全备份模式的信息，请参见 [启用和禁用安全备份模式](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode).


>[!NOTE]
>
>临时目录中的文件和全局文档存储(GDS)根目录中的长期文档可能包含敏感的用户信息，例如使用API或用户界面访问时需要特殊凭据的信息。 因此，必须使用操作系统可用的任何方法来正确保护此目录。 建议只有用于运行应用程序服务器的操作系统帐户才具有此目录的读写访问权限。


1. 在管理控制台中，选择 **[!UICONTROL “设置”>“核心系统设置”>“配置”]**.
1. 在Core Configurations页面上，根据需要更改选项并选择 **[!UICONTROL 确定]**. 有关选项的详细信息，请参阅 [核心配置选项](configure-general-aem-forms-settings.md#core-configurations-options).


## 核心配置选项 {#core-configurations-options}

**临时目录的位置** AEM表单将创建产品临时文件的目录路径。 如果此设置的值为空，则该位置默认为系统临时目录。 确保临时目录是可写文件夹。

>[!NOTE]
>
>确保临时目录位于本地文件系统中。 AEM forms不支持远程位置的临时目录。

**全局文档存储根目录** *ndash；全局文档存储(GDS)根目录用于以下目的：

* 存储长期文档。 长效文档没有过期时间，并且会一直保留，直到被删除(例如，工作流进程中使用的PDF文件)。 长寿命文档是整个系统状态的重要组成部分。 如果其中的部分或全部文档丢失或损坏，Forms服务器可能会变得不稳定。 因此，将此目录存储在RAID设备上非常重要。
* 存储处理过程中所需的临时文档。

>[!NOTE]
>
>您还可以在AEM表单数据库中启用文档存储。 但是，使用GDS时，系统性能会更好。

* 在群集中的节点之间传输文档。 如果在群集环境中运行AEM表单，则必须可从群集中的所有节点访问此目录。
* 接收来自远程API调用的传入参数。

如果未指定GDS根目录，则该目录默认为应用程序服务器目录：

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>更改GDS根目录设置的值时应特别小心。 GDS目录用于存储进程中使用的长期文件以及关键的AEM Forms产品组件。 更改GDS目录的位置是一项重大的系统更改。 错误配置GDS目录的位置将导致AEM表单无法运行，并且可能需要完全重新安装AEM表单。 如果为GDS目录指定了新位置，则需要关闭应用程序服务器并迁移数据，然后才能重新启动服务器。 系统管理员必须将所有文件从旧位置移动到新位置，但保留内部目录结构。

>[!NOTE]
>
>不要为temp目录和GDS目录指定相同的目录。

有关GDS目录的其他信息，请参见 [准备安装AEM表单（单服务器）](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Adobe服务器字体目录的位置** *ndash；键入包含Adobe服务器字体的目录的路径。 这些字体随AEM表单一起安装。 这些字体的默认位置为 [aem-forms根]/fonts目录。 如果无法访问此目录，则可以将字体复制到其他位置，然后使用此设置指定新位置。

**Customer Fonts目录的位置** *ndash；键入包含要使用的其他字体的目录的路径。

***注意&#x200B;**：从Windows系统字体缓存中选取字体，需要重新启动系统才能更新缓存。 指定Customer font目录后，请确保重新启动安装了AEM表单的系统。*

**System Fonts目录的位置** *ndash；键入操作系统提供的fonts目录的路径。 可以添加多个目录，以分号分隔 **；**.

**数据服务配置文件的位置** *ndash；指定services-config.xml文件的位置。 默认情况下，此文件嵌入到adobe-core-appserver.ear文件中，且用户无法访问。 默认services-config.xml文件的副本位于 [aem-forms根]\sdk\misc\DataServices\Server-Configuration. 如果更改了此文件并移动了它，请在此字段中键入新位置。

数据服务配置文件允许自定义数据服务设置，如身份验证类型和调试输出。

默认情况下，此设置为空。

**默认文档最大内联大小（字节）** *ndash；在各种AEM表单组件之间传递文档时内存中保留的最大字节数。 使用此设置进行性能优化。 小于此数字的文档存储在内存中，并保留在数据库中。 超过此最大值的文档存储在硬盘上。

此设置是必需的。 默认值为65536字节。

**默认文档处理超时（秒）** *ndash；在各种AEM表单组件之间传递的文档被视为活动状态的最长时间（以秒为单位）。 在此时间过后，将删除用于存储此文档的文件。 使用此设置控制磁盘空间的使用。

此设置是必需的。 默认值为600秒。

**文档整理间隔（秒）** *ndash；尝试删除不再需要的文件以及用于在服务之间传递文档数据之间的间隔时间（以秒为单位）。

此设置是必需的。 默认值为30秒。

**启用FIPS** *ndash；选择此选项可启用FIPS模式。 联邦信息处理标准(FIPS) 140-2是美国政府定义的加密标准。 在FIPS模式下运行时，AEM Forms会使用RSA BSAFE Crypto-C 2.1加密模块限制对FIPS 140-2认可算法的数据保护。

FIPS模式不支持Adobe Acrobat® 7.0之前的版本中使用的加密算法。如果启用了FIPS模式，并且您使用加密服务，使用兼容性级别设置为Acrobat 5的密码对PDF进行加密，则加密尝试将失败，并出现错误。

通常，启用FIPS时，Assembler服务不会对任何文档应用密码加密。 如果尝试此操作，则会引发FIPSModeException，指示“在FIPS模式下不允许密码加密”。 此外，当基础文档进行了密码加密时，FIPS模式中不支持文档描述XML (DDX) PDFsFromBookmarks元素。

>[!NOTE]
>
>AEM forms软件不会验证代码以确保FIPS兼容性。 它提供了FIPS操作模式，以便将FIPS批准的算法用于来自FIPS批准的库(RSA)的加密服务。

**启用WSDL** *ndash；选择此选项可为AEM表单中的所有服务启用Web服务定义语言(WSDL)生成。

在开发环境中启用此选项，开发人员可在开发环境中使用WSDL生成来构建其客户端应用程序。 您可以选择在生产环境中禁用WSDL生成，以避免公开服务的内部详细信息。

**在数据库中启用文档存储** *ndash；选择此选项可在AEM表单数据库中存储长期文档。 启用此选项不会删除对GDS目录的需要。 但是，选择此选项可以简化AEM表单备份。 如果只使用GDS ，则备份包括将AEM formsAEM forms系统置于备份模式，然后完成数据库和GDS的备份。 如果选择数据库选项，则备份包括完成新安装的数据库备份，或完成数据库备份和GDS的一次性升级备份。 与仅使用GDS的配置相比，清除作业和数据可能需要对数据库进行额外管理。 （请参阅将数据库用于文档存储时的备份选项。）

**启用DSC调用统计信息** *ndash；选择此选项时，AEM Forms将跟踪调用统计信息，例如调用次数、调用所用时间和调用中的错误数。 此信息存储在JMX Bean中，以便您可以使用Java™ JConsole或第三方软件来查看统计信息。 如果您不想查看这些统计信息，请取消选择此选项以提高AEM表单性能。

**启用RDS** *ndash；选择此选项可在AEM表单中启用远程开发服务(RDS) servlet。 启用此选项后，客户端工具可以与数据服务进行交互，执行部署或取消部署模型等操作，以创建目标和端点，或查找已将哪些模型部署到端点。 默认情况下，不选中此选项。

**允许非安全RDS请求** *ndash；选择此选项时，RDS请求不需要使用https。 默认情况下，未选中此选项，所有与数据服务的通信都必须是https请求。

**允许从Flex应用程序上传不安全的文档** *ndash；用于将文档从AdobeFlex®应用程序上传到AEM表单的文件上传servlet要求用户在上传文档之前必须经过身份验证和授权。 必须为用户分配文档上载应用程序用户角色或包含文档上载权限的其他角色。 这有助于防止未经授权的用户将文档上传到AEM Forms服务器。 如果要在开发环境中禁用此安全功能，或者要与以前版本的AEM表单向后兼容，请选择此选项。 默认情况下，不选中此选项。 有关详细信息，请参阅使用AEM表单进行编程中的“使用AEM表单远程处理调用AEM表单”。

**允许从Java SDK应用程序上传不安全的文档** *ndash； HTTP DocumentManager上传必须安全。 默认情况下，HTTP上传要求用户在上传文档之前进行身份验证和授权。 必须为用户分配服务用户角色或包含服务调用权限的其他角色。 这有助于防止未经授权的用户将文档上传到Forms服务器。 如果要在开发环境中禁用此安全功能、要与以前版本的AEM表单向后兼容，或要基于防火墙设置来禁用此安全功能，请选择此选项。 默认情况下，不选中此选项。 有关详细信息，请参阅使用AEM表单进行编程中的“使用Java API调用AEM表单”。
