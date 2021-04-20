---
title: 使用代理UI准备和发送交互式通信
seo-title: 使用代理UI准备和发送交互式通信
description: 代理UI允许代理准备交互式通信并将其发送到后续进程。 代理根据允许进行所需的修改，并将交互通信提交到帖子流程，如电子邮件或打印。
seo-description: 使用代理UI准备和发送交互式通信
uuid: d1a19b83-f630-4648-9ad2-a22374e31aa9
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 110c86ea-9bd8-4018-bfcc-ca33e6b3f3ba
feature: Interactive Communication
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2062'
ht-degree: 0%

---


# 使用代理UI {#prepare-and-send-interactive-communication-using-the-agent-ui}准备和发送交互式通信

代理UI允许代理准备交互式通信并将其发送到后续进程。 代理根据允许进行所需的修改，并将交互通信提交到帖子流程，如电子邮件或打印。

## 概述 {#overview}

创建交互式通信后，代理可以在代理UI中打开交互式通信，并通过输入数据和管理内容和附件来准备收件人特定的副本。 最后，代理可以将交互式通信提交到后续进程。

在使用代理UI准备交互式通信时，代理在将交互式通信提交到帖子进程之前，会在代理UI中管理交互式通信的以下方面：

* **数据**:代理用户界面的“数据”选项卡显示交互通信中任何可编辑代理的变量和已解锁表单数据模型属性。这些变量/属性是在编辑或创建包含在交互通信中的文档片段时创建的。 “数据”选项卡还包括在XDP/打印渠道模板中构建的任何字段。 仅当代理可编辑的交互通信中存在任何变量、表单数据模型属性或字段时，才会显示“数据”选项卡。
* **内容**:在“内容”选项卡中，代理管理交互式通信中的内容，如文档片段和内容变量。在这些文档片段的属性中创建交互通信时，代理可以根据允许在文档片段中进行更改。 如果允许，代理还可以重新排序、添加/删除文档片段和添加分页符。
* **附件**:仅当交互式通信具有任何附件或代理具有库访问权限时，“附件”选项卡才会显示在代理UI中。座席可以更改或编辑附件，也可以不允许。

## 使用代理UI {#prepare-interactive-communication-using-the-agent-ui}准备交互式通信

1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 选择相应的交互式通信，然后点按&#x200B;**[!UICONTROL 打开代理UI]**。

   >[!NOTE]
   >
   >代理UI仅在选定的交互通信具有打印渠道时有效。

   ![openentiui](assets/openagentiui.png)

   根据交互通信的内容和属性，代理UI将显示以下三个选项卡：数据、内容和附件。

   ![阿根托](assets/agentuitabs.png)

   继续输入数据、管理内容和管理附件。

### 输入数据 {#enter-data}

1. 在“数据”选项卡中，根据需要输入变量、表单数据模型属性和打印模板(XDP)字段的数据。 填写标有星号(&amp;ast;)的所有必填字段，以启用&#x200B;**“提交**”按钮。

   点按“交互式通信”预览中的数据字段值，以在“数据”选项卡中突出显示相应的数据字段，反之亦然。

### 管理内容 {#manage-content}

在“内容”选项卡中，管理交互式通信中的内容，如文档片段和内容变量。

1. 选择&#x200B;**[!UICONTROL 内容]**。 此时将显示“交互式通信”的内容选项卡。

   ![agentuicontentab](assets/agentuicontenttab.png)

1. 根据需要，在“内容”选项卡中编辑文档片段。 要将焦点置于内容层次结构中的相关片段，您可以点按“交互通信”预览中的相关行或段落，或直接点按内容层次结构中的片段。

   例如，在下图的文档中选择了行为“立即在线付款……”的文档片段，在“内容”选项卡中选择了同一预览片段。

   ![contentmodulefocus](assets/contentmodulefocus.png)

   在“内容”或“数据”选项卡中，通过点按预览左上角的“高亮显示内容中的选定模块”(![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png))，可以禁用或启用在预览中点按/选择相关文本、段落或数据字段时转到文档片段的功能。

   在创建交互通信时，代理允许编辑的片段具有“编辑选定内容”(![iconeditedtedcontent](assets/iconeditselectedcontent.png))图标。 点按编辑选定内容图标以在编辑模式下启动片段并在其中进行更改。 使用以下选项设置文本格式和管理文本：

   * [格式选项](#formattingtext)

      * [从其他应用程序复制粘贴格式文本](#pasteformattedtext)
      * [高亮部分文本](#highlightemphasize)
   * [特殊字符](#specialcharacters)
   * [键盘快捷键](/help/forms/using/keyboard-shortcuts.md)

   有关Agent用户界面中各种文档片段可用的操作的详细信息，请参阅[Agent用户界面中的可用操作和信息](#actionsagentui)。

1. 要将分页符添加到交互通信的打印输出，请将光标置于要插入分页符的位置，然后选择“分页前”或“分页后”（![分页前后](assets/pagebreakbeforeafter.png)）。

   在交互通信中插入显式分页符占位符。 要视图显式分页符对交互式通信的影响，请参阅打印预览。

   ![excitpagebreak](assets/explicitpagebreak.png)

   继续管理交互式通信的附件。

### 管理附件{#manage-attachments}

1. 选择&#x200B;**[!UICONTROL 附件]**。 代理UI在创建交互式通信时按设置显示可用的附件。

   通过点按“视图”图标，您可以选择不随“交互式通信”一起提交附件，也可以点按附件中的叉号，从“交互式通信”中删除该附件（如果允许代理删除或隐藏附件）。 对于创建交互式通信时指定为必需的附件，将禁用“视图”和“删除”图标。

   ![attachmentsagentui](assets/attachmentsagentui.png)

1. 点按库访问（![库访问](assets/libraryaccess.png)）图标以访问内容库以将DAM资产作为附件插入。

   >[!NOTE]
   >
   >仅当在创建交互式通信时(在打印渠道的文档容器属性中)启用库访问时，“库访问”图标才可用。

1. 如果在创建交互式通信时未锁定附件的顺序，则可以通过选择附件并点按向下和向上箭头来重新排序附件。
1. 使用Web预览和打印预览查看这两个输出是否符合您的要求。

   如果您认为预览令人满意，请点按&#x200B;**[!UICONTROL Submit]**&#x200B;以提交/发送交互通信至后续流程。 或者，要进行更改，请退出预览以返回所做的更改。

## 设置文本格式{#formattingtext}

在代理UI中编辑文本片段时，工具栏会根据您选择要进行的编辑类型而发生更改：字体、段落或列表:

![样式](assets/typeofformattingtoolbar.png) ![格式工具栏字体工具栏](do-not-localize/fonttoolbar.png)

字体工具栏

![段落工具栏](do-not-localize/paragraphtoolbar.png)

段落工具栏

![列表工具栏](do-not-localize/listtoolbar.png)

列表工具栏

### 突出显示/强调部分文本{#highlightemphasize}

要高亮\突出显示可编辑片段中的部分文本，请选择文本并点按高亮颜色。

![highlighttextagentui](assets/highlighttextagentui.png)

### 粘贴格式化文本{#pasteformattedtext}

![过文本](assets/pastedtext.png)

### 在文本{#specialcharacters}中插入特殊字符

代理UI内置了对210个特殊字符的支持。 管理员可以通过自定义](/help/forms/using/custom-special-characters.md)添加对更多/自定义特殊字符的支持。[

#### 附件投放{#attachmentdelivery}

* 当使用服务器端API将交互式通信渲染为交互式或非交互式PDF时，渲染的PDF将包含附件作为PDF附件。
* 当将与交互式通信关联的后期进程作为“使用代理UI提交”的一部分加载时，附件将作为列表&lt;com.adobe.idp.文档> inAttachmentDocs参数传递。
* 投放机制工作流（如电子邮件和打印）还随PDF版本的交互式通信一起提供附件。

## 代理用户界面{#actionsagentui}中可用的操作和信息

### 文档片段{#document-fragments}

![](do-not-localize/contentoptionsdocfragments.png)

* **向上/向下箭头**:在交互通信中向上或向下移动文档片段的箭头。
* **删除**:如果允许，请从交互通信中删除文档片段。
* **分页前** (适用于目标区域的子片段):在文档片段前插入分页符。
* **缩进**:增大或减小文档片段的缩进。
* **Page Break After(适** 用于目标区域的子片段):在文档片段后插入分页符。

![docfragoptions](assets/docfragoptions.png)

* 编辑（仅限文本片段）：打开富文本编辑器以编辑文本文档片段。 有关详细信息，请参阅[格式化文本](#formattingtext)。

* 选择（眼睛图标）：包括\排除交互通信中的文档片段。
* 未填充值（信息）：指示文档片段中未填充变量的数量。

### 列表文档片段{#list-document-fragments}

![列表选项](assets/listoptions.png)

* 插入空行：插入新的空行。
* 选择（眼睛图标）：包括\排除交互通信中的文档片段。
* 跳过项目符号/编号：启用此选项可跳过列表文档片段中的项目符号/编号。
* 未填充值（信息）：指示文档片段中未填充变量的数量。

## 将交互通信另存为草稿{#save-as-draft}

您可以使用代理UI为每个交互式通信保存一个或多个草稿，并稍后检索草稿以继续处理它。 您可以为每个草稿指定一个不同的名称以标识它。

Adobe建议按顺序执行这些说明，以成功将交互式通信另存为草稿。

### 启用“另存为草图”功能{#before-save-as-draft}

默认情况下，“另存为拔模”(Save a Draft)功能未启用。 请执行以下步骤以启用该功能：

1. 实现[ccrDocumentInstance](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/ccr/ccrDocumentInstance/api/services/CCRDocumentInstanceService.html)服务提供商接口(SPI)。

   SPI允许您将交互式通信的草稿版本保存到数据库，其中草稿ID作为唯一标识符。 这些说明假定您事先已经了解如何使用Maven项目构建OSGi捆绑包。

   有关示例SPI实现，请参阅[示例ccrDocumentInstance SPI实现](#sample-ccrDocumentInstance-spi)。
1. 打开`http://<hostname>:<port>/ system/console/bundles`并点按&#x200B;**[!UICONTROL 安装/更新]**&#x200B;以上传OSGi包。 验证已上载包的状态是否显示为&#x200B;**活动**。 如果包的状态未显示为&#x200B;**活动**，请重新启动服务器。
1. 转到 `https://'[server]:[port]'/system/console/configMgr`.
1. 点按&#x200B;**[!UICONTROL 创建对应配置]**。
1. 选择&#x200B;**[!UICONTROL “启用使用CCRDocumentInstanceService]**&#x200B;保存”，然后点按&#x200B;**[!UICONTROL 保存]**。

### 将交互式通信另存为草稿{#save-as-draft-agent-ui}

请执行以下步骤将交互式通信另存为草稿：

1. 在Forms Manager中选择一个交互式通信，然后点按&#x200B;**[!UICONTROL 打开代理UI]**。

1. 在代理UI中进行适当的更改，然后点按&#x200B;**[!UICONTROL 另存为草稿]**。

1. 在&#x200B;**[!UICONTROL 名称]**&#x200B;字段中指定草稿的名称，然后点按&#x200B;**[!UICONTROL 完成]**。

将交互式通信另存为草稿后，点按&#x200B;**[!UICONTROL 保存更改]**&#x200B;以保存对草稿所做的任何进一步更改。

### 检索交互式通信的草稿{#retrieve-draft}

将交互式通信保存为草稿后，您可以检索它以继续处理它。 检索交互通信：

`https://server:port/aem/forms/createcorrespondence.hmtl?draftid=[draftid]`

[拖] 动到草稿版本的唯一标识符，该标识符在将交互式通信另存为草稿后生成。

>[!NOTE]
>
>如果在将交互通信另存为草稿后对它进行了任何更改，草稿版本将无法打开。

### 示例ccrDocumentInstance SPI实现{#sample-ccrDocumentInstance-spi}

实施`ccrDocumentInstance` SPI以将交互通信另存为草稿。 以下是`ccrDocumentInstance` SPI的示例实现。

```javascript
package Implementation;

import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.exception.CCRDocumentException;
import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.model.CCRDocumentInstance;
import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.services.CCRDocumentInstanceService;
import org.apache.commons.lang3.StringUtils;
import org.osgi.service.component.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.*;


@Component(service = CCRDocumentInstanceService.class, immediate = true)
public class CCRDraftService implements CCRDocumentInstanceService {

    private static final Logger logger = LoggerFactory.getLogger(CCRDraftService.class);

    private HashMap<String, Object> draftDataMap = new HashMap<>();

    @Override
    public String save(CCRDocumentInstance ccrDocumentInstance) throws CCRDocumentException {
        String documentInstanceName = ccrDocumentInstance.getName();
        if (StringUtils.isNotEmpty(documentInstanceName)) {
            logger.info("Saving ccrData with name : {}", ccrDocumentInstance.getName());
            if (!CCRDocumentInstance.Status.SUBMIT.equals(ccrDocumentInstance.getStatus())) {
                ccrDocumentInstance = mySQLDataBaseServiceCRUD(ccrDocumentInstance,null, "SAVE");
            }
        } else {
            logger.error("Could not save data as draft name is empty");
        }
        return ccrDocumentInstance.getId();
    }

    @Override
    public void update(CCRDocumentInstance ccrDocumentInstance) throws CCRDocumentException {
        String documentInstanceName = ccrDocumentInstance.getName();
        if (StringUtils.isNotEmpty(documentInstanceName)) {
            logger.info("Saving ccrData with name : {}", documentInstanceName);
            mySQLDataBaseServiceCRUD(ccrDocumentInstance, ccrDocumentInstance.getId(), "UPDATE");
        } else {
            logger.error("Could not save data as draft Name is empty");
        }
    }

    @Override
    public CCRDocumentInstance get(String id) throws CCRDocumentException {
        CCRDocumentInstance cCRDocumentInstance;
        if (StringUtils.isEmpty(id)) {
            logger.error("Could not retrieve data as draftId is empty");
            cCRDocumentInstance = null;
        } else {
            cCRDocumentInstance = mySQLDataBaseServiceCRUD(null, id,"GET");
        }
        return cCRDocumentInstance;
    }

    @Override
    public List<CCRDocumentInstance> getAll(String userId, Date creationTime, Date updateTime,
                                            Map<String, Object> optionsParams) throws CCRDocumentException {
        List<CCRDocumentInstance> ccrDocumentInstancesList = new ArrayList<>();

        HashMap<String, Object> allSavedDraft = mySQLGetALLData();
        for (String key : allSavedDraft.keySet()) {
            ccrDocumentInstancesList.add((CCRDocumentInstance) allSavedDraft.get(key));
        }
        return ccrDocumentInstancesList;
    }

    //The APIs call the service in the database using the following section.
    private CCRDocumentInstance mySQLDataBaseServiceCRUD(CCRDocumentInstance ccrDocumentInstance,String draftId, String method){
        if(method.equals("SAVE")){

            String autoGenerateId = draftDataMap.size() + 1 +"";
            ccrDocumentInstance.setId(autoGenerateId);
            draftDataMap.put(autoGenerateId, ccrDocumentInstance);
            return ccrDocumentInstance;

        }else if (method.equals("UPDATE")){

            draftDataMap.put(ccrDocumentInstance.getId(), ccrDocumentInstance);
            return ccrDocumentInstance;

        }else if(method.equals("GET")){

            return (CCRDocumentInstance) draftDataMap.get(draftId);

        }
        return null;
    }

    private HashMap<String, Object> mySQLGetALLData(){
        return draftDataMap;
    }
}
```

`save`、`update`、`get`和`getAll`操作调用数据库服务，将交互式通信保存为草稿，更新交互式通信，从数据库检索数据，并检索数据库中所有可用的交互式通信的数据。 此示例使用`mySQLDataBaseServiceCRUD`作为数据库服务的名称。

下表说明了示例`ccrDocumentInstance` SPI实现。 它演示了示例实现中`save`、`update`、`get`和`getAll`操作如何调用数据库服务。

<table> 
 <tbody>
 <tr>
  <td><p><strong>操作</strong></p></td>
  <td><p><strong>数据库服务示例</strong></p></td> 
   </tr>
  <tr>
   <td><p>您可以为交互式通信创建草稿或直接提交它。 保存操作的API将检查交互通信是否作为草稿提交，并包含草稿名称。 然后，API将调用mySQLDataBaseServiceCRUD服务，并将保存作为输入方法。</p></br><img src="assets/save-as-draft-save-operation.png"/></br>[#$sd1_sf1_dp9]</td>
   <td><p>mySQLDataBaseServiceCRUD服务验证“另存为”为输入方法，并生成一个自动生成的草稿ID并将其返回到AEM。 生成草稿ID的逻辑可能因数据库而异。</p></br><img src="assets/save-operation-service.png"/></br>[#$sd1_sf1_dp13]</td>
   </tr>
  <tr>
   <td><p>更新操作的API会检索交互式通信草稿的状态，并检查交互式通信是否包含草稿名称。 API调用mySQLDataBaseServiceCRUD服务以在数据库中更新该状态。</p></br><img src="assets/save-as-draft-update-operation.png"/></br>[#$sd1_sf1_dp17]</td>
   <td><p>mySQLDataBaseServiceCRUD服务将Update验证为输入方法，并将Interactive Communication草稿的状态保存在数据库中。</br></p><img src="assets/update-operation-service.png"/></td>
   </tr>
   <tr>
   <td><p>获取操作的API检查交互通信是否包含草稿ID。 然后，API调用mySQLDataBaseServiceCRUD服务，将Get作为输入方法来检索交互通信的数据。</br></p><img src="assets/save-as-draft-get-operation.png"/></td>
   <td><p>mySQLDataBaseServiceCRUD服务验证Get为输入方法，并基于草稿ID检索交互式通信的数据。</p></br><img src="assets/get-operation-service.png"/></br>[#$sd1_sf1_dp29]</td>
   </tr>
   <tr>
   <td><p>getAll操作的API调用mySQLGetALLData服务，以检索保存在数据库中的所有交互式通信的数据。</br></p><img src="assets/save-as-draft-getall-operation.png"/></td>
   <td><p>mySQLGetALLData服务检索数据库中保存的所有Interactive Communications的数据。</p></br><img src="assets/getall-operation-service.png"/></br>[#$sd1_sf1_dp37]</td>
   </tr>
  </tbody>
</table>

以下是作为实现一部分的`pom.xml`文件的示例：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.adobe.livecycle</groupId>
    <artifactId>draft-sample</artifactId>
    <version>2.0.0-SNAPSHOT</version>

    <name>Interact</name>
    <packaging>bundle</packaging>

    <dependencies>
        <dependency>
            <groupId>com.adobe.aemfd</groupId>
            <artifactId>aemfd-client-sdk</artifactId>
            <version>6.0.160</version>
        </dependency>
    </dependencies>


    <!-- ====================================================================== -->
    <!-- B U I L D D E F I N I T I O N -->
    <!-- ====================================================================== -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.felix</groupId>
                <artifactId>maven-bundle-plugin</artifactId>
                <version>3.3.0</version>
                <extensions>true</extensions>
                <executions>
                    <!--Configure extra execution of 'manifest' in process-classes phase to make sure SCR metadata is generated before unit test runs-->
                    <execution>
                        <id>scr-metadata</id>
                        <goals>
                            <goal>manifest</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <exportScr>true</exportScr>
                    <instructions>
                        <!-- Enable processing of OSGI DS component annotations -->
                        <_dsannotations>*</_dsannotations>
                        <!-- Enable processing of OSGI metatype annotations -->
                        <_metatypeannotations>*</_metatypeannotations>
                        <Bundle-SymbolicName>${project.groupId}-${project.artifactId}</Bundle-SymbolicName>
                    </instructions>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>8</source>
                    <target>8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
    <profiles>
        <profile>
            <id>autoInstall</id>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.apache.sling</groupId>
                        <artifactId>maven-sling-plugin</artifactId>
                        <executions>
                            <execution>
                                <id>install-bundle</id>
                                <phase>install</phase>
                                <goals>
                                    <goal>install</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
    </profiles>

</project>
```

>[!NOTE]
>
>确保将`aemfd-client-sdk`文件中的`pom.xml`依赖关系更新为6.0.160。
