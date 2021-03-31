---
title: 使用MSM重复使用资源
description: 跨从父资产派生并链接到父资产的多个页面/文件夹使用资产。 资产与主副本保持同步，单击几下即可从父资产接收更新。
contentOwner: AG
mini-toc-levels: 1
role: 业务从业者，管理员，架构师
feature: 资产管理，多站点管理器
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '3375'
ht-degree: 9%

---


# 对[!DNL Assets] {#reuse-assets-using-msm-for-assets}使用MSM重复使用资源

[!DNL Adobe Experience Manager]中的多站点管理器(MSM)功能使用户能够重复使用一次创作的内容，并在多个Web位置间重复使用。 与MSM一样，数字资产也适用于[!DNL Assets]功能。 使用MSM [!DNL Assets]，您可以：

* 只需创建一次资源，即可复制这些资源并在站点的其他区域重复使用。
* 在同步过程中保留多个副本，并一次更新原始主副本，以将更改推送到子副本。
* 通过暂时或永久暂停父资产和子资产之间的链接来进行本地更改。

## 前提条件 {#prereq}

要将MSM用于[!DNL Assets]，请至少安装[!DNL Experience Manager] 6.5 Service Pack 1。 有关详细信息，请参阅[最新服务包的发行说明](/help/release-notes/sp-release-notes.md)。

## 了解优势和概念{#concepts}

### 工作方式及优势{#how-it-works-and-the-benefits}

要了解在多个Web位置重复使用相同内容（文本和资产）的使用方案，请参阅[可能的MSM方案](/help/sites-administering/msm.md)。 [!DNL Experience Manager] 在原始资产及其链接副本之间保持一个链接，称为Live Copy(LC)。维护的链接允许将集中的更改推送到多个Live Copy。 这样可以在不受管理重复副本限制的情况下实现更快的更新。 改变的传播是无误的，是集中的。 该功能允许仅允许选定Live Copy进行更新。 用户可以分离链接（即中断继承），并进行在下次更新主副本和转出更改时不会覆盖的本地编辑。 可以对几个选定的元数据字段或整个资产进行分离。 它允许灵活地本地更新最初从主副本继承的资产。

MSM在源资产及其Live Copy之间保持实时关系，以便：

* 对源资产所做的更改也会应用（转出）到Live Copy，即Live Copy与源同步。
* 您可以通过暂停实时关系来更新Live Copy，或删除少数有限字段的继承。 对源的修改不再应用于Live Copy。

### [!DNL Assets]术语{#glossary}的MSM术语表

**来源：** 原始资产或文件夹。从中派生Live Copy的主副本。

**Live Copy:** 与其源同步的源资产/文件夹的副本。Live Copy可以是其他Live Copy的源。 了解如何创建LC。

**继承：** Live Copy资产/文件夹与其源之间的链接/引用，系统使用它来记住将更新发送到的位置。继承存在于元数据字段的粒度级别。 可以删除选择性元数据字段的继承，同时保留源与其Live Copy之间的实时关系。

**转出：** 将修改推送到源下游的Live Copy的操作。可以使用转出操作在一次操作中更新一个或多个Live Copy。 请参阅转出。

**转出配置：** 确定同步哪些属性、方式和时间的规则。创建Live Copy时会应用这些配置；稍后可以编辑；和子项可以从其父资产继承转出配置。 对于[!DNL Assets]的MSM，请仅使用标准转出配置。 其他转出配置对于[!DNL Assets]不可用。

**同步：** 除了转出之外，还有一个操作，通过将更新从源发送到Live Copy，使源与其Live Copy之间具有对等性。将为特定Live Copy启动同步，该操作会从源中提取更改。 使用此操作，只能更新其中一个Live Copy。 请参阅同步操作。

**暂停：** 暂时删除Live Copy与其源资产/文件夹之间的Live关系。您可以恢复关系。 请参阅暂停操作。

**继续：** 恢复Live关系，以便Live Copy再次开始从源接收更新。请参阅恢复操作。

**重置：** 重置操作通过覆盖所有本地更改，使Live Copy再次成为源的副本。它还会删除继承取消，并重置所有元数据字段的继承。 要在将来进行本地修改，您必须再次取消特定字段的继承。 请参见对LC的本地修改。

**分离：** 不可撤消地删除Live Copy资产/文件夹的Live关系。分离操作后，Live Copy永远无法从源接收更新，并且它不再是Live Copy了。 请参阅删除关系。

## 创建资产{#createlc}的Live Copy

要从一个或多个源资产或文件夹创建Live Copy，请执行以下操作之一：

* 方法1:选择源资产，然后从顶部的工具栏中单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL Live Copy]**。
* 方法2:在[!DNL Experience Manager]用户界面中，单击界面右上角的&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL Live Copy]**。

您可以一次创建一个资产或文件夹的Live Copy。 您可以创建从资产或作为Live Copy本身的文件夹派生的Live Copy。 用例不支持内容片段(CF)。 在尝试创建其Live Copy时，CF将按原样复制，而不与任何关系。 复制的CF是及时的快照，在更新原始CF时不会更新。

要使用第一种方法创建Live Copy，请执行以下步骤：

1. 选择源资产或文件夹。 在工具栏中，单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL Live Copy]**。

   ![从界面创建Live  [!DNL Experience Manager] Copy](assets/create_lc1.png)

   *图：从界面创建 [!DNL Experience Manager] Live Copy。*

1. 选择目标文件夹。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 提供标题和名称。 资产没有子项。 在创建文件夹的Live Copy时，您可以选择包括或排除子项。
1. 选择转出配置。 单击&#x200B;**[!UICONTROL 创建]**。

要使用第二种方法创建Live Copy，请执行以下步骤：

1. 在[!DNL Experience Manager]接口中，从右上角单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL Live Copy]**。

   ![从界面创建Live  [!DNL Experience Manager] Copy](assets/create_lc2.png)

   *图：从界面创建 [!DNL Experience Manager] Live Copy。*

1. 选择源资产或文件夹。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 选择目标文件夹。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 提供标题和名称。 资产没有子项。 在创建文件夹的Live Copy时，您可以选择包括或排除子项。
1. 选择转出配置。 单击&#x200B;**[!UICONTROL 创建]**。

>[!NOTE]
>
>移动源或Live Copy时，会保留关系。 删除Live Copy后，这些关系即被删除。

## 视图源和Live Copy {#properties}的各种属性和状态

您可以从[!DNL Experience Manager]用户界面的各个区域视图Live Copy的信息和MSM相关状态，如关系、同步、转出等。

以下两种方法适用于资产和文件夹：

* 选择Live Copy资产，并在其属性页面中查找信息。
* 选择源文件夹，并从[!UICONTROL  Live Copy控制台]中查找每个Live Copy的详细信息。

>[!TIP]
>
>要检查几个单独Live Copy的状态，请使用第一种方法检查&#x200B;**[!UICONTROL 属性]**&#x200B;页。 要检查多个Live Copy的状态，请使用第二种方法检查&#x200B;**[!UICONTROL 关系状态]**&#x200B;页。

### Live Copy的信息和状态{#statuslcasset}

要检查Live Copy资产或文件夹的信息和状态，请执行以下步骤。

1. 选择Live Copy资产或文件夹。 单击工具栏中的&#x200B;**[!UICONTROL 属性]**。 或者，使用键盘快捷键`p`。
1. 单击&#x200B;**[!UICONTROL Live Copy]**。 您可以检查源的路径、挂起状态、同步状态、上次转出日期和执行上次转出的用户。

   ![Live Copy信息和状态显示在控制台的属性中](assets/lcfolder_info_properties.png)

   *图：Live Copy信息和状态。*

1. 在子资产借用Live Copy配置时，您可以启用或禁用。

1. 您可以为Live Copy选择选项，以从父项继承转出配置或更改配置。

### 文件夹{#status-lc-folder}的所有Live Copy的信息和状态

[!DNL Experience Manager] 提供一个控制台，用于检查源文件夹的所有Live Copy的状态。此控制台显示所有子资产的状态。

1. 选择源文件夹。 单击工具栏中的&#x200B;**[!UICONTROL 属性]**。 或者，使用键盘快捷键`p`。
1. 单击 **[!UICONTROL Live Copy 源]**。要打开控制台，请单击 **[!UICONTROL Live Copy 概述]**。此功能板提供所有子资产的顶级状态。

   ![视图源的Live Copy控制台中Live Copy的状态](assets/livecopy-statuses.png)

   *图：视图源Live Copy Console中 [!UICONTROL Live Copy] 的状态。*

1. 要查看 Live Copy 文件夹中每个资产的详细信息，请选择一个资产，然后单击工具栏中的&#x200B;**[!UICONTROL 关系状态]**。

   ![文件夹中Live Copy子资产的详细信息和状态](assets/livecopy_relationship_status.png)

   文件夹中Live Copy子资产的详细信息和状态

>[!TIP]
>
>您可以快速查看其他文件夹的Live Copy的状态，而无需浏览太多。 从&#x200B;**[!UICONTROL Live Copy概述]**&#x200B;接口的中上部更改文件夹。

### 源{#refrailsource}的“引用”边栏中的快速操作

对于源资产或文件夹，您可以看到以下信息，并直接从引用边栏中执行以下操作：

* 请参阅Live Copy的路径。
* 在[!DNL Experience Manager]用户界面中打开或显示特定Live Copy。
* 将更新同步到特定Live Copy。
* 暂停关系或更改特定Live Copy的转出配置。
* 访问Live Copy概述控制台。

选择源资产或文件夹，打开左边栏，然后单击&#x200B;**[!UICONTROL 引用]**。 或者，选择一个资产或文件夹，然后使用键盘快捷键 `Alt + 4`。

![所选源的“引用”边栏中可用的操作和信息](assets/referencerail_source.png)

*图：所选源的“引用”边栏中可用的操作和信息。*

对于特定的Live Copy，单击&#x200B;**[!UICONTROL 编辑Live Copy]**&#x200B;以暂停关系或更改转出配置。

![对于特定Live Copy，在选择源资产时，可从引用边栏访问暂停关系或更改转出配置的选项](assets/referencerail_editlc_options.png)

*图：暂停关系或更改特定Live Copy的转出配置。*

### Live Copy {#ref-rail-lc}的“引用”边栏中的快速操作

对于Live Copy资产或文件夹，您可以看到以下信息，并直接从引用边栏中执行以下操作：

* 查看源的路径。
* 在[!DNL Experience Manager]用户界面中打开或显示特定Live Copy。
* 推出更新。

选择 Live Copy 资产或文件夹，打开左边栏，然后单击&#x200B;**[!UICONTROL 引用]**。或者，选择一个资产或文件夹，然后使用键盘快捷键 `Alt + 4`。

![所选 Live Copy 的“引用”边栏中的可用操作](assets/referencerail_livecopy.png)

*图：在引用边栏中为所选Live Copy提供的操作。*

## 将源中的修改传播到Live Copy {#rolloutsync}

修改源后，可以使用同步操作或转出操作将更改传播到Live Copy。 要了解两个操作之间的差异，请参阅[词汇表](#glossary)。

### 转出操作{#rollout}

您可以从源资产启动转出操作，并更新全部或几个选择的Live Copy。

1. 选择Live Copy资产或文件夹。 单击工具栏中的&#x200B;**[!UICONTROL 属性]**。 或者，使用键盘快捷键`p`。
1. 单击 **[!UICONTROL Live Copy 源]**。单击工具栏中的&#x200B;**[!UICONTROL 转出]**。
1. 选择要更新的Live Copy。 单击&#x200B;**[!UICONTROL 转出]**。
1. 要转出对子资产所做的更新，请选择&#x200B;**[!UICONTROL 转出源和所有子资产]**。

   ![将源的修改转出为几个或所有Live Copy](assets/livecopy_rollout_page.png)

   *图：将源的修改转出为几个或所有Live Copy。*

>[!NOTE]
>
>在源资产中所做的修改将仅转出到直接相关的Live Copy。 如果Live Copy是从其他Live Copy派生的，则不会将修改转出到派生的Live Copy。

或者，您也可以在选择特定Live Copy后从引用边栏启动转出操作。 有关详细信息，请参阅Live Copy的[引用边栏中的快速操作](#ref-rail-lc)。 在转出的此方法中，只更新所选Live Copy及其子项（可选）。

![将源的修改转出到所选Live Copy](assets/livecopy_rollout_dialog.png)

*图：将源的修改转出到所选Live Copy。*

### 关于同步操作{#about-sync}

同步操作将仅将源中的修改提取到选定的Live Copy。 同步操作尊重并维护取消继承后完成的本地修改。 不会覆盖本地修改，也不会重新建立取消的继承。 可以通过三种方式启动同步操作。

| 在[!DNL Experience Manager]接口中的位置 | 何时及为何使用 | 如何使用 |
|---|---|---|
| [!UICONTROL 引用边] 栏 | 在已选择源时快速同步。 | 请参阅[源](#refrailsource)的引用边栏中的快速操作 |
| 工具栏。 | 在您已打开Live Copy属性时启动同步。 | 请参阅[同步Live Copy](#sync-lc) |
| [!UICONTROL Live Copy概述控] 制台 | 选择源文件夹或[!UICONTROL Live Copy概述]控制台已打开时，快速同步多个资产（不一定全部）。 同步操作是一次为一个资产启动的，但是这是一次为多个资产执行同步的更快方式。 | 请参阅[对Live Copy文件夹中的许多资产执行的操作](#bulk-actions) |

### 同步Live Copy {#sync-lc}

要开始同步操作，请打开Live **[!UICONTROL Copy的]** “属性”页，单击 **[!UICONTROL Live Copy]** ，然后单击工具栏中所需的操作。

要查看与同步操作相关的状态和信息，请参 [阅Live Copy的信息和状态](#statuslcasset) ，以 [及文件夹所有Live Copy的信息和状态](#status-lc-folder)。

![“同步”操作会拉取对源所做的更改](assets/livecopy_sync.png)

*图：“同步”操作会拉取对源所做的更改。*

>[!NOTE]
>
>如果关系已挂起，则工具栏中不提供同步操作。 同步操作在引用边栏中可用，但即使成功转出，修改也不会传播。

## 暂停和恢复关系{#suspend-resume}

您可以暂时暂停关系，以防止Live Copy接收对源资产或文件夹所做的修改。 还可以恢复Live Copy的关系，以便开始从源接收修改。

要暂停或继续，请打 **[!UICONTROL 开Live Copy的]** “属性”页面，单击 **[!UICONTROL Live Copy]** ，然后从工具栏中单击所需的操作。

或者，您也可以从 **[!UICONTROL Live Copy 概述]**&#x200B;控制台快速暂停或恢复 Live Copy 文件夹中多个资产的关系。请参阅[对 Live Copy 文件夹中的许多资产执行操作](#bulk-actions)。

## 对Live Copy {#local-mods}进行本地修改

Live Copy是创建时原始源的副本。 Live Copy的元数据值是从源继承的。 元数据字段单独维护对源资产各个字段的继承。

但是，您可以灵活地对Live Copy进行本地修改，以更改一些选定的属性。 要进行本地修改，请取消所需属性的继承。 取消一个或多个元数据字段的继承后，资产的实时关系和其他元数据字段的继承将保留。 任何同步或转出不会覆盖本地修改。 要执行此操作，请打开Live Copy资产的&#x200B;**[!UICONTROL 属性]**&#x200B;页面，单击元数据字段旁边的&#x200B;**[!UICONTROL 取消继承]**&#x200B;选项。

您可以撤消所有本地修改并将资产还原到其源的状态。 不可撤消且即时地重置操作会覆盖所有本地修改，并在所有元数据字段上重新建立继承。 要还原，请从Live Copy资产的&#x200B;**[!UICONTROL 属性]**&#x200B;页面，单击工具栏中的&#x200B;**[!UICONTROL 重置]**。

![重置操作会覆盖本地编辑内容，并部分将Live Copy与其源关联。](assets/livecopy_reset.png)

*图：重置操作会覆盖本地编辑内容，并部分将Live Copy与其源关联。*

## 删除实时关系{#detach}

您可以使用分离操作完全删除源与Live Copy之间的关系。 分离后，Live Copy将成为独立的资产或文件夹。 在分离后立即在[!DNL Experience Manager]接口中显示为新资产。 要将Live Copy从源中分离出来，请执行以下步骤。

1. 选择Live Copy资产或文件夹。 单击工具栏中的&#x200B;**[!UICONTROL 属性]**。 或者，使用键盘快捷键`p`。

1. 单击&#x200B;**[!UICONTROL Live Copy]**。 单击工具栏中的&#x200B;**[!UICONTROL 分离]**。 在显示的对话框中单击&#x200B;**[!UICONTROL 分离]**。

   ![分离操作会完全删除源和Live Copy之间的关系](assets/livecopy_detach.png)

   *图：分离操作会完全删除源和Live Copy之间的关系。*

   >[!CAUTION]
   >
   >单击对话框中的&#x200B;**[!UICONTROL 分离]**&#x200B;时，该关系将立即删除。 无法通过单击“属性”页上的&#x200B;**[!UICONTROL 取消]**&#x200B;来撤消。

或者，您也可以从&#x200B;**[!UICONTROL Live Copy概述]**&#x200B;控制台中快速分离Live Copy文件夹中的多个资产。 请参阅[对 Live Copy 文件夹中的许多资产执行操作](#bulk-actions)。

## Live Copy文件夹{#bulk-actions}中的批量操作

如果您在Live Copy文件夹中有多个资产，则启动每个资产的操作可能会很繁琐。 您可以从[!UICONTROL Live Copy控制台]快速对许多资产启动基本操作。 以上方法继续适用于单个资产。

1. 选择源文件夹。 单击工具栏中的&#x200B;**[!UICONTROL 属性]**。 或者，使用键盘快捷键`p`。
1. 单击 **[!UICONTROL Live Copy 源]**。要打开控制台，请单击 **[!UICONTROL Live Copy 概述]**。
1. 在此功能板中，从 Live Copy 文件夹中选择 Live Copy 资产。单击工具栏中的所需操作。可用的操作有&#x200B;**[!UICONTROL 同步]**、**[!UICONTROL 重置]**、**[!UICONTROL 暂停]**&#x200B;和&#x200B;**[!UICONTROL 分离]**。您可以快速对任意数量的Live Copy文件夹中与选定源文件夹存在Live Relationhy关系的任何资产启动这些操作。

   ![从Live Copy概述控制台轻松更新Live Copy文件夹中的许多资产](assets/livecopyconsole_update_many_assets.png)

   *图：从Live Copy概述控制台轻松更新Live Copy文件夹 [!UICONTROL 中的许] 多资产。*

## 扩展[!DNL Assets] {#extend-api}的MSM

[!DNL Experience Manager] 允许您使用MSM Java API扩展功能。对于[!DNL Assets]，扩展的工作方式与对于[!DNL Sites]的MSM相同。 有关详细信息，请参阅[扩展MSM](/help/sites-developing/extending-msm.md)和以下内容，以了解有关特定任务的信息：

* [API概述](/help/sites-developing/extending-msm.md#overview-of-the-java-api)
* [创建同步操作](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action)
* [创建转出配置](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration)
* [创建并使用一个简单的LiveActionFactory类](/help/sites-developing/extending-msm.md#creating-and-using-a-simple-liveactionfactory-class)

>[!NOTE]
>
>* [!DNL Sites]的MSM中的Blueprint在[!DNL Assets]的MSM中称为Live Copy源。
>* [!DNL Assets]的MSM不支持删除创建站点向导中的章节步骤。
>* [!DNL Assets]的MSM不支持在页面属性（触屏优化UI）上配置MSM锁。


## 资产管理任务对Live Copy {#manage-assets}的影响

Live Copy和源是可以作为数字资产在某种程度上进行管理的资产或文件夹。 [!DNL Experience Manager]中的某些资产管理任务对Live Copy具有特定影响。

* 复制Live Copy时，会创建一个Live Copy资产，其源与第一个Live Copy相同。
* 移动源或其Live Copy时，将保留Live关系。
* “编辑”操作不适用于Live Copy资产。 如果Live Copy的源本身是Live Copy，则编辑操作不适用。
* 签出操作不适用于Live Copy资产。
* 对于源文件夹，可使用创建审阅任务的选项。
* 在列表视图和列视图中查看资产列表时，Live Copy资产或文件夹会对其显示“Live Copy”。 它可帮助您轻松识别文件夹中的Live Copy。

## 比较[!DNL Assets]和[!DNL Sites] {#comparison}的MSM

在更多情况下，[!DNL Assets]的MSM与“站点”功能的MSM行为相匹配。 需要注意的一些主要区别是：

* [!DNL Sites]的MSM中的Blueprint在[!DNL Assets]的MSM中称为Live Copy源。
* 在站点中，您可以比较Blueprint及其Live Copy，但是在[!DNL Assets]中无法将源与其Live Copy进行比较。
* 不能在[!DNL Assets]中编辑Live Copy。
* 站点通常有子项，但[!DNL Assets]没有。 在创建单个资产的Live Copy时，不提供包含或排除子项的选项。
* [!DNL Assets]的MSM不支持删除创建站点向导中的章节步骤。
* 对于[!DNL Assets],MSM不支持在页面属性（触屏优化UI）上配置MSM锁。
* 对于[!DNL Assets]的MSM，请仅使用&#x200B;**[!UICONTROL 标准转出配置]**。 其他转出配置对于[!DNL Assets]不可用。

## 最佳实践{#best-practices}

MSM的一些最佳实践是：

* 在开始实施之前，计划资产和内容流的父子关系。

## MSM对[!DNL Assets] {#limitations}的限制和已知问题

以下是MSM对[!DNL Assets]的限制。

* 用例不支持内容片段(CF)。 在尝试创建其Live Copy时，CF将按原样复制，而不与任何关系。 复制的CF是及时的快照，在更新原始CF时不进行更新。

* MSM不支持元数据写回。 写回时，继承会中断。
