---
title: Adobe Experience Manager Mobile - GDPR就绪
description: 了解Adobe Experience Manager如何准备好帮助您履行GDPR合规义务。
contentOwner: trushton
exl-id: d06e675f-fb61-47da-85de-e0b50dd44153
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# AEM Mobile - GDPR就绪 {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>以下部分使用GDPR作为示例，但包含的详细信息适用于所有数据保护和隐私法规；例如GDPR和CCPA。

{{ue-over-mobile}}

## AEM Mobile GDPR支持 {#aem-mobile-gdpr-support}

AEM Mobile随时准备帮助客户履行其GDPR合规义务。 AEM Mobile中未存储任何个人数据。 如果已配置，您可以使用Adobe ID登录AdobeExperience Mobile 。

<!-- [https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html) -->

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

Adobe的数字发布产品(在AEM Mobile之前)支持Adobe的GDPR准备工作。 请参阅[https://business.adobe.com/privacy/general-data-protection-regulation.html](https://business.adobe.com/privacy/general-data-protection-regulation.html)。 下面提供了有关在Digital Publishing Suite产品中支持GDPR相关功能的详细信息，包括如何与Adobe合作来启动GDPR请求。

要确保不会将AEM Mobile与旧版Digital Publishing Suite产品混淆，您可以在此处登录Digital Publishing Suite产品：

[https://acrobat.adobe.com/us/en/](https://acrobat.adobe.com/us/en/)

### 启动GDPR请求 {#initiating-a-gdpr-request}

请联系Adobe客户关怀团队，以便您可以为该Digital Publishing Suite启动GDPR请求。

查找客户数据需要以下ID。 收到的任何子集意味着其他ID不适用于此用户。

必需：

* 客户的合同ID： *dpsc-contractId*

提供以下至少一项内容：

* 最终用户的客户提供的OAuth ID（在客户的直接授权系统中使用的ID）： *dpsc-directEntitlementId*
* 对于Windows应用用户，最终用户的App Store ID： *dpsc-windowsAppStoreId*
* 最终用户用于与DPS应用程序交互的电子邮件地址： *电子邮件*

### 常见问题解答(FAQ) {#frequently-asked-questions-faq}

**启动Adobe请求时，DELETE是否正在删除我的App Store购买项目？**

Adobe会删除与应用商店购买（订阅等）相关的信息，但购买行为仍会记录在应用商店中。 如果应用程序（最终用户）已登录到应用商店，则会再次提取这些回执，并将其发送给Adobe。 稍后，这些内容会被视为新购买，并由应用程序恢复，然后再次访问。

**启动DELETEAdobe时请求是否正在删除客户提供的权利？**

Adobe删除其拥有的客户额外直接权利津贴信息。 如果应用程序（最终用户）登录到客户使用的OAuth机制，则会向Adobe发送信息，然后服务会再次获取额外权利。

**最终用户需要什么？**

由于为应用程序分配权限的键作为查看器软件的一部分驻留在设备上，因此最终用户应卸载应用程序。 最终用户应该认识到，如果他们重新安装应用程序，则现有购买（与应用商店用户关联）和直接权利津贴（与客户的OAuth用户关联）仍会恢复。

**当设备上的人员共享某个应用程序时，会发生什么情况？**

Adobe具有最少的信息，可直接关联回特定用户。 它使用随机创建的UUID关联数据，该UUID保留在应用程序数据中，并在应用程序发起的每个请求中传递。 这意味着在同一设备上共享应用程序的最终用户使用的是相同的UUID，并且所有数据都被视为归GDPR请求人所有。 对于访问和删除请求，DPSC都将共享应用程序的人员视为一个人。

**Analytics跟踪了哪些个人数据？**

无。 虽然会跟踪数据，但跟踪的数据属于应用程序级别（而非个人数据）。 这包括启动次数、崩溃次数、关闭次数、活动、购买次数或作品集叠加等事件。 不会跟踪地理位置、名称、设备ID或IP地址。

**最终用户提供了其信息，但未找到任何内容。 为什么不？**

随着Digital Publishing Suite产品的发展，服务实现发生了变化，更多数据被混淆。 如果使用用户提供的数据未找到任何数据，则意味着用户的数据无法跟踪回该人员。

### 示例 {#example}

请联系Adobe客户关怀团队，以便您发出GDPR请求。

以下是Digital Publishing SuiteGDPR请求的输入和结果输出示例：

#### 输入： {#inputs}

```
dpsc-contractId = "12345-1234-12416234" 
directEntitlementId = "1234-1234-1234" 
windowsAppStoreId = "testWinAppStoreId" 
email = "test@what.com"
```

#### 输出 {#outputs}

```
{

    "jobId": "test-1524750204384",

    "product": "DPSC",

    "action": "access",

    "userIDS": [

        {

        "namespace": "email",

        "value": "test@what.com"

        },

        {

        "namespace": "windowsAppStoreId",

        "value": "testWinAppStoreId"

        },

        {

        "namespace": "directEntitlementId",

        "value": "1234-1234-1234"

        }

    ],

    "receiptData": {

    "recordsFound": 6,

    "recordsAffected": 0,

    "tablesModified": 0,

    "subscriptionsFound": 24,

    "entitlementsFound": 24

    },

    "records": {

        "DPS_Stage_EntitlementUserDevices": [

        {

            "user_id": "testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "device_id": "appleStore:test1b16-f032-4d9c-9200-0d19999405c4",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test967d-5179-4dc6-958c-facd9d94da38",

            "device_id": "appleStore:test3f07-d5aa-4b32-8fac-b2b690b7ccd7",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test1838-6494-4e74-912c-1edf61581d0e",

            "device_id": "appleStore:test3813-f8cc-49ce-b021-50eb0814a3bb",

            "account_id": "1234-1234-1234"

        },

        {

            "user_id": "test5468-1a11-4e4c-be43-274181a9ef81",

            "device_id": "appleStore:testf082-2783-498d-ab62-b1b2e3eb67ae",

            "account_id": "1234-1234-1234"

        }

        ],

            "DPS_Stage_EntitlementUsers": [

        {

            "id": "store:test04a7-33a3-4b90-863d-79981ead0f19:appleStore",

            "part_id": "0",

            "alias_user_id": "testWinAppStoreId"

        },

        {

            "id": "internal:testd2da-0606-4444-87ef-0d5a1d4a121d:adobe",

            "part_id": "0",

            "user_id": "test@what.com"

        }

        ],

            "DPS_Stage_Subscriptions": [

        {

            "id": "appleStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test3531-a209-4391-beb9-951c7822244e",

            "overflow": "test4e59-86a8-4b75-b699-77e980c287ab",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "test491b-379e-4d24-96ef-e481bf8d3062",

            "overflow": "test931b-7422-485d-85a5-134828187b6c",

            "entitlement_count": "12"

        }

        ],

            "DPS_Stage_Entitlements": [

        {

            "id": "samsungStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test7332-60a0-42b8-a508-474668d83d2e",

            "overflow": "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "testf766-102a-460d-8f5a-42f7bb9d68b7",

            "overflow": "test4d96-2197-45a8-9caf-2aa2846b770c",

            "entitlement_count": "12"

        }

        ],

            "s3Buckets": {

            "name": "DPS-Entitlements-Overflow",

            "folder": "stage/",

            "overflows": {

            "subscriptions": [

            "test4e59-86a8-4b75-b699-77e980c287ab",

            "test931b-7422-485d-85a5-134828187b6c"

        ],

            "entitlements": [

            "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "test4d96-2197-45a8-9caf-2aa2846b770c"

                ]

            }

        }

    }

}
```
