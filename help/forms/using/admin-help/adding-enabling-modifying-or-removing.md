---
title: 添加、启用、修改或删除端点
description: 了解如何添加、启用、修改和删除端点。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b7461d5c-95d1-4da2-9d2a-f54c410a87f9
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# 添加、启用、修改或删除端点 {#adding-enabling-modifying-or-removing-endpoints}

## 向服务添加端点 {#add-an-endpoint-to-a-service}

端点只能添加到服务。 端点不能单独存在；它必须与服务相关联。

>[!NOTE]
>
>建议您在添加端点时使用唯一的名称。

1. 在管理控制台中，单击服务>应用程序和服务>服务管理。
1. 在“服务管理”页上，单击要配置的服务。
1. 在“端点”选项卡的列表中，选择要添加的端点类型，然后单击“添加”。
1. 根据端点类型，配置其他端点设置。

[观察文件夹终结点设置](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

[电子邮件端点设置](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

[配置任务管理器端点](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

[远程端点设置](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. 单击“添加”。

## 启用或禁用端点 {#enable-or-disable-an-endpoint}

默认情况下，新端点会自动启用。 但是，如果您已禁用端点，则必须启用它才能使其可操作。

如果您遇到服务问题，请禁用关联的端点以便更好地解决问题。 您可能还希望在常规系统维护期间或升级服务时禁用端点。

1. 在Administration Console中，单击服务>应用程序和服务>端点管理。
1. 在“端点管理”页面上，选中要启用或禁用端点的复选框，然后单击“启用”或“禁用”。

## 修改端点 {#modify-an-endpoint}

>[!NOTE]
>
>您使用管理控制台对端点配置所做的更改不会反映在应用程序的设计时副本中。 如果重新部署应用程序，则使用管理控制台对其端点所做的任何更改都将丢失。

1. 在Administration Console中，单击服务>应用程序和服务>端点管理。
1. 在“端点管理”页面上，单击要修改的端点。
1. 在“更新端点”页面上，修改端点名称、描述和设置。

   >[!NOTE]
   >
   >不要在名称或描述中包含&lt;字符，因为它将截断Workspace中显示的名称或描述。

1. 要保存更改，请单击“更新”。

您还可以在“服务管理”页中，通过选择服务，然后单击“端点”选项卡来执行此任务。

## 删除端点 {#remove-an-endpoint}

1. 在Administration Console中，单击服务>应用程序和服务>端点管理。
1. 在“端点管理”页面上，选中要删除的端点的复选框，然后单击“删除”。 终结点不再显示。
