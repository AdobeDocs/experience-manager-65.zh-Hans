---
title: 项目管理——最佳做法清单
description: 实施 Adobe Experience Manager（AEM）的项目管理需要充分的规划与理解。项目清单旨在为项目投放提供一套最佳做法。它们会引导您完成项目生命周期的各个阶段，并对您的状态进行高层次监控。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist, introduction
content-type: reference
docset: aem65
exl-id: 94b91996-d2b2-4d4a-b770-334cfa2dc0b7
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Admin,Architect,Data Architect,Developer,Leader
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: ht
source-wordcount: '3212'
ht-degree: 100%

---

# 项目管理——最佳做法清单{#managing-projects-best-practices-checklist}

要成功实施 Adobe Experience Manager（AEM）项目，您需要提前并在实施过程中持续进行规划与研判，以明确将要面对的问题以及需要作出的相关决策。

为此，最佳做法包括以下内容：

* 一份[交互式清单](/help/managing/best-practices-checklist.md)，用于跟踪并监控您在这些最佳做法上的推进进度。

   * 按项目阶段、里程碑与角色定义输入与可交付结果。
   * 提供自动化概述（质量、健康度与完整度），以指示进度与项目健康状况。

* 基于该[清单](/help/managing/best-practices-checklist.md)的文档会详细说明以下内容：

   * [项目节奏](#projectheartbeat)分析。
   * [按角色划分的状态](#status-by-role)概述。
   * [阶段和里程碑](#phases-and-milestones)。
   * [关键角色](#persona)及其在各（相关）阶段的参与情况。
   * [所需文档与可交付结果](#required-documents-and-deliverables)的[术语表](/help/managing/best-practices-glossary.md)。

* 可供[进一步参考](/help/managing/best-practices-further-reference.md)的资料，提供特定领域的详细信息。

## 项目节奏仪表板 {#project-heartbeat-dashboard}

**项目节奏**&#x200B;工作表以可视化形式概述项目的关键量度：

* **阶段质量**

   * 指示整个项目范围内[必要文档与可交付结果](#required-documents-and-deliverables)的质量状况。

* **阶段健康度**

   * 用于反映项目整体状态的高层级指标，便于突出显示可能存在风险的区域。

* **阶段完整度**

   * 在项目任一时间点，显示项目的各个阶段已完成的比例。

## 按角色划分的状态 {#status-by-role}

**按角色划分的状态**&#x200B;工作表按&#x200B;**[阶段](#phases-and-milestones)**&#x200B;与&#x200B;**[角色](#persona)**&#x200B;维度，细分展示&#x200B;[**健康度**、**质量与&#x200B;**完整度**](#projectheartbeat)。

## 阶段和里程碑 {#phases-and-milestones}

项目计划会被划分为清晰的（高层级）阶段。

每个阶段都包含相应的里程碑。针对每个[角色](#persona)，列出了相关的里程碑，以及为产出既定可交付结果所需的文档。

>[!NOTE]
>
>单个所需文档与可交付成果之间并不存在直接的 1:1 对应关系。

### 准备阶段 {#preparation}

项目准备构成整个项目的基础。需明确关键需求，并设定清晰的目标与期望，包括：

* **业务理由**

   * 开展该项目的根本原因与正当性。

* **范围与计划**

   * 应制定基本范围和初步计划，以界定项目需要完成的内容及时间框架；如有助于澄清情况，还可明确哪些内容不在项目范围内。

您如何准备、规划和执行项目，以及如何实施解决方案，会受到现有约束条件的影响。例如，固定预算、固定时间线、内容数量以及所需质量。

与往常一样，调整任何一个因素都会影响其他因素。例如，在缩短时间的同时仍要求保持相同质量，往往会导致成本上升，同时可处理的内容数量减少。预算通常是关键因素，因此这种关联关系不容忽视。

四大要素：

![projectphases_fourphases](assets/projectphases_fourphases.png)

#### 里程碑 {#milestones}

* **验证**

  在此阶段，您必须验证并确认项目目标，例如：

   * 您希望实现/提供什么？
   * 受益对象是谁？
   * 项目范围是什么？

      * 如有助于澄清情况，您还可以界定哪些内容不在项目范围内。

   * 您如何定义成功？
   * 您如何衡量成功？
   * 有哪些业务和技术需求？
   * 是否需要替换旧版系统？若需要，是否有数据需要迁移？
   * 参与者有哪些？
   * 您如何衡量项目进展？
   * 在项目周期内，您多久会审查一次进度？

* **预算**

  在启动任何项目之前，您需要对实施成本做出可靠且切合实际的估算：

   * 应以验证里程碑阶段的信息作为估算依据。
   * 估算应切合实际。
   * 应考虑并尊重客户所遵循的指南、流程或限制条件。
   * 如需在后期对预算进行复审或调整，应考虑应急方案并规划复审流程。
   * 请注意，成本可能以多种形式出现，例如采购、资源使用以及各类费用等。

### 规划 {#planning}

项目规划是对准备工作的进一步落实。在此阶段，您应将目标和期望转化为清晰的路线图，路线图需包含具体任务，并辅以明确的沟通与严格的评审机制，以衡量项目进展。

#### 里程碑 {#milestones-1}

* **交接**

  顺畅的交接可确保相关角色/团队清楚自身在项目中的职责。

  应提供或生成完整的细节，使其充分了解包括路线图、范围、目标、需求及关键绩效指标（KPI）在内的所有相关内容。

* **风险评估**

  为避免出现意外情况，应通过风险评估识别并量化潜在风险，同时评估其影响与发生概率。

  风险评估应在项目生命周期的早期进行，以确保尽早发现并评估潜在漏洞。根据评估结果，您可以向利益相关者汇报是否能够实施全部需求，并在必要时规划并跟踪相应的应对措施。

* **沟通**

  沟通始终是任何项目成功的关键。应进行清晰高效的沟通，以确保所有人：

   * 朝着相同的基本目标努力
   * 基于相同的信息来源
   * 使用相同的渠道

* **启动会**

  启动会用于正式宣告项目即将开始。这是一个绝佳的机会，可用于：

   * 邀请所有相关方（或至少各组代表）。
   * 介绍项目的关键信息。
   * 解答问题。
   * 确保所有人拥有一致的知识库。
   * 争取所有参与人员的承诺——这需要通过建立信任来获得。

      * 在项目最初阶段就让关键成员（包括潜在的内容作者）参与进来，将更有助于获得他们对项目的承诺。

### 开发准备 {#development-preparation}

开发规划是确保项目由具备所需知识的团队在稳固的设计基础上进行构建的关键。

#### 里程碑 {#milestones-2}

* **开发团队配备与培训**

  在启动任何项目之前，应确保开发团队人员配备合理，并对所有团队成员进行与任务相关的培训。

* **内容架构**

  内容架构定义并描述了未来的内容体系，其中包括：

   * 内容树；包括资产
   * 基本结构；包括营销活动等。
   * 多网站与多语言结构（MSM、翻译等）
   * 支持型内容（包括标记及标记概念）
   * 缓存与内容复用策略

* **系统架构**

  系统架构定义系统的概念性视图，其中包括（但不限于）：

   * 各所需环境的[系统结构](/help/sites-deploying/recommended-deploys.md#deployment-scenarios)
   * 子系统
   * 第三方系统
   * 接口；硬件、软件与人工交互
   * 各环境的服务器；请参阅[技术要求](/help/sites-deploying/technical-requirements.md)和[硬件选型指南](/help/managing/hardware-sizing-guidelines.md)

   * 各环境的流程；例如部署与维护要求
   * 维护活动（数据存储垃圾回收、TarPM 优化等）
   * [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans) 缓存
   * [集群](/help/sites-deploying/recommended-deploys.md#deployment-scenarios)发布/作者共享
   * 客户端性能优化（JS 压缩、合并、CSS Sprite、HTTP 请求总数等）

* **应用程序架构**

  应用架构定义并描述拟实施应用程序的行为。

  重点包括：

   * 应用程序之间以及与用户之间的交互方式。
   * 应用程序需消耗和生成的数据，而非其内部结构。

  这些定义应涵盖以下内容：

   * 项目的基本代码结构
   * 代码工件（捆绑包、软件包等）
   * 模板/组件的拆分及其关系
   * 所需自定义的高层级细节（具体覆盖内容将在后续定义）
   * 解决方案所需工作流的设计（例如内容创建、审批、发布、转化、导入与导出）
   * 对 MSM、Commerce、第三方集成等复杂模块的特别考量

* **系统集成**

  系统集成需要您规划（并实施）：

   * 如何将所有子系统与[解决方案集成](/help/sites-administering/integration.md)统一起来，使其作为一个整体系统协同运行
   * 如何集成任何第三方系统；以及需要考虑的特殊情况，例如在线/离线、客户端/浏览器端，或在第三方系统宕机时的故障切换处理

* **测试概念**

  在开始开发之前，应制定一个深入而全面的概念方案，以覆盖项目的所有[测试](/help/sites-developing/planning.md)需求。

  该方案应包括（但不限于）：

   * 需执行的所有测试的详细说明
   * 测试所需内容的准备
   * 计划使用的任何测试工具的信息
   * 高层级说明参与测试的人员，特别是质量保证（QA）团队之外的群体
   * 测试自动化的细节；例如使用 Selenium 或 AEM 开发者模式

* **Experience Design**

  Experience Design（XD）涉及为解决方案设计用户体验。

  用户体验应针对内容作者和网站的最终用户分别进行分析与设计。

* **支持设置**

  在开发开始之前，应建立所有与部署、发布、测试和问题报告相关的支持流程。

  另请参阅 [Adobe 支持门户](https://experienceleague.adobe.com/zh-hans?support-solution=General&support-tab=home#support)。

### 运营规划与运营 {#operations-planning-and-operations}

同样地，必须做好运营规划，以确保在项目生命周期的各个阶段都具备所需的运行环境。还需要配套的维护流程来保障其运行。

#### 里程碑 {#milestones-3}

* **权限**

  您需要为所有将使用该解决方案的用户/组规划并实施角色与权限方案。

  例如：

   * 列出角色列表（即组），并为每个角色定义 `read`/ `write` 访问权限

   * 定义影响发布环境的权限使用情况，例如 `replicate`
   * 应为权限最小化的用户定义工作流
   * `editor` 组中的用户不应拥有 `admin` 权限，也不应属于 `administrators` 组

  有关详细信息，请参阅[用户管理与安全](/help/sites-administering/security.md)。

* **监控与维护**

  监控与维护是确保解决方案上线后平稳运行的关键环节。为此，您需要定义：

   * 需要监控的内容
   * 维护任务；包括常规任务与特殊情况处理

  另请参阅[监控和维护](/help/sites-deploying/monitoring-and-maintaining.md)，以了解更多信息。

* **迁移**

  应审查并确认旧版系统中的所有内容是否适合迁移。

* **恢复计划**

  确保制定了恢复计划。在紧急情况下，必须依靠该计划来保障 AEM 的生产使用。计划应涵盖备份、恢复、故障切换等情况。

### 开发 {#development}

开发是一个至关重要的阶段，远不止于编写代码。

#### 里程碑 {#milestones-4}

* **开发环境**

  规划并记录您的开发环境，包括：

   * 架构
   * [开发工具](/help/sites-developing/dev-tools.md)

      * 一个典型的环境包括：

         * 问题跟踪系统，例如 Jira
         * 集成开发环境（IDE），例如 Eclipse
         * 构建管理工具，例如 Maven
         * 持续集成工具，例如 Jenkins
         * 版本控制工具，例如 GIT/SVN
         * 构建工件存储库管理器，例如 Archiva/Nexus

   * 第三方软件集成/依赖项
   * [解决方案集成/依赖项](/help/sites-administering/integration.md)
   * 部署节奏

* **测试系统**

  规划并记录您的测试环境，包括：

   * 架构
   * 对开发构建的依赖；包括每日构建
   * 第三方软件集成/依赖项的测试可能性或局限性
   * 测试工具
   * 自动化测试策略

* **生产系统**

  规划并记录您的生产环境，包括：

   * 架构
   * 部署节奏
   * 第三方软件集成/依赖项
   * 安全设置
   * 在生产环境中运行 [Tough Day 测试](/help/sites-developing/tough-day.md)以验证基准性能
   * 性能测试的要求；参见[质量保证最佳做法](/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance)

* **集成**

  规划、记录并测试系统与[解决方案集成](/help/sites-administering/integration.md)的各个方面，包括：

   * 自动化测试策略
   * 自动化流程，用于[将应用程序从开发环境迁移至测试环境，再迁移至生产环境](/help/managing/enterprise-devops.md#code-movement)
   * 自动化流程，用于[将内容从生产环境迁移至测试与开发环境](/help/managing/enterprise-devops.md#content-movement)

* **迁移**

  规划、记录并测试内容迁移的各个方面，包括：

   * 内容架构
   * 迁移策略

* **沟通**

  确保所有团队成员和项目角色在必要时都能及时获得最新信息。

* **文档**

  完整记录解决方案，包括：

   * 操作手册
   * 可能影响升级的任何自定义内容
   * 发行说明

### 性能和测试 {#performance-and-testing}

新应用程序一旦可用，就必须经过严格的测试，其中涵盖功能性和[性能](/help/sites-deploying/configuring-performance.md)。

>[!NOTE]
>
>任何测试团队应保持中立，客观提交测试结果。
>
>项目经理有责任评估这些结果的影响，并决定相应的后续措施。

#### 里程碑 {#milestones-5}

* **最终用户验收测试**

  [用户验收测试](/help/sites-developing/acceptance-signoff.md)（UAT）至关重要，用于确保：

   * 解决方案满足用户/客户的需求
   * 客户/用户认可解决方案（功能、设计和性能）

  应制定正式的客户交接清单；理想情况下，应能自动化执行，并在夜间基于快照运行。测试结果应发送给项目经理和开发团队

* **性能与负载测试**

  性能和负载测试用于确保解决方案在平均与峰值负载下均能满足所需性能水平。

  有关性能测试的更多信息，请参阅：

   * [性能测试](/help/sites-deploying/configuring-performance.md)
   * [如何规划与执行测试](/help/sites-developing/planning.md)

   * [基本性能指南](/help/sites-deploying/configuring-performance.md#basic-performance-guidelines)

  >[!NOTE]
  >
  >在 AEM 的日常使用中，该过程必须持续进行，但初始阶段尤为关键。

### 转出 {#rollout}

新应用程序的转出需要精心规划，以确保平稳切换至正式上线。这包括确认较高的安全水平、对所有潜在用户进行培训，以及进行多次演练，以确保所有问题已得到解决。

#### 里程碑 {#milestones-6}

* **准备**

  充分的准备与规划有助于确保顺利转出。

* **培训**

  确保所有相关人员均已接受培训。

  请参阅课程目录中的 [Adobe Experience Manager](https://training.adobe.com/training/courses.html#solution=adobeExperienceManager)。

* **管理员培训**

  确保您的解决方案管理员已完成以下事项：

   * 已接受培训
   * 已获得相应的培训资料
   * 已获得相应的文档

* **用户培训**

  确保您的作者已完成以下事项：

   * 已接受培训
   * 已获得相应的培训资料
   * 已获得相应的文档，例如《用户指南》

* **渗透测试**

  渗透测试通过模拟对计算机系统的攻击来识别潜在的安全漏洞。

* **渗透/安全测试**

  为确保解决方案的安全性，应执行特定的渗透测试，并结合更广泛的安全测试。

  详情请参阅[安全清单](/help/sites-administering/security-checklist.md)。

### 上线 {#go-live}

您希望上线事宜尽可能顺利。同样，需要规划最后阶段，以确保无缝执行。

#### 里程碑 {#milestones-7}

* **准备**

  充分的准备与规划将有助于确保顺利上线。

* **安全性**

  确认您的解决方案在内部与外部用户及其内容方面的安全性。

* **回退**

  确保在上线之前，所有所需的系统、程序与机制均已就绪，以支持回退。

* **支持**

  确保支持服务已准备到位。

* **过渡**

  规划并执行向生产环境及用户的过渡。

* **转出**

  准备并执行冒烟测试。

## 角色 {#persona}

这些清单是按照角色设计的。这些角色在项目生命周期中扮演着重要作用。

另外还有一些[其他角色](#other-persona)，他们会参与特定任务。

### 项目赞助者 {#project-sponsor}

项目赞助者的职责包括：

* 负责提供/呈现项目的商业论证。
* 在制定和界定项目范围时起关键作用；包括：

   * 成功的定义与评判标准
   * 主要关键绩效指标（KPI）

* 根据客户路线图提供主要里程碑。

### 项目经理 {#project-manager}

项目经理的职责包括：

* 根据项目赞助者提供的需求（如范围、KPI、成功标准与定义），全面负责项目投放。
* 负责制定预算并基于预算分配资源。
* 作为项目中所有角色的主要沟通接口。

### 架构师 {#architect}

解决方案架构师的职责包括：

* 负责解决方案和系统的高层级设计。
* 协助定义 AEM 的实施策略。例如，是否实施集群部署，是否需要冷备份，或者何时需要内容传递网络（CDN）。
* 还需根据客户需求定义 AEM 解决方案架构。这可能包括用户角色（及相关权限）的概念、模板与组件之间的关系，或何时采用多站点管理。

### 业务分析师 {#business-analyst}

业务分析师的职责包括：

* 主要负责收集和分析高层级需求，并将其转化为规范：

   * 供项目经理在规划开发时使用
   * 供开发团队在设计与开发过程中使用

* 与客户紧密合作以分析需求。并将这些需求与以下内容对照：

   * 成功的定义。
   * 成功的评判标准。
   * KPI（涵盖业务与性能两方面）。

### 开发负责人 {#development-lead}

开发负责人的职责包括：

* 负责项目的技术投放。
* 负责选择符合客户需求的开发方法论。
* 制定开发战略，包括：

   * 确保与业务及性能 KPI 保持一致
   * 兼顾成功标准与定义

* 与架构师紧密合作（尤其是在制定 AEM 开发战略时），以定义模板与组件之间的关系、第三方应用程序的集成策略及任何专用功能。

### 质量负责人 {#quality-lead}

质量负责人的职责包括：

* 负责交付成果的质量；确保其符合成功标准及客户定义的任何 KPI。
* 定义质量量度，与所有利益相关者达成一致，拟定测试计划并确保执行。
* 创建报告并向项目利益相关者提交报告。

### 系统工程师 {#system-engineer}

系统工程师的职责包括：

* 负责监督项目基础架构。
* 具体负责：

   * 搭建内部开发与测试环境
   * 并确保这些系统与客户系统相匹配

* 提供硬件建议，监控各项实施，并在上线前后提供运维支持。

### 安全负责人 {#security-lead}

安全负责人的职责包括：

* 负责解决方案的整体安全概念，确保其符合客户的各项需求与策略。
* 提供安全概念与安全运营方案，并就基于硬件的安全措施（如分区与防火墙）提供建议。

### 其他角色 {#other-persona}

* 利益相关者

   * 通常是业务方面人员，他们对项目的成功有既得利益。他们往往会参与预算投入。

* 法律顾问

   * 在合同谈判过程中需要法律顾问的支持。

* 培训师

   * 根据项目的规模和性质，可聘请专业培训师为相关群体开发并开展培训课程。

* 技术文档撰写人员

   * 根据项目的规模和性质，可聘请专业的技术写作者为特定群体编写指南和手册。例如，供系统管理员使用的《维护手册》或供作者使用的《用户指南》。

* 系统管理员

   * 负责系统的日常运行与维护。

* 作者与最终用户

   * 使用系统创建和维护网站内容的人员。

## 必需文档与可交付结果 {#required-documents-and-deliverables}

该清单涵盖了每个里程碑所需的&#x200B;**必需文档**&#x200B;与&#x200B;**可交付结果**。

* 两者之间并非 1:1 对应关系；例如，一组必需文档可能对应一个可交付结果。
* 某个角色的可交付结果在同一里程碑中可能成为另一个角色的必需文档。

### 必需文件 {#required-documents}

**必需文档**&#x200B;是在相应角色产出可交付结果时所需的资料。

对于每份&#x200B;**必需文档**，相关角色应标明：

* **Y/N**：是否已接收。
* **1-3**：对所接收文档质量的评价。

### 可交付结果 {#deliverables}

在每个里程碑中，相应角色需交付特定文档，从而履行该具体里程碑的职责。

对于每个&#x200B;**可交付结果**，相关角色必须标明：

* **Y/N**：是否已完成。

可交付结果通常会作为当前或后续里程碑的&#x200B;**必需文档**&#x200B;使用。

## 相关最佳做法 {#related-best-practices}

有关部署、管理、开发或创作的最佳做法，请参阅以下内容：

* 与 AEM 项目管理相关的其他最佳做法与指南：
   * [硬件选型指南](/help/managing/hardware-sizing-guidelines.md)
   * [企业 DevOps](/help/managing/enterprise-devops.md)
   * [SEO 和 URL 管理最佳做法](/help/managing/seo-and-url-management.md)
   * [AEM 与 Web 无障碍指南](/help/managing/web-accessibility.md)
   * [通用数据保护条例](/help/managing/data-protection-and-privacy.md)* [部署与维护最佳做法](/help/sites-deploying/best-practices.md)
* [管理最佳做法](/help/sites-administering/administer-best-practices.md)
* [开发最佳做法](/help/sites-developing/best-practices.md)
* [创作最佳做法](/help/sites-authoring/best-practices.md)

## 关键文档区域 {#key-documentation-areas}

* AEM 文档
此外，以下 AEM 文档部分尤为重要（但不限于此清单）：

   * [安全性](/help/sites-developing/security.md)
   * [推荐的部署](/help/sites-deploying/recommended-deploys.md)
   * [企业 DevOps](/help/managing/enterprise-devops.md)
   * [硬件选型](/help/managing/hardware-sizing-guidelines.md)
   * AEM 概念：

      * [开发——基础知识](/help/sites-developing/the-basics.md)
      * [MSM 概念](/help/sites-administering/msm.md)
      * [HTML 模板语言（HTL）](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=zh-Hans)

* 相关文档

   * Adobe Experience Cloud - [Adobe Experience Cloud 规划](https://experienceleague.adobe.com/docs/core-services/interface/services/core-services.html?lang=zh-Hans)
