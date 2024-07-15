---
title: oracle数据库最大打开游标阈值
description: 了解如何在Oracle中为打开的游标配置最大值。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5be26485-afe5-47ac-918c-e2fff4f394b2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# oracle数据库最大打开游标阈值 {#oracle-database-maximum-open-cursors-threshold}

要为Oracle中的打开游标配置最大值，您可能必须将此值调整为适合您的应用程序的数字。 显然，在中等负载下，平均打开游标为2700。 建议您从3000的上限开始。 有关详细信息，请转到[https://www.orafaq.com/node/758](https://www.orafaq.com/node/758)。
