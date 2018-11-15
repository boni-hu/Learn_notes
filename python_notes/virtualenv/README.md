## ubuntu 下python 虚拟环境的安装和使用

### 安装

```python
sudo apt install python-virtualenv
sudo easy_install virtualenvwarpper
```

或者使用pip 安装

```
sudo pip install virtualenv
sudo pip install virtualenvwrapper
```

### 创建虚拟环境

```
mkvirtualenv 虚拟环境名称
mkvirtualenv -p python路径 虚拟环境名称 # 创建指定python版本的虚拟环境
whereis python3 # 寻找python的安装路径
eg. mkvirtualenv -p /usr/bin/python3 mywork
```

### 虚拟环境的查看和使用

```
workon+两次Tab键  # 提示所有的虚拟环境
pip list  # 查看虚拟环境中安装的python包
pip freeze # 同上
deactivate # 退出虚拟环境
rmvirtualenv 虚拟环境名称 # 删除虚拟环境
```

### 在虚拟环境下安装python包

```
pip install 包的名字
```

**注意：一定不要sudo pip ...，这里是在虚拟环境中安装python包，如果使用了sudo权限，python包会被安装在主机非虚拟环境下，在虚拟环境中找不到这个包**



