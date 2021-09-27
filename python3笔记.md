# Python3 学习笔记
## 建立数据库连接
``` python
mydb = mysql.connector.connect(
    host="localhost",
    user="root",
    passwd="hushiqi"
)
```
## pip 使用
### 安装pip
```sh
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py   # 下载安装脚本
sudo python get-pip.py    # 运行安装脚本
```
### 显示pip版本和路径
```sh
pip --version
```
### 获取帮助
```sh
pip --help
```
### 升级pip
```sh
pip install -U pip
```
### 安装包
```sh
pip install SomePackage              # 最新版本
pip install SomePackage==1.0.4       # 指定版本
pip install "SomePackage>=1.0.4"    # 最小版本
```
### 升级包（指定版本方法同上）
```sh
pip install --upgrade SomePackage
```
### 卸载包
```sh
pip uninstall SomePackage
```
### 显示安装包信息
```sh
pip show SomePackage
```
### 列出已安装的包
```sh
pip list
```
### 显示可以升级的包
```sh
pip list -o
```
## virtualenv 使用
### 通过pip安装virtualenv：
```sh
pip install virtualenv
```
### 查看virtualenv版本（测试安装是否成功）：
```sh
virtualenv --version
```
### 在当前目录下搭建一个虚拟环境：
```sh
virtualenv my_project_env(环境名)
```
### 激活当前目录下虚拟环境：
```sh
my_project_env/bin/activate # windows
source my_project_env/bin/activate
```
### 停用当前虚拟环境：
```sh
deactivate
```