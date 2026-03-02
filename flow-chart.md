# 流程图生成规范指南

## 一、基本要求

### 1.1 样式规范
- **背景色**：白色（white）
- **文字颜色**：黑色（black）
- **线条颜色**：黑色（#000000）
- **连接线**：必须是直线，不能弯曲
- **线之间**：不能交叉，必须清晰分离

### 1.2 图形元素标准

#### 开始/结束节点
- **形状**：圆角矩形（rounded=1, arcSize=50）
- **填充色**：白色或浅灰色（#f5f5f5）
- **边框**：黑色（#666666）
- **示例**：`style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#ffffff;strokeColor=#000000;fontColor=#000000;"`

#### 输入/输出节点（平行四边形）
- **形状**：平行四边形（shape=parallelogram）
- **填充色**：白色（#ffffff）
- **边框**：黑色（#000000）
- **示例**：`style="shape=parallelogram;perimeter=parallelogramPerimeter;whiteSpace=wrap;html=1;fixedSize=1;fillColor=#ffffff;strokeColor=#000000;fontColor=#000000;"`

#### 处理节点（矩形）
- **形状**：矩形（rounded=0）
- **填充色**：白色（#ffffff）
- **边框**：黑色（#000000）
- **示例**：`style="rounded=0;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#000000;fontColor=#000000;"`

#### 判断节点（菱形）
- **形状**：菱形（rhombus）
- **填充色**：白色（#ffffff）
- **边框**：黑色（#000000）
- **示例**：`style="rhombus;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#000000;fontColor=#000000;"`

## 二、Draw.io XML 结构规范

### 2.1 文件头部格式
```xml
<mxfile host="app.diagrams.net" modified="2026-03-02T10:00:00.000Z" agent="Mozilla/5.0" version="21.0.0" etag="flowchart_name" type="device">
  <diagram name="流程图名称" id="flowchart_id">
    <mxGraphModel dx="800" dy="600" grid="0" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="800" pageHeight="1200" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <!-- 节点和连接线在这里 -->
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### 2.2 节点定义格式
```xml
<mxCell id="node_id" value="节点文本" style="样式定义" vertex="1" parent="1">
  <mxGeometry x="水平位置" y="垂直位置" width="宽度" height="高度" as="geometry" />
</mxCell>
```

### 2.3 连接线定义格式
```xml
<mxCell id="edge_id" value="标签文字（如是/否）" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;strokeColor=#000000;fontColor=#000000;" edge="1" parent="1" source="源节点id" target="目标节点id">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

## 三、布局设计原则

### 3.1 垂直流向布局
- 主流程从上到下垂直排列
- 每个节点垂直间距建议 40-60 像素
- 同一列的节点水平对齐

### 3.2 水平分支布局
- 判断节点的分支向左右两侧展开
- "是"分支通常向下继续
- "否"分支通常向右然后向上循环或向下结束

### 3.3 避免线条交叉的技巧
1. **使用正交路由**：`edgeStyle=orthogonalEdgeStyle`
2. **合理设置转折点**：使用 `<Array as="points">` 定义中间点
3. **分层布局**：不同层次的节点放在不同水平线上
4. **循环回流**：从右侧绕回顶部，保持线条整齐

## 四、连接线关键点

### 4.1 出口点设置（exitX, exitY）
- 上：`exitX=0.5, exitY=0`
- 下：`exitX=0.5, exitY=1`
- 左：`exitX=0, exitY=0.5`
- 右：`exitX=1, exitY=0.5`

### 4.2 入口点设置（entryX, entryY）
- 上：`entryX=0.5, entryY=0`
- 下：`entryX=0.5, entryY=1`
- 左：`entryX=0, entryY=0.5`
- 右：`entryX=1, entryY=0.5`

### 4.3 中间点定义（用于复杂路径）
```xml
<mxGeometry relative="1" as="geometry">
  <Array as="points">
    <mxPoint x="640" y="290" />
    <mxPoint x="640" y="100" />
  </Array>
</mxGeometry>
```

## 五、中文显示优化

### 5.1 字体设置
- 使用 `whiteSpace=wrap;html=1` 支持自动换行
- 对于长文本，适当增加节点宽度
- 使用 `<br>` 标签手动换行

### 5.2 文本对齐
- 默认居中对齐即可满足大部分需求
- 如需调整，可使用 `align=center;verticalAlign=middle;`

## 六、完整示例代码

以下是一个标准的登录流程图 XML 示例：

```xml
<mxfile host="app.diagrams.net" modified="2026-03-02T10:00:00.000Z" agent="Mozilla/5.0" version="21.0.0" etag="admin_login" type="device">
  <diagram name="管理员登录流程图" id="admin_login_flow">
    <mxGraphModel dx="800" dy="600" grid="0" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="800" pageHeight="1200" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        
        <!-- 开始节点 -->
        <mxCell id="start" value="开始" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#ffffff;strokeColor=#000000;fontColor=#000000;" vertex="1" parent="1">
          <mxGeometry x="340" y="20" width="120" height="40" as="geometry" />
        </mxCell>
        
        <!-- 输入节点（平行四边形） -->
        <mxCell id="input_account" value="输入账号" style="shape=parallelogram;perimeter=parallelogramPerimeter;whiteSpace=wrap;html=1;fixedSize=1;fillColor=#ffffff;strokeColor=#000000;fontColor=#000000;" vertex="1" parent="1">
          <mxGeometry x="340" y="80" width="120" height="40" as="geometry" />
        </mxCell>
        
        <!-- 判断节点（菱形） -->
        <mxCell id="check_captcha" value="判断验证码<br>是否正确" style="rhombus;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#000000;fontColor=#000000;" vertex="1" parent="1">
          <mxGeometry x="340" y="260" width="120" height="60" as="geometry" />
        </mxCell>
        
        <!-- 处理节点（矩形） -->
        <mxCell id="error_captcha" value="显示验证码错误" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#000000;fontColor=#000000;" vertex="1" parent="1">
          <mxGeometry x="520" y="270" width="120" height="40" as="geometry" />
        </mxCell>
        
        <!-- 结束节点 -->
        <mxCell id="end" value="结束" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#ffffff;strokeColor=#000000;fontColor=#000000;" vertex="1" parent="1">
          <mxGeometry x="340" y="840" width="120" height="40" as="geometry" />
        </mxCell>
        
        <!-- 连接线 - 垂直 -->
        <mxCell id="e1" value="" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;strokeColor=#000000;fontColor=#000000;" edge="1" parent="1" source="start" target="input_account">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        
        <!-- 连接线 - 带标签的水平分支 -->
        <mxCell id="e5" value="否" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;strokeColor=#000000;fontColor=#000000;labelBackgroundColor=#ffffff;" edge="1" parent="1" source="check_captcha" target="error_captcha">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        
        <!-- 连接线 - 带转折的循环回流 -->
        <mxCell id="e7" value="" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=1;entryY=0.5;entryDx=0;entryDy=0;strokeColor=#000000;fontColor=#000000;" edge="1" parent="1" source="error_captcha" target="input_account">
          <mxGeometry relative="1" as="geometry">
            <Array as="points">
              <mxPoint x="640" y="290" />
              <mxPoint x="640" y="100" />
            </Array>
          </mxGeometry>
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

## 七、常见问题解决方案

### 7.1 线条交叉问题
- 使用 `edgeStyle=orthogonalEdgeStyle` 启用正交路由
- 通过 `<Array as="points">` 添加中间转折点
- 将返回线放在最右侧，远离主流程线

### 7.2 中文乱码问题
- 确保 XML 文件使用 UTF-8 编码
- 特殊字符使用 HTML 实体编码（如 `<br>` 表示换行）

### 7.3 标签位置问题（重要）
- **标签必须独立**："是"/"否" 等判断标签必须使用**独立的文本节点**，不能作为连接线的value属性
- **标签位置**：标签必须放在连接线**旁边的空白处**，不能嵌入线内或在线的上方
- **关键原则**：标签与连接线之间必须有明显间隙，确保标签完全独立于线条

#### 标签位置的详细规则：

**1. 水平连接线（左右方向）的标签位置：**
- "否"标签：放在连接线**上方**的空白处，与线保持10-15像素距离
- "是"标签（向下分支）：放在连接线**左侧**的空白处，靠近菱形节点
- 坐标计算：如果连接线从 (x1, y) 到 (x2, y)，则标签放在 (x1+x2)/2, y-15

**2. 垂直连接线（上下方向）的标签位置：**
- "是"/"否"标签：放在连接线**右侧**的空白处，与线保持10-15像素距离
- 坐标计算：如果连接线从 (x, y1) 到 (x, y2)，则标签放在 x+15, (y1+y2)/2

**3. 标签与连接线的关系：**
- 连接线：`value=""`（必须为空，不能有标签文字）
- 标签节点：独立的 `mxCell`，类型为文本节点
- 两者在XML中是平级关系，不是父子关系

#### 正确示例（水平连接线+上方标签）：
```xml
<!-- 连接线（无标签，纯直线） -->
<mxCell id="edge_no" value="" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;strokeColor=#000000;" edge="1" parent="1" source="check_node" target="error_node">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- "否"标签：放在连接线上方空白处 -->
<mxCell id="label_no" value="否" style="text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;fontColor=#000000;" vertex="1" parent="1">
  <mxGeometry x="465" y="265" width="30" height="20" as="geometry" />
</mxCell>
```

#### 正确示例（垂直连接线+右侧标签）：
```xml
<!-- 连接线（无标签，纯直线） -->
<mxCell id="edge_yes" value="" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;strokeColor=#000000;" edge="1" parent="1" source="check_node" target="next_node">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- "是"标签：放在连接线右侧空白处 -->
<mxCell id="label_yes" value="是" style="text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;fontColor=#000000;" vertex="1" parent="1">
  <mxGeometry x="400" y="320" width="30" height="20" as="geometry" />
</mxCell>
```

#### 常见错误（必须避免）：
❌ **错误1**：将标签作为连接线的value属性
```xml
<!-- 错误！标签会嵌入线内 -->
<mxCell id="edge_wrong" value="否" style="..." edge="1" ...>
```

❌ **错误2**：标签位置与连接线重叠
```xml
<!-- 错误！标签y坐标与连接线相同 -->
<mxCell id="label_wrong" value="否" ...>
  <mxGeometry x="470" y="290" ... />  <!-- y=290与线重合 -->
</mxCell>
```

✅ **正确做法**：
- 连接线：`value=""`（空）
- 标签节点：独立节点，位置偏移（水平线上方/垂直线右侧）

## 八、调用 Draw.io MCP 工具

使用 `c2_r7R0mcp0open_drawio_xml` 工具打开流程图：

```python
c2_r7R0mcp0open_drawio_xml(
    content="完整的XML字符串",
    task_progress="任务进度列表"
)
```

生成的流程图将在浏览器中打开，可以进一步编辑和导出为 PNG/SVG/PDF 格式。

## 九、检查清单

在生成流程图前，请确认：
- [ ] 所有节点使用白底黑字
- [ ] 所有连接线都是直线（orthogonalEdgeStyle）
- [ ] 线之间没有交叉
- [ ] 使用了正确的中文文本
- [ ] 判断节点的分支标签（是/否）清晰可见
- [ ] 整体布局整洁美观
