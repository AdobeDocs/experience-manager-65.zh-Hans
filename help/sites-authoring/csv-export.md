---
title: 导出到 CSV
description: 将与页面相关的信息导出到本地系统上的 CSV 文件
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: 18910143-f2f2-4cfe-88b9-651df90d9cb9
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 78%
---
# 导出到 CSV{#export-to-csv}

**创建 CSV 报表**&#x200B;允许您将页面的相关信息导出到本地系统上的 CSV 文件。

* 所下载的文件名为 `export.csv`
* 其内容取决于您选择的属性。
* 您可以定义导出的路径以及深度。

>[!NOTE]
>
>系统将使用您浏览器的下载功能及默认目标位置。

**创建 CSV 导出**&#x200B;向导让您选择以下内容：

* 要导出的属性
  * 元数据
    * 名称
    * 修改时间
    * 发布时间
    * 模板
    * 工作流
  * 翻译
    * 已翻译
  * 分析
    * 页面视图
    * 独特访客
    * 页面停留时间
* 深度
  * 父项路径
  * 仅直接子项
  * 其他级别的子项
  * 级别

生成的 `export.csv` 文件可以用 Excel 或任何其他兼容的应用程序打开。

![etc-01](assets/etc-01.png)

在浏览&#x200B;**站点**&#x200B;控制台（在“列表”视图中）时，可以使用创建&#x200B;**CSV报告**&#x200B;选项：它是&#x200B;**创建**&#x200B;下拉菜单的一个选项：

![etc-02](assets/etc-02.png)

要创建 CSV 导出，请执行以下操作：

1. 打开&#x200B;**站点**&#x200B;控制台，根据需要导航到所需的位置。
1. 从工具栏中，选择&#x200B;**创建**，然后选择 **CSV 报表**，以打开向导：

   ![etc-03](assets/etc-03.png)

1. 选择需要导出的属性。
1. 选择&#x200B;**创建**。
