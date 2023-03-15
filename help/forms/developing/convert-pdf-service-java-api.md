---
title: 转换PDF服务Java API快速启动(SOAP)
seo-title: Convert PDF Service Java API QuickStart(SOAP)
description: 转换PDF服务Java API快速启动(SOAP)
uuid: 97253ac7-f0c1-4766-a7bd-c19af52adf51
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: bdd9bb56-14f6-448b-be4a-7c11f670e901
role: Developer
exl-id: 8974c468-ff2b-431d-96fb-e987698619bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# 转换PDF服务Java API快速入门(SOAP) {#convert-pdf-service-java-api-quickstart-soap}

以下快速启动适用于ConvertPDF服务API。

[快速入门（SOAP模式）：使用Java API将PDF文档转换为PostScript](convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[快速入门（SOAP模式）：使用Java API将PDF文档转换为JPEG文件](convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

AEM Forms操作可以使用AEM Forms强类型API执行，并且连接模式应设置为SOAP。

>[!NOTE]
>
>位于“使用AEM进行编程”表单中的快速入门指南基于部署在JBoss Application Server和Microsoft Windows操作系统上的Forms Server。 但是，如果您使用的是其他操作系统（如UNIX），请将特定于Windows的路径替换为适用的操作系统支持的路径。 同样，如果您使用的是其他J2EE应用程序服务器，请确保指定有效的连接属性。 参见 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 快速入门（SOAP模式）：使用Java API将PDF文档转换为PostScript {#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api}

以下代码示例转换一个名为的PDF文档 *Loan.pdf* 到名为的PostScript文档 *贷款.ps*. (请参阅 [将PDF文档转换为PostScript](/help/forms/developing/converting-pdf-postscript-image-files.md#converting-pdf-documents-to-postscript).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-convertpdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7.  commons-collections-3.1.jar  (required for SOAP mode)
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
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.convertpdfservice.client.ConvertPdfServiceClient;
 import com.adobe.livecycle.convertpdfservice.client.ToPSOptionsSpec;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.Color;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.LineWeight;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.PSLevel;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.PageSize;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.Color;
 
 public class JavaAPIConvertPDFtoPSSOAP
 {
     public static void main(String[] args)
     {
     try
         {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a ConvertPdfServiceClient object
         ConvertPdfServiceClient convertPDFClient= new ConvertPdfServiceClient(myFactory);
 
         //Get a PDF file document to convert to a PS document
         //and populate a com.adobe.idp.Document object
         String inputFileName = "C:\\Adobe\Loan.pdf";
         FileInputStream fileInputStream = new FileInputStream(inputFileName);
         Document inDoc = new Document(fileInputStream);
 
         //Create a ToPSOptionsSpec object that defines run-time options
         ToPSOptionsSpec psSpec = new ToPSOptionsSpec();
         psSpec.setPsLevel(PSLevel.LEVEL_3);
         psSpec.setShrinkToFit(true);
         psSpec.setPageSize(PageSize.A4);
         psSpec.setRotateAndCenter(true);
         psSpec.setColor(Color.compositeGray);
         psSpec.setLineWeight(LineWeight.point25);
 
         //Convert the PDF document to a PostScript file
         Document createdDocument =convertPDFClient.toPS2(
             inDoc,
             psSpec
             );
 
         //Save the PostScript file
         createdDocument.copyToFile(new File("C:\\Adobe\Loan.ps"));
         }
     catch (Exception e)
         {
             e.printStackTrace();
         }
     }
 }
```

## 快速入门（SOAP模式）：使用Java API将PDF文档转换为JPEG文件 {#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api}

以下Java代码示例将一个PDF文档转换为 *Loan.pdf* 到一组JPEG文件，并将其存储在C:\Adobe目录中。 每个文件都命名为 `tempFile[index].jpg`，其中第一个图像文件名为 *tempFile0.jpg*. (请参阅 [将PDF文档转换为图像格式](/help/forms/developing/converting-pdf-postscript-image-files.md#converting-pdf-documents-to-image-formats).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-convertpdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7.  commons-collections-3.1.jar  (required for SOAP mode)
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
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Iterator;
 import java.util.List;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.convertpdfservice.client.ConvertPdfServiceClient;
 import com.adobe.livecycle.convertpdfservice.client.ToImageOptionsSpec;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.CMYKPolicy;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.ColorCompression;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.ColorSpace;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.GrayScaleCompression;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.GrayScalePolicy;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.ImageConvertFormat;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.Interlace;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.JPEGFormat;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.MonochromeCompression;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.PNGFilter;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.RGBPolicy;
 
 public class JavaAPIConvertPDFtoImageSOAP {
 
     public static void main(String[] args)
     {
     try
     {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create the ConvertPDF service client
         ConvertPdfServiceClient serviceClient = new ConvertPdfServiceClient(myFactory);
 
         //Get a PDF file document to convert to a JPEG document and populate a com.adobe.idp.Document object
         String inputFileName = "C:\\Adobe\Loan.pdf";
         FileInputStream fileInputStream = new FileInputStream(inputFileName);
         Document inDoc = new Document(fileInputStream);
 
         // Set up the runtime options for the new JPEG file to be created
         ToImageOptionsSpec spec = new ToImageOptionsSpec();
         spec.setImageConvertFormat(ImageConvertFormat.JPEG);
         spec.setGrayScaleCompression(GrayScaleCompression.Low);
         spec.setColorCompression(ColorCompression.Low);
         spec.setFormat(JPEGFormat.BaselineOptimized);
         spec.setRgbPolicy(RGBPolicy.Off);
         spec.setCmykPolicy(CMYKPolicy.Off);
         spec.setColorSpace(ColorSpace.RGB);
         spec.setResolution("72");
         spec.setMonochrome(MonochromeCompression.None);
         spec.setFilter(PNGFilter.Sub);
         spec.setInterlace(Interlace.Adam7);
         spec.setTileSize(180);
         spec.setGrayScalePolicy(GrayScalePolicy.Off);
 
         //Perform the conversion and get the containing the newly created JPEG files
         List allImages = serviceClient.toImage2(
             inDoc,
             spec
         );
 
         //Create an Iterator object and iterate through
         //the List object to get all images
         Iterator iter = allImages.iterator();
         int i = 0 ;
         while (iter.hasNext()) {
             Document file = (Document)iter.next();
             file.copyToFile(new File("C:\\Adobe\tempFile"+i+".jpg"));
             i++;
         }
     }
     catch (Exception e) {
         e.printStackTrace();
         }
     }
 }
```
