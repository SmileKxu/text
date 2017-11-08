### Ubuntu 16.04 安装QQ国际版

QQ国际版下载地址:[http://pan.baidu.com/s/1jIwKdXs](http://pan.baidu.com/s/1jIwKdXs) 

### 安装过程

1. 安装依赖库
在终端输入
```
sudo apt-get install  libgtk2.0-0:i386
```
另外，如果是64位系统还要安装ia32-libs，但是Ubuntu 16.04 中该软件包已经被其他版本替代，所以这里我们选择安装lib32ncurses5.

因此在终端输入
```
sudo apt-get install lib32ncurses5
```
2. 解压并安装 wineqqintl

将 wineqqintl 下载下来后，找到下载位置，然后将 Zip 中的档案提取出来，可以得到三个 .deb 压缩包，然后分别解压
```
sudo dpkg -i wine-qqintl_0.1.3-2_i386.deb
```
安装 wine-qqintl_0.1.3-2_i386.deb包。如果还有 lib 没有配置，在安装中发生错误，那么配置一下依赖环境
```
sudo apt-get install -f
```
然后重新输入 ```sudo dpkg -i wine-qqintl_0.1.3-2_i386.deb```就可以正常安装了。

之后在继续解压第二个
```
sudo dpkg -i ttf-wqy-microhei_0.2.0-beta-2_all.deb
```
和
```
sudo dpkg -i fonts-wqy-microhei_0.2.0-beta-2_all.deb
```
将剩余的两个deb包安装。

3. 运行 wineqqIntl 

为检测wineqqIntl已正常安装，我们可以输入```sudo dpkg -l|grep qq``` 然后就会显示所有的qq安装版本

最后找到 qq 路径，wineqqIntl默认安装路径为/usr/share/applications/ 当中，当然你也可以输入
```
sudo find / -name qq*
```
命令在终端中查找qq的有关安装信息。或者在搜索中找到qq图标启动就可以了。
