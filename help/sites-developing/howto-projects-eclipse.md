---
title: 如何使用Eclipse开发AEM项目
description: 本指南介绍如何使用Eclipse开发基于AEM的项目
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 9d421599-0417-4329-a528-9cda4e3716f5
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 如何使用Eclipse开发AEM项目{#how-to-develop-aem-projects-using-eclipse}

本指南介绍如何使用Eclipse开发基于AEM的项目。

>[!NOTE]
>
>Adobe现在提供了[AEM Eclipse开发工具](/help/sites-developing/aem-eclipse.md)，可帮助您使用Eclipse开发AEM解决方案。

## 概述 {#overview}

要开始在Eclipse上开发AEM，需要执行以下步骤。

在本操作方法的其余部分中，将更详细地解释每个方法。

* 安装Eclipse 4.3 (Kepler)
* 基于Maven设置您的AEM项目
* 在Maven POM中为Eclipse准备JSP支持
* 将Maven项目导入Eclipse

>[!NOTE]
>
>本指南基于Eclipse 4.3 (Kepler)和AEM 5.6.1。

## 安装Eclipse {#install-eclipse}

从[Eclipse下载页面](https://www.eclipse.org/downloads/)下载“面向Java EE开发人员的Eclipse IDE”。

按照[安装说明](https://wiki.eclipse.org/Eclipse/Installation)安装Eclipse。

## 基于Maven设置您的AEM项目 {#set-up-your-aem-project-based-on-maven}

接下来，使用Maven设置项目，如[如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md)中所述。

## 为Eclipse准备JSP支持 {#prepare-jsp-support-for-eclipse}

Eclipse还可以在使用JSP时提供支持，例如，

* 自动完成标记库
* 由&lt;cq：defineObjects />和&lt;sling：defineObjects />定义的对象的Eclipse感知

要使此功能正常工作，请执行以下操作：

1. 按照[如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md)中的[如何使用JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)的说明进行操作。
1. 将以下内容添加到内容模块POM的&lt;build />部分中。

   Eclipse的Maven支持插件m2e不提供maven-jspc-plugin支持，此配置告知m2e忽略插件以及清理临时编译结果的相关任务。

   这不是问题：如[如何使用JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)中所述，此设置中的maven-jspc-plugin仅用于验证JSP是否会在构建过程中编译。 Eclipse已报告JSP中的任何问题，并且不依赖此Maven插件来执行此操作。

   **myproject/content/pom.xml**

   ```xml
   <build>
     <!-- ... -->
     <pluginManagement>
       <plugins>
         <!--This plugin's configuration is used to store Eclipse m2e settings only. It has no influence on the Maven build itself.-->
         <plugin>
           <groupId>org.eclipse.m2e</groupId>
           <artifactId>lifecycle-mapping</artifactId>
           <version>1.0.0</version>
           <configuration>
             <lifecycleMappingMetadata>
               <pluginExecutions>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.sling</groupId>
                     <artifactId>maven-jspc-plugin</artifactId>
                     <versionRange>[2.0.6,)</versionRange>
                     <goals>
                       <goal>jspc</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.maven.plugins</groupId>
                     <artifactId>maven-clean-plugin</artifactId>
                     <versionRange>[2.4.1,)</versionRange>
                     <goals>
                       <goal>clean</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
               </pluginExecutions>
             </lifecycleMappingMetadata>
           </configuration>
         </plugin>
       </plugins>
     </pluginManagement>
   </build>
   ```

### 将Maven项目导入Eclipse {#import-the-maven-project-into-eclipse}

1. 在Eclipse中，选择文件>导入……
1. 在“导入”对话框中，选择“Maven”>“现有Maven项目”，然后单击“下一步”。

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. 输入项目顶级文件夹的路径，然后单击“全选”和“完成”。

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. 现在，您已准备好使用Eclipse来开发您的AEM项目，包括JSP自动完成。

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >如果在`/libs`中包含`/libs/foundation/global.jsp`或其他JSP，则必须将其复制到项目，以便Eclipse能够解析该包含。 同时，您需要确保它未由Maven捆绑到您的内容包中。 有关如何实现此目标请参见[如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md)。
