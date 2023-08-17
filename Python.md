<hr>

[TOC]

<hr>

### [Default]

#### [list]

```python
lst = [1, 2, 3, 2, 4, 1, 5, 6, 5]
duplicates = list(set([x for x in lst if lst.count(x) > 1]))
```

#### [str]

- format():
  - format(float num, "0.2f"): 保留2位小数;
  - format(float num, "^10.10f"): 多占10位空格，"^"代表居中;

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

