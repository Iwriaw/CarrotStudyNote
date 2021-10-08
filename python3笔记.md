# Python3 学习笔记
## python基础
### with as语句
## mysql-connector使用
### 导入包
```python
import mysql.connection
```
### 建立数据库连接
``` python
mydb = mysql.connector.connect(
    host="localhost",
    user="root",
    passwd="hushiqi"
)
```
### 选择数据库建立连接
```python
mydb = mysql.connector.connect(
    host="localhost",
    user="root",
    passwd="hushiqi",
    database="carrot_db"
)
```
### 执行sql语句
```python
mydb = mysql.connector.connect(
    host="localhost",
    user="root",
    passwd="hushiqi"
)
mycsr = mydb.cursor()
mycsr.execute("SHOW DATABASES")
mycsr.commit()#如果执行对表内容修改的语句，需要commit才能在数据库生效
```
### 带参数的execute()防止sql注入
```python
mydb = mysql.connector.connect(
    host="localhost",
    user="root",
    passwd="hushiqi"
    database="carrot_db"
)
mycsr = mydb.cursor()
#传入可迭代数据结构
mycsr.execute("SELECT * FROM user WHERE name=%s", ["carrot"])
```
### executemany()批量执行sql语句
```python
mydb = mysql.connector.connect(
  host="localhost",
  user="root",
  passwd="hushiqi",
  database="carrot_db"
)
mycsr = mydb.cursor()
sql = "INSERT INTO users (name, age) VALUES (%s, %s)"
val = [
    ("hushiqi", 21),
    ("honglongyu", 21),
    ("huyue", 22)
]
mycsr.executemany(sql, val)
mydb.commit()    # 数据表内容有更新，必须使用到该语句
```

### 执行完sql语句后后应关闭游标
```
mycsr.close()
```
### 连接用完后应关闭连接
```pyhton
mydb.close()
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
### 根据requirements.txt安装包
```sh
pip install -r requirements.txt
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