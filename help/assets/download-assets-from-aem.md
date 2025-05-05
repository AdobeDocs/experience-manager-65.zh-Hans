---
title: 下载资源
description: 了解如何从 [!DNL Adobe Experience Manager] 下载资产，以及启用或禁用下载功能。
contentOwner: AG
role: User
feature: Asset Management,Asset Distribution
exl-id: 6bda9e52-5a6e-446e-99c7-96793482c190
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 2%

---

# 从[!DNL Adobe Experience Manager]下载资源 {#download-assets-from-aem}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/download-assets-from-aem.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

您可以下载资源，包括静态和动态演绎版。 或者，您可以直接从[!DNL Adobe Experience Manager Assets]发送带有资产链接的电子邮件。 下载的资源捆绑在一个ZIP文件中。 对于导出作业，压缩的ZIP文件的最大文件大小为1 GB。 每个导出作业最多允许500个总资产。

>[!NOTE]
>
>在`/var/dam/share`位置具有读取权限的任何用户都可以访问电子邮件中共享的下载链接。
>
>任何对`/var/dam/jobs/download`位置具有读取权限的用户都可以下载资产。
>
>无法下载资源类型 — 图像集、旋转集、混合媒体集和轮播集。

<!--
OLD content of the above NOTE, changed wrt CQDOC-18661.
>The email recipients must be members of the `dam-users` group to access the ZIP download link in the email message.
>
-->

**要下载资源，请执行以下步骤：**

1. 单击左上角的徽标。 在左边栏中，单击&#x200B;**[!UICONTROL 导航]**。
1. 在[!UICONTROL 导航]页面上，单击&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 文件]**。
1. 导航到包含要下载的资源的文件夹。
1. 选择文件夹或文件夹中的一个或多个资源。
1. 在工具栏上，单击&#x200B;**[!UICONTROL 下载]**。
1. 在下载对话框中，选择所需的下载选项。

   | 导出或下载选项 | 描述 |
   |---|---|
   | **[!UICONTROL 为每个资产创建单独的文件夹]** | 选择此选项可将下载的每个资产（包括嵌套在资产父文件夹下的子文件夹中的资产）包含到本地计算机上的一个文件夹中。 如果未选择此选项，则默认情况下会忽略文件夹层次结构，并且所有资产都下载到本地计算机上的一个文件夹中。 |
   | **[!UICONTROL 电子邮件]** | 会向用户发送电子邮件通知。 标准电子邮件模板可在以下位置使用：<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> 您可以在以下位置找到部署期间自定义的模板： <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul>您可以在以下位置存储特定于租户的自定义模板：<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> |
   | **[!UICONTROL 资源]** | 选择此选项可下载原始格式的资源，而无需任何演绎版。<br>如果原始资产具有子资产，则子资产选项可用。 |
   | **[!UICONTROL 节目]** | 演绎版是资产的二进制表示形式。 Assets具有主要表示形式 — 已上传文件的主要表示形式。 它们可以有任意数量的呈现。 <br>使用此选项，您可以选择想要下载的演绎版。 可用的演绎版取决于您选择的资源。 如果资产具有任何演绎版，则该选项可用。 |
   | **[!UICONTROL 智能裁剪]** | 选择此选项可从AEM中下载所选资源的所有智能裁剪演绎版。 将创建包含智能裁剪呈现的zip文件并下载到本地计算机。 |
   | **[!UICONTROL 动态演绎版]** | 选择此选项可实时生成一系列替代演绎版。 选择此选项时，您还可以通过从[图像预设](image-presets.md)列表中选择来选择要动态创建的演绎版。 <br>此外，您还可以选择大小和度量单位、格式、颜色空间、分辨率以及任何可选的图像修饰符（如反转图像）。 仅当您启用了[!DNL Dynamic Media]时，该选项才可用。 |

1. 在该对话框中，单击&#x200B;**[!UICONTROL 下载]**。

选择要下载的文件夹时，将下载该文件夹下的完整资源层次结构。 要将您下载的每个资源（包括嵌套在父文件夹下的子文件夹中的资源）包含在单个文件夹中，请选择&#x200B;**[!UICONTROL 为每个资源创建单独的文件夹]**。

## 启用资源下载servlet {#enable-asset-download-servlet}

[!DNL Experience Manager]中的默认servlet允许经过身份验证的用户发出任意大型的并发下载请求，以创建对他们可见的资产的ZIP文件，这会使服务器和网络过载。 为了减少此功能导致的潜在DoS风险，默认情况下为发布实例禁用`AssetDownloadServlet` OSGi组件。

要允许从DAM下载资产，例如在使用Asset Share Commons或其他类似门户的实施时，请通过OSGi配置手动启用servlet。 Adobe建议将允许的下载大小设置得尽可能小，而不影响日常下载要求。 高值可能会影响性能。

1. 使用针对发布运行模式(`config.publish`)的命名约定创建文件夹： `/apps/<your-app-name>/config.publish`。 要定义运行模式的配置属性，请参阅[运行模式](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode)。
1. 在配置文件夹中，创建名为`com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`的`nt:file`类型的文件。
1. 使用以下内容填充`com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`。 将下载的最大大小（以字节为单位）设置为`asset.download.prezip.maxcontentsize`的值。 下面的示例将ZIP下载的最大大小配置为不超过100 kb。

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

默认情况下，对于`GET`个下载文件的请求，[!DNL Experience Manager]对ZIP存档的下载大小强制限制50 MB。 通过`POST`请求或用户界面启动的下载不受此限制的影响。

## 禁用资源下载servlet {#disable-asset-download-servlet}

通过更新Dispatcher配置以阻止任何资源下载请求，可以在[!DNL Experience Manager]个Publish实例上禁用`Asset Download Servlet`。 也可以直接通过OSGi控制台手动禁用servlet。

1. 要通过Dispatcher配置阻止资源下载请求，请编辑`dispatcher.any`配置并将规则添加到[筛选条件部分](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hans#defining-a-filter)。`/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. 要在Publish实例上禁用OSGi组件，请访问位于`http://[aem_server]:[port]/system/console/components`的OSGi控制台。 找到`com.day.cq.dam.core.impl.servlet.AssetDownloadServlet`并单击&#x200B;**[!UICONTROL 禁用]**。

>[!MORELIKETHIS]
>
>* [使用Brand Portal下载资源](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html?lang=zh-Hans)
>* [下载受DRM保护的资产](drm.md)。
>* [在Win或Mac桌面上使用Experience Manager桌面应用程序下载资源](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=zh-Hans#download-assets)。
>* [使用支持的Assets应用程序中的AdobeAdobe Creative Cloud链接下载资源](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html)。
