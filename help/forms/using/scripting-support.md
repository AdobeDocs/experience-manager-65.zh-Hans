---
title: HTML5表单的脚本支持
seo-title: HTML5表单的脚本支持
description: HTML5 Forms支持的JavaScript、FormCalc属性和其他方法。
seo-description: HTML5 Forms支持的JavaScript、FormCalc属性和其他方法。
uuid: 697d5ec4-c818-41e4-b813-883c01b7ff3a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4ef78c8c-783f-4aac-a499-692cd4acef75
translation-type: tm+mt
source-git-commit: b2fd6e0412ee0dacf7b68f4a0b219804dd4a6150

---


# HTML5表单的脚本支持 {#scripting-support-for-html-forms}

HTML5表单中支持的JavaScript、FormCalc属性和方法如下：

## $event {#event}

<table>
 <tbody>
  <tr>
   <th>属性 </th>
   <th>描述<br /> </th>
   <th>例外</th>
  </tr>
  <tr>
   <td><code>prevText</code></td>
   <td>指定字段内容，然后字段根据用户的操作进行更改。 可以调用此值，与撤消功能类似。</td>
   <td><p>不适用于下拉框和列表框。 <code>PrevText </code>在以下情况下无法正确工作：</p>
    <ul>
     <li>在iPad上的数字字段中键入一些特殊字符键(例如$、(、)、&amp;、@等)，以及 </li>
     <li>对于“日期”字段（当通过日历输入日期时）。<br /> </li>
    </ul> <p>不支持通过脚本设置值。</p> </td>
  </tr>
  <tr>
   <td><code>target</code></td>
   <td>指定事件所作用的对象。</td>
   <td>不支持通过脚本设置值。<br /> </td>
  </tr>
  <tr>
   <td><code>newtext</code></td>
   <td>指定字段在响应用户操作而更改后的内容。</td>
   <td><p>在以 <code>newText</code> 下情况下，该属性无法正常工作：</p>
    <ul>
     <li>论文本的选择与替换</li>
     <li>在删除、复制和粘贴文本时。</li>
     <li>在“数字”字段中键入一些特殊字符键(例如$、(、)、&amp;、@等)<br /> </li>
     <li>使用shift+字母数字组合。 </li>
     <li>使用日期／时间字段时。</li>
    </ul>
    <div>
      不支持通过脚本设置值。
    </div> </td>
  </tr>
  <tr>
   <td>更改</td>
   <td>指定用户在执行操作后立即键入或粘贴到字段中的值。 </td>
   <td><p>更改属性在以下情况下无法正常工作：</p>
    <ul>
     <li>论文本的选择与替换</li>
     <li>在删除、复制和粘贴文本时。</li>
     <li>在“数字”字段中键入一些特殊字符键(例如$、(、)、&amp;、@等)<br /> </li>
     <li>使用shift+字母数字组合。 </li>
     <li>使用日期／时间字段时。</li>
    </ul> <p>不支持通过脚本设置值。</p> </td>
  </tr>
  <tr>
   <td>关键</td>
   <td>确定用户是否按箭头键进行选择。 此属性仅适用于列表框和下拉列表。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>修饰符</td>
   <td>确定在执行特定事件时是否按住修饰符键（例如，Microsoft® Windows®上的Ctrl）。</td>
   <td>无</td>
  </tr>
 </tbody>
</table>

### $host {#host}

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
   <th>例外</th>
  </tr>
  <tr>
   <td><code>apptype</code></td>
   <td>返回主机的应用程序类型。 仅适用于客户端应用程序。</td>
   <td>退货 <code>HTML 5</code>。</td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>返回当前应用程序的名称。</td>
   <td>返回浏览器名称及其版本。 例如，在Chrome浏览器中，返回的值为 <code>Chrome &lt;version&gt;.</code></td>
  </tr>
  <tr>
   <td><code>numPages</code></td>
   <td>返回文档中的页数。</td>
   <td>HTML5表单的分页策略与PDF表单分页策略不相同。 因此，numPages API在这两种情况下都可以返回不同的值。</td>
  </tr>
  <tr>
   <td><code>platform</code></td>
   <td>返回一个字符串，它表示运行该脚本的计算机的平台。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>title</code></td>
   <td>指定文档的标题。 它仅对客户端应用程序可用。</td>
   <td>它以表单形式返回HTML文档的标题，而不是像“PDF表单”那样返回表单元数据标题。</td>
  </tr>
  <tr>
   <td><code>version</code></td>
   <td>返回表示当前应用程序版本号的字符串。</td>
   <td>它返回表单的版本。</td>
  </tr>
  <tr>
   <td><code>calculationsEnabled</code></td>
   <td>指定是否执行计算脚本。<br /> </td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>validationsEnabled</code></td>
   <td>指定是否将执行验证脚本。<br /> </td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>pageUp</code></td>
   <td>转到上一页。</td>
   <td>HTML5表单与PDF表单不遵循相同的分页策略，因此HTML5表单的上一页与PDF表单的上一页不同。</td>
  </tr>
  <tr>
   <td><code>pageDown</code></td>
   <td>移到表单的下一页。 在运行时使用pageDown方法。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>setFocus</code></td>
   <td>将键盘焦点设置到指定的字段。 该字段被指定为对象，或由字段的SOM表达式指定。 它仅对客户端应用程序可用。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>resetdata</code></td>
   <td>将字段重置为文档中的默认值。</td>
   <td>清除具有合并数据的表单中的所有数据，而不是将其恢复为默认值。</td>
  </tr>
  <tr>
   <td><code>messageBox</code></td>
   <td>在屏幕上显示一个对话框。 它仅对客户端应用程序可用</td>
   <td>类型为“是／否”的消息框将转换为“确定／取消”。 不支持包含三个按钮的消息框。</td>
  </tr>
  <tr>
   <td>currentPage</td>
   <td><p>在运行时设置文档的当前活动页面。</p> <p>页面值基于0，因此文档的第一页返回值0。</p> <p>当layout:ready在客户端上执行时，currentPage属性可用。 但是，当layout:ready在服务器上执行时，它不可用，因为直到表单布局执行之前，该属性才会执行。</p> </td>
   <td>无</td>
  </tr>
 </tbody>
</table>

### 字段{#field}

<table>
 <tbody>
  <tr>
   <th><strong><span>属性</span></strong></th>
   <th><strong><span>描述<br /> </span></strong></th>
   <th><strong><span>例外</span></strong></th>
  </tr>
  <tr>
   <td><code>presence</code></td>
   <td>控制关联对象在不同处理阶段的参与情况。 如果对象是容器，则容器的内容将继承此控件应用的任何限制。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>access</code></td>
   <td>控制用户对内容的访问。</td>
   <td>不适用于排除组。 此外，HTML5表单对非交互式和受保护的对象也给予相同的处理。<br /> </td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>用于在脚本表达式中标识此元素的标识符。</td>
   <td>HTML5表单不允许为对象设置name属性。 它是HTML5表单的只读属性。</td>
  </tr>
  <tr>
   <td><code>value</code></td>
   <td>包含单个数据内容的内容元素。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>rawValue</code></td>
   <td>指定此字段的无格式值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>formattedValue</code></td>
   <td>指定此字段的格式化值。</td>
   <td>不支 <code>formattedValue</code> 持通过脚本设置。</td>
  </tr>
  <tr>
   <td><code>editValue</code></td>
   <td>指定此字段的编辑值。</td>
   <td>不支 <code>editValue </code>持通过脚本设置。</td>
  </tr>
  <tr>
   <td><code>formatMessage</code></td>
   <td>指定此字段的格式验证消息字符串。</td>
   <td>不支 <code>formatMessage </code>持通过脚本设置。</td>
  </tr>
  <tr>
   <td><code>fillcolor</code></td>
   <td>指定此字段的背景颜色值。 您需要将border.fill.presence属性设置为单独可见。</td>
   <td>它无法正确返回字段的默认颜色。</td>
  </tr>
  <tr>
   <td><code>border</code></td>
   <td>边框对象描述对象周围的边框。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>ui</code></td>
   <td>ui对象包含表单对象的用户界面描述。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>mandatory</code></td>
   <td>指定字段的nullTest值。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>borderColor</code></td>
   <td>指定此字段的边框颜色值。 您需要将border.edge.presence属性设置为单独可见。</td>
   <td>它无法正确返回字段的默认边框颜色。</td>
  </tr>
  <tr>
   <td><code>length</code></td>
   <td>列表中的项目数。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>addItem</code></td>
   <td>将新项目添加到当前字段。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>clearItem</code></td>
   <td>从字段中删除所有项目。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>boundItem</code></td>
   <td>获取下拉列表或列表框的特定显示项的绑定值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>execCalculate</code></td>
   <td>执行字段的计算脚本。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>execValidate</code></td>
   <td>执行字段的验证脚本。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>execEvent</code></td>
   <td>执行对象的事件脚本。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>getItemState</code></td>
   <td>返回指定项的选择状态</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>setItemState</code></td>
   <td>设置指定项目的选择状态。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>getDisplayItem</code></td>
   <td>检索指定项目索引的项目显示文本。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>getSaveItem</code></td>
   <td>检索指定项索引的数据值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>deleteItem</code></td>
   <td>删除指定索引处的项目。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>setItems</code></td>
   <td>在当前字段中设置指定的项目。 它替换了预先存在的项目。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>h</td>
   <td>布局的高度度量。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>w</td>
   <td>指定布局宽度的度量。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>x</td>
   <td>使用定位布局放置时，指定容器锚点相对于父容器的左上角的x坐标。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>y</td>
   <td>使用定位布局放置时，指定容器锚点相对于父容器的左上角的y坐标。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>题注对象描述与表单设计对象关联的描述性标签。<br /> </td>
   <td>无</td>
  </tr>
  <tr>
   <td>验证</td>
   <td>验证对象控制表单上用户提供的数据的验证。 在表单生命周期中，验证对象可以多次激活。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>parentSubform</td>
   <td>指定此字段的父子表单（页）。</td>
   <td>始终返回父子表单，而不是返回第一个非范围覆盖的父子表单。<br /> </td>
  </tr>
  <tr>
   <td>selectedIndex</td>
   <td>第一个选定项的索引。</td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## 表单 {#form}

| **属性** | **描述** | **例外** |
|---|---|---|
| formNodes | 返回绑定到指定数据对象的所有表单模型对象的列表。 |  |

## InstanceManager {#instancemanager}

| 属性 | 描述 |
|---|---|
| `name` | 用于在脚本表达式中标识此元素的标识符。 |
| `occur` | 描述对其封闭容器允许的实例数的限制。 |
| `min` | 指定可实例化的最小实例数。 |
| `max` | 指定可实例化的实例的最大数量。 |
| `count` | 指定实例化的实例的当前数量。 |
| `setInstances` | 从此节点添加或删除指定的子表单或子表单集。 |
| `addInstance` | 将子表单或子表单集的新实例添加到此节点。 |
| `removeInstance` | 从此节点中删除子表单或子表单集。 |
| `moveInstance` | 将表单模型对象的子对象移动到表单模型内的其他指定位置。 对象的相应数据模型信息也被重新定位在数据模型内。 |
| `insertInstance` | 将子表单或子表单集的新实例插入此节点。 |

## list {#list}

| 属性 | 描述 |
|---|---|
| `length` | 列表中的元素数。 |
| `item` | 集合中从零开始的索引。 |
| `append` | 在节点列表的末尾附加一个节点。 |
| `remove` | 从节点列表中删除节点。 |
| `insert` | 在节点列表中特定节点之前插入节点。 |

## 节点 {#node}

| 属性 | 描述 | 例外 |
|---|---|---|
| createNode | 根据有效的类名创建新节点。 | 无 |
| `isContainer` | 指定此对象是否为容器对象。 | 无 |
| `isNull` | 指示当前数据值是否为空值。 | 无 |
| `resolveNode` | 从当前XML表单对象模型对象开始计算指定的SOM表达式，并返回在SOM表达式中指定的对象的值。 | 无 |
| `resolveNodes` | 从当前XML表单对象模型对象开始计算指定的SOM表达式，并返回在SOM表达式中指定的对象的值。 | 无 |
| oneOfChild | 根据有效的类名创建新节点。 | 无 |
| getElement | 返回指定的子对象。 | 无 |
| getAttribute | 获取指定的属性值。 | 无 |
| setAttribute | 设置指定属性的值。 | 无 |

## model {#model}

| 属性 | 描述 | 例外 |
|---|---|---|
| NA | NA | NA |

## 子表单 {#subform}

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
   <th>例外</th>
  </tr>
  <tr>
   <td>instanceIndex</td>
   <td>指定对象的索引，相对于其他实例化的实例。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>execEvent</td>
   <td>执行对象的事件脚本。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>getInvalidObjects</td>
   <td>返回子表单（包含）中包含的未通过验证测试的节点列表。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>边框</td>
   <td>边框对象描述对象周围的边框。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>指定此字段的边框颜色值。 您需要将border.edge.presence属性设置为单独可见。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>h</td>
   <td>布局的高度度量。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>w</td>
   <td>指定布局宽度的度量。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>x</td>
   <td>使用定位布局放置时，指定容器锚点相对于父容器的左上角的x坐标。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>y</td>
   <td>使用定位布局放置时，指定容器锚点相对于父容器的左上角的y坐标。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>验证</td>
   <td>验证对象控制表单上用户提供的数据的验证。 在表单生命周期中，验证对象可以多次激活。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>名称</td>
   <td>用于在脚本表达式中标识此元素的标识符。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>存在</td>
   <td>指定对象的可见性。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>访问</td>
   <td>控制用户对容器对象（如子表单）内容的访问。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>execValidate</td>
   <td>根据子表单或子表单集相对于同一表单对象的其他实例的位置计算其索引。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>instanceManager</td>
   <td>instanceManager对象管理表单模型对象的实例创建、删除和移动。<br /> </td>
   <td>无</td>
  </tr>
 </tbody>
</table>

### 提交 {#submit}

| 属性 | 描述 |
|---|---|
| 目标 | 向其提交数据的URL。 忽略此属性意味着XFA处理应用程序使用产品特定技术（如访问配置对象中的产品特定信息）获取URI。 |

## 树 {#tree}

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
   <th>例外</th>
  </tr>
  <tr>
   <td>节点</td>
   <td>返回当前对象的所有子对象的列表。</td>
   <td>
    <ul>
     <li>xfa.nodes、desc不支持</li>
     <li>为PDF和HTML报告的节点数不同。 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>名称</td>
   <td>指定此节点的名称。</td>
   <td>HTML中不允许使用脚本设置名称。</td>
  </tr>
  <tr>
   <td>parent</td>
   <td>获取此节点的父项。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>索引</td>
   <td>返回此节点在其类似名称、范围内类似子关系节点集合中的位置。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>somExpression</td>
   <td>获取此节点的SOM表达式。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>resolveNode</td>
   <td>从当前XML表单对象模型对象开始计算指定的SOM表达式，并返回在SOM表达式中指定的对象的值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>resolveNodes</td>
   <td>从当前XML表单对象模型对象开始计算指定的SOM表达式，并返回在SOM表达式中指定的对象的值。</td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## 子格式集 {#subformset}

| 属性 | 描述 | 例外 |
|---|---|---|
| instanceManager | instanceManager对象管理表单模型对象的实例创建、删除和移动。 | 无 |

## content {#content}

| **属性** | **描述** | **例外** |
|---|---|---|
| isNull | 指示当前数据值是否为null值。 |  |

## dataValue {#datavalue}

| **属性** | **描述** | **例外** |
|---|---|---|
| isNull | 指示当前数据值是否为null值。 |  |

## 边缘 {#edge}

<table>
 <tbody>
  <tr>
   <td><strong>属性 </strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>color属性描述图案对象的唯一颜色。</td>
   <td>
    <ul>
     <li>无法检索默认值。 </li>
     <li>这些更改反映在“模型”中，可用于脚本编写，但不会同步到HTML元素。 因此，更改不会反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 填充 {#fill}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>颜色属性定义了唯一的填充颜色。</td>
   <td>
    <ul>
     <li>无法检索默认值。 </li>
     <li>这些更改反映在“模型”中，可用于脚本编写，但不会同步到HTML元素。 因此，更改不会反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## linear {#linear}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>颜色属性描述表单上线性渐变填充的唯一颜色。</td>
   <td>
    <ul>
     <li>无法检索默认值。 </li>
     <li>这些更改反映在“模型”中，可用于脚本编写，但不会同步到HTML元素。 因此，更改不会反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 折线图 {#line}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>边缘</td>
   <td>边对象描述弧线、线或边框或矩形的一侧。<br /> </td>
   <td>不支持颜色、上限等属性。<br /> </td>
  </tr>
 </tbody>
</table>

## 图案 {#pattern}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>color属性描述图案对象的唯一颜色。 </td>
   <td>
    <ul>
     <li>无法检索默认值。 </li>
     <li>这些更改反映在“模型”中，可用于脚本编写，但不会同步到HTML元素。 因此，更改不会反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## radial {#radial}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>颜色属性描述径向对象的唯一颜色</td>
   <td>
    <ul>
     <li>无法检索默认值。 </li>
     <li>这些更改反映在“模型”中，可用于脚本编写，但不会同步到HTML元素。 因此，更改不会反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 点 {#stipple}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>color属性描述点状对象的唯一颜色。</td>
   <td>
    <ul>
     <li>无法检索默认值。 </li>
     <li>这些更改反映在模型中，可用于脚本编写，但不会同步到HTML元素。 因此，更改不会反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## draw {#draw}

<table>
 <tbody>
  <tr>
   <td>属性</td>
   <td>描述</td>
   <td>例外</td>
  </tr>
  <tr>
   <td>ui</td>
   <td>ui对象包含表单对象的用户界面描述。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>caption</td>
   <td>题注对象描述与表单设计对象关联的描述性标签。</td>
   <td> </td>
  </tr>
  <tr>
   <td>存在</td>
   <td>指定对象的可见性。</td>
   <td> </td>
  </tr>
  <tr>
   <td>名称</td>
   <td>指定可用于在脚本表达式中指定此对象或事件的标识符。</td>
   <td>不支持在运行时设置值</td>
  </tr>
  <tr>
   <td>value</td>
   <td>值对象包含单个数据内容单位。<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 角 {#corner}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>color属性描述角对象的唯一颜色。</td>
   <td>
    <ul>
     <li>无法检索默认值。 </li>
     <li>这些更改反映在模型中，可用于脚本编写，但不会同步到HTML元素。 因此，更改不会反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## checkButton {#checkbutton}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>边框</td>
   <td>边框对象描述checkButton对象周围的边框。 </td>
   <td>这些更改反映在模型中，可用于脚本编写，但不会同步到HTML元素。 因此，更改不会反映在UI中。<br /> </td>
  </tr>
 </tbody>
</table>

## choiceList {#choicelist}

<table>
 <tbody>
  <tr>
   <td><strong>属性<br /> </strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>边框</td>
   <td>边框对象描述choiceList对象周围的边框。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## dateTimeEdit {#datetimeedit}

| **属性** | **描述** | **例外** |
|---|---|---|
| 边框 | 边框对象描述围绕dateTimeEdit对象的边框。 |  |

## 图像 {#image}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>contentType</td>
   <td>指定引用文档中的内容类型，以MIME类型表示。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>名称<br /> </td>
   <td>用于在脚本表达式中标识此元素的标识符。</td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## imageEdit {#imageedit}

| **属性** | **描述** | **例外** |
|---|---|---|
| 边框 | 边框对象描述imageEdit对象周围的边框。 |  |

## numericEdit {#numericedit}

| **属性** | **描述** | **例外** |
|---|---|---|
| 边框 | 边框对象描述对象周围的边框。 | 无 |

## 对象{#object}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>className</td>
   <td>确定此对象的类的名称。<br /> </td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## rectangle {#rectangle}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>边缘</td>
   <td>边对象描述弧线、线或边框或矩形的一侧。<br /> </td>
   <td>不支持颜色、上限等属性。</td>
  </tr>
 </tbody>
</table>

## textEdit {#textedit}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>边框</td>
   <td>边框对象描述对象周围的边框。<br /> </td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## exclGroup {#exclgroup}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>布局</td>
   <td>指定此对象要使用的布局策略。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>边框</td>
   <td>指定此字段周围的边框。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>mandatory</td>
   <td>指定字段的nullTest值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>指定此字段的边框颜色值。必须先定义边框，然后才能通过脚本更改颜色。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>borderWidth</td>
   <td>指定此字段的边框宽度。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>h</td>
   <td>布局的高度度量。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>瞬态</td>
   <td>指定处理应用程序是否必须将排除组的值保存为表单提交或保存操作的一部分。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>w</td>
   <td>指定布局宽度的度量。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>x</td>
   <td>使用定位布局放置时，指定容器锚点相对于父容器的左上角的x坐标。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>y</td>
   <td>使用定位布局放置时，指定容器锚点相对于父容器的左上角的y坐标。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>题注对象描述与表单设计对象关联的描述性标签。<br /> </td>
   <td>无</td>
  </tr>
  <tr>
   <td>验证</td>
   <td>验证对象控制表单上用户提供的数据的验证。 在表单生命周期中，验证对象可以多次激活。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>dataNode</td>
   <td>获取合并后表单节点绑定到的数据节点。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>存在</td>
   <td>指定对象的可见性。</td>
   <td> </td>
  </tr>
  <tr>
   <td>访问</td>
   <td>控制用户对容器对象（如子表单）内容的访问。</td>
   <td>对于exclgrp中的单个项目，它始终返回打开状态。 </td>
  </tr>
  <tr>
   <td>名称</td>
   <td>指定可用于在脚本表达式中指定此对象或事件的标识符。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>成员</td>
   <td>指定排除组的成员。 </td>
   <td>无</td>
  </tr>
  <tr>
   <td>selectedMember</td>
   <td>返回排除组的选定成员。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>execCalculate</td>
   <td>对指定对象和任何子对象的计算事件执行任何脚本。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>计算</td>
   <td>计算对象控制字段值的计算。<br /> </td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## 弧 {#arc}

<table>
 <tbody>
  <tr>
   <td><strong>属性<strong></strong></strong></td>
   <td><strong>描述<strong></strong></strong></td>
   <td><strong>例外<strong></strong></strong></td>
  </tr>
  <tr>
   <td>边缘</td>
   <td>边对象描述弧线、线或边框或矩形的一侧。<br /> </td>
   <td>不支持颜色、上限等属性。 </td>
  </tr>
 </tbody>
</table>

## border {#border}

<table>
 <tbody>
  <tr>
   <td><strong>属性<strong></strong></strong></td>
   <td><strong>描述<strong></strong></strong></td>
   <td><strong>例外<strong></strong></strong></td>
  </tr>
  <tr>
   <td>边缘</td>
   <td>边对象描述弧线、线或边框或矩形的一侧。<br /> </td>
   <td>不支持颜色、上限等属性。 </td>
  </tr>
 </tbody>
</table>

## $布局 {#layout}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>h</td>
   <td>确定给定表单设计对象的高度。<br /> </td>
   <td>
    <ul>
     <li>页面区域和内容区域不支持高度(h)属性。 </li>
     <li>不支持参数“从XFA-Form对象出现的第一个内容区域偏移”。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>w</td>
   <td>确定给定表单设计对象的宽度。</td>
   <td>
    <ul>
     <li>页面区域和内容区域不支持宽度(w)属性。 </li>
     <li>不支持参数“从XFA-Form对象出现的第一个内容区域偏移”。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>x</td>
   <td>确定给定表单设计对象相对于其父对象的x坐标。</td>
   <td>
    <ul>
     <li>页面区域和内容区域不支持x coordinate(x)属性。 </li>
     <li>不支持参数“从XFA-Form对象出现的第一个内容区域偏移”。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>y</td>
   <td>确定给定表单设计对象相对于其父对象的y坐标。</td>
   <td>
    <ul>
     <li>页面区域和内容区域不支持y坐标(y)属性。 </li>
     <li>不支持参数“从XFA-Form对象出现的第一个内容区域偏移”。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecount</td>
   <td>确定当前表单的页数。</td>
   <td>
    <ul>
     <li>layout.pageCount()方法为PDF和HTML表单返回不同的值。</li>
     <li>通过隐藏对象来减少页数时，abspagecount方法返回的值不正确。<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecontent</td>
   <td>从表单的指定页面检索表单设计对象的类型。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>absPageCount</td>
   <td>确定当前表单的页数。</td>
   <td>
    <ul>
     <li>layout.pageCount()方法为PDF和HTML表单返回不同的值。</li>
     <li>通过隐藏对象来减少页数时，abspagecount方法返回的值不正确。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 项目 {#items}

| **属性** | **描述** | **例外** |
|---|---|---|
| 存在 | 指定对象的可见性。 | 无 |

## FormCalc {#formcalc}

FormCalc是一种特定于XFA的语言，用于创建以电子表单为中心的逻辑和计算根。 FormCalculation提供一组功能强大的构建函数。

### FormCalc支持的函数 {#formcalc-supported-functions}

### FormCalc表达式支持 {#formcalc-expression-support}

<table>
 <tbody>
  <tr>
   <td><strong>类别 </strong></td>
   <td><strong>描述 </strong></td>
   <td><strong>样本 </strong></td>
  </tr>
  <tr>
   <td>简单表达</td>
   <td>加、减、乘、除和括号</td>
   <td>(a+b)*3</td>
  </tr>
  <tr>
   <td>变量声明</td>
   <td>定义变量</td>
   <td>var a<br /> var a=3<br /> a=3</td>
  </tr>
  <tr>
   <td>逻辑表达式</td>
   <td>
    <ul>
     <li>逻辑（和／或）</li>
     <li>比较（大于／小于／等于）</li>
    </ul> </td>
   <td>A或1<br /> 1 &lt;&gt;2<br /> A NE B<br /> a或1<br /> 1 &lt;&gt;2<br /> A NE B</td>
  </tr>
  <tr>
   <td>If表达式</td>
   <td><br type="_moz" /> </td>
   <td>if(a&gt;b)then 2 endif</td>
  </tr>
  <tr>
   <td>whilg</td>
   <td><br type="_moz" /> </td>
   <td>while(ilt 5)do i = i + 1 endwhile</td>
  </tr>
  <tr>
   <td>对象</td>
   <td><br type="_moz" /> </td>
   <td>对于i = 100，向下到1 <br /> do s = s + iendfor</td>
  </tr>
  <tr>
   <td>for each</td>
   <td><br type="_moz" /> </td>
   <td>对于(1, 2, 3)中的每个i, <br /> do s = s + iend for</td>
  </tr>
  <tr>
   <td>函数声明</td>
   <td>在FormCalc中定义自定义函数</td>
   <td>func foo(n)do var f = n endfunc</td>
  </tr>
 </tbody>
</table>

### Acrobat API支持 {#acrobat-api-support}

1. **算术函数**

   1. Abs()
   1. Avg()
   1. Ceil()
   1. 计数()
   1. Floor()
   1. 最大()
   1. 最小()
   1. Mod()
   1. Round()
   1. 总计()

1. **科学功能**

   1. Acos()
   1. Asin()
   1. Atan()
   1. Atan2()
   1. Cos()
   1. Sin()
   1. Tan()
   1. Exp()
   1. 日志()
   1. Pow()
   1. Sqrt()
   1. Deg2Rad()
   1. Rad2Deg()
   1. Pi()

1. **财务职能**

   1. 四月()
   1. Cterm()
   1. Fv()
   1. Ipmt()
   1. Npv()
   1. Pmt()
   1. Ppmt()
   1. Pv()
   1. Rate()
   1. Term()

1. **逻辑函数**

   1. Choose()
   1. If()
   1. Oneof()
   1. Within()

1. **字符串函数**

   1. 于()
   1. Concat()
   1. 左()
   1. Len()
   1. Lower()
   1. Ltrim()
   1. 替换()
   1. 右()
   1. Rtrim()
   1. 空间()
   1. Stuff()
   1. Substr()
   1. Upper()
   1. WordNum()

1. **日期和时间**

   1. 日期()
   1. num2date()
   1. DateFmt()

<table>
 <tbody>
  <tr>
   <td><strong>API</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>像差</strong></td>
  </tr>
  <tr>
   <td>console.println()</td>
   <td>此Acrobat API会将输出转储到javascript控制台。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.alert()</td>
   <td>此Acrobat API通过javascript弹出窗口发出警报消息。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.beep()</td>
   <td>使系统播放声音。</td>
   <td>不执行任何操作。</td>
  </tr>
  <tr>
   <td>app.execDialog()</td>
   <td>向用户显示模态对话框。 Modal对话框必须由用户关闭，才能直接再次使用主机应用程序。</td>
   <td>不执行任何操作。<br /> </td>
  </tr>
  <tr>
   <td>app.launchURL()</td>
   <td>在浏览器窗口中启动URL。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setInterval()</td>
   <td>指定JavaScript脚本和时间段。 每次经过该时段时，都会执行该脚本。 此方法的返回值必须保存在JavaScript变量中。 否则，间隔对象将受到垃圾收集的影响，这会导致时钟停止。 要终止定期执行，请将返回的间隔对象传递给clearInterval。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setTimeOut()</td>
   <td>指定JavaScript脚本和时间段。 该脚本仅在经过一段时间后执行一次。此方法的返回值必须保存在JavaScript变量中。 否则，超时对象将受垃圾收集的约束，这会导致时钟停止。 要取消超时事件，请将返回的超时对象传递给clearTimeOut。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.clearInterval()</td>
   <td>取消先前由setInterval方法设置的注册间隔。</td>
   <td>在HTML5表单中，API无法正确工作。</td>
  </tr>
  <tr>
   <td>app.clearTimeOut()</td>
   <td>取消之前注册的超时间隔。 这种间隔最初由setTimeOut设置。</td>
   <td>在HTML5表单中，API无法正确工作。<br /> </td>
  </tr>
  <tr>
   <td>app.eval()</td>
   <td>运行给定的脚本。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.activeDocs</td>
   <td>包含每个活动文档的Doc对象的数组。 如果没有活动的文档，activeDocs将不返回任何内容；即，它的行为与核心JavaScript中d = new Array(0)的行为相同。</td>
   <td>为HTMl5表单返回空数组。</td>
  </tr>
  <tr>
   <td>app.calculate</td>
   <td>如果为true（默认值），则可以执行计算。 如果为false，则不允许计算。</td>
   <td>对于HTMl5 Forms，始终为true。</td>
  </tr>
  <tr>
   <td>app.constants</td>
   <td>用于保持各种常数值的包装器对象。 当前，此属性返回一个具有单个属性align的对象。</td>
   <td>HTML5表单返回空对齐对象。</td>
  </tr>
  <tr>
   <td>app.focusRect</td>
   <td>打开和关闭焦点矩形。 焦点矩形是按钮、复选框、单选按钮和签名周围的淡淡虚线，用于指示表单域具有键盘焦点。 如果值为true，则会打开焦点矩形。</td>
   <td>对于HTML5表单始终如此。</td>
  </tr>
  <tr>
   <td>app.formsVersion</td>
   <td>查看器表单软件的版本号。 检查此属性以确定如果希望在脚本中保持向后兼容性，则软件较新版本中的对象、属性或方法是否可用。</td>
   <td>11.001总是。</td>
  </tr>
  <tr>
   <td>app.language</td>
   <td>运行的Acrobat查看器的语言。</td>
   <td>对于HTMl5表单，始终为“ENU”。</td>
  </tr>
 </tbody>
</table>

## 支持的XFA事件 {#supported-xfa-events}

支持以下客户端XFA事件：

* 初始化
* 验证
* 计算
* 单击
* Enter
* 退出
* 更改
* ValidationState

>[!NOTE]
>
>HTML5表单在客户端（浏览器）上呈现。 建议使用客户端验 **证****和计** 算脚本，而不是服务器端脚本。

**[联系支持](https://www.adobe.com/account/sign-in.supportportal.html)**
