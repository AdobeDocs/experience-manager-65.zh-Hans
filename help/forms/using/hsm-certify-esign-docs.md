---
title: 使用HSM对文档进行数字签名或认证
seo-title: Use HSM to certify eSigned documents
description: 使用HSM或etoken设备来验证电子签名文档
seo-description: Use HSM or etoken devices to certify eSigned documents
uuid: bbe057c1-6150-41f9-9c82-4979d31d305d
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 536bcba4-b754-4799-b0d2-88960cc4c44a
exl-id: 4d423881-18e0-430a-849d-e1762366a849
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 0%

---

# 使用HSM对文档进行数字签名或认证 {#use-hsm-to-digitally-sign-or-certify-documents}

硬件安全模块(HSM)和令牌是专用的、经过硬化的、抗篡改的计算设备，旨在安全地管理、处理和存储数字密钥。 这些设备直接连接到计算机或网络服务器。

Adobe Experience Manager Forms可以使用存储在HSM或etoken上的凭据来eSign或将服务器端数字签名应用到文档。 要将HSM或令牌设备与AEM Forms结合使用，请执行以下操作：

1. 启用DocAssurance服务。
1. 为Reader扩展设置证书。
1. 在AEM Web Console中为HSM或etoken设备创建别名。
1. 使用文档保障服务API，使用存储在设备上的数字密钥对文档进行签名或验证。

## 在使用AEM Forms配置HSM或etoken设备之前 {#configurehsmetoken}

* 安装 [AEM Forms附加组件](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) 包。
* 在与AEM服务器相同的计算机上安装和配置HSM或etoken客户端软件。 客户端软件需要与HSM和令牌设备通信。
* (仅限Microsoft Windows)将JAVA_HOME_32环境变量设置为指向安装Java 8开发工具包(JDK 8)的32位版本的目录。 目录的默认路径为C:\Program Files(x86)\Java\jdk&lt;version>
* (仅限OSGi上的AEM Forms)在信任存储中安装根证书。 需要验证已签名的PDF

>[!NOTE]
>
>在Microsoft Windows上，仅支持32位LunaSA或EToken客户端。

## 启用DocAssurance服务 {#configuredocassurance}

默认情况下，未启用DocAssurance服务。 请执行以下步骤以启用服务：

1. 停止AEM Forms环境的创作实例。

1. 打开 [AEM_root]\crx-quickstart\conf\sling.properties文件进行编辑。

   >[!NOTE]
   >
   >如果您使用 [AEM_root]\crx-quickstart\bin\start.bat文件以启动AEM实例，然后打开 [AEM_root]\crx-quickstart\sling.properties文件进行编辑。

1. 将以下属性添加或替换到sling.properties文件：

   ```shell
   sling.bootdelegation.sun=sun.*,com.sun.*,sun.misc.*
   sling.bootdelegation.ibm=com.ibm.xml.*,com.ibm.*
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. 保存并关闭sling.properties文件。
1. 重新启动AEM实例。

## 设置Reader扩展的证书 {#set-up-certificates-for-reader-extensions}

执行以下步骤来设置证书：

1. 以管理员身份登录到AEM创作实例。

1. 单击&#x200B;**Adobe Experience Manager** 中。 转到 **工具** >  **安全性** >  **用户**.
1. 单击 **name** 字段。 的 **编辑用户设置** 页面。
1. 在AEM创作实例中，证书位于KeyStore中。 如果您之前尚未创建KeyStore，请单击 **创建KeyStore** 并为KeyStore设置新密码。 如果服务器已包含KeyStore，请跳过此步骤。

1. 在 **编辑用户设置** 页面，单击 **管理KeyStore**.

1. 在KeyStore管理对话框中，展开 **从密钥存储文件添加私钥** 选项，并提供别名。 别名用于执行Reader扩展操作。
1. 要上载证书文件，请单击 **选择密钥存储文件** 并上传 `.pfx` 文件。
1. 添加 **密钥存储密码**,**私钥密码**&#x200B;和 **私钥别名** 与证书关联到相应字段的ID。 单击 **提交**.

   >[!NOTE]
   >
   >确定P **私钥别名** 在证书中，可以使用Java密钥工具命令： `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

   >[!NOTE]
   >
   >在 **密钥存储密码** 和 **私钥密码** 字段，指定随证书文件提供的密码。

>[!NOTE]
>
>对于OSGi上的AEM Forms，要验证已签名的PDF（信任存储中安装的根证书）。

>[!NOTE]
>
>迁移到生产环境时，请将您的评估凭据替换为生产凭据。 在更新过期或评估凭据之前，请确保删除旧的Reader扩展凭据。

## 为设备创建别名 {#configuredeviceinaemconsole}

别名包含HSM或令牌需要的所有参数。 执行下面列出的说明，为eSign或数字签名使用的每个HSM或etoken凭据创建别名：

1. 打开AEM控制台。 AEM控制台的默认URL为https://&lt;host>:&lt;port>/system/console/configMgr
1. 打开 **HSM凭据配置服务** 并为以下字段指定值：

   * **凭据别名**:指定用于标识别名的字符串。 此值用作某些数字签名操作（如签名字段操作）的属性。
   * **DLL路径**:指定服务器上HSM或etoken客户端库的完全限定路径。 例如， C:\Program Files\LunaSA\cryptoki.dll。 在群集环境中，此路径对于群集中的所有服务器都必须相同。
   * **HSM针**:指定访问设备密钥所需的密码。
   * **HSM插槽Id**:指定整数类型的插槽标识符。 插槽ID是逐个客户端设置的。 如果将第二台计算机注册到不同的分区（例如，同一HSM设备上的HSMPART2），则插槽1与客户端的HSMPART2分区相关联。

   >[!NOTE]
   >
   >在配置Etoken时，为HSM插槽ID字段指定一个数值。 要使签名操作正常工作，需要一个数值。

   * **证书SHA1**:为您使用的凭据指定公钥(.cer)文件的SHA1值（指纹）。 确保SHA1值中不使用空格。 如果您使用的是物理证书，则不需要此证书。
   * **HSM设备类型**:选择HSM（Luna或其他）或eToken设备的制造商。

   单击“**保存**”。已为AEM Forms配置硬件安全模块。 现在，您可以将硬件安全模块与AEM Forms一起使用来签署或验证文档。

## 使用文档保障服务API，使用存储在设备上的数字密钥对文档进行签名或认证  {#programatically}

以下示例代码使用HSM或etoken来签署或验证文档。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.ByteArrayInputStream;
import java.io.IOException;
import java.io.InputStream;

import javax.jcr.Binary;
import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 * Digital signatures can be applied to PDF documents to provide a level of security. Digital signatures, like handwritten signatures, provide a means by which signers
 * identify themselves and make statements about a document. The technology used to digitally sign documents helps to ensure that both the signer and recipients are clear
 * about what was signed and confident that the document was not altered since it was signed.
 *
 * PDF documents are signed by means of public-key technology. A signer has two keys: a public key and a private key. The private key is stored in a user's credential that
 * must be available at the time of signing. The public key is stored in the user's certificate that must be available to recipients to validate the signature. Information
 * about revoked certificates is found in certificate revocation lists (CRLs) and Online Certificate Status Protocol (OCSP) responses distributed by Certificate Authorities (CAs).
 * The time of signing can be obtained from a trusted source known as a Timestamping Authority.
 *
 * The following Java code example digitally signs a PDF document that is based on a PDF file.
 * The alias that is specified for the security credential is secure, and revocation checking is performed.
 * Because no CRL or OCSP server information is specified, the server information is obtained from the certificate used to
 * digitally sign the PDF document
 *
 * PreRequisites - Digital certificate for signing the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=Sign.class)
public class Sign{
 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at JCR node
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void signExtend(String inputFile, String outputFile, String alias) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  Document inDoc = new Document(inputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you don't want to use that service
             //as we don't want encryption in this case, passing null for Encryption Options
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, null, getSignatureOptions(alias,resourceResolver),null,null);
        }
  catch(Exception e){
   e.printStackTrace();
  }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        //flush the output document contents to JCR Node
  flush(outDoc, outputFile);

 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getSignatureOptions(String alias, ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.SIGN);

  //field to sign
  String fieldName = "Signature1" ;

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;

        //Reason for signing/certifying
        String reason = "Test Reason";

        //location of the signer
        String location = "Test Location";

        //contact info of the signer
        String contactInfo = "Test Contact";

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);

        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr, true));
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
    /**
     * This method copies the data from {@code Document}, to the specified file at the given resourcePath.
     * @param doc
     * @param resourcePath
     * @throws IOException
     */
    private void flush(Document doc, String resourcePath) throws IOException {
   //extracts the byte data from Document
   byte[] output = doc.getInlineData();
   Binary opBin;
   Session adminSession = null;
      try {
         adminSession = slingRepository.loginAdministrative(null);

         //get access to the specific node
         //here we are assuming that node exists
           Node node = adminSession.getNode(resourcePath);

           //convert byte[] to Binary
           opBin = adminSession.getValueFactory().createBinary((InputStream)new ByteArrayInputStream(output));

           //set the Binary data value to node's jcr:data
           node.getNode("jcr:content").getProperty("jcr:data").setValue(opBin);
      } catch (RepositoryException e) {

      }
      finally{

       if(adminSession != null && adminSession.isLive()){
        try {
      adminSession.save();
      adminSession.logout();
     } catch (RepositoryException e) {

     }

             }
      }

  }
}
```

如果您从AEM 6.0 Form或AEM 6.1 Forms升级，并且在以前的版本中使用了DocAssurance服务，则：

* 要在没有HSM或令牌设备的情况下使用DocAssurance服务，请继续使用现有代码。
* 要将DocAssurance服务与HSM或令牌设备一起使用，请将您现有的CredentialContext对象代码替换为下面列出的API。

```java
/**
  *
  * @param credentialAlias alias of the PKI Credential stored in CQ Key Store or
  * the alias of the HSM Credential configured using HSM Credentials Configuration Service.
  * @param resourceResolver corresponding to the user with the access to the key store and trust store.
  * @param isHSMCredential if the alias is corresponding to HSM Credential.
  */
 public CredentialContext(String credentialAlias, ResourceResolver resourceResolver, boolean isHSMCredential);
```

有关DocAssurance服务的API和示例代码的详细信息，请参阅 [以编程方式使用AEM Document Services](/help/forms/using/aem-document-services-programmatically.md).
