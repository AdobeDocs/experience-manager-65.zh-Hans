---
title: 生成PDF服务Java API快速启动(SOAP)
description: 使用生成PDF服务将Microsoft Word文档转换为PDF文档，将HTML内容转换为PDF文档，并使用Java API将PDF文档转换为RTF文件。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
role: Developer
exl-id: b856a93b-91fa-47a5-9e46-6a537218fd4e
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# 生成PDF服务Java API快速入门(SOAP) {#generate-pdf-service-java-api-quickstart-soap}

Java API快速入门(SOAP)可用于生成PDF服务。

[快速入门(SOAP模式)：使用Java API将Microsoft Word文档转换为PDF文档](generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[快速入门(SOAP模式)：使用Java API将HTML内容转换为PDF文档](generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[快速入门(SOAP模式)：使用Java API(SOAP模式)将PDF文档转换为RTF文件](generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-an-rtf-file-using-the-java-api-soap-mode)

AEM Forms操作可以使用AEM Forms强类型API执行，并且连接模式应设置为SOAP。

>[!NOTE]
>
>《使用AEM Forms进行编程快速入门》基于在JBoss Application Server和Microsoft Windows操作系统上部署的Forms Server。 但是，如果您使用的是其他操作系统（如UNIX），请将特定于Windows的路径替换为适用的操作系统支持的路径。 同样，如果您使用的是其他J2EE应用程序服务器，请确保指定有效的连接属性。 请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## 快速入门(SOAP模式)：使用Java API将Microsoft Word文档转换为PDF文档 {#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api}

以下代码示例转换一个名为的Word文件 *Loan.doc* 到名为的PDF文档 *Loan.pdf*. (请参阅 [将Word文档转换为PDF文档](/help/forms/developing/converting-file-formats-pdf.md#converting-word-documents-to-pdf-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-generatepdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
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
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Properties;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
 import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
 
 public class ConvertWordDocumentSOAP {
 
     public static void main(String[] args)
     {
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
 
         //Create a GeneratePdfServiceClient object
         GeneratePdfServiceClient pdfGenClient = new GeneratePdfServiceClient(myFactory);
 
         //Get a Microsoft Word file document to convert to a PDF document
         String inputFileName = "C:\\Adobe\\Loan.doc";
         FileInputStream fileInputStream = new FileInputStream(inputFileName);
         Document inDoc = new Document(fileInputStream);
 
         //Set createPDF2 parameter values
         String adobePDFSettings = "Smallest_File_Size";
          String securitySettings = "No Security";
          String fileTypeSettings = "Filetype Settings";
 
          //Convert the Word document to a PDF document
          CreatePDFResult result = pdfGenClient.createPDF2(
             inDoc,
             inputFileName,
             fileTypeSettings,
             adobePDFSettings,
             securitySettings,
             null,
             null);
 
          //Get the newly created document
          Document createdDocument = result.getCreatedDocument();
 
          //Save the converted PDF document as a PDF file
         createdDocument.copyToFile(new File("C:\\Adobe\\Loan.pdf"));
     }
     catch (Exception e) {
         System.out.println("Error OCCURRED: " + e.getMessage());
         }
     }
 }
```

## 快速入门(SOAP模式)：使用Java API将HTML内容转换为PDF文档 {#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api}

以下Java代码示例将位于https://www.adobe.com的HTML内容转换为名为的PDF文档 *AdobeHTML.pdf*. (请参阅 [将HTML文档转换为PDF文档](/help/forms/developing/converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-generatepdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
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
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.io.File;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
 import com.adobe.livecycle.generatepdf.client.HtmlToPdfResult;
 
 public class ConvertHTMLSOAP {
 
     public static void main(String[] args)
     {
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
 
         //Create a GeneratePdfServiceClient object
         GeneratePdfServiceClient pdfGenClient = new GeneratePdfServiceClient(myFactory);
 
         //Get an HTML document to convert to a PDF document a
         String inputFileName = "https://www.adobe.com";
 
          String securitySettings = "No Security";
         String fileTypeSettings = "Standard";
 
          //Convert HTML content to a PDF document
          HtmlToPdfResult result = pdfGenClient.htmlToPDF2(
                  inputFileName,
                  fileTypeSettings,
                  securitySettings,
                  null,
                 null);
 
          //Get the newly created document
          Document createdDocument = result.getCreatedDocument();
 
          //Save the PDF document as a PDF file
         createdDocument.copyToFile(new File("C:\\AdobeHTML.pdf"));
     }
     catch (Exception e) {
         System.out.println("Error OCCURRED: " + e.getMessage());
     }
     }
 }
```

## 快速入门(SOAP模式)：使用Java API(SOAP模式)将PDF文档转换为RTF文件 {#quick-start-soap-mode-converting-a-pdf-document-to-an-rtf-file-using-the-java-api-soap-mode}

以下代码示例转换名为的PDF文档 *Loan.pdf* 到名为的RTF文档 *Loan.rtf*. (请参阅 [将PDF文档转换为非图像格式](/help/forms/developing/converting-file-formats-pdf.md#converting-pdf-documents-to-non-image-formats).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-generatepdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
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
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.generatepdf.client.ConvertPDFFormatType;
 import com.adobe.livecycle.generatepdf.client.ExportPDFResult;
 import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
 
 
 public class GeneratePdf_ExportPDFSOAP {
 
     public static void main(String[] args)
     {
         try{
             //Set connection properties required to invoke AEM Forms using SOAP mode
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a GeneratePdfServiceClient object
             GeneratePdfServiceClient pdfGenClient = new GeneratePdfServiceClient(factory);
 
             //Get a PDF document to convert to an RTF document
             String inputFileName = "C:\\Adobe\\Loan.pdf.pdf";
             FileInputStream fileInputStream = new FileInputStream(inputFileName);
             Document inDoc = new Document(fileInputStream);
 
             //Convert a PDF document to a RTF document
             ExportPDFResult result = pdfGenClient.exportPDF2(
                 inDoc,
                 inputFileName,
                 ConvertPDFFormatType.RTF,
                 null);
 
          //Get the newly created RTF document
          Document createdDocument = result.getConvertedDocument();
 
          //Save the RTF file
         createdDocument.copyToFile(new File("C:\\Adobe\\Loan.pdf.rtf"));
         }
         catch (Exception e) {
             System.out.println("Error OCCURRED: " + e.getMessage());
         }
     }
 }
```
