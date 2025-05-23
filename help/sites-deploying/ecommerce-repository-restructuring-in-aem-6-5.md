---
title: AEM 6.5中的E-Commerce存储库重组
description: 了解如何进行必要的更改，以迁移到AEM 6.5中适用于E-Commerce的新存储库结构。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 78b7c497-c474-4308-bfab-8f424b5f7268
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 1%

---

# AEM 6.5中的E-Commerce存储库重组{#e-commerce-repository-restructuring-in-aem}

如AEM 6.5[&#128279;](/help/sites-deploying/repository-restructuring.md)中的父存储库重构页面中所述，升级到AEM 6.5的客户应使用此页面评估与影响AEM E-Commerce解决方案的存储库更改相关的工作量。 在AEM 6.5升级过程中，有些更改需要您尽心尽力，而其他更改则可能会推迟到将来升级时再进行。

## 6.5版升级 {#with-upgrade}

### 产品、订单、集合、分类、配送方式和支付方式数据 {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><p><code>/etc/commerce/products</code></p> <p><code>/etc/commerce/orders</code></p> <p><code>/etc/commerce/collections</code></p> <p><code>/etc/commerce/classifications</code></p> <p><code>/etc/commerce/shipping-methods</code></p> <p><code>/etc/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/var/commerce/products</code></p> <p><code>/var/commerce/orders</code></p> <p><code>/var/commerce/collections</code></p> <p><code>/var/commerce/classifications</code></p> <p><code>/var/commerce/shipping-methods</code></p> <p><code>/var/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>您可以使用<a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">延迟迁移</a>任务来迁移E-Commerce数据。</p> <p>它执行以下步骤：</p>
    <ul>
     <li>调整对旧位置的引用以指向新位置</li>
     <li>将内容从旧位置移动到新位置</li>
     <li>删除旧位置以最终激活整个系统中新位置的使用</li>
    </ul> <p>该任务覆盖的位置包括：</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>对于较大的目录，Adobe建议您将以下Java™系统属性传递给AEM，以单独运行商业迁移任务：</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>迁移后，重新启动AEM。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>
