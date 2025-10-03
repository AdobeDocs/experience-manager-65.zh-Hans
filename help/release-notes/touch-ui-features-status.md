---
title: 触控 UI 功能状态
description: 与 [!DNL Adobe Experience Manager] 触控 UI 相关的发行说明。
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 25bf0d64b6839afec0112ea8c9fde0510e56ccf4
workflow-type: ht
source-wordcount: '1087'
ht-degree: 100%

---

# 触控 UI 功能状态 {#touch-ui-feature-status}

从 Adobe Experience Manager（AEM）6.4 起，[经典 UI 已弃用](../release-notes/deprecated-removed-features.md)。Adobe 不再对经典 UI 进行任何功能增强，并鼓励用户使用触控 UI 中提供的强大新功能。

从 6.0 版本开始，AEM 引入了一种新的用户界面，称为“触控 UI”（Touch UI），该界面与 [!DNL Adobe Experience Cloud] 保持一致，并遵循 Adobe 的整体用户界面规范。随着功能几乎达到对等，触控 UI 已成为 AEM 的标准用户界面，而传统的桌面式界面则被称为“经典 UI”。

尽管大多数功能已在触控 UI 中提供，但仍有部分功能尚未完善，并会在未来版本中补充。

以下列表展示了在 AEM 6.5 中各项功能的实施状态。

有关升级到 AEM 6.5 的客户建议，请参阅[面向客户的用户界面建议](/help/sites-deploying/ui-recommendations.md)。

>[!NOTE]
>
>本页面仅涵盖与经典 UI 的功能对等情况。触控 UI 中新增的、经典 UI 中不具备的独有功能未在此列出。

>[!NOTE]
>
>该列表力求完整，但并非详尽无遗。

## 图例 {#legend}

* **完整**：该功能已在触控 UI 中完全提供。
* **大部分提供**：该功能在触控 UI 中基本可用。
* **缺失**：该功能在触控 UI 中不可用，需使用经典 UI 执行此操作。
* **已替换**：该功能已被以不同方式进行的新实施所取代。
* **已移除**：该功能在触控 UI 中已不存在，且不会被替代。

## 功能状态：站点管理员 {#feature-status-sites-admin}

以下是经典 UI 站点管理员（`/siteadmin`）所具备的功能列表，以及其在触控 UI（`/sites.html`）中的状态。

| 功能 | 状态 | 注释 |
|--- |--- |--- |
| 浏览网站层级 | 完整 | AEM 6.4 引入了[内容树视图](/help/sites-authoring/basic-handling.md#content-tree)。 |
| 启动工作流 | 完整 |  |
| 创建新页面 | 完整 |  |
| 创建新网站 | 完整 |  |
| 创建新发布项 | 完整 |  |
| 创建新 Live Copy | 完整 |  |
| 创建文件夹 | 完整 |  |
| 显示发布状态 | 完整 | 从 AEM 6.5 开始，工作流状态会在列表视图中显示。 |
| 搜索 | 完整 |  |
| 复制并粘贴页面（重复） | 完整 |  |
| 移动页面 | 完整 |  |
| 发布页面 | 完整 |  |
| 在无复制权限的情况下发布页面 | 完整 |  |
| 稍后发布 | 完整 |  |
| 发布树 | 完整 |  |
| 取消发布页面 | 完整 |  |
| 在无复制权限的情况下取消发布页面 | 完整 |  |
| 稍后取消发布 | 完整 |  |
| 删除 | 完整 |  |
| 锁定/解锁 | 完整 |  |
| 查看/编辑属性 | 完整 |  |
| 设置页面权限 | 完整 |  |
| 版本历史记录 | 完整 |  |
| 恢复版本 | 完成 |  |
| 恢复树并恢复已删除的页面 | 缺失 | 请使用经典 UI。 |
| 显示旧版本与当前版本之间的差异 | 完整 |  |
| Live Copy 操作（推出） | 完整 |  |
| 查看语言副本 | 完整 |  |
| 查找并替换 | 缺失 | 请使用经典 UI。 |
| 通知收件箱（JCR 事件） | 缺失 | 请使用经典 UI。将在未来版本中由不同的实施方式替代。 |
| 引用 | 完整 | 在 AEM 6.5 中新增了显示传入页面链接的功能。出于性能方面的考虑，仅显示页面的直接链接。 |

## 功能状态：页面编辑器 {#feature-status-page-editor}

以下是经典 UI 页面编辑器（`/cf#`）所具备的功能列表，以及其在触控 UI（`/editor.html`）中的状态。

| 功能 | 状态 | 注释 |
|--- |--- |--- |
| 编辑网页 | 完整 |  |
| 编辑移动网页 | 完整 |  |
| 编辑通过设计导入器导入的内容 | 完整 |  |
| 编辑电子邮件 | 完整 |  |
| 编辑混合移动应用程序 | 完整 |  |
| 编辑表单 | 完整 |  |
| 编辑产品建议 | 完整 |  |
| 编辑工作流模型 | 完整 |  |
| 模式：编辑和预览 | 完整 |  |
| 响应式预览 | 完整 |  |
| 模式：编辑设计 | 完整 |  |
| 模式：基架 | 完整 |  |
| 模式：Live Copy 状态 | 完整 |  |
| 添加批注 | 完整 |  |
| 编辑属性 | 完整 |  |
| 转出页面 | 完整 |  |
| 启动并显示工作流 | 完整 |  |
| 工作流包处理 | 大部分提供 | 可在触控 UI 中使用。多个工作流负载仍在经典 UI 中呈现。 |
| 锁定/解锁页面 | 完整 |  |
| 发布页面 | 完整 |  |
| 取消发布页面 | 完整 |  |
| 复制页面 | 已移除 | 使用站点管理员来[复制页面](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page)。 |
| 移动页面 | 已移除 | 使用站点管理员来[移动页面](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page)。 |
| 删除页面 | 已移除 | 使用站点管理员来[删除页面](/help/sites-authoring/managing-pages.md#deleting-a-page)。 |
| 显示引用 | 已移除 | 使用站点管理员来查看[详细引用列表](/help/sites-authoring/author-environment-tools.md#references)。 |
| 审核日志 | 已移除 | 使用站点管理员并[打开活动边栏](/help/sites-authoring/author-environment-tools.md#events-timeline)。 |
| 创建版本 | 已移除 | 使用站点管理员来[创建新版本](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version)。 |
| 恢复版本 | 已移除 | 使用站点管理员来[恢复版本](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version)。 |
| 切换发布项 | 已移除 | 使用站点管理员[在发布项之间切换](/help/sites-authoring/launches-promoting.md)。 |
| 翻译页面 | 已移除 | 使用站点管理员[将页面添加到翻译项目](/help/sites-administering/tc-manage.md)。 |
| 时间扭曲（选择日期/时间并以当时的状态浏览网站） | 完整 |  |
| 设置权限 | 完整 |  |
| 客户端上下文 UI | 已替换 | 请改用 [ContextHub](/help/sites-authoring/ch-previewing.md) UI。 |
| 多种媒体类型的内容查找器 | 完整 |  |
| 组件列表 | 完整 |  |
| 复制并粘贴组件 | 完整 |  |
| 剪贴板中的组件列表 | 缺失 |  |
| 还原/重做 | 完整 |  |
| 将内容拖入组件占位符 | 完整 |  |
| 将内容直接拖入 parsys 占位符并自动创建组件 | 完整 |  |

## 功能状态：文本、表格和图像编辑器 {#feature-status-text-table-and-image-editors}

以下是经典 UI 文本、表格和图像编辑器具备的功能，以及其在触控 UI 中的状态。

| 功能 | 状态 | 注释 |
|--- |--- |--- |
| 富文本编辑器 | 完整 | 可在页面内、对话框及全屏模式下使用。 |
| 启用/禁用 RTE 插件 | 完整 | 可通过[模板编辑器](/help/sites-authoring/templates.md)完成。 |
| 在纯文本中使用 RTE | 完整 |  |
| RTE 插件：链接和锚点 | 完整 |  |
| RTE 插件：字符映射 | 完整 |  |
| RTE 插件：复制/粘贴 | 完整 |  |
| RTE 插件：从 Microsoft® Word 粘贴 | 完整 |  |
| RTE 插件：查找和替换 | 完整 |  |
| RTE 插件：文本格式（粗体等） | 完整 |  |
| RTE 插件：上下标 | 完整 |  |
| RTE 插件：对齐 | 完整 |  |
| RTE 插件：列表（项目符号/编号） | 完整 |  |
| RTE 插件：段落格式 | 完整 |  |
| RTE 插件：文本样式 | 完整 |  |
| RTE 插件：源编辑器（编辑 HTML） | 完整 | 仅可在对话框和全屏模式下使用。 |
| RTE 插件：拼写检查器 | 完整 |  |
| RTE 插件：表格（嵌入式表格编辑器） | 完整 |  |
| RTE 插件：撤消/重做 | 完整 |  |
| RTE 插件：允许内嵌图像 | 完整 |  |
| 表格编辑器 | 完整 | 可在页面内、对话框及全屏模式下使用。 |
| 将图像拖入表格单元格 | 完整 | 可在内联模式下使用 |
| 图像编辑器 | 完整 | 可在页面内、对话框及全屏模式下使用。 |
| 启用/禁用 IPE 插件 | 完整 | AEM 6.3 在[模板编辑器](/help/sites-authoring/templates.md)中引入了相关 UI。 |
| IPE 插件：裁剪 | 完整 |  |
| IPE 插件：翻转 | 完整 |  |
| IPE 插件：撤消/重做 | 完整 |  |
| IPE 插件：图像映射 | 完整 |  |
| IPE 插件：旋转 | 完整 |  |
| IPE 插件：缩放 | 完整 |  |

## 功能状态：工具 {#feature-status-tools}

以下是经典 UI 中提供的各类工具及其在触控 UI 中的状态。

| 功能 | 状态 | 注释 |
|--- |--- |--- |
| 任务管理 | 已替换 | 自 6.0 起引入了项目和任务功能。 |
| 工作流收件箱 | 完整 |  |
| 页面模板配置的工作流（`/etc/workflow/wcm/templates.html`） | 缺失 | 请使用经典 UI。 |
| 标记管理员 UI | 完整 |  |
| MSM/Blueprint 控制中心 | 完整 |  |
| Blueprint 管理器 UI | 完整 |  |
| 转出配置 UI | 缺失 | 使用经典 UI。 |
| 用户、组和权限 UI | 大部分提供 | 如需进行高级权限编辑，请使用经典 UI。 |
| 清理版本（`/etc/versioning/purge.html`） | 缺失 | 使用经典 UI。 |
| 外部链接检查程序（`/etc/linkchecker.html`） | 缺失 | 使用经典 UI。 |
| 批量编辑器（`/etc/importers/bulkeditor.html`） | 缺失 | 使用经典 UI。 |
| 上传缩略图以新增或覆盖现有缩略图 | 缺失 | 使用经典 UI。 |
