---
title: 组织您的数字资产
description: 使用Experience Manager整理您的数字资源、图像、文件、文件夹等。
contentOwner: AG
role: User
feature: Asset Management,Search
exl-id: d6f815b5-e4fc-4f8c-a6c1-9e50035ab9f2
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 2%

---

# 组织您的数字资产 {#organize-digital-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| Adobe Experience Manager (AEM)as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/organize-assets.html?lang=en) |
| AEM 6.5 | 本文 |

Microsoft®Office和PDF文档的所有数字资源、元数据和内容都将进行提取并使其可搜索。 搜索允许对资产进行复杂的筛选，并完全尊重适当的权限。 数字资产管理中的元数据详细介绍了元数据。

[!DNL Experience Manager Assets] 支持多种内容组织方式。 您可以使用文件夹以层级方式组织它们，也可以使用标签（例如）以无序、临时方式组织它们。 用户可以在DAM资产编辑器中编辑显示子资产、演绎版和元数据的标记。

## 在文件夹中组织资源 {#organize-using-folders}

组织资源的最基本方法是将这些资源保存在文件夹中。 这类似于在本地文件系统的文件夹中组织文件。 有关如何创建和管理文件夹的详细信息，请参阅 [管理资源](manage-assets.md). 如何命名文件和文件夹、如何排列子文件夹以及如何处理这些文件夹中的文件可能会对这些资源的处理方式产生重大影响。 通过使用一致且适用的文件和文件夹命名策略以及良好的元数据做法，您可以充分利用数字资源存储库。

* 通常，您的数字资产存储库会一直不断增长。 因此，在内容创建周期早期将元数据的使用、文件夹结构和文件命名正规化非常重要。
* 仅使用文件夹为您的数字资产强制实施一致的存储结构。 此一致性可帮助您的流程更好地管理您的资产。 例如，将资源置于以下类型的文件夹中可以帮助您使用适当的文件夹 [用于资产处理的配置文件](processing-profiles.md)：

   * **开发文件夹**：包含您当前正在处理的数字资产。
   * **客户端文件夹**：包含基于客户端或项目名称的数字资源。
   * **主文件夹**：包含原始的源数字资源。
   * **节目文件夹**：包含原始源数字资产的演绎版和副本。
   * **文件大小文件夹**：包含基于小型、中型或大型文件大小的数字资源。
   * **暂存文件夹**：包含准备在网站上实时发布的数字资产。
   * **MIME类型文件夹**：包含特定于MIME类型的数字资产，例如图像、文档和多媒体。
   * **存档文件夹**：包含已弃用的数字资产。
   * **基于日期的文件夹**：包含基于创建日期或上次修改日期的数字资源。

* 创建不太可能更改的文件夹的目录，以便任何自定义或自动化均可继续工作。 例如，分配的处理配置文件将继续工作。
* 如果资产已发布，则使用 [!DNL Experience Manager] 要将资产移动到其他文件夹并从其新位置重新发布，原始发布的资产位置以及新重新发布的资产仍然可用。 然而，最初发布的资产是 *丢失* 到 [!DNL Experience Manager] 和无法取消发布。 因此，作为最佳实践，首先取消发布资产，然后将其移动到其他文件夹。

## 使用标记组织资源 {#use-tags-to-organize-assets}

将标记用作元数据时，您可以轻松搜索资源，使用搜索结果创建收藏集，提高某些资源的搜索排名，以及使用Adobe Sensei的人工智能算法发现资源。

[!DNL Adobe Experience Manager Assets] 使用自学习算法创建具有高度描述性的标记，让您只需单击几下即可找到所需的资产。 智能标记使用Adobe的人工智能和机器学习框架Adobe Sensei，该框架经过培训可以识别标准标签和业务特定标签，并将其应用于图像。 智能标记还可以识别内容、单个单词或短语，并自动将描述性标记应用于资产

有关更多信息，请参阅以下文章：

* [关于Experience Manager中的标记](/help/sites-authoring/tags.md)
* [编辑资源元数据](metadata.md)
* [资产中的增强型智能标记](enhanced-smart-tags.md)

## 组织为收藏集 {#organize-as-collections}

在中使用资产收藏集 [!DNL Experience Manager Assets]，您可以简化在用户之间创建、编辑和共享资源的功能。 根据您的使用方式创建多种类型的收藏集，包括包含资产、文件夹和收藏集的静态引用列表的收藏集，以及根据搜索条件拉入资产的收藏集。 您还可以使用不同位置的资源创建收藏集，并与具有不同访问级别、查看和编辑权限的多个用户共享这些收藏集。

有关更多信息，请参阅 [管理收藏集](manage-collections.md).

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## 组织资源以使用配置文件 {#organize-to-use-profiles}

处理配置文件包含 [!DNL Assets] 处理应用于上传到预定义文件夹的资源的命令。 配置文件用于自动处理文件夹的内容或最新上传的资产。 您可以使用用户档案更好地组织资源。

标准化元数据使用、文件命名和文件夹结构可确保随着数字资产池的增长，您可以更精确和一致地将处理配置文件应用到文件夹。

>[!MORELIKETHIS]
>
>* [用于处理元数据、图像和视频的配置文件](processing-profiles.md).
>* [元数据配置文件](/help/assets/metadata-config.md#metadata-profiles).
>* [视频配置文件](video-profiles.md).
>* [Dynamic Media图像配置文件](image-profiles.md).
