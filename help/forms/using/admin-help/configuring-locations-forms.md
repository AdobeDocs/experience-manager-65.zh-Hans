---
title: 为Forms配置位置
description: 了解如何配置AEM表单的位置。 可以指定属性的文件位置、表单的位置、种子PDF文件和高速缓存位置。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0d9eb7fe-28a6-444e-957d-023687158c61
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 1%

---

# 为Forms配置位置 {#configuring-locations-for-forms}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

您可以指定属性的URL、URI和文件位置，例如Web根目录、要检索的表单的位置、PDForm转换中使用的种子PDF文件以及缓存位置。

1. 在管理控制台中，单击服务> Forms。
1. 在“位置”下，指定相应的选项。 这些选项如下所述。
1. 单击“保存”。

## 位置设置 {#locations-settings}

**基本URL：**&#x200B;表单资源（如图像和脚本）所在的基本URL。 对于包含外部依赖项（如图像或脚本）的HREF引用的HTML转换，需要此值。 xfasubset.js就是一个此类脚本，HTML表单需要该脚本来执行XFA智能。 此值必须是内容根URI的HTTP等效值。

>[!NOTE]
>
>基本URL仅支持HTTP或存储库协议。 它不支持file:///之类的协议。 如果您需要访问资源（如自定义CSS或数字签名URI），请使用相应的API参数值指定绝对位置。

当依赖关系路径为绝对路径时，将忽略基本URL值。 否则，依赖关系路径将与基本URL相结合。

默认值为空字符串。

以下示例指向相同的内容（使用内容根URI和基本URL）：

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**FS Web根URI：** Forms Web应用程序的URL。 如果将Forms Web应用程序和客户端应用程序部署在同一应用程序服务器上；使用了Forms API Web根URL，则可以将此框留空。

如果Forms Web应用程序和客户端应用程序未部署到同一应用程序服务器，请在此框中提供Forms Web应用程序的URL，如以下示例所示：

`https://<host name>:<port>/FormServer`

其中`host name`和`port`是承载Forms Web应用程序的服务器的服务器名称和端口号。

默认值为空字符串。

**Web根URI：**&#x200B;应用程序的Web根。 该值会与通过AEM forms SDK指定的sTargetURL参数（以相对形式提供sTargetURL时）相结合，来构造访问特定于应用程序的Web内容的绝对URL。

默认值为空字符串。

**内容根URI：**&#x200B;从中检索表单的URI或绝对位置。 此值与sFormQuery参数（通过API指定）相结合，构建检索到的表单的绝对路径。 此值可引用可使用HTTP访问的目录或Web位置。

默认值为空字符串。

**XCI配置URI：**&#x200B;找到用于渲染的XCI文件的相对或绝对位置。 对于相对值，假定XCI文件驻留在可部署的AEM Forms EAR文件中。

默认值为 `com/adobe/formServer/PA/pa.xci`。

**字体映射URI：**&#x200B;字体映射文件的相对或绝对位置。 对于相对值，假定此文件位于可部署的AEM Forms EAR文件中。

font-mapping文件用于为表单中的HTML转换创建自定义字体映射，因此允许您指定在客户端计算机上没有可用的字体时将替换的字体。

默认值为 `com/adobe/formServer/client-font-map.properties`。

以下条目是字体映射文件中一个条目的示例：

`Arial=Arial,Helvetica,sans-serif`

**种子PDF文件：**&#x200B;在PDFForm转换中用于优化投放的初始PDF文件。 种子PDF文件指定附加到表单设计和数据的自定义PDF文件（仅包含XFA流、图像和字体资源）。 表单由Acrobat 7或更高版本渲染，并适用于PDForm转换。

默认值为空字符串。

**缓存位置：**&#x200B;指定Forms磁盘缓存的位置。 更改此设置时，将重置当前位置的所有现有缓存信息，并在新位置创建一个新缓存。 选择以下选项之一：

**默认位置：**&#x200B;这是默认选项。 如果选择该选项，则会在依赖于您正在使用的应用程序服务器的位置创建缓存：

* **JBoss：**&#x200B;[JBoss主页]\server\[安装类型]\svcdata\FormServer\Cache
* **WebLogic：** [WebLogic主页]\user_projects\domains\[aem-forms域名]\adobe\[Forms服务器名称]\FormServer\Cache
* **WebSphere：** [IBM主页]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**LC Temp目录：**&#x200B;缓存在AEM Forms临时目录的子目录中创建，该目录在管理控制台中的“设置”>“核心系统设置”>“配置”>“临时目录的位置”下指定。 该子目录名为adobeform_[服务器名称]。

>[!NOTE]
>
>如果您使用临时清理实用程序，虽然删除这些目录不会影响功能，但在创建新缓存之前，可能会在短时间内显着影响性能。 为避免出现此问题，在清除AEM forms临时目录时，请勿删除这些目录。
