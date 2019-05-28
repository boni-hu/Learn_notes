# Python的包管理工具: `pip`

由于python是模块化的开发，因此能够能够利用其他人写的现成的包来快速的完成特定的任务。为了加快包的安装，python有很多包管理的工具,比如easy_install、setuptools和distribute，其中`pip`是目前使用最多的包管理工具。

## 1. 安装pip
在ubuntu系统可以直接安装python-pip

```
# Python 3的pip （建议安装Python3）
sudo apt-get install python3-pip

# Python 2的pip
sudo apt-get install python3-pip
```

Upgrade pip
```
sudo pip3 install --upgrade pip
```

安装之后，可以输入`pip`查看简要的使用说明。**需要注意的是，通过系统安装的pip，在使用pip安装包的时候，需要用sudo来执行。**


## 2. pip的命令

### 2.1 查找一个给定名字的package
```
pip search numpy
```
会找到很多跟numpy有关联的包，可以拷贝每一行最前面的那个包名字，通过安装命令去安装。


### 2.2 安装一个给定的package
```
$ pip install numpy
```
安装`numpy`这个包，同时它的依赖也自动安装到系统。

使用一个给定的URL安装包
```
$ pip -f URL install PACKAGE    # 从指定URL下载安装包
```


### 2.3 升级一个包
```
$ pip -U install PACKAGE        # 升级包
```

### 2.4 列出当前系统中已经安装的包
```
$ pip list
```

查看一个安装好的包的信息
```
$ pip show numpy
```


## 3. 设置pip的镜像
但是由于直接使用pip去访问国外的网站慢，所以需要设置好pip的镜像，从而加快包的安装。目前国内有很多pip包镜像，选择其中一个就可以加快很多安装速度

```
pip config set global.index-url 'https://mirrors.ustc.edu.cn/pypi/web/simple'
```

## 4. 查看更换pip版本
因为python2和python3版本不兼容的原因，所以很多系统上避免不了转python2 和python3。 pip 有时候指向pip2；有时候指向pip3。在我的电脑上，pip和pip3 都指向了python3.。为了让pip指向python2， pip3 指向python3.需要做一些简单的修改：

命令如下：which pip

一般情况下会显示：

```/usr/local/bin/pip```

然后 ```vim /usr/local/bin/pip```

我们可以看到如下：

```
#!/usr/bin/python3
# -*- coding: utf-8 -*-
import re
import sys

from pip import main

if __name__ == '__main__':
    sys.argv[0] = re.sub(r'(-script\.pyw|\.exe)?$', '', sys.argv[0])
    sys.exit(main())
```
将第一行``` #!/usr/bin/python3 ```修改为

```#!/usr/bin/python2```
然后`Esc`退出编辑模式 `Shift`+`ZZ`保存

然后pip 就指向pip2 也就是python2了
