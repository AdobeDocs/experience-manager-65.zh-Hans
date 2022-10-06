---
title: Java API快速入门简介
seo-title: Introducing Java API QuickStart
description: Java API快速入门简介
uuid: 480e1809-f789-4ad8-b5d5-2d97aba8411a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
discoiquuid: 38fd51ec-347e-4ae3-86d4-9d2429f79bdd
role: Developer
exl-id: 1d4062ef-fb24-4527-b899-896ce757beda
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Java API快速入门简介 {#introducing-java-api-quickstart}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

AdobeAEM Forms API快速入门可以帮助您加快开发与AEM Forms服务交互的程序的速度。 *快速入门*&#x200B;是完整的项目，您可以将其复制并粘贴到您自己的项目中，并用作起点。 您可以运行快速入门以查看其行为方式，并根据您自己的需求对其进行修改。

AEM Forms操作可以使用AEM Forms强类型API执行，连接模式应设置为SOAP。

Java强类型API快速入门提供了执行Java应用程序所需的JAR文件列表。 大多数Java快速入门都是在 `main`. 但是，Forms Java强类型API快速入门是作为在Web应用程序中运行的Java Servlet实施的。

JAR文件列表位于快速入门开头的注释部分。 例如，以下注释位于“输出”快速入门中，是在每个Java快速入门中找到的典型JAR文件列表。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe--client.jar
     * 3. adobe-usermanager-client.jar
     *
     * These JAR files are located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
     *
     * If you want to invoke a remote AEM Forms instance and there is a
     * firewall between the client application and AEM Forms, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms library files" in Programming
     * with AEM Forms
     */
```

## 多项服务快速入门 {#multiple-services-quick-start}

位于 *在JEE上使用AEM Forms进行编程* 调用特定服务以执行操作。 但是，某些快速入门会调用多个AEM Forms服务以执行给定的工作流。 以下列表提供了调用多个AEM Forms服务的Java快速入门：

[快速入门（SOAP模式）：使用Java API将位于AEM Forms存储库中的文档传递到输出服务](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) （调用存储库和输出服务）

[快速入门（SOAP模式）：使用Java API根据片段创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) （调用汇编程序和输出服务）

[快速入门（SOAP模式）：使用Java API使用提交的XML数据创建PDF文档](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api) (调用Forms、输出和文档管理服务)

[快速入门（SOAP模式）：使用Java API将文档传递到Forms服务](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) (调用Forms和文档管理服务)

[快速入门（SOAP模式）：使用Java API对基于XFA的表单进行数字签名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api) (调用Forms和签名服务)

[快速入门（SOAP模式）：使用Java API管理角色和权限](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) （调用DirectoryManager和AuthorizationManager服务）

[快速入门（SOAP模式）：使用Java API将文档传递到输出服务](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) （调用输出和文档管理服务）

>[!NOTE]
>
>“使用AEM Forms进行编程”中的“快速入门”基于在JBoss® Application Server和Microsoft® Windows®操作系统上部署的AEM Forms。 但是，如果您使用的是其他操作系统(如UNIX®)，请将特定于Windows的路径替换为适用操作系统支持的路径。 同样，如果您使用的是其他J2EE应用程序服务器，请确保指定有效的连接属性。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>大多数Web服务快速入门都使用C#编写，并且使用.NET框架。 但是，您可以创建客户端应用程序逻辑，该逻辑能够在任何支持SOAP标准的开发环境中调用AEM Forms服务。 (请参阅 [使用Web服务调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
