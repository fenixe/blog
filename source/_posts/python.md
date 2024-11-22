---
title: python
date: 2022-11-22 22:01:02
tags:
---

# Base
## 查看系统版本
python -c "import platform;print(platform.architecture()[0]);print(platform.machine())"

## 在线
colab.research.google.com

## CLI
pip install aliyun-python-sdk-core==2.13.3
pip uninstall aliyun-python-sdk-core

pip升级包命令：pip install --upgrade packagename
pip检测更新命令：pip list –outdated

pip --version
pip install --upgrade pip

更新 pip：pip install --upgrade pip

安装了那些包
pip list

设置清华源：https://mirrors.tuna.tsinghua.edu.cn/help/pypi/
pip install fastapi i https://mirrors.tuna.tsinghua.edu.cn/help/pypi/

pip install -i https://pypi.tuna.tsinghua.edu.cn/simple --trusted-host pypi.tuna.tsinghua.edu.cn selenium

安装文件内第三方库
pip install --no-cache-dir -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple

阿里云源：https://mirrors.aliyun.com/pypi/simple

## 安装
python.org download

python3 -V
pip3 -V

## 包管理
https://pypi.org/
### 查看安装的包
pip show pandas

## 卸载
删除Python 3.7 框架，打开终端，输入
sudo rm -rf /Library/Frameworks/Python.framework/Versions/3.7

删除 Python 3.7 应用目录
cd /Applications
sudo rm -rf Python 3.7

删除/usr/local/bin 目录下指向的Python3.7 的连接
cd /usr/local/bin/

ls -l /usr/local/bin

rm Python3.7相关的文件和链接

#Python3.7相关的文件和链接需要自行确认是否删除

5. 删除 Python 的环境路径

vi ~/.bash_profile

6. 确认python 是否已经删除

python3.7

-bash: python3.7: command not found

## 查看当前环境安装了哪些py程序包
pip freeze

将这个命令的输出保存到文件中，以备将来需要安装相同版本的包时使用。例如，您可以运行以下命令来将输出保存到名为 requirements.txt 的文件中：
pip freeze > requirements.txt

## requirements.txt 管理套件相依性
### 安装
```zsh
$ pip install -r requirements.txt
```

## 目录中安装环境
electron中使用
https://pyloong.github.io/pythonic-project-guidelines/introduction/install/#112-python
https://www.python.org/downloads/release/python-3915/
XZ 文件

## pyenv
Python版本管理

### 安装pyenv
```zsh
brew install pyenv 
# 或
git clone https://github.com/pyenv/pyenv.git ~/.pyenv


echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n eval "$(pyenv init -)"\nfi' >> ~/.zshrc
```

echo 命令的含义是：将引号中内容写入某文件中
请注意，以上的三条 echo 命令的最后一条长长的命令，请你保证它引号中的内容处于 ~/.bashrc 或者 ~/.zshrc 的最底部。
因为在 pyenv 初始化期间会操作 path 环境变量，导致不可预测的行为。

### 卸载pyenv
如果是手动安装的
rm -rf ~/.pyenv
vim .zshrc 删除pyenv配置

### CLI
``` zsh
# 查看当前版本
pyenv version

# 查看所有版本
pyenv versions

# 查看所有可安装的版本
pyenv install --list

# 安装指定版本
pyenv install 3.6.5
# 安装新版本后rehash一下
pyenv rehash

# 删除指定版本
pyenv uninstall 3.5.2

# 指定全局版本
pyenv global 3.6.5

# 指定多个全局版本, 3版本优先
pyenv global 3.6.5 2.7.14

# 实际上当你切换版本后, 相应的pip和包仓库都是会自动切换过去的
```

### install 太慢问题
进入源码页面下载`.tar.xz`文件，https://www.python.org/downloads/source/

将下载的 Python 版本压缩包放到 pyenv 的缓存文件夹: `~/.pyenv/cache`

执行安装命令
```zsh
$ pyenv install 3.9.15
python-build: use openssl@1.1 from homebrew
Downloading readline-8.1.tar.gz...
-> https://ftpmirror.gnu.org/readline/readline-8.1.tar.gz
Installing readline-8.1...
Installed readline-8.1 to /Users/qkil/.pyenv/versions/3.9.15

Installing Python-3.9.15...
python-build: use zlib from xcode sdk
WARNING: The Python lzma extension was not compiled. Missing the lzma lib?
Installed Python-3.9.15 to /Users/qkil/.pyenv/versions/3.9.15
```

## 语言
- 高级编程语言
- 解释型语言（翻译）
  C：编译型语言，执行前先编译，再汇编，再链接，更接近机器执行的代码。比python速度更快，执行效率更高
- 语法和自然语言很像

## 运行特定版本
```zsh
python3.9 -V
python3.10 -V

# 查看python3 多少位
$ python3
Python 3.11.0 (v3.11.0:deaf509e8f, Oct 24 2022, 14:43:23) [Clang 13.0.0 (clang-1300.0.29.30)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import platform
>>> platform.architecture()
('64bit', '')
>>>
```

## 交互式运行
```
$ python3 -i 2.py
Hello world!
>>> print('h')
h

非交互式运行
$ python3 -i 2.py
Hello world!
```

# 创建项目
- 创建项目目录
- 创建虚拟环境
  python -m venv venv
- 激活虚拟环境
  source venv/bin/activate
- 创建 requirements.txt 文件
  pip freeze > requirements.txt
- 创建主程序文件，main.py
- 编写代码，Hello World; print("Hello, World!")
- 运行项目
  python main.py

- 增加服务
```py
from fastapi import FastAPI
import uvicorn

app = FastAPI()

@app.get("/")
def read_root():
  return {"Hello": "World"}

if __name__ == '__main__':
    uvicorn.run(app='main:app', host="0.0.0.0", port=8080, reload=True)
```

安装服务包
pip install uvicorn

- 启一个服务，
  uvicorn main:app --reload

linux:
uvicorn main:app --host '0.0.0.0' --port 8000 --reload

## 添加服务
- pip install fastapi

## 连接mysql数据库
pip install pymysql
同步数据库驱动，会阻塞执行它的线程直到查询完成并且结果返回。
```py
if __name__ == '__main__':
 # 连接到 MySQL 数据库
    connect = pymysql.connect(user='dev', password='xx',
                                    host='xx',
                                    database='niekaifa')
    cursor = connect.cursor()

    # 执行 SQL 查询语句
    sql = "SELECT * FROM t_convert"
    cursor.execute(sql)

    # 获取所有结果
    results = cursor.fetchall()
    columns = [column[0] for column in cursor.description] # 获取列名
    row_dict = [dict(zip(columns, row)) for row in results]
    print(row_dict)

    # 关闭游标和数据库连接
    cursor.close()
    connect.close()
```

### 动态sql的拼接
#### 合法
参数化查询
```py
sql = "SELECT vip, coin FROM user_asset WHERE uid=%s "
# 可以使用数组和元组的方式传递参数
cursor.execute(sql, [uid])
```

#### 非合法
会有sql注入风险

``` py
# 1、%s占位符形式
sql = "SELECT vip, coin FROM user_asset WHERE uid='%s' " % uid

# 2、format形式
sql = "SELECT vip, coin FROM user_asset WHERE uid='{}' ".format(uid)

# 3、f string形式
sql = f"SELECT vip, coin FROM user_asset WHERE uid='{uid}' "

In [62]: uid = "'; delete FROM test_user_asset WHERE ''='"
In [63]:  "SELECT vip, coin FROM user_asset WHERE uid='%s' " % uid
Out[63]: "SELECT vip, coin FROM user_asset WHERE uid=''; delete FROM test_user_asset WHERE ''='' " # 极端恶意！删除全表记录
```

### 逻辑控制内容插入字符串
```py
if receive_status == 1:
    update_receive_sql += ",result_file = %s"
    receive_sql_params.append(json_file_name)
```

### 插入和更新
```py
cursor.execute(process_sql, [a])
# 更改提交到数据库
cnx.commit()
# 相应数量的行被更新
process_ret = cursor.rowcount
```

### excel文件导入数据库
7010条 3分钟
```py
@router.get("/test")
async def test():
    print("test ......")
    local_excel_dir = "./src/output/oss_files/store_data_copy.xlsx"
    cursor = None
    try:
        cursor = cnx.cursor()
        df = pd.read_excel(local_excel_dir)
        combined = {'省份':'province', '城市':'city', '名称':'name', '地址':'address', 'X,Y':'xy'}
        df.rename(columns=combined, inplace=True)

        # 检查'name'列是否有重复的记录
        duplicate_rows = df[df.duplicated('name', keep=False)]
        if not duplicate_rows.empty:
            print('duplicate_rows', duplicate_rows)
            return

        # 空值处理
        df = df.where(df.notnull(), '')

        insert_query = "insert into store(name,address,province,city,xy) values (%s,%s,%s,%s,%s)"
        for index, row in df.iterrows():
            cursor.execute(insert_query, (row['name'],row['address'],row['province'],row['city'],row['xy']))
        # 提交事务
        cnx.commit()
        store_ret = cursor.rowcount
        print(store_ret)
        return return_vo(store_ret)
    except Exception as e:
        logger.error(f"创建store失败: {e}")
        cnx.rollback()
        return return_error("创建store异常")
    finally:
        if cursor:
            cursor.close()
```

### excel更新
```py
update_sql = "update store set keyword=%s where name=%s"
for index, row in df.iterrows():
    # 判断是否为非空值
    if pd.notnull(row['keyword']):
        cursor.execute(update_sql, (row['keyword'],row['name']))
```


## gitignore
```
**/.DS_Store
# Ignore compiled Python files
*.pyc
__pycache__/

# Ignore the virtual environment folder
venv/

# Ignore local configuration files
*.env

# Ignore logs
*.log
logs/

# Ignore package build and distribution files
build/
dist/
*.egg-info/

# Ignore cache and temporary files
*.pyc
*.pyo
*.pyd
*.so
*.swp
*.cache
*.coverage
.coverage
nosetests.xml
coverage.xml
htmlcov/

# Ignore Jupyter Notebook checkpoints
.ipynb_checkpoints/
*.ipynb_checkpoints

# Ignore database files
*.db
*.sqlite3

# Ignore macOS metadata files
.DS_Store

# Ignore Windows Thumbs.db files
Thumbs.db
```

# windows安装
下载
https://www.python.org/downloads/windows/
安装
https://zhuanlan.zhihu.com/p/111168324

PowerShell 激活虚拟环境
PowerShell默认可能不允许执行外部脚本
查看当前策略：Get-ExecutionPolicy
如果返回 Restricted 或 AllSigned，你需要将其更改为 RemoteSigned 或 Unrestricted（请注意这可能对系统安全有影响）。以管理员权限开启 PowerShell，并执行：
Set-ExecutionPolicy RemoteSigned

然后：
C:\path\to\env\Scripts\ activate 

## 激活虚拟环境
``` bash
# powerShell
$ venv\Scripts\Activate.ps1

# git bash
$ source venv/Scripts/activate
```

# 语法
## 目录
```py
# 程序运行时所在的目录
import os
# 获取当前工作目录
current_dir = os.getcwd()
# 打印当前工作目录
print(current_dir)


# 获取当前工作目录
current_dir = os.path.dirname(os.path.abspath(__file__))

# 打印当前工作目录
print(current_dir)
```
## 输入输出
``` py
var=input()
print(var)
```

## 类型
- 整数 int 8
- 浮点数 float 8.8
- 字符串 str '8'
- 布尔值 bool True,False

### 判断类型
type(8)
type('8')
type("8")
type(True)

### 类型转换
int('8')
str(123)
bool(123) //非0返回True

## 注释
```py
# 首先第一行写程序用来做什么的
```

## int
n += 1
number = None  # 在if逻辑之外预先定义变量，并给予一个初始值

## 字符串
### 长度
len(str)
### 取值
单个：str[0]
多个：str[0:4] /不包含4
后面：str[-1]

### 判断是否在字符串中
'1' in '123'
'0' not in '123'

```py
# 使用Python字符串方法检查keyword是否在name中，并且确保keyword不为空字符串
if keyword and keyword in name:
    print(f"Keyword '{keyword}' is found in name '{name}'.")
```

### 分割
data.split('|')

### 去除
line.strip('\n')

### 元组
存储内容，不可变更
（1, 10) > (2, 20)
看成：110 > 220

```py
a=(1,3,5,7)
b=4
list filter(lambda x: x < b, a) #取出a中小于4的元素
```

### 字符串模版
'%s 年的生肖是 %s' %(year, s)

### 字符串替换
```py
my_string = 'abc;def;g'
new_string = my_string.replace(';', '*;')
```

## 数组
```py
list = []
list.append('X') #新增
list.remove('X') #删除

# 3.9
rm_file(files: list[str]):

# typing模块
from typing import List
def rm_file(files: List[str]):

# 长度
len(arr)

# 合并
list1 = [1, 2, 3]
list2 = [4, 5, 6]
combined_list = list1 + list2
``` 

### 判断一个数组为空
```py
# 定义一个空数组
arr = []

# 使用布尔运算符检查数组是否为空
if not arr:
    print("数组为空")
else:
    print("数组不为空")
```

### 转字符串
my_string = ','.join(my_list)

## 字典
字典是一种内置的数据类型，用于存储键值对（key-value pairs）。每个键（key）与一个值（value）相关联，你可以通过键来访问对应的值。字典在其他编程语言中可能被称为map、hashmaps或associative arrays。
字典的每个键必须是唯一的，即不能有两个相同的键存在于同一个字典中。而值则可以重复，不同的键可以关联到相同的值。


## Object
### JSON字符串
json_string = json.dumps(data)

## 逻辑判断
### 条件语句
``` py
x = 'abcd'
if x == 'abc' :
  print('相等')
elif x == 'xyz':
  print('xyz')
else:
  print('都不相等')

# if not语句用于检查一个条件是否为False。它可以是直接的布尔值True或False，也可以是任何Python数据类型。因为Python中的值都有一个隐含的布尔值，称为其"Truthiness"。
# 1、布尔值False本身
flag = False
if not flag:
    print("Flag is false")
# 2、数值0（包括整数0、浮点数0.0，以及其他数值类型的0，如0j）
num = 0
if not num:
    print("Number is zero")
# 3、空序列和集合，包括""(空字符串), [](空列表), ()(空元组), {}(空字典), set()(空集合)
lst = []
if not lst:
    print("List is empty")
# 4、None，Python中的“空”或“无”的指示符:
nothing = None
if not nothing:
    print("Nothing is None")

# 是否有值，是否等于某值
# 使用.get()方法，它在尝试访问一个可能不存在的键时不会抛出异常
if biz_res and biz_res.get("code") == 200:
    print("biz_res['code'] is 200.")
else:
    print("biz_res has no value or biz_res['code'] is not 200.")


# 判断为False情况返回
def check_oss_exist(oss_exist):
    if not oss_exist:
        # 当 oss_exist 为 False 时，执行以下语句
        return "oss_exist is False, returning..."  
    # 当 oss_exist 为 True 时，继续执行函数的其他部分
    return "oss_exist is True, continued processing..."

# 判断文件不存在
if not os.path.isfile(file_path):
    print('文件不存在')
# 检查文件是否存在
if os.path.isfile(file_path):
    os.remove(file_path)  # 删除文件
    print(f'文件 {file_path} 已被删除。')
else:
    print(f'文件 {file_path} 不存在。')

# 判断不等于200
# 只有当状态码为200时才继续执行
if response.status_code != 200:
    print('下载失败，状态码：', response.status_code)
    return

# 判断用户是否传入有效值
value = user_input if user_input else default_value

# 数据库查询
result = cursor.fetchone()
if result is None:

results = cursor.fetchall()
if not results:

my_value = False
my_value = {}
if not my_value:
    print("此条件为 False")

# 某属性
# 获取result字段的内容
result = data.get("result")
# 如果result为空或不存在
if not result:
    print("Result字段为空或不存在。")
else:
    print("使用有效的result：", result)
```

### 循环语句
#### while语句
``` py
while 表达式：# 表达式如果为真，会一直执行, 直到表达式为假
  代码块

while True:
  print('a')
  break # 终断

import time
num = 5
while True:
  num = num + 1
  if num == 10:
    continue # 跳过本次
  print(num)
  time.sleep(1)
```

#### for语句
``` py
for 迭代变量 in 可迭代对象：
  代码块
    # 跳过本次循环
    continue
    # 终止循环
    break

for s in [1,2,3]:
  print(s)

for i in range(1,13): # range(13) 1,--12; 不包含最后一个数
  print(i)


arr = [{"name": "Alice", "age": 20}, {"name": "Bob", "age": 25}]
# 遍历数组
for item in arr:
    # 获取并打印每项里面的 name 属性
    print(item["name"])

# 输出：
# Alice
# Bob

for index, dir in enumerate(dirs, start=1):
    print(f"Index: {index}, Directory: {dir}")
```

#### 
```py
json_result = [{table_name:1,table_comment:1}]
json_data = {d['table_name']: d['table_comment'] for d in json_result}
```

## 函数
### 定义
``` py
def 函数名称():
  代码
  return 需要返回的内容
```

### 调用
函数名称()

## 关键字
### with
Python 中的 with 语句用于异常处理，封装了 try…except…finally 编码范式，提高了易用性。
with 语句使代码更清晰、更具可读性， 它简化了文件流等公共资源的管理。
```py
# try…except…finally
file = open('./test_runoob.txt', 'w')
try:
    file.write('hello world')
finally:
    file.close()

# with 关键字
with open('./test_runoob.txt', 'w') as file:
    file.write('hello world !')
```

## 异步任务
### FastAPI 后台任务
```py
from fastapi import FastAPI, BackgroundTasks
app = FastAPI()
def method_a():
    # 执行某些操作
    print("Task is running in the background")
@app.post("/start-task")
async def start_task(background_tasks: BackgroundTasks):
    background_tasks.add_task(method_a)
    # 方法中带参数
    background_tasks.add_task(processHandle, bizInfo, uuid1, table_row, table_field_names)
    return {"message": "Task received and started"}
```

### 等待
```py
import time
time.sleep(3)
```

### 异步函数
```py
import asyncio
from fastapi import FastAPI
app = FastAPI()
async def method_a():
    # 异步执行某些操作
    print("Task is running asynchronously")
    await asyncio.sleep(5)  # 模拟异步操作
    print("Task completed")
@app.post("/start-task")
async def start_task():
    asyncio.create_task(method_a())  # 创建一个新的任务
    return {"message": "Task received and started"}
```

# Issuse
## Missing dependencies for SOCKS support
环境变量中则设置了 socks5 的代理; ~/.zshrc
Python 本身在没有安装 pysocks 时并不支持 socks5 代理
取消代理
unset all_proxy && unset ALL_PROXY

安装
pip install pysocks

## 时间
### 时间戳
秒级
```py
import time
timestamp_in_seconds = int(time.time())
```
### 定时器
``` py
import threading
def print_message():
    print("This is a message from the timer!")
# 创建一个定时器，指定5秒后执行print_message函数
timer = threading.Timer(5.0, print_message)
# 启动定时器
timer.start()
print("Timer has been set...")
```

# 轮子 Tool
## 随机不重复字符串
``` py
import random

# 定义字符集，用于生成随机字符串
charset = "abcdefghijklmnopqrstuvwxyz0123456789"

# 生成随机字符串
random_str = "".join(random.choice(charset) for _ in range(16))

# 打印字符串
print(random_str)
```

## 执行py文件
```py
import subprocess
subprocess.run(['python', 'test.py'], check=True)
```

## matplotlib画图
mac下python matplotlib中文乱码解决方案
plt.rcParams["font.family"] = 'Arial Unicode MS'

## uuid
```py
import uuid
# 最常用的是UUID
## UUID1（基于时间和节点（MAC地址）的UUID）
uuid1 = uuid.uuid1()
print(f"UUID1: {uuid1}")
## UUID4（基于随机数的UUID）
uuid4 = uuid.uuid4()
print(f"UUID4: {uuid4}")
# 通常在不需要跟踪对象创建时间和来源的情况下，建议使用uuid4，因为它完全是基于随机数的，能提供更好的唯一性保证。
```

## 格式化时间
``` py
from datetime import datetime
# 获取当前时间
now = datetime.now()
# 格式化时间 - 注意这里的格式应该是 "yymmdd HH:MM:SS"
formatted_time = now.strftime("%y%m%d %H:%M:%S")
print(formatted_time)
```

## config.ini
```ini
[database]
server = 192.168.1.1
```
```py
from configparser import ConfigParser

config = ConfigParser()
config.read('config.ini')

db_server = config.get('database', 'server')
```

## .env
pip install python-dotenv
.env
```
DB_HOST=
DB_USER=
DB_PASS=
DB_NAME=
DB_PORT=
```
```py
from dotenv import load_dotenv

load_dotenv()

db_host = os.getenv('DB_HOST')
```

## logging日志文件
```py
import logging

logging.basicConfig(filename='application.log',
                    level=logging.INFO,
                    format='%(asctime)s - %(levelname)s - %(message)s',
                    encoding='utf-8')

logging.info('应用程序启动')
```   

## 打开浏览器
```py
from selenium import webdriver
driver = webdriver.Edge()
```

# Nacos
```yaml
aliyun:
  oss:
    accessKeyId: 123
```
```py
from nacos import NacosClient
self.client = NacosClient(server_addresses=self.serverAddr, namespace=self.namespace)

from src.utils.NacosUtils import NacosUtils
aliyunOss = res["aliyun"]["oss"]
```

# mysql
## insert
```py
# 1
record_ret = cursor.rowcount
# 57
id = cursor.lastrowid
```

## select
### 不为空
```py
query = f"SELECT id,keyword,tel FROM {table_name} WHERE keyword IS NOT NULL AND keyword <> '' AND status=1 limit {batch_size}"
```

# fastapi
## mysql查询
``` py
@router.post("/record")
async def record(no):
    print("query record start ...")
    cursor = None
    output = {}
    try:
        # 1.检查业务编号表格字段映射
        cursor = cnx.cursor()
        biz_record_sql = "select * from a where no=%s"
        cursor.execute(biz_record_sql, [no])
        record_row = cursor.fetchone()
        record_field_names = [i[0] for i in cursor.description]
        output = dict(zip(record_field_names, record_row))
        print("record_row", record_row)
    except Exception as e:
        print(f"error: {e}")
        return return_error("查询解析记录异常")
    finally:
        # 关闭连接
        cursor.close()
    return return_vo(output)
```

## 是否在方法前加 async
```py
# 如果路由处理函数中需要进行异步操作，比如访问数据库、调用异步API、执行异步文件操作等，那么定义异步函数并使用 async def 是有必要的。
# 如果路由处理函数只执行同步操作，并且这些操作非常快速，不会造成明显的阻塞
```
## 文件处理
文件操作默认是同步的
image
```py
@router.post("/ocr-test",  name="test")
async def ocrTest(
    file: UploadFile = File(...)
) -> None:
    print("file", file)
    contents = await file.read()
    random_str = "".join(random.choice(charset) for _ in range(16))
    save_path = "./assets/test/" + random_str + ".png"
    with open(save_path, 'wb') as f: # write() 是同步
        f.write(contents)
```

### excel下载
```py
file_path = f"./src/output/oss_files/{uuid4}.xlsx"
oss_path_ret = requests.get(bizInfo.oss_path)
with open(file_path, 'wb') as file:
    # 使用.iter_content()按块写入数据
    for chunk in oss_path_ret.iter_content(chunk_size=65536):
        file.write(chunk)
print('OSS文件下载完成')
```

### URL下载
```py
# 1.判断url是否存在, 发送GET请求并获取响应
url_res = requests.get(bizInfo.url)
if url_res.status_code != 200:
    logger.error(f"请求url未响应, url: {bizInfo.url}")
    return return_error("请求url未响应, 请检查url有效性")

# 判断是否是excel文件
uuid4 = uuid.uuid4()
file_path = f"./src/output/oss_files/{uuid4}.xlsx"
# 下载url对应文件
Tools.download_file(bizInfo.url, file_path)
try:
    load_workbook(file_path)
    # Excel文件
except InvalidFileException:
    # 非Excel文件
    logger.error(f"请求url非Excel文件, url: {bizInfo.url}")
    Tools.rm_files([file_path])
    return return_error("请求url非Excel文件, 请检查url对应资源")
logger.info("url对应文件格式正确")
```

## 请求参数类型
```py
from fastapi import FastAPI, Body, Query
app = FastAPI()
@app.put("/items/{item_id}")
# URL路径中有一个路径参数item_id，请求体中有一个item对象，URL查询字符串还有一个可选的查询参数q。
async def update_item(item_id: int, item: Item = Body(...), q: str = Query(None)):
    results = {"item_id": item_id, "item": item}
    if q:
        results.update({"q": q})
    return results

# Query
async def test(q: str = Query(None, title="Query string"), s: str = Query(None)):
```

## 请求参数校验
pydantic 作为参数，没有使用Query、Body等明确声明，FastAPI默认会读取它作为JSON请求体（Body）参数。
``` py
from pydantic import BaseModel, StringConstraints
class BizInfo(BaseModel):
    biz_no: Annotated[str, StringConstraints(min_length=1)]
    des: str = "123"

class RecordRequest(BaseModel):
    # id: Annotated[Union[str, int], constr(min_length=1)]
    id: Union[str, int]

    @validator('id')
    def check_id(cls, v):
        if isinstance(v, str) and len(v) == 0:
            raise ValueError('id 不能为空！')
        return v
```

## 事务处理
在Python中使用MySQL时，需要添加事务处理（即使用commit()和rollback()）的操作类型主要包括对数据库数据进行变更的SQL语句，这些操作一旦执行会修改数据库中的数据。通常包括以下几种：
INSERT - 向表中插入新行。
UPDATE - 更新表中的现有行。
DELETE - 从表中删除行。
REPLACE - 一个特殊的INSERT，如果在插入时遇到主键或唯一索引冲突，则先删除旧行，再插入新行。

## __init__.py文件
`__init__.py`文件用作标识一个目录为Python包的角色。它可以被用来执行包的初始化代码，如包级别的变量设置、以及子模块的导入等。


# AI数据处理
## pandas
### merge 销量
df_sales = df.groupby('年月').agg({'数量': 'sum'}).reset_index().rename(columns={'数量': '总数量'})

### excel表格头映射
```py
# 假设你的Excel中文表头为'姓名'和'年龄'，英文对应为'Name'和'Age'。
chinese_to_english = {
    '姓名': 'Name',
    '年龄': 'Age'
    # 以此类推，其它列也进行相应的映射。
}

# 使用映射字典重命名DataFrame的列名。
df.rename(columns=chinese_to_english, inplace=True)
```

### excel转为json
```py
# value值全部设为字符串
df = pd.read_excel(file_path, dtype=str)
# 表头映射
df.rename(columns=combined_ret, inplace=True)
# file_json_path = f"./src/output/excel_json_files/{uuid4}.json"
# df.to_json(file_json_path, orient='records', lines=False)

# 获取分割后的DataFrame片段
df_subset = df.iloc[start_row:end_row]
# 将所有的NaN值替换为空字符串
df_subset_filled = df_subset.fillna('')
# 构造JSON格式的数据。 to_dict方法：DataFrame转换为字典
json_data = {"total": total_rows, "row": df_subset_filled.shape[0], "datas": df_subset_filled.to_dict(orient='records')}

with open(local_json_file, 'w') as fp:
    # 当ensure_ascii设置为False时, 直接使用UTF-8编码写入中文字符, 而不是将它们转换为Unicode转义序列。
    json.dump(json_data, fp, ensure_ascii=False)
```

```py
df = pd.read_excel(local_excel_dir)
num_rows = df.shape[0]
logger.info(f"Excel总行数: {num_rows}")
df.rename(columns=combined, inplace=True)

# 定义每个JSON文件的行数
rows_per_file = 10000
# 计算需要多少个JSON文件
num_files = math.ceil(num_rows / rows_per_file)

# 分割DataFrame并写入JSON文件
for i in range(num_files):
    start_row = i * rows_per_file
    end_row = start_row + rows_per_file
    # 获取分割后的DataFrame片段
    df_subset = df.iloc[start_row:end_row]
    # 构造JSON格式的数据
    json_data = {"columns": len(df.columns), "datas": df_subset.to_dict(orient='records')}
    # 设置文件名并保存为JSON
    json_file_name = f"{local_json_dir}_{i+1}.json"
    with open(json_file_name, 'w') as fp:
        json.dump(json_data, fp)

    # 更新日志信息
    logger.info(f"已导出 {json_file_name}")
```

# 研究
## NLP
NLP：Natural Language Processing，自然语言处理
将人类之间交流沟通所用的语言经过处理转化为机器所能理解的机器语言。
目的就是让机器理解并生成人类的语言，从而和人类平等流畅地沟通交流。

### 两种方向
- 自然语言理解（Natural Language Understanding, NLU）【如何理解文本】
- 自然语言生成（Natural Language Generation, NLG）【理解文本后如何生成自然文本】

### 应用
作为人工智能领域的底层技术，自然语言处理常常与智能语音、知识图谱等技术方向衔接捆绑。通过语音识别、语音合成、语义分析等细化技术的互相组合，以对话式AI、机器翻译、文字审核、知识库等类型的产品和应用出现。
在实际应用层面，则常常用以满足较为复杂的社交网络文本情感分析、客户信息挖掘等的需求，比如电商平台中构建知识图谱实现智能导购，挖掘客户兴趣以实现精准营销；客服场景中智能机器人提供客服服务、翻译机器人在跨境电商业务中对商品信息、广告词等进行翻译。

由于自然语言作为人类社会信息的载体，使得NLP不只是计算机科学的专属。在医疗健康、金融、法律、教育等领域，同样存在着海量的文本，NLP也就成为了重要支持技术。

#### 医疗行业
- 从病历、检验单、医嘱等医疗文本中提取患者的性别年龄、临床症状等关键信息，将非结构化数据转化成一致、统一的表格等形式的结构化数据
- 基于提取出的信息，并且让机器掌握医生具备的医疗知识，构建出显示各类医疗信息之间关系的知识图谱，比如患者症状、药物、疾病诊疗等
- 知识图谱可以根据患者的症状诊断疾病，或者根据特定的疾病推断出未来可能出现的症状

## Issuse
### 应用领域？
- 电子医生 -> 智能辅助诊疗
- Siri手机助手
- 智能客服


# OCR
OCR：Optical Character Recognition，光学字符识别
指电子设备（例如扫描仪或数码相机）检查纸上打印的字符，通过检测暗、亮的模式确定其形状，然后用字符识别方法将形状翻译成计算机文字的过程

在NLP的相关产品中，OCR扮演着不可或缺的角色，主要是在关于文档处理的一些场景中，例如，pdf等格式的文档抽取、文档审核、文档比对等。

## 应用
- 银行卡拍照识别
- 快递信息拍照，自动录入

# Paddle
人工智能 > 机器学习 > 深度学习

# 包
## cv2
cv2是Python语言的一个计算机视觉库，用于图像处理和计算机视觉领域的开发。它是OpenCV库的Python语言绑定，提供了许多图像处理和计算机视觉的算法和方法，使得Python开发者可以方便地实现图像处理和计算机视觉的功能。

cv2库提供了常用的图像处理和计算机视觉算法，例如图像分割、目标检测、图像分类、视频分析等。它还提供了一些图像处理和计算机视觉的工具，例如图像显示、图像读取、图像保存等。

使用Python的cv2包，开发者可以快速实现图像处理和计算机视觉功能，并且可以通过深度学习模型来提高算法的性能。

## pandas
简单例子
```py
# 创建一个字典，包含学生的姓名和年龄
data = {'姓名': ['张三', '李四', '王五'],
        '年龄': [20, 21, 19]}

# 创建数据帧
df = pd.DataFrame(data)

# 打印数据帧
print(df)

# 输出
姓名  年龄
0  张三  20
1  李四  21
2  王五  19
```

## openpyxl
```py
from openpyxl import Workbook
  # 创建一个工作簿对象
  wb = Workbook()
  # 在索引为0的位置创建一个名为mytest的sheet页
  ws = wb.create_sheet('mytest',0)
  # 对sheet页设置一个颜色（16位的RGB颜色）
  ws.sheet_properties.tabColor = 'ff72BA'
  # 将创建的工作簿保存为Mytest.xlsx
  wb.save('Mytest.xlsx')
  # 最后关闭文件
  wb.close()
```

## pyinstaller
``` bash
 * On Debian/Ubuntu, you would need to install Python development packages
    * apt-get install python3-dev
    * apt-get install python-dev
    * If you're building Python by yourself, please rebuild your Python with `--enable-shared` (or, `--enable-framework` on Darwin)
$ env PYTHON_CONFIGURE_OPTS="--enable-framework" pyenv install 3.9.15
```

```py
import webbrowser
import os

print("Hello, World!")
filename = './test.html'
webbrowser.open('file://' + os.path.realpath(filename))
```

pyinstaller -w main.py

### 指令参数
-i exe.ico, macos.icns
--distpath out
--add-data "config.ini:." "config.ini;."
-w 不显示命令行窗口（控制台窗口）

### GUI
pip install pyside6
```py
from threading import Thread
from fastapi import FastAPI
from uvicorn import Config, Server
from PySide6.QtWidgets import QApplication, QMainWindow, QPushButton
import sys

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "World"}

def start_api():
    config = Config(app=app, host="0.0.0.0", port=8000)
    server = Server(config)
    server.run()

class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle('FastAPI Server Controller')
        self.setGeometry(100, 100, 200, 100)
        self.start_button = QPushButton('Start Server', self)
        self.start_button.clicked.connect(self.start_server_thread)
        self.start_button.resize(200, 100)

    def start_server_thread(self):
        api_thread.start()
        self.start_button.setEnabled(False)
        self.start_button.setText('Server Running')

if __name__ == "__main__":
    qt_app = QApplication(sys.argv)
    window = MainWindow()
    window.show()
    # 使用线程来启动FastAPI服务
    api_thread = Thread(target=start_api)
    sys.exit(qt_app.exec())
```

#### 打开本地html文件
QWebEngineView是一个基于Chromium的浏览器引擎，用于在Qt应用程序中嵌入网页。它可以显示来自互联网的网页，也可以渲染本地存储的HTML文件。QWebEngineView为Qt提供了现代的Web浏览能力，包括HTML5、CSS3和JavaScript的支持。
```py
from PySide6.QtWebEngineWidgets import QWebEngineView
from PySide6.QtCore import QUrl
class MainWindow(QMainWindow):
    def __init__(self):
        super(MainWindow, self).__init__()
        self.browser = QWebEngineView()

        # Load local HTML file
        # self.browser.load(QUrl.fromLocalFile("test.html"))
        # self.setCentralWidget(self.browser)

        # 获取当前工作目录
        cwd = os.getcwd()
        print("Current working directory:", cwd)
        
        # 指定文件路径 -- 方法1: 直接使用文件名（如果HTML文件和main.py在同一目录下）【不可行】
        # file_path = "test.html"
        
        # 指定文件路径 -- 方法2: 使用绝对路径
        file_path = os.path.join(cwd, "test.html")
        
        # 检查文件是否存在
        if os.path.exists(file_path):
            self.browser.load(QUrl.fromLocalFile(file_path))
            self.setCentralWidget(self.browser)
        else:
            print("Error: File does not exist at the specified path", file_path)
```

#### 子线程和GUI+chromium
```py
from uvicorn import Config, Server
from PySide6.QtWidgets import QApplication, QMainWindow
from PySide6.QtWebEngineWidgets import QWebEngineView
from PySide6.QtCore import QUrl
from multiprocessing import Process, Event
import sys
import os
import signal
def start_api(started_event):
    config = Config(app=app, host="0.0.0.0", port=8020)
    server = Server(config)
    started_event.set()  # 设置请求的Event
    server.run()


class MainWindow(QMainWindow):
    def __init__(self):
        super(MainWindow, self).__init__()
        self.browser = QWebEngineView()

        cwd = os.getcwd()
        file_path = os.path.join(cwd, "dist/index.html")
        self.browser.load(QUrl.fromLocalFile(file_path))
        self.setCentralWidget(self.browser)

    def closeEvent(self, event):
        # 当窗口关闭时，发送SIGTERM信号到FastAPI服务进程
        os.kill(api_process.pid, signal.SIGTERM)
        event.accept()

if __name__ == "__main__":
    # 在子进程中启动FastAPI服务
    started_event = Event()  # 创建一个事件对象
    api_process = Process(target=start_api, args=(started_event,))
    api_process.start()

    started_event.wait()  # 等待事件被设置
    print("FastAPI服务应该已经启动并设置了事件")

    qt_app = QApplication(sys.argv)
    window = MainWindow()
    window.show()

    sys.exit(qt_app.exec())
```

#### windows控制台颜色乱码
```
[32mINFO[0m:     127.0.0.1:53140 - "[1mOPTIONS /list HTTP/1.1[0m" [32m200 OK[0m
```
```py
# 解决办法
import colorama
colorama.init()
```

## pycryptodome
加密包
要改，项目中的 venv/lib/python3.9/site-packages/
crypto -> Crypto

PyCryptodome 是一个用于加密和解密的Python库，提供了多种加密算法的实现，包括AES（高级加密标准）。在使用AES加密时，AES.new() 方法是创建一个AES加密对象的主要方法。这个方法需要传入几个关键参数：加密密钥（key）和加密向量（IV，Initialization Vector），具体参数取决于所选择的模式（mode）。

AES.new() 方法
AES.new() 方法用于创建一个新的AES加密对象。其基本语法如下：

```py
from Crypto.Cipher import AES
cipher = AES.new(key, mode, iv)
```

参数解释
key（密钥）：

类型：字节串（bytes）
长度：AES支持三种密钥长度：16字节（128位），24字节（192位），和32字节（256位）。
作用：密钥用于加密和解密数据，是加密过程中的核心秘密。
mode（模式）：

类型：常量，表示AES的工作模式。
常见模式：
AES.MODE_ECB：电子密码本模式（不推荐，因为它不使用IV，容易受到多种攻击）。
AES.MODE_CBC：密码分组链接模式（需要IV）。
AES.MODE_CFB：密码反馈模式（需要IV）。
AES.MODE_OFB：输出反馈模式（需要IV）。
AES.MODE_CTR：计数器模式（不需要IV，但需要nonce）。
AES.MODE_GCM：Galois/Counter模式（需要IV，提供认证）。
iv（初始化向量）：

类型：字节串（bytes）
长度：通常与块大小相同，即16字节（128位）。
作用：IV用于确保相同的明文块在不同的加密操作中生成不同的密文，增加安全性。
注意：IV必须是唯一的，但不需要保密。对于一些模式（如CTR），可以使用nonce代替IV。

例子
```py
import hashlib
import json
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad
import time

def hex_encode(string):
    return ''.join(format(ord(char), '02x') for char in string)

content = json.dumps({
    "appSecret": "000"
})  # 加密原文
key = '000'.encode('utf-8')  # 加密 key
iv = '000'.encode('utf-8')  # 加密向量

# AES-256-CBC 加密
cipher = AES.new(key, AES.MODE_CBC, iv)
encrypted = cipher.encrypt(pad(content.encode('utf-8'), AES.block_size))

# Hex 编码
hex_encrypted = hex_encode(encrypted.decode('latin1'))

print(hex_encrypted)  # 输出结果

# 生成签名
appKey = '000'  # appkey 值莲藕提供
nonce = '1006148241'  # 动态获取
# timestamp = '1721966058'  # 动态获取
print('====================')
timestamp = int(time.time())  # 动态获取
# print(timestamp)

sign_string = f'appKey={appKey}&content={hex_encrypted}&nonce={nonce}&timestamp={timestamp}'
# print(sign_string)
# print('----------------------')
sign = hashlib.sha1(sign_string.encode('utf-8')).hexdigest().upper()

print(sign)  # 输出签名

print('---->->-->--->----->-------')
url_string = f'https://test/Token?nonce={nonce}&timestamp={timestamp}&sign={sign}'
print(url_string)
```


# FN
## 提取文字
``` py
# pdf提取文字，但无法识别pdf中的图片
import PyPDF2

# 打开 PDF 文件
with open('insert_img.pdf', 'rb') as file:
    pdf = PyPDF2.PdfFileReader(file)

    # 获取文档页数
    pages = pdf.getNumPages()
    print('pages', pages)

    # 循环每一页，提取文本
    for i in range(pages):
        page = pdf.getPage(i)
        text = page.extractText()
        print(text)
```

## 每年非工作日
``` py
# coding=utf-8
# !/usr/bin/python
import requests
import json


# 从百度的php接口中获取到数据
def catch_url_from_baidu(calcultaion_year, month):
    headers = {
        "Content-Type": "application/json;charset=UTF-8"
    }
    param = {
        "query": calcultaion_year + "年" + month + "月",
        "resource_id": "39043",
        "t": "1604395059555",
        "ie": "utf8",
        "oe": "gbk",
        "format": "json",
        "tn": "wisetpl",
        "cb": ""
    }
    # 抓取位置：百度搜索框搜索日历，上面的日历的接口，可以在页面上进行核对
    r = requests.get(url="https://sp0.baidu.com/8aQDcjqpAAV3otqbppnN2DJv/api.php",
                     headers=headers, params=param).text
    month_data = json.loads(r)["data"][0]["almanac"]
    not_work_day = []
    for one in month_data:
        if (one["cnDay"] == '日' or one["cnDay"] == '六'):
            if ('status' in one):
                if (one["status"] == "2"):
                    # status为2的时候表示周末的工作日，比如10月10日。即百度工具左上角显示“班”的日期
                    continue
                else:
                    # 普通周末时间
                    not_work_day.append(one)
                    continue
            else:
                # 普通周末时间。（接口中，如果左上角没有特殊表示，则不会返回status）
                not_work_day.append(one)
                continue
        if ('status' in one and one["status"] == "1"):
            # status为1的时候表示休息日，比如10月1日。即百度工具左上角显示“休”的日期
            not_work_day.append(one)
    print_info(not_work_day)


def print_info(not_work_day):
    nonWorkingDays = ""
    for one in not_work_day:
        # insert_sql = "insert TABLE (YEAR,MONTH,DAY) VALUES (" + one["year"] + "," + one[
        #     "month"] + "," + one["day"] + ");"
        # print(insert_sql)

        monthNum = one["month"]
        if(int(monthNum) < 10):
            monthNum = "0"+monthNum
        dayNum = one["day"]
        if(int(dayNum) < 10):
            dayNum = "0"+dayNum
        ret = one["year"]+"-"+ monthNum +"-"+ dayNum + ","
        nonWorkingDays = nonWorkingDays + ret
        # print(one["year"]+"-"+one["month"]+"-"+one["day"])
    print(nonWorkingDays)


if __name__ == '__main__':
    # 此处只能算当年之前的，因为国务院是每年12月份才会发布第二年的放假计划，所以此接口对于下一年的统计是错的。eg：2020年11月4日，国务院没有发布21年的放假计划，那查询2021年元旦的时候，元旦那天不显示休息
    calcultaion_year = "2024"
    # 因该接口传入的时间，查询了前一个月，当前月和后一个月的数据，所以只需要2、5、8、11即可全部获取到。比如查询5月份，则会查询4,5,6月分的数据
    calculation_month = ["2", "5", "8", "11"]
    for one_month in calculation_month:
        catch_url_from_baidu(calcultaion_year, one_month)
```

# 其他
## Process 和 Thread 区别
在Python中，Process和Thread都能用于实现并发编程，但是他们的使用场景和实现方式有所不同。
进程（Process）:
进程是操作系统进行资源分配和调度的基本单位。每个进程都有自己独立的内存空间和环境变量，进程之间的通信需要使用进程间通信（IPC）技术如管道，消息队列，信号量等。
Python的multiprocessing模块提供了Process类来创建一个进程。在Python中，由于存在全局解释器锁（GIL）的问题，多线程无法利用多核CPU的优势。而使用多进程则可以实现并行计算，即在同一时间内利用多核CPU执行多个任务。

线程（Thread）:
线程是操作系统进行CPU调度的基本单位，一个进程可以包含多个线程，所有线程共享进程的内存空间和环境变量，因此线程之间的通信更简单，可以直接分享数据。
Python的threading模块提供了Thread类来创建一个线程。由于全局解释器锁（GIL）的影响，在Python中，多线程主要适用于I/O密集型任务，例如文件操作，网络请求等，这是因为这些任务的主要时间在等待I/O操作，而不是在CPU计算。在等待的过程中，CPU可以切换到其他线程执行任务，这样就能提高程序的并发性。

总的来说，Process和Thread都可以用来执行并发任务，但是由于Python的全局解释器锁（GIL）的存在，对于计算密集型任务，建议使用多进程。对于I/O密集型任务，可以使用多线程或者异步I/O模型（比如asyncio）。而且，Process和Thread之间的选择也应该根据具体需求和场景来决定。

### 注意
如果你决定使用 threading.Thread 来启动 FastAPI 服务而不是 multiprocessing.Process，你将不会遇到额外的客户端实例启动的问题，因为线程与进程有不同的行为——线程是在同一个进程空间内运行，不会创建新的进程。

# Issuse
## pycharm报错提示：无法加载文件\venv\Scripts\activate.ps1
此系统上禁止运行脚本
https://blog.csdn.net/freedomofu/article/details/126537492

## pyinstaller报错
uvicorn的Config配置启动信息，使用pyinstaller打包后出错。
配置：config = Config(app=app, host="0.0.0.0", port=8020)
错误信息：启动api服务失败: Unable to configure formatter 'default'
解决办法：pyinstaller -w 参数去掉

## Index(['name'], dtype='object')
```py
import pandas as pd

# 示例数据
data = {
    'name': ['Alice', 'Bob', 'Alice', 'Charlie', 'Bob'],
    'age': [25, 30, 25, 35, 30]
}

# 创建 DataFrame
df = pd.DataFrame(data)

# 打印列名
print("Columns:", df.columns)

# 打印前几行数据
print("DataFrame head:\n", df.head())

# 清理列名
df.columns = df.columns.str.strip()

# 使用 duplicated 方法
print("Duplicated rows:\n", df.duplicated(subset=['name'], keep=False))
```