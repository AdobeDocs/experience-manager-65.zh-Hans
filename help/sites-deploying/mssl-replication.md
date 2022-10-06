---
title: 使用互相SSL复制
seo-title: Replicating Using Mutual SSL
description: 了解如何配置AEM，以便创作实例上的复制代理使用双向SSL(MSSL)连接发布实例。 使用MSSL，发布实例上的复制代理和HTTP服务使用证书来相互进行身份验证。
seo-description: Learn how to configure AEM so that a replication agent on the author instance uses mutual SSL (MSSL) to connect with the publish instance. Using MSSL, the replication agent and the HTTP service on the publish instance use certificates to authenticate each other.
uuid: f4bc5e61-a58c-4fd2-9a24-b31e0c032c15
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 8bc307d9-fa5c-44c0-bff9-2d68d32a253b
feature: Configuring
exl-id: 0a8d7831-d076-45cf-835c-8063ee13d6ba
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 3%

---

# 使用互相SSL复制{#replicating-using-mutual-ssl}

配置AEM，以便创作实例上的复制代理使用互相SSL(MSSL)与发布实例连接。 使用MSSL，发布实例上的复制代理和HTTP服务使用证书来相互进行身份验证。

为复制配置MSSL涉及执行以下步骤：

1. 创建或获取创作实例和发布实例的私钥和证书。
1. 在创作实例和发布实例上安装密钥和证书：

   * 作者：作者的私钥和Publish的证书。
   * 发布：Publish的私钥和作者证书。 证书与通过复制代理验证的用户帐户关联。

1. 在发布实例上配置基于Jetty的HTTP服务。
1. 配置复制代理的传输和SSL属性。

![chlimage_1-64](assets/chlimage_1-64.png)

您必须确定执行复制的用户帐户。 在发布实例上安装受信任的作者证书时，该证书与此用户帐户相关联。

## 获取或创建MSSL的凭据 {#obtaining-or-creating-credentials-for-mssl}

对于创作实例和发布实例，您需要私钥和公共证书：

* 私钥必须包含在pkcs#12或JKS格式中。
* 证书必须包含在pkcs#12或JKS格式中。 此外，还可以将“CER”格式包含的证书添加到Granite Truststore。
* 证书可以由认可的CA自签名或签名。

### JKS格式 {#jks-format}

以JKS格式生成私钥和证书。 私钥存储在KeyStore文件中，证书存储在TrustStore文件中。 使用 [Java `keytool`](https://docs.oracle.com/javase/7/docs/technotes/tools/solaris/keytool.html) 创建和。

使用Java执行以下步骤 `keytool` 要创建私钥和凭据，请执行以下操作：

1. 在KeyStore中生成私钥对。
1. 创建或获取证书：

   * 自签名：从KeyStore导出证书。
   * CA签名：生成证书请求并将其发送到CA。

1. 将证书导入TrustStore。

请按照以下步骤为创作实例和发布实例创建私钥和自签名证书。 相应地，对命令选项使用不同的值。

1. 打开命令行窗口或终端。 要创建私钥对 — 公钥对，请使用下表中的选项值输入以下命令：

   ```shell
   keytool -genkeypair -keyalg RSA -validity 3650 -alias alias -keystore keystorename.keystore  -keypass key_password -storepass  store_password -dname "CN=Host Name, OU=Group Name, O=Company Name,L=City Name, S=State, C=Country_ Code"
   ```

   | 选项 | 创作 | 发布 |
   |---|---|---|
   | -alias | 作者 | 发布 |
   | -keystore | author.keystore | publish.keystore |

1. 要导出证书，请使用下表中的选项值输入以下命令：

   ```shell
   keytool -exportcert -alias alias -file cert_file -storetype jks -keystore keystore -storepass store_password
   ```

   | 选项 | 创作 | 发布 |
   |---|---|---|
   | -alias | 作者 | 发布 |
   | -file | author.cer | publish.cer |
   | -keystore | author.keystore | publish.keystore |

### pkcs#12格式 {#pkcs-format}

以pkcs#12格式生成私钥和证书。 使用 [openSSL](https://www.openssl.org/) 来生成它们。 请按照以下过程生成私钥和证书请求。 要获取证书，请使用您的私钥对请求进行签名（自签名证书），或将请求发送到CA。 然后，生成包含私钥和证书的pkcs#12存档。

1. 打开命令行窗口或终端。 要创建私钥，请使用下表中的选项值输入以下命令：

   ```shell
   openssl genrsa -out keyname.key 2048
   ```

   | 选项 | 创作 | 发布 |
   |---|---|---|
   | -out | author.key | publish.key |

1. 要生成证书请求，请使用下表中的选项值输入以下命令：

   ```shell
   openssl req -new -key keyname.key -out key_request.csr
   ```

   | 选项 | 创作 | 发布 |
   |---|---|---|
   | -key | author.key | publish.key |
   | -out | author_request.csr | publish_request.csr |

   签署证书请求或将请求发送到CA。

1. 要对证书请求进行签名，请使用下表中的选项值输入以下命令：

   ```shell
   openssl x509 -req -days 3650 -in key_request.csr -signkey keyname.key -out certificate.cer
   ```

   | 选项 | 创作 | 发布 |
   |---|---|---|
   | -signkey | author.key | publish.key |
   | -in | author_request.csr | publish_request.csr |
   | -out | author.cer | publish.cer |

1. 要将私钥和签名证书添加到pkcs#12文件，请使用下表中的选项值输入以下命令：

   ```shell
   openssl pkcs12 -keypbe PBE-SHA1-3DES -certpbe PBE-SHA1-3DES -export -in certificate.cer -inkey keyname.key -out pkcs12_archive.pfx -name "alias"
   ```

   | 选项 | 创作 | 发布 |
   |---|---|---|
   | -inkey | author.key | publish.key |
   | -out | author.pfx | publish.pfx |
   | -in | author.cer | publish.cer |
   | -name | 作者 | 发布 |

## 在作者上安装私钥和TrustStore {#install-the-private-key-and-truststore-on-author}

在创作实例上安装以下项目：

* 创作实例的私钥。
* 发布实例的证书。

要执行以下过程，您必须以创作实例的管理员身份登录。

### 安装创作私钥 {#install-the-author-private-key}

1. 打开创作实例的“用户管理”页面。 ([http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html))
1. 要打开您的用户帐户的属性，请单击或点按您的用户名。
1. 如果“Create KeyStore”（创建密钥存储）链接出现在“Account Settings”（帐户设置）区域，请单击该链接。 配置密码，然后单击“确定”。
1. 在“帐户设置”区域，单击“管理密钥库”。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 单击密钥存储文件中的添加私钥。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 单击“选择密钥存储文件”，然后浏览并选择author.keystore文件或author.pfx文件（如果使用pkcs#12），然后单击“打开”。
1. 输入密钥存储的别名和密码。 输入私钥的别名和密码，然后单击“提交”。
1. 关闭KeyStore管理对话框。

   ![chlimage_1-67](assets/chlimage_1-67.png)

### 安装发布证书 {#install-the-publish-certificate}

1. 打开创作实例的“用户管理”页面。 ([http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html))
1. 要打开您的用户帐户的属性，请单击或点按您的用户名。
1. 如果“Create TrustStore”（创建信任存储）链接出现在“Account Settings”（帐户设置）区域，请单击该链接，为TrustStore创建密码，然后单击“OK”（确定）。
1. 在“帐户设置”区域，单击“管理信任存储”。
1. 单击“从CER文件添加证书”。

   ![chlimage_1-68](assets/chlimage_1-68.png)

1. 清除将证书映射到用户选项。 单击选择证书文件，选择publish.cer，然后单击打开。
1. 关闭TrustStore管理对话框。

   ![chlimage_1-69](assets/chlimage_1-69.png)

## 在发布时安装私钥和TrustStore {#install-private-key-and-truststore-on-publish}

在发布实例上安装以下项目：

* 发布实例的私钥。
* 创作实例的证书。 将证书与用于执行复制请求的用户关联。

要执行以下过程，您必须以发布实例的管理员身份登录。

### 安装发布私钥 {#install-the-publish-private-key}

1. 打开发布实例的“用户管理”页面。 ([http://localhost:4503/libs/granite/security/content/useradmin.html](http://localhost:4503/libs/granite/security/content/useradmin.html))
1. 要打开您的用户帐户的属性，请单击或点按您的用户名。
1. 如果“Create KeyStore”（创建密钥存储）链接出现在“Account Settings”（帐户设置）区域，请单击该链接。 配置密码，然后单击“确定”。
1. 在“帐户设置”区域，单击“管理密钥库”。
1. 单击密钥存储文件中的添加私钥。
1. 单击“选择密钥存储文件”，然后浏览并选择publish.keystore文件或publish.pfx文件（如果使用pkcs#12），然后单击“打开”。
1. 输入密钥存储的别名和密码。 输入私钥的别名和密码，然后单击“提交”。
1. 关闭KeyStore管理对话框。

### 安装作者证书 {#install-the-author-certificate}

1. 打开发布实例的“用户管理”页面。 ([http://localhost:4503/libs/granite/security/content/useradmin.html](http://localhost:4503/libs/granite/security/content/useradmin.html))
1. 找到用于执行复制请求的用户帐户，然后单击或点按用户名。
1. 如果“Create TrustStore”（创建信任存储）链接出现在“Account Settings”（帐户设置）区域，请单击该链接，为TrustStore创建密码，然后单击“OK”（确定）。
1. 在“帐户设置”区域，单击“管理信任存储”。
1. 单击“从CER文件添加证书”。
1. 确保选中将证书映射到用户选项。 单击选择证书文件，选择author.cer，然后单击打开。
1. 单击提交，然后关闭TrustStore管理对话框。

## 在发布时配置HTTP服务 {#configure-the-http-service-on-publish}

在发布实例上配置基于Apache Felix Jetty的HTTP服务的属性，以便它在访问Granite Keystore时使用HTTPS。 服务的PID是 `org.apache.felix.http`.

下表列出了在使用Web控制台时需要配置的OSGi属性。

| Web控制台上的属性名称 | OSGi 属性名称 | 值 |
|---|---|---|
| 启用HTTPS | org.apache.felix.https.enable | true |
| 启用HTTPS以使用Granite KeyStore | org.apache.felix.https.use.granite.keystore | true |
| HTTPS 端口 | org.osgi.service.http.port.secure | 8443（或其他所需端口） |
| 客户端证书 | org.apache.felix.https.clientcertificate | &quot;需要客户端证书&quot; |

## 在创作时配置复制代理 {#configure-the-replication-agent-on-author}

在创作实例上配置复制代理，以在连接到发布实例时使用HTTPS协议。 有关配置复制代理的完整信息，请参阅 [配置复制代理](/help/sites-deploying/replication.md#configuring-your-replication-agents).

要启用MSSL，请根据下表在“传输”选项卡上配置属性：

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>值</th>
  </tr>
  <tr>
   <td>URI</td>
   <td><p>https://server_name:SSL_port/bin/receive?sling:authRequestLogin=1</p> <p>例如：</p> <p>http://localhost:8443/bin/receive?sling:authRequestLogin=1</p> </td>
  </tr>
  <tr>
   <td>用户</td>
   <td>无值</td>
  </tr>
  <tr>
   <td>密码</td>
   <td>无值</td>
  </tr>
  <tr>
   <td>SSL</td>
   <td>客户端身份验证</td>
  </tr>
 </tbody>
</table>

![chlimage_1-70](assets/chlimage_1-70.png)

配置复制代理后，请测试连接以确定MSSL配置是否正确。

```xml
29.08.2014 14:02:46 - Create new HttpClient for Default Agent
29.08.2014 14:02:46 - * HTTP Version: 1.1
29.08.2014 14:02:46 - * Using Client Auth SSL configuration *
29.08.2014 14:02:46 - adding header: Action:Test
29.08.2014 14:02:46 - adding header: Path:/content
29.08.2014 14:02:46 - adding header: Handle:/content
29.08.2014 14:02:46 - deserialize content for delivery
29.08.2014 14:02:46 - No message body: Content ReplicationContent.VOID is empty
29.08.2014 14:02:46 - Sending POST request to http://localhost:8443/bin/receive?sling:authRequestLogin=1
29.08.2014 14:02:46 - sent. Response: 200 OK
29.08.2014 14:02:46 - ------------------------------------------------
29.08.2014 14:02:46 - Sending message to localhost:8443
29.08.2014 14:02:46 - >> POST /bin/receive HTTP/1.0
29.08.2014 14:02:46 - >> Action: Test
29.08.2014 14:02:46 - >> Path: /content
29.08.2014 14:02:46 - >> Handle: /content
29.08.2014 14:02:46 - >> Referer: about:blank
29.08.2014 14:02:46 - >> Content-Length: 0
29.08.2014 14:02:46 - >> Content-Type: application/octet-stream
29.08.2014 14:02:46 - --
29.08.2014 14:02:46 - << HTTP/1.1 200 OK
29.08.2014 14:02:46 - << Connection: Keep-Alive
29.08.2014 14:02:46 - << Server: Day-Servlet-Engine/4.1.64
29.08.2014 14:02:46 - << Content-Type: text/plain;charset=utf-8
29.08.2014 14:02:46 - << Content-Length: 26
29.08.2014 14:02:46 - << Date: Fri, 29 Aug 2014 18:02:46 GMT
29.08.2014 14:02:46 - << Set-Cookie: login-token=3529326c-1500-4888-a4a3-93d299726f28%3ac8be86c6-04bb-4d18-80d6-91278e08d720_98797d969258a669%3acrx.default; Path=/; HttpOnly; Secure
29.08.2014 14:02:46 - << Set-Cookie: cq-authoring-mode=CLASSIC; Path=/; Secure
29.08.2014 14:02:46 - <<
29.08.2014 14:02:46 - << R
29.08.2014 14:02:46 - << eplicationAction TEST ok.
29.08.2014 14:02:46 - Message sent.
29.08.2014 14:02:46 - ------------------------------------------------
29.08.2014 14:02:46 - Replication (TEST) of /content successful.
Replication test succeeded
```
