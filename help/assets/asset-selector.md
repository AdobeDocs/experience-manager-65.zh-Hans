---
title: 资源选择器
description: 了解如何使用资源选择器在Adobe Experience Manager Assets中搜索、筛选、浏览和获取资源的元数据。 还可了解如何自定义资产选择器界面。
contentOwner: Adobe
feature: Asset Management,Metadata,Search
role: User
hide: true
exl-id: c84ce84a-1e52-48fd-a16c-38c7769df9af
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---

# 资源选择器 {#asset-selector}

>[!NOTE]
>
>[资产选择器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-selector.html?lang=zh-Hans)在早期版本的[!DNL Experience Manager]中被称为[资产选取器](https://helpx.adobe.com/cn/experience-manager/6-2/assets/using/asset-picker.html)。

通过资源选择器，您可以在[!DNL Adobe Experience Manager] Assets中浏览、搜索和筛选资源。 您还可以获取使用资源选择器选择的资源的元数据。 要自定义资产选择器界面，您可以使用支持的请求参数启动该界面。 这些参数为特定方案设置资源选择器的上下文。

目前，您可以将请求参数`assettype` (*Image/Video/Text*)和选择`mode` (*Single/Multiple*)作为资产选择器的上下文信息传递，该上下文信息在整个选择过程中保持不变。

资源选择器使用HTML5 **Window.postMessage**&#x200B;消息将选定资源的数据发送给收件人。

资产选择器基于Granite的基础选取器词汇。 默认情况下，资产选择器在浏览模式下运行。 但是，您可以使用Omnisearch体验来应用过滤器，以优化对特定资产的搜索。

您可以将任何网页（无论它是否是CQ容器的一部分）与资产选择器(`https://[AEM_server]:[port]/aem/assetpicker.html`)集成。

## 上下文参数 {#contextual-parameters}

您可以在URL中传递以下请求参数，以在特定上下文中启动资产选择器：

| 名称 | 值 | 示例 | 用途 |
|---|---|---|---|
| 资源后缀(B) | 文件夹路径作为URL中的资源后缀：`http://localhost:4502/aem/`<br>`assetpicker.html/<folder_path>` | 要在选定特定文件夹（例如选定文件夹`/content/dam/we-retail/en/activities`）的情况下启动资产选择器，URL应采用以下形式： `http://localhost:4502/aem/assetpicker.html`<br>`/content/dam/we-retail/en/activities?assettype=images` | 如果在启动资产选择器时要求选择特定文件夹，请将其作为资源后缀传递。 |
| 模式 | 单个，多个 | `http://localhost:4502/aem/assetpicker.html`<br>`?mode=multiple` <br> `http://localhost:4502/aem/assetpicker.html`<br>`?mode=single` | 在多个模式下，您可以使用资产选择器同时选择多个资产。 |
| 对话框 | true， false | `http://localhost:4502/aem/assetpicker.html`<br>`?dialog=true` | 使用这些参数以Granite对话框形式打开资产选择器。 仅当通过Granite路径字段启动资产选择器，并将其配置为pickerSrc URL时，此选项才适用。 |
| 根 | `<folder_path>` | `http://localhost:4502/aem/`<br>`assetpicker.html?assettype=images`<br>`&root=/content/dam/we-retail/en/activities` | 使用此选项可指定资源选择器的根文件夹。 在这种情况下，资产选择器允许您仅选择根文件夹下的子资产（直接/间接）。 |
| 视图模式 | 搜索 |  | 要在搜索模式下启动资产选择器，请使用assettype和mimetype参数。 |
| assettype (S) | 图像、文档、多媒体、存档 | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives`</li> | 使用此选项可根据传递的值筛选资源类型。 |
| mimetype | 资产的mimetype (`/jcr:content/metadata/dc:format`)（也支持通配符） | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=image/png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&?mimetype=*png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=*presentation`</li>  <li>`http://localhost:4502/aem/assetpicker?viewmode=search&mimetype=*presentation&mimetype=*png`</li></ul> | 使用它根据MIME类型筛选资源 |

## 使用资源选择器 {#using-the-asset-selector}

1. 要访问资产选择器界面，请转到`https://[AEM_server]:[port]/aem/assetpicker`。
1. 导航到所需的文件夹，然后选择一个或多个资产。

   ![chlimage_1-441](assets/chlimage_1-441.png)

   或者，您可以从OmniSearch框中搜索所需的资产，然后选择该资产。

   ![chlimage_1-442](assets/chlimage_1-442.png)

   如果您使用OmniSearch框搜索资产，则可以从&#x200B;**[!UICONTROL 筛选器]**&#x200B;窗格中选择各种筛选器以优化您的搜索。

   ![chlimage_1-443](assets/chlimage_1-443.png)

1. 单击工具栏中的&#x200B;**[!UICONTROL 选择]**。

>[!MORELIKETHIS]
>
>* AEM as a Cloud Service中的[微前端资源选择器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-selector.html?lang=zh-Hans)
