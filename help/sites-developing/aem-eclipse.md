---
title: 适用于 Eclipse 的 AEM 开发人员工具
description: 了解Adobe Experience Manager的Eclipse开发人员工具。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 00473769-c447-4966-a71e-117c669e0151
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 172b8667b1ff0bd533a035b21c316e2e66721bf8
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 4%

---

# 适用于 Eclipse 的 AEM 开发人员工具{#aem-developer-tools-for-eclipse}

适用于Eclipse的AEM Developer Tools的![圆形图像基元。](do-not-localize/chlimage_1-9.png)

## 概述 {#overview}

“AEM Developer Tools”是一个基于Apache许可证2下发布的适用于Apache Sling[的](https://sling.apache.org/documentation/development/ide-tooling.html)Eclipse插件的Eclipse插件。

它提供了多项功能，可简化AEM的开发：

* 通过Eclipse Server Connector与AEM实例无缝集成。
* 内容和OSGI捆绑包的同步。
* 使用代码热插拔功能调试支持。
* 通过特定项目创建向导简单BootstrapAEM项目。
* 轻松编辑JCR属性。

## 要求 {#requirements}

在使用AEM Developer Tools之前，请执行以下操作：

* 下载并安装适用于Java™ EE开发人员的[Eclipse IDE](https://www.eclipse.org/downloads/packages/release/luna/r/eclipse-ide-java-ee-developers)。 AEM开发人员工具当前支持Eclipse Kepler或更高版本

* 可与AEM版本5.6.1或更高版本一起使用
* 按照`eclipse.ini`Eclipse常见问题解答[中的说明，通过编辑](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F)配置文件来配置Eclipse安装，确保您至少有1 GB的栈内存。

>[!NOTE]
>
>在macOS上，右键单击&#x200B;**Eclipse.app**，然后选择&#x200B;**显示包内容**&#x200B;以查找您的`eclipse.ini`。

## 如何安装适用于Eclipse的AEM开发人员工具 {#how-to-install-the-aem-developer-tools-for-eclipse}

在满足上述[要求](#requirements)后，您可以按如下方式安装插件：

1. 打开[AEM开发人员工具网站](https://eclipse.adobe.com/)。

1. 复制&#x200B;**安装链接**。

   或者，您也可以下载归档文件，而不是使用安装链接。 这样做允许脱机安装，但您会遗漏自动更新通知。

1. 在Eclipse中，打开&#x200B;**帮助**&#x200B;菜单。
1. 单击&#x200B;**安装新软件**。
1. 单击&#x200B;**添加……**。
1. 在&#x200B;**名称**&#x200B;中，键入AEM Developer Tools。
1. 在&#x200B;**位置**&#x200B;中，复制安装URL。
1. 单击&#x200B;**确定**。
1. 检查&#x200B;**AEM**&#x200B;和&#x200B;**Sling**&#x200B;插件。
1. 单击&#x200B;**下一步**。
1. 单击&#x200B;**下一步**。
1. 接受Lincese协议，然后单击&#x200B;**完成**。
1. 单击&#x200B;**是**&#x200B;重新启动Eclipse。

## 如何导入现有项目 {#how-to-import-existing-projects}

>[!NOTE]
>
>查看从AEM[下载包时如何在Eclipse中使用包](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407)。

## AEM视角 {#the-aem-perspective}

适用于Eclipse的AEM开发工具附带了一个透视，您可以通过该透视图完全控制AEM项目和实例。

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## 示例多模块项目 {#sample-multi-module-project}

“AEM开发人员工具”包含一个示例的多模块项目，可帮助您快速上手Eclipse中的项目设置。 它还可用作几项AEM功能的最佳实践指南。 [了解有关项目原型的更多信息](https://github.com/adobe/aem-project-archetype)。

要创建示例项目，请完成以下步骤：

1. 在&#x200B;**文件** > **新建** > **项目**&#x200B;菜单中，浏览到&#x200B;**AEM**&#x200B;部分并选择&#x200B;**AEM示例多模块项目**。

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. 单击&#x200B;**下一步**。

   >[!NOTE]
   >
   >此步骤可能需要一些时间，因为m2eclipse必须扫描原型目录。

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. 从菜单中选择&#x200B;**com.adobe.granite.archetypes ： sample-project-archetype ： （最高编号）**，然后单击&#x200B;**下一步**。

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. 为示例项目填写&#x200B;**名称**、**组ID**&#x200B;和&#x200B;**工件ID**。 您还可以选择设置一些高级属性。

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. 现在，配置Eclipse可以连接的AEM服务器。

   要使用Debugger功能，请确保在调试模式下启动AEM，可以通过向命令行添加以下内容来实现该模式：

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. 单击&#x200B;**完成**。 将创建项目结构。

   >[!NOTE]
   >
   >在全新安装中（更具体地说：从未下载maven依赖项时），您可能会创建项目，但出现错误。 在这种情况下，请按照[解析无效项目定义](#resolving-invalid-project-definition)中所述的过程操作。

## 疑难解答 {#troubleshooting}

### 解析无效的项目定义 {#resolving-invalid-project-definition}

要解决无效依赖项和项目定义，请按照以下步骤操作：

1. 选择所有已创建的项目。
1. 右键单击。 在菜单&#x200B;**Maven**&#x200B;中，选择&#x200B;**更新项目**。
1. 检查&#x200B;**强制更新快照/版本**。
1. 单击&#x200B;**确定**。 Eclipse会尝试下载所需的依赖项。

### 在JSP文件中启用标记库自动完成 {#enabling-tag-library-autocompletion-in-jsp-files}

标记库自动完成可开箱即用，前提是将适当的依赖关系添加到项目中。 使用AEM Uber Jar时存在一个已知问题，该问题不包括所需的tld和TagExtraInfo文件。

要解决此问题，请确保org.apache.sling.scripting.jsp.taglib工件位于AEM Uber Jar之前的类路径中。 对于Maven项目，请将以下依赖项放在pom.xml中的Uber Jar之前。

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

确保为AEM的部署添加正确的版本。

## 更多信息 {#more-information}

适用于Eclipse网站的官方Apache Sling IDE工具为您提供有用信息：

* 适用于Eclipse的&#x200B;[**Apache Sling IDE工具**&#x200B;用户指南](https://sling.apache.org/documentation/development/ide-tooling.html)，本文档将指导您了解AEM开发工具支持的整体概念、服务器集成和部署功能。
* [疑难解答部分](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)。
* [已知问题列表](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)。

以下官方[Eclipse](https://www.eclipse.org/)文档可以帮助设置环境：

* [开始使用Eclipse](https://eclipseide.org/getting-started/)
* [Eclipse Luna帮助系统](https://help.eclipse.org/latest/index.jsp)
* [Maven集成(m2eclipse)](https://www.eclipse.org/m2e/)
