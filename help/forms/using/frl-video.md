---
source-git-commit: b5e44b78659f0cb1b8b0025be30143b98c0bf8df
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---
# 视频脚本：为AEM Forms上的Adobe Acrobat设置功能限制许可(FRL)

| 可视化 | 标题 | 扬声器脚本 |
|--------|-------|---------------|
| 带有AEM Forms徽标和FRL图形的标题屏幕 | 简介 | 欢迎阅读本教程，了解如何在AEM Forms服务器上为Adobe Acrobat设置功能限制许可(FRL)。 在Adobe从永久许可证过渡到新FRL模型时，此过程至关重要。 |
| 显示带箭头指向FRL过渡的EOL日期的时间线 | 背景 | 拥有永久许可证的Adobe Acrobat Classic版本即将结束其生命周期，需要迁移到较新版本。 AEM Forms PDF Generator依赖Adobe Acrobat实现文档转换功能。 功能受限许可模型提供了相同的功能，但采用通过Adobe Admin Console管理的现代许可方法。 |
| 带有复选框和图标的所需项目的清单 | 先决条件 | 在开始之前，让我们确保您拥有所需的一切：首先，使用系统管理员权限访问Adobe Admin Console 。 其次，在Admin Console中具有部署管理员角色的用户帐户。 第三，运行AEM Forms的服务器上的本地管理员权限。 第四，AEM Forms服务器上的Windows 64位操作系统。 第五，为许可证激活提供稳定的互联网连接。 您还应该熟悉Adobe Admin Console界面，并了解AEM Forms部署架构。 |
| 带有备份图形的警告图标 | 重要说明 | 切记在启动之前备份任何自定义Acrobat设置，因为在此过程中您将需要卸载现有Acrobat安装。 |
| 显示1-7中编号步骤的流程图 | 流程概述 | 此过程涉及几个关键步骤：在Admin Console中准备FRL包、授予下载权限、卸载以前的Acrobat版本、安装新的Acrobat Pro、部署FRL包以及验证安装。 让我们逐步了解一下每个步骤。 |
| 突出显示了“包”选项卡的Adobe Admin Console界面屏幕截图 | 步骤1：Admin Console准备 | 首先，使用系统管理员权限登录到Adobe Admin Console。 导航到“包”选项卡，然后选择“功能受限许可证”。 单击“开始”按钮开始创建包。 |
| 创建包配置屏幕，突出显示设置 | 包配置 | 使用以下建议的设置配置您的包：为激活方法选择“脱机”，为授权选择“PDF生成”，为平台选择“Windows 64位”。 对于应用程序选择，仅在选定的应用程序中保留许可证文件。 为包提供一个描述性名称(如“Acrobat FRL AEM Forms”)，然后创建包。 |
| 包含“权限”对话框的“Admin Console用户”选项卡 | 步骤2：授予下载权限 | 接下来，您需要创建或识别将下载包的用户。 在Admin Console中，导航到用户选项卡，选择您的用户，并为其分配“部署管理员”角色。 这允许他们下载您创建的FRL包。 |
| Windows控制面板(应用与功能显示Acrobat) | 步骤3：卸载以前的Acrobat | 在安装新版本之前，必须完全删除所有现有的Acrobat安装。 打开Windows控制面板，导航到“应用”，找到Adobe Acrobat，然后选择“卸载”。 要彻底删除，请考虑使用Adobe Acrobat清洁器工具，尤其是当您在过程的后期遇到问题时。 |
| Adobe Acrobat DC下载页面中安装程序部分突出显示 | 步骤4：下载并安装Adobe Acrobat Pro | 卸载后，从Acrobat Pro DC下载页面下载相应的Adobe Acrobat安装程序。 为兼容PDF Generator，建议使用Windows 32位安装程序。 |
| 显示提取和设置步骤的安装过程 | 安装过程 | 将下载的zip文件解压到文件夹，找到Setup.exe，然后以管理员身份运行它。 按照屏幕上的说明完成安装。 安装后，打开一次Acrobat Pro以关闭任何欢迎对话框，并完成初始设置。 |
| Admin Console的“包”选项卡，其中突出显示了下载按钮 | 步骤5：下载FRL包 | 现在，使用您之前授予的下载权限帐户登录Adobe Admin Console。 导航到包选项卡，找到您的FRL包，然后将其下载到您的AEM Forms服务器。 |
| 键入命令时以管理员身份显示命令提示 | 步骤6：部署包 | 将下载的包解压到服务器上的某个目录。 以管理员身份打开命令提示符并导航到提取目录。 |
| 显示激活命令且语法高亮显示的命令行 | 激活命令 | 使用以下语法运行激活命令： `adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json`。 将JSON文件名替换为包中的确切文件名。 命令参数为： -p （用于平台）、 -i （用于安装许可证）和 — f （用于指定JSON文件路径）。 成功后，您会看到消息“操作已成功完成”。 |
| 显示命令参数和说明的表 | 命令参数 | p参数指定平台并自动检测操作系统。 i参数指示工具安装和激活许可证。 并且 — f参数指定JSON许可证文件的路径。 |
| AEM Forms管理界面显示PDF Generator服务 | 步骤7：测试和验证 | 最后，通过打开AEM Forms管理员界面并使用PDF Generator服务将简单文档转换为PDF来测试您的安装。 此外，您还可以通过打开Acrobat，导航到“帮助”→“关于”，并确认版本号和许可证状态来验证Acrobat Pro的安装。 |
| 分屏： Acrobat“关于”对话框和成功的PDF转换 | 验证 | 检查许可证是否在Acrobat中显示为已激活，以及PDF Generator是否能够成功转换文档。 |
| 常见错误和解决方案列表（包含图标） | 疑难解答提示 | 如果遇到问题，请检查以下常见问题：确保您以管理员身份运行命令提示符，验证JSON文件名是否正确，检查是否存在冲突的安装，并确认服务器是否具有激活所需的正确Internet连接。 |
| 带有复选标记的其他疑难解答项目 | 更多疑难解答 | 此外，还要检查服务器上的防火墙限制、软件包损坏或冲突Adobe ID。 如果其余所有操作失败，请联系Adobe支持并附上详细的错误消息。 |
| 包含复选标记图标和联系信息的成功屏幕 | 结论 | 现在，您已在您的AEM Forms服务器上为Adobe Acrobat成功设置功能限制许可。 如果您需要其他帮助，请联系Adobe支持或参阅Experience League上的详细文档。 |
| 带有Adobe徽标和致谢的结束屏幕 | 谢谢 | 感谢您观看本教程。 有关更多信息，请访问Experience League文档。 |

生产环境的&#x200B;**注释：**

- 此表中的每一行表示视频中的一个场景或主要部分
- 估计总时长：6-7分钟
- 尽可能包括实际流程的屏幕录制
- 使用标注和突出显示来强调重要的UI元素
- 包含用于辅助功能的字幕
- 考虑为查看器添加章节标记以跳转到特定章节