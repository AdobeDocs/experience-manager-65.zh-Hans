---
title: Expression builder中的远程函数
seo-title: 表达式生成器
description: “对应管理”中的“表达式构建器”允许您创建表达式和远程函数。
seo-description: “对应管理”中的“表达式构建器”允许您创建表达式和远程函数。
uuid: 6afb84c0-ad03-4bb1-a154-d46cc47650ae
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 68e3071e-7ce6-4bdc-8561-14bcaeae2b6c
docset: aem65
translation-type: tm+mt
source-git-commit: 5a586758da84f467e075adcc33cdcede2fbf09c7

---


# Expression builder中的远程函数{#remote-functions-in-expression-builder}

使用Expression Builder，您可以创建对数据字典或最终用户提供的数据值执行计算的表达式或条件。 对应管理使用表达式评估的结果选择文本、图像、列表和条件等资产，并根据需要将其插入对应资产。

## 使用表达式构建器创建表达式和远程函数 {#creating-expressions-and-remote-functions-with-expression-builder}

Expression builder内部使用JSP EL库，因此该表达式符合JSPEL语法。 有关详细信息，请参阅示 [例表达式](#exampleexpressions)。

![表达式生成器](assets/expressionbuilder.png)

### 运营商 {#operators}

表达式构建器的顶栏中提供了可用于表达式中的运算符。

### 示例表达式 {#exampleexpressions}

以下是几个常用的JSP EL示例，您可以在您的通信管理解决方案中使用这些示例：

* 要添加两个数字：${number1 + number2}
* 要连接两个字符串：${str1} ${str2}
* 要比较两个数字：${age &lt; 18}

您可以在 [JSP EL规范中找到更多信息](https://download.oracle.com/otn-pub/jcp/jsp-2.1-fr-spec-oth-JSpec/jsp-2_1-fr-spec-el.pdf)。 客户端表达式管理器不支持JSP EL规范中的某些变量和函数，具体而言：

* 在客户端计算的表达式的变量名 [] 中不支持集合索引和映射键（使用记号）。
* 以下是表达式中使用的函数的参数类型或返回类型：

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * 布尔型
   * java.lang.Integer
   * Int
   * java.util.list
   * java.lang.Short
   * 短
   * java.lang.Byte
   * 字节
   * java.lang.Double
   * 双精度型
   * java.lang.Long
   * 长整型
   * java.lang.Float
   * 浮点数
   * java.util.Calendar
   * java.util.Date
   * java.util.List

### 远程功能 {#remote-function}

远程函数提供在表达式中使用自定义逻辑的功能。 您可以编写自定义逻辑以在表达式中使用作为Java中的方法，而在表达式中也可以使用相同的函数。 可用的远程功能列在表达式编辑器左侧的“远程功能”选项卡下。

![remotefunction](assets/remotefunction.png)

#### 添加自定义远程功能 {#adding-custom-remote-functions}

您可以创建自定义捆绑包，以导出自己的远程函数以在表达式内部使用。 要创建用于导出您自己的远程功能的自定义捆绑包，请执行以下任务。 它演示了如何编写使其输入字符串大写的自定义函数。

1. 为OSGi服务定义一个接口，其中包含要导出以供表达式管理器使用的方法。
1. 在接口A上声明方法，并使用@ServiceMethod注释(com.adobe.exm.expeval.ServiceMethod)对它们进行注释。 表达式管理器忽略任何未加注释的方法。 ServiceMethod注释具有以下可选属性，也可以指定这些属性：

   1. **已启用**:确定是否启用此方法。 表达式管理器忽略禁用的方法。
   1. **familyId**:指定方法的系列（组）。 如果为空，则表达式管理器假定该方法属于默认系列。 没有从中选择函数的系列（默认的系列除外）的注册表。 Expression Manager通过采用由各种包导出的所有函数指定的所有系列ID的联合来动态创建注册表。 确保他们在此处指定的ID是可读的，因为它也显示在表达式创作用户界面中。
   1. **displayName**:函数的可读名称。 此名称用于创作用户界面中的显示目的。 如果为空，则表达式管理器使用函数的前缀和local-name构造默认名称。
   1. **说明**:函数的详细描述。 此说明用于创作用户界面中的显示目的。 如果为空，则表达式管理器使用函数的前缀和local-name构造默认描述。

   ```java
   package mergeandfuse.com;
   import com.adobe.exm.expeval.ServiceMethod;
   
   public interface RemoteFunction {
    @ServiceMethod(enabled=true,displayName="Returns_all_caps",description="Function to convert to all CAPS", familyId="remote")
    public String toAllCaps(String name);
   
   }
   ```

   也可以选择使用@ServiceMethodParameter注释(com.adobe.exm.expeval.ServiceMethodParameter)对方法的参数进行注释。 此注释仅用于指定在创作用户界面中使用的方法参数的可读名称和说明。 确保接口方法的参数和返回值属于以下类型之一：

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * 布尔型
   * java.lang.Integer
   * Int
   * java.lang.Short
   * 短
   * java.lang.Byte
   * 字节
   * java.lang.Double
   * 双精度型
   * java.lang.Long
   * 长整型
   * java.lang.Float
   * 浮点数
   * java.util.Calendar
   * java.util.Date
   * java.util.List


1. 定义接口的实现，将其配置为OSGI服务并定义以下服务属性：

```
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "<service_id>"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
```

exm.service=true条目指示表达式管理器，该服务包含适合在表达式中使用的远程函数。 &lt;service_id>值必须是有效的Java标识符（字母数字、$、_，不含其他特殊字符）。 此值前缀为REMOTE_关键字，构成表达式内部使用的前缀。 例如，使用REMOTE_foo:bar()可以在表达式内部引用带有注释的方法bar()和服务属性中的服务ID foo的接口。

```
package mergeandfuse.com;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = true, immediate = true, label = "RemoteFunctionImpl")
@Service(value = RemoteFunction.class)
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "test1"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
public class RemoteFuntionImpl implements RemoteFunction {

 @Override
 public String toAllCaps(String name) {
  System.out.println("######Got######"+name);
  
  return name.toUpperCase();
 }
 
}
```

以下是要使用的示例存档：

* **GoodFunctions.jar.zip** 是包含示例远程函数定义的jar文件。 下载GoodFunctions.jar.zip文件并解压缩它以获取jar文件。
* **GoodFunctions.zip是用于定义自定义远程函数和为其创建包的源代码包。**

GoodFunctions.jar.zip

[获取文件](assets/goodfunctions.jar.zip)

GoodFunctions.zip

[获取文件](assets/goodfunctions.zip)
