---
title: 导入和导出 PDF Generator 配置文件
description: 了解如何导入和导出PDF Generator配置文件。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: b363b23a-29bb-4ea4-a8f2-5ba9fe3c7b27
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: b26425d0-6fde-5e02-bfd6-e560e2fa86c9
    internal-label: PDF Generator
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 3%
---
# 导入和导出 PDF Generator 配置文件 {#importing-and-exporting-pdf-generator-configuration-files}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

配置文件包含PDF Generator转换信息，包括PDF、文件类型和安全设置。

>[!NOTE]
>
>无法通过导入自定义native2pdfconfig.xml文件来更改PDF Generator的超时设置。 该文件中的超时设置仅供参考，并在PDF Generator中显示当前设置。 要更改超时设置，请参阅[安装和部署PDF Generator表单](https://www.adobe.com/go/learn_aemforms_installJBoss_63)中的“设置AEM性能参数”。

## 导出当前配置文件 {#export-your-current-configuration-file}

1. 在管理控制台中，单击服务> PDF Generator >配置文件>导出配置。
1. 要导出设置，请选择相应的选项：

   * 要导出所有命名设置，请选择下载整个配置。
   * 要仅导出一个Adobe PDF设置、安全设置或文件类型设置，请选择“下载最低配置”。

     如果要导出最低配置，请选择要导出的Adobe PDF、安全和文件类型设置。

1. 单击下载，并将XML文件保存在适当的位置。

## 导入配置文件 {#import-a-configuration-file}

>[!NOTE]
>
>系统将根据导入文件中的信息重新配置系统。

1. 在管理控制台中，单击服务> PDF Generator >配置文件>导入配置。
1. 选择“导入现有配置文件”。
1. 若要在“配置文件”框中指定文件位置，请单击“浏览”查找并选择该文件，然后单击“**导入**”。

## 转换AutoCAD文件中的所有图层 {#convert-all-layers-within-autocad-files}

默认情况下，PDF Generator仅将AutoCAD文件的默认图层转换为PDF，而不是文件中的所有图层。 要转换所有层，请按照以下步骤操作。

1. 在管理控制台中，单击服务> PDF Generator >配置文件>导出配置。
1. 选择下载整个配置，然后单击下载。
1. 在文本编辑器中，打开下载的文件，并在`PDFMaker`标记内的`AutoCAD`标记下添加文本`convertAllPages="true"`。
1. 在管理控制台中，单击服务> PDF Generator >配置文件>导入配置。
1. 选择“导入现有配置文件”，指定更新的文件，然后单击“导入”。

   使用修改后的配置文件转换的任何AutoCAD文件都将转换所有图层。

## 将您的配置重置为随PDF Generator一起安装的原始设置 {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. 在管理控制台中，单击服务> PDF Generator >配置文件>导入配置。
1. 选择将配置重置为默认设置，然后单击导入。
