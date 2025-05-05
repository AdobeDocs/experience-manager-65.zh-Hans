---
title: 解决 MSM 问题和常见问题
description: 了解如何解决与 MSM 相关的最常见问题以及获得与 MSM 相关的最常见疑问的答案。
feature: Multi Site Manager
role: Admin
exl-id: 23f3391b-5ce3-48e1-ab27-a37737778089
solution: Experience Manager, Experience Manager Sites
source-git-commit: 3aa55b88f589749fb49d5ff46340b0912d490157
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 81%

---

# 解决 MSM 问题和常见问题 {#troubleshooting-msm}

## 排查首要步骤的问题 {#first-steps}

如果您在 MSM 中遇到您认为不正确的行为或错误，则在开始详细的问题排查之前，请务必：

* 查看 [MSM 常见问题](#faq)，因为其中可能已包含您的问题或疑问的答案。
* 查看 [MSM 最佳实践文章](msm-best-practices.md)，因为那里提供了若干提示并澄清了一些误解。

## 查找有关您的 Blueprint 和 Live Copy 状态的高级信息 {#advanced-info}

MSM 注册了几个 servlet，可以使用资源 URL 上的选择器来请求这些 servlet。它们由 UI 使用，也可以直接请求以直接查看页面的其他高级计算 MSM 状态：

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * 在 Blueprint 页面上使用它可检索与之链接的所有 Live Copy 的列表，以及其他 Live Copy 状态信息。
   * 例如：

     `http://localhost:4502/content/wknd/language-masters/en.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`


1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * 在 Live Copy 页面上使用它可检索有关其与 Blueprint 页面的连接的高级信息。如果页面不是 Live Copy，则不会返回任何内容。
   * 例如：

     `http://localhost:4502/content/wknd/ca/en.msm.json`

servlet 通过 `com.day.cq.wcm.msm` 记录器生成 DEBUG 日志消息，这些消息也很有用。

## 查看存储库中的 MSM 特定信息 {#checking-repo}

先前的 servlet 已返回基于 MSM 特定节点和 mixin 的计算信息。该信息通过以下方式存储在存储库中。

* `cq:LiveSync` mixin 类型
   * 它在 `jcr:content` 节点上设置，并定义根 Live Copy 页面。
   * 这些页面具有类型为`cq:LiveCopy`的`cq:LiveSyncConfig`子节点，这些子节点通过下列属性包含有关Live Copy的基本和强制性信息：
      * `cq:master` 指向 Live Copy 的 Blueprint 页面。
      * `cq:rolloutConfigs` 表示应用于 Live Copy 的活动转出配置。
      * 如果此根 Live Copy 页面的子页面包含在 Live Copy 中，则 `cq:isDeep` 为 true。
* `cq:LiveRelationship` mixin 类型
   * 任何 Live Copy 页面的 `jcr:content` 节点上均具有一个此 mixin 类型。
   * 否则，已在某个时刻通过 Live Copy 操作（创建或转出）之外的创作界面分离或手动创建了该页面。
* `cq:LiveSyncCancelled` mixin 类型
   * 添加到已暂停的 Live Copy 页面的 `jcr:content` 节点。
   * 如果暂停对子页面也有效，则 `cq:isCancelledForChildren` 属性在同一节点上设置为 true。

这些属性包含的信息应反映在 UI 中，但在进行问题排查时，在 MSM 操作发生时直接在存储库中观察 MSM 行为可能会很有用。

了解这些属性对于查询存储库并找出处于特定状态的页面集也很有用。 例如：

* `select * from cq:LiveSync` 返回所有 Live Copy 根页面。

## 常见问题 {#faq}

以下是与 MSM 和 Live Copy 相关的一些常见问题。

### 为什么一些属性（例如标题、注释）在 MSM 转出期间未更新？ {#missing-properties}

可非常灵活地配置 MSM 同步操作。在转出期间修改哪些属性或组件直接取决于这些配置的属性。

有关此主题的更多信息，请参阅[MSM最佳实践](msm-best-practices.md)。

### 如何删除一组作者的转出权限？ {#remove-rollout-permissions}

无法为 AEM 主体（用户或组）设置或删除任何&#x200B;**转出**&#x200B;权限。

作为替代方案，您可以：

* 自定义产品 UI 以隐藏给定主体的转出操作。
* 从 Live Copy 树删除不允许其转出的作者的写入权限。

### 为什么看到 Live Copy 页面具有“_msm_moved”后缀？ {#moved-pages}

如果转出Blueprint页面，它将更新其Live Copy页面或创建一个新的Live Copy页面（如果尚不存在）。 例如，首次转出它或手动删除 Live Copy 页面时。

但在后一种情况下，如果存在不带`cq:LiveRelationship`属性的同名页面，则在创建Live Copy页面之前会重命名此页面。

默认情况下，转出需要一个链接的Live Copy页面，Blueprint的更新将转出到该页面。 或者，它期望在创建Live Copy页面时完全没有页面。

如果找到“独立”页面，MSM 会选择重命名该页面，并创建一个单独的、链接的 Live Copy 页面。

Live Copy 子树中的此类独立页面一般是&#x200B;**分离**&#x200B;操作的结果，或者是作者手动删除了以前的 Live Copy 页面，然后重新创建一个同名的页面所致。

要避免发生这种情况，请使用 Live Copy **暂停**&#x200B;功能代替&#x200B;**分离**。可在[本文](msm-livecopy.md)中找到关于&#x200B;**分离**&#x200B;操作的更多详情。
