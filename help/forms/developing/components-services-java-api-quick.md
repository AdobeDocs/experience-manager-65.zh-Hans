---
title: 组件和服务Java API快速启动(SOAP)
description: 使用Java API快速入门(SOAP)以编程方式操作AEM Forms组件和服务。
uuid: 7d9ade2d-f927-4558-9e80-df08bd572772
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: 14f17126-e744-479b-a8e6-24c131615b46
role: Developer
exl-id: fe1198b5-4145-4dcd-ab8a-4015daaf89b7
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# 组件和服务Java API快速入门(SOAP) {#components-and-services-java-apiquick-start-soap}

Java API快速入门(SOAP)可用于组件和服务。


[快速入门（SOAP模式）：使用Java API部署组件](components-services-java-api-quick.md#quick-start-soap-mode-deploying-a-component-using-the-java-api)

[快速启动（SOAP模式）：使用Java API设置服务的执行上下文](components-services-java-api-quick.md#quick-start-soap-mode-setting-the-execution-context-of-a-service-using-the-java-api)

[快速启动（SOAP模式）：使用Java API禁用服务安全性](components-services-java-api-quick.md#quick-start-soap-mode-disabling-service-security-using-the-java-api)

[快速启动（SOAP模式）：使用Java API启动服务](components-services-java-api-quick.md#quick-start-soap-mode-starting-a-service-using-the-java-api)

[快速启动（SOAP模式）：使用Java API修改服务配置值](components-services-java-api-quick.md#quick-start-soap-mode-modifying-a-services-configuration-values-using-the-java-api)

[快速入门（SOAP模式）：使用Java API删除组件](components-services-java-api-quick.md#quick-start-soap-mode-removing-components-using-the-java-api)


AEM Forms操作可以使用AEM Forms强类型API执行，并且连接模式应设置为SOAP。

>[!NOTE]
>
>无法使用Web服务以编程方式处理组件和服务。

>[!NOTE]
>
>位于“使用AEM进行编程”表单中的快速入门指南基于正在JBoss和Windows操作系统上部署的Forms服务器。 但是，如果您使用的是其他操作系统（如Unix），请将windows特定的路径替换为适用的操作系统支持的路径。 同样，如果您使用的是其他J2EE应用程序服务器，请确保指定有效的连接属性。 请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

>[!NOTE]
>
>如果您有自定义组件，并且使用SOAP或EJB协议在同一本地服务器上调用DSC，并且这些调用在升级后停止工作，则使用VM内调用策略。 使用具有默认ServiceClientFactory的in-VM DSC调用方法，并且不要使用SOAP或EJB协议构建ServiceClientFactory。

## 快速入门（SOAP模式）：使用Java API部署组件 {#quick-start-soap-mode-deploying-a-component-using-the-java-api}

以下Java示例部署基于名为的JAR文件的组件 *adobe-emailSample-dsc.jar*.

```java
 /* 
        * This Java Quick Start uses the following JAR files 
        * 1. adobe-taskmanager-client.jar 
        * 2. adobe-livecycle-client.jar 
        * 3. adobe-usermanager-client.jar 
        * 4. activation.jar (required for SOAP mode) 
        * 5. axis.jar (required for SOAP mode) 
        * 6. commons-codec-1.3.jar (required for SOAP mode) 
        * 7. commons-collections-3.2.jar  (required for SOAP mode) 
        * 8. commons-discovery.jar (required for SOAP mode) 
        * 9. commons-logging.jar (required for SOAP mode) 
        * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
        * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
        * 12. jaxrpc.jar (required for SOAP mode) 
        * 13. log4j.jar (required for SOAP mode) 
        * 14. mail.jar (required for SOAP mode) 
        * 15. saaj.jar (required for SOAP mode) 
        * 16. wsdl4j.jar (required for SOAP mode) 
        * 17. xalan.jar (required for SOAP mode) 
        * 18. xbean.jar (required for SOAP mode) 
        * 19. xercesImpl.jar (required for SOAP mode)
        * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to  
        * your local development environment and then include the 3 JBoss JAR files in your class path 
        * 
        * These JAR files are located in the following path: 
        * <install directory>/sdk/client-libs/common 
        * 
        * The adobe-utilities.jar file is located in the following path: 
        * <install directory>/sdk/client-libs/jboss 
        * 
        * The jboss-client.jar file is located in the following path: 
        * <install directory>/jboss/bin/client 
        * 
        * If you want to invoke a remote forms server instance and there is a 
        * firewall between the client application and the server, then it is  
        * recommended that you use the SOAP mode. When using the SOAP mode,  
        * you have to include additional JAR files located in the following  
        * path 
        * <install directory>/sdk/client-libs/thirdparty 
        * 
        * For information about the SOAP  
        * mode and the additional JAR files that need to be included,  
        * see "Setting connection properties" in Programming  
        * with AEM Forms 
     */ 
 import java.io.FileInputStream; 
 import java.util.*; 
  
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.idp.dsc.registry.component.client.*; 
 import com.adobe.idp.dsc.registry.infomodel.Component; 
  
 public class DeployComponents { 
  
     public static void main(String[] args) { 
          
         try{ 
          
             //Set connection properties required to invoke AEM Forms                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                          
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
             //Create a ComponentRegistryClient object 
             ComponentRegistryClient    componentReg = new ComponentRegistryClient(myFactory);  
              
             //Reference a JAR file that represents the component to deploy 
         //    FileInputStream componentFile = new FileInputStream("C:\\Adobe\adobe-emailSample-dsc.jar");  
              
             FileInputStream componentFile = new FileInputStream("C:\\A22\Bank.jar");  
             Document component = new Document(componentFile);  
              
             //Install the component 
             Component myComponent = componentReg.install(component); 
             componentReg.start(myComponent); 
              
             System.out.println("The component has been deployed");  
             } 
              
         catch(Exception e) 
         { 
             e.printStackTrace(); 
         } 
     } 
 } 
  
 
```

## 快速启动（SOAP模式）：使用Java API设置服务的执行上下文 {#quick-start-soap-mode-setting-the-execution-context-of-a-service-using-the-java-api}

以下Java代码示例将运行方式调用器执行上下文设置为名为的示例服务 *加密文档*.

```java
 /* 
        * This Java Quick Start uses the following JAR files 
        * 1. adobe-taskmanager-client.jar 
        * 2. adobe-livecycle-client.jar 
        * 3. adobe-usermanager-client.jar  
        * 4. activation.jar (required for SOAP mode) 
        * 5. axis.jar (required for SOAP mode) 
        * 6. commons-codec-1.3.jar (required for SOAP mode) 
        * 7. commons-collections-3.2.jar  (required for SOAP mode) 
        * 8. commons-discovery.jar (required for SOAP mode) 
        * 9. commons-logging.jar (required for SOAP mode) 
        * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
        * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
        * 12. jaxrpc.jar (required for SOAP mode) 
        * 13. log4j.jar (required for SOAP mode) 
        * 14. mail.jar (required for SOAP mode) 
        * 15. saaj.jar (required for SOAP mode) 
        * 16. wsdl4j.jar (required for SOAP mode) 
        * 17. xalan.jar (required for SOAP mode) 
        * 18. xbean.jar (required for SOAP mode) 
        * 19. xercesImpl.jar (required for SOAP mode) 
        * The JBoss files must be kept in the jboss\bin\client folder. You can copy the client folder to  
        * your local development environment and then include the 3 JBoss JAR files in your class path 
        * 
        * These JAR files are located in the following path: 
        * <install directory>/sdk/client-libs/common 
        * 
        * 
        * 
        * If you want to invoke a remote forms server instance and there is a 
        * firewall between the client application and the server, then it is  
        * recommended that you use the SOAP mode. When using the SOAP mode,  
        * you have to include additional JAR files located in the following  
        * path 
        * <install directory>/sdk/client-libs/thirdparty 
        * 
        * For information about the SOAP  
        * mode and the additional JAR files that need to be included,  
        * see "Setting connection properties" in Programming  
        * with AEM Forms 
     */ 
 import java.util.*; 
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.idp.dsc.registry.infomodel.ServiceConfiguration; 
 import com.adobe.idp.dsc.registry.service.ModifyServiceConfigurationInfo; 
 import com.adobe.idp.dsc.registry.service.client.ServiceRegistryClient; 
  
 /* 
     * This Java quick start sets the Run-As Invoker to a service named EncryptDocument 
     */ 
 public class SetRunAsConfiguration { 
      
      public static void main(String[] args) { 
  
     try{ 
         //Set connection properties required to invoke AEM Forms 
         Properties connectionProps = new Properties(); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "tblue"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
          
         //Create a ServiceRegistryClient object      
         ServiceClientFactory _factory = ServiceClientFactory.createInstance(connectionProps); 
         ServiceRegistryClient _src = new ServiceRegistryClient(_factory); 
          
         //Reference the EncryptDocument service 
         ServiceConfiguration _config  = _src.getHeadActiveConfiguration("EncryptDocument"); 
          
         //Set the RUN_AS_INVOKER execution context 
         ModifyServiceConfigurationInfo _configModifyInfo = new ModifyServiceConfigurationInfo(); 
         _configModifyInfo.setServiceId(_config.getServiceId()); 
         _configModifyInfo.setMajorVersion(_config.getMajorVersion()); 
         _configModifyInfo.setMinorVersion(_config.getMinorVersion()); 
         _configModifyInfo.setRunAsConfiguration(ServiceConfiguration.RUN_AS_INVOKER); 
         _config = _src.modifyConfiguration(_configModifyInfo); 
     }catch (Exception e) { 
          e.printStackTrace(); 
         }     
     } 
 } 
 
```

## 快速启动（SOAP模式）：使用Java API禁用服务安全性 {#quick-start-soap-mode-disabling-service-security-using-the-java-api}

以下Java代码示例对示例EncryptDocument服务和从该服务中调用的服务（Set Value和Encryption服务）禁用安全性。

```java
 /* 
        * This Java Quick Start uses the following JAR files 
        * 1. adobe-taskmanager-client.jar 
        * 2. adobe-livecycle-client.jar 
        * 3. adobe-usermanager-client.jar 
        * 4. activation.jar (required for SOAP mode) 
        * 5. axis.jar (required for SOAP mode) 
        * 6. commons-codec-1.3.jar (required for SOAP mode) 
        * 7. commons-collections-3.2.jar  (required for SOAP mode) 
        * 8. commons-discovery.jar (required for SOAP mode) 
        * 9. commons-logging.jar (required for SOAP mode) 
        * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
        * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
        * 12. jaxrpc.jar (required for SOAP mode) 
        * 13. log4j.jar (required for SOAP mode) 
        * 14. mail.jar (required for SOAP mode) 
        * 15. saaj.jar (required for SOAP mode) 
        * 16. wsdl4j.jar (required for SOAP mode) 
        * 17. xalan.jar (required for SOAP mode) 
        * 18. xbean.jar (required for SOAP mode) 
        * 19. xercesImpl.jar (required for SOAP mode) 
* 
        * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to 
        * your local development environment and then include the 3 JBoss JAR files in your class path 
        * 
        * These JAR files are located in the following path: 
        * <install directory>/sdk/client-libs/common 
        * 
        * The adobe-utilities.jar file is located in the following path: 
        * <install directory>/sdk/client-libs/jboss 
        * 
        * The jboss-client.jar file is located in the following path: 
        * <install directory>/jboss/bin/client 
        * 
        * If you want to invoke a remote forms server instance and there is a 
        * firewall between the client application and the server, then it is  
        * recommended that you use the SOAP mode. When using the SOAP mode,  
        * you have to include additional JAR files located in the following  
        * path 
        * <install directory>/sdk/client-libs/thirdparty 
        * 
        * For information about the SOAP  
        * mode and the additional JAR files that need to be included,  
        * see "Setting connection properties" in Programming  
        * with AEM Forms 
     */ 
 import java.util.*; 
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.idp.dsc.registry.infomodel.ServiceConfiguration; 
 import com.adobe.idp.dsc.registry.service.ModifyServiceInfo; 
 import com.adobe.idp.dsc.registry.service.client.ServiceRegistryClient; 
  
 /* 
     * This Java quick start disables security from the EncryptDocument process 
     * and each service that is located in this process 
     */ 
 public class DisableSecurity{ 
      
      public static void main(String[] args) { 
  
     try{ 
         //Set connection properties required to invoke AEM Forms                                 
         Properties connectionProps = new Properties(); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                      
          
         //Create a ServiceRegistryClient object      
         ServiceClientFactory _factory = ServiceClientFactory.createInstance(connectionProps); 
         ServiceRegistryClient _src = new ServiceRegistryClient(_factory); 
          
         //Reference the EncryptDocument process and each service that is  
         //invoked from within the EncryptDocument process 
         ServiceConfiguration encryptDocumentService  = _src.getHeadActiveConfiguration("EncryptDocument"); 
         ServiceConfiguration setValueService  = _src.getHeadActiveConfiguration("SetValue"); 
         ServiceConfiguration encryptionService  = _src.getHeadActiveConfiguration("EncryptionService"); 
          
         //Create a ModifyServiceInfo object 
         ModifyServiceInfo si = new ModifyServiceInfo(); 
          
         //Disable security from the EncryptDocument service 
         si.setId(encryptDocumentService.getServiceId()); 
         si.setSecurityEnabled(false); 
         _src.modifyService(si); 
          
         //Disable security from the SetValue service 
         si.setId(setValueService.getServiceId()); 
         si.setSecurityEnabled(false); 
         _src.modifyService(si); 
          
         //Disable security from the EncryptionService 
         si.setId(encryptionService.getServiceId()); 
         si.setSecurityEnabled(false); 
         _src.modifyService(si); 
              
     }catch (Exception e) { 
          e.printStackTrace(); 
         }     
     } 
 } 
 
```

## 快速启动（SOAP模式）：使用Java API启动服务 {#quick-start-soap-mode-starting-a-service-using-the-java-api}

以下Java代码示例启动一个名为的服务 *SendEmailService*.

```java
 package com.adobe.sample.servicemanager; 
  
 /** 
     * This Java Quick Start uses the following JAR files: 
     * 1. adobe-livecycle-client.jar 
     * 2. adobe-usermanager-client.jar 
     * 3. adobe-workflow-client-sdk.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if AEM Forms is not deployed on Jboss) 
     * 6. jacorb.jar (use a different JAR file if the forms server is not deployed on JBoss) 
     * 7. jnp-client.jar (use a different JAR file if the forms server is not deployed on JBoss) 
     */ 
 import java.util.*; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.registry.infomodel.ServiceConfiguration; 
 import com.adobe.idp.dsc.registry.service.client.ServiceRegistryClient; 
  
 public class StartService { 
  
     public static void main(String[] args) { 
          
         try{ 
             //Set connection properties required to invoke AEM Forms      
             Properties ConnectionProps = new Properties(); 
             ConnectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'"); 
             ConnectionProps.setProperty("DSC_TRANSPORT_PROTOCOL","SOAP");           
             ConnectionProps.setProperty("DSC_SERVER_TYPE", "JBoss"); 
             ConnectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator"); 
             ConnectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(ConnectionProps); 
  
             //Create a ServiceRegistryClient object 
             ServiceRegistryClient serviceReg = new ServiceRegistryClient(myFactory);  
          
             //Reference the SendEmailService 
             ServiceConfiguration myServiceConfig = serviceReg.getHeadActiveConfiguration("SendEmailService"); 
          
             //Start the SendEmailService 
             serviceReg.start(myServiceConfig); 
             } 
              
                 catch(Exception e) 
                 { 
                     e.printStackTrace(); 
                 } 
     } 
 } 
  
 
```

## 快速启动（SOAP模式）：使用Java API修改服务配置值 {#quick-start-soap-mode-modifying-a-services-configuration-values-using-the-java-api}

以下Java示例修改属于SendEmail服务的配置值。

```java
 /* 
     * This Java Quick Start uses the following JAR files 
        * 1. adobe-taskmanager-client.jar 
        * 2. adobe-livecycle-client.jar 
        * 3. adobe-usermanager-client.jar 
        * 4. activation.jar (required for SOAP mode) 
        * 5. axis.jar (required for SOAP mode) 
        * 6. commons-codec-1.3.jar (required for SOAP mode) 
        * 7. commons-collections-3.2.jar  (required for SOAP mode) 
        * 8. commons-discovery.jar (required for SOAP mode) 
        * 9. commons-logging.jar (required for SOAP mode) 
        * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
        * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
        * 12. jaxrpc.jar (required for SOAP mode) 
        * 13. log4j.jar (required for SOAP mode) 
        * 14. mail.jar (required for SOAP mode) 
        * 15. saaj.jar (required for SOAP mode) 
        * 16. wsdl4j.jar (required for SOAP mode) 
        * 17. xalan.jar (required for SOAP mode) 
        * 18. xbean.jar (required for SOAP mode) 
        * 19. xercesImpl.jar (required for SOAP mode) 
        * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to  
        * your local development environment and then include the 3 JBoss JAR files in your class path 
        * 
        * These JAR files are located in the following path: 
        * <install directory>/sdk/client-libs/common 
        * 
        * The adobe-utilities.jar file is located in the following path: 
        * <install directory>/sdk/client-libs/jboss 
        * 
        * The jboss-client.jar file is located in the following path: 
        * <install directory>/jboss/bin/client 
        * 
        * If you want to invoke a remote forms server instance and there is a 
        * firewall between the client application and the server, then it is  
        * recommended that you use the SOAP mode. When using the SOAP mode,  
        * you have to include additional JAR files located in the following  
        * path 
        * <install directory>/sdk/client-libs/thirdparty 
        * 
        * For information about the SOAP  
        * mode and the additional JAR files that need to be included,  
        * see "Setting connection properties" in Programming  
        * with AEM Forms 
     */ 
 import java.util.*; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.registry.infomodel.ConfigParameter; 
 import com.adobe.idp.dsc.registry.infomodel.ServiceConfiguration; 
 import com.adobe.idp.dsc.registry.service.ModifyServiceConfigurationInfo; 
 import com.adobe.idp.dsc.registry.service.client.ServiceRegistryClient; 
  
  
 public class ModifyService { 
  
     public static void main(String[] args) { 
          
         try{ 
             //Set connection properties required to invoke AEM Forms     
             Properties ConnectionProps = new Properties(); 
             ConnectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'"); 
             ConnectionProps.setProperty("DSC_TRANSPORT_PROTOCOL","SOAP");           
             ConnectionProps.setProperty("DSC_SERVER_TYPE", "JBoss"); 
             ConnectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator"); 
             ConnectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(ConnectionProps); 
  
             //Create a ServiceRegistryClient object 
             ServiceRegistryClient serviceReg = new ServiceRegistryClient(myFactory);  
          
             //Reference the SendEmailService 
             ServiceConfiguration myServiceConfig = serviceReg.getHeadServiceConfiguration("SendEmailService"); 
                              
             //Create a ModifyServiceConfigurationInfo object 
                 ModifyServiceConfigurationInfo modService = new ModifyServiceConfigurationInfo(); 
                      
             //Set configuration values required by the SendEmailService 
             String serviceId = myServiceConfig.getServiceId(); 
             modService.setServiceId(serviceId); 
             modService.setMajorVersion(1); 
             modService.setConfigParameterAsText("smtpHost","mySMTPSERVER"); 
             modService.setConfigParameterAsText("smtpUser","smyUserName");     
             modService.setConfigParameterAsText("smtpPassword","myPassword");     
                      
             //Modify the service’s configuration values 
             serviceReg.modifyConfiguration(modService); 
                          
             //Conform the new configuration values 
             ServiceConfiguration serviceConfig = serviceReg.getServiceConfiguration("SendEmailService",1,0); 
             ConfigParameter cp = serviceConfig.getConfigParameter("smtpUser"); 
             String configValue = cp.getTextValue();  
             System.out.println(configValue); 
             } 
      
             catch(Exception e) 
             { 
                 e.printStackTrace(); 
             } 
     } 
 } 
  
  
 
```

## 快速入门（SOAP模式）：使用Java API删除组件 {#quick-start-soap-mode-removing-components-using-the-java-api}

以下Java代码示例通过使用Java API删除组件。

```java
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-taskmanager-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed 
     * on JBoss) 
     * 6. commons-code-1.3.jar 
     * 7. adobe-workflow-client-sdk.jar 
     * 8. jacorb.jar (use a different JAR file if the forms server is not deployed on JBoss) 
     * 9. jnp-client.jar (use a different JAR file if the forms server is not deployed on JBoss) 
     * 
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to  
     * your local development environment and then include the 3 JBoss JAR files in your class path 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * The adobe-utilities.jar file is located in the following path: 
     * <install directory>/sdk/client-libs/jboss 
     * 
     * The jboss-client.jar file is located in the following path: 
     * <install directory>/jboss/bin/client 
     * 
     * If you want to invoke a remote forms server instance and there is a 
     * firewall between the client application and the server, then it is  
     * recommended that you use the SOAP mode. When using the SOAP mode,  
     * you have to include additional JAR files located in the following  
     * path 
     * <install directory>/sdk/client-libs/thirdparty 
     * 
     * For information about the SOAP  
     * mode and the additional JAR files that need to be included,  
     * see "Setting connection properties" in Programming  
     * with AEM Forms 
     */ 
 import java.util.*; 
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.idp.dsc.registry.component.client.*; 
 import com.adobe.idp.dsc.registry.infomodel.Component; 
  
 public class RemoveComponent { 
  
     public static void main(String[] args) { 
          
         try{ 
               //Set connection properties required to invoke AEM Forms                                                                                                                        
               Properties connectionProps = new Properties(); 
               connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
               connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
               connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
               connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
             //Create a ComponentRegistryClient object 
             ComponentRegistryClient    componentReg = new ComponentRegistryClient(myFactory);  
              
             //Retrieve the Id of the component to remove from the service container 
             Component myComponent = componentReg.getComponent("com.adobe.livecycle.sample.email.emailSampleComponent", "1.0"); 
              
             //Determine if the component is in a running state 
             if (myComponent.getState()== Component.RUNNING) 
             { 
                 //Stop the component 
                 Component stoppedComponent = componentReg.stop(myComponent); 
                  
                 //Uninstall the component 
                 componentReg.uninstall(stoppedComponent); 
             } 
             else 
                 componentReg.uninstall(myComponent); 
                  
             System.out.println("The component was removed."); 
             } 
              
             catch(Exception e) 
             { 
                 e.printStackTrace(); 
             } 
     } 
 } 
  
  
 
```
