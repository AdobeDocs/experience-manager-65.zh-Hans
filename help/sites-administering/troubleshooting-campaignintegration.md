---
title: Adobe Campaign Classic集成疑难解答
description: 了解如何对Adobe Campaign Classic集成问题进行故障诊断。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 317bab41-3504-4e46-9ddc-72e291a34e06
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---


# Adobe Campaign Classic集成疑难解答{#troubleshooting-your-adobe-campaign-classic-integration}

了解如何对Adobe Campaign Classic (ACC)集成问题进行故障诊断。

以下故障诊断提示有助于解决在将AEM与ACC集成时可能遇到的最常见问题。

## 一般疑难解答提示 {#general-troubleshooting-tips}

检查两个解决方案(AEM > Adobe Campaign Classic、Adobe Campaign Classic > AEM)是否发送和接收HTTP调用。 此提示可帮助您避免防火墙/SSL问题。

* 对于AEM功能，您可以看到从AEM创作界面请求了JSON调用
   * 这些调用不应导致HTTP-500错误。
   * 如果您看到HTTP-500错误，请查看`error.log`以了解更多信息。
* 提高AEM中促销活动类的调试级别也有助于排除问题。

## 如果连接失败 {#when-the-connection-fails}

检查您是否已在Adobe Campaign Classic中配置&#x200B;**`aemserver`**&#x200B;运算符。

## 如果图像未显示在Adobe Campaign Classic控制台中 {#if-images-do-not-appear-in-the-adobe-campaign-console}

检查HTML源并验证是否可以从客户端计算机打开该URL。 如果URL中包含`localhost:4503`，请在AEM创作实例上更改Day CQ Link Externalizer的配置。 使其指向可从Adobe Campaign Classic控制台计算机访问的发布实例。

请参阅[配置外部化器。](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## 如果无法从AEM连接到Adobe Campaign Classic  {#if-you-cannot-connect-from-aem-to-adobe-campaign}

在Adobe Campaign Classic中查找以下错误消息。

* `No datasource defined in the instance 'default'.`

* `Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

要解决此问题，请在`$CAMPAIGN_HOME/conf/config-<instance-name>.xml`中更改以下内容：

* `<dataStore hosts="*" lang="en_GB">`

## 如果Adobe Campaign Classic对话框中未显示任何数据 {#if-no-data-displays-in-the-adobe-campaign-dialog}

在Adobe Campaign Classic中，请确保端口号后面没有尾随斜杠(`/`)。

![Adobe Campaign Classic — 确保端口号](assets/chlimage_1-149.png)后面没有尾随斜杠

## 如果收到有关setlocale的警告 {#if-you-get-a-warning-about-your-setlocale}

启动Adobe Campaign Classic的Apache HTTPD服务时，您可能会看到错误`Warning: setlocale: LC_CTYPE cannot change locale`

确保您的Adobe Campaign Classic服务器上安装了`en_CA.ISO-8859-15 locale`。

* 您可以使用`local -a`检查它是否已安装。
* 如果未安装，您可以修补`/usr/local/neolane/nl6/env.sh`脚本并将区域设置更改为已安装的区域设置。

## 如果在编译脚本“get_nms_amcGetSeedMetaData_jssp”时出错 {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

如果您在AEM日志文件中看到以下错误消息：

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

在Adobe Campaign Classic服务器上使用以下解决方法。

1. 打开文件`$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js`
1. 修改方法`amcGetSeedMetaData`的第467行
1. 将`label : [inclView.@label](mailto:inclView.@label)`更改为`label : String([inclView.@label](mailto:inclView.@label))`
1. 保存。
1. 重新启动服务器。

## 如果Adobe Campaign Classic在单击“同步”按钮时显示错误 {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

单击Adobe Campaign Classic中的&#x200B;**同步**&#x200B;按钮时，您可能会看到以下错误。

* `Error while executing the method 'aemListContent' of service [nms:delivery](https://nmsdelivery/)`

要解决此问题，请确保可以从计算机访问在Adobe Campaign Classic中的&#x200B;**外部帐户**&#x200B;中配置的AEM连接URL。

从`localhost`切换到URL的IP地址通常可以解决此问题。

## 如果您收到“无法解析XTK日期+时间”的“未定义”错误 {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

在AEM中单击&#x200B;**同步**&#x200B;后，您可能会收到页面上的脚本已发生的错误。

* `Cannot parse XTK Date+Time 'undefined': not a valid XTK value.`

如果AEM实例上存在过期的Adobe Campaign Classic信息，则会发生此错误。 您可以通过执行以下操作来解决此问题：

1. 删除AEM上的所有Adobe Campaign Classic集成配置。
1. 重建集成。
1. 创建模板。

## 如果与SSL的连接在设置Cloud Service时显示错误 {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

如果您在AEM的`error.log`中看到以下内容，请向Adobe Campaign支持团队提交票证。

```text
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

## 如果您在同步对话框中看到HTTP而不是预期的HTTPS链接 {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

尝试同步Adobe Campaign Classic交付中的内容时，AEM会返回新闻稿列表。 但是，列表中新闻稿的URL可能是HTTP地址而不是HTTPS。 选择列表中的项目之一时出现错误。 以下设置可能发生此错误。

* 使用https托管Adobe Campaign以与AEM作者进行通信
* 反向代理终止SSL
* 内部部署AEM创作实例

要解决此问题，请执行以下操作：

* 必须将AEM Dispatcher或反向代理配置为将原始协议作为标头传递。
* AEM OSGi配置中的&#x200B;**Apache Felix Http服务SSL过滤器**&#x200B;必须使用所需的标头设置进行配置。
   * `https://<host>:<port>/system/console/configMgr`
   * 请参阅[https://github.com/apache/felix-dev/tree/master/http#using-the-ssl-filter](https://github.com/apache/felix-dev/tree/master/http#using-the-ssl-filter)

## 无法在页面属性中选择自定义模板 {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

在AEM for Adobe Campaign Classic中创建邮件模板时，必须在模板的`jcr:content`节点中包含值为`mapRecipient`的属性`acMapping`。 如果不这样做，则无法在AEM的&#x200B;**页面属性**&#x200B;中选择Adobe Campaign Classic模板。 该字段显示为禁用。

## 如果您在AEM日志中看到错误“com.day.cq.mcm.campaign.servlets.util.ParameterMapper” {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

使用自定义模板时，您可能会在AEM日志中看到错误`com.day.cq.mcm.campaign.servlets.util.ParameterMapper`。

如果将`acMapping`属性设置为`recipient.firstName`以外的值，则在Adobe Campaign管理器中创建空白值，则会出现此错误。

如果出现此错误，请从[包共享](/help/sites-administering/package-manager.md#package-share)安装AEM功能包6576。
