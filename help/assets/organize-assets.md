---
title: 组织您的数字资产
description: 使用Experience Manager整理数字资产、图像、文件、文件夹等。
contentOwner: AG
role: User
feature: Asset Management,Search
exl-id: d6f815b5-e4fc-4f8c-a6c1-9e50035ab9f2
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 2%

---

# 组织您的数字资产 {#organize-digital-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/organize-assets.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/organize-assets.html?lang=en) |

Microsoft Office和PDF文档的所有数字资产、元数据和内容都被提取并可搜索。 搜索允许对资产进行复杂的筛选，并完全尊重正确的权限。 在数字资产管理的元数据中，元数据有详细的介绍。

[!DNL Experience Manager Assets] 支持多种内容组织方式。 您可以使用文件夹以分层方式组织它们，或者使用例如标记以无序、临时的方式组织它们。 用户可以在DAM资产编辑器中编辑标记，其中显示子资产、演绎版和元数据。

## 在文件夹中组织资产 {#organize-using-folders}

组织资产的最基本方式是将这些资产保存在文件夹中。 它类似于在本地文件系统的文件夹中组织文件。 有关如何创建和管理文件夹的更多信息，请参阅 [管理资产](manage-assets.md). 如何命名文件和文件夹、如何排列子文件夹以及如何处理这些文件夹中的文件，可能会对这些资产的处理方式产生重大影响。 通过使用一致且适当的文件和文件夹命名策略以及良好的元数据实践，您可以充分利用数字资产存储库。

* 在大多数情况下，您的数字资产存储库始终在增长。 因此，在内容创建周期的早期，务必要正规化元数据的使用、文件夹结构和文件命名。
* 仅使用文件夹来为数字资产强制实施一致的存储结构。 此一致性有助于您的流程和更好地管理资产。 例如，放置在以下类型文件夹中的资产可以帮助您使用适当的 [用于资产处理的配置文件](processing-profiles.md):

   * **开发文件夹**:包含您当前正在处理的数字资产。
   * **客户端文件夹**:包含基于客户或项目名称的数字资产。
   * **主文件夹**:包含原始的源数字资产。
   * **演绎版文件夹**:包含原始源数字资产的演绎版和副本。
   * **文件大小文件夹**:包含基于小、中或大文件大小的数字资产。
   * **暂存文件夹**:包含已准备好在您的网站上实时发布的数字资产。
   * **MIME类型文件夹**:包含特定于MIME类型（如图像、文档和多媒体）的数字资产。
   * **存档文件夹**:包含已停用的数字资产。
   * **基于日期的文件夹**:包含基于创建日期或上次修改日期的数字资产。

* 创建不太可能更改的文件夹目录，以便任何自定义或自动操作都可以继续运行。 例如，分配的处理配置文件可继续工作。
* 如果资产已发布，则您可以使用 [!DNL Experience Manager] 要将资产移动到其他文件夹并从新位置重新发布，原始发布的资产位置以及新重新发布的资产仍然可用。 但是，原始发布的资产是 *丢失* to [!DNL Experience Manager] 和无法取消发布。 因此，作为最佳实践，请先取消发布资产，然后将其移动到其他文件夹。

## 使用标记组织资产 {#use-tags-to-organize-assets}

使用标记作为元数据，您可以轻松搜索资产、使用搜索结果创建收藏集、提升某些资产的搜索排名，以及利用Adobe Sensei的AI算法进行资产发现。

[!DNL Adobe Experience Manager Assets] 使用自学算法创建高度描述性的标记，以便您只需单击几下即可找到正确的资产。 智能标记使用Adobe Sensei，这是我们的人工智能和机器学习框架，经过培训后，该框架可识别标准标记和特定于业务的标记并将其应用于图像。 智能标记还可以识别内容、单个词或短语，并自动将描述性标记应用于资产

有关更多信息，请参阅以下文章：

* [关于Experience Manager中的标记](/help/sites-authoring/tags.md)
* [编辑资产元数据](metadata.md)
* [资产中增强的智能标记](enhanced-smart-tags.md)

## 组织为收藏集 {#organize-as-collections}

将资产收藏集放在 [!DNL Experience Manager Assets]，您可以简化在用户之间创建、编辑和共享资产的功能。 根据您使用收藏集的方式创建多种类型的收藏集，包括包含资产、文件夹和收藏集的静态引用列表的收藏集，以及根据搜索条件提取资产的收藏集。  您还可以使用不同位置的资产创建收藏集，并与具有不同访问、查看和编辑权限级别的多个用户共享这些收藏集。

有关更多信息，请参阅 [管理收藏集](manage-collections.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## 组织资产以使用用户档案 {#organize-to-use-profiles}

处理配置文件包含 [!DNL Assets] 处理命令，这些命令适用于上传到预定义文件夹的资产。 配置文件用于自动处理文件夹或新上传资产的内容。 您可以利用用户档案更好地组织资产。

标准化元数据使用、文件命名和文件夹结构可确保随着数字资产池的增长，您可以更精确、更一致地将处理配置文件应用到文件夹。

>[!MORELIKETHIS]
>
>* [用于处理元数据、图像和视频的配置文件](processing-profiles.md).
>* [元数据配置文件](/help/assets/metadata-config.md#metadata-profiles).
>* [视频配置文件](video-profiles.md).
>* [Dynamic Media图像配置文件](image-profiles.md).

