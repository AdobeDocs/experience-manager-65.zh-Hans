---
title: 使用媒体处理程序和工作流处理资源
description: 了解媒体处理程序以及如何使用工作流对您的数字资产执行任务。
mini-toc-levels: 1
contentOwner: AG
role: User
feature: Workflow,Renditions
exl-id: cfd6c981-1a35-4327-82d7-cf373d842cc3
solution: Experience Manager, Experience Manager Assets
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '2113'
ht-degree: 3%

---

# 使用媒体处理程序和工作流处理资源 {#processing-assets-using-media-handlers-and-workflows}

[!DNL Adobe Experience Manager Assets]附带一组默认的工作流和媒体处理程序以处理资产。 工作流定义要在资产上执行的任务，然后将特定任务委派给媒体处理程序，例如缩略图生成或元数据提取。

可以将工作流配置为在上传特定MIME类型的资产时自动执行。 处理步骤是根据一系列[!DNL Assets]媒体处理程序定义的。 [!DNL Experience Manager]提供了一些[内置处理程序](#default-media-handlers)，额外的处理程序可以是[自定义开发的](#creating-a-new-media-handler)，也可以通过将进程委托给[命令行工具](#command-line-based-media-handler)来定义。

媒体处理程序是[!DNL Assets]中的服务，可对资源执行特定操作。 例如，将MP3音频文件上载到[!DNL Experience Manager]时，工作流会触发一个MP3处理程序，该处理程序将提取元数据并生成缩略图。 媒体处理程序与工作流一起使用。 [!DNL Experience Manager]中支持最常见的MIME类型。 可以通过扩展或创建工作流、扩展或创建媒体处理程序或禁用和启用媒体处理程序来对资产执行特定任务。

>[!NOTE]
>
>有关[!DNL Assets]支持的所有格式以及每种格式支持的功能的说明，请参阅[支持的资产格式](assets-formats.md)页面。

## 默认媒体处理程序 {#default-media-handlers}

以下媒体处理程序在[!DNL Assets]中可用，可处理最常见的MIME类型：

<!-- TBD: Java versions should not be set to 1.5. Must be updated.
-->

| 处理程序名称 | 服务名称（在系统控制台中） | 支持的MIME类型 |
|--------------|--------------------------------------|----------------------|
| [!UICONTROL 文本处理程序] | com.day.cq.dam.core.impl.handler.TextHandler | text/plain |
| [!UICONTROL PdfHandler] | com.day.cq.dam.handler.standard.pdf.PdfHandler | <ul><li>application/pdf</li><li>application/illustrator</li></ul> |
| [!UICONTROL JpegHandler] | com.day.cq.dam.core.impl.handler.JpegHandler | image/jpeg |
| [!UICONTROL Mp3Handler] | com.day.cq.dam.handler.standard.mp3.Mp3Handler | audio/mpeg<br><b>重要信息</b> — 已上传的MP3文件[使用第三方库](https://www.zxdr.it/programmi/SistEvolBDD/LibJava/doc/de/vdheide/mp3/MP3File.html)处理。 如果MP3具有可变比特率(VBR)，则库会计算不准确的近似长度。 |
| [!UICONTROL ZipHandler] | com.day.cq.dam.handler.standard.zip.ZipHandler | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | com.day.cq.dam.handler.standard.pict.PictHandler | image/pict |
| [!UICONTROL StandardImageHandler] | com.day.cq.dam.core.impl.handler.StandardImageHandler | <ul><li>image/gif </li><li> image/png </li> <li>application/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler | application/msword |
| [!UICONTROL MSPowerPointHandler] | com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | com.day.cq.dam.handler.standard.epub.EPubHandler | application/epub+zip |
| [!UICONTROL GenericAssetHandler] | com.day.cq.dam.core.impl.handler.GenericAssetHandler | 如果未找到其他处理程序来从资产中提取数据，则进行回退 |

{style="table-layout:auto"}

所有处理程序均执行以下任务：

* 从资源提取所有可用元数据。
* 创建资源的缩略图图像。

要查看活动媒体处理程序，请执行以下操作：

1. 在浏览器中，导航到`https://localhost:4502/system/console/components`。
1. 单击 `com.day.cq.dam.core.impl.store.AssetStoreImpl`。
1. 将显示包含所有活动媒体处理程序的列表。 例如：

![chlimage_1-437](assets/chlimage_1-437.png)

## 在工作流中使用媒体处理程序对资产执行任务 {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

媒体处理程序是与工作流一起使用的服务。

[!DNL Experience Manager]有一些默认的工作流来处理资产。 要查看它们，请打开“工作流”控制台，然后单击&#x200B;**[!UICONTROL 模型]**&#x200B;选项卡：以[!DNL Assets]开头的工作流标题是特定于资产的工作流标题。

可以扩展现有工作流，并创建新工作流以根据特定要求处理资产。

以下示例演示如何增强 **[!UICONTROL AEM Assets 同步工作流]**，以便为除 PDF 文档外的所有资产生成子资产。

### 禁用或启用媒体处理程序 {#disabling-enabling-a-media-handler}

可以通过Apache Felix Web管理控制台禁用或启用媒体处理程序。 禁用媒体处理程序后，将不会对资源执行其任务。

启用/禁用媒体处理程序：

1. 在浏览器中，导航到`https://<host>:<port>/system/console/components`。
1. 单击媒体处理程序名称旁边的&#x200B;**[!UICONTROL 禁用]**。 例如：`com.day.cq.dam.handler.standard.mp3.Mp3Handler`。
1. 刷新页面：媒体处理程序旁边会显示一个图标，指示已禁用该页面。
1. 要启用媒体处理程序，请单击媒体处理程序名称旁边的&#x200B;**[!UICONTROL 启用]**。

### 创建媒体处理程序 {#creating-a-new-media-handler}

要支持新的媒体类型或对资产执行特定任务，需要创建媒体处理程序。 本节介绍如何继续。

#### 重要类和接口 {#important-classes-and-interfaces}

启动实现的最佳方法是继承提供的抽象实现，该实现处理大多数事务并提供合理的默认行为： `com.day.cq.dam.core.AbstractAssetHandler`类。

此类已提供抽象服务描述符。 因此，如果您从此类继承并使用maven-sling-plugin，请确保将继承标志设置为`true`。

实施以下方法：

* `extractMetadata()`：提取所有可用的元数据。
* `getThumbnailImage()`：根据传递的资源创建缩略图图像。
* `getMimeTypes()`：返回资源MIME类型。

以下是示例模板：

```Java
package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts }
```

接口和类包括：

* `com.day.cq.dam.api.handler.AssetHandler`接口：此接口描述添加了对特定MIME类型的支持的服务。 添加MIME类型需要实现此接口。 该界面包含用于导入和导出特定文档、用于创建缩略图和提取元数据的方法。
* `com.day.cq.dam.core.AbstractAssetHandler`类：此类用作所有其他资产处理程序实现的基础，并提供常用功能。
* `com.day.cq.dam.core.AbstractSubAssetHandler` class:
   * 此类用作所有其他资产处理程序实现的基础，并提供常用功能以及子资产提取的常用功能。
   * 启动实现的最佳方法是继承提供的抽象实现，该实现处理大多数事务并提供合理的默认行为：com.day.cq.dam.core.AbstractAssetHandler类。
   * 此类已提供抽象服务描述符。 因此，如果您从此类继承并使用maven-sling-plugin，请确保将继承标志设置为true。

必须实施以下方法：

* `extractMetadata()`：此方法提取所有可用的元数据。
* `getThumbnailImage()`：此方法根据传递的资源创建缩略图图像。
* `getMimeTypes()`：此方法返回资产MIME类型。

以下是示例模板：

包my.own.stuff； /&amp;amp；ast；&amp;amp；ast； &amp;amp；@scr.component inherit=&quot;true&quot; &amp;amp；ast； @scr.service &amp;amp；ast；/ public类MyMediaHandler扩展com.day.cq.dam.core.AbstractAssetHandler { //实现相关部分}

接口和类包括：

* `com.day.cq.dam.api.handler.AssetHandler`接口：此接口描述添加了对特定MIME类型的支持的服务。 添加MIME类型需要实现此接口。 该界面包含用于导入和导出特定文档、用于创建缩略图和提取元数据的方法。
* `com.day.cq.dam.core.AbstractAssetHandler`类：此类用作所有其他资产处理程序实现的基础，并提供常用功能。
* `com.day.cq.dam.core.AbstractSubAssetHandler`类：此类用作所有其他资产处理程序实现的基础，并为子资产提取提供常用功能以及常用功能。

#### 示例：创建特定的文本处理程序 {#example-create-a-specific-text-handler}

在此部分中，您将创建一个特定的文本处理程序，以生成带有水印的缩略图。

按照以下步骤操作：

请参阅[开发工具](../sites-developing/dev-tools.md)以使用[!DNL Maven]插件安装和设置Eclipse，并设置[!DNL Maven]项目所需的依赖项。

执行以下过程后，将TXT文件上载到[!DNL Experience Manager]时，将提取文件的元数据并生成两个带水印的缩略图。

1. 在Eclipse中，创建`myBundle` [!DNL Maven]项目：

   1. 在菜单栏中，单击&#x200B;**[!UICONTROL 文件]** > **[!UICONTROL 新建]** > **[!UICONTROL 其他]**。
   1. 在对话框中，展开[!DNL Maven]文件夹，选择[!DNL Maven]项目，然后单击&#x200B;**[!UICONTROL 下一步]**。
   1. 选中“创建简单项目”框和“使用默认Workspace位置”框，然后单击&#x200B;**[!UICONTROL 下一步]**。
   1. 定义[!DNL Maven]项目：

      * 组ID： `com.day.cq5.myhandler`。
      * 工件ID： myBundle。
      * 名称：我的[!DNL Experience Manager]包。
      * 描述：这是我的[!DNL Experience Manager]捆绑包。

   1. 单击&#x200B;**[!UICONTROL 完成]**。

1. 将[!DNL Java™]编译器设置为版本1.5：

   1. 右键单击`myBundle`项目，选择[!UICONTROL 属性]。
   1. 选择[!UICONTROL Java™编译器]并将以下属性设置为1.5：

      * 编译器符合性级别
      * 生成的.class文件兼容性
      * Source兼容性

   1. 单击&#x200B;**[!UICONTROL 确定]**。 在对话框窗口中，单击&#x200B;**[!UICONTROL 是]**。

1. 将`pom.xml`文件中的代码替换为以下代码：

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!-- ====================================================================== -->
    <!-- P A R E N T P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <parent>
     <groupId>com.day.cq.dam</groupId>
     <artifactId>dam</artifactId>
     <version>5.2.14</version>
     <relativePath>../parent</relativePath>
    </parent>
    <!-- ====================================================================== -->
    <!-- P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <groupId>com.day.cq5.myhandler</groupId>
    <artifactId>myBundle</artifactId>
    <name>My CQ5 bundle</name>
    <version>0.0.1-SNAPSHOT</version>
    <description>This is my CQ5 bundle</description>
    <packaging>bundle</packaging>
    <!-- ====================================================================== -->
    <!-- B U I L D D E F I N I T I O N -->
    <!-- ====================================================================== -->
    <build>
     <plugins>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-scr-plugin</artifactId>
      </plugin>
      <plugin>
       <groupId>org.apache.sling</groupId>
       <artifactId>maven-sling-plugin</artifactId>
       <configuration>
        <slingUrlSuffix>/libs/dam/install/</slingUrlSuffix>
       </configuration>
      </plugin>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-bundle-plugin</artifactId>
       <extensions>true</extensions>
       <configuration>
        <instructions>
         <Bundle-Category>cq5</Bundle-Category>
         <Export-Package> com.day.cq5.myhandler </Export-Package>
        </instructions>
       </configuration>
      </plugin>
     </plugins>
    </build>
    <!-- ====================================================================== -->
    <!-- D E P E N D E N C I E S -->
    <!-- ====================================================================== -->
    <dependencies>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-api</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-core</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq</groupId>
      <artifactId>cq-commons</artifactId>
     </dependency>
     <dependency>
      <groupId>javax.jcr</groupId>
      <artifactId>jcr</artifactId>
     </dependency>
     <dependency>
      <groupId>org.apache.felix</groupId>
      <artifactId>org.osgi.compendium</artifactId>
     </dependency>
     <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-lang</groupId>
      <artifactId>commons-lang</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-collections</groupId>
      <artifactId>commons-collections</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-io</groupId>
      <artifactId>commons-io</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-gfx</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-text</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.workflow</groupId>
      <artifactId>cq-workflow-api</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.wcm</groupId>
      <artifactId>cq-wcm-foundation</artifactId>
      <version>5.2.22</version>
     </dependency>
    </dependencies>
   ```

1. 创建包`com.day.cq5.myhandler`，其中包含`myBundle/src/main/java`下的[!DNL Java™]类：

   1. 在myBundle下，右键单击`src/main/java`，选择新建，然后选择包。
   1. 将其命名为`com.day.cq5.myhandler`，然后单击“完成”。

1. 创建[!DNL Java™]类`MyHandler`：

   1. 在[!DNL Eclipse]中的`myBundle/src/main/java`下，右键单击`com.day.cq5.myhandler`包。 选择[!UICONTROL 新建]，然后选择[!UICONTROL 类]。
   1. 在对话框窗口中，将[!DNL Java™]类命名为`MyHandler`并单击[!UICONTROL 完成]。 [!DNL Eclipse]创建并打开文件`MyHandler.java`。
   1. 在`MyHandler.java`中，使用以下内容替换现有代码，然后保存更改：

   ```java
   package com.day.cq5.myhandler;
   import java.awt.Color;
   import java.awt.Rectangle;
   import java.awt.image.BufferedImage;
   import java.io.IOException;
   import java.io.InputStream;
   import java.io.InputStreamReader;
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   import org.apache.commons.io.IOUtils;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import com.day.cq.dam.api.metadata.ExtractedMetadata;
   import com.day.cq.dam.core.AbstractAssetHandler;
   import com.day.image.Font;
   import com.day.image.Layer;
   import com.day.cq.wcm.foundation.ImageHelper;
   
   /**
    * The <code>MyHandler</code> can extract text files
    * @scr.component inherit="true" immediate="true" metatype="false"
    * @scr.service
    *
    **/
   
   public class MyHandler extends AbstractAssetHandler {
    /** * Logger instance for this class. */
    private static final Logger log = LoggerFactory.getLogger(MyHandler.class);
    /** * Music icon margin */
    private static final int MARGIN = 10;
    /** * @see com.day.cq.dam.api.handler.AssetHandler#getMimeTypes() */
    public String[] getMimeTypes() {
     return new String[] {"text/plain"};
    }
   
    public ExtractedMetadata extractMetadata(Node asset) {
     ExtractedMetadata extractedMetadata = new ExtractedMetadata();
     InputStream data = getInputStream(asset);
     try {
      // read text data
      InputStreamReader reader = new InputStreamReader(data);
      char[] buffer = new char[4096];
      String text = "";
      while (reader.read(buffer) != -1) {
       text += new String(buffer);
      }
      reader.close();
      long wordCount = this.wordCount(text);
      extractedMetadata.setProperty("text", text);
      extractedMetadata.setMetaDataProperty("Word Count",wordCount);
      setMimetype(extractedMetadata, asset);
     } catch (Throwable t) {
      log.error("handling error: " + t.toString(), t);
     } finally {
      IOUtils.closeQuietly(data);
     }
     return extractedMetadata; }
    // ----------------------< helpers >----------------------------------------
    protected BufferedImage getThumbnailImage(Node node) {
     ExtractedMetadata metadata = extractMetadata(node);
     final String text = (String) metadata.getProperty("text");
     // create text layer
     final Layer layer = new Layer(500, 600, Color.WHITE);
     layer.setPaint(Color.black);
     Font font = new Font("Arial", 12);
     String displayText = this.getDisplayText(text, 600, 12);
     if(displayText!=null && displayText.length() > 0) {
      // commons-gfx Font class would throw IllegalArgumentException on empty or null text
      layer.drawText(10, 10, 500, 600, displayText, font, Font.ALIGN_LEFT, 0, 0);
     }
     // create watermark and merge with text layer
     Layer watermarkLayer;
     try {
      final Session session = node.getSession();
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/we-retail/en/products/apparel/gloves/Gloves.jpg");
      watermarkLayer.setX(MARGIN);
      watermarkLayer.setY(MARGIN);
      layer.merge(watermarkLayer);
     } catch (RepositoryException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
     } catch (IOException e) {
      // TODO Auto-generated catch block
      e.printStackTrace(); }
     layer.crop(new Rectangle(510, 600));
     return layer.getImage(); }
    // ---------------< private >-----------------------------------------------
    /**
     * This method cuts lines if the text file is too long..
     * * @param text
     * * text to check
     * * @param height
     * * text box height (px)
     * * @param fontheight
     * * font height (px)
     * * @return the text which will fit into the box
     */
    private String getDisplayText(String text, int height, int fontheight) {
     String trimmedText = text.trim();
     int numOfLines = height / fontheight;
     String lines[] = trimmedText.split("\n");
     if (lines.length <= numOfLines) {
      return trimmedText;
     } else {
      String cuttetText = "";
      for (int i = 0; i < numOfLines; i++) {
       cuttetText += lines[i] + "\n";
      }
      return cuttetText;
     }
    }
    /**
     * * This method counts the number of words in a string
     * * @param text the String whose words would like to be counted
     * * @return the number of words in the string
     * */
    private long wordCount(String text) {
     // We need to keep track of the last character, if we have two whitespaces in a row we do not want to double count.
     // The starting of the document is always a whitespace.
     boolean prevWhiteSpace = true;
     boolean currentWhiteSpace = true;
     char c; long numwords = 0;
     int j = text.length();
     int i = 0;
     while (i < j) {
      c = text.charAt(i++);
      if (c == 0) { break; }
      currentWhiteSpace = Character.isWhitespace(c);
      if (currentWhiteSpace && !prevWhiteSpace) { numwords++; }
      prevWhiteSpace = currentWhiteSpace;
     }
     // If we do not end with a whitespace then we need to add one extra word.
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. 编译[!DNL Java™]类并创建捆绑包：

   1. 右键单击`myBundle`项目，选择&#x200B;**[!UICONTROL 运行方式]**，然后选择&#x200B;**[!UICONTROL Maven安装]**。
   1. 在`myBundle/target`下创建了包`myBundle-0.0.1-SNAPSHOT.jar`（包含已编译的类）。

1. 在CRX资源管理器中，在`/apps/myApp`下创建一个节点。 名称= `install`，类型= `nt:folder`。
1. 复制包`myBundle-0.0.1-SNAPSHOT.jar`并将其存储在`/apps/myApp/install`下（例如，使用WebDAV）。 新文本处理程序现在在[!DNL Experience Manager]中处于活动状态。
1. 在浏览器中，打开[!UICONTROL Apache Felix Web管理控制台]。 选择[!UICONTROL 组件]选项卡并禁用默认文本处理程序`com.day.cq.dam.core.impl.handler.TextHandler`。

## 基于命令行的媒体处理程序 {#command-line-based-media-handler}

[!DNL Experience Manager]允许您在工作流中运行任何命令行工具来转换资产（如[!DNL ImageMagick]）并将新演绎版添加到该资产。 仅在托管[!DNL Experience Manager]服务器的磁盘上安装命令行工具，并向工作流添加和配置进程步骤。 调用的进程`CommandLineProcess`也根据特定的MIME类型进行筛选，并根据新演绎版创建多个缩略图。

以下转换可以自动运行并存储在[!DNL Assets]中：

* 使用[ImageMagick](https://www.imagemagick.org/script/index.php)和[Ghostscript](https://www.ghostscript.com/)的EPS和AI转换。
* 使用[FFmpeg](https://ffmpeg.org/)的FLV视频转码。
* 使用[LAME](https://lame.sourceforge.io/)的MP3编码。
* 使用[SOX](https://sourceforge.net/projects/sox/)进行音频处理。

>[!NOTE]
>
>在非Windows系统上，FFmpeg工具在为文件名中包含单引号(&#39;)的视频资源生成演绎版时返回错误。 如果您的视频文件的名称包含单引号，请先将其删除，然后再上传到[!DNL Experience Manager]。

`CommandLineProcess`进程按列出的顺序执行以下操作：

* 根据特定的MIME类型筛选文件（如果指定）。
* 在托管[!DNL Experience Manager]服务器的磁盘上创建临时目录。
* 将原始文件流式传输到临时目录。
* 执行由步骤的参数定义的命令。 正在临时目录中以运行[!DNL Experience Manager]的用户的权限执行该命令。
* 将结果流式传输回[!DNL Experience Manager]服务器的格式副本文件夹。
* 删除临时目录。
* 如果指定，则根据这些演绎版创建缩略图。 缩略图的数量和尺寸由步骤的参数定义。

### 使用[!DNL ImageMagick]的示例 {#an-example-using-imagemagick}

以下示例说明如何设置命令行流程步骤，以便每次将具有miMIME e类型GIF或TIFF的资源添加到[!DNL Experience Manager]服务器上的`/content/dam`时，都会创建原始资源的翻转图像。 还创建了另外三个缩略图140x100、48x48和10x250。

为此，请使用[!DNL ImageMagick]。 [!DNL ImageMagick]是一个免费的命令行软件，用于创建、编辑和合成位图图像。

在托管[!DNL Experience Manager]服务器的磁盘上安装[!DNL ImageMagick]：

1. 安装[!DNL ImageMagick]：请参阅[ImageMagick文档](https://www.imagemagick.org/script/download.php)。
1. 设置该工具，以便在命令行中运行`convert`。
1. 要查看工具是否正确安装，请在命令行上运行以下命令`convert -h`。

   它会显示一个帮助屏幕，其中包含转换工具的所有可能选项。

   >[!NOTE]
   >
   >在某些Windows版本中，转换命令可能无法运行，因为它与[!DNL Windows]安装中的本机转换实用程序冲突。 在这种情况下，请提及用于将图像文件转换为缩略图的[!DNL ImageMagick]软件的完整路径。 例如：`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`。

1. 要查看该工具是否正常运行，请将JPG映像添加到工作目录中，并在命令行上运行命令convert `<image-name>.jpg -flip <image-name>-flipped.jpg`。 翻转的图像将添加到目录中。 然后，将命令行流程步骤添加到&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;工作流。
1. 转到&#x200B;**[!UICONTROL 工作流]**&#x200B;控制台。
1. 在&#x200B;**[!UICONTROL 模型]**&#x200B;选项卡中，编辑&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;模型。
1. 将&#x200B;**[!UICONTROL 启用Web的演绎版]**&#x200B;步骤的[!UICONTROL 参数]更改为： `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`。
1. 保存工作流。

要测试修改后的工作流，请将资产添加到`/content/dam`。

1. 在文件系统中，获取您选择的TIFF映像。 将其重命名为`myImage.tiff`并将其复制到`/content/dam`，例如，通过使用WebDAV。
1. 转到&#x200B;**[!UICONTROL CQ5 DAM]**&#x200B;控制台，例如`https://localhost:4502/libs/wcm/core/content/damadmin.html`。
1. 打开资产&#x200B;**[!UICONTROL myImage.tiff]**，并验证是否已创建翻转的图像和三个缩略图。

#### 配置CommandLineProcess进程步骤 {#configuring-the-commandlineprocess-process-step}

本节介绍如何设置 [!UICONTROL CommandLineProcess] 的[!UICONTROL 进程参数]。

使用逗号分隔[!UICONTROL 进程参数]的值，并且不要以空格开头。

| 参数 — 格式 | 描述 |
|---|---|
| mime：&lt;mime-type> | 可选参数。 如果资产的MIME类型与参数中的相同，则会应用该流程。 <br>可以定义多个MIME类型。 |
| tn：&lt;宽度>：&lt;高度> | 可选参数。 该过程会使用参数中定义的维度创建一个缩略图。 <br>可以定义多个缩略图。 |
| cmd： &lt;命令> | 定义执行的命令。 语法取决于命令行工具。 只能定义一个命令。 <br>以下变量可用于创建命令：<br>`${filename}`：输入文件的名称，例如original.jpg <br> `${file}`：输入文件的完整路径名，例如，`/tmp/cqdam0816.tmp/original.jpg` <br> `${directory}`：输入文件的目录，例如`/tmp/cqdam0816.tmp` <br>`${basename}`：不带扩展名的输入文件的名称，例如，原始<br>`${extension}`：输入文件的扩展名，例如JPG。 |

例如，如果在托管[!DNL Experience Manager]服务器的磁盘上安装了[!DNL ImageMagick]，并且您使用[!UICONTROL CommandLineProcess]作为实现和以下值作为[!UICONTROL 进程参数]创建进程步骤：

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

然后，当工作流运行时，该步骤仅适用于将`image/gif`或`mime:image/tiff`作为`mime-types`的资产。 它创建原始图像的翻转图像，将其转换为JPG，并创建三个尺寸为140x100、48x48和10x250的缩略图。

使用以下[!UICONTROL 进程参数]，使用[!DNL ImageMagick]创建三个标准缩略图：

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

使用以下[!UICONTROL 进程参数]，使用[!DNL ImageMagick]创建启用Web的演绎版：

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>[!UICONTROL CommandLineProcess]步骤仅适用于资源（类型为`dam:Asset`的节点）或资源的后代。

>[!MORELIKETHIS]
>
>* [处理资源](assets-workflow.md)
