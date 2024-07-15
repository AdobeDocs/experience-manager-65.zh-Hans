---
title: 为JBoss应用程序服务器配置SSL
description: 了解如何为JBoss应用程序服务器配置SSL。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8eb4f691-a66b-498e-8114-307221f63718
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# 为JBoss应用程序服务器配置SSL {#configuring-ssl-for-jboss-application-server}

要在JBoss Application Server上配置SSL，您需要用于身份验证的SSL凭据。 您可以使用Java keytool创建凭据或请求并从证书颁发机构(CA)导入凭据。 然后，必须在JBoss上启用SSL。

可以使用包含创建密钥库所需的所有信息的单个命令来运行keytool。

在此过程中：

* `[appserver root]`是运行AEM表单的应用程序服务器的主目录。
* `[type]`是一个文件夹名称，该名称会因您执行的安装类型而异。

## 创建SSL凭据 {#create-an-ssl-credential}

1. 在命令提示符下，导航到&#x200B;*[JAVA HOME]*/bin并键入以下命令以创建凭据和密钥库：

   `keytool -genkey -dname "CN=`*主机名* `, OU=`*组名* `, O=`*公司名称* `,L=`*城市名称* `, S=`*省/州* `, C=`国家/地区代码“`-alias "AEMForms Cert"` `-keyalg RSA -keypass`*key_password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >将`[JAVA_HOME]`替换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。 主机名是应用程序服务器的完全限定域名。

1. 提示输入密码时输入`keystore_password`。 密钥库的密码和密钥必须相同。

   >[!NOTE]
   >
   >在此步骤输入的`keystore_password` *可能与您在步骤1中输入的密码(key_password)相同，也可能不同。*

1. 通过键入以下命令之一，将&#x200B;*keystorename*.keystore复制到`[appserver root]/server/[type]/conf`目录：

   * (Windows Single Server) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * （Windows Server群集）副本`keystorename.keystore[appserver root]\domain\configuration`
   * （Linux单服务器） `cp keystorename.keystore [appserver root]/standalone/configuration`
   * （Linux服务器群集） `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. 通过键入以下命令导出证书文件：

   * （单个服务器） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * （服务器群集） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. 在提示输入密码时输入&#x200B;*keystore_password*。
1. 通过键入以下命令，将AEMForms_cert.cer文件复制到&#x200B;*[appserver root] \conf*&#x200B;目录：

   * (Windows Single Server) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * （Windows Server群集） `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * （Linux单服务器） `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * （Linux服务器群集） `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. 通过键入以下命令查看证书的内容：

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. 要提供对`[JAVA_HOME]\jre\lib\security`中cacerts文件的写入权限，请执行以下任务（如有必要）：

   * (Windows)右键单击cacerts文件并选择“属性”，然后取消选择“只读”属性。
   * (Linux)类型`chmod 777 cacerts`

1. 通过键入以下命令导入证书：

   `keytool -import -alias "AEMForms Cert" -file`*AEMForms_cert* `.cer -keystore`*JAVA_HOME* `\jre\lib\security\cacerts`

1. 键入`changeit`作为密码。 此密码是Java安装的默认密码，系统管理员可能已对其进行更改。
1. 当系统提示`Trust this certificate? [no]`时，键入`yes`。 此时会显示确认“Certificate waded to keystore”。
1. 如果通过SSL从Workbench连接，请在Workbench计算机上安装证书。
1. 在文本编辑器中，打开以下文件进行编辑：

   * 单服务器 — `[appserver root]`/standalone/configuration/lc_&lt;dbname/turnkey>.xml

   * 服务器群集 — `[appserver root]`/domain/configuration/host.xml

   * 服务器群集 — `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **对于lc_&lt;dbaname/tunkey>.xml文件中的单个服务器**，在&lt;security-realms>部分后添加以下内容：

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   找到以下代码后存在的`<server>`部分：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   将以下内容添加到上述代码后存在的&lt;server>部分中：

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **对于所有节点上的[appserver根]\domain\configuration\host.xml中的服务器群集**，在&lt;security-realms>部分后添加以下内容：

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   在服务器群集的主节点上的[appserver root]\domain\configuration\domain_&lt;dbname>.xml中，找到以下代码后面存在的&lt;server>部分：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   将以下内容添加到上述代码后存在的&lt;server>部分中：

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. 将`keystoreFile`属性和`keystorePass`属性的值更改为您在创建密钥库时指定的密钥库密码。
1. 重新启动应用程序服务器：

   * 对于统包安装：

      * 在Windows控制面板中，单击“管理工具”，然后单击“服务”。
      * 选择适用于Adobe Experience Manager表单的JBoss。
      * 选择操作>停止。
      * 等待服务的状态显示为已停止。
      * 选择操作>开始。

   * 对于Adobe预配置或手动配置的JBoss安装：

      * 在命令提示符下，导航到&#x200B;*`[appserver root]`*/bin。
      * 输入以下命令停止服务器：

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`

      * 等待JBoss进程完全关闭（当JBoss进程将控制权返回到在其中启动它的终端时）。
      * 输入以下命令启动服务器：

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`

1. 要使用SSL访问管理控制台，请在Web浏览器中键入`https://[host name]:'port'/adminui`：

   JBoss的默认SSL端口为8443。 从此处，在访问AEM表单时指定此端口。

## 从CA请求凭据 {#request-a-credential-from-a-ca}

1. 在命令提示符下，导航到&#x200B;*[JAVA HOME]*/bin并键入以下命令以创建密钥库和密钥：

   `keytool -genkey -dname "CN=`*主机名* `, OU=`*组名* `, O=`*公司名称* `, L=`*城市名称* `, S=`*省/市/自治区* `, C=`*国家/地区代码*“`-alias "AEMForms Cert"` `-keyalg RSA -keypass`-*key_password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >将&#x200B;*`[JAVA_HOME]`*&#x200B;替换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。

1. 键入以下命令以生成要发送到证书颁发机构的证书请求：

   `keytool -certreq -alias` “AEMForms证书”`-keystore`*keystorename* `.keystore -file`*AEMFormscertRequest.csr*

1. 当您完成证书文件请求后，请完成下一个过程。

## 使用从CA获得的凭据启用SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. 在命令提示符下，导航到&#x200B;*`[JAVA HOME]`*/bin并键入以下命令以导入已与CSR签名的CA的根证书：

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   如果根证书不在浏览器中，也将其导入浏览器。

   >[!NOTE]
   >
   >将&#x200B;*`[JAVA_HOME]`替换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。*

1. 在命令提示符下，导航到&#x200B;*`[JAVA HOME]`*/bin并键入以下命令以将凭据导入密钥库中：

   `keytool -import -trustcacerts -file`*CACertificateName* `.crt -keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >* 将`[JAVA_HOME]`替换为安装JDK的目录，并将斜体文本替换为与您的环境对应的值。
   >* 导入的CA签名证书将替换自签名公共证书（如果存在）。

1. 完成创建SSL凭据的步骤13 - 18。
