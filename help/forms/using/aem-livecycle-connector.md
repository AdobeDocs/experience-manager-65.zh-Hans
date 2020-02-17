---
title: 将AEM Forms与Adobe LiveCycle连接
seo-title: 将AEM Forms与Adobe LiveCycle连接
description: AEM LiveCycle Connector允许您从AEM应用程序和工作流程中启动LiveCycle ES4 Document Services。
seo-description: AEM LiveCycle Connector允许您从AEM应用程序和工作流程中启动LiveCycle ES4 Document Services。
uuid: 7dc9d5ec-7b19-4d93-936d-81ceb45dfffa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 7e404b45-1302-4dd1-b3c9-3f47fedb5f94
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 将AEM Forms与Adobe LiveCycle连接 {#connecting-aem-forms-with-adobe-livecycle}

Adobe Experience Manager(AEM)LiveCycle连接器可在AEM web应用程序和工作流程中无缝调用Adobe LiveCycle ES4 Document Services。 LiveCycle提供富客户端SDK，它允许客户端应用程序使用Java API启动LiveCycle服务。 AEM LiveCycle Connector在OSGi环境中使用这些API简化了操作。

## 将AEM服务器连接到Adobe LiveCycle {#connecting-aem-server-to-adobe-livecycle}

AEM LiveCycle Connector是 [AEM Forms加载项包的一部分](/help/forms/using/installing-configuring-aem-forms-osgi.md)。 安装AEM Forms加载项包后，请执行以下步骤，将LiveCycle服务器的详细信息添加到AEM Web Console。

1. 在AEM web控制台配置管理器中，找到Adobe LiveCycle Client SDK配置组件。
1. 单击组件可编辑配置服务器URL、用户名和密码。
1. 查看设置，然后单击“ **保存”**。

尽管属性是自解释的，但重要属性如下：

* **服务器URL** —— 指定LiveCycle服务器的URL。 如果希望LiveCycle和AEM通过https通信，请使用以下JVM启动AEM

   ```
   argument
    -Djavax.net.ssl.trustStore=<<em>path to LC keystore</em>>
   ```

   选项。

* **用户名**-指定用于在AEM和LiveCycle之间建立通信的帐户的用户名。 该帐户是具有启动文档服务权限的LiveCycle用户帐户。
* **密码**-指定密码。
* **服务名称** -指定使用“用户名”和“密码”字段中提供的用户凭据开始的服务。 默认情况下，启动LiveCycle服务时不会传递任何凭据。

## 启动文档服务 {#starting-document-services}

客户端应用程序可以使用Java API、Web服务、远程处理和REST以编程方式启动LiveCycle服务。 对于Java客户端，应用程序可以使用LiveCycle SDK。 LiveCycle SDK提供了一个Java API，用于远程启动这些服务。 例如，要将Microsoft word文档转换为PDF，客户端将启动GeneratePDFService。 调用流包含以下步骤：

1. 创建一个ServiceClientFactory实例。
1. 每个服务都提供一个客户端类。 要启动服务，请创建服务的客户端实例。
1. 启动服务并处理结果。

AEM LiveCycle Connector通过将这些客户端实例公开为可使用标准OSGi手段访问的OSGi服务，从而简化了流程。 LiveCycle连接器提供以下功能：

* 作为OSGi服务的客户端实例：打包为OSGI捆绑包的客户端列在“文档 [服务”列表部分](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p) 。 每个客户端jar将客户端实例注册为OSGi服务，并将其注册为OSGi服务注册表。
* 用户凭据传播：连接到LiveCycle服务器所需的连接详细信息在一个中央位置进行管理。
* ServiceClientFactory服务：要启动进程，客户端应用程序可以访问ServiceClientFactory实例。

### 通过OSGi Service Registry中的服务引用启动 {#starting-via-service-references-from-osgi-service-registry}

要从AEM中启动公开的服务，请执行以下步骤：

1. 确定主依赖关系。 在maven pom.xml文件中向所需的客户端jar添加依赖关系。 至少，向adobe-livecycle-client和adobe-usermanager-clientJar添加依赖关系。

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-livecycle-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-usermanager-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-cq-integration-api</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

   要启动服务，请为服务添加相应的Maven依赖关系。 有关依赖关系的列表，请参 [阅Document Service List](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p)。 例如，对于“生成PDF”服务，添加以下依赖关系：

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-generatepdf-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

1. 获取服务引用。 获取服务实例的句柄。 如果编写的是Java类，则可以使用声明性服务注释。

   ```java
   import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
   import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
   import com.adobe.idp.Document;
   
   @Reference
   GeneratePdfServiceClient generatePDF;
   ...
   
   Resource r = resourceResolver.getResource("/path/tp/docx");
   Document sourceDoc = new Document(r.adaptTo(InputStream.class));
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

   以上代码片断启动GeneratePdfServiceClient的createPDF API，将文档转换为PDF。 您可以使用以下代码在JSP中执行类似调用。 主要区别在于以下代码使用Sling ScriptHelper访问GeneratePdfServiceClient。

   ```java
   <%@ page import="com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient" %>
   <%@ page import="com.adobe.livecycle.generatepdf.client.CreatePDFResult" %>
   <%@ page import="com.adobe.idp.Document" %>
   
   GeneratePdfServiceClient generatePDF = sling.getService(GeneratePdfServiceClient.class);
   Document sourceDoc = ...
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

### 通过ServiceClientFactory启动 {#starting-via-serviceclientfactory}

在某些情况下，ServiceClientFactory类是必需的。 例如，您需要ServiceClientFactory调用进程。

```java
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;

@Reference
ServiceClientFactoryProvider scfProvider;

...
ServiceClientFactory scf = scfProvider.getDefaultServiceClientFactory();
...
```

## RunAs支持 {#runas-support}

LiveCycle中几乎每个文档服务都需要身份验证。 您可以使用以下任意选项启动这些服务，而无需在代码中提供显式凭据：

### 白名单配置 {#whitelist-configuration}

LiveCycle Client SDK配置包含有关服务名的设置。 此配置是服务列表，调用逻辑会立即使用管理员凭据。 例如，如果将DirectoryManager服务（用户管理API的一部分）添加到此列表，则任何客户端代码都可以直接使用该服务，并且调用层作为发送到LiveCycle服务器的请求的一部分自动传递配置的凭据

### RunAsManager {#runasmanager}

作为集成的一部分，提供了新的服务RunAsManager。 它允许您以编程方式控制调用LiveCycle服务器时使用的凭据。

```java
import com.adobe.livecycle.dsc.clientsdk.security.PasswordCredential;
import com.adobe.livecycle.dsc.clientsdk.security.PrivilegedAction;
import com.adobe.livecycle.dsc.clientsdk.security.RunAsManager;
import com.adobe.idp.dsc.registry.component.ComponentRegistry;

@Reference
private RunAsManager runAsManager;

List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
            public List<Component> run() {
                return componentRegistry.getComponents();
            }
        });
assertNotNull(components);
```

如果要传递不同的凭据，可以使用采用PasswordCredential实例的重载方法。

```java
PasswordCredential credential = new PasswordCredential("administrator","password");
List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
    public List<Component> run() {
        return componentRegistry.getComponents();
    }
},credential);
```

### InvocationRequest属性 {#invocationrequest-property}

如果调用进程或直接使用ServiceClientFactory类并创建InvocationRequest，则可以指定一个属性以指示调用层应使用配置的凭据。

```java
import com.adobe.idp.dsc.InvocationResponse
import com.adobe.idp.dsc.InvocationRequest
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory
import com.adobe.livecycle.dsc.clientsdk.InvocationProperties

ServiceClientFactoryProvider scfp = sling.getService(ServiceClientFactoryProvider.class)
ServiceClientFactory serviceClientFactory = scfp.getDefaultServiceClientFactory()
InvocationRequest ir = serviceClientFactory.createInvocationRequest("sample/LetterSubmissionProcess", "invoke", new HashMap(), true);

//Here we are invoking the request with system user
ir.setProperty(InvocationProperties.INVOKER_TYPE,InvocationProperties.INVOKER_TYPE_SYSTEM)

InvocationResponse response = serviceClientFactory.getServiceClient().invoke(ir);
```

## 文档服务列表 {#document-services-list}

### Adobe LiveCycle Client SDK API捆绑 {#adobe-livecycle-client-sdk-api-bundle}

提供以下服务：

* com.adobe.idp.um.api.AuthenticationManager
* com.adobe.idp.um.api.DirectoryManager
* com.adobe.idp.um.api.AuthorizationManager
* com.adobe.idp.dsc.registry.service.ServiceRegistry
* com.adobe.idp.dsc.registry.component.ComponentRegistry

#### Maven依赖关系 {#maven-dependencies}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-client</artifactId>
  <version>11.0.0</version>
</dependency>
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-usermanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Client SDK捆绑 {#adobe-livecycle-client-sdk-bundle}

提供以下服务：

* com.adobe.livecycle.dsc.clientsdk.security.RunAsManager
* com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider

#### Maven依赖关系 {#maven-dependencies-1}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-cq-integration-api</artifactId>
  <version>1.1.10</version>
</dependency>
```

### Adobe LiveCycle TaskManager客户端捆绑 {#adobe-livecycle-taskmanager-client-bundle}

提供以下服务：

* com.adobe.idp.taskmanager.dsc.client.task.TaskManager
* com.adobe.idp.taskmanager.dsc.client.TaskManagerQueryService
* com.adobe.idp.taskmanager.dsc.client.queuemanager.QueueManager
* com.adobe.idp.taskmanager.dsc.client.emailsettings.EmailSettingService
* com.adobe.idp.taskmanager.dsc.client.endpoint.TaskManagerEndpointClient
* com.adobe.idp.taskmanager.dsc.client.userlist.UserlistService

#### Maven依赖关系 {#maven-dependencies-2}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-taskmanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Workflow Client Bundle {#adobe-livecycle-workflow-client-bundle}

提供以下服务：

* com.adobe.idp.workflow.client.WorkflowServiceClient

#### Maven依赖关系 {#maven-dependencies-3}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-workflow-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle PDF Generator客户端捆绑 {#adobe-livecycle-pdf-generator-client-bundle}

提供以下服务：

* com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient

#### Maven依赖关系 {#maven-dependencies-4}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-generatepdf-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Application Manager客户端捆绑 {#adobe-livecycle-application-manager-client-bundle}

提供以下服务：

* com.adobe.idp.applicationmanager.service.ApplicationManager
* com.adobe.livecycle.applicationmanager.client.ApplicationManager
* com.adobe.livecycle.design.service.DesigntimeService

#### Maven依赖关系 {#maven-dependencies-5}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-applicationmanager-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe liveCycle Assembler客户端捆绑 {#adobe-livecycle-assembler-client-bundle}

提供以下服务：

* com.adobe.livecycle.assembler.client.AssemblerServiceClient

#### Maven依赖关系 {#maven-dependencies-6}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-assembler-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Form Data Integration客户端捆绑 {#adobe-livecycle-form-data-integration-client-bundle}

提供以下服务：

* com.adobe.livecycle.formdataintegration.client.FormDataIntegrationClient

#### Maven依赖关系 {#maven-dependencies-7}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-formdataintegration-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Forms Client捆绑 {#adobe-livecycle-forms-client-bundle}

提供以下服务：

* com.adobe.livecycle.formsservice.client.FormsServiceClient

#### Maven依赖关系 {#maven-dependencies-8}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-forms-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Output client捆绑 {#adobe-livecycle-output-client-bundle}

提供以下服务：

* com.adobe.livecycle.output.client.OutputClient

#### Maven依赖关系 {#maven-dependencies-9}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-output-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Reader Extensions客户端捆绑 {#adobe-livecycle-reader-extensions-client-bundle}

提供以下服务：

* com.adobe.livecycle.readerextensions.client.ReaderExtensionsServiceClient

#### Maven依赖关系 {#maven-dependencies-10}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-reader-extensions-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Rights Manager客户端捆绑 {#adobe-livecycle-rights-manager-client-bundle}

提供以下服务：

* com.adobe.livecycle.rightsmanagement.client.DocumentManager
* com.adobe.livecycle.rightsmanagement.client.EventManager
* com.adobe.livecycle.rightsmanagement.client.ExternalUserManager
* com.adobe.livecycle.rightsmanagement.client.LicenseManager
* com.adobe.livecycle.rightsmanagement.client.WatermarkManager
* com.adobe.livecycle.rightsmanagement.client.PolicyManager
* com.adobe.livecycle.rightsmanagement.client.AbstractPolicyManager

#### Maven依赖关系 {#maven-dependencies-11}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-rightsmanagement-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Signatures Client捆绑 {#adobe-livecycle-signatures-client-bundle}

提供以下服务：

* com.adobe.livecycle.signatures.client.SignatureServiceClientInterface

#### Maven依赖关系 {#maven-dependencies-12}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-signatures-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Truststore客户端捆绑 {#adobe-livecycle-truststore-client-bundle}

提供以下服务：

* com.adobe.truststore.dsc.TrustConfigurationService
* com.adobe.truststore.dsc.CRLService
* com.adobe.truststore.dsc.CredentialService
* com.adobe.truststore.dsc.CertificateService

#### Maven依赖关系 {#maven-dependencies-13}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-truststore-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe liveCycle Repository客户端捆绑 {#adobe-livecycle-repository-client-bundle}

提供以下服务：

* com.adobe.repository.bindings.ResourceRepository
* com.adobe.repository.bindings.ResourceSynchronizer

#### Maven依赖关系 {#maven-dependencies-14}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-repository-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

[联系支持](https://www.adobe.com/account/sign-in.supportportal.html)
