---
title: Teaser和策略
description: 营销活动通常使用Teaser作为吸引特定访客群体访问专注于其兴趣内容的机制。 为特定营销活动定义了一个或多个Teaser。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 27b8302c-250b-4ce6-b3cf-c938738f2d92
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 2%

---

# Teaser和策略{#teasers-and-strategies}

营销活动通常使用Teaser作为吸引特定访客群体访问专注于其兴趣内容的机制。 为特定营销活动定义了一个或多个Teaser。

>[!NOTE]
>
>AEM 6.2现已弃用Teaser组件。请改用[Target组件](/help/sites-authoring/content-targeting-touch.md)。

* **品牌页面**&#x200B;存储在网站的“促销活动”部分。 品牌包含单独的营销活动。
* **促销活动页面**&#x200B;存储在网站的“促销活动”部分。 每个营销活动都有一个单独的页面，其中包含了Teaser定义。 容器或概述页面还包含有关各个Teaser页面的某些信息和统计信息。

AEM中的Teaser由以下几个部分组成：

* **Teaser页面**&#x200B;存储在相应的营销活动页面下，并保存每个特定营销活动可用的Teaser段落的定义。 在显示Teaser段落时，会使用这些定义；包括内容变体，以及用于选择变体和Boost因子的区段。
* **Teaser组件**&#x200B;现成可用，允许您在内容页面中创建特定Teaser段落的实例。 您可以从sidekick中拖动Teaser组件，然后指定您的Teaser定义以创建您自己的Teaser段落。 **注意：** AEM 6.2现已弃用Teaser组件。请改用[Target组件](/help/sites-authoring/content-targeting-touch.md)。
* **Teaser段落**&#x200B;是内容页面中Teaser的实际实例。 这些功能可吸引部分访客进入专注于其兴趣的内容。
* 包含营销活动内容的页面侧重于特定访客区段。 通常，Teaser段落会将访客引向此类页面。

## 策略 {#strategies}

将Teaser段落添加到页面时，必须定义&#x200B;**策略**。

这适用于多个Teaser可供选择的情况，因为它们分配的区段都已成功解析。 **策略**&#x200B;然后指定用于选择显示的Teaser的额外条件：

* **点击流得分**&#x200B;基于访客客户端上下文中保留的标记和相关标记点击（显示访客点击包含相应标记的页面的频率）。 比较Teaser页面上定义的标记的点击率。
* **随机**，用于“随机”选择；使用为页面生成的随机因子，这可以在[客户端上下文](/help/sites-administering/client-context.md)中看到。
* 已解析区段列表中的&#x200B;**第一个**。 顺序是营销活动容器页面中Teaser的顺序。

区段的[提升因子](/help/sites-administering/campaign-segmentation.md#boost-factor)也会对选择产生影响。 这是添加到区段定义的加权系数，用于增加/减少选择区段的相对可能性。

各种选择标准的流程和相互关系用一个示例进行了最充分的说明（该方法也可用于确保Teaser将达到所需的受众）。

如果已创建以下区段并为其分配了各自的Boost因子：

| 市场细分 | 提升因子 |
|---|---|
| S1 | 0 |
| S2 | 0 |
| S3 | 10 |
| S4 | 30 |
| S5 | 0 |
| S6 | 100 |

我们使用以下Teaser定义：

<table>
 <tbody>
  <tr>
   <td>营销活动</td>
   <td>Teaser</td>
   <td>已分配的区段</td>
   <td>已分配的标记 </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1， S2</td>
   <td>商业、营销</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3、S4</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2， S5</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1、S2、S6</td>
   <td>营销</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>商业<br /> </td>
  </tr>
 </tbody>
</table>

然后，如果将此变量应用于访客，其中：

* 已成功解析&#x200B;**S1**、**S2和&#x200B;**S6**

* 标记&#x200B;**marketing**&#x200B;具有三次点击
* 标记&#x200B;**业务**&#x200B;有六个点击

我们可以看到结果：

* 匹配成功 — 是否已将任何分配给Teaser的区段成功解析为当前访客？
* 提升系数 — 所有适用区段中的最高提升系数
* clickstream得分 — 所有适用标记点击的累积总数

算之加权平均数，然后于应用适当策略前计算：

<table>
 <tbody>
  <tr>
   <td>营销活动</td>
   <td>Teaser</td>
   <td>已分配的区段</td>
   <td>标记 </td>
   <td>匹配是否成功？</td>
   <td>产生的提升因子</td>
   <td>生成的Clickstream得分 </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1， S2</td>
   <td>商业、营销</td>
   <td>是</td>
   <td>0</td>
   <td>9</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
   <td>是</td>
   <td>0</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3、S4</td>
   <td><br /> </td>
   <td>否</td>
   <td><br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2， S5</td>
   <td><br /> </td>
   <td>是<br /> </td>
   <td>0<br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1、S2、S6</td>
   <td>营销</td>
   <td>是</td>
   <td>100</td>
   <td>3</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>商务</td>
   <td>是</td>
   <td>100</td>
   <td>6 </td>
  </tr>
 </tbody>
</table>

根据应用于Teaser段落的&#x200B;**策略**，这些值用于确定访客将看到的Teaser：

<table>
 <tbody>
  <tr>
   <td>战略</td>
   <td>生成的Teaser</td>
   <td>评论</td>
  </tr>
  <tr>
   <td>第一个</td>
   <td>T5</td>
   <td>只有T5和T6被视为其区段都解析<i>和</i>，它们具有最高的提升因子。 返回的列表顺序为T5、T6；因此选择并显示T5。</td>
  </tr>
  <tr>
   <td>随机</td>
   <td>T5或T6</td>
   <td>两个Teaser都有所有解析度和同一提升因子的区段。 因此，两个Teaser按同等比例显示。</td>
  </tr>
  <tr>
   <td>Clickstream分数</td>
   <td>T6</td>
   <td><p>T1、T4、T5和T6的区段都会解析为访客。 T5和T6的升压因子越高，T1和T4被排除在外。 最后，T6的点击流得分越高，就越会选中它。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>如果在上述分辨率技术之后，有多个Teaser可供选择，则内部选择（随机）将选择单个Teaser进行显示。
>
>例如，如果策略是Clickstream得分，并且T5的Clickstream得分与T6相同（即，6而不是3），则将使用内部选择（随机）来选择这两种方法之一。

Teaser页面/段落用于引导特定访客区段访问关注其兴趣的内容。 它们可以呈现一系列可供访客选择的选项，或仅显示一个基于特定访客区段的Teaser段落。 例如，显示的Teaser段落可能取决于访客的年龄。

通常，Teaser页面是一种临时操作，将持续特定时间，直到它被下一个Teaser页面替换为止。

创建品牌和活动后，您可以创建和设置Teaser体验。

### 为Teaser创建接触点 {#creating-a-touchpoint-for-your-teaser}

>[!NOTE]
>
>AEM 6.2现已弃用Teaser组件。请改用[Target组件](/help/sites-authoring/content-targeting-touch.md)。

1. 导航到要放置指向活动页面的Teaser段落的内容页面。
1. 在所需位置添加&#x200B;**Teaser**&#x200B;组件(可在sidekick的&#x200B;**Personalization**&#x200B;部分中找到)。 首次创建时，将显示尚未配置营销活动路径：

   ![chlimage_1](assets/chlimage_1.png)

1. 编辑Teaser组件以添加：

   * **营销活动路径**
包含个别Teaser页面的营销活动页面的路径；区段确切决定要显示哪个Teaser。

   * **[策略](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#strategies)**
成功解析多个区段时用于选择的方法。

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. 单击&#x200B;**确定**&#x200B;进行保存。 根据您在Teaser上设置的区段以及您当前作为登录的用户的用户档案，将显示相应的内容：

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. 将鼠标悬停在Teaser段落上可显示问号图标（组件的右下角）。 单击此项可查看应用的区段以及它们当前是否解析。

   ![chlimage_1-3](assets/chlimage_1-3.png)

### Teaser概述 {#teaser-overview}

除了MCM中的营销活动视图外，营销活动页面还提供有关与其连接的Teaser的信息：

1. 从&#x200B;**网站**&#x200B;控制台中，打开促销活动页面；例如：

   `https://localhost:4502/content/campaigns/geometrixx-outdoors/storefront/summer.html`

   下面显示了Teaser定义和查看统计信息的概述：

   ![chlimage_1-4](assets/chlimage_1-4.png)
