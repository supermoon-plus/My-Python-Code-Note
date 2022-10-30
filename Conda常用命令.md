




### Conda第三方库命令 / [CSDN 文章](http://t.csdn.cn/BgOeO)
```python
conda install xxx
#安装第三方库，（在当前环境下）conda install xxx=2.1 #可指定版本号

pip install -r requirements.txt
# 在某个目录下，执行安装，用CD C:\ 命令进入目录

conda install xxx -i 源名称或链接 # 指定下载源
conda install opencv-python -i http://pypi.douban.com/simple --trusted-host pypi.douban.com

conda uninstall xxx
# 卸载第三方库

conda list # 查看当前环境中，第三方库列表

```


### conda环境篇
```python
conda activate python38
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple

conda activate python38
#激活 / 进入到 python38 这个虚拟环境

conda create -n python38 python==3.8.5
#创建叫python38的环境

conda remove -n python38 --all
#删除叫python38的环境

python --version
# 查看当前环境的python版本

conda env list
# 虚拟环境列表，总共创建了哪些虚拟环境

nvidia-smi # 查看显卡驱动版本

```

### 注意事项：
- Conda需要提前设置好国内下载源 [CSDN Link](http://t.csdn.cn/HqvHh)
- WARNING:Ignore 报错时，修改系统默认UTF-8编码 [CSND Link](http://t.csdn.cn/Qkv0c)
- 




---

#### 【旧版】为大家整理了一些常用的conda命令：  [Bili Video](https://www.bilibili.com/video/BV1PT4y1i7qt)
```python
1. conda --version #查看conda版本，验证是否安装
2. conda update conda #更新至最新版本，也会更新其它相关包
3. conda update --all #更新所有包
4. conda update package_name #更新指定的包
conda env list # 查看当前存在哪些虚拟环境

5. conda create -n env_name package_name
#创建名为env_name的新环境，并在该环境下安装名为package_name 的包，
#可以指定新环境的版本号，
#例如：conda create -n python2 python=python2.7 numpy pandas，
#创建了python2环境，python版本为2.7，同时还安装了numpy pandas包

6. source activate env_name #切换至env_name环境
7. source deactivate #退出环境
8. conda info -e #显示所有已经创建的环境
9. conda create --name new_env_name --clone old_env_name 
#复制old_env_name为new_env_name
10. conda remove --name env_name –all #删除环境
11. conda list #查看所有已经安装的包

13. conda install --name env_name package_name #在指定环境中安装包
14. conda remove -- name env_name package #删除指定环境中的包
15. conda remove package #删除当前环境中的包
16. conda env remove -n env_name #采用第10条的方法删除环境失败时，可采用这种方法
```






