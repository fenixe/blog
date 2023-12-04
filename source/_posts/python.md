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
## 安装
python.org download

python3 -V
pip3 -V

## 查看安装的包
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

app = FastAPI()

@app.get("/")
def read_root():
  return {"Hello": "World"}
```
- 启一个服务，pip install uvicorn
  uvicorn main:app --reload


## 添加服务
- pip install fastapi

## 连接数据库
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

## gitignore
```
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

# Issuse
## Missing dependencies for SOCKS support
环境变量中则设置了 socks5 的代理; ~/.zshrc
Python 本身在没有安装 pysocks 时并不支持 socks5 代理
取消代理后，安装
pip install pysocks


# 轮子
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

# fastapi
## 文件处理
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

# 预测-线性回归
## 线性回归
线性回归是一种常见的统计分析方法，用于建立自变量（输入）和因变量（输出）之间的线性关系模型。它假设自变量与因变量之间存在线性关系，并试图通过拟合最佳的直线来预测因变量的值。

以下是线性回归的基本步骤：

收集数据：收集包含自变量和因变量的数据样本。

数据预处理：对数据进行清洗和预处理，包括处理缺失值、异常值和数据转换等。

划分数据集：将数据集划分为训练集和测试集，用于模型训练和评估。

建立模型：选择合适的线性回归模型，例如简单线性回归（只有一个自变量）或多元线性回归（多个自变量），并设置模型参数。

拟合模型：使用训练集数据拟合线性回归模型，估计模型的系数和截距，以找到最佳拟合直线。

模型评估：使用测试集数据评估模型的性能，常见的评估指标包括均方误差（Mean Squared Error, MSE）、决定系数（Coefficient of Determination, R²）等。

模型应用：使用训练好的线性回归模型对新的自变量进行预测，得到对应的因变量值。

需要注意的是，线性回归的前提是自变量和因变量之间存在线性关系，且数据满足一些基本的假设条件，如线性性、独立性、常态性和同方差性等。在实际应用中，应该对数据进行适当的探索和验证这些假设条件。


# Issuse
## pycharm报错提示：无法加载文件\venv\Scripts\activate.ps1
此系统上禁止运行脚本
https://blog.csdn.net/freedomofu/article/details/126537492