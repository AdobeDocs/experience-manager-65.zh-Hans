---
title: 安装和配置Designer
description: Designer作为独立安装程序提供，并且与Workbench捆绑在一起。 了解如何安装独立的Designer。
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin, User, Developer
feature: Forms Designer,Designer
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
solution: Experience Manager, Experience Manager Forms
source-git-commit: 89f807e1d31c5588d86e50160b0149e00422b78c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 安装和配置Designer{#installing-and-configuring-designer}

## 先决条件 {#pre-requisites}

+++ 对于64位AEM Forms Designer（推荐）

* 安装64位版本的[Visual C++ 2019可再发行组件(x64)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)。 在开始安装之前，请确保已安装前面提到的可再分发运行时包。
* 具有管理员权限的用户可以安装或卸载AEM Forms Designer。

+++

+++ 对于32位AEM Forms Designer

* 安装32位版本的[Visual C++ 2019可再发行组件(x64)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)。 在开始安装之前，请确保已安装前面提到的可再分发运行时包。
* 具有管理员权限的用户可以安装或卸载AEM Forms Designer。

+++

>[!NOTE]
>
>* AEM 6.5 Forms Service Pack 19 (6.5.19.0)中引入了设计器的64位版本。
>* 自[AEM Forms Service Pack 21 (6.5.21.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)发行以来，已弃用32位版本的设计器。
> * Forms Designer支持的平台与AEM Forms支持的平台一致。 要了解Forms Designer支持的平台，请[单击此处](/help/forms/using/aem-forms-jee-supported-platforms.md)。

有关安装Forms Designer的更多信息，请访问[常见问题解答](#fandq)。

## 安装AEM Forms Designer {#install-designer}

Designer作为独立安装程序提供，并且与WorkBench捆绑在一起。 如果您使用的是独立的AEM Forms Designer安装程序，请执行以下步骤：

1. 卸载以前版本的AEM Forms Designer（如果已安装）。
1. 根据您的要求，下载64位AEM Forms Designer（推荐）或32位AEM Forms Designer。

   >[!NOTE]
   > 
   >* AEM 6.5 Forms Service Pack 20 (6.5.20.0)版本计划弃用32位Forms Designer。 Adobe建议您升级到64位Forms designer。
   >* 64位Forms Designer仅适用于AEM 6.5 Forms Service Pack 19 (6.5.19.0)或更高版本。
   >* 从Adobe Experience Manager 6.5 Forms Service Pack 15 (6.5.15.0)开始，Forms Designer版本也包含Service Pack版本。 例如，对于Service Pack 15，版本号为6.5.15.20221112.1.0。在此示例中，6.5.15是Service Pack版本。

1. 通过双击setup.exe启动AEM Forms Designer安装程序。
1. 继续并在Personalization屏幕上提供您的详细信息和序列号。

   >[!NOTE]
   >
   >* 从[Adobe授权网站](https://licensing.adobe.com/)获取您的Forms Designer许可证密钥。

1. 如果您接受许可协议，请单击“下一步”继续。
1. （可选）如果您要在所选位置安装Designer，请更改默认安装路径。 单击“下一步”。
1. 单击“上一步”以更改任何首选项。 要安装Designer，请单击“安装”。
1. 安装完成后，单击“完成”。

或者，您也可以使用被动模式或静默模式，通过命令行安装AEM Forms Designer。

* 被动命令行安装：安装程序显示进度条，指示安装正在进行，但不显示提示或错误消息。 启动后，无法取消安装。

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* 静默命令行安装：安装程序运行安装时不显示用户界面。 不显示提示、消息或对话框。 启动后，无法取消安装。

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```

## 更新AEM Forms Designer {#update-forms-designer}

在更新AEM Forms Designer 6.5.16.0的最新版本时，有两种情况：

* **用例1**：当用户的AEM Forms Designer版本低于6.5.15.0时。
* **用例2**：用户具有6.5.15.0 AEM Forms Designer版本时。

+++**当用户的AEM Forms Designer版本低于6.5.15.0时。**

如果您使用的是独立的AEM Forms Designer安装程序，请执行以下步骤：

1. 在安装&#x200B;**AEM Forms Designer 6.5.16.0**&#x200B;之前，用户必须卸载任何以前的版本。
1. 从AEM表单发布页面下载并安装[AEM Forms Designer 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。
1. 成功安装&#x200B;**AEM Forms Designer 6.5.15.0**&#x200B;后，通过双击下载的安装程序文件下载并安装[AEM Forms Designer 6.5.16.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。

+++

+++**当用户使用6.5.15.0 AEM Forms Designer版本时**

如果您使用的是独立的AEM Forms Designer安装程序，请执行以下步骤：
1. 从[软件分发门户](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)下载最新版本的AEM Forms Designer。
1. 通过双击下载的安装程序文件来安装最新版本的AEM Forms Designer。

+++

## 常见问题解答 {#fandq}

* **用户能否直接升级或安装64位设计器？**
   * 可以，用户可以直接升级或安装64位设计器。 若要升级，请安装[SP19](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/Designer-Patch/sp19_x64/aemforms_designer_6_5_0_wwe_win.zip)设计器完整安装程序并应用后续设计器修补程序版本。

     >[!NOTE]
     > 在升级到64位设计器之前，请先卸载32位设计器（如果存在）。

* **用户是否可以在其系统上同时安装32位和64位？**
   * 不可以，32位和64位安装不能在同一台计算机上工作。 用户可以使用32位设计器或64位设计器。

* **如何检查用户是否使用64位设计器或32位设计器？**
   * 可通过两种方式检查Forms Designer版本：

      1. 打开Designer，转到“帮助”，单击“关于设计器”，您会看到设计器版本信息以及bits信息，例如，您会看到64位写入版本末尾，如下所示：

         `6.5.21.20240522.1.161 | 64 bit`
      1. 打开Designer，左上角显示一个品牌图标，其中包含带有产品名称的64位信息。

