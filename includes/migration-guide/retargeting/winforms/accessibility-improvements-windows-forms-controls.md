### <a name="accessibility-improvements-in-windows-forms-controls"></a>Windows 窗体控件中的可访问性改进

|   |   |
|---|---|
|详细信息|Windows 窗体提高它的工作原理与可访问性技术更好地支持 Windows 窗体客户。 这些方法包括以下更改：<ul><li>在高对比度模式下显示更改，以提高。</li><li>更改，以提高属性浏览器体验。 属性浏览器改进包括：</li><li>更好地通过各种下拉选择窗口使用键盘导航。</li><li>减少不必要的制表位。</li><li>更好地报告控件类型。</li><li>改进了讲述人行为。</li><li>若要在控件中实现缺少的 UI 可访问性模式的更改。</li></ul>|
|建议|<strong>如何选择加入或退出这些更改</strong>使应用程序以利用这些更改，它必须运行.NET Framework 4.7.1 上或更高版本。 应用程序可以利用这些更改通过以下方式之一：<ul><li>它被编译为面向.NET Framework 4.7.1。 这些可访问性更改为默认情况下，在面向.NET Framework 4.7.1 的 Windows 窗体应用程序上启用或更高版本。</li><li>它通过将以下内容添加 opts 外的旧的可访问性行为[AppContext 交换机](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)到<code>&lt;runtime&gt;</code>部分的 app.config 文件，将其设置为<code>false</code>，如下面的示例所示。</li></ul><pre><code class="language-xml">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;&#13;&#10;&lt;configuration&gt;&#13;&#10;&lt;startup&gt;&#13;&#10;&lt;supportedRuntime version=&quot;v4.0&quot; sku=&quot;.NETFramework,Version=v4.7&quot;/&gt;&#13;&#10;&lt;/startup&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;!-- AppContextSwitchOverrides value attribute is in the form of &#39;key1=true/false;key2=true/false  --&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>面向.NET Framework 4.7.1 的应用程序或更高版本，并且想要保留旧可访问性行为来选择加入的旧的可访问性功能的使用通过此 AppContext 开关显式设置为<code>true</code>。UI 自动化的概述，请参阅[UI 自动化概述](~/docs/framework/ui-automation/ui-automation-overview.md)。<strong>增加了对 UI 自动化模式和属性支持</strong>辅助功能客户端可以通过使用通用、 公开描述调用模式充分利用新 WinForms 可访问性功能。 这些模式不是特定于 WinForms 的。 例如，辅助功能客户端可以 IAccessible 接口 (MAAS) 若要获取的 IServiceProvider 接口上调用 QueryInterface 方法。 此接口是否可用，客户端可以使用其 QueryService 方法来请求 IAccessibleEx 接口。 有关详细信息，请参阅[从客户端使用 IAccessibleEx](https://msdn.microsoft.com/library/windows/desktop/dd561924.aspx)。 从.NET Framework 4.7.1，IServiceProvider 开始和[IAccessibleEx](https://msdn.microsoft.com/library/windows/desktop/dd561898.aspx) （如果适用） 可用于 WinForms 辅助功能对象。.NET Framework 4.7.1 添加以下 UI 自动化模式和属性的支持：<ul><li><code>T:System.Windows.Forms.ToolStripSplitButton</code>和<code>T:System.Windows.Forms.ComboBox</code>控件支持[展开/折叠模式](~/docs/framework/ui-automation/implementing-the-ui-automation-expandcollapse-control-pattern.md)。</li><li><code>T:System.Windows.Forms.ToolStripMenuItem</code>控件具有[ControlType](~/docs/framework/ui-automation/ui-automation-support-for-the-menubar-control-type.md)属性值<xref:System.Windows.Automation.ControlType.MenuItem?displayProperty=nameWithType>。</li><li><code>T:System.Windows.Forms.ToolStripItem</code>控件支持[名称](xref:System.Windows.Automation.AutomationElement.NameProperty)属性和[展开/折叠模式](~/docs/framework/ui-automation/implementing-the-ui-automation-expandcollapse-control-pattern.md)。</li><li><code>T:System.Windows.Forms.ToolStripDropDownItem</code>控件支持<xref:System.Windows.Forms.AccessibleEvents>，该值指示 StateChange 和 NameChange 时下拉列表是展开还是折叠。</li><li><code>T:System.Windows.Forms.ToolStripDropDownButton</code>控件具有[ControlType](~/docs/framework/ui-automation/ui-automation-support-for-the-menubar-control-type.md)属性值<xref:System.Windows.Automation.ControlType.MenuItem?displayProperty=nameWithType>。</li><li><code>T:System.Windows.Forms.DataGridViewCheckBoxCell</code>控件支持[Toggle 模式](xref:System.Windows.Automation.TogglePattern)。</li><li><code>T:System.Windows.Forms.NumericUpDown</code>和<code>T:System.Windows.Forms.DomainUpDown</code>控件支持[名称](xref:System.Windows.Automation.AutomationElement.NameProperty)并且具有[ControlType](~/docs/framework/ui-automation/ui-automation-support-for-the-spinner-control-type.md)的<xref:System.Windows.Automation.ControlType.Spinner?displayProperty=nameWithType>。</li></ul><strong>对属性网格控制的改进</strong>的.NET Framework 4.7.1 向 PropertyBrowser 控件添加了以下改进：<ul><li><strong>详细信息</strong>在用户输入中的值不正确时，将显示错误对话框的按钮<code>T:System.Windows.Forms.PropertyGrid</code>控件支持[展开/折叠模式](~/docs/framework/ui-automation/implementing-the-ui-automation-expandcollapse-control-pattern.md)、 状态和名称更改通知，和一个[ControlType](~/docs/framework/ui-automation/ui-automation-support-for-the-menubar-control-type.md)属性值为<xref:System.Windows.Automation.ControlType.MenuItem?displayProperty=nameWithType>。</li><li>消息窗格中显示时<strong>详细信息</strong>展开的错误对话框的按钮现在是键盘可访问并且允许讲述人地宣布错误消息的内容。</li><li><xref:System.Windows.Forms.AccessibleRole>中的行<code>T:System.Windows.Forms.PropertyGrid</code>控制已更改从&quot;行&quot;到&quot;单元格&quot;。 单元格将映射到 UIA ControlType &quot;DataItem&quot;，这使得它能够支持相应的键盘快捷方式和讲述人公告。</li><li><code>T:System.Windows.Forms.PropertyGrid</code>控制哪些表示标头的项的行<code>T:System.Windows.Forms.PropertyGrid</code>控件具有<code>P:System.Windows.Forms.PropertySort</code>属性设置为<code>F:System.Windows.Forms.PropertySory.Categorized</code>具有[ControlType](~/docs/framework/ui-automation/ui-automation-support-for-the-menubar-control-type.md)属性值 <xref:System.Windows.Automation.ControlType.Button?displayProperty=nameWithType></li><li><code>T:System.Windows.Forms.PropertyGrid</code>控制哪些表示标头的项的行<code>T:System.Windows.Forms.PropertyGrid</code>控件具有<code>P:System.Windows.Forms.PropertySort</code>属性设置为<code>F:System.Windows.Forms.PropertySory.Categorized</code>支持[展开/折叠模式](~/docs/framework/ui-automation/implementing-the-ui-automation-expandcollapse-control-pattern.md)。</li><li>网格与它上方的工具栏之间改进的键盘导航。 按&quot;Shift Tab&quot;现在选择第一个工具栏按钮，而不是整个工具栏</li><li><code>T:System.Windows.Forms.PropertyGrid</code> 在高对比度模式下显示的控件将现在周围绘制聚焦框的工具栏按钮对应到当前<code>P:System.Windows.Forms.PropertySort</code>属性值。</li><li><code>T:System.Windows.Forms.PropertyGrid</code> 控件显示在高对比度模式，并与<code>P:System.Windows.Forms.PropertySort</code>属性设置为<code>F:System.Windows.Forms.PropertySory.Categorized</code>将现在显示高度对比颜色的颜色的类别标题的背景。</li><li><code>T:System.Windows.Forms.PropertyGrid</code> 控件更好地区分具有焦点的工具栏项和工具栏项表示的当前值<code>P:System.Windows.Forms.PropertySort</code>属性。 此修补程序包含高对比度更改和非高对比度方案的更改。</li><li><code>T:System.Windows.Forms.PropertyGrid</code> 控制工具栏项表示的当前值<code>P:System.Windows.Forms.PropertySort</code>属性支持[Toggle 模式](xref:System.Windows.Automation.TogglePattern)。</li><li>改进了对区分对齐选取器中的所选的对齐讲述人支持。</li><li>当一个空<code>T:System.Windows.Forms.PropertyGrid</code>窗体上显示控件，它现在将会收到的焦点其中以前它不会。</li></ul><strong>高对比度主题中的使用操作系统定义的颜色</strong><ul><li><code>T:System.Windows.Forms.Button</code> 和<code>T:System.Windows.Forms.CheckBox</code>控制与<code>P:System.Windows.Forms.Control.FlatStyle</code>设置为<xref:System.Windows.Forms.FlatStyle.System?displayProperty=nameWithType>默认样式时，现在使用选中的高对比度主题中的操作系统定义的颜色。 以前，文本和背景色已不对比，且难以读取。</li><li><code>T:System.Windows.Forms.Button</code><code>T:System.Windows.Forms.CheckBox</code>， <code>T:System.Windows.Forms.RadioButton</code>， <code>T:System.Windows.Forms.Label</code>，<code>T:System.Windows.Forms.LinkLabel</code>和<code>T:System.Windows.Forms.GroupBox</code>与<code>P:System.Windows.Forms.Control.Enabled</code>设置为<em>false</em>，使用带的阴影颜色呈现在高对比度主题，从而导致针对低对比度的文本背景。 现在，这些控件使用&quot;禁用文本&quot;由操作系统定义的颜色。 此修补程序适用于使用的控件<code>P:System.Windows.Forms.Control.FlatStyle</code>属性设置为值非<code>F:System.Windows.Forms.FlatStyle.System</code>。 后一种控件呈现操作系统。</li><li><code>T:System.Windows.Forms.DataGridView</code> 现在呈现当前具有焦点的单元格内容周围可见矩形。 以前，这不是在某些高对比度主题中可见的。</li><li><code>T:System.Windows.Forms.ToolStripMenuItem</code> 控制与<code>P:System.Windows.Forms.ToolStripItem.Enabled</code>属性设置为<em>false</em>现在使用&quot;禁用文本&quot;由操作系统定义的颜色。</li><li><code>T:System.Windows.Forms.ToolStripMenuItem</code> 控制与<code>P:System.Windows.Forms.ToolStripItem.Checked</code>属性设置为<em>true</em>现在呈现关联的复选标记以对比系统颜色。  以前的复选标记颜色已不对比足够和在高对比度主题中不可见。</li></ul>注意： windows 10 已更改一些高对比度系统颜色的值。 Windows 窗体框架基于 Win32 framework。 为获得最佳体验，最新版本的 Windows 上运行并选择加入到最新的操作系统更改，通过在测试应用程序中添加应用程序清单文件并取消注释以下代码：<pre><code>&lt;!-- Windows 10 --&gt;&#13;&#10;&lt;supportedOS Id=&quot;{8e0f7a12-bfb3-4fe8-b9a5-48fd50a15a9a}&quot; /&gt;&#13;&#10;</code></pre><strong>改进的键盘导航</strong><ul><li>当<code>T:System.Windows.Forms.ComboBox</code>控件具有<code>P:System.Windows.Forms.ComboBox.DropDownStyle</code>设置为<code>F:System.Windows.Forms.DropDownStyle.DropDownList</code>且在窗体上排序的选项卡中的第一个控件使用键盘打开父窗体时，它会立即显示聚焦框。 在此更改之前键盘焦点在控件中，但不是呈现焦点指示器。</li></ul><strong>改进了讲述人支持</strong><ul><li><code>T:System.Windows.Forms.MonthCalendar</code>控件已添加对辅助技术，以访问控件，包括讲述人时以前无法阅读该控件的值的功能的支持。</li><li><code>T:System.Windows.Forms.CheckedListBox</code>控件现在通知讲述人时<code>P:System.Windows.Forms.CheckState</code>属性已更改。 以前，讲述人未收到通知，因此用户就会通知，<code>P:System.Windows.Forms.CheckState</code>已更新。</li><li><code>T:System.Windows.Forms.LinkLabel</code>控制已更改其通知控件中的文本的讲述人的方式。 以前，讲述人两次宣布此文本和读取&quot; &amp; &quot;符号为实际的文本，即使它们不是对用户可见。 重复的文本已从讲述人公告，移除以及不必要&quot; &amp; &quot;符号。</li><li><code>T:System.Windows.Forms.DataGridViewCell</code>控件现在类型正确报表只读状态设置为讲述人和其他辅助技术。</li><li>讲述人现在是否能够读取系统菜单中的子窗口[多文档界面](~/docs/framework/winforms/advanced/multiple-document-interface-mdi-applications.md)应用程序。</li><li>讲述人现在是否能够读取<code>T:System.Windows.Forms.ToolStripMenuItem</code>控制与<code>P:System.Windows.Forms.ToolStripItem.Enabled</code>属性设置为<em>false</em>。 以前，讲述人是无法专注于已禁用的菜单项来读取内容。</li></ul>|
|范围|主要|
|版本|4.7.1|
|类型|重定目标|
|受影响的 API|<ul><li><xref:System.Windows.Forms.ToolStripDropDownButton.CreateAccessibilityInstance?displayProperty=nameWithType></li><li><xref:System.Windows.Forms.DomainUpDown.DomainUpDownAccessibleObject.Name?displayProperty=nameWithType></li><li>[MonthCalendar.AccessibilityObject](xref:System.Windows.Forms.Control.AccessibilityObject)</li></ul>|
