# PyQt5 学习笔记

---
[Python Qt官方文档 - 控件部分](https://doc.qt.io/qtforpython-5.12/PySide2/QtWidgets/index.html#module-PySide2.QtWidgets)

[【白月黑羽】Qt图形界面 图文教程合集](https://www.byhy.net/tut/py/gui/qt_05_1/)

[作者视频](https://www.bilibili.com/video/BV1Zf4y1W79o?p=1)
https://www.bilibili.com/video/BV1Zf4y1W79o?p=1


---
# 【注意事项】 缩进 Tab 与 空格 互斥

本文的代码示例，缩进使用的是Tab，直接复制进IDE可能会报错，自行替换成**四个空格**

---

### 通用示例：

```py
button.setText(text) # 改变 按钮/line行输入框 的文本，传入字符串

button.setEnabled(True) # 启用  某个控件，所有继承自QWidget类控件，都支持。
button.setEnabled(False) # 禁用  某个控件，禁用后用户不可操作。

# ↓ 修改某个控件的 背景颜色，传入'red', 'blue', #72a771; 等等参数
self.button.setStyleSheet('background-color: #72a771;') # 背景颜色


```

---
## 按钮 `QPushButton` 

```py
push1.setText('按钮1') # 修改按钮的文本 传入字符串

push1.clicked.connect(self.function) # 当按钮被按下，则执行某个函数
push1.clicked.connect(lambda: self.function('123')) # 函数需传参时用lambda表达式


```


---
## 单行文本框 `QLineEdit` 

![](https://doc.qt.io/qtforpython/_images/windows-lineedit.png)
```py
self.line.text() # 读取文本框的内容
self.line.setText(text) # 把内容写入到文本框内
# 冷门功能 ↓ 
self.line.clear() # 清除文本框的内容
self.line.copy() # 只复制 选中文本 的内容
self.line.paste() # 把剪贴板的内容，粘贴在文本框的光标处
self.line.setPlaceholderText('请在这里输入URL') # 文本框显示提示内容

self.line.textChanged.connect(self.function) # 文本框被编辑, 则调用函数
def function（self, text): # 同上，回调函数会传入文本框的内容，用text接收可直接print。
	print(text) 
	# 可用于检测填入内容，如邮箱手机号等。用法：填处理函数，在函数内用setText获取文本并处理。

```

---
## 多行纯文本框 `QPlainTextEdit`
纯文本与 QTextEdit 不同，TextEdit 是富文本框，可以修改加粗、颜色、字体、字号等等内容。

```py
self.edit.toPlainText() # 获取编辑框内的文本内容
self.edit.setPlainText(text) # 把内容写入到文本框内，覆盖，之前内容会清除
self.edit.insertPlainText('这是在光标插入的信息') # 在光标处插入文本，不换行
self.edit.appendPlainText('你好，这是新加入的消息') # 在末尾添加文本，自动换行

self.edit.setPlaceholderText('请在这里输入薪资表...') # 纯文本框 没消息时的提示消息
self.selection = self.edit.textCursor().selectedText() # 获取选中文本
edit.cursorPositionChanged.connect(self.function) # 当文本框光标改变时，调用函数

self.edit.clear() # 清除文本框的内容
self.edit.copy() # 只复制 选中文本 的内容
self.edit.paste() # 把剪贴板的内容，粘贴在文本框的光标处
self.edit.textChanged.connect(self.function) # 当文本框内容被编辑则调用函数
edit.document().setMaximumBlockCount(100) # 最大行数，超过则删除前面内容，防占用

```

---
## 文本浏览框 `QTextBrowser`
`QTextBrowser` 是 `只能查看文本` 控件。
通常用来显示一些操作日志信息、或者不需要用户编辑的大段文本内容。
该控件获取文本、修改、清除、剪贴板复制粘贴 等等， 都和上面纯文本框是一样的。

不同的地方：
```py
edit.append('你好，白月黑羽') # 在编辑框末尾添加文本内容
edit.insertPlainText('你好，白月黑羽') # 在编辑框末尾添加文本内容，不换行

def print_logo(self,test): # 打印logo日志, 传入字符串，并显示新消息
	self.print_logo.append(test) # 把内容添加到日志框
	self.print_logo.ensureCursorVisible() # 自动翻滚文本框，显示新添加的消息
```


---
## 标签 `QLabel`
常见的标签，可以显示文字（包括纯文本和富文本）、图片 甚至动画。
插入图片在 Qlabel - pixmap 内可选择图片路径。
`button.setText(text) # 修改标签文本内容`

---


## 选择文件 / 选择文件夹 `QFileDialog`

选择文件或者目录
`getExistingDirectory` 选择目录，字符串。
`getOpenFileName` 选择单个文件，字符串。
`getOpenFileNames` 选择 单个/多个 文件，返回列表。

```py
image_file, _ = QFileDialog.getOpenFileName(self,'选择文件', './','选择图片 (*.jpg*.png *.jpeg)') # 传参（self父类，选择框标题，起始目录'D://'，说明+格式要求）
# 选择单个文件，返回两个参数，字符串，取消不选则为''空，

image_files, _ = QFileDialog.getOpenFileNames(self,'选择单个或多个文件', './','选择图片 (*.jpg*.png *.jpeg)') # 同上，# 选择单个/多个文件，返回两个参数，接收内容为列表，取消不选则为[]空列表

image_dir = QFileDialog.getExistingDirectory(self,'选择文件夹', './') # 标题、路径
# 选择文件夹，返回文件夹路径字符串，取消不选则为''空

save_path, _ = QFileDialog.getSaveFileName(self, "选择保存文件路径", './', '保存格式 (*.txt *.mpr)') # 选择保存路径, return返回选择路径，字符串，如'D:/aa/t1.txt'，取消为''空

# 在 我的模板 里有详细的完成的函数
```


---
## 下拉框 / 组合选择框 `QComboBox`

组合选择框，下拉框。 [官网介绍](https://doc.qt.io/qtforpython-5.12/PySide2/QtWidgets/QComboBox.html)

```py
mode = cbox.currentText() # 获取当前选项的 文本/内容

cbox.addItem('选项x') # 在末尾，新增一个选项
cbox.addItems(['byhy','白月黑羽','python教程']) # 在末尾，新增多个选项
cbox.removeItem(index) # 删除某一个选项，传入选项的索引
cbox.clear() # 清空/删除 全部所有选项
cbox.currentIndexChanged.connect(self.function) # 信号，当选项改变时执行函数
```

---
## 单选按钮 `QRadioButton`

![image](https://cdn2.byhy.net/imgs/gh/36257654_69709779-0a30cd80-1139-11ea-8ac6-eb19387ad278.png)

`同一个父窗口` 里面的多个按钮，只能选中一项。
如果你有多组单选按钮， 每组都应该有不同的父控件，或者不同的Layout。
**建议：** 把每一组单选按钮，放到不同的按钮组，右键分组。 [作者视频讲解](https://www.bilibili.com/video/BV1cJ411R7bP?p=12)

```py
# 示例： 创建了两个按钮，猫和狗，放进了叫 cat_dog 的按钮组
self.cat_dog.buttonClicked.connect(self.function) # 信号，点击任意按钮 调用函数
txt = self.cat_dog.checkedButton().text() # 获取按钮组里，选项的文本，字符串
```

---
## 勾选按钮 `QCheckBox`

![image](https://cdn2.byhy.net/imgs/gh/36257654_69712525-f3d94080-113d-11ea-87f7-473072834121.png)

同上，多个按钮，放进一个按钮组里，默认为单选，使用方法和效果 同上 ↑ 

多选模式，需要注意
在 Qt设计师编辑器中，可以设置 按钮组 的 `exclusive` 属性，√为单选，X为多选

```py
# 示例：创建多个勾选按钮，并放进 buttonGroup_feizai 按钮组
self.buttonGroup_feizai.buttonClicked.connect(self.function) # 信号 调用函数
# 单选模式
txt = self.buttonGroup_feizai.checkedButton().text() # 按钮组单选，读取按钮组的结果

# 多选模式，手动查询每个按钮，勾选时为True，不勾为False
print(self.checkBox_1.isChecked()) # 查询按钮状态，勾True，不勾False
print(self.checkBox_2.isChecked())

# 多选模式下，不能用单选的方式，不勾时返回None，无法做判断
```

---

## 进度条 `QProgressBar`

进度条是一个常用的控件，当程序需要做一件比较耗费时间的任务（比如统计数据，下载文件等），可以用来向用户指示操作的进度。

放在循环中，但是当处理时间很长，如超过10秒，防止未响应，最好是在多线程运行

```py
self.progressBar.setRange(0,10) # 设定进度的步数，起始和结束
self.progressBar.setValue(3) # 更新进度到哪一步
self.progressBar.reset() # 重置进度条
```






---
## 表格控件 `QTableWidget`

[【文章介绍】](https://www.byhy.net/tut/py/gui/qt_05_2/#表格)

```py
txt = self.excel.item(0,0).text() # 获取单元格的文本内容，参数为 行/列 索引

self.excel.setItem(1, 1, QTableWidgetItem('白月黑羽')) # ↓ 新增/修改表格内容。传入 行/列 的索引，和表格实例化后的内容。索引与表格不符则跳过不报错
self.excel.item(0,0).setText('江老师') # 修改表格已有内容。传入行/列索引，索引无效则报错

# 行列数量 读取/修改，删除表格内容
rowcount = self.excel.rowCount() # 获取表格所有的 行数
rowcount = self.excel.columnCount() # 获取表格所有的 列数
currentrow = table.currentRow() # 获取当前选中是第几行 (索引), 方便在表格中间插入新行
self.excel.setRowCount(10) # 设置修改 表格行数
self.excel.setColumnCount(10) # 设置修改 表格列数
self.excel.clearContents() # 删除表格所有内容，但表格行列还在，删除用setRowCount

self.excel.horizontalHeader().setStretchLastSection(True) #表格最后1列贴边不留空
# 或者在Qt设计师编辑器内，表格控件属性里，勾选 HorizontalHeaderStretchLastSection

self.excel.cellChanged.connect(self.function) # 信号，当表格内容改变时调用函数
def function(self, row, columu): # 回调函数，返回行列索引
	print(f'第{row}行，第{columu}列，内容被修改')

# 只有列的表格：
# 表格每列的宽度，默认100，传入列的索引和宽度
self.excel.horizontalHeader().resizeSection(0,150)
self.excel.horizontalHeader().resizeSection(1,100)
# 插入显示至表格，传入二维列表，如[[1,2,3],[4,5,6],] 只有一个列表需写成 [[1,2,3],] 
def input_excel(self, lists): 
	for i in range(len(lists)):
		item = lists[i]
		row = self.excel.rowCount()
		self.excel.insertRow(row)
		for j in range(len(item)):
			item = QTableWidgetItem(str(lists[i][j]))
			self.excel.setItem(row,j,item)

```

---


## 日期控件 `QDateEdit` 

QDate 对象的具体说明[参考官方文档](https://doc.qt.io/qtforpython-5.12/PySide2/QtCore/QDate.html)

```py

qdate = self.dateEdit.date()
qdate.toString('yyyy-MM-dd') # 获取控件内容，并转换成指定格式
# 年月日
year = qdate.year()   # 返回 2020
month = qdate.month() # 返回 5
day = qdate.day()     # 返回 2
# 格式参考
'yyyy-MM-dd dddd'=2000-01-01 星期六

# 相关内容不太好找，已放弃摆烂

```

---

> 未完待续...  


---

笔记时间：
2022年12月9日下午晚上 创建  
2022年12月10日05:37:08 完成大部分  



