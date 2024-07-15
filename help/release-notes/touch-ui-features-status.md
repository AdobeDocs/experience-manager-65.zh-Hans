---
title: 触屏 UI 功能状态
description: 特定于 [!DNL Adobe Experience Manager] 触屏UI的发行说明。
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 15%

---

# 触屏 UI 功能状态 {#touch-ui-feature-status}

Adobe Experience Manager (AEM) 6.4及更高版本[已弃用经典UI](../release-notes/deprecated-removed-features.md)。 Adobe不再对经典UI进行任何增强，我们鼓励用户使用触屏UI中提供的强大新功能。

从版本6.0开始，AEM引入了一个称为“触屏UI”（称为“触屏UI”）的新用户界面，该界面与[!DNL Adobe Experience Cloud]和整个Adobe用户界面准则保持一致。 随着功能接近等同性，这已成为AEM中的标准UI，具有称为“经典UI”的旧式面向桌面的界面。

虽然触屏UI中已存在大多数功能，但仍有一些功能尚不完整，而且也有一些功能有待在将来的版本中添加。

以下列表显示了AEM 6.5中实现的功能的状态。

有关升级到AEM 6.5的客户的建议，请参阅[客户的用户界面建议](/help/sites-deploying/ui-recommendations.md)。

>[!NOTE]
>
>本页只介绍与经典UI的功能对等性。 未列出在经典UI中不存在的、添加到触屏优化UI且仅用于该触屏优化UI的功能。

>[!NOTE]
>
>这份清单力求完整，但并非详尽无遗。

## 图例 {#legend}

* **完成**：该功能在触屏UI中完全可用。
* **大部分时间**：该功能主要在触屏UI中可用。
* **缺失**：触屏优化UI中不存在该功能，必须使用经典UI执行此操作。
* **已替换**：该功能已替换为工作方式不同的新实现。
* **已删除**：触屏UI中不再存在该功能，不会将其替换。

## 功能状态：站点管理员 {#feature-status-sites-admin}

这是经典UI站点管理员(`/siteadmin`)的功能列表，以及触控式UI (`/sites.html`)中的状态。

| 专题 | 状态 | 注释 |
|--- |--- |--- |
| 导航站点层次结构 | 完成 | AEM 6.4引入了[内容树视图](/help/sites-authoring/basic-handling.md#content-tree)。 |
| 启动工作流 | 完成 |  |
| 创建新页面 | 完成 |  |
| 创建新站点 | 完成 |  |
| 新建启动项 | 完成 |  |
| 新建Live Copy | 完成 |  |
| 创建文件夹 | 完成 |  |
| 显示发布状态 | 完成 | 从AEM 6.5开始，工作流状态将显示在列表视图中。 |
| 搜索 | 完成 |  |
| 复制并粘贴页面（复制） | 完成 |  |
| 移动页面 | 完成 |  |
| Publish页面 | 完成 |  |
| 没有复制权限的Publish页面 | 完成 |  |
| 稍后发布 | 完成 |  |
| Publish树 | 完成 |  |
| 取消发布页面 | 完成 |  |
| 取消发布没有复制权限的页面 | 完成 |  |
| 稍后取消发布 | 完成 |  |
| 删除 | 完成 |  |
| 锁定/解锁 | 完成 |  |
| 查看/编辑属性 | 完成 |  |
| 设置页面权限 | 完成 |  |
| 版本历史记录 | 完成 |  |
| 恢复版本 | 完成 |  |
| 恢复树并恢复已删除的页面 | 缺失 | 使用经典UI。 |
| 显示旧版本与当前版本之间的差异 | 完成 |  |
| Live Copy操作（转出） | 完成 |  |
| 查看语言副本 | 完成 |  |
| 查找并替换 | 缺失 | 使用经典UI。 |
| 通知收件箱（JCR事件） | 缺失 | 使用经典UI。 替换为将来的其他实施。 |
| 引用 | 完成 | 显示添加到AEM 6.5的传入页面链接。 |

## 功能状态：页面编辑器 {#feature-status-page-editor}

这是经典UI页面编辑器(`/cf#`)所具有的功能的列表，以及已启用触控(`/editor.html`)中的状态。

| 专题 | 状态 | 注释 |
|--- |--- |--- |
| 编辑网页 | 完成 |  |
| 编辑移动网页 | 完成 |  |
| 编辑通过设计导入程序导入的内容 | 完成 |  |
| 编辑电子邮件 | 完成 |  |
| 编辑混合移动应用程序 | 完成 |  |
| 编辑Forms | 完成 |  |
| 编辑选件 | 完成 |  |
| 编辑工作流模型 | 完成 |  |
| 模式：编辑和预览 | 完成 |  |
| 响应式预览 | 完成 |  |
| 模式：编辑设计 | 完成 |  |
| 模式：基架 | 完成 |  |
| 模式： Live Copy状态 | 完成 |  |
| 添加注释 | 完成 |  |
| 编辑属性 | 完成 |  |
| 转出页面 | 完成 |  |
| 开始和显示工作流 | 完成 |  |
| 工作流包处理 | 大部分 | 可在触屏UI中访问。 经典UI中仍存在多个工作流有效负载。 |
| 锁定/解锁页面 | 完成 |  |
| 发布页面 | 完成 |  |
| 取消发布页面 | 完成 |  |
| 复制页面 | 已删除 | 使用站点管理员[复制页面](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page)。 |
| 移动页面 | 已删除 | 使用网站管理员[移动页面](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page)。 |
| 删除页面 | 已删除 | 使用站点管理员[删除页面](/help/sites-authoring/managing-pages.md#deleting-a-page)。 |
| 显示引用 | 已删除 | 使用站点管理员查看[详细引用列表](/help/sites-authoring/author-environment-tools.md#references)。 |
| 审核日志 | 已删除 | 使用站点管理员并[打开活动边栏](/help/sites-authoring/author-environment-tools.md#events-timeline)。 |
| 创建版本 | 已删除 | 使用站点管理员[创建新版本](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version)。 |
| 恢复版本 | 已删除 | 使用站点管理员[还原版本](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version)。 |
| 切换启动项 | 已删除 | 使用“站点管理员”可在启动项](/help/sites-authoring/launches-promoting.md)之间[切换。 |
| 翻译页面 | 已删除 | 使用站点管理员[将页面添加到翻译项目](/help/sites-administering/tc-manage.md)。 |
| 时间扭曲（选择日期/时间并浏览当时的网站） | 完成 |  |
| 设置权限 | 完成 |  |
| 客户端上下文UI | 已替换 | 以后请使用[ContextHub](/help/sites-authoring/ch-previewing.md) UI。 |
| 各种媒体类型的内容查找器 | 完成 |  |
| 组件列表 | 完成 |  |
| 复制并粘贴组件 | 完成 |  |
| 剪贴板中的组件列表 | 缺失 |  |
| 还原/重做 | 完成 |  |
| 将内容拖到组件占位符中 | 完成 |  |
| 通过组件自动创建将内容直接拖入Parsys占位符 | 完成 |  |

## 功能状态：文本、表格和图像编辑器 {#feature-status-text-table-and-image-editors}

这是经典UI文本、表和图像编辑器在触屏UI中拥有的功能以及状态的列表。

| 专题 | 状态 | 注释 |
|--- |--- |--- |
| 富文本编辑器 | 完成 | 可在原位、对话框和全屏中使用。 |
| 启用/禁用RTE插件 | 完成 | 可以使用[模板编辑器](/help/sites-authoring/templates.md)完成此操作。 |
| 将RTE用于纯文本 | 完成 |  |
| RTE插件：链接和锚点 | 完成 |  |
| RTE插件：字符映射 | 完成 |  |
| RTE插件：复制/粘贴 | 完成 |  |
| RTE插件：从Microsoft® Word中粘贴 | 完成 |  |
| RTE插件：查找和替换 | 完成 |  |
| RTE插件：文本格式（粗体、...） | 完成 |  |
| RTE插件：下标和上标 | 完成 |  |
| RTE插件：调整 | 完成 |  |
| RTE插件：列表（项目符号/编号） | 完成 |  |
| RTE插件：段落格式 | 完成 |  |
| RTE插件：文本样式 | 完成 |  |
| RTE插件：Source编辑器(编辑HTML) | 完成 | 仅在对话框和全屏中可用。 |
| RTE插件：拼写检查程序 | 完成 |  |
| RTE插件：表（嵌入式表编辑器） | 完成 |  |
| RTE插件：撤消/重做 | 完成 |  |
| RTE插件：允许使用内联图像 | 完成 |  |
| 表编辑器 | 完成 | 可在原位、对话框和全屏中使用。 |
| 将图像拖入表单元格 | 完成 | 可内嵌使用 |
| 图像编辑器 | 完成 | 可在原位、对话框和全屏中使用。 |
| 启用/禁用IPE插件 | 完成 | AEM 6.3在[模板编辑器](/help/sites-authoring/templates.md)中引入了用户界面。 |
| IPE插件：裁切 | 完成 |  |
| IPE插件：翻转 | 完成 |  |
| IPE插件：撤消/重做 | 完成 |  |
| IPE插件：图像映射 | 完成 |  |
| IPE插件：旋转 | 完成 |  |
| IPE插件：缩放 | 完成 |  |

## 功能状态：工具 {#feature-status-tools}

这是经典UI所具有的各种工具的列表，以及触屏UI中的状态。

| 专题 | 状态 | 注释 |
|--- |--- |--- |
| 任务管理 | 已替换 | 6.0介绍了项目及任务。 |
| 工作流收件箱 | 完成 |  |
| 工作流到页面模板配置(`/etc/workflow/wcm/templates.html`) | 缺失 | 使用经典UI。 |
| 标记管理员UI | 完成 |  |
| MSM/Blueprint控制中心 | 完成 |  |
| Blueprint Manager UI | 完成 |  |
| 转出配置UI | 缺失 | 使用经典UI。 |
| 用户、组和权限UI | 大部分完成 | 要进行高级权限编辑，请使用经典UI。 |
| 清除版本(`/etc/versioning/purge.html`) | 缺失 | 使用经典UI。 |
| 外部链接检查程序(`/etc/linkchecker.html`) | 缺失 | 使用经典UI。 |
| 批量编辑器(`/etc/importers/bulkeditor.html`) | 缺失 | 使用经典UI。 |
| 上传缩略图以添加或覆盖这些缩略图 | 缺失 | 使用经典UI。 |
