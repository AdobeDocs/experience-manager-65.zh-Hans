---
title: 与Adobe Target集成的先决条件
description: 了解与Adobe Target集成的先决条件。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 7%

---

# 与Adobe Target集成的先决条件{#prerequisites-for-integrating-with-adobe-target}

作为 [AEM与Adobe Target的集成](/help/sites-administering/target.md)，您需要向Adobe Target注册，配置复制代理，并在发布节点上配置安全活动设置。

## 在Adobe Target中注册 {#registering-with-adobe-target}

要将AEM与Adobe Target集成，您必须拥有有效的Adobe Target帐户。 此帐户必须具有 **审批者** 最低级别权限。 当您注册Adobe Target时，您会收到一个客户端代码。 您需要客户端代码以及Adobe Target登录名和密码才能将AEM连接到Adobe Target。

客户端代码在调用Adobe Target服务器时标识Adobe Target客户帐户。

>[!NOTE]
>
>您的帐户还必须由Target团队启用才能使用该集成。
>
>如果不是这种情况，请联系 [Adobe客户关怀](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html).

## 启用目标复制代理 {#enabling-the-target-replication-agent}

测试和目标 [复制代理](/help/sites-deploying/replication.md) 必须在创作实例上启用。 请注意，如果您使用 [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) 用于安装AEM的运行模式。 有关保护生产环境的更多信息，请参见 [安全核对清单](/help/sites-administering/security-checklist.md).

1. 在AEM主页上，单击 **工具** > **部署** > **复制**.
1. 单击 **作者代理**.
1. 单击 **测试和定位（测试和定位）** 复制代理，然后单击 **编辑**.
1. 选择启用选项，然后单击 **确定**.

   >[!NOTE]
   >
   >在配置Test and Target复制代理时，请在 **传输** 选项卡，URI默认设置为 **tnt:///**. 不要将此URI替换为 **https://admin.testandtarget.omniture.com**.
   >
   >如果您尝试测试与的连接 **tnt:///**，会引发错误。 这是预期行为，因为此URI仅供内部使用；请勿与一起使用 **测试连接**.

## 保护活动设置节点 {#securing-the-activity-settings-node}

确保发布实例中的活动设置节点 **cq:ActivitySettings** 安全，以使其不可由普通用户访问。该活动设置节点应当只能由负责将活动同步到 Adobe Target 的服务访问。

此 **cq：ActivitySettings** 节点在CRXDE lite中可用，位于 `/content/campaigns/*nameofbrand*`* *在活动jcr：content节点下；* *例如， `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. 此节点仅在定向组件后创建。

此 **cq：ActivitySettings** 节点在活动的jcr：content下受以下ACL保护：

* 拒绝所有人的所有
* 允许“target-activity-authors”使用jcr：read，rep：write（作者是此组的一名现成成员）
* 允许jcr：read，rep：write用于“targetservice”

这些设置可确保普通用户无权访问节点属性。 在创作实例和发布实例上使用相同的ACL。 请参阅 [用户管理和安全性](/help/sites-administering/security.md) 以了解更多信息。

## 配置AEM链接外部化器 {#configuring-the-aem-link-externalizer}

在Adobe Target中编辑活动时，URL指向 **localhost** 除非您更改了AEM创作节点上的URL。 如果希望导出的内容指向特定的，则可以配置AEM Link Externalizer *发布* 域。

>[!NOTE]
>
>另请参阅 [添加云配置](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration).

要配置AEM外部化器，请执行以下操作：

>[!NOTE]
>
>有关更多详细信息，请参阅 [将URL外部化](/help/sites-developing/externalizer.md).

1. 导航到OSGi Web控制台，网址为 **https://&lt;server>：&lt;port>/system/console/configMgr。**
1. 查找 **Day CQ链接外部化器** 并输入创作节点的域。

   ![Day CQ链接外部化器](assets/aem-externalizer-01.png)
