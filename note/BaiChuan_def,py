'''

【测试demo-找图找色的def】
mode定义 默认为1=点击 2=双击 3=右击  4=鼠标移动到  0=不做任何操作

找图示例： # 传入图片绝对路径、mode模式、相似度  mode模式 1=点击 2=双击 3=右击  4=鼠标移动到 0=不执行
zhaotu("D:\PyCharm\image\image.png",1,0.8)

找色示例： # 颜色传入的是(元组)的形式,如：(255,255,255)，mode 1=点击 2=双击 3=右击  4=鼠标移动到 0=不执行
zhaose(100,100,(255,255,255),1)

这篇脚本方法的部分逻辑由GitHub copilot生成, 这效果实在是把我震撼到了！！


---------------------------------------
【百百川创建的函数列表：】


yanci(time_sleep) # 延迟函数

# 文件夹处理函数 2022年6月25日, 在写完红警YOLO后, 总结的一部分常用函数
if_file_suffix(path, suffix)                # 判断文件路径的后缀,符合则True,否则False. ("c:\123.txt", ".txt")=True
path_and_name_to_file_path(path, file_name) # 将路径和文件名 组合为文件路径, ("c:\aaa", "123.txt" to "c:\aaa\123.txt")
path_to_filename(path)                      # 将路径转换为文件名,"c:\123.txt" to "123"
path_to_file(path)                          # 将路径 to name.txt 转换为文件+后缀, "c:\123.txt" to "123.txt"
file_path_to_path(path)                     # 将文件路径to path 换为路径目录，不带文件名+后缀，"c:\aaa\123.txt" to "c:\aaa"
if_dir(path)                                # 判断path是否为文件夹, "c:\aaa"=True, "c:\123.txt"=False
if_file(path)                               # 判断path是否为文件夹, "c:\aaa.txt"=True, "c:\123"=False
if_path(path)                               # 判断路径是否存在，不存在则创建
path_to_suffix(path)                        # 将文件路径 to .txt 转换为后缀, "c:\123.txt" to ".txt"

path_to_filename_list(path, notdir=False)   # 传path+是否没有文件夹,传真假,默认False,遍历path下所有文件+文件夹返回list "c:\path"to" [c:\path\11.txt, c:\path\22.txt, ...] "
path_file_to_list(path) # 改名，改成上面的 ↑

# 找图/找色 函数
zhaotu(path, mode, 0.8, xx, yy) # 按键精灵找图, 传入图片绝对路径、mode模式、相似度、偏移量....【除了路径, 其他参数都可以不传】
zhaose(x, y, colour, mode=1, xx=0, yy=0) # 参数为坐标x y、(颜色RGB)、mode模式、偏移量. 【除了路径+颜色, 其他参数都可以不传】
zhaose(500, 330, (255, 255, 255), 1, 0, 0) # 找图示例
# mode模式 1=点击 2=双击 3=右击  4=鼠标移动到 0=不执行

run()   # 传入state="exit"则exit结束脚本，2可以传入str结束原因print。
        # 判断鼠标是否在屏幕↖ ↗角落，是则False，正常则True，便于控制脚本执行与停止。

zhaotu(path, mode=1, confidence=0.8, xx=0, yy=0) # 传入图片非中文绝对路径path, mode模式, 相似度, 点击偏移量(可填负数)
例如: zhaotu('c:\\PyCharm\\1.png', 1, 0.8, xx=50, yy=-10)

zhaose(x, y, colour, mode=1, xx=0, yy=0)    # 参数为坐标x y、(颜色)、mode模式、点击偏移量(可填负数)
例如: zhaose(960, 540, (255,255,255), 1, xx=50, yy=-10)


更新：
2022年11月13日 更新优化了大量细节和注释说明。

---------------------------------------

'''

import pyautogui
import time
import os


# for a,b,c in os.walk(path):
#     print("绝对路径=",a)
#     print("相对路径=",b)
#     print("文件名=",c)

def yanci(time): # 延迟函数, yanci(0.5)
    time.sleep(time)

def if_file_suffix(path, suffix): # 判断文件路径的后缀,符合则True,否则False. ("c:\123.txt", ".txt")=True
    return path.endswith(suffix)

def path_and_name_to_file_path(path, file_name): # 将路径和文件名 组合为文件路径, ("c:\aaa", "123.txt" to "c:\aaa\123.txt")
    return os.path.join(path, file_name)

def path_to_filename(path): # 将路径转换为文件名,"c:\123.txt" to "123"
    return os.path.split(path)[1].split(".")[0]

def path_to_file(path): # 将路径 to name.txt 转换为文件+后缀, "c:\123.txt" to "123.txt"
    return os.path.split(path)[1]

def file_path_to_path(path): # 将文件路径to path 换为路径目录，不带文件名+后缀，"c:\aaa\123.txt" to "c:\aaa"
    return os.path.split(path)[0]

def path_to_suffix(path): # 将文件路径 to .txt 转换为后缀, "c:\123.txt" to ".txt"
    return os.path.splitext(path)[1]

def if_dir(path): # 判断path是否为文件夹, "c:\aaa"=True, "c:\123.txt"=False
    return os.path.isdir(path)

def if_file(path): # 判断path是否为文件夹, "c:\aaa.txt"=True, "c:\123"=False
    return os.path.isfile(path)

def if_path(path): # 判断路径是否存在，不存在则创建
    path = path.strip() # 去除多余空格
    path = path.rstrip("\\") # 去除多余的//
    if not os.path.exists(path):
        os.makedirs(path)
        print("已成功创建文件夹：", path)
        return True
    else:
        print("该文件夹已存在，跳过。")
        return False

def path_to_filename_list(path, notdir=False): # 传path+是否没有文件夹,传真假,默认False,遍历path下所有文件+文件夹返回list "c:\path"to" [c:\path\11.txt, c:\path\22.txt, ...] "
    def_files_list = []
    for file_name_list in os.listdir(path): # 不知道下级文件夹内的文件会不会加进来，待测试
        if notdir and if_dir(path):
            continue
        def_files_list.append(os.path.join(path, file_name_list))
        # print(file_name_list)
    return def_files_list


# a = "D:\\PyCharm\\image"
# b = if_dir(a)
# print(b)

def zhaotu(path, mode=1, confidence=0.8, xx=0, yy=0): # 传入图片非中文绝对路径path, mode模式, 相似度, 点击偏移量(可填负数)
    # 例如: zhaotu('c:\\PyCharm\\1.png', 1, 0.8, xx=50, yy=-10)
    image_run = pyautogui.locateOnScreen(path, confidence=confidence)
    if image_run is not None: # 判断查找后的值是否 不是空的
        x, y = pyautogui.center(image_run) # 将图片的坐标赋值
        print("√ 找到图片，坐标为：", x, y)
        x = x + xx # 偏移量重新赋值
        y = y + yy
        if mode == 1:
            pyautogui.click(x,y) # 点击该坐标
            print("点击坐标")
        elif mode == 2:
            pyautogui.doubleClick(x,y) # 双击该坐标
            print("双击坐标")
        elif mode == 3:
            pyautogui.rightClick(x,y) # 右击该坐标
            print("右击坐标")
        elif mode == 4:
            pyautogui.moveTo(x,y) # 鼠标移动到该坐标
            print("鼠标移动到坐标")
        elif mode == 0: # 0 无动作
            pass
        else:
            print("mode模式0-4填写错误,已忽略本次操作")
        # pyautogui.leftClick(x, y) # 点击该坐标
    else:
        print("X 本次找图: 没有找到图片，请检查路径、图片、屏幕显示等等")
        return False
    return True

def zhaose(x, y, colour, mode=1, xx=0, yy=0): # 参数为坐标x y、(颜色)、mode模式、点击偏移量(可填负数)
    # 例如: zhaose(960, 540, (255,255,255), 1, xx=50, yy=-10)
    run = pyautogui.screenshot().getpixel((x, y))  # 根据坐标取色，注意：坐标+颜色均为(元组)的形式传入
    x = x + xx
    y = y + yy
    if run == (colour):
        print('√ 找到颜色')
        if mode == 1:
            pyautogui.click(x, y)
            print("点击坐标")
        elif mode == 2:
            pyautogui.doubleClick(x, y)
            print("双击坐标")
        elif mode == 3:
            pyautogui.rightClick(x, y)
            print("右击坐标")
        elif mode == 4:
            pyautogui.moveTo(x, y)
            print("鼠标移动到坐标")
        elif mode == 0:
            pass
        else:
            print("mode模式0-4填写错误,已忽略本次操作")
    else:
        print('X 找不到颜色')
        return False
    return True

# def run(): # 当鼠标处于右上角时，return false 脚本关闭(第一版)
#     now_x, now_y = pyautogui.position()  # 获取记录鼠标当前位置
#     if now_x == 0 and now_y == 0: # 判断坐标
#         print("当前鼠标处于左上角0, 0  触发脚本关闭")
#         return False
#     elif now_x == 2559 and now_y == 0:
#         print("当前鼠标处于右上角1920, 0   触发脚本关闭")
#         return False
#     return True

# def run(mode1=1, mode2=2): # 判断鼠标是否在屏幕↖ ↗角落，返回布尔值，便于控制脚本执行与停止。(初版写法，搞复杂了)
#     width1, height1 = pyautogui.size() # 获取当前屏幕分辨率, 这句最好是写在脚本开头，避免无意义的反复、重复获取。
#     new_x, new_y = pyautogui.position() # 记录此时此刻的鼠标坐标
#     if mode1 == 1 :
#         if new_x <= 20 and new_y <= 20:
#             print("=== 当前鼠标在屏幕左上角，已发出停止信号。当前鼠标坐标：", new_x, new_y )
#             return False
#     if mode2 == 2 :
#         if new_x >= width1 - 20 and new_y <= 20:
#             print("=== 当前鼠标在屏幕右上角，已发出停止信号。当前鼠标坐标：", new_x, new_y)
#             return False
#     print(new_x, new_y)
#     return True
#     # exit() # 结束停止整个脚本

def run(state = '', yuanyin = ""): # 传入state="exit"则exit结束脚本，2可以传入str结束原因print。
    # 判断鼠标是否在屏幕↖ ↗角落，是则False，正常则True，便于控制脚本执行与停止。
    width1, height1 = pyautogui.size() # 获取当前屏幕分辨率, 这句最好是写在脚本开头，避免无意义的反复、重复获取。
    new_x, new_y = pyautogui.position() # 记录此时此刻的鼠标坐标
    if new_x <= 20 and new_y <= 20 or new_x >= width1 - 20 and new_y <= 20:
        print("=== 当前鼠标在屏幕左上角or右上角，已发出停止信号。当前鼠标坐标：", new_x, new_y )
        if state == 'exit': # 判断是否要退出程序
            print("=" * 20)
            for _ in range(3):
                for _ in range(2):
                    print("="*20,"检测到结束条件，【", yuanyin, "】程序正在退出！","="*20)
                print("=" * 20)
            time.sleep(4)
            exit() # 结束停止整个脚本
        return False
    return True



# while not zhaotu("D:\PyCharm\image\liulanqi_off.png",0,0.8):

# if zhaotu("D:\PyCharm\image\liulanqi_off.png",0,0.8):
#     print("找到图片")
# else:
#     print("找不到图片")




