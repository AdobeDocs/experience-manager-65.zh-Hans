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
feature: Integration
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 7%

---

# 与Adobe Target集成的先决条件{#prerequisites-for-integrating-with-adobe-target}

作为AEM与Adobe Target[&#128279;](/help/sites-administering/target.md)的集成的一部分，您需要向Adobe Target注册、配置复制代理以及发布节点上的安全活动设置。

## 在Adobe Target中注册 {#registering-with-adobe-target}

要将AEM与Adobe Target集成，您必须拥有有效的Adobe Target帐户。 此帐户必须至少具有&#x200B;**审批者**&#x200B;级别的权限。 当您注册Adobe Target时，您会收到一个客户端代码。 您需要客户端代码以及Adobe Target登录名和密码才能将AEM连接到Adobe Target。

客户端代码在调用Adobe Target服务器时标识Adobe Target客户帐户。

>[!NOTE]
>
>您的帐户还必须由Target团队启用才能使用该集成。
>
>如果不是这种情况，请联系[Adobe客户关怀](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html)。

## 启用目标复制代理 {#enabling-the-target-replication-agent}

必须在创作实例上启用测试和目标[复制代理](/help/sites-deploying/replication.md)。 请注意，如果您使用[nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent)运行模式来安装AEM，则默认情况下不启用此复制代理。 有关保护生产环境的更多信息，请参阅[安全核对清单](/help/sites-administering/security-checklist.md)。

1. 在AEM主页上，单击&#x200B;**工具** > **部署** > **复制**。
1. 单击作者上的&#x200B;**代理**。
1. 单击&#x200B;**测试和目标（测试和目标）**&#x200B;复制代理，然后单击&#x200B;**编辑**。
1. 选择“已启用”选项，然后单击&#x200B;**确定**。

   >[!NOTE]
   >
   >配置Test and Target复制代理时，在&#x200B;**传输**&#x200B;选项卡中，URI默认设置为&#x200B;**tnt:///**。 不要将此URI替换为&#x200B;**https://admin.testandtarget.omniture.com**。
   >
   >如果尝试测试与&#x200B;**tnt:///**&#x200B;的连接，则会引发错误。 这是预期行为，因为此URI仅供内部使用；请勿与&#x200B;**测试连接**&#x200B;一起使用。

## 保护活动设置节点 {#securing-the-activity-settings-node}

确保发布实例中的活动设置节点 **cq:ActivitySettings** 安全，以使其不可由普通用户访问。该活动设置节点应当只能由负责将活动同步到 Adobe Target 的服务访问。

**cq：ActivitySettings**&#x200B;节点在CRXDE lite中位于活动jcr：content节点；**下的`/content/campaigns/*nameofbrand*`**&#x200B;下，例如`/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`。 此节点仅在定向组件后创建。

活动的jcr：content下的&#x200B;**cq：ActivitySettings**&#x200B;节点受以下ACL保护：

* 拒绝所有人的所有
* 允许“target-activity-authors”使用jcr：read，rep：write（作者是此组的一名现成成员）
* 允许jcr：read，rep：write用于“targetservice”

这些设置可确保普通用户无权访问节点属性。 在创作实例和发布实例上使用相同的ACL。 有关详细信息，请参阅[用户管理和安全性](/help/sites-administering/security.md)。

## 配置AEM链接外部化器 {#configuring-the-aem-link-externalizer}

在Adobe Target中编辑活动时，除非更改AEM创作节点上的URL，否则URL将指向&#x200B;**localhost**。 如果您希望导出的内容指向特定的&#x200B;*发布*&#x200B;域，则可以配置AEM Link Externalizer。

>[!NOTE]
>
>另请参阅[添加云配置](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration)。

要配置AEM外部化器，请执行以下操作：

>[!NOTE]
>
>有关更多详细信息，请参阅[外部化URL](/help/sites-developing/externalizer.md)。

1. 导航到&#x200B;**https://&lt;server>：&lt;port>/system/console/configMgr.**&#x200B;处的OSGi Web控制台。
1. 查找&#x200B;**Day CQ Link Externalizer**&#x200B;并输入创作节点的域。

   ![天CQ链接外部化器](assets/aem-externalizer-01.png)
