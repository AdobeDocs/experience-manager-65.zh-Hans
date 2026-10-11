---
title: 更改身份验证的评估顺序
description: 您可以更改AEM Forms评估多个身份验证提供程序的顺序。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7e29c9d4-fb82-4308-aac7-0f5cb1f4aef2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 8%
---
# 更改身份验证的评估顺序 {#change-the-order-of-evaluation-for-authentication}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

如果您配置了多个身份验证提供程序，则可以更改AEM表单评估它们进行身份验证的顺序。 config.xml文件中列出的身份验证提供程序的顺序决定了身份验证的评估顺序。

1. 在管理控制台中，单击设置>用户管理>配置>导入和导出配置文件。
1. 要将当前配置设置导出到文件，请单击“导出”并将配置文件保存到其他位置。
1. 在文件中找到以下节点：

   ```xml
    <node name="AuthSchemes">
        <map />
            <node name="CertificateAuth">
                <map>
                    <entry key="order" value="3" />
                    <entry key="name" value="edc.server.auth.scheme.certificate" />
                </map>
        </node>
        <node name="Kerberos">
            <map>
                <entry key="kerberosSPN" value="defaultSPN" />
                <entry key="order" value="1" />
                <entry key="name" value="edc.server.auth.scheme.kerberos" />
            </map>
    </node>
   ```

   在`<entry key="order" value="3" />`中，编辑每个节点的值以设置身份验证评估的顺序。

1. 要导入更新的文件，请在“用户管理”中单击“配置”>“导入和导出配置文件”。
1. 单击“浏览”查找文件，单击“导入”，然后单击“确定”。
