<hr>

[TOC]

<hr>

### [Default]

#### [list]

- index(ele)

```python
lst = [1, 2, 3, 2, 4, 1, 5, 6, 5]
duplicates = list(set([x for x in lst if lst.count(x) > 1]))
```

#### [str]

- format():
  - format(float num, "0.2f"): 保留2位小数;
  - format(float num, "^10.10f"): 多占10位空格，"^"代表居中;
- split(str, num):
  - str: 需要切片的字符串。
  - num: 需要切片的次数，默认-1表示全部切片。

### [dic]

- keys()

- values()

- items()

  ```python
  for key, value in my_dict.items():  
      print(key, value)
  ```

#### [ANSI]

##### [Color]

<table style="text-align:center;background-color:#333" border=5px>
    <tr><th>背景色</th><th>字体色</th></tr>
    <tr><td bgcolor="black">30:黑</td><td style="color:black">40:黑</td></tr>
    <tr><td bgcolor="red">31:红</td><td style="color:red">41:红</td></tr>
    <tr><td bgcolor="green">32:绿</td><td style="color:green">42:绿</td></tr>
    <tr><td bgcolor="yellow">33:黄</td><td style="color:yellow">43:黄</td></tr>
    <tr><td bgcolor="blue">34:蓝</td><td style="color:blue">44:蓝</td></tr>
    <tr><td bgcolor="purple">35:紫</td><td style="color:purple">45:紫</td></tr>
    <tr><td bgcolor="cyan">36:青</td><td style="color:cyan">46:青</td></tr>
    <tr><td bgcolor="white">37:白</td><td style="color:white">47:白</td></tr>
</table>

##### [Command]

<table style="text-align:center;background-color:#333" border=5px>
    <tr><th>代码</th><th>效果</th></tr>
    <tr><td>\033[0m</td><td>关闭全部</td></tr>
    <tr><td>\033[1m</td><td><mark>高亮</mark></td></tr>
    <tr><td>\033[4m</td><td><u>下划线</u></td></tr>
    <tr><td>\033[5m</td><td>闪烁</td></tr>
    <tr><td>\033[7m</td><td bgcolor="#bbb" style="color:#333">反显</td></tr>
    <tr><td>\033[8m</td><td style="color:#333">消隐</td></tr>
    <tr><td width=50%>\033[30m ~ \033[37m</td><td>背景色</td></tr>
    <tr><td width=50%>\033[40m ~ \033[47m</td><td>字体色</td></tr>
    <tr><td>\033[nA</td><td>光标上移n行</td></tr>
    <tr><td>\033[nB</td><td>光标下移n行</td></tr>
    <tr><td>\033[nC</td><td>光标右移n行</td></tr>
    <tr><td>\033[nD</td><td>光标左移n行</td></tr>
    <tr><td>\033[y;xH</td><td>光标坐标(x,y)</td></tr>
    <tr><td>\033[2J</td><td>清屏</td></tr>
    <tr><td>\033[K</td><td>从光标清除到行尾</td></tr>
    <tr><td>\033[s & \033[u</td><td>保存&恢复光标位置</td></tr>
    <tr><td>\033[25l & \033[25h</td><td>隐藏&显示光标</td></tr>
</table>

<hr>



### os

- getcwd()

  - 获取当前工作目录;

- listdir(path)

  - 获取所给path中的所有文件/文件夹;
  - list;

- mkdir(path)

  - 创建一个名为path的目录。

- rmdir(path)

- makedirs(path, exist_ok)

  - 创建一个名为path的目录。
  - 若path包含多个目录，则创建所有目录。
  - exist_ok: 取值False时若创建目录已存在则引发异常，取值True时则不会。

- remove(file)

- chdir(path)

- walk(path)

  ```python
  for(dirpath, dirnames, filenames) in os.walk(path):
      files += filenames
      dires += dirnames
  ```

- listdire(path)

#### [path]

- realpath(path)
- abspath(path)
- exists(path)
- getsize(path)
- getmtime(path)
- isdir(path)
- dirname(file)
  - 去掉文件名，返回其路径。

<hr>

### sys


- exit(0)
- argv
  - 列表，执行python文件时输入的参数。
  - `python demo.py a b c` -> `["demo.py", "a", "b", "c"]`

<hr>

### shutil

- rmtree(path, ignore_errors=True)
  - 递归删除目录所有的子目录和子文件。

<hr>

### glob


- glob(pat)
  - `exes = glob.glob(r"d:/tmp/*.txt")`

<hr>

### urllib

#### [parse]

- urllib.parse.quote(text, encoding='utf-8')

<hr>


### pandas

- `data = pandas.read_excel("main.xls")`; `data = pandas.read_excel("main.xls", sheet_name = "Sheet1")`; data: dict; 使用列首格名作为索引; 默认"Unnamed: 1";
- `data.iloc[row_index, column_index]`; `data.iloc[:, Index]`: 按照索引值Index取列值;
-  `data.iloc`: Integer location; 将数据转换为使用索引选取内容;

<hr>

### keyboard

```python
def func(event):
    if event.name == "esc" or event.name == "f1":
        keyboard.unhook_all()
        quit()
```

- `keyboard.on_press(func)`: 绑定事件;
- `keyboard.wait()`: 开始监听;
- `keyboard.unhook_all()`: 取消键盘监听;

<hr>

### psutil

#### disk_usage(str path)

```python
disk=psutil.disk_usage('./')
print(f"[{disk.percent}%]-[{disk.used/1E9} GB/{disk.total/1E9} GB]-[Free:{disk.free/1E9} GB]")
```

```python
disk = psutil.disk_usage('./')
res = disk.free / 1E9
print(f'\033[2;3H[{format(res, "^10.10f")} GB]')
```

#### sensors_battery()

```python
battery = psutil.sensors_battery()
print(f"{battery.percent}% Plugged:{battery.power_plugged}")
```

<hr>

### datetime

#### date

- today();

#### datetime

- now().strftime("%H:%M:%S");

<hr>

### asyncio

- sleep(num)

  - 异步函数中设置间隔。

- run(func())

  - 运行一个async关键词定义的函数。

  ```python
  async def func():
      print("Hello")
      await asyncio.sleep(1) # 异步等待1秒;
      print("World")
  asyncio.run(func())
  ```


<hr>

### threading

- active_count()
  - 正在运行线程的数量
- enumerate()
  - 正在运行线程的列表
- current_thread()
  - 当前线程变量
- Thread(group=None, target=None, name=None, args=(), daemon=None)

```python
def func(n):
    pass
T = threading.Thread(target=func,args=("func",))
T.start()
```

```python
import threading
def my_function(arg1, arg2):
    print(arg1, arg2)
thread = threading.Thread(target=my_function, kwargs={'arg1': 'hello', 'arg2': 'world'})
thread.start()
```

<hr>

### execjs

- get().name

  - 显示当前使用的javascript运行环境。
  - `os.environ["EXECJS_RUNTIME"] = "Node"`: 设置运行环境为NodeJs。

- get()

  - eval("code")

- eval("code")

- compile("code")

  ```python
  ctx = execjs.compole("""
  function add(x, y){
  return x+y;
  }
  """)
  ctx.call("add", 1, 2)
  ```


### requests

- Session()
  - `session = requests.Session()`
  - cookies
    - `session.cookies.update(cookies)`
    - `session.headers = headers`
  - `res = session.post(url, data=data)`

### re

- match

```python
>>> import re
>>> result = re.match("itcast","itcast.cn")
>>> result.group()
'itcast'
```

- findall

```python
>>> import re
>>> ret = re.findall(r"\d+", "python = 9999, c = 7890, c++ = 12345")
>>> print(ret)
['9999', '7890', '12345']
```



<table align="center" cellspacing="0"><tbody><tr><td style="vertical-align:middle;width:54pt;"><span style="color:#000000;">字符</span></td><td style="vertical-align:middle;width:364px;"><span style="color:#000000;">功能</span></td><td style="vertical-align:middle;width:628px;">位置</td></tr><tr><td style="vertical-align:middle;"><span style="color:#000000;">.</span></td><td style="vertical-align:middle;width:364px;"><span style="color:#000000;">匹配任意1个字符（除了\n）</span></td><td style="vertical-align:middle;width:628px;"></td></tr><tr><td style="vertical-align:middle;"><span style="color:#000000;">[<span style="color:#000000;"> ]</span></span></td><td style="vertical-align:middle;width:364px;"><span style="color:#000000;">匹配[ ]中列举的字符</span></td><td style="vertical-align:middle;width:628px;"></td></tr><tr><td style="vertical-align:middle;"><span style="color:#000000;">\d</span></td><td style="vertical-align:middle;width:364px;"><span style="color:#000000;">匹配数字，即0-9</span></td><td style="vertical-align:middle;width:628px;">可以写在字符集[...]中</td></tr><tr><td style="vertical-align:middle;"><span style="color:#000000;">\D</span></td><td style="vertical-align:middle;width:364px;"><span style="color:#000000;">匹配⾮数字，即不是数字</span></td><td style="vertical-align:middle;width:628px;">可以写在字符集[...]中</td></tr><tr><td style="vertical-align:middle;"><span style="color:#000000;">\s</span></td><td style="vertical-align:middle;width:364px;"><span style="color:#000000;">匹配空⽩，即空格，tab键</span></td><td style="vertical-align:middle;width:628px;">可以写在字符集[...]中</td></tr><tr><td style="vertical-align:middle;"><span style="color:#000000;">\S</span></td><td style="vertical-align:middle;width:364px;"><span style="color:#000000;">匹配⾮空⽩字符</span></td><td style="vertical-align:middle;width:628px;">可以写在字符集[...]中</td></tr><tr><td style="vertical-align:middle;"><span style="color:#000000;">\w</span></td><td style="vertical-align:middle;width:364px;"><span style="color:#000000;">匹配单词字符，即a-z、A-Z、0-9、_</span></td><td style="vertical-align:middle;width:628px;">可以写在字符集[...]中</td></tr><tr><td style="vertical-align:middle;"><span style="color:#000000;">\W</span></td><td style="vertical-align:middle;width:364px;"><span style="color:#000000;">匹配⾮单词字符</span></td><td style="vertical-align:middle;width:628px;">可以写在字符集[...]中</td></tr><tr><td style="vertical-align:middle;"><span style="color:#000000;">\w</span></td><td style="vertical-align:middle;width:364px;"><span style="color:#000000;">\w 匹配单词字符，即a-z、A-Z、0-9、_</span></td><td style="vertical-align:middle;width:628px;"></td></tr><tr><td style="vertical-align:middle;"><span style="color:#000000;">\W</span></td><td style="vertical-align:middle;width:364px;"><span style="color:#000000;">匹配⾮单词字符</span></td><td style="vertical-align:middle;width:628px;"></td></tr></tbody></table>

<table align="center" cellspacing="0"><tbody><tr><td style="vertical-align:middle;width:54pt;">字符</td><td style="vertical-align:middle;width:469px;">功能</td><td style="vertical-align:middle;width:142px;">位置</td><td style="vertical-align:middle;width:1px;">表达式实例</td><td style="vertical-align:middle;width:120px;">完整匹配的字符串</td></tr><tr><td style="vertical-align:middle;width:54pt;"><span style="color:#000000;">*</span></td><td style="vertical-align:middle;width:469px;"><span style="color:#000000;">匹配前⼀个字符出现0次或者⽆限次，即可有可⽆</span></td><td style="vertical-align:middle;width:142px;">用在字符或(...)之后</td><td style="vertical-align:middle;width:1px;">abc*</td><td style="vertical-align:middle;width:120px;">abccc</td></tr><tr><td style="vertical-align:middle;"><span style="color:#000000;">+</span></td><td style="vertical-align:middle;width:469px;"><span style="color:#000000;">匹配前⼀个字符出现1次或者⽆限次，即⾄少有1次</span></td><td style="vertical-align:middle;width:142px;">用在字符或(...)之后</td><td style="vertical-align:middle;width:1px;">abc+</td><td style="vertical-align:middle;width:120px;">abccc</td></tr><tr><td style="vertical-align:middle;"><span style="color:#000000;">?</span></td><td style="vertical-align:middle;width:469px;"><span style="color:#000000;">匹配前⼀个字符出现1次或者0次，即要么有1次，要么没有</span></td><td style="vertical-align:middle;width:142px;">用在字符或(...)之后</td><td style="vertical-align:middle;width:1px;">abc?</td><td style="vertical-align:middle;width:120px;">ab,abc</td></tr><tr><td style="vertical-align:middle;"><span style="color:#000000;">{m}</span></td><td style="vertical-align:middle;width:469px;"><span style="color:#000000;">匹配前⼀个字符出现m次</span></td><td style="vertical-align:middle;width:142px;">用在字符或(...)之后</td><td style="vertical-align:middle;width:1px;">ab{2}c</td><td style="vertical-align:middle;width:120px;">abbc</td></tr><tr><td style="vertical-align:middle;"><span style="color:#000000;">{m,n}</span></td><td style="vertical-align:middle;width:469px;"><span style="color:#000000;">匹配前⼀个字符出现从m到n次，若省略m，则匹配0到n次，若省略n，则匹配m到无限次</span></td><td style="vertical-align:middle;width:142px;">用在字符或(...)之后</td><td style="vertical-align:middle;width:1px;">ab{1,2}c</td><td style="vertical-align:middle;width:120px;">abc,abbc</td></tr></tbody></table>

`?P<M>`:`.group("M")`

```python
>>>match("-\d+","-3").group()
>>>'-3'
>>>match("-\d+","L-3").group()
AttributeError: 'NoneType' object has no attribute 'group'
>>>search("-\d+","L-3").group()
>>>'-3'
```

