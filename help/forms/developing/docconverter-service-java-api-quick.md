---
title: DocConverter服务Java API快速启动(SOAP)
seo-title: DocConverter Service Java API QuickStart(SOAP)
description: DocConverter服务Java API快速启动(SOAP)
uuid: a02e13a5-4557-4c8a-a4be-e8d017127128
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: ea4b26c8-b9cf-42c2-b4da-2884336014a9
role: Developer
exl-id: 554b19d6-47c3-4171-b59d-343f1ad935b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# DocConverter服务Java API快速入门(SOAP) {#docconverter-service-java-api-quickstart-soap}

Java API快速入门(SOAP)可用于DocConverter服务。

[快速入门（SOAP模式）：使用Java API确定PDF/A合规性](docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[快速入门（SOAP模式）：使用Java API将文档转换为PDF/文档](docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

AEM Forms操作可以使用AEM Forms强类型API执行，连接模式应设置为SOAP。

>[!NOTE]
>
>“使用AEM表单进行编程”中的“快速入门”基于JBoss应用程序服务器和Microsoft Windows操作系统上部署的Forms服务器。 但是，如果您使用的是其他操作系统（如UNIX），请将特定于Windows的路径替换为适用操作系统支持的路径。 同样，如果您使用的是其他J2EE应用程序服务器，请确保指定有效的连接属性。 请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## 快速入门（SOAP模式）：使用Java API将文档转换为PDF/文档 {#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api}

以下Java代码示例将转换名为的PDF文档 *Loan.pdf* PDF/文档，保存为名为 *LoanArchive.pdf*. (请参阅 [将文档转换为PDF/A文档](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdf-a-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-docconverter-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
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
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.docconverter.client.DocConverterServiceClient;
 import com.adobe.livecycle.docconverter.client.PDFAConversionOptionSpec;
 import com.adobe.livecycle.docconverter.client.PDFAConversionResult;
 
 public class CreatePDFADocumentSOAP {
 
     public static void main(String[] args) {
     try{
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a DocConverterServiceClient object
         DocConverterServiceClient docConverter = new DocConverterServiceClient(myFactory);
 
         //Reference a PDF document to convert to a PDF/A document
         FileInputStream myPDF = new FileInputStream("C:\\Adobe\Loan.pdf");
         Document inDoc = new Document(myPDF);
 
         //Create a PDFAConversionOptionSpec object and set
         //tracking information
         PDFAConversionOptionSpec spec = new PDFAConversionOptionSpec();
         spec.setLogLevel("FINE");
 
         //Convert the PDF document to a PDF/A document
         PDFAConversionResult result =  docConverter.toPDFA(inDoc,spec);
 
         //Save the PDF/A file
         Document pdfADoc= result.getPDFADocument();
         File pdfAFile = new File("C:\\Adobe\LoanArchive.pdf");
         pdfADoc.copyToFile(pdfAFile);
       }catch (Exception e) {
         e.printStackTrace();
     }
      }
 }
```

## 快速入门（SOAP模式）：使用Java API确定PDF/A合规性 {#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api}

以下Java代码示例确定输入PDF文档是否与PDF/A兼容。 传递到DocConverter服务的输入PDF文档名为 *LoanArchive.pdf*. 验证结果将写入名为 *ValidationResults.xml*. (请参阅 [以编程方式确定PDF/符合性](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-docconverter-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
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
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.docconverter.client.DocConverterServiceClient;
 import com.adobe.livecycle.docconverter.client.PDFAValidationOptionSpec;
 import com.adobe.livecycle.docconverter.client.PDFAValidationResult;
 
 public class IsDocumentPDFASOAP {
 
     public static void main(String[] args) {
     try{
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a DocConverterServiceClient object
         DocConverterServiceClient docConverter = new DocConverterServiceClient(myFactory);
 
         //Reference a PDF document used to determine PDF/A compliancy
         FileInputStream myPDF = new FileInputStream("C:\\Adobe\LoanArchive.pdf");
         Document inDoc = new Document(myPDF);
 
         //Create a PDFAValidationOptionSpec object and set
         //run-time values
         PDFAValidationOptionSpec spec = new PDFAValidationOptionSpec();
         spec.setCompliance(PDFAValidationOptionSpec.Compliance.PDFA_1B);
         spec.setResultLevel(PDFAValidationOptionSpec.ResultLevel.DETAILED);
         spec.setLogLevel("FINE");
         spec.setIgnoreUnusedResource(true);
 
         //Determine if the PDF document is PDF/A compliant
         PDFAValidationResult result =  docConverter.isPDFA(inDoc,spec)    ;
 
         //Get the results of the operation
         Boolean isPDFA = result.getIsPDFA();
 
         //Get XML data that contains validaction results
         Document validationResults =  result.getValidationLog();
         File file= new File("C:\\Adobe\ValidationResults.xml");
         validationResults .copyToFile(file);
 
     }catch (Exception e) {
         e.printStackTrace();
     }
      }
 }
```
