<<<<<<< HEAD
# Matplotlib学习笔记

### 1.图例legend

### 2.画图

### 3.设置刻度

### 4.创建画布

### 5.打网格

### 6.样式美化

plt.style.use定制画布风格

```python
print(plt.style.available) # 打印样式列表
['Solarize_Light2',
 '_classic_test_patch',
 'bmh',
 'classic',
 'dark_background',
 'fast',
 'fivethirtyeight',
 'ggplot',
 'grayscale',
 'seaborn',
 'seaborn-bright',
 'seaborn-colorblind',
 'seaborn-dark',
 'seaborn-dark-palette',
 'seaborn-darkgrid',
 'seaborn-deep',
 'seaborn-muted',
 'seaborn-notebook',
 'seaborn-paper',
 'seaborn-pastel',
 'seaborn-poster',
 'seaborn-talk',
 'seaborn-ticks',
 'seaborn-white',
 'seaborn-whitegrid',
 'tableau-colorblind10']
```

- 默认风格：

![](https://i.loli.net/2021/05/16/KNV3kECl18Dfp6J.png)

- plt.style.use('bmh')

![](https://i.loli.net/2021/05/16/OLirs2TJ84zCBbG.png)

- plt.style.use('classic')
  ![](https://i.loli.net/2021/05/16/ykZMDcfWgAH9hJj.png)

- plt.style.use('dark_background')
  ![](https://i.loli.net/2021/05/16/Rc584KPvuQrVpeh.png)

- plt.style.use('fast')
  ![](https://i.loli.net/2021/05/16/Rc584KPvuQrVpeh.png)
- plt.style.use('fivethirtyeight')
  ![](https://i.loli.net/2021/05/16/8HR2E5lB3m6qgGQ.png)

- plt.style.use('ggplot')
  ![](https://i.loli.net/2021/05/16/dvqnFSEyIAbQ5o8.png)

- plt.style.use('grayscale')
  ![](https://i.loli.net/2021/05/16/BE8GL7DFgmxd2fb.png)

- plt.style.use('seaborn-bright')
  ![](https://i.loli.net/2021/05/16/UsRfjHXi9NtZVk4.png)

- plt.style.use('seaborn-colorblind')
  ![](https://i.loli.net/2021/05/16/NdpEHxYAD9WqV2v.png)

- plt.style.use('tableau-colorblind10')

![](https://i.loli.net/2021/05/16/ACv16Wp7e283QXZ.png)



# Jupyter notebook作图

1画图嵌入notebook的方式

%matplotlib inline 标准

%matplotlib notebook 可能会比较卡

mpld3 通过matplotlib代码的替代性呈现（通过d3），虽然不完整，但很好

bokeh 生产可交互图像的更好选择

plot.ly 可以生成非常好的图，貌似付费



# widgets

## 1.ToolHandles

对象：matplotlib.widgets.ToolHandles(ax, x, y, marker='o', marker_props=None, useblit=True)

参数：

- ax：[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)对象
- x，y：一维数组，控制handles的坐标
- marker：字符，显示句柄的标记形状，具体可见[matplotlib.pyplot.plot](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.plot.html#matplotlib.pyplot.plot)
- marker_props：字典，附加的标记属性，具体可见[matplotlib.lines.Line2D](https://matplotlib.org/stable/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D)

方法/属性：

- closest(x, y)：返回索引和到最近索引的像素距离
- set_animated(val)：
- set_data(pts, y=None)：设置句柄x和y的距离
- set_visible(val)：
- x
- y

## 2.SpanSelector

对象：`matplotlib.widgets.SpanSelector(ax, onselect, direction, minspan=None, useblit=False,  rectprops=None, onmove_callback=None, span_stays=False, button=None)`

基类：`matplotlib.widgets._SelectorWidget`

在单个轴上可视化地选择一个范围，然后用这些值调用函数（onselect）。为了保证选择器保持响应，要保留对它的引用，意思就是在构造SpanSelector的时候要把返回值赋值，也就是像`span = SpanSelector(ax,...)`这样。

要关闭 SpanSelector，把span_selector.active 设置为 False。

参数：

- ax：[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)对象
- onselect：func(min, max)，min、max是浮点数
- direction：{"horizontal", "vertical"}，选择器的方向
- minspan：浮点数，默认None，如果小于minspan值则不会调用onselect
- useblit：布尔型，默认False，如果为 True，则使用后端相关的blitting功能来加快画布更新
- rectprops：字典，默认None，[matplotlib.patches.Patch](https://matplotlib.org/stable/api/_as_gen/matplotlib.patches.Patch.html#matplotlib.patches.Patch)的属性字典
- onmove_callback：func(min, max)，min、max是浮点数，默认None，在选择范围内时调用鼠标移动
- span_stays：布尔型，默认False，如果是True，在释放鼠标后SpanSelector保持可见
- button：[MouseButton](https://matplotlib.org/stable/api/backend_bases_api.html#matplotlib.backend_bases.MouseButton)或是[MouseButton](https://matplotlib.org/stable/api/backend_bases_api.html#matplotlib.backend_bases.MouseButton)列表，激活选择器的鼠标按钮

方法：

- ignore(event)：返回是否忽略某个事件。它应该在任何事件回调开始时调用。
- new_axes(ax)：设置SpanSelector在新轴上操作

rectprops的属性可以设置的地方有很多，可以点击链接了解更多，常用的属性是好理解的。

而button的设置暂时还不怎么懂。

## 3.PolygonSelector

对象：`matplotlib.widgets.PolygonSelector(ax, onselect, useblit=False, lineprops=None, markerprops=None, vertex_select_radius=15)`

基类：`matplotlib.widgets._SelectorWidget`

在坐标轴中选择一个多边形区域。

每次单击鼠标放置顶点，并通过完成多边形（单击第一个顶点）来进行选择。 按住Ctrl键并单击并拖动顶点以重新定位它（如果多边形已经完成，则不需要Ctrl键）。按住Shift键并单击并拖动轴中的任意位置以移动所有顶点。 按Esc键开始一个新的多边形。要让选择器保持响应，必须保留对它的引用。

参数：

- ax：[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)对象
- onselect：函数对象，当一个多边形完成或在完成后修改时，调用onselect函数并将顶点列表作为 (xdata, ydata) 元组传递。
- useblit：布尔型，默认False
- lineprops：字典类型，默认为`dict(color='k', linestyle='-', linewidth=2, alpha=0.5)`，表示多边形边缘的线条属性
- markerprops：字典类型，默认为`dict(marker='o', markersize=7, mec='k', mfc='k', alpha=0.5)`，表示多边形定点的标记属性
- vertex_select_radius：浮点数，默认15px，如果鼠标单击在顶点的vertex_select_radius像素内，则选择顶点（以完成多边形或移动顶点）

方法：

- onmove(event)：光标移动的事件处理程序和验证程序

属性：

- verts：多边形顶点，是 (x, y) 点对的列表。

## 4.LockDraw

对象：`matplotlib.widgets.LockDraw`

一些小部件，例如光标，会在画布上绘制，这在所有情况下都是不可取的，例如当工具栏处于缩放至矩形模式并绘制矩形的时候。 为了避免这种情况，在画布上绘制之前，小部件可以使用`canvas.widgetlock(widget)`获取画布的锁；这样能阻止其他小部件同时这样做（如果它们也尝试先获取锁）。

方法：

- available(o)：返回o是否可绘图
- isowner(o)：返回o是否拥有这个锁
- locked()：返回锁当前是否由所有者持有
- release(o)：从o中释放锁

## 5.LassoSelector

对象：`matplotlib.widgets.LassoSelector(ax, onselect=None, useblit=True,lineprops=None, button=None)`

基类：`matplotlib.widgets._SelectorWidget`

可以任意形状的选择曲线，全凭鼠标选择。类似于之前其他的选择器，需要保留引用。所选路径可与contains_point结合使用以从图像中选择数据点

参数：

- ax：[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)对象
- onselect：函数对象，每当套索被释放时，onselect 函数就会被调用并传递所选路径的顶点。
- useblit：布尔型，默认False
- lineprops：字典类型，默认None
- button：用于矩形选择的鼠标按钮。 默认为无，对应所有按钮。

方法：

- onpress(event)
- onrelease(event)

## 6.RectangleSelector

对象：`matplotlib.widgets.RectangleSelector(ax, onselect, drawtype='box', minspanx=0, minspany=0,useblit=False, lineprops=None, rectprops=None, spancoords='data', button=None, maxdist=10, marker_props=None, interactive=False, state_modifier_keys=None)`

基类：`matplotlib.widgets._SelectorWidget`

选择坐标区的一个矩形区域。要保持光标的响应，必须保留对它的引用。

参数：

- ax：[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)对象
- onselect：函数对象，选择完成后的回调函数，它像这样：`def onselect(eclick: MouseEvent, erelease: MouseEvent)`。其中 eclick 和 erelease 是启动和完成选择的鼠标单击和释放鼠标事件
- drawtype：{"box", "line", "none"}，默认box。是否绘制完整的矩形框、矩形的对角线还是什么都不绘制
- minspanx：浮点型，默认为0，x 跨度上最小的选择，更小的会忽略
- minspany：浮点型，默认为0，y 跨度上最小的选择，更小的会忽略
- useblit：布尔值，默认False，是否使用blitting加速绘制
- lineprops：字典，可选，绘制线条的属性，如果drawtype=="line"，默认为`dict(color="blcak", linestyle="-", linewidth=2, alpha=0.5)`
- rectprops：字典，可选，绘制矩形的属性，如果drawtype=="box"，默认为`dict(facecolor="red", edgecolor="black", alpha=0.2, fill=True)`
- spancoords：{"data", "pixels"}，默认"data"，是否以数据或像素坐标解释minspanx和minspany。
- button：MouseButton，或其列表，触发矩形选择的按钮
- maxdist：浮点型，默认10，可以激活交互式工具句柄的距离（以像素为单位）
- marker_props：字典，用于绘制交互式手柄的属性。 当前未实施并被忽略
- interactive：布尔值，默认False，是否绘制一组句柄，允许在绘制后与小部件进行交互
- state_modifier_keys：字典，可选，影响小部件行为的键盘修饰符。 值修改默认值。
  - "move"：移动现有形状，默认：无修饰符
  - "clear"：清除当前形状，默认："escape"
  - "square"：使形状为方形，默认值："shift"
  - "center"：使初始点成为形状的中心，默认值："ctrl"

属性：

- center：矩形的中心
- corners：矩形的四个角，从左下角开始，顺时针移动
- edge_centers：矩形边缘的中点从左边开始，逆时针移动
- extents：返回(xmin, xmax, ymin, ymax)
- geometry：返回一个 形状为(2, 5) 数组，其中包含从左上角开始和结束的矩形四个角的 x (RectangleSelector.geometry[1, :]) 和 y (RectangleSelector.geometry[0, :]) 坐标。

方法：

- draw_shape(extents)

### EllipseSelector

对象：`matplotlib.widgets.EllipseSelector(ax, onselect, drawtype='box', minspanx=0, minspany=0, useblit=False, lineprops=None, rectprops=None, spancoords='data', button=None, maxdist=10, marker_props=None, interactive=False, state_modifier_keys=None)`

基类：`matplotlib.widgets.RectangleSelector`

选择轴的椭圆区域。要保持光标响应，必须保留对它的引用。

参数参考基类RectangleSelector



## 7.Widget

对象：`matplotlib.widgets.Widget`

基类：`object`

GUI元部件的抽象基类。

属性：

- active：是否这个部件激活
- drawon=True
- eventson=True

方法：

- get_active()：获取部件是否激活
- ignore(event)：返回是否应该忽略事件event。此方法应在任何事件回调开始时调用
- set_active(active)：设置部件是否处于激活状态

### AxesWidget

对象：`matplotlib.widgets.AxesWidget(ax)`

基类：`matplotlib.widgets.Widget`

将部件连接到轴Axes。为了保证部件保持响应性而不是垃圾收集，用户应该保持对对象的引用。

属性：

- ax：[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)对象
- canvas：[FigureCanvasBase](https://matplotlib.org/stable/api/backend_bases_api.html#matplotlib.backend_bases.FigureCanvasBase)，部件的父图形画布
- active：布尔值，是否部件是激活的

- cids：

方法：

- connect_event(event, callback)：将回调函数与事件event连接起来。这应该用来代替 figure.canvas.mpl_connect，因为这个函数存储回调 id 以便以后清理

- disconnect_events()：断开由此部件创建的所有事件连接。

#### Button

对象：`matplotlib.widgets.Button(ax, label, image=None, color='0.85', hovercolor='0.95')`

基类：`matplotlib.widgets.AxesWidget`

调用on_clicked连接按钮

属性：

- ax：按钮渲染的[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)对象
- label：一个[matplotlib.text.Text](https://matplotlib.org/stable/api/text_api.html#matplotlib.text.Text)实例
- color：未悬停时按钮的颜色
- hovercolor：悬停时按钮的颜色

参数：

- ax：按钮将被放入哪个[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)实例
- label：字符串，按钮的文本
- image：数组或PIL图像，要放置在按钮中的图像，如果不是None。参数直接转发给imshow
- color：按钮未激活的颜色
- hovercolor：鼠标悬停时按钮的颜色

cnt：

observers：

方法：

- disconnect(cid)：删除连接ID为cid的回调函数
- on_clicked(func)：将回调函数 func 连接到按钮单击事件。返回一个连接id，可用于断开回调。

#### CheckButtons

对象：`matplotlib.widgets.CheckButtons(ax, labels, actives=None)`

基类：`matplotlib.widgets.AxesWidget`

调用on_clicked连接按钮

属性：

- ax：按钮渲染的[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)对象
- labels：[matplotlib.text.Text](https://matplotlib.org/stable/api/text_api.html#matplotlib.text.Text)列表
- rectangles：[Rectangle](https://matplotlib.org/stable/api/_as_gen/matplotlib.patches.Rectangle.html#matplotlib.patches.Rectangle)列表
- lines：(Line2D, Line2D)点对，是复选框中 x 的列表。 每个框都存在这些行，但在未选中其框时具有 set_visible(False) 

参数：

- ax：复选按钮将被放入哪个[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)实例
- labels：字符串列表，复选按钮的文本
- actives：布尔值的列表，可选，复选按钮的初始状态，必须和labels长度一致。如果不提供则默认所有按钮未选

cnt：

observers：

方法：

- disconnect(cid)：删除连接ID为cid的回调函数
- on_clicked(func)：将回调函数 func 连接到按钮单击事件。返回一个连接id，可用于断开回调。

- get_status()：返回所有复选按钮的状态（真/假）的元组。
- set_active(index)：按索引切换（激活或停用）复选按钮。如果 eventson 为 True，则触发回调。index为要切换的复选按钮索引，index不合法会触发ValueError

#### Cursor

#### Lasso

#### RadioButtons

#### SliderBase

#### TextBox

### MultiCursor

### SubplotTool

=======
# Matplotlib学习笔记

### 1.图例legend

### 2.画图

### 3.设置刻度

### 4.创建画布

### 5.打网格

### 6.样式美化

plt.style.use定制画布风格

```python
print(plt.style.available) # 打印样式列表
['Solarize_Light2',
 '_classic_test_patch',
 'bmh',
 'classic',
 'dark_background',
 'fast',
 'fivethirtyeight',
 'ggplot',
 'grayscale',
 'seaborn',
 'seaborn-bright',
 'seaborn-colorblind',
 'seaborn-dark',
 'seaborn-dark-palette',
 'seaborn-darkgrid',
 'seaborn-deep',
 'seaborn-muted',
 'seaborn-notebook',
 'seaborn-paper',
 'seaborn-pastel',
 'seaborn-poster',
 'seaborn-talk',
 'seaborn-ticks',
 'seaborn-white',
 'seaborn-whitegrid',
 'tableau-colorblind10']
```

- 默认风格：

![](https://i.loli.net/2021/05/16/KNV3kECl18Dfp6J.png)

- plt.style.use('bmh')

![](https://i.loli.net/2021/05/16/OLirs2TJ84zCBbG.png)

- plt.style.use('classic')
  ![](https://i.loli.net/2021/05/16/ykZMDcfWgAH9hJj.png)

- plt.style.use('dark_background')
  ![](https://i.loli.net/2021/05/16/Rc584KPvuQrVpeh.png)

- plt.style.use('fast')
  ![](https://i.loli.net/2021/05/16/Rc584KPvuQrVpeh.png)
- plt.style.use('fivethirtyeight')
  ![](https://i.loli.net/2021/05/16/8HR2E5lB3m6qgGQ.png)

- plt.style.use('ggplot')
  ![](https://i.loli.net/2021/05/16/dvqnFSEyIAbQ5o8.png)

- plt.style.use('grayscale')
  ![](https://i.loli.net/2021/05/16/BE8GL7DFgmxd2fb.png)

- plt.style.use('seaborn-bright')
  ![](https://i.loli.net/2021/05/16/UsRfjHXi9NtZVk4.png)

- plt.style.use('seaborn-colorblind')
  ![](https://i.loli.net/2021/05/16/NdpEHxYAD9WqV2v.png)

- plt.style.use('tableau-colorblind10')

![](https://i.loli.net/2021/05/16/ACv16Wp7e283QXZ.png)



# Jupyter notebook作图

1画图嵌入notebook的方式

%matplotlib inline 标准

%matplotlib notebook 可能会比较卡

mpld3 通过matplotlib代码的替代性呈现（通过d3），虽然不完整，但很好

bokeh 生产可交互图像的更好选择

plot.ly 可以生成非常好的图，貌似付费



# widgets

## 1.ToolHandles

对象：matplotlib.widgets.ToolHandles(ax, x, y, marker='o', marker_props=None, useblit=True)

参数：

- ax：[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)对象
- x，y：一维数组，控制handles的坐标
- marker：字符，显示句柄的标记形状，具体可见[matplotlib.pyplot.plot](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.plot.html#matplotlib.pyplot.plot)
- marker_props：字典，附加的标记属性，具体可见[matplotlib.lines.Line2D](https://matplotlib.org/stable/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D)

方法/属性：

- closest(x, y)：返回索引和到最近索引的像素距离
- set_animated(val)：
- set_data(pts, y=None)：设置句柄x和y的距离
- set_visible(val)：
- x
- y

## 2.SpanSelector

对象：`matplotlib.widgets.SpanSelector(ax, onselect, direction, minspan=None, useblit=False,  rectprops=None, onmove_callback=None, span_stays=False, button=None)`

基类：`matplotlib.widgets._SelectorWidget`

在单个轴上可视化地选择一个范围，然后用这些值调用函数（onselect）。为了保证选择器保持响应，要保留对它的引用，意思就是在构造SpanSelector的时候要把返回值赋值，也就是像`span = SpanSelector(ax,...)`这样。

要关闭 SpanSelector，把span_selector.active 设置为 False。

参数：

- ax：[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)对象
- onselect：func(min, max)，min、max是浮点数
- direction：{"horizontal", "vertical"}，选择器的方向
- minspan：浮点数，默认None，如果小于minspan值则不会调用onselect
- useblit：布尔型，默认False，如果为 True，则使用后端相关的blitting功能来加快画布更新
- rectprops：字典，默认None，[matplotlib.patches.Patch](https://matplotlib.org/stable/api/_as_gen/matplotlib.patches.Patch.html#matplotlib.patches.Patch)的属性字典
- onmove_callback：func(min, max)，min、max是浮点数，默认None，在选择范围内时调用鼠标移动
- span_stays：布尔型，默认False，如果是True，在释放鼠标后SpanSelector保持可见
- button：[MouseButton](https://matplotlib.org/stable/api/backend_bases_api.html#matplotlib.backend_bases.MouseButton)或是[MouseButton](https://matplotlib.org/stable/api/backend_bases_api.html#matplotlib.backend_bases.MouseButton)列表，激活选择器的鼠标按钮

方法：

- ignore(event)：返回是否忽略某个事件。它应该在任何事件回调开始时调用。
- new_axes(ax)：设置SpanSelector在新轴上操作

rectprops的属性可以设置的地方有很多，可以点击链接了解更多，常用的属性是好理解的。

而button的设置暂时还不怎么懂。

## 3.PolygonSelector

对象：`matplotlib.widgets.PolygonSelector(ax, onselect, useblit=False, lineprops=None, markerprops=None, vertex_select_radius=15)`

基类：`matplotlib.widgets._SelectorWidget`

在坐标轴中选择一个多边形区域。

每次单击鼠标放置顶点，并通过完成多边形（单击第一个顶点）来进行选择。 按住Ctrl键并单击并拖动顶点以重新定位它（如果多边形已经完成，则不需要Ctrl键）。按住Shift键并单击并拖动轴中的任意位置以移动所有顶点。 按Esc键开始一个新的多边形。要让选择器保持响应，必须保留对它的引用。

参数：

- ax：[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)对象
- onselect：函数对象，当一个多边形完成或在完成后修改时，调用onselect函数并将顶点列表作为 (xdata, ydata) 元组传递。
- useblit：布尔型，默认False
- lineprops：字典类型，默认为`dict(color='k', linestyle='-', linewidth=2, alpha=0.5)`，表示多边形边缘的线条属性
- markerprops：字典类型，默认为`dict(marker='o', markersize=7, mec='k', mfc='k', alpha=0.5)`，表示多边形定点的标记属性
- vertex_select_radius：浮点数，默认15px，如果鼠标单击在顶点的vertex_select_radius像素内，则选择顶点（以完成多边形或移动顶点）

方法：

- onmove(event)：光标移动的事件处理程序和验证程序

属性：

- verts：多边形顶点，是 (x, y) 点对的列表。

## 4.LockDraw

对象：`matplotlib.widgets.LockDraw`

一些小部件，例如光标，会在画布上绘制，这在所有情况下都是不可取的，例如当工具栏处于缩放至矩形模式并绘制矩形的时候。 为了避免这种情况，在画布上绘制之前，小部件可以使用`canvas.widgetlock(widget)`获取画布的锁；这样能阻止其他小部件同时这样做（如果它们也尝试先获取锁）。

方法：

- available(o)：返回o是否可绘图
- isowner(o)：返回o是否拥有这个锁
- locked()：返回锁当前是否由所有者持有
- release(o)：从o中释放锁

## 5.LassoSelector

对象：`matplotlib.widgets.LassoSelector(ax, onselect=None, useblit=True,lineprops=None, button=None)`

基类：`matplotlib.widgets._SelectorWidget`

可以任意形状的选择曲线，全凭鼠标选择。类似于之前其他的选择器，需要保留引用。所选路径可与contains_point结合使用以从图像中选择数据点

参数：

- ax：[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)对象
- onselect：函数对象，每当套索被释放时，onselect 函数就会被调用并传递所选路径的顶点。
- useblit：布尔型，默认False
- lineprops：字典类型，默认None
- button：用于矩形选择的鼠标按钮。 默认为无，对应所有按钮。

方法：

- onpress(event)
- onrelease(event)

## 6.RectangleSelector

对象：`matplotlib.widgets.RectangleSelector(ax, onselect, drawtype='box', minspanx=0, minspany=0,useblit=False, lineprops=None, rectprops=None, spancoords='data', button=None, maxdist=10, marker_props=None, interactive=False, state_modifier_keys=None)`

基类：`matplotlib.widgets._SelectorWidget`

选择坐标区的一个矩形区域。要保持光标的响应，必须保留对它的引用。

参数：

- ax：[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)对象
- onselect：函数对象，选择完成后的回调函数，它像这样：`def onselect(eclick: MouseEvent, erelease: MouseEvent)`。其中 eclick 和 erelease 是启动和完成选择的鼠标单击和释放鼠标事件
- drawtype：{"box", "line", "none"}，默认box。是否绘制完整的矩形框、矩形的对角线还是什么都不绘制
- minspanx：浮点型，默认为0，x 跨度上最小的选择，更小的会忽略
- minspany：浮点型，默认为0，y 跨度上最小的选择，更小的会忽略
- useblit：布尔值，默认False，是否使用blitting加速绘制
- lineprops：字典，可选，绘制线条的属性，如果drawtype=="line"，默认为`dict(color="blcak", linestyle="-", linewidth=2, alpha=0.5)`
- rectprops：字典，可选，绘制矩形的属性，如果drawtype=="box"，默认为`dict(facecolor="red", edgecolor="black", alpha=0.2, fill=True)`
- spancoords：{"data", "pixels"}，默认"data"，是否以数据或像素坐标解释minspanx和minspany。
- button：MouseButton，或其列表，触发矩形选择的按钮
- maxdist：浮点型，默认10，可以激活交互式工具句柄的距离（以像素为单位）
- marker_props：字典，用于绘制交互式手柄的属性。 当前未实施并被忽略
- interactive：布尔值，默认False，是否绘制一组句柄，允许在绘制后与小部件进行交互
- state_modifier_keys：字典，可选，影响小部件行为的键盘修饰符。 值修改默认值。
  - "move"：移动现有形状，默认：无修饰符
  - "clear"：清除当前形状，默认："escape"
  - "square"：使形状为方形，默认值："shift"
  - "center"：使初始点成为形状的中心，默认值："ctrl"

属性：

- center：矩形的中心
- corners：矩形的四个角，从左下角开始，顺时针移动
- edge_centers：矩形边缘的中点从左边开始，逆时针移动
- extents：返回(xmin, xmax, ymin, ymax)
- geometry：返回一个 形状为(2, 5) 数组，其中包含从左上角开始和结束的矩形四个角的 x (RectangleSelector.geometry[1, :]) 和 y (RectangleSelector.geometry[0, :]) 坐标。

方法：

- draw_shape(extents)

### EllipseSelector

对象：`matplotlib.widgets.EllipseSelector(ax, onselect, drawtype='box', minspanx=0, minspany=0, useblit=False, lineprops=None, rectprops=None, spancoords='data', button=None, maxdist=10, marker_props=None, interactive=False, state_modifier_keys=None)`

基类：`matplotlib.widgets.RectangleSelector`

选择轴的椭圆区域。要保持光标响应，必须保留对它的引用。

参数参考基类RectangleSelector



## 7.Widget

对象：`matplotlib.widgets.Widget`

基类：`object`

GUI元部件的抽象基类。

属性：

- active：是否这个部件激活
- drawon=True
- eventson=True

方法：

- get_active()：获取部件是否激活
- ignore(event)：返回是否应该忽略事件event。此方法应在任何事件回调开始时调用
- set_active(active)：设置部件是否处于激活状态

### AxesWidget

对象：`matplotlib.widgets.AxesWidget(ax)`

基类：`matplotlib.widgets.Widget`

将部件连接到轴Axes。为了保证部件保持响应性而不是垃圾收集，用户应该保持对对象的引用。

属性：

- ax：[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)对象
- canvas：[FigureCanvasBase](https://matplotlib.org/stable/api/backend_bases_api.html#matplotlib.backend_bases.FigureCanvasBase)，部件的父图形画布
- active：布尔值，是否部件是激活的

- cids：

方法：

- connect_event(event, callback)：将回调函数与事件event连接起来。这应该用来代替 figure.canvas.mpl_connect，因为这个函数存储回调 id 以便以后清理

- disconnect_events()：断开由此部件创建的所有事件连接。

#### Button

对象：`matplotlib.widgets.Button(ax, label, image=None, color='0.85', hovercolor='0.95')`

基类：`matplotlib.widgets.AxesWidget`

调用on_clicked连接按钮

属性：

- ax：按钮渲染的[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)对象
- label：一个[matplotlib.text.Text](https://matplotlib.org/stable/api/text_api.html#matplotlib.text.Text)实例
- color：未悬停时按钮的颜色
- hovercolor：悬停时按钮的颜色

参数：

- ax：按钮将被放入哪个[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)实例
- label：字符串，按钮的文本
- image：数组或PIL图像，要放置在按钮中的图像，如果不是None。参数直接转发给imshow
- color：按钮未激活的颜色
- hovercolor：鼠标悬停时按钮的颜色

cnt：

observers：

方法：

- disconnect(cid)：删除连接ID为cid的回调函数
- on_clicked(func)：将回调函数 func 连接到按钮单击事件。返回一个连接id，可用于断开回调。

#### CheckButtons

对象：`matplotlib.widgets.CheckButtons(ax, labels, actives=None)`

基类：`matplotlib.widgets.AxesWidget`

调用on_clicked连接按钮

属性：

- ax：按钮渲染的[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)对象
- labels：[matplotlib.text.Text](https://matplotlib.org/stable/api/text_api.html#matplotlib.text.Text)列表
- rectangles：[Rectangle](https://matplotlib.org/stable/api/_as_gen/matplotlib.patches.Rectangle.html#matplotlib.patches.Rectangle)列表
- lines：(Line2D, Line2D)点对，是复选框中 x 的列表。 每个框都存在这些行，但在未选中其框时具有 set_visible(False) 

参数：

- ax：复选按钮将被放入哪个[matplotlib.axes.Axes](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes)实例
- labels：字符串列表，复选按钮的文本
- actives：布尔值的列表，可选，复选按钮的初始状态，必须和labels长度一致。如果不提供则默认所有按钮未选

cnt：

observers：

方法：

- disconnect(cid)：删除连接ID为cid的回调函数
- on_clicked(func)：将回调函数 func 连接到按钮单击事件。返回一个连接id，可用于断开回调。

- get_status()：返回所有复选按钮的状态（真/假）的元组。
- set_active(index)：按索引切换（激活或停用）复选按钮。如果 eventson 为 True，则触发回调。index为要切换的复选按钮索引，index不合法会触发ValueError

#### Cursor

#### Lasso

#### RadioButtons

#### SliderBase

#### TextBox

### MultiCursor

### SubplotTool

>>>>>>> 282b71fdf6459991c55880644af9aa6bb5e0787b
