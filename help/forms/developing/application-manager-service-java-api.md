---
title: Application Manager Service JavaAPI快速开始(SOAP)
seo-title: Application Manager Service JavaAPI快速开始(SOAP)
description: Application Manager Service JavaAPI快速开始(SOAP)
uuid: 01a9bce3-868b-495b-bdee-bc60f029129e
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 12da2a9b-4009-496e-953f-c2ae0352f59f
role: 开发人员
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Application Manager Service JavaAPI快速开始(SOAP){#application-manager-service-javaapi-quick-start-soap}

Java API快速开始(SOAP)可用于Application Manager服务。

[快速开始:使用Java API(SOAP)部署应用程序](application-manager-service-java-api.md#quick-start-soap-mode-deploying-applications-using-the-java-api)

[快速开始:使用Java API(SOAP)删除应用程序](application-manager-service-java-api.md#quick-start-soap-mode-removing-an-application-using-the-java-api)

>[!NOTE]
>
>应用程序管理器API仅支持AEM Forms LCA文件。 它不支持LiveCycle ES2和ES4的LCA文件。

AEM Forms操作可以使用AEM Forms强类型API执行，连接模式应设置为SOAP。

>[!NOTE]
>
>使用AEM表单进行编程中的Java API(SOAP)快速开始基于Forms（如果您使用的是其他操作系统，如Unix），则使用适用操作系统支持的路径替换特定于窗口的路径。 同样，如果您使用的是另一台J2EE应用程序服务器，请确保指定有效的连接属性。 请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

## 快速开始（SOAP模式）：使用Java API {#quick-start-soap-mode-deploying-applications-using-the-java-api}部署应用程序

以下Java代码示例导入基于名为&#x200B;*EncryptDocument.lca*&#x200B;的现有LCA文件的应用程序。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
     * 3. activation.jar (required for SOAP mode)
     * 4. axis.jar (required for SOAP mode)
     * 5. commons-codec-1.3.jar (required for SOAP mode)
     * 6. commons-collections-3.2.jar  (required for SOAP mode)
     * 7. commons-discovery.jar (required for SOAP mode)
     * 8. commons-logging.jar (required for SOAP mode)
     * 9. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 10. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 11. jaxrpc.jar (required for SOAP mode)
     * 12. log4j.jar (required for SOAP mode)
     * 13. mail.jar (required for SOAP mode)
     * 14. saaj.jar (required for SOAP mode)
     * 15. wsdl4j.jar (required for SOAP mode)
     * 16. xalan.jar (required for SOAP mode)
     * 17. xbean.jar (required for SOAP mode)
     * 18. xercesImpl.jar (required for SOAP mode)
     * 19. adobe-workflow-client-sdk.jar
     * 20. adobe-applicationmanager-client-sdk.jar
 
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
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
 import com.adobe.idp.applicationmanager.application.ApplicationStatus;
 import com.adobe.idp.applicationmanager.client.ApplicationManager;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class DeployApplication {
 
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
 
             //Get the AEM Forms application to deploy
             FileInputStream fileApp = new FileInputStream("C:\\Adobe\EncryptDocument.lca");
             Document lcApp = new Document(fileApp);
 
             //Create an ApplicationManager object
             ApplicationManager appManager = new ApplicationManager(myFactory);
 
             //Import the application into the production server
             ApplicationStatus appStatus = appManager.importApplicationArchive(lcApp);
             int status = appStatus.getStatusCode();
 
             //Determine if the application was successfully deployed
             if (status==1)
                     System.out.println("The application was successfully deployed");
             else
                     System.out.println("The application was not successfully deployed. The status is "+status);
         }
         catch(Exception e)
         {
             e.printStackTrace();
         }
     }
 }
 
```

## 快速开始（SOAP模式）：使用Java API {#quick-start-soap-mode-removing-an-application-using-the-java-api}删除应用程序

以下Java代码示例删除了名为&#x200B;*EncryptDocument*&#x200B;的应用程序。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
     * 3. activation.jar (required for SOAP mode)
     * 4. axis.jar (required for SOAP mode)
     * 5. commons-codec-1.3.jar (required for SOAP mode)
     * 6. commons-collections-3.2.jar  (required for SOAP mode)
     * 7. commons-discovery.jar (required for SOAP mode)
     * 8. commons-logging.jar (required for SOAP mode)
     * 9. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 10. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 11. jaxrpc.jar (required for SOAP mode)
     * 12. log4j.jar (required for SOAP mode)
     * 13. mail.jar (required for SOAP mode)
     * 14. saaj.jar (required for SOAP mode)
     * 15. wsdl4j.jar (required for SOAP mode)
     * 16. xalan.jar (required for SOAP mode)
     * 17. xbean.jar (required for SOAP mode)
     * 18. xercesImpl.jar (required for SOAP mode)
     * 19. adobe-workflow-client-sdk.jar
     * 20. adobe-applicationmanager-client-sdk.jar
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
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
 
 import com.adobe.idp.applicationmanager.application.Application;
 import com.adobe.idp.applicationmanager.application.ApplicationId;
 
 import com.adobe.idp.applicationmanager.client.ApplicationManager;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RemoveApplication {
 
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
             ApplicationManager appManager = new ApplicationManager(myFactory);
 
             //Get all the deployed applications
             List allApps = appManager.getApplications();
 
             //Iterate through the applications
             Iterator iter= allApps.iterator();
             while (iter.hasNext()) {
 
              //Cast each element to an Application object
              Application myApplication  = (Application)iter.next();
              ApplicationId appID = myApplication.getApplicationId();
              String appName = appID.getApplicationName();
 
              System.out.println("The name of the AEM Forms application is "+ appID.getApplicationName());
              //Determine the name of the application
              if (appName.compareTo("EncryptDocument")==0)
              {
                  //Remove the application
                 appManager.removeApplication(appID);
                 System.out.println("The  "+ appID.getApplicationName() +" application was removed.");
              }
         }
         }
         catch(Exception e)
             {
             e.printStackTrace();
             }
     }
 }
 
```

