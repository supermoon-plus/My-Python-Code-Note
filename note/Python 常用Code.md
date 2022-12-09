


# Python常用代码集 md版

---


- TK窗口库[链接](https://www.jianshu.com/p/91844c5bca78)
- pynput库，截图 = grab_screen(region=(x1, y1, x2, y2))

图像PIL库的基础用法笔记  
[Link1](https://www.jb51.net/article/225452.htm) / [Link2](https://blog.csdn.net/zhangziju/article/details/79123275) / [Link3](https://blog.csdn.net/qq_37816453/article/details/80434150)

教程：[董付国老师Python教程合集 Link](https://space.bilibili.com/33583863/channel/collectiondetail?sid=142598)

安装第三方库时，需要关闭代理...`Off Free internet`

CMD中安装失败时，可以在后面加上
`--trusted-host mirrors.aliyun.com`  
如：
`python -m pip install --upgrade pip --trusted-host mirrors.aliyun.com`

安装第三方库命令, 防失败版 [来源](https://blog.csdn.net/bjtu_linxinyu/article/details/105468658)  
`pip install 库名 -i http://pypi.douban.com/simple --trusted-host pypi.douban.com`

【升级pip】  
`python -m pip install --upgrade pip`

清华的镜像安装第三方库，如OpenCV  
`pip install -i https://pypi.tuna.tsinghua.edu.cn/simple opencv-python`


**国内镜像源：**  [来源视频：python安装库的4种方式](https://www.bilibili.com/video/BV1WB4y1P7Nk)  
阿里云： http://mirrors.aliyun.com/pypi/simple/  
中国科技大学： https://pypi.mirrors.ustc.edu.cn/simple/   
豆瓣(douban)： http://pypi.douban.com/simple/  
清华大学： https://pypi.tuna.tsinghua.edu.cn/simple/  


## ==记录一些常见代码== ↓

```Python

# PyAutoGui 的弹窗
pyautogui.alert('这个消息弹窗是文字+OK按钮')
pyautogui.confirm('这个消息弹窗是文字+OK+Cancel按钮')
pyautogui.prompt('这个消息弹窗是让用户输入字符串，单击OK')

path.replace("\\", "/") #路径转义\转/，c:\aa\1.jpg → c:/aa/1.jpg
path.replace('\\','\\\\') #双反斜杠 c:\\aa\\2.jpg

random.choice(png_list) # 从列表中随机取1个元素
random.choices(png_list, k=20) # 从列表中随机截取20个元素，返回一个新列表

with open("text.txt","w") as f: # 读取文本、分割符号、"r"read读取，"x"读取.若无 则生成,"w"写文件,"a"追加内容
    f = f.strip() # 去除前后空行
    f_list = f.split(",") # 用，分割字符
    f1 = f_list[1] # 取下标

a=[]
a.pop() # 将a列表最后一位移除，可赋值给变量，加(1)下标可移除指定元素
b.strip() # 可以去掉前后的空格、Tab等等

# 让Python播放声音，库名winsound，链接http://t.csdn.cn/dscTe
winsound.PlaySound('D:\PyCharm\music\yuri.wav', winsound.SND_FILENAME) # 某个文件
winsound.PlaySound('SystemExit', winsound.SND_ALIAS) #系统弹窗提示音
winsound.PlaySound('SystemHand', winsound.SND_ALIAS) #系统-噔↗噔噔↘~

# 一行代码：浏览器DIY 全局修改
document.body.contentEditable='true';

#四舍五入至整数，后面可定义小数保留位数，无则不处理
round(3.1415926585,2)

# 计算代码运行时间
t1=time.time()
t2=time.time()
print(t2-t1)

# 按Q键退出程序（CV2的）
if cv2.waitKey(1) == ord('q'):
    break
```

### 内容模板
```Python

```
### 内容模板
```Python

```



### PyQt5 PySide2 相关内容
- ==【PyCharm】== 安装pyqt5-tools，打开File文件—>Settings设置—工具->External Tools外部工具，配置designer和pyuic工具
    - 添加Name:QtDesigner，填入`designer.exe`路径，Working directory工作参数 $ProjectFileDir$  
    - add Name:Pyuic,Program填入`pyuic5.exe`路径，Arguments实参：`-m PyQt5.uic.pyuic $FileName$ -o $FileNameWithoutExtension$.py`
    Working directory工作目录：$FileDir$  
    [CSDN 相关参考链接](https://blog.csdn.net/qq_40548768/article/details/121051406)
- ==【VSCode】PyQt5：== 安装pyqt integration扩展，进入设置-拓展-PYQT integration  
`Pyqt-integration › Pyuic: Cmd`, 填入`pyuic5.exe`路径  
`Pyqt-integration › Qtdesigner: Path`, 填入`designer.exe`路径  
在ui文件右键`Compile From`转换  
[参考文章](https://blog.csdn.net/anwei20000/article/details/127951729)  
- ==【VSCode】PySide2：== 安装PySide2-VSC，进入设置-拓展-PySide2-VSC，  
`Designer-creator: Path`, 填入`designer.exe`路径  
`Uic: Cmd`, 填入`pyuic5.exe`路径  
在ui文件右键`Compile From`转换  
- ==【手动执行】==, 在pyuic5目录下启动cmd命令窗口执行`pyuic5 -o demo.py demo.ui`，执行转换当前目录下的ui文件至py文件  

[窗口测试和调用ui参考帖子](https://blog.csdn.net/weixin_33895016/article/details/94172010)



```Python
import sys
from PyQt5 import QtCore, QtGui, QtWidgets
from PyQt5.QtCore import *
from PyQt5.QtWidgets import QFileDialog, QMessageBox, QDockWidget, QListWidget
from PyQt5.QtGui import *
from ui_demo import Ui_MainWindow  #导入创建的GUI类

#自己建一个mywindows类，mywindow是自己的类名。QtWidgets.QMainWindow：继承该类方法
class mywindow(QtWidgets.QMainWindow, Ui_MainWindow):
    #__init__:析构函数，也就是类被创建后就会预先加载的项目。
    # 马上运行，这个方法可以用来对你的对象做一些你希望的初始化
    def __init__(self):
        #这里需要重载一下mywindow，同时也包含了QtWidgets.QMainWindow的预加载项。
        super(mywindow, self).__init__()
        self.setupUi(self)
if __name__ == '__main__': #如果整个程序是主程序
    # QApplication相当于main函数，也就是整个程序（很多文件）的主入口函数。
    # 对于GUI程序必须至少有一个这样的实例来让程序运行。
    app = QtWidgets.QApplication(sys.argv)
    #生成 mywindow 类的实例。
    window = mywindow()
    #有了实例，就得让它显示，show()是QWidget的方法，用于显示窗口。
    window.setWindowTitle("窗口标题")
    window.show()
    # 调用sys库的exit退出方法，条件是app.exec_()，也就是整个窗口关闭。
    # 有时候退出程序后，sys.exit(app.exec_())会报错，改用app.exec_()就没事
    # https://stackoverflow.com/questions/25719524/difference-between-sys-exitapp-exec-and-app-exec
    sys.exit(app.exec_())
```



### keyboard · 键盘控制 [【GitHub自述】](https://github.com/boppreh/keyboard)
```Python
keyboard.wait('a') #阻塞暂停并持续监听按键a, 直到按下

keyboard.add_hotkey('esc', def_aaa) #按esc 调用aaa函数
keyboard.add_hotkey('ctrl+alt', def_bbb, args=('传参')) #按ctrl+alt 调用bbb函数，并传参
keyboard.wait('q') # 按q键时结束监听组合，停止阻塞继续往下执行，不可循环

event = keyboard.read_event()
#阻塞,获取按键按下事件并判断是否按下和等于xx，按任意键继续，套循环内
if event.event_type == keyboard.KEY_DOWN and event.name == 'space':
    print('space was pressed')

```


### Pywin32 · 库 
【文章：】[【掘金Link1】](https://juejin.cn/post/7090752895699648549)  [【小鹏同学公号 · 函数模板】](https://mp.weixin.qq.com/s/s2cDsD0f-orJpydYB_sHXg)  
[【微软键盘码】](https://learn.microsoft.com/zh-cn/windows/win32/inputdev/virtual-key-codes)/[【CSDN键码】](https://blog.csdn.net/zhanglidn013/article/details/35988381)/[【图床 · 键码对照表.jpg】](https://www.imagehub.cc/image/JPninT)
```Python
import win32gui, win32api, win32con

win32api.SetCursorPos((100, 100)) # 移动鼠标至坐标
x, y = win32api.GetCursorPos() # 获取当前鼠标坐标

win32api.keybd_event(78, 0, 0, 0) # 模拟键盘,传入键码78
win32api.keybd_event(78, 0, win32con.KEYEVENTF_KEYUP, 0)

handle = win32gui.FindWindow(None, '记事本')
# 获取窗口句柄
handleDetail = win32gui.GetWindowRect(handle)
# 返回句柄窗口的左上xy + 右下xy坐标
```


---
## Python嵌入式
[【Python嵌入式 DIY Pyinstaller】](https://github.com/750ti/DIY-Pyinstaller-embed)https://github.com/750ti/DIY-Pyinstaller-embed   
【PyStand】嵌入式Python启动器[【知乎文章】](https://www.zhihu.com/question/48776632/answer/2336654649) / [【GitHub】](https://github.com/skywind3000/PyStand)  



---

[【pyhook监控键盘库】](https://www.jianshu.com/p/9146a6038e70)

### keyboard 鼠标键盘库 [【Github项目】](https://github.com/boppreh/keyboard#keyboard.KEY_DOWN) / [【鼠标库】](https://github.com/boppreh/mouse)
```Python
keyboard.wait('a') # 持续等待按键,是否按下a,等待中程序停止
keyboard.add_hotkey('f1', 函数a)
# 按下F1后，执行函数, 程序不会停止，注意会重复执行的问题
keyboard.add_hotkey('ctrl+alt', test, args=('b',)) # 同上，并传递参数
keyboard.add_hotkey('space', lambda: print('按下空格!'))
keyboard.add_hotkey('a', lambda: print('按下 a '))
keyboard.wait() # 让上面的语句持续循环

recorded = keyboard.record(until='esc') # 



```

### 徽标制作方法  
[**【徽标官网 Shields】**](https://shields.io/)  /  [【CSDN】](https://blog.csdn.net/Wang_Si_D/article/details/115764014)  
使用Shields网站，填入【标签-name-颜色】即可生成网站，打开后为图片、图标  
再使用MarkDown语法, ```![]()```, 将该图片显示出来，加链接同理```[]()```, 用[]包住整个语句再（）里加链接，颜色可用16进制值, 如```ff3c53```  
![](https://img.shields.io/badge/YouTube-baicai-red)   
比如这段便是上面图标的图片网址```https://img.shields.io/badge/YouTube-baicai-red```


### 读写文件 [Video Link](https://www.bilibili.com/video/BV19o4y1Q75E)
```Python
f = open("text.txt",x) # "r"表示read读取，"x"表示读取，若无 则生成。"w"写文件，"a"追加内容
f.close() # 关闭文件，有打开必须有关闭

f.read # 读取整个文件，加(10)表示只读前10个字符串，用for遍历可取每一行
f.readline # 只读一行
f.write("Hello World!") # 写入内容并覆盖
f.writelines("Hello python 222") # 写入（未知

os.remove("text.txt") # 用os库删除文件

```

### 脚本控制 常用代码
```Python
def run(): # 判断鼠标位置，控制脚本是否终止
    now_x, now_y = pyautogui.position() # 获取记录鼠标当前位置
    if now_x <30 and now_y < 30: # 比对条件，如鼠标移动某个位置，则触发，示例为左上角30像素内
        return False
    return True
while run(): # 让每次循环，都符合预定的条件，否则循环off
while pyautogui.onScreen(pyautogui.position()): #条件死循环：当鼠标在主显示器内时为true，屏幕外为false，用于判断条件

exit() # 停止/终止 当前整个脚本运行
break # 跳出/结束 整个循环，不影响 if判断
continue # 跳过 本次循环

```
### 仿按键精灵_找色_找图

```python
# 找色
单人游戏 = pyautogui.screenshot().getpixel((x, y))  # 根据坐标取色，注意：坐标+颜色均为(元组)的形式传入
    if 单人游戏 == (107, 16, 16):
    pyautogui.click(x, y) # 点击该坐标
    #pyautogui.moveTo(x,y) # 移动鼠标位置
```
```python
# 找图
变量名=pyautogui.locateOnScreen("D:\PyCharm\image\a.png",confidence=0.8) # 填入非中文的 绝对路径，相似度0.8
if 变量名 is not None: # 判断查找后的值是否 不是空的
    x,y=pyautogui.center(变量名) # 将图片的坐标赋值
    print("已找到图标")
    print(x, y) # 打印该坐标
    pyautogui.leftClick(x, y) # 点击该坐标
```
#### **代码集 ↑**

---

### 列表推导式、三元运算
```Python
# 常用写法
a=1
print('OK成立') if a==1 else print('NO不成立') # 【成立 判断 不成立】，三段式结构
变量 = "OK_True" if a==1 else "NO_False" # 变量赋值 = 【成立 判断 不成立】
# 套娃写法
pyint('OK') if 条件2==1 else print('NO') if 条件1==1 else print('条件1 is NO')
# 条件成立时，可以继续套娃下去，但代码可读性极差
```


### 循环条件，鼠标移除显示器则为False
```

```

### 遍历txt文本，并逐行比对，案例：红警地图有多少颗树
```python
map=open("冰天雪地.map")
a=1
for list in map:
    if "TREE" in list:
        print("计次",a,":",list,end="")
        a+=1
map.close() # 关闭文件
```
### 时间库 time/datetime [定时脚本](https://blog.csdn.net/t8116189520/article/details/78832548)
```python
time.sleep(1) # 延时 1秒
now = datetime.datetime.now() # 获取当前时间
print(now.hour,now.minute) # 获取当前小时、分钟时间，可用于定时任务判断

#获取当前的日期和时间
import time, datetime
now = datetime.datetime.now()
print ("当前的日期和时间是 %s" %now)
print ("当前的年份是 %s" %now.year)
print ("当前的月份是 %s" %now.month)
print ("当前的日期是  %s" %now.day)
print ("当前小时是 %s" %now.hour)
print ("当前分钟是 %s" %now.minute)
print ("当前秒是  %s" %now.second)
```
### 用BAT打开.py文件脚本 路径非中文
```bat
@echo off
chcp 65001
.\runtime\python.exe .\demo.py
// 新方法，↑ 空格分割，前为解释器，后面是.py
// 可以是绝对坐标，也可以是基于bat文件的相对坐标
// 例如 D:\a\python.exe D:\demo1.py
```
```bat
@echo off  
D:
cd D:\PyCharm
start python demo.py
exit 
// 常规方法 D:是py脚本盘符，cd到py文件目录再打开
```

### OS 系统库 打开文件
```python

os.MessageBox("hello world弹窗")

# https://www.bilibili.com/video/BV1Fa411m7Uq
for a,b,c in os.walk(path): # http://t.csdn.cn/RvLAD
    # 遍历指定路径，并用abc接收，a=当前绝对路径，b=当前文件夹名list，c=文件名list
path.isfile(path) # 布尔值,判断是否为文件，排除文件夹，搭配判断后缀
file_path.endswith(".txt") # 用于判断该文件的后缀拓展名，返回布尔值
os.path.splitext(path) #剪路径分割成2个参数,方便判断文件后缀，"c:\\text",".txt"
os.path.splitdrive(path) #将绝对路径按盘符分割成两个参数,"c:","\\text.txt"

os.path.join(png_path, png_file) # 将文件目录和文件名拼接在一起，得出一个文件路径参数
os.path.dirname(path) # 获取该文件的目录,不含文件名
os.path.split(path) # 获取该文件目录+文件名，分割为两个参数

os.remove(path) #删除指定文件, 需有删除权限,并文件无只读等属性,或用chdir(path)可以改变权限
os.rename("c:\\text1.txt","c:\\text2.txt") # 文件改名，改路径则为移动文件，若无文件/已存在则抛出异常，不可跨盘符
os.replace(old,new) #同上改名/移动，但目标存在则覆盖，不跨盘

os.path.isdir(path) # 判断path是否为文件夹
os.path.isfile(path) # 判断path是否为文件
os.exists("text.txt") # 判断具体路径  或文件是否存在，返回布尔值，填绝对/相对路径和文件名
os.listdir(path) # 返回path目录下的文件和列表，列表形式，填空则为当前目录

os.system("D:\PyCharm\music\yuri.wav") # 使用系统软件打开各种文件
os.system('D:/BBC-an-Zhuang/RA2/RUN.bat') # 打开BAT文件-注意反斜杠/除号
os.startfile(r"C:\install\文件.exe")  # 打开程序、.py和文件等，填入绝对路径，加r不用转义\
```
### 玩家输入=input('请输入...')

```python
玩家输入 = input('请输入...')
if 玩家输入 != '':
    break # 当玩家没有输入内容时，按了回车，则传进参数为空，实现任意按键结束
```
## Pyautogui库常用命令 [【链接】](https://blog.csdn.net/hange521/article/details/105184541/)，[【脚本之家文章链接】](https://www.jb51.net/article/183926.htm)
```python
# 基础命令
pyautogui.PAUSE=1 # pyautogui相关的命令延迟1秒，不建议使用
pyautogui.FAILSAFE=True # 启用防故障

pyautogui.onScreen(x, y) # 判断(x,y)是否在屏幕上，返回结果为布尔值，真假

width, height = pyautogui.size() # 屏幕的宽度和高度
print(width, height)
pyautogui.moveTo(width/2,height/2) # 移动鼠标至屏幕中间

```
- #### 鼠标命令：
```python
pyautogui.click() # .click鼠标单击 .doubleClick双击 .rightClick右击
pyautogui.click(x=100, y=200, duration=2)  # duration=2 移动周期2秒
pyautogui.doubleClick()  # 鼠标当前位置左击两下-双击
now_pos=pyautogui.position() # 获取记录鼠标当前位置

pyautogui.move(x,y) # 移动鼠标至相对坐标
yautogui.moveRel(100,50) # 相对移动

pyautogui.moveTo(x,y)  # 移动鼠标至绝对坐标
pyautogui.moveTo(x,y,duration=1)  # 移动鼠标过程中，周期为1秒
# 移动鼠标的命令都可以使用移动时间周期命令，模拟线性移动，非瞬间移动

pyautogui.mouseDown()
pyautogui.mouseUp()  # 【按下 / 松开】鼠标左键

```

- ### 键盘命令：
```python
pyautogui.typewrite('Hello world!') # 输入Hello world!字符串
pyautogui.typewrite('Hello world!', interval=0.1) #输入间隔x秒,限英文+符号,模拟键盘
pyautogui.press('enter') # 按下并松开，可设置多次和间隔，例("esc",5,0.2)按5次隔0.2
pyautogui.press(['left', 'left', 'left', 'left']) # 按下并松开（轻敲）四下左方向键

pyautogui.keyDown('shift') # 按下。这里可用于多键组合，或连续组合键
pyautogui.press('4')
pyautogui.keyUp('shift') # 抬起，组合键：输出 $ 符号的按键
pyautogui.hotkey('ctrl', 'v') # 组合按键（Ctrl+V）粘贴功能，按下并松开'ctrl'和'v'按键

```

- ### 找色

```python
变量名 = pyautogui.screenshot().getpixel((x,y)) # 传入坐标为元组
if 变量名 == (255,255,255): # 得到的RGB 颜色也是元组
    print("找到色了")

pyautogui.locateOnScreen('Part.png', region=(0, 0, 600, 800))  # region：缩小查找区域，可提升找图速度 (已忘记-待定)
```

- ### 弹窗
```python
pyautogui.alert(text='⚠️这是一段警告!!!!!!', title='alert 测试', button='OK')
pyautogui.confirm(text='窗口名', title='弹窗内容', buttons=range(10))
# ↑ 弹出一个带10个数字按钮窗口，可接受返回数值
```

### keyboard
[键盘监听等待按键](https://coco56.blog.csdn.net/article/details/107847467)  
[按键说明](https://blog.csdn.net/weixin_51802807/article/details/121179861)

```python
keyboard.type_string('Hello, World!')  #输入字符
keyboard.tap_key('H') 						# 点击H键
keyboard.tap_key('H', n=2, interval=5) 		# 点击H键2次，每次间隔5秒
keyboard.tap_key(keyboard.numpad_keys[5])   # 点击小键盘5
keyboard.tap_key(keyboard.function_keys[5]) # 点击功能键F5

keyboard.press_key(keyboard.alt_key)   # 按住Alt键
keyboard.tap_key(keyboard.tab_key) 	   # 点击Tab键
keyboard.release_key(keyboard.alt_key) # 松开Alt键，组合键同时按 Alt + Tab

```
#### 【其它键盘按键参考，小鹏同学】[公号链接](https://mp.weixin.qq.com/s/s2cDsD0f-orJpydYB_sHXg)

---
### pygame 键盘按键事件_ [参考链接](https://www.it610.com/article/1280841738579099648.htm)
```python
# 获取事件，比如按键等
for event in pygame.event.get():
    # 判断是否是点击了退出按钮
    if event.type == QUIT:
        print("exit")
        exit()
    # 判断是否是按下了键
    elif event.type == KEYDOWN:
        # 检测按键是否是a或者left
        if event.key == K_a or event.key == K_LEFT:
            print('left')
        # 检测按键是否是d或者right
        elif event.key == K_d or event.key == K_RIGHT:
            print('right')
        # 检测按键是否是w或者up
        elif event.key == K_w or event.key == K_UP:
            print("up")
        # 检测按键是否是s或者down
        elif event.key == K_s or event.key == K_DOWN:
            print("down")
        # 检测按键是否是空格键
        elif event.key == K_SPACE:
            print('space')
```






```python

```


```python

```


```python

```




