<hr>

[TOC]

# Version:1.5 

------

# [- - -短代码块- - -] 



## [C#函数]

<div style="background-color: cyan; height: 2px;"></div>

### Write/WriteLine


```cs
Console.Write("Hello, World");
Console.WriteLine("Hello, World"); // 句末自带'\n'符;
```

<hr>

### ReadKey/KeyChar

```cs
var key = Console.ReadKey(); // 读取输入的一个字符; 
Console.WriteLine((int)key.KeyChar); // 输出读取到的字符的ascii码;
```

<hr>

```cs
public readonly static int x = 1;
```

<hr>

### Thread.Sleep

```cs
using System.Threading;
```


```cs
System.Threading.Thread.Sleep(1000);
Thread.Sleep(1000);
```

<hr>

### Timer

```cs
System.Timers.Timer timer = new System.Timers.Timer(1000);
// 实例化Timer类, 设置间隔为1000毫秒;

timer.Elapsed += new System.Timers.ElapsedEventHandler((object source, System.Timers.ElapsedEventArgs e) => { flg = false; });

timer.AutoReset = false; // 设置是执行一次(false)还是一直执行(true);
timer.Enabled = true; // 是否执行System.Timers.Timer.Elapsed事件;
```

<hr>

### Array.Exists

```cs
using.System;
Debug.Log(Array.Exists(List, e => e == null)); // 判断null是否存在于List;
```

### List<T>.Exists

```cs
List<int> list1 = new List<int>() { 11, 12, 13, 14, 15, 16, 17, 18, 19, 20 };
var bRet= list1.Exists(t => t == 15); // 判断15是否存在于list1;
```

<hr>

## [基础功能]


<div style="background-color: cyan; height: 2px;"></div>


### SceneManager.LoadScene

```cs
using UnityEngine.SceneManagement;
```

```cs
SceneManager.LoadScene("Demo", LoadSceneMode.Additive); // 根据关卡名称加载场景, 不销毁当前场景;世界内容重叠;
SceneManager.LoadScene(SceneManager.GetActiveScene().buildIndex + 1); // 根据关卡索引加载场景; 
```

<hr>

### Invoke/InvokeRepeating

```cs
Invoke("Func", 3); // 方法在3秒后调用;
InvokeRepeating("Func", 3, 1); // 方法在3秒后调用, 每1秒执行一次; 
bool Flag = IsInvoking("Func");
CancelInvoke(); // 取消所有的Invoke/InvokeReprating;
CancelInvoke("Func"); // 取消调用Func;
```

<hr>

## [数学公式]


### [两向量求角]

```cs
float Angle(Vector3 a, Vector3 b)
{
    float dot = Vector3.Dot(a, b);
    float det = (a.x * b.y) - (b.x * a.y);
    return Mathf.Atan2(det, dot) * Mathf.Rad2Deg;
}
```

### [柏林噪声]

```cs
public Vector3[] GetPerlinPositions(int positionCount, float Span = 1f, float Height = 1f, int StartIndex = 0, float Lacunarity = 0.01f, int Seed = 0)
{
	Random.InitState(Seed);
	float RandomOffset = Random.Range(0f, 10000f);
		
	Vector3[] positions = new Vector3[positionCount];
	float sampleHeight = 0f;
		
	for (int i = StartIndex; i < StartIndex + positionCount; i++){
		sampleHeight = Mathf.PerlinNoise(i * Lacunarity + RandomOffset, 0f);
		positions[i - StartIndex] = new Vector3(i * Span, sampleHeight * Height, 0);
	}
	return positions;
}
```



## [物理系统]

<div style="background-color: cyan; height: 2px;"></div>


### Physics2D.Raycast/Debug.DrawRay/Physics2D.CircleCastAll

```cs
RaycastHit2D hit = Physics2D.Raycast (new Vector2 (x, y), new Vector2 (1, 0), 10);
// 从(x,y)的坐标发射一条射线，方向是(1,0)，距离是10; 

RaycastHit store;Ray ray;
if(Phsics.Raycast(ray, out store)){ }
// 若射线ray触发, 函数返回true; 碰撞信息传给store; 

Vector3 forward = transform.TransformDirection(Vector3.left) * 10;
Debug.DrawRay(transform.position, forward, Color.green);
// 每帧中向坐发射可视射线; 

RaycastHit2D hit = Physics2D.Raycast(Camera.main.ScreenToWorldPoint(Input.mousePosition), Vector2.zero);
// 2D鼠标位置射线碰撞self; 从摄像机主屏幕位置发射, 检测鼠标位置处的任何2D碰撞体; 
```

#### Physics2D.Raycast(Vector2 origin, Vector2 direction, float distance)

- origin: 射线起点; 
- direction: 射线发射的起点;
- distance: 射线发射距离;2

#### Debug.DrawRaw(Vector3 start, Vector3 dir, Color color = Color.white, float duration = 0.0f, bool depthTest = true)

- GameScreen中Gizmos选项开启才能显示;
- duration: 取值为0时仅在一帧中出现;  

### Pysics2D.CircleCast(Vector2 origin, float radius, Vector2 direction, float distance = Mathf.Infinity, int layerMask = DafaultRaycastLayers, float minDepth = -Mathf.Infinity, float maxDepth = Mathf.Infinity)

- Pysics2D.CircleCastAll(transform.position, radius, Vector2.zero);

```cs
    public List<GameObject> AttackRange(string tag, float radius)
    {
        RaycastHit2D[] hits = Physics2D.CircleCastAll(transform.position, radius, Vector2.zero);
        List<GameObject> DestObject = new List<GameObject>();
        foreach (RaycastHit2D hit in hits)
        {
            if (hit.collider.gameObject.CompareTag(tag))
            {
                DestObject.Add(hit.collider.gameObject);
            }
        }
        if (DestObject.Count > 0)
        {
            return DestObject;
        }
        return null;
    }
```

<hr>

### Rigidbody.AddForce / AddTorque

```cs
public Rigidbody rb;
// public void AddForce(Vector3 force, ForceMode mode = ForceMode.Force);
rb.AddForce(100, 0, 0);
// public void AddTorque(Vector3 torque, ForceMode mode = ForceMode.Force); (施加旋转力，旋转方向按左手定则);
rb.AddTorque(100, 0, 0);
```

#### ForceMode

- 公式: Ft = mv(t); v(t) = Ft / m;
- ForceMode.Force: 持续施加一个力, 与重力mass有关, t = 每帧间隔时间, m = mass;
- ForceMode.Impulse: 瞬间施加一个力, 与重力mass有关, t = 1.0f, m = mass;
- ForceMode.Acceleration: 持续施加一个力, 与重力mass无关, t = 每帧间隔时间, m = 1.0f;
- ForceMode.VelocityChange: 瞬间施加一个力, 与重力mass无关, t = 1.0f, m = 1.0f;

<hr>
## [特殊语法]

<div style="background-color: cyan; height: 2px;"></div>

### public static Demo Instance

```cs
class Demo{
    public static Demo Instance;
    void Awake(){
        // Start晚于Awake; 使用Start赋值Instance可能在调用时报空;
        Instance = this;
    }
}
```

<hr>

### public int num {get; private set;}

- 将具有公有权限的变量设置为禁止外界改变取值;

<hr>

### [Coroutine(协程)]


#### [StartCoroutine]


- public Coroutine StartCoroutine(IEnumerator routine);
- 协同程序执行时可在任意位置是同yield语句;
- yield返回值控制何时恢复协同程序向下执行;

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Test : MonoBehaviour
{
    void Start()
    {
        StartCoroutine(Wait(2f));
    }
    IEnumerator Wait(float TheTime)
    {
        yield return new WaitForSeconds(TheTime);
        print("2秒后");
    }
}

```

#### [Yield]

- `yield return new WaitForSeconds(3.0f);`: 等待3秒;
- `yield return null;` / `yield return 0;`: 暂停当前这一帧, 下一帧继续运行下一句;
- `yield return new WaitForEndOfFrame();`: 等到当前这一帧的cameras和GUI渲染结束后再继续执行;
- `yield return new WaitForFixedUpdate();`: 在下一次执行FixedUpdate时继续执行; 即等待一次物理引擎的更新;
- `yield return www;`: 等待直至异步下载完成;
- `yield break;`: 跳出协程;
- `yield return StartCoroutine(Func);`: 等待指定的另一个协程执行完再继续执行;

#### [StopAllCoroutines]

- 停止当前对象中全部已开始的协程;
- 对于其他类中的协程不起作用;

#### [StopCoroutine]

```cs
StartCoroutine("First");
StartCoroutine("Second");

StopCoroutine("First");
```

- 仅能停止通过传入字符串而开始的协程;

#### [嵌套协程]

```cs
IEnumerator Sleep(float duration){
    for (float timer = 0; timer < duration; timer += Time.deltaTime) yield return 0;
}
```

```cs
void Start(){
    StartCoroutine(Main());
}
IEnumerator Main(){
    Debug.Log("Start");
    Yield return StartCoroutine(Sleep(1f));
    Debug.Log("After 1s");
    Yield return StartCoroutine(Sleep(2.5f));
    Debug.Log("After 2.5s");
}
```

<hr>

### [Enum(枚举)]

- 默认递增取值;

```cs
public enum Direction{
    up, // 0 
    Down, // 1
    Left, // 2
    Right, // 3
}
```

```cs
public enum Categories: int{
    A, // 0
    B, // 1
    C = 6, // 6
    D, // 7
    E, // 8
}
```

- 枚举可以是任何数字数据类型，例如 byte，sbyte，short，ushort，int，uint，long 或 ulong。但是，枚举不能为字符串类型。

### [delegate(委托)]

```cs
public delegate void Func(int x);
void Start(){
    Func func;
    func = Test;
    func(1);
}
void Test(int x){
    print(x);
}
```

```cs
public delegate void Action();
public void Func(){    
    StartCoroutine(Delay.Do(delegate
    {
        // TODO;
    }, 3f));
}
public class Delay : MonoBehaviour
{
    public static IEnumerator Do(Action action, float delaySeconds)
    {
        yield return new WaitForSeconds(delaySeconds);
        action();
    }
}
```

<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

[TOC]


<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

# [- - -方法函数- - -]

## [基础功能]

### {System}

#### DataTime

- DateTime(int year, int mouth, int day, int hour, int minute, int second, DateTimeKind kind);
- public DateTime(int year, int month, int day, int hour, int minute, int second, int millisecond, DateTimeKind kind);
- public DateTime(int year, int month, int day, int hour, int minute, int second, int millisecond, Calendar calendar, DateTimeKind kind);

##### [DataTime转换long(时间戳)]

```cs
public static long DateTimeToLong(System.DateTime time)
{
    System.DateTime dateTime= TimeZone.CurrentTimeZone.ToLocalTime(new System.DateTime(1970, 1, 1, 0, 0, 0, 0));
    long date = (time.Ticks - dateTime.Ticks) / 10000;   //除10000调整为13位      
    return date ;
}
```

##### [long(时间戳转换DataTime)]

```cs
public static DateTime LongToDateTime(long date)
{
        System.DateTime dateTime = TimeZone.CurrentTimeZone.ToLocalTime(new System.DateTime(1970, 1, 1));
        //dateTime = dateTime.AddMilliseconds(date);
        //return dateTime ;

        TimeSpan toNow = new TimeSpan(long.Parse(date + "0000"));
        dateTime = dateTime.Add(toNow);
        return dateTime ;
}
```

- Now -> 05/07/2023 12:15:22;

  - .ToString(string sign) -> 2023/5/7 12:23:20;

    - "t" -> 12:24;
    - "T" -> 12:24:26;
    - "d" -> 2023/5/7;
    - "D" -> 2023年5月7日;
    - "f" -> 2023年5月7日 12:26;
    - "F" -> 2023年5月7日 12:26:32;
    - "g" -> 2023/5/7 12:28;
    - "G" -> 2023/5/7 12:28:05;
    - "m" -> 5月7日;
    - "r" -> Sun, 07 May 2023 12:29:13 GMT;
    - "s" -> 2023-05-07T12:29:13;
    - "u" -> 2023-05-07 12:31:28Z;
    - "U" -> 2023年5月7日 4:31:28;
    - "y" / "Y" -> 2023年5月;

    <hr>

    - "dddd" -> 星期日;
    - "ddd" -> 周日;
    - "dd" -> 07;
    - "d" -> 7;
    - "MMMM" -> 五月;
    - "MMM" -> 5月;
    - "MM" -> 05;
    - "M" -> 5;
    - "yyyy" / "yyy"-> 2023;
    - "yy" / "y" -> 23;

#### Random

##### [构造函数]

- Random();

- Random(Int32): 参数作为种子值;

  - Next(): 每次产生一个不同的随机正整数;

    ```cs
    Random Ran = new Random();
    int num = Ran.Next(); // 2114319875
    ```

  - Next(int max): 产生一个比max小的正整数;

    ```cs
    Random Ran = new Random();
    int num = Ran.Next(10); // num >= 0 && num < 10;
    ```

  - Next(int min, int max);

    ```cs
    Random Ran = new Random();
    int num = Ran.Next(10, 100);
    ```

  - NextDouble();

  - NextBytes(byte[]);

#### [String]

- Length;
- ToUpper();
- ToLower();
- Equals(string Ano, StringComparison Opt);
- Split(char[] chs, StringSplitOptions Opt):
  - StringSplitOptions.RemoveEmptyEntries: 移除空格;
- SubString(int StartIndex, 'Len):
  - StartIndex: 要进行截取的开始下标; 保留字符串中下标从StartIndex开始后面的全部字符串;
  - Len: 要截取的长度; 保留字符串中下标从StartIndex开始后面的Len个长度的字符串;
- IndexOf(): 判断某个字符串在字符串中第一次出现的位置，如果没有返回-1、值类型和引用类型在内存上存储的地方不一样。
- LastIndexOf(): 判断某个字符串在字符串中最后一次出现的位置，如果没有同样返回-1;
- StartsWith(): 判断是否以…开始;
- EndsWith(): 判断是否以…结束;
- Replace(): 将字符串中某个字符串替换成一个新的字符串;
- Contains(): 判断某个字符串是否包含指定的字符串;
- Trim('Char[] chs): 去掉字符串中前后的空格:
  - chs: 想要去掉的字符数组; 去掉字符串开始处和结尾处char[]中的所有字符。
- TrimEnd(): 去掉字符串中结尾的空格;
- TrimStart(): 去掉字符串中前面的空格;
- Insert(int Index, string Content);
- Remove(int StartIndex, 'int Len);
- PadLeft(int num): 左对齐; 空格补齐左对齐;
- PadRight(int num): 右对齐;

#### string

- IsNullOrEmpty(): 判断一个字符串是否为空或者为null;
- String.Join(SplitCh, array): 将字符串书组合并成一个字符串，每个元素之间用SplitCh隔开;
  - SplitCh: 合并后的分隔符;
  - array: 要合并的字符串数组; 
- Concat(str1, str2, …., strn): 将n个字符串连接，中间没有连接符;
- Format(string Flag, int num):
  - string str1 =string.Format("{0:N1}",56789); //result: 56,789.0
  - string str2 =string.Format("{0:N2}",56789); //result: 56,789.00
  - string str3 =string.Format("{0:N3}",56789); //result: 56,789.000
  - string str8 =string.Format("{0:F1}",56789); //result: 56789.0
  - string str9 =string.Format("{0:F2}",56789); //result: 56789.00
  - string str11 =(56789 / 100.0).ToString("#.##"); //result: 567.89
  - string str12 =(56789 / 100).ToString("#.##"); //result: 567
  - string.Format("{0:C}",0.2); //result: ￥0.20 (英文操作系统结果: $0.20); 默认格式化小数点后面保留两位小数，如果需要保留一位或者更多，可以指定位数;
  - string.Format("{0:C1}",23.15); //result: ￥23.2 (截取会自动四舍五入)
  - string.Format(“市场价：{0:C}，优惠价{1:C}”,23.15,19.82)
  - string.Format("{0:D3}",23) //result：023
  - string.Format("{0:D2}",1223) //result：1223
  - string.Format("{0:N}", 14200) //result：14,200.00 (默认为小数点后面两位)
  - string.Format("{0:N3}", 14200.2458) //result：14,200.246 (自动四舍五入)
  - string.Format("{0:P}", 0.24583) //result：24.58% (默认保留百分的两位小数)
  - string.Format("{0:P1}", 0.24583) //result：24.6% (自动四舍五入)
  - string.Format("{0:d}",System.DateTime.Now) //result：2009-3-20 (月份位置不是03)
  - string.Format("{0:D}",System.DateTime.Now) //result：2009年3月20日
  - string.Format("{0:f}",System.DateTime.Now) //result：2009年3月20日 15:37
  - string.Format("{0:F}",System.DateTime.Now) //result：2009年3月20日 15:37:52
  - string.Format("{0:g}",System.DateTime.Now) //result：2009-3-20 15:38
  - string.Format("{0:G}",System.DateTime.Now) //result：2009-3-20 15:39:27
  - string.Format("{0:m}",System.DateTime.Now) //result：3月20日
  - string.Format("{0:t}",System.DateTime.Now) //result：15:41
  - string.Format("{0:T}",System.DateTime.Now) //result：15:41:50;

#### Collections.Generic

##### List<T>

- `List<int> list1 = new List<int> { 1, 2, 3, 4, 5, };`
- Add(T Ele): 添加一个元素;
- AddRange(T[] Eles): 添加一组元素; `string[] Arr = { "Ha","Hunter", "Tom", "Lily", "Jay", "Jim", "Kuku",  "Locu" };list.AddRange(Arr);`
- Insert(int Index, T Ele);
- ForEach((i) => { });
- Remove(T Ele);
- RemoveAt(int Index);
- RemoveRange(int StartIndex, int RemoveNum);
- Clear();
- bool Contains(T Ele);
- bool Equals(List<T> Ano);
- int CompareTo();
- IndexOf(T Ele);
- Reverse();
- ToArray();
- Count;
- Capacity;

<div style="background-color: cyan; height: 2px;"></div>

### {Message}

<hr>

- Awake(): 当物体载入时调用一次; 
- OnEnable(): 脚本对象启用时调用; 
- Start(): 物体载入且脚本对象启用时调用;

<hr>

- FixedUpdate(): 固定时间调用, 默认0.02s; 设置: Project -> Time -> Fixed TimeStep; 
- Update(): 每次渲染场景(每帧)时调用; 
- LateUpdate(): 在每次Update函数调用之后执行; 
- OnGUI(): 渲染和处理GUI事件时调用; 每帧调用多次; 

<hr>

- OnBecameVisible(): 当MeshRenderer在任何相机上可见时调用; 
- OnBecameInvisible(): 当MeshRenderer在任何相机上不可见时调用; 
- OnDisable(): 禁用当前脚本时调用; 对象变为不可用和附属游戏对象非激活状态时调用; 
- OnDestroy(): 物体销毁时调用; 脚本销毁或附属的游戏对象销毁时调用; 
- OnApplacationQuit(): 应用程序退出时调用;

<hr>

#### Box Collider (2D)

- OnMouseOver(): 鼠标停留; 
- OnMouseEnter(): 鼠标进入; 
- OnMouseExit(): 鼠标离开; 
- OnMouseDown(): 鼠标按下; 
- OnMouseUp(): 鼠标抬起; 
- OnMouseDrag(): 鼠标拖拽;
- OnMouseUpAsButton(): 相当于按钮功能; 当鼠标在同一个游戏物体上按下抬起时触发; 若按下和抬起不在同一个游戏对象则不触发; 

<hr>

#### Rigidbody

- OnCollisionEnter(Collision collision){ }

  - 碰撞时触发;

  - 碰撞双方必须是碰撞体;
  - 碰撞的主动方必须是刚体，注意我的用词是主动方，而不是被动方;
  - 刚体不能勾选IsKinematic;
  - 碰撞体不能够勾选IsTigger;

- OnTriggerEnter(Collider collision){ }

  - 触发器重叠触发;

- OnCollisionExit(Collision collision){ }

- OnTriggerExit(Collider collision){ }

<hr>

#### Rigidbody2D


- OnCollisionEnter2D(Collision2D collision){ }
  - 碰撞时触发;
- OnTriggerEnter2D(Collider2D collision){ }
  - 触发器重叠触发;
- OnCollisionExit2D(Collision2D collision){ }
- OnTriggerExit2D(Collider2D collision){ }

<hr>

#### ParticleSystem

- void OnParticleCollision(GameObject other){ }
  - 粒子系统开启Collision选项后开启Send Collision Messages选项后开始触发;

<hr>

#### CharacterController

- private void OnControllerColliderHit(ControllerColliderHit hit){ }

  ```cs
  using UnityEngine;
  public class Example : MonoBehaviour
  {
      // this script pushes all rigidbodies that the character touches
      float pushPower = 2.0f;
      void OnControllerColliderHit(ControllerColliderHit hit)
      {
          Rigidbody body = hit.collider.attachedRigidbody;
          // no rigidbody
          if (body == null || body.isKinematic)
          {
              return;
          }
          // We dont want to push objects below us
          if (hit.moveDirection.y < -0.3)
          {
              return;
          }
          // Calculate push direction from move direction,
          // we only push objects to the sides never up and down
          Vector3 pushDir = new Vector3(hit.moveDirection.x, 0, hit.moveDirection.z);
          // If you know how fast your character is trying to move,
          // then you can also multiply the push velocity by that.
          // Apply the push
          body.velocity = pushDir * pushPower;
      }
  }
  ```

### {EventSystems}


- #### {IPointerDownHandler}

  - **public** OnPointerDown(PointerEventData Data):点击时触发;

- #### {IPointerEnterHandler}

  - **public** OnPointerEnter(PointerEventData Data)

- #### {IPointerExitHandler}

  - **public** OnPointerExit(PointerEventData Data)
  
- PointerEventData

```
Position: (783.36, 184.16)
delta: (0.00, 0.00)
eligibleForClick: True
pointerEnter: Image (UnityEngine.GameObject)
pointerPress: 
lastPointerPress: Image (UnityEngine.GameObject)
pointerDrag: 
Use Drag Threshold: True
Current Raycast:
Name: Image (UnityEngine.GameObject)
module: Name: Canvas (UnityEngine.GameObject)
eventCamera: Main Camera (UnityEngine.Camera)
sortOrderPriority: -2147483648
renderOrderPriority: -2147483648
distance: 108.3208
index: 0
depth: 0
worldNormal: (0.00, 0.00, -1.00)
worldPosition: (-18.89, -37.05, 90.00)
screenPosition: (783.36, 184.16)
module.sortOrderPriority: -2147483648
module.renderOrderPriority: -2147483648
sortingLayer: 0
sortingOrder: 0
Press Raycast:
Name: Image (UnityEngine.GameObject)
module: Name: Canvas (UnityEngine.GameObject)
eventCamera: Main Camera (UnityEngine.Camera)
sortOrderPriority: -2147483648
renderOrderPriority: -2147483648
distance: 108.3208
index: 0
depth: 0
worldNormal: (0.00, 0.00, -1.00)
worldPosition: (-18.89, -37.05, 90.00)
screenPosition: (783.36, 184.16)
module.sortOrderPriority: -2147483648
module.renderOrderPriority: -2147483648
sortingLayer: 0
sortingOrder: 0
pressure: 0
tangentialPressure: 0
altitudeAngle: 0
azimuthAngle: 0
twist: 0
tilt: (0.00, 0.00)
penStatus: None
radius: (0.00, 0.00)
radiusVariance: (0.00, 0.00)
```

<div style="background-color: cyan; height: 2px;"></div>

### {Events}

#### [UnityEvent]

- 构造函数

  - UnityEvent()

    ```cs
    UnityEvent Eve = new UnityEvent();
    void Start(){
        Eve.AddListener(TODO);
    }
    void TODO(){
        // TODO;
    }
    void OnCollisionEnter(Collision Coll){
        Eve.Invoke();
    }
    ```

  - UnityEvent<T0>()

    ```cs
    public UnityEvent<int> Eve;
    ```

  - UnityEvent<T0,T1>()

  - UnityEvent<T0,T1,T2>()

  - UnityEvent<T0,T1,T2,T3>()

- AddListener(Call)

  - 向UnityEvent添加非持久性监听器; 

  - Call:回调函数; 

- Invoke()

- RemoveListener(Events.UnityAction Call)

- int GetPersistentEventCount()

  - 获取已注册的持久性监听器的数量;

- string GetPersistentMethodName(int index)

  - 获取索引处监听器目标方法的名称;

- Object GetPersistentTarget(int index)

  - 获取索引处监听器的目标组件;

- RemoveAllListeners()

- SetPersistentListenerState(int index, Events.UnityEventCallState state)


<div style="background-color: cyan; height: 2px;"></div>

## [插件扩展]

### {DG.Tweening}

- #### DOTween

  - ##### Init(bool recycleAllByDefault, bool useSafeMode, LogBahavior logBehavior)

    - recycleAllByDefault: 取值true则所有动画补间将会在调用完后回收放入一个对象池而不是直接销毁;
    - useSafeMode: 取值true则补间变慢; 对象被销毁后补间仍然执行;
    - logBehaviour: LogBehaviour.ErrorsOnly-只记录错误; LogBehaviour.Default-记录错误和警告; LogBehaviour.Verbose-记录全部内容;

- #### transform

  ```cs
  transform.DOMove(new Vector3(10, 0, 0), 10, false);
      作用：移动到某一指定点。(世界坐标)
  	参数：
  	     Vector3 to               要移动到的位置
  	     float   duration         所需要花费的时间
  	     bool    snapping         为true时平滑地将所有值变为整数。(每次移动整数值)默认为false
  transform.DOMoveX()/DOMoveY()/DOMoveZ(10, 10f,false);
   	作用：沿着某一轴移动到指定位置。
  	参数:
  		 float   to				  要移动到的轴的坐标
  		 float   duration         所需要花费的时间
  		 bool    snapping         为true时平滑地将所有值变为整数。(每次移动整数值)默认为false
  transform.DOLocalMove(new Vector3(10,0.5f,0),10f,false);
   	作用：移动自身坐标到指定位置。
   	参数：
   	Vector3 to               要移动到的位置
  	     float   duration         所需要花费的时间
  	     bool    snapping         为true时平滑地将所有值变为整数。(每次移动整数值)默认为false
  transform.DOLocalMoveX()/DOLocalMoveY()/DOLocalMoveZ();
  	作用：移动自身坐标到指定轴的指定位置。
  	参数:
  		 float   to				  要移动到的轴的坐标
  		 float   duration         所需要花费的时间
  		 bool    snapping         为true时平滑地将所有值变为整数。(每次移动整数值)默认为false
  transform.DOJump(new Vector3(10, 0, 0),10,3,10,false);
  	作用：实现跳跃到指定位置。
  	参数：
  		 Vector3 endValue         最终要跳跃到的位置
  		 float   jumpPower        跳跃的强度，决定跳跃的高度(当前位置Y加上该值)
  		 int     numJumps         跳跃的次数
  		 float   duration         总持续时间
  		 bool    snapping         为true时平滑地将所有值变为整数。(每次移动整数值)默认为false
  transform.DOLocalJump(new Vector3(10, 0, 0),10,3,10,false);
      作用：实现跳跃到指定位置（自身坐标）。
  	参数：
  		 Vector3 endValue         最终要跳跃到的位置
  		 float   jumpPower        跳跃的强度，决定跳跃的高度(当前位置Y加上该值)
  		 int     numJumps         跳跃的次数
  		 float   duration         总持续时间
  		 bool    snapping         为true时平滑地将所有值变为整数。(每次移动整数值)默认为false
  
  ```

  <hr>

  ```cs
  transform.DORotate(Rote, 0.1f, RotateMode.Fast);
  	作用：旋转到指定的值（根据欧拉角）。
  	参数：
  	     Vector3 to               旋转目标值
  		 float   duration         总旋转用时
  		 RotateMode
  		 	     Fast             旋转采用最短路线，切旋转不会超过360°
  		 	     FastBeyond360    旋转将超过360°
  		 	     WorldAxisAdd     类似于使用transform.Rotate(new Vector3(20, 0, 0)，Space.World)，最终值始终被视为相对值
  		 	     LocalAxisAdd     类似于使用transform.Rotate(new Vector3(20, 0, 0)，Space.Self)，最终值始终被视为相对值
  transform.DORotateQuaternion();
  	作用：旋转到指定的值（四元数）。
  	参数：
  		 Quaternion  to            要旋转到的四元数值
  		 float   duration          旋转用时
  transform.DOLocalRotate();
  	作用：自身坐标旋转。
  transform.DOLocalRotateQuaternion();
  	作用：自身坐标旋转。
  transform.DOLookAt();
  	作用：旋转目标，使其朝向给定位置。
  	参数：
  		 Vector3			 towards			旋转目标值
  		 float	    		 duration			旋转总用时
  		 AxisConstraint		 axisConstraint 	旋转最终轴约束，只旋转此轴
  		 Vector3             up                 定义向上方向的矢量
  transform.DODynamicLookAt();
  	作用：旋转目标，使其朝向给定位置，每帧更新 lookAt 位置（与此相反，当补间开始时，只计算一次 lookAt 旋转）
  	参数：
  		 Vector3			 towards			旋转目标值
  		 float	    		 duration			旋转总用时
  		 AxisConstraint		 axisConstraint 	旋转最终轴约束，只旋转此轴
  		 Vector3             up                 定义向上方向的矢量
  
  ```

  <hr>

  ```cs
  DOScale();
  	作用：将物体放大/缩小到指定大小
  	参数：
  	float/Vector3 			to					浮点数为倍数，向量为指定大小
  	float 					duration			放大/缩小总消耗时间
  DOScaleX/DOScaleY/DOScaleZ();
  	作用：对某一轴方向进行放大缩小
  	float					to					放大到的倍数
  	float 					duration			放大/缩小总消耗时间
  ```

  <hr>

  ```cs
  DOPunchPosition();
  	作用:受到冲击后的回弹效果
  	参数：
  	Vector3					punch 				要被击打到的最远位置（相对值，相对于局部坐标）
  	float					duration			总持续时间
  	int						vibrato				物体振动频率
  	float					elasticity			值一般在0到1之间，0表示起点到冲击方向的震荡，1表示为一个完整的震荡，可能会超过起点，个人感觉后者效果更好。
  	bool					snapping			是否进行平滑插值
  	DOPunchRotation()
  	作用：受到冲击后旋转效果
  	参数：
  	Vector3					punch 				要被击打到的角度（相对值，相对于局部坐标）
  	float					duration			总持续时间
  	int						vibrato				物体旋转频率
  	float					elasticity			值一般在0到1之间，0表示最初角度到最大角度的旋转，1表示为一个完整的旋转，可能会超过最远角度。
  	DOPunchScale()
  	作用：实现一个弹性效果，反复弹，最终复原。
  	参数
  	Vector3					punch 				弹到的大小
  	float					duration			总持续时间
  	int						vibrato				物体放缩频率
  	float					elasticity			值一般在0到1之间，0表示最初角度到目标大小的放缩，1会产生负值，出现警告。
  
  ```

  - DOShakePosition(flaot time, Vector3 Vec, int Num)

  ```cs
  //持续时间,其余默认
  transform.DOShakePosition(1);
  //持续时间、强度（下为只在X、Y方向上震动）
  transform.DOShakePosition(1,new Vector3(3,3,0));
  //持续时间、强度（下为只在X、Y方向上震动）; 仅摇晃三次
  transform.DOShakePosition(1,new Vector3(3,3,0), 3);
  ```

#### Tweener

  - From(bool)
    -  默认false-绝对坐标移动; 
    - true-相对坐标移动; 
    - DOMove函数默认是从当前位置运行到目标位置, 加上From()方法以后表示从目标位置移动到当前位置; 
    - 参数为true表示目标为相对位置, 即目标位置 = 目标位置+当前位置; 
  - SetAutoKill(false);
  - Pause()
  - DOKill()
  - DOPlay()
    - 播放一次，再次调用不可播放;
  - DOPlayForward()
    - 向前播放动画;
  - DOPlayBackwards()
    - 倒放;
  - DORestart()
    - 重新播放动画;

<hr>

- SetEase(Ease.Linear)
- SetLoops(int)
  - 播放次数;
- OnComplete(Func)
- OnKill(Func)
- OnPlay(Func)
- OnPause(Func)
- OnRewind(Func)
  - 动画重置时调用;
- OnStart(Func)

<hr>

#### Text

- DOText("Content", 3)
  - 若文本框内无文字，在3s内逐字显示文字; 
  - 若有文字，则逐字覆盖掉原先文字，显示新文字;
- DOColor(Color.red, 2)
  - 在2s中将原本颜色变为红色;
- DOFade(1, 3)
  - 文字透明度在3秒内从0变为1;

<div style="background-color: cyan; height: 2px;"></div>


### {Rendering}

- #### Postprocessing

  - `using UnityEngine.Rendering.Postprocessing;`

  - ##### [Vignette]
  
    ```cs
        [Range(0f, 1f)]
        public float VignetteStep = 0.01f;
        public float VignetteInit = 0f;
        private PostProcessVolume m_Volume;
        [HideInInspector]
        public Vignette m_Vignette;
        public GameObject PostProcessObject;
    ```
  
    ```cs
    void Awake()
        {
            m_Vignette = ScriptableObject.CreateInstance<Vignette>();
            m_Vignette.enabled.Override(true);
            m_Vignette.intensity.Override(VignetteInit);
            m_Volume = PostProcessManager.instance.QuickVolume(PostProcessObject.layer, 100f, m_Vignette);
        }
    ```
  
    ```cs
        private IEnumerator VignetteBegin(string OnFinish = null, float Delay = 0f)
        {
            for (int i = 0; i < (1f / VignetteStep); i++)
            {
                if (m_Vignette.intensity > 0)
                {
                    m_Vignette.intensity.Override(m_Vignette.intensity - VignetteStep);
                }
                yield return null;
            }
            if (OnFinish != null) Invoke(OnFinish, Delay);
        }
        private IEnumerator VignetteEnd(string OnFinish = null, float Delay = 0f)
        {
            for (int i = 0; i < (1f / VignetteStep); i++)
            {
                if (m_Vignette.intensity < 1)
                {
                    m_Vignette.intensity.Override(m_Vignette.intensity + VignetteStep);
                    yield return null;
                }
            }
            if (OnFinish != null) Invoke(OnFinish, Delay);
        }
    ```

  - ##### [DepthOfField]
  
    ```cs
        [Range(0f, 1f)]
        public float DepthOfFieldStep = 0.01f;
        public int DepthOfFieldInit = 0;
        private PostProcessVolume m_Volume;
        [HideInInspector]
        public DepthOfField m_Vignette;
        public GameObject PostProcessObject;
    ```
  
    ```cs
    void Awake()
        {
            m_DepthOfField = ScriptableObject.CreateInstance<DepthOfField>();
            m_DepthOfField.focalLength.Override(DepthOfFieldInit);
            m_DepthOfField.enabled.Override(true);
            m_Volume = PostProcessManager.instance.QuickVolume(PostProcessObject.layer, 100f, m_DepthOfField);
        }
    ```
  
    ```cs
    private IEnumerator DepthOfFieldBegin(string OnFinish = null, float Delay = 0f)
        {
            for (int i = 0; i < (50f / DepthOfFieldStep); i++)
            {
                if (m_DepthOfField.focalLength > 0)
                {
                    m_DepthOfField.focalLength.Override(m_DepthOfField.focalLength - DepthOfFieldStep);
                    yield return null;
                }
            }
            if (OnFinish != null) Invoke(OnFinish, Delay);
        }
    private IEnumerator DepthOfFieldEnd(string OnFinish = null, float Delay = 0f)
        {
            for (int i = 0; i < (50f / DepthOfFieldStep); i++) 
            {
                if (m_DepthOfField.focalLength < 50)
                {
                    m_DepthOfField.focalLength.Override(m_DepthOfField.focalLength + DepthOfFieldStep);
                    yield return null;
                }
            }
            if (OnFinish != null) Invoke(OnFinish, Delay);
        }
    ```


<div style="background-color: cyan; height: 2px;"></div>

### {RectTransformExtensions}

```cs
public static class RectTransformExtensions
{

    public static bool Overlaps(this RectTransform a, RectTransform b)
    {
        return a.WorldRect().Overlaps(b.WorldRect());
    }
    public static bool Overlaps(this RectTransform a, RectTransform b, bool allowInverse)
    {
        return a.WorldRect().Overlaps(b.WorldRect(), allowInverse);
    }

    public static Rect WorldRect(this RectTransform rectTransform)
    {
        Vector2 sizeDelta = rectTransform.sizeDelta;
        float rectTransformWidth = sizeDelta.x * rectTransform.lossyScale.x;
        float rectTransformHeight = sizeDelta.y * rectTransform.lossyScale.y;

        Vector3 position = rectTransform.position;
        return new Rect(position.x + rectTransformWidth * rectTransform.pivot.x, position.y - rectTransformHeight * rectTransform.pivot.y, rectTransformWidth, rectTransformHeight);
    }
}
```

<div style="background-color: cyan; height: 2px;"></div>

### iTween

#### [模板]

- iTween.MoveTo(Object, iTween.Hash("position", new Vector3(0f, 0f, 0f),"time", 5f, "easetype", iTween.EaseType.linear)): 基本移动;

- iTween.ValueTo(gameObject, 

  iTween.Hash(

  "from", fromY,

  "to", toY, 

  "easetype", easeType,

  "looptype", loopType,

  "onupdate", "onupdate",

  "time", Time)): 数值过度;

- iTween.ShakePosition(target, Vector3(0, 0.1, 0), 1): 振动;

#### [函数]

- MoveBy();
- MoveFrom();
- MoveTo();
- MoveUpdate();
- FadeTo();
- FadeFrom();
- CameraFadeAdd(blackScreen, 99): 创建一个对象模拟摄像机的淡入淡出;
- Stop("name"): 根据名称停止对应脚本;

#### [参数]

- "y": 设置每帧移动步长; 表示移动的位置; x:float or double; y: float or double; z: float or double;
- ”name": 指定名称用于Stop()函数; string;
- "position": 移动的位置; Transform or Vector3;
- "path": 移动路径; Transform[] or Vector3[] or List\<Vector3\>;
- "looktarget": 移动过程中面朝一个点; Transform or Vector3;
- "looktime": 看向"looktarget"的速度; float or double;
- "axis": 限制仅在指定的轴上旋转; "x" or "y" or "z";
- "onstart": 开始移动时调用; string;
- "onstarttarget": 接受方法的对象, 默认自身; GameObject;
- "onstartparams": onstart方法调用的方法; Object; Start(float f);
- "onupfate": 移动中调用的方法;
- "onupdatetarget": GameObject;
- "onupdateparams": Object;
- "oncomplete": 移动结束调用的方法;
- "oncompletetarget": GameObject;
- "oncompleteparams": Object;
- easeType: 运动线性模型;
  - iTween.EaseType.easeOutQuad: 曲线模型;
  - iTween.EaseType.linear: 线性; 匀速;
  - ......
- "time": 运动时间;
- "delay": 延迟;
- "alpha": 透明度;
- "looptype": 循环方式;
  - iTween.LoopType.pingPong: 来回循环;
  - none: 不循环;
  - loop: 退回重新开始;
- "movetopath";
  - true: 按照路径循环移动时移动完成回到原点; 先从原始位置走到路径中第一个点的位置;
  - false;
- "orienttopath";
  - true: 让模型 始终面朝当前目标方向, 拐弯时自动旋转模型;

#### EaseType:

<img src = "/EaseType.png" />

<div style="background-color: cyan; height: 2px;"></div>

### {TMPro}

```html
粗体 <b>Bold</b>
倾斜<i>Italics</i>
字体大小<size=48>Point size 48</size>
字体大小（百分比）<size=80%>Point size </size>Point size;
字体大小（微调）<size=+40>Point size increased by 18</size>
<size=-40>Point size increased by 18</size>
下划线<u>UnderLine</u>
上标 2<sup>n</sup>即2n;
下标<sub>1</sub>
对齐<align=center></align>left和right分别为居左和居右，justified为自适应填满整个显示区域，除了最后一行 ,flush为填满整个显示区域，包括最后一行;
全部大写<allcaps>all Caps</allcaps>
<uppercase>uppercase</uppercase>
全部小写<lowercase>LOWERCASE</lowercase>
字符间距<cspace=1em>Spacing</cspace>
缩进<indent=50%>indent</indent>
行高<line-height=50%>Hello world</line-height>
行缩进<line-indent=15%></line-indent>
边距<margin=0.5em>设置边距<margin-right=0.5em>marhin可以增加-right或-left来指定左边距还是右边距;
标识<mark=#ffff00aa>Mark</mark>
行等宽字体<mspace=1em>Any font can become monospace</font>
不换行<nobr>can't be sent</nobr>
水平位置<pos 50%>hello;
水平间距Give me some <space=1em>space;
旋转<rotate="-10">Hello;
删除线<s>Strikethrough</s>
下划线<u>Underline</u>
颜色<color=yellow>Color</color>
<color=#FF0000>Color</color>
颜色渐变<gradient="BlueToRed">any</gradient>
动态表情 <sprite=1 anim="1,10,20">
设置透明度<alpha=#82>This a Center Position Tex;
不解析<noparse><b></noparse>
分页符<page>需要将Overflow设置成page;
————————————————
版权声明：本文为CSDN博主「Unity_Kane」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_40833062/article/details/129276352
```

#### [TMP_Text]

- ForceMeshUpdate(): 刷新文字Mesh;

- UpdateGeometry(Mesh mesh, int index);

- ##### textInfo: 文字信息;

  - characterCount: 字符数; 未ForceMeshUpdate时返回0; 包括回车符; 不包括超文本标签;

  - characterInfo: 返回CharacterInfo[]数组; 长度为包括超文本标签的全部字符长度; 

  - ###### characterInfo[i]:

    - isVisible: 字符是否可见;
    - materialReferenceIndex;
    - vertexIndex;

  - meshInfo: 返回MeshInfo[]数组;

  - ###### meshInfo[i]:

    - vertices: 获取顶点信息; 返回Vector3[]数组; Length Demo: 72;
    - mesh: 返回UnityEngine.Mesh对象;

```cs
// 上下波动
using UnityEngine;
using TMPro;
public class TMP_Wave : MonoBehaviour
{
    public TMP_Text tmp;
    void Update()
    {
        tmp.ForceMeshUpdate();

        var textInfo = tmp.textInfo;

        for (int i = 0; i < textInfo.characterCount; i++)
        {
            var charInfo = textInfo.characterInfo[i];
            if (!charInfo.isVisible) continue;

            var verts = textInfo.meshInfo[charInfo.materialReferenceIndex].vertices;
            for (int j = 0; j < 4; j++)
            {
                var orig = verts[charInfo.vertexIndex + j];
                verts[charInfo.vertexIndex + j] = orig + new Vector3(0, Mathf.Sin(Time.time * 3f + orig.x * 1.0f) * 2.0f, 0);

            }
        }
        for (int i = 0; i < textInfo.meshInfo.Length; i++)
        {
            var meshInfo = textInfo.meshInfo[i];
            meshInfo.mesh.vertices = meshInfo.vertices;
            tmp.UpdateGeometry(meshInfo.mesh, i);
        }
    }
}
```

```cs
// 逐个打字
using UnityEngine;
public class TMP_Typer : MonoBehaviour
{
	public bool isAnimating { get; private set; } = false;
	public float speedPerCharacter = 0.1f;
	[SerializeField]
	private bool playOnEnable = false;
	public bool isLoop = false;
	private TMPro.TMP_Text text = default;
	private float time = 0.0f;
	private void Awake()
	{
		text = GetComponent<TMPro.TMP_Text>();
	}
	private void Start()
	{
		if (this.playOnEnable) { Play(); }
	}
	private void OnEnable()
	{
		if (this.playOnEnable) { Play(); }
	}
	private void Update()
	{
		if(this.isAnimating)
			UpdateAnimation(Time.deltaTime);
	}
	public void Play()
	{
		if (this.isAnimating)
			return;
		this.time = 0.0f;
		this.isAnimating = true;
		this.text.ForceMeshUpdate(true);
		UpdateAnimation(0.0f);
	}
	public void Finish()
	{
		if (!this.isAnimating)
			return;

		this.isAnimating = false;
		this.text.maxVisibleCharacters = this.text.textInfo.characterCount;
		this.time = 0.0f;
	}
	private void UpdateAnimation(float deltaTime)
	{

		int maxVisibleCharacters = this.text.textInfo.characterCount;
		float maxTime = (maxVisibleCharacters + 1) * speedPerCharacter;
		this.time += deltaTime;
		int visibleCharacters = Mathf.Clamp(Mathf.FloorToInt(time / speedPerCharacter), 0, maxVisibleCharacters);
		if (text.maxVisibleCharacters != visibleCharacters)
			text.maxVisibleCharacters = visibleCharacters;
		if (this.time > maxTime)
		{
			if (this.isLoop)
			{
				time = time % maxTime;
			}
			else
			{
				Finish();
			}
		}
	}
}
```

```cs
// 渐隐渐显
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using TMPro;

public class TMP_VanishOrArise : MonoBehaviour
{
    public float Time = 3f;
    public float Delay = 3f;
    public int Mince = 100;
    public bool VanishOrArise = true;
    private TMP_Text Tmp = default;
    private float Alpha = 0f;
    void OnEnable()
    {
        Tmp = GetComponent<TMP_Text>();
        if (VanishOrArise)
        {
            Invoke("StartVanish", Delay);
        }
        else
        {
            Invoke("StartArise", Delay);
        }
    }
    void StartVanish()
    {
        if (Tmp.color.a == 0f) Tmp.color = new Color(Tmp.color.r, Tmp.color.g, Tmp.color.b, 1f);
        StartCoroutine(Vanish());
    }
    void StartArise()
    {
        if (Tmp.color.a == 1f) Tmp.color = new Color(Tmp.color.r, Tmp.color.g, Tmp.color.b, 0f);
        StartCoroutine(Arise());
    }
    IEnumerator Vanish()
    {
        for (int i = 0; i < Mince; i++)
        {
            Tmp.color = new Color(Tmp.color.r, Tmp.color.g, Tmp.color.b, Tmp.color.a - (1f / Mince));
            if (Tmp.color.a <= 0f)
            {
                break;
            }
            yield return new WaitForSeconds(Time / Mince);
        }
    }
    IEnumerator Arise()
    {
        for (int i = 0; i < Mince; i++)
        {
            Tmp.color = new Color(Tmp.color.r, Tmp.color.g, Tmp.color.b, Tmp.color.a + (1f / Mince));
            if (Tmp.color.a >= 1f)
            {
                break;
            }
            yield return new WaitForSeconds(Time / Mince);
        }
    }
}
```

### {U2D}

#### SpriteShapeRenderer

- color: SpriteShape的渲染颜色;
- maskInteraction: 指定SpriteShape如何与遮罩交互;
- GetBounds()
  - 获取边界数据作为NativeArray;
  - 此NativeArray的数量始终为1;
- GetChannels()
  - 获取/设置SpriteShapeRenderer的网格数据数组;
  - public void **GetChannels** (int **dataSize**, out NativeArray<ushort> **indices**, out NativeSlice<Vector3> **vertices**, out NativeSlice<Vector2> **texcoords**);
    - dataSize: 要为NativeArray保留的大小;
    - indices: 索引NativeArray;
    - vertives: 顶点NativeSlice;
    - texcoords: 通道0的纹理坐标NativeSlice;
  - public void **GetChannels** (int **dataSize**, out NativeArray<ushort> **indices**, out NativeSlice<Vector3> **vertices**, out NativeSlice<Vector2> **texcoords**, out NativeSlice<Vector4> **tangents**);
    - tangents: 切线NativeSlice；
  - public void **GetChannels** (int **dataSize**, out NativeArray<ushort> **indices**, out NativeSlice<Vector3> **vertices**, out NativeSlice<Vector2> **texcoords**, out NativeSlice<Vector4> **tangents**, out NativeSlice<Vector3> **normals**);
    - normals: 法线NativeSlice;

#### SpriteShapeSegment

- geomIndex: SpriteShape生成的子网格列表的几何索引;
- indexCount: SpriteShape子网格的索引数量;
- spriteIndex: 用于为此SpriteShapeSegment生成分段/角的Sprite的索引;
- vertexCount: SpriteShape子网格的顶点数量;

<div style="background-color: cyan; height: 2px;"></div>

## [界面]

### {UI}

#### Button

<table class="list">
        <tbody><tr><td class="lbl"><a href="Events.UnityEvent.AddListener.html">AddListener</a></td><td class="desc">向 UnityEvent 添加非持久性监听器。</td></tr>
        <tr><td class="lbl"><a href="Events.UnityEvent.Invoke.html">Invoke</a></td><td class="desc">调用所有已注册的回调（运行时和持久性）。</td></tr>
        <tr><td class="lbl"><a href="Events.UnityEvent.RemoveListener.html">RemoveListener</a></td><td class="desc">从 UnityEvent 中删除非持久性监听器。</td></tr>
        <tr><td class="lbl"><a href="Events.UnityEventBase.GetPersistentEventCount.html">GetPersistentEventCount</a></td><td class="desc">获取已注册的持久性监听器的数量。</td></tr>
        <tr><td class="lbl"><a href="Events.UnityEventBase.GetPersistentMethodName.html">GetPersistentMethodName</a></td><td class="desc">获取索引处的监听器的目标方法名称。</td></tr>
        <tr><td class="lbl"><a href="Events.UnityEventBase.GetPersistentTarget.html">GetPersistentTarget</a></td><td class="desc">获取索引处的监听器的目标组件。</td></tr>
        <tr><td class="lbl"><a href="Events.UnityEventBase.RemoveAllListeners.html">RemoveAllListeners</a></td><td class="desc">从事件中删除所有非持久性（即通过脚本创建的）监听器。</td></tr>
        <tr><td class="lbl"><a href="Events.UnityEventBase.SetPersistentListenerState.html">SetPersistentListenerState</a></td><td class="desc">修改持久性监听器的执行状态。</td></tr>
      </tbody></table>

<div style="background-color: cyan; height: 2px;"></div>

### Cursor

- lockState: 确定硬件指针是否锁定到视图的中心、受限于窗口或者根本不受限制。

```cs
Cursor.lockState = CursorLockMode.Locked;
```

- visible: 确定硬件指针是否可见。
- SetCursor(Texture 2D texture, Vector2 hotspot, CursorMode cursorMode):
  - texture: 默认为null, 光标图案;
  - hotspot: 要用作目标点的从左上角开始的纹理偏移(光标边界内);
  - cursorMode: 运行此光标在支持的平台上渲染为硬件光标或者强制使用软件光标;

```cs
using UnityEngine;
using System.Collections;

public class ExampleClass : MonoBehaviour
{
    public Texture2D cursorTexture;
    public CursorMode cursorMode = CursorMode.Auto;
    public Vector2 hotSpot = Vector2.zero;
    void OnMouseEnter()
    {
        Cursor.SetCursor(cursorTexture, hotSpot, cursorMode);
    }

    void OnMouseExit()
    {
        Cursor.SetCursor(null, Vector2.zero, cursorMode);
    }
}
```

<div style="background-color: cyan; height: 2px;"></div>

## [工具]

### Debug

- Log()
- DrawRay(Vector3 Start, Vector3 End, Color color)

```cs
    public void DrawLine(Vector3 Start, Vector3 End)
    {
        StartCoroutine(Temp_AFWA(Start, End));
    }
    private IEnumerator Temp_AFWA(Vector3 Start, Vector3 End)
    {
        for (int i = 0; i < 100; i++)
        {
            yield return 0;
            Debug.DrawRay(Start, End, Color.green);
        }
    }
```

- DrawLine(Vector3 start, Vector3 end, Color color = Color.white, float duration = 0.0f, bool depthTest = true)

<div style="background-color: cyan; height: 2px;"></div>

### Application

#### [属性]

- dataPath: 工程文件路径; `D:/UnityProject/MyProject3D/Assets`;
- streamingAssetsPath: 可以通过文件流来进行读取的文件路径; `D:/UnityProject/MyProject3D/Assets/StreamingAssets`;
- persistenDataPath :可以实例的文件路径; `C:/Users/LEGION/AppData/LocalLow/DefaultCompany/MyProject3D`;
- tempporaryCachePath :临时的文件路径; `C:/Users/LEGION/AppData/Local/Temp/DefaultCompany/MyProject3D`;

<hr>

- identifier: 标识名;
- companyName: 公司名;
- productName: 产品名;
- installMode: 安装包名;
- isEditor: 是否在编辑器模式;
- isFocused;
- isMobilePlatform;
- isPlaying;
- isWebPlayer;
- platform;
- unityVersion;
- version: 项目版本号;
- runInBackground: 是否可以在后台运行;

```cs
UnityEditor.EditorApplication.isPlaying = false; // 在编辑器模式下退出编辑状态;
```



#### [方法]

- OpenURL("url"): 打开指定的网址;
- Quit(): 退出游戏;
- CaptureScreenshot("Test.png");

<div style="background-color: cyan; height: 2px;"></div>

### Resources

- Load<GameObject>("PrefabName"): 获取位于主Resources文件夹内的名为PrefabName的GameObject对象;

<table class="list">
      <tbody><tr><td class="lbl"><a href="Resources.FindObjectsOfTypeAll.html">FindObjectsOfTypeAll</a></td><td class="desc">返回所有类型为 type 的对象的列表。</td></tr>
      <tr><td class="lbl"><a href="Resources.Load.html">Load</a></td><td class="desc">加载存储在 Resources 文件夹中的 path 处的资源。</td></tr>
      <tr><td class="lbl"><a href="Resources.LoadAll.html">LoadAll</a></td><td class="desc">加载位于 Resources 文件夹中的 path 处的文件夹中的所有资源，或加载位于该处的文件。</td></tr>
      <tr><td class="lbl"><a href="Resources.LoadAsync.html">LoadAsync</a></td><td class="desc">异步加载存储在 Resources 文件夹中的 path 处的资源。</td></tr>
      <tr><td class="lbl"><a href="Resources.UnloadAsset.html">UnloadAsset</a></td><td class="desc">从内存中卸载 /assetToUnload/。</td></tr>
      <tr><td class="lbl"><a href="Resources.UnloadUnusedAssets.html">UnloadUnusedAssets</a></td><td class="desc">卸载未使用的资源。</td></tr>
    </tbody></table>

<div style="background-color: cyan; height: 2px;"></div>

### SceneManagement

#### SceneManager

- LoadScene(): 加载下一个场景; 一般用于下一个场景不大的情况;
  - public static void  LoadScene (int  sceneBuildIndex ,  SceneManagement.LoadSceneMode mode = LoadSceneMode.Single);
  - public static void LoadScene(string sceneName, SceneManagement.LoadSceneMode mode = LoadSceneMode.Single); 
- LoadSceneAsync(): 异步加载下一个场景; 返回AsyncOperation类型包含加载信息和进度条等信息;
- sceneCount: 当前加载的场景个数;
- sceneCountInBuildSettings: 在Build面板中加载的场景个数;
- GetActiveScene(): 获取已加载的当前场景的信息;
- GetSceneAt(Index): 加载Index指定索引的场景;

##### [变量]

<table class="list">
      <tbody><tr><td class="lbl"><a href="SceneManagement.SceneManager-sceneCount.html">sceneCount</a></td><td class="desc">当前加载的场景总数。</td></tr>
      <tr><td class="lbl"><a href="SceneManagement.SceneManager-sceneCountInBuildSettings.html">sceneCountInBuildSettings</a></td><td class="desc">Build Settings 中的场景数量。</td></tr>
    </tbody></table>

##### [函数]

<table class="list">
      <tbody><tr><td class="lbl"><a href="SceneManagement.SceneManager.CreateScene.html">CreateScene</a></td><td class="desc">在运行时使用给定名称创建一个新的空场景。</td></tr>
      <tr><td class="lbl"><a href="SceneManagement.SceneManager.GetActiveScene.html">GetActiveScene</a></td><td class="desc">获取当前活动的场景。</td></tr>
      <tr><td class="lbl"><a href="SceneManagement.SceneManager.GetSceneAt.html">GetSceneAt</a></td><td class="desc">获取 SceneManager 的已加载场景列表中索引处的场景。</td></tr>
      <tr><td class="lbl"><a href="SceneManagement.SceneManager.GetSceneByBuildIndex.html">GetSceneByBuildIndex</a></td><td class="desc">从构建索引中获取场景结构。</td></tr>
      <tr><td class="lbl"><a href="SceneManagement.SceneManager.GetSceneByName.html">GetSceneByName</a></td><td class="desc">搜索已加载的场景，查找包含给定名称的场景。</td></tr>
      <tr><td class="lbl"><a href="SceneManagement.SceneManager.GetSceneByPath.html">GetSceneByPath</a></td><td class="desc">搜索所有已加载的场景，查找具有给定资源路径的场景。</td></tr>
      <tr><td class="lbl"><a href="SceneManagement.SceneManager.LoadScene.html">LoadScene</a></td><td class="desc">按照 Build Settings 中的名称或索引加载场景。</td></tr>
      <tr><td class="lbl"><a href="SceneManagement.SceneManager.LoadSceneAsync.html">LoadSceneAsync</a></td><td class="desc">在后台异步加载场景。</td></tr>
      <tr><td class="lbl"><a href="SceneManagement.SceneManager.MergeScenes.html">MergeScenes</a></td><td class="desc">这会将源场景合并到 destinationScene 中。</td></tr>
      <tr><td class="lbl"><a href="SceneManagement.SceneManager.MoveGameObjectToScene.html">MoveGameObjectToScene</a></td><td class="desc">将游戏对象从当前场景移至新场景。</td></tr>
      <tr><td class="lbl"><a href="SceneManagement.SceneManager.SetActiveScene.html">SetActiveScene</a></td><td class="desc">将场景设置为活动状态。</td></tr>
      <tr><td class="lbl"><a href="SceneManagement.SceneManager.UnloadSceneAsync.html">UnloadSceneAsync</a></td><td class="desc">销毁所有与给定场景关联的游戏对象，并将场景从 SceneManager 中移除。</td></tr>
    </tbody></table>

##### [事件]

<table class="list">
      <tbody><tr><td class="lbl"><a href="SceneManagement.SceneManager-activeSceneChanged.html">activeSceneChanged</a></td><td class="desc">订阅此事件可在活动场景发生变化时收到通知。</td></tr>
      <tr><td class="lbl"><a href="SceneManagement.SceneManager-sceneLoaded.html">sceneLoaded</a></td><td class="desc">向此事件添加委托，以在加载场景时收到通知。</td></tr>
      <tr><td class="lbl"><a href="SceneManagement.SceneManager-sceneUnloaded.html">sceneUnloaded</a></td><td class="desc">向此事件添加委托以在卸载场景时收到通知。</td></tr>
    </tbody></table>

```cs
public class Loding : MonoBehaviour
{
    public Image processView; //一张图片，将Image 的Image Type 改为Filled模式即可;
    private void Start()
    {
        LodeGameMethod();
    }
    public void LodeGameMethod()
    {
        StartCoroutine(StartLoding(2));
    } 
    private IEnumerator StartLoding(int scence)
    {
        int displayProgress = 0;
        int toProgress = 0;
        AsyncOperation Loading = SceneManager.LoadSceneAsync(scence);
        //在场景为加载到100不允许场景被激活;
        Loading.allowSceneActivation = false;
        while (Loading.progress<0.9f)
        {
            toProgress = (int)Loading.progress * 100;
            while (displayProgress< 90)
            {
                ++displayProgress;
                Debug.Log(displayProgress);
                SetLoadingPercentage(displayProgress);
                yield return new WaitForEndOfFrame();
            }
        }
        //Unity通常会加载到89%便会卡顿，此时场景已经加载完毕;
        toProgress = 100;
        while (displayProgress<toProgress)
        {
            ++displayProgress;
            SetLoadingPercentage(displayProgress);
            yield return new WaitForEndOfFrame();
        }
        Loading.allowSceneActivation = true; //激活已经加载的场景;
    }
    private void SetLoadingPercentage(int displayProgress)
    {
        Debug.LogError(displayProgress / 100);
        processView.fillAmount = (float)displayProgress / 100;
    } 
}
```

#### [事件]

- activeSceneChanged: 当新场景被加载时调用;
- sceneLoaded: 当新场景加载完成时调用;

```cs
SceneManager.activeSceneChanged += OnActiveSceneChanged; // 事件的注册时通过加方法来进行注册;
```

#### LoadSceneMode

- Single: 关闭所有当前加载的场景并加载一个场景;

- Additive: 将场景添加到当前加载的场景;

  ```cs
  using UnityEngine;
  using UnityEngine.SceneManagement;
  public class Example : MonoBehaviour
  {
      void OnGUI()
      {
          if (GUI.Button(new Rect(20, 30, 150, 30), "Other Scene Single"))
          {
              SceneManager.LoadScene("YourScene", LoadSceneMode.Single);
          }
          if (GUI.Button(new Rect(20, 60, 150, 30), "Other Scene Additive"))
          {
              SceneManager.LoadScene("YourScene", LoadSceneMode.Additive);
          }
      }
  }
  ```

#### LocalPhysicsMode

- None: 不会创建本地2D或3D物理场景;
- Physics2D: 本地2D物理场景将由Scene创建并拥有;
- Physics3D: 本地3D物理场景将由Scene创建并拥有;

<div style="background-color: cyan; height: 2px;"></div>

### RenderSettings

- skybox: Material; 天空球材质;

<div style="background-color: cyan; height: 2px;"></div>

### PlayerPrefs

- Save(): 立刻保存数据; 
- SetInt(string key, int val);
- GetInt(string key);
- SetFloat(string key, float val);
- GetFloat(string key);
- SetString(string key, string val);
- GetString(string key);
- HasKey(string key); 返回bool判断键名是否存在;
- DeleteKey(string key): 删除指定键值对;
- DeleteAll(): 清除全部内容;

#### [存储路径]

- Windows: HKCU\Software\[公司名称]\[产品名称]项下的注册表中; 注册表中

- HKEY_CURRENT_UESE->SOFTWARE->UNITY->UnityEditor->公司名称->产品名称

  可以对注册表中数据直接进行修改;

- Android: /data/data/包名/shared_prefs/pkg-name.xml;

- IOS: /LIbrary/Preferences/[应用ID].plist;

<div style="background-color: cyan; height: 2px;"></div>

### JsonUtility

- public static T **FromJson** (string **json**): 通过 JSON 表示形式创建对象; 只支持普通类和结构；不支持派生自 UnityEngine.Object 的类;

  ```cs
  using UnityEngine;
  
  [System.Serializable]
  public class PlayerInfo
  {
      public string name;
      public int lives;
      public float health;
  
      public static PlayerInfo CreateFromJSON(string jsonString)
      {
          return JsonUtility.FromJson<PlayerInfo>(jsonString);
      }
  
      // Given JSON input:
      // {"name":"Dr Charles","lives":3,"health":0.8}
      // this example will return a PlayerInfo object with
      // name == "Dr Charles", lives == 3, and health == 0.8f.
  }
  ```

- public static object **FromJson** (string **json**, Type **type**);

  - json: 对象的JSON表示形式;
  - type: 由Json表示的对象类型;

- public static string **ToJson** (object **obj**);

- public static string **ToJson** (object **obj**, bool **prettyPrint**);

  - obj: 要转换为JSON形式的对象;
  - prettyPrint: 如果为 true, 则格式化输出以实现可读性; 如果为 false, 则格式化输出以实现最小大小; 默认为 false; 
  - return: **string** JSON 格式的对象数据。

  ```cs
  using UnityEngine;
  
  public class PlayerState : MonoBehaviour
  {
      public string playerName;
      public int lives;
      public float health;
  
      public string SaveToString()
      {
          return JsonUtility.ToJson(this);
      }
  
      // Given:
      // playerName = "Dr Charles"
      // lives = 3
      // health = 0.8f
      // SaveToString returns:
      // {"playerName":"Dr Charles","lives":3,"health":0.8}
  }
  ```

<div style="background-color: cyan; height: 2px;"></div>

### AnimationCurve

- Evaluate()

  - `public AnimationCurve Curve;`

  - `Height = Curve.Evaluate(Height);` 

<div style="background-color: cyan; height: 2px;"></div>

## [常用]

### Input


- GetButtonDown("KeyName")
- GetButton("虚拟按键")
  - 虚拟按键一直按着时触发;
- GetButtonUp("虚拟按键")
  - 虚拟按键抬起时触发;

<hr>

- GetKeyDown(KeyCode)
- GetKeyUp(KeyCode)
- GetKey()
  - 按键一直按着时触发;

#### [KeyCode]


<table>
<tr><td>Backspace:退格键</td>  <td>Delete</td></tr>
<tr><td>Tab</td>  <td>Clear</td></tr>
<tr><td>Return:回车键</td>  <td>Pause</td></tr>
<tr><td>Escape</td>  <td>Space</td></tr>
<tr><td>Home</td>  <td>Keypad0:小键盘0</td></tr>
<tr><td>KeypadPeriod:小键盘"."</td>  <td>KeypadDivide:小键盘"/"</td></tr>
<tr><td>KeypadMultiply:小键盘"*"</td>  <td>KeypadMinus:小键盘"-"</td></tr>
<tr><td>KeypadPlus:小键盘"+"</td>  <td>KeypadEnter:小键盘"Enter"</td></tr>
<tr><td>KeypadEquals:小键盘"="</td>  <td>UpArrow</td></tr>
<tr><td>DownArrow</td>  <td>LeftArrow</td></tr>
<tr><td>RightArrow</td>  <td>Insert</td></tr>
<tr><td>End</td>  <td>PageUp</td></tr>
<tr><td>F1</td>  <td>Alpha0:按键0</td></tr>
<tr><td>Exclaim:"!"</td>  <td>DoubleQuote</td></tr>
<tr><td>Hash</td>  <td>Dollar:"$"</td></tr>
<tr><td>Ampersand</td>  <td>Quote</td></tr>
<tr><td>LeftParen</td>  <td>RightParen</td></tr>
<tr><td>Asterisk:"*"</td>  <td>Plus:"+"</td></tr>
<tr><td>Comma:","</td>  <td>Minus:"-"</td></tr>
<tr><td>Period:"."</td>  <td>Slash:"/"</td></tr>
<tr><td>Colon:":"</td>  <td>Semicolon:";"</td></tr>
<tr><td>Less</td>  <td>Equals</td></tr>
<tr><td>Greater</td>  <td>Question:"?"</td></tr>
<tr><td>At:"@"</td>  <td>LeftBracket"["</td></tr>
<tr><td>BackSlash</td>  <td>Caret:"^"</td></tr>
<tr><td>Underscore:"_"</td>  <td>BackQuote:"`"</td></tr>
<tr><td>A</td>  <td>Numlock</td></tr>
<tr><td>Capslock</td>  <td>RightShift</td></tr>
<tr><td>RightShift</td>  <td>LeftShift</td></tr>
<tr><td>RightControl</td>  <td>LeftControl</td></tr>
<tr><td>RightAlt</td>  <td>LeftAlt</td></tr>
<tr><td>LeftApple</td>  <td>RightApple</td></tr>
<tr><td>LeftWindows</td>  <td>RightWindows</td></tr>
<tr><td>Mouse0:鼠标左键</td>  <td>Mouse1:鼠标右键</td></tr>
<tr><td>Mouse2:鼠标中键</td>
</table>
<hr>

- anyKeyDown: 任何按键被按下时返回true;
- anyKey: 任何按键被按着时返回true;
- mousePosition: 返回鼠标在屏幕上的像素坐标; z轴始终为0;


<hr>

- GetMouseButton(0|1|2)
  - 鼠标一直按着时触发;
  - 0-1-2左右中键;
- GetMouseButtonDown(0|1|2);
- GetMouseButtonUp(0|1|2);

<hr>

- GetAxisRaw("虚拟轴名"): 返回值仅有0 / -1 / 1;
- GetAxis("虚拟轴名"): 通过按下虚拟轴来返回-1到1之间的值，初始值为0; 

<hr>

- multiTouchEnabled: 允许多点触控; Bool;
- simulateMouseWithTouches: 将触摸输入模拟为鼠标输入; Bool;
- touchCount: 多点总数;
- touches: 多个记录触控点;
- touchSupported: ;
- GetTouch(): ;

`Touch myTouch = Input.touches[0]`: 获取当前的第一个触点;

- myTouch.fingerId: 触电Id;
- myTouch.deltaPosition: 触点移动距离;
- myTouch.deltaTime: 触点经过时间;
- myTouch.tapCount: 触点点击次数;
- myTouch.phase: 触点状态;

<div style="background-color: cyan; height: 2px;"></div>

### Vector2

- Distance(Vector2 Position, Vector2 RawPosition);
- magnitude: 返回向量的长度;
- nomalized;
- Normalize();
- ClampMagnitude(): 将一个向量限制在参数中指定的长度之间；
- MoveToWards(): 用来做匀速的运动，由一个位置向另一个位置进行移动;
- sqrMagnitude: 对向量的长度开方运算;

<div style="background-color: cyan; height: 2px;"></div>

### Vector3

- Normalize(): 将一个Vector3向量长度归一化; Demo: `Vector3 v = new Vector3(1, -2, 3); v.Normalize(); //v = (1, -1, 1);`

- MoveTowards(transform.position, Vector3 TargetPosition, Speed * Time.deltaTime): ;

- .normalized: 返回归一化的向量;

- Cross(): 叉乘运算; 通过两个向量获得另一个向量的方向;

- Project(): 投影运算;

- Reflect():  反射运算;

- Slerp(): 按照角度进行插值; Lerp按照位置插值;

- float Dot (Vector3 lhs, Vector3 rhs)

  - 计算两个向量的点积;

  ```cs
  float Angle(Vector3 a, Vector3 b)
  {
      float dot = Vector3.Dot(a, b);
      float det = (a.x * b.y) - (b.x * a.y);
      return Mathf.Atan2(det, dot) * Mathf.Rad2Deg;
  }
  ```

  

<div style="background-color: cyan; height: 2px;"></div>

### Vector3Int

- RoundToInt(): 将Vector3类型转换为Vector3Int类型; 四舍五入取整;  
- FloorToInt(): 将Vector3类型转换为Vector3Int类型; 向下取整; 
- CeilToInt(): 将Vector3类型转换为Vector3Int类型; 向上取整;

<div style="background-color: cyan; height: 2px;"></div>

### GameObject

- Instantiate<GameObject>(GameObject original, Vector3 position, Quaternion rotation, Transform parent);

- activeSelf: 返回是否激活状态的布尔值;

- tag;

- activeInHierarchy: 受父类影响的判断是否处于激活状态; 弗雷取消激活后子类也被取消激活;

- SetActive(bool);

- CreatePrimitive(PrimitibeType.---): 创建原始的游戏物体; 

- GetComponent<T>();

- GetComponentInChildren<T>();

  ```cs
  public GameObject SquareParent;
  Transform[] Squares = SquareParent.GetComponentsInChildren<Transform>();
  ```

#### [变量]

<table class="list">
      <tbody><tr><td class="lbl"><a href="GameObject-activeInHierarchy.html">activeInHierarchy</a></td><td class="desc">定义 GameObject 在 Scene 中是否处于活动状态。</td></tr>
      <tr><td class="lbl"><a href="GameObject-activeSelf.html">activeSelf</a></td><td class="desc">此 GameObject 的本地活动状态。（只读）</td></tr>
      <tr><td class="lbl"><a href="GameObject-isStatic.html">isStatic</a></td><td class="desc">仅限 Editor 的 API，指定游戏对象是否为静态。</td></tr>
      <tr><td class="lbl"><a href="GameObject-layer.html">layer</a></td><td class="desc">该游戏对象所在的层。</td></tr>
      <tr><td class="lbl"><a href="GameObject-scene.html">scene</a></td><td class="desc">该 GameObject 所属的场景。</td></tr>
      <tr><td class="lbl"><a href="GameObject-tag.html">tag</a></td><td class="desc">此游戏对象的标签。</td></tr>
      <tr><td class="lbl"><a href="GameObject-transform.html">transform</a></td><td class="desc">附加到此 GameObject 的 Transform。</td></tr>
    </tbody></table>

#### [函数]

<table class="list">
      <tbody><tr><td class="lbl"><a href="GameObject.AddComponent.html">AddComponent</a></td><td class="desc">将名为 className 的组件类添加到该游戏对象。</td></tr>
      <tr><td class="lbl"><a href="GameObject.BroadcastMessage.html">BroadcastMessage</a></td><td class="desc">调用此游戏对象或其任何子项中的每个 MonoBehaviour 上名为 methodName 的方法。</td></tr>
      <tr><td class="lbl"><a href="GameObject.CompareTag.html">CompareTag</a></td><td class="desc">此游戏对象是否使用 tag 进行了标记？</td></tr>
      <tr><td class="lbl"><a href="GameObject.GetComponent.html">GetComponent</a></td><td class="desc">如果游戏对象附加了类型为 type 的组件，则将其返回，否则返回 null。</td></tr>
      <tr><td class="lbl"><a href="GameObject.GetComponentInChildren.html">GetComponentInChildren</a></td><td class="desc">使用深度首次搜索返回 GameObject 或其任何子项中类型为 type 的组件。</td></tr>
      <tr><td class="lbl"><a href="GameObject.GetComponentInParent.html">GetComponentInParent</a></td><td class="desc">返回 GameObject 或其任何父项中类型为 type 的组件。</td></tr>
      <tr><td class="lbl"><a href="GameObject.GetComponents.html">GetComponents</a></td><td class="desc">返回 GameObject 中类型为 type 的所有组件。</td></tr>
      <tr><td class="lbl"><a href="GameObject.GetComponentsInChildren.html">GetComponentsInChildren</a></td><td class="desc">返回 GameObject 或其任何子项中类型为 type 的所有组件。</td></tr>
      <tr><td class="lbl"><a href="GameObject.GetComponentsInParent.html">GetComponentsInParent</a></td><td class="desc">返回 GameObject 或其任何父项中类型为 type 的所有组件。</td></tr>
      <tr><td class="lbl"><a href="GameObject.SendMessage.html">SendMessage</a></td><td class="desc">调用此游戏对象中的每个 MonoBehaviour 上名为 methodName 的方法。</td></tr>
      <tr><td class="lbl"><a href="GameObject.SendMessageUpwards.html">SendMessageUpwards</a></td><td class="desc">调用此游戏对象中的每个 MonoBehaviour 上或此行为的每个父级上名为 methodName 的方法。</td></tr>
      <tr><td class="lbl"><a href="GameObject.SetActive.html">SetActive</a></td><td class="desc">根据给定的值 true 或 /false/，激活/停用 GameObject。</td></tr>
    </tbody></table>

<table class="list">
      <tbody><tr><td class="lbl"><a href="GameObject.CreatePrimitive.html">CreatePrimitive</a></td><td class="desc">创建一个具有原始网格渲染器和相应碰撞体的游戏对象。</td></tr>
      <tr><td class="lbl"><a href="GameObject.Find.html">Find</a></td><td class="desc">按 name 查找 GameObject，然后返回它。</td></tr>
      <tr><td class="lbl"><a href="GameObject.FindGameObjectsWithTag.html">FindGameObjectsWithTag</a></td><td class="desc">返回标记为 tag 的活动 GameObject 的列表。如果未找到 GameObject，则返回空数组。</td></tr>
      <tr><td class="lbl"><a href="GameObject.FindWithTag.html">FindWithTag</a></td><td class="desc">返回一个标记为 tag 的活动 GameObject。如果未找到 GameObject，则返回 null。</td></tr>
    </tbody></table>

<div style="background-color: cyan; height: 2px;"></div>

### ScriptableObject

#### [方法]

- `CreateInstance(string className) / CreateInstance(Type type)`: Creates an instance of a scriptable object; To easily create a ScriptableObject instance that is bound to a .asset file via the Editor user interface, consider using [CreateAssetMenuAttribute]; 
- .GetInstanceID();
- .ToString();

```cs
using UnityEngine;
using UnityEngine.Rendering.PostProcessing;
public class VignettePulse : MonoBehaviour
{
PostProcessVolume m_Volume;
Vignette m_Vignette;
void Start()
{
   m_Vignette = ScriptableObject.CreateInstance<Vignette>();
   m_Vignette.enabled.Override(true);
   m_Vignette.intensity.Override(1f);
   m_Volume = PostProcessManager.instance.QuickVolume(gameObject.layer, 100f, m_Vignette);
}
void Update()
{
    m_Vignette.intensity.value = Mathf.Sin(Time.realtimeSinceStartup);
}
void OnDestroy()
{
   RuntimeUtilities.DestroyVolume(m_Volume, true, true);
}
}
```

<div style="background-color:cyan; height:2px;"></div>

### Object

- name: 名字，调用该变量，则无论是通过GameObject还是Component都是返回游戏物体的名字;
- Destroy(): 删除游戏物体，但是不会立马在unity中删除，而是会先进行回收，等确定没对象使用的时候，在进行删除;
- DontDestroyOnLoad(): 当加载新的场景的时候，不删除这个场景中的某个游戏物体;
- FindObjectType<>;
- FindObjectsType<>: t通过类型来进行查找，是进行全局的查找，则就是在整个场景中进行查找;
- FindGameObjectWithTag: 如果查到的是多个，则只返回查找到的第一个;
- FindGameObejctsWithTag: 返回查找到的游戏物体集合;

<hr>

- Cube cube = target.GetComponent<Cube>(); 返回一个对应的组件，如果有多个，则只返回第一个;
- Cube[] cubes= target.GetComponents<Cube>(); 返回该游戏物体上所有符合条件的组件，返回一个组件数组;
- Cube[] cubes = target.GetComponentsInChildren<Cube>(); 返回该游戏物体上的对应组件，同时返回该游戏物体的子类上对应的组件;
- Cube[] cubes = target.GetComponentsInParent<Cube>(); 返回该游戏物体上的对应组件，同时返回该游戏物体的父类上对应的组件;

<div style="background-color: cyan; height: 2px;"></div>

### Quaternion

- identity: 返回一个单位四元数; 表示没有旋转角度; 

- LookRotation(Vector3 forward, Vector3 up): 创建一个Quanternion, 将指定的向量指向目标方向; 将一个对象旋转到指定方向或朝向目标对象;
  - forward: 指向目标方向的向量;
  - up: 指向Quanternion在旋转时的"上方向";
  
- .eulerAngles: 返回转换成的Vector3对象;

- Euler(Vector3 Dest): 返回Vector3转换成的Quaternion对象;

  ```cs
  Des.transform.rotation = Quaternion.Euler(new Vector3(0f, 0f, Random.Range(0f, 360f)));
  ```

  ```cs
      public void LookAt2D(float angles)
      {
          Vector3 playerRelativePosition = player.position - transform.position;
  
          Quaternion lookRotation = Quaternion.LookRotation(Vector3.forward, new Vector2(playerRelativePosition.x, playerRelativePosition.y));
  
          Vector3 lookRotationVector = lookRotation.eulerAngles;
          lookRotationVector.z -= angles;
  
          transform.rotation = Quaternion.Euler(lookRotationVector);
      }
  ```

- **Slerp** ([Quaternion](https://docs.unity.cn/cn/2018.4/ScriptReference/Quaternion.html) **a**, [Quaternion](https://docs.unity.cn/cn/2018.4/ScriptReference/Quaternion.html) **b**, float **t**):在 `a` 和 `b` 之间以球形方式插入 t。参数 `t` 被限制在 [0, 1] 范围内;

  ```cs
  transform.rotation = Quaternion.Slerp(from.rotation, to.rotation, timeCount);
  timeCount = timeCount + Time.deltaTime;
  ```

#### [identity]

- .SetFromToRotation(Vector3 fromDirection, Vector3 toDirection): 创建一个从fromDirection到toDirection的Quaternion实例;

```cs
private Quaternion qua = Quaternion.identity;
qua.SetFromToRotation(Vec2, Vec2);
transform.rotation = qua;
```

- .SetLookRotation(Vector3 view, Vector3 up): 设置Quaternion实例的朝向; view决定transform.forward方向; up决定transform.up方向;

```cs
private Quaternion qua = Quaternion.identity;
qua.SetLookRotation(Vec1, Vec2);
transform.rotation = qua;
```

<div style="background-color: cyan; height: 2px;"></div>

### transform

- TransformDirection(): 将一个空间中的方向转换为另一个空间中的方向; 本地坐标系与世界坐标系相互转换; 
- SetParent(Transform, false): ;
- parent;

#### [变量]

<table class="list">
      <tbody><tr><td class="lbl"><a href="Transform-childCount.html">childCount</a></td><td class="desc">父变换具有的子项数。</td></tr>
      <tr><td class="lbl"><a href="Transform-eulerAngles.html">eulerAngles</a></td><td class="desc">以欧拉角表示的旋转（以度为单位）。</td></tr>
      <tr><td class="lbl"><a href="Transform-forward.html">forward</a></td><td class="desc">世界空间中变换的蓝轴。</td></tr>
      <tr><td class="lbl"><a href="Transform-hasChanged.html">hasChanged</a></td><td class="desc">自上次将标志设置为“false”以来，变换是否发生更改？</td></tr>
      <tr><td class="lbl"><a href="Transform-hierarchyCapacity.html">hierarchyCapacity</a></td><td class="desc">变换的层级视图数据结构的变换容量。</td></tr>
      <tr><td class="lbl"><a href="Transform-hierarchyCount.html">hierarchyCount</a></td><td class="desc">变换的层级视图数据结构中变换的数量。</td></tr>
      <tr><td class="lbl"><a href="Transform-localEulerAngles.html">localEulerAngles</a></td><td class="desc">以欧拉角表示的相对于父变换旋转的旋转（以度为单位）。</td></tr>
      <tr><td class="lbl"><a href="Transform-localPosition.html">localPosition</a></td><td class="desc">相对于父变换的变换位置。</td></tr>
      <tr><td class="lbl"><a href="Transform-localRotation.html">localRotation</a></td><td class="desc">相对于父级变换旋转的变换旋转。</td></tr>
      <tr><td class="lbl"><a href="Transform-localScale.html">localScale</a></td><td class="desc">相对于父对象的变换缩放。</td></tr>
      <tr><td class="lbl"><a href="Transform-localToWorldMatrix.html">localToWorldMatrix</a></td><td class="desc">将点从本地空间转换到世界空间的矩阵（只读）。</td></tr>
      <tr><td class="lbl"><a href="Transform-lossyScale.html">lossyScale</a></td><td class="desc">对象的全局缩放。（只读）</td></tr>
      <tr><td class="lbl"><a href="Transform-parent.html">parent</a></td><td class="desc">变换的父级。</td></tr>
      <tr><td class="lbl"><a href="Transform-position.html">position</a></td><td class="desc">世界空间中的变换位置。</td></tr>
      <tr><td class="lbl"><a href="Transform-right.html">right</a></td><td class="desc">世界空间中变换的红轴。</td></tr>
      <tr><td class="lbl"><a href="Transform-root.html">root</a></td><td class="desc">返回层级视图中最顶层的变换。</td></tr>
      <tr><td class="lbl"><a href="Transform-rotation.html">rotation</a></td><td class="desc">一个四元数，用于存储变换在世界空间中的旋转。</td></tr>
      <tr><td class="lbl"><a href="Transform-up.html">up</a></td><td class="desc">世界空间中变换的绿轴。</td></tr>
      <tr><td class="lbl"><a href="Transform-worldToLocalMatrix.html">worldToLocalMatrix</a></td><td class="desc">将点从世界空间转换到本地空间的矩阵（只读）。</td></tr>
    </tbody></table>

#### [函数]

<table class="list">
      <tbody><tr><td class="lbl"><a href="Transform.DetachChildren.html">DetachChildren</a></td><td class="desc">清除所有子项的父级。</td></tr>
      <tr><td class="lbl"><a href="Transform.Find.html">Find</a></td><td class="desc">按 n 查找子项，然后返回它。</td></tr>
      <tr><td class="lbl"><a href="Transform.GetChild.html">GetChild</a></td><td class="desc">按索引返回变换子项。</td></tr>
      <tr><td class="lbl"><a href="Transform.GetSiblingIndex.html">GetSiblingIndex</a></td><td class="desc">获取同级索引。</td></tr>
      <tr><td class="lbl"><a href="Transform.InverseTransformDirection.html">InverseTransformDirection</a></td><td class="desc">将 direction 从世界空间变换到本地空间。与 Transform.TransformDirection 相反。</td></tr>
      <tr><td class="lbl"><a href="Transform.InverseTransformPoint.html">InverseTransformPoint</a></td><td class="desc">将 position 从世界空间变换到本地空间。</td></tr>
      <tr><td class="lbl"><a href="Transform.InverseTransformVector.html">InverseTransformVector</a></td><td class="desc">将 vector 从世界空间变换到本地空间。与 Transform.TransformVector 相反。</td></tr>
      <tr><td class="lbl"><a href="Transform.IsChildOf.html">IsChildOf</a></td><td class="desc">该变换是否为 parent 的子项？</td></tr>
      <tr><td class="lbl"><a href="Transform.LookAt.html">LookAt</a></td><td class="desc">旋转变换，使向前矢量指向 target 的当前位置。</td></tr>
      <tr><td class="lbl"><a href="Transform.Rotate.html">Rotate</a></td><td class="desc">使用 Transform.Rotate 以各种方式旋转游戏对象。通常以欧拉角而不是四元数提供旋转。</td></tr>
      <tr><td class="lbl"><a href="Transform.RotateAround.html">RotateAround</a></td><td class="desc">将变换围绕穿过世界坐标中的 point 的 axis 旋转 angle 度。</td></tr>
      <tr><td class="lbl"><a href="Transform.SetAsFirstSibling.html">SetAsFirstSibling</a></td><td class="desc">将变换移动到本地变换列表的开头。</td></tr>
      <tr><td class="lbl"><a href="Transform.SetAsLastSibling.html">SetAsLastSibling</a></td><td class="desc">将变换移动到本地变换列表的末尾。</td></tr>
      <tr><td class="lbl"><a href="Transform.SetParent.html">SetParent</a></td><td class="desc">设置变换的父级。</td></tr>
      <tr><td class="lbl"><a href="Transform.SetPositionAndRotation.html">SetPositionAndRotation</a></td><td class="desc">设置变换组件的世界空间位置和旋转。</td></tr>
      <tr><td class="lbl"><a href="Transform.SetSiblingIndex.html">SetSiblingIndex</a></td><td class="desc">设置同级索引。</td></tr>
      <tr><td class="lbl"><a href="Transform.TransformDirection.html">TransformDirection</a></td><td class="desc">将 direction 从本地空间变换到世界空间。</td></tr>
      <tr><td class="lbl"><a href="Transform.TransformPoint.html">TransformPoint</a></td><td class="desc">将 position 从本地空间变换到世界空间。</td></tr>
      <tr><td class="lbl"><a href="Transform.TransformVector.html">TransformVector</a></td><td class="desc">将 vector 从本地空间变换到世界空间。</td></tr>
      <tr><td class="lbl"><a href="Transform.Translate.html">Translate</a></td><td class="desc">根据 translation 的方向和距离移动变换。</td></tr>
    </tbody></table>

<div style="background-color: cyan; height: 2px;"></div>

### Time

- deltaTime: 上一帧到当前帧的时间间隔, 单位秒; Demo: 0.0021938;
- fixedTime;
- fixedDeltaTime;
- SmoothDeltaTime;
- timeScale = 0f; :暂停游戏时间; timeScale = 1f; :继续游戏时间;
- time: 从游戏开始到现在的时间，随着游戏暂停而停止计算;
- timeSinceLevelLoad: 当前Scene开始到目前为止的时间，随着暂停而停止计算;
- frameCount: 总帧数;
- realtimeSinceStartup: 游戏开始后的总时间;暂停不影响计算;
- captureFramerate: 每秒的帧率;
- unscaledDeltaTime;
- unscaledTime;



<div style="background-color: cyan; height: 2px;"></div>

### Array

#### [属性]

- IsFixedSize: 是否具有固定大小;
- IsReadOnly: 是否只读;
- IsSynchronized: 是否同步对Array的访问(线程安全);
- Length: 获取一个32位整数; 元素总数;
- LongLength: 获取一个64位整数; 元素总数;
- Rank: 获取维数; 
- SyncRoot: 获取可用于同步对Array的访问的对象; 

#### [方法]

- Exists(Array, Func): ;
- Fill(Array, Value): ;
- Clear(Array, Int32, Int32): 设置某个范围内的元素为0 / false / null;
- Copy(Array, Array, Int32): 复制指定长度的数组内容到另一个数组中; 
- CopyTo(Array, int32): 从当前一维数组复制到一个指定的一维数组的指定索引位置;
- GetLength: 获取元素总数;
- GetLongLength: ;
- GetLowerBound: 获取下界;
- GetType: 获取当前实例的类型; 从对象Object继承;
- GetUpperBound: ;
- GetValue(Int32): 获取一维数组指定位置的值;
- IndexOf(Array, Object): 搜索指定对象第一次出现的索引; 
- Reverse(Array): ;
- SetValue(Object, Int32): ;
- Sort(Array): ;
- ToString: ;

```cs
using System.Linq;
int[] Arr = {1, 2, 3};
List<int> Lis = Arr.ToList();
```

<div style="background-color: cyan; height: 2px;"></div>

### Mathf

- Sign(num);

- Abs(num);

- Clamp(float value, float min, float max);

- Abs(num);

- Ceil(num);

- Floor(num);

- Pow(i, j);

- Lerp(float from, float to, float t)
  - 基于浮点数t返回a到b之间的插值, t限制在0到1之间, 当t=0返回from, 当t=1返回to; 
  - t=0.5返回from和to的平均值;
  
- ClosePowerOfTwo(value)
  - 取得离value的2次方最近的值;
  
- DeltaAngle(float fromAngle, float toAngle)
  - 取得两个角之间的差值; 
  - 差值保证在-180到180之间;
  
- PingPong(float t, flaot Length)
  - 返回0到length之间的数值，不会到0也不会到length; 
  - t只能用Time.time, 不能用固定数值; 
  - 类似乒乓球的来回运动，起始 值是0，通过t变量来控制值由0向maxValue移动，当t大于maxValue的时候又向0进行移动，然后就这样的来回往复运动，一般t变量用时间Time.deltatime来进行控制的。
  
- public static float **PerlinNoise** (float **x**, float **y**)

  - 返回介于 0.0 和 1.0 之间的值;
  
  - 返回值可能会稍微超过1.0;
  
  - 生成2D柏林噪声;

  - 输入参数为整数时返回值固定;
  
  - 输入参数不变返回值固定;
  
  - x: 采样点的X坐标;
  
  - y: 采样点的Y坐标;
  
  - PerlinNoise (int i + float Offset)
  
    - `positions[i] = new Vector3(i * 0.1f, Mathf.PerlinNoise(i + OffsetFloat, 0f) * Height, 0);`
  
    - i: 递增值;
    - Offset: 取值0.5f时峰值最大;
  
  - PerlinNoise (int i * float Offset)
  
    - `positions[i] = new Vector3(i * 0.1f, Mathf.PerlinNoise(i * OffsetFloat, 0f) * Height, 0);`
  
    - Offset: 取值越小返回值越平滑;

#### [变量]

<table class="list">
      <tbody><tr><td class="lbl"><a href="Mathf.Deg2Rad.html">Deg2Rad</a></td><td class="desc">度到弧度换算常量（只读）。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Epsilon.html">Epsilon</a></td><td class="desc">微小浮点值（只读）。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Infinity.html">Infinity</a></td><td class="desc">正无穷大的表示形式（只读）。</td></tr>
      <tr><td class="lbl"><a href="Mathf.NegativeInfinity.html">NegativeInfinity</a></td><td class="desc">负无穷大的表示形式（只读）。</td></tr>
      <tr><td class="lbl"><a href="Mathf.PI.html">PI</a></td><td class="desc">众所周知的“3.14159265358979...”值（只读）。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Rad2Deg.html">Rad2Deg</a></td><td class="desc">弧度到度换算常量（只读）。</td></tr>
    </tbody></table>

#### [函数]

<table class="list">
      <tbody><tr><td class="lbl"><a href="Mathf.Abs.html">Abs</a></td><td class="desc">返回 f 的绝对值。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Acos.html">Acos</a></td><td class="desc">返回 f 的反余弦 - 其余弦为 f 的角度（以弧度为单位）。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Approximately.html">Approximately</a></td><td class="desc">比较两个浮点值，如果它们相似，则返回 true。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Asin.html">Asin</a></td><td class="desc">返回 f 的反正弦 - 其正弦为 f 的角度（以弧度为单位）。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Atan.html">Atan</a></td><td class="desc">返回 f 的反正切 - 其正切为 f 的角度（以弧度为单位）。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Atan2.html">Atan2</a></td><td class="desc">返回其 Tan 为 y/x 的角度（以弧度为单位）。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Ceil.html">Ceil</a></td><td class="desc">返回大于或等于 f 的最小整数。</td></tr>
      <tr><td class="lbl"><a href="Mathf.CeilToInt.html">CeilToInt</a></td><td class="desc">返回大于或等于 f 的最小整数。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Clamp.html">Clamp</a></td><td class="desc">在给定的最小浮点值和最大浮点值之间钳制给定值。如果在最小和最大范围内，则返回给定值。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Clamp01.html">Clamp01</a></td><td class="desc">将值限制在 0 与 1 之间并返回值。</td></tr>
      <tr><td class="lbl"><a href="Mathf.ClosestPowerOfTwo.html">ClosestPowerOfTwo</a></td><td class="desc">返回最接近的 2 的幂值。</td></tr>
      <tr><td class="lbl"><a href="Mathf.CorrelatedColorTemperatureToRGB.html">CorrelatedColorTemperatureToRGB</a></td><td class="desc">将以开尔文为单位的色温转换为 RGB 颜色。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Cos.html">Cos</a></td><td class="desc">返回角度 f 的余弦。</td></tr>
      <tr><td class="lbl"><a href="Mathf.DeltaAngle.html">DeltaAngle</a></td><td class="desc">计算两个给定角度（以度为单位给定）之间的最短差异。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Exp.html">Exp</a></td><td class="desc">返回 e 的指定幂。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Floor.html">Floor</a></td><td class="desc">返回小于或等于 f 的最大整数。</td></tr>
      <tr><td class="lbl"><a href="Mathf.FloorToInt.html">FloorToInt</a></td><td class="desc">返回小于或等于 f 的最大整数。</td></tr>
      <tr><td class="lbl"><a href="Mathf.GammaToLinearSpace.html">GammaToLinearSpace</a></td><td class="desc">将给定值从伽马 (sRGB) 转换为线性颜色空间。</td></tr>
      <tr><td class="lbl"><a href="Mathf.InverseLerp.html">InverseLerp</a></td><td class="desc">计算在范围 [a, b] 内生成插值 value 的线性参数 t。</td></tr>
      <tr><td class="lbl"><a href="Mathf.IsPowerOfTwo.html">IsPowerOfTwo</a></td><td class="desc">如果值是 2 的幂，则返回 true。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Lerp.html">Lerp</a></td><td class="desc">在 a 与 b 之间按 t 进行线性插值。</td></tr>
      <tr><td class="lbl"><a href="Mathf.LerpAngle.html">LerpAngle</a></td><td class="desc">与 Lerp 相同，但是在值环绕 360 度时确保值正确插入。</td></tr>
      <tr><td class="lbl"><a href="Mathf.LerpUnclamped.html">LerpUnclamped</a></td><td class="desc">在 a 与 b 之间按 t 进行线性插值，t 没有限制。</td></tr>
      <tr><td class="lbl"><a href="Mathf.LinearToGammaSpace.html">LinearToGammaSpace</a></td><td class="desc">将给定值从线性转换为伽马 (sRGB) 颜色空间。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Log.html">Log</a></td><td class="desc">返回指定的数字以指定的底数为底的对数。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Log10.html">Log10</a></td><td class="desc">返回指定的数字的以 10 为底的对数。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Max.html">Max</a></td><td class="desc">返回两个或更多值中的最大值。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Min.html">Min</a></td><td class="desc">返回两个或更多值中的最小值。</td></tr>
      <tr><td class="lbl"><a href="Mathf.MoveTowards.html">MoveTowards</a></td><td class="desc">将值 current 向 target 靠近。</td></tr>
      <tr><td class="lbl"><a href="Mathf.MoveTowardsAngle.html">MoveTowardsAngle</a></td><td class="desc">与 MoveTowards 相同，但是在值环绕 360 度时确保值正确插入。</td></tr>
      <tr><td class="lbl"><a href="Mathf.NextPowerOfTwo.html">NextPowerOfTwo</a></td><td class="desc">返回大于或等于参数的下一个 2 的幂。</td></tr>
      <tr><td class="lbl"><a href="Mathf.PerlinNoise.html">PerlinNoise</a></td><td class="desc">生成 2D 柏林噪声。</td></tr>
      <tr><td class="lbl"><a href="Mathf.PingPong.html">PingPong</a></td><td class="desc">对值 t 进行 PingPong 操作，使它不会大于长度，并且不会小于 0。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Pow.html">Pow</a></td><td class="desc">返回 f 的 p 次幂。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Repeat.html">Repeat</a></td><td class="desc">对值 t 进行循环，使它不会大于长度，并且不会小于 0。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Round.html">Round</a></td><td class="desc">返回舍入为最近整数的 /f/。</td></tr>
      <tr><td class="lbl"><a href="Mathf.RoundToInt.html">RoundToInt</a></td><td class="desc">返回舍入为最近整数的 /f/。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Sign.html">Sign</a></td><td class="desc">返回 f 的符号。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Sin.html">Sin</a></td><td class="desc">返回角度 f 的正弦。</td></tr>
      <tr><td class="lbl"><a href="Mathf.SmoothDamp.html">SmoothDamp</a></td><td class="desc">随时间推移将一个值逐渐改变为所需目标。</td></tr>
      <tr><td class="lbl"><a href="Mathf.SmoothDampAngle.html">SmoothDampAngle</a></td><td class="desc">随时间推移将以度为单位给定的角度逐渐改变为所需目标角度。</td></tr>
      <tr><td class="lbl"><a href="Mathf.SmoothStep.html">SmoothStep</a></td><td class="desc">在 min 与 max 之间进行插值，在限制处进行平滑。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Sqrt.html">Sqrt</a></td><td class="desc">返回 f 的平方根。</td></tr>
      <tr><td class="lbl"><a href="Mathf.Tan.html">Tan</a></td><td class="desc">返回角度 f 的正切（以弧度为单位）。</td></tr>
    </tbody></table>



<div style="background-color: cyan; height: 2px;"></div>

### Random

- InitState(seed): 通过参数指定种子; 参数一般取值时间戳:`System.DataTime.Now.Ticks`;
- insideUnitCircle: 在单位为1的圆内随机生成一个位置信息;
- insideUnitSphere: 在单位为1的球内随机生成一个位置信息;

#### [变量]

<table class="list">
      <tbody><tr><td class="lbl"><a href="Random-insideUnitCircle.html">insideUnitCircle</a></td><td class="desc">返回半径为 1 的圆形内的随机点（只读）。</td></tr>
      <tr><td class="lbl"><a href="Random-insideUnitSphere.html">insideUnitSphere</a></td><td class="desc">返回半径为 1 的球体内的随机点（只读）。</td></tr>
      <tr><td class="lbl"><a href="Random-onUnitSphere.html">onUnitSphere</a></td><td class="desc">返回半径为 1 的球体表面上的随机点（只读）。</td></tr>
      <tr><td class="lbl"><a href="Random-rotation.html">rotation</a></td><td class="desc">返回随机旋转（只读）。</td></tr>
      <tr><td class="lbl"><a href="Random-rotationUniform.html">rotationUniform</a></td><td class="desc">返回具有一致分布的随机旋转（只读）。</td></tr>
      <tr><td class="lbl"><a href="Random-state.html">state</a></td><td class="desc">获取/设置随机数生成器的完整内部状态。</td></tr>
      <tr><td class="lbl"><a href="Random-value.html">value</a></td><td class="desc">返回介于 0.0 [含] 与 1.0 [含] 之间的随机数（只读）。</td></tr>
    </tbody></table>

#### [函数]

- public static void **InitState** (int **seed**);

  - seed: 用于初始化随机数生成器的种子;

- public static [Color](https://docs.unity.cn/cn/2018.4/ScriptReference/Color.html) **ColorHSV** ();

- public static [Color](https://docs.unity.cn/cn/2018.4/ScriptReference/Color.html) **ColorHSV** (float **hueMin**, float **hueMax**);

- public static [Color](https://docs.unity.cn/cn/2018.4/ScriptReference/Color.html) **ColorHSV** (float **hueMin**, float **hueMax**, float **saturationMin**, float **saturationMax**);

- public static [Color](https://docs.unity.cn/cn/2018.4/ScriptReference/Color.html) **ColorHSV** (float **hueMin**, float **hueMax**, float **saturationMin**, float **saturationMax**, float **valueMin**, float **valueMax**);

- public static [Color](https://docs.unity.cn/cn/2018.4/ScriptReference/Color.html) **ColorHSV** (float **hueMin**, float **hueMax**, float **saturationMin**, float **saturationMax**, float **valueMin**, float **valueMax**, float **alphaMin**, float **alphaMax**);

  <table class="list"><tbody><tr><td class="name lbl">hueMin</td><td class="desc">最小色调 [0..1]。</td></tr><tr><td class="name lbl">hueMax</td><td class="desc">最大色调 [0..1]。</td></tr><tr><td class="name lbl">saturationMin</td><td class="desc">最小饱和度 [0..1]。</td></tr><tr><td class="name lbl">saturationMax</td><td class="desc">最大饱和度 [0..1]。</td></tr><tr><td class="name lbl">valueMin</td><td class="desc">最小值 [0..1]。</td></tr><tr><td class="name lbl">valueMax</td><td class="desc">最大值 [0..1]。</td></tr><tr><td class="name lbl">alphaMin</td><td class="desc">最小 Alpha [0..1]。</td></tr><tr><td class="name lbl">alphaMax</td><td class="desc">最大 Alpha [0..1]。</td></tr></tbody></table>

<table class="list">
      <tbody><tr><td class="lbl"><a href="Random.ColorHSV.html">ColorHSV</a></td><td class="desc">通过 HSV 和 Alpha 范围生成随机颜色。</td></tr>
      <tr><td class="lbl"><a href="Random.InitState.html">InitState</a></td><td class="desc">使用种子初始化随机数生成器状态。</td></tr>
      <tr><td class="lbl"><a href="Random.Range.html">Range</a></td><td class="desc">返回介于 min [含] 与 max [含] 之间的随机浮点数（只读）。</td></tr>
    </tbody></table>

<div style="background-color: cyan; height: 2px;"></div>

### Gradient

```cs
using UnityEngine;
public class ExampleScript : MonoBehaviour
{
    Gradient gradient;
    GradientColorKey[] colorKey;
    GradientAlphaKey[] alphaKey;
    void Start()
    {
        gradient = new Gradient();
        // Populate the color keys at the relative time 0 and 1 (0 and 100%)
        colorKey = new GradientColorKey[2];
        colorKey[0].color = Color.red;
        colorKey[0].time = 0.0f;
        colorKey[1].color = Color.blue;
        colorKey[1].time = 1.0f;

        // Populate the alpha  keys at relative time 0 and 1  (0 and 100%)
        alphaKey = new GradientAlphaKey[2];
        alphaKey[0].alpha = 1.0f;
        alphaKey[0].time = 0.0f;
        alphaKey[1].alpha = 0.0f;
        alphaKey[1].time = 1.0f;

        gradient.SetKeys(colorKey, alphaKey);

        // What's the color at the relative time 0.25 (25 %) ?
        Debug.Log(gradient.Evaluate(0.25f));
    }
}
```

#### [变量]

- alphaKeys: 在渐变中定义的所有Alpha键;
- colorKeys: 在渐变中定义的所有颜色键;
- mode: 控制计算渐变的方式; 

#### [函数]

- Gradient();
- Evaluate(): 计算给定时间处的颜色;
- SetKeys(GradientColorKey[] colorKeys, GradientAlphaKey[] alphaKeys): 使用颜色键和Alpha键的数组设置渐变;

<div style="background-color: cyan; height: 2px;"></div>

### GradientAlphaKey(Constructor)

- alpha;
- time;

<div style="background-color: cyan; height: 2px;"></div>

### GradientColorKey(Constructor)

- color;
- time;

<div style="background-color: cyan; height: 2px;"></div>

### Color

#### [变量]

<table class="list">
      <tbody><tr><td class="lbl"><a href="Color-black.html">black</a></td><td class="desc">纯黑色。RGBA 为 (0, 0, 0, 1)。</td></tr>
      <tr><td class="lbl"><a href="Color-blue.html">blue</a></td><td class="desc">纯蓝色。RGBA 为 (0, 0, 1, 1)。</td></tr>
      <tr><td class="lbl"><a href="Color-clear.html">clear</a></td><td class="desc">完全透明。RGBA 为 (0, 0, 0, 0)。</td></tr>
      <tr><td class="lbl"><a href="Color-cyan.html">cyan</a></td><td class="desc">青色。RGBA 为 (0, 1, 1, 1)。</td></tr>
      <tr><td class="lbl"><a href="Color-gray.html">gray</a></td><td class="desc">灰色。RGBA 为 (0.5, 0.5, 0.5, 1)。</td></tr>
      <tr><td class="lbl"><a href="Color-green.html">green</a></td><td class="desc">纯绿色。RGBA 为 (0, 1, 0, 1)。</td></tr>
      <tr><td class="lbl"><a href="Color-grey.html">grey</a></td><td class="desc">
          gray 的英式拼写。RGBA 为相同的 (0.5, 0.5, 0.5, 1)。</td></tr>
      <tr><td class="lbl"><a href="Color-magenta.html">magenta</a></td><td class="desc">洋红色。RGBA 为 (1, 0, 1, 1)。</td></tr>
      <tr><td class="lbl"><a href="Color-red.html">red</a></td><td class="desc">纯红色。RGBA 为 (1, 0, 0, 1)。</td></tr>
      <tr><td class="lbl"><a href="Color-white.html">white</a></td><td class="desc">纯白色。RGBA 为 (1, 1, 1, 1)。</td></tr>
      <tr><td class="lbl"><a href="Color-yellow.html">yellow</a></td><td class="desc">黄色。RGBA 为 (1, 0.92, 0.016, 1)，但该颜色很好看！</td></tr>
    </tbody></table>

<table class="list">
      <tbody><tr><td class="lbl"><a href="Color-a.html">a</a></td><td class="desc">颜色的 Alpha 分量（0 为透明，1 为不透明）。</td></tr>
      <tr><td class="lbl"><a href="Color-b.html">b</a></td><td class="desc">颜色的蓝色分量。</td></tr>
      <tr><td class="lbl"><a href="Color-g.html">g</a></td><td class="desc">颜色的绿色分量。</td></tr>
      <tr><td class="lbl"><a href="Color-gamma.html">gamma</a></td><td class="desc">应用了伽马曲线的颜色版本。</td></tr>
      <tr><td class="lbl"><a href="Color-grayscale.html">grayscale</a></td><td class="desc">颜色的灰度值。（只读）</td></tr>
      <tr><td class="lbl"><a href="Color-linear.html">linear</a></td><td class="desc">sRGB 颜色的线性值。</td></tr>
      <tr><td class="lbl"><a href="Color-maxColorComponent.html">maxColorComponent</a></td><td class="desc">返回最大颜色分量值：Max(r,g,b)。</td></tr>
      <tr><td class="lbl"><a href="Color-r.html">r</a></td><td class="desc">颜色的红色分量。</td></tr>
      <tr><td class="lbl"><a href="Color.Index_operator.html">this[int]</a></td><td class="desc">分别使用 [0]、[1]、[2]、[3] 访问 r、g、b、a 分量。</td></tr>
    </tbody></table>

#### [函数]

- Color(r, g, b, a);

  ```cs
  public Button Btn;
  public void Chocie(){
      Btn.GetComponent<Image>().color = new Color(100f / 255f, 149f / 255f, 237f / 255f);
  }
  ```

- ToString();

<table class="list">
      <tbody><tr><td class="lbl"><a href="Color.HSVToRGB.html">HSVToRGB</a></td><td class="desc">用 HSV 输入创建 RGB 颜色。</td></tr>
      <tr><td class="lbl"><a href="Color.Lerp.html">Lerp</a></td><td class="desc">在颜色 a 与 b 之间按 t 进行线性插值。</td></tr>
      <tr><td class="lbl"><a href="Color.LerpUnclamped.html">LerpUnclamped</a></td><td class="desc">在颜色 a 与 b 之间按 t 进行线性插值。</td></tr>
      <tr><td class="lbl"><a href="Color.RGBToHSV.html">RGBToHSV</a></td><td class="desc">计算 RGB 输入颜色的色调、饱和度和值。</td></tr>
    </tbody></table>

<div style="background-color: cyan; height: 2px;"></div>

## [物理系统]

### Physics2D

#### [静态方法]

<table class="list">
<tr>
<td class="lbl">
<a href="Physics2D.AllLayers.html">AllLayers</a>
</td>
<td class="desc">包括所有层的层遮罩常量。</td>
</tr>
<tr>
<td class="lbl">
<a href="Physics2D-alwaysShowColliders.html">alwaysShowColliders</a>
</td>
<td class="desc">是否应始终显示碰撞体辅助图标（即使未选中时也显示）？</td>
</tr>
<tr>
<td class="lbl">
<a href="Physics2D-angularSleepTolerance.html">angularSleepTolerance</a>
</td>
<td class="desc">如果刚体的角速度高于该公差，将无法进入睡眠状态。</td>
</tr>
<tr>
<td class="lbl">
<a href="Physics2D-autoSimulation.html">autoSimulation</a>
</td>
<td class="desc">设置是否应该自动模拟物理。</td>
</tr>
<tr>
<td class="lbl">
<a href="Physics2D-autoSyncTransforms.html">autoSyncTransforms</a>
</td>
<td class="desc">当 Transform 组件发生更改时，是否自动将变换更改与物理系统同步。</td>
</tr>
<tr>
<td class="lbl">
<a href="Physics2D-baumgarteScale.html">baumgarteScale</a>
</td>
<td class="desc">控制解析重叠速度的缩放因子。</td>
</tr>
<tr>
<td class="lbl">
<a href="Physics2D-baumgarteTOIScale.html">baumgarteTOIScale</a>
</td>
<td class="desc">控制解析 TOI 重叠速度的缩放因子。</td>
</tr>
<tr>
<td class="lbl">
<a href="Physics2D-callbacksOnDisable.html">callbacksOnDisable</a>
</td>
<td class="desc">用于控制 Collider2D 处于禁用状态时是否应调用相应的 OnCollisionExit2D 或 OnTriggerExit2D 回调。</td>
</tr>
<tr>
<td class="lbl">
<a href="Physics2D-colliderAABBColor.html">colliderAABBColor</a>
</td>
<td class="desc">设置辅助图标使用的颜色，以显示所有对齐 Collider 轴的包围盒 (AABB)。</td>
</tr>
<tr>
<td class="lbl">
<a href="Physics2D-colliderAsleepColor.html">colliderAsleepColor</a>
</td>
<td class="desc">辅助图标显示所有睡眠碰撞体（当身体处于睡眠状态时，碰撞体也处于睡眠状态）所用的颜色。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-colliderAwakeColor.html">colliderAwakeColor</a>
</td>
<td class="desc">辅助图标显示所有唤醒碰撞体（当身体处于唤醒状态时，碰撞体也处于唤醒状态）所用的颜色。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-colliderContactColor.html">colliderContactColor</a>
</td>
<td class="desc">辅助图标显示所有碰撞体接触点所用的颜色。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-contactArrowScale.html">contactArrowScale</a>
</td>
<td class="desc">碰撞体辅助图标使用的接触箭头的缩放。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-defaultContactOffset.html">defaultContactOffset</a>
</td>
<td class="desc">新创建的碰撞体的默认接触偏移。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-defaultPhysicsScene.html">defaultPhysicsScene</a>
</td>
<td class="desc">Unity 启动时自动创建的 PhysicsScene2D。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.DefaultRaycastLayers.html">DefaultRaycastLayers</a>
</td>
<td class="desc">层遮罩常量，包括默认情况下参与射线投射的所有层。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-gravity.html">gravity</a>
</td>
<td class="desc">重力产生的加速度。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.IgnoreRaycastLayer.html">IgnoreRaycastLayer</a>
</td>
<td class="desc">忽略射线投射的默认层的层遮罩常量。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-jobOptions.html">jobOptions</a>
</td>
<td class="desc">一组选项，用于控制在使用作业系统进行多线程物理模拟时物理系统的工作方式。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-linearSleepTolerance.html">linearSleepTolerance</a>
</td>
<td class="desc">如果刚体的线性速率高于该公差，将无法进入睡眠状态。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-maxAngularCorrection.html">maxAngularCorrection</a>
</td>
<td class="desc">解算约束时使用的最大角位置校正。这有助于防止过冲。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-maxLinearCorrection.html">maxLinearCorrection</a>
</td>
<td class="desc">解算约束时使用的最大线性位置校正。这有助于防止过冲。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-maxRotationSpeed.html">maxRotationSpeed</a>
</td>
<td class="desc">每次物理更新时，刚体的最大角速度。增大该值可能会导致数值问题。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-maxTranslationSpeed.html">maxTranslationSpeed</a>
</td>
<td class="desc">每次物理更新时，刚体的最大线性速度。增大该值可能会导致数值问题。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-positionIterations.html">positionIterations</a>
</td>
<td class="desc">考虑对象位置时，物理解算器的迭代次数。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-queriesHitTriggers.html">queriesHitTriggers</a>
</td>
<td class="desc">射线投射是否检测配置为触发器的碰撞体？</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-queriesStartInColliders.html">queriesStartInColliders</a>
</td>
<td class="desc">设置始于碰撞体内部的射线投射或线条投射是否检测这些碰撞体。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-showColliderAABB.html">showColliderAABB</a>
</td>
<td class="desc">碰撞体辅助图标是否应显示每个碰撞体的 AABB？</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-showColliderContacts.html">showColliderContacts</a>
</td>
<td class="desc">碰撞体辅助图标是否应显示每个碰撞体的当前接触点？</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-showColliderSleep.html">showColliderSleep</a>
</td>
<td class="desc">碰撞体辅助图标是否应显示每个碰撞体的睡眠状态？</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-timeToSleep.html">timeToSleep</a>
</td>
<td class="desc">刚体进入睡眠状态前必须保持静止的时间（以秒为单位）。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-velocityIterations.html">velocityIterations</a>
</td>
<td class="desc">考虑对象速度时，物理解算器的迭代次数。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D-velocityThreshold.html">velocityThreshold</a>
</td>
<td class="desc">将相对线性速度低于该阈值的任何碰撞都视为非弹性碰撞。</td>
                                    </tr>
                                </table>
<hr>

#### [静态函数]

<hr>

<table class="list">
<tr>
    <td class="lbl">
        <a href="Physics2D.BoxCast.html">BoxCast</a>
    </td>
    <td class="desc">向场景中的碰撞体投射盒体，返回与盒体接触的第一个碰撞体。</td>
</tr>
<tr>
    <td class="lbl">
        <a href="Physics2D.BoxCastAll.html">BoxCastAll</a>
    </td>
<td class="desc">向场景中的碰撞体投射盒体，返回与盒体接触的所有碰撞体。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.BoxCastNonAlloc.html">BoxCastNonAlloc</a>
</td>
<td class="desc">向场景中投射一个盒体，将与盒体接触的碰撞体返回到提供的结果数组中。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.CapsuleCast.html">CapsuleCast</a>
</td>
<td class="desc">向场景中的碰撞体投射胶囊体，返回与胶囊体接触的第一个碰撞体。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.CapsuleCastAll.html">CapsuleCastAll</a>
</td>
<td class="desc">向场景中的碰撞体投射胶囊体，返回与胶囊体接触的所有碰撞体。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.CapsuleCastNonAlloc.html">CapsuleCastNonAlloc</a>
</td>
<td class="desc">向场景中投射一个胶囊体，将与胶囊体接触的碰撞体返回到提供的结果数组中。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.CircleCast.html">CircleCast</a>
</td>
<td class="desc">向场景中的碰撞体投射圆形，返回与圆形接触的第一个碰撞体。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.CircleCastAll.html">CircleCastAll</a>
</td>
<td class="desc">向场景中的碰撞体投射圆形，返回与圆形接触的所有碰撞体。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.CircleCastNonAlloc.html">CircleCastNonAlloc</a>
</td>
<td class="desc">向场景中投射一个圆形，将与圆形接触的碰撞体返回到提供的结果数组中。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.Distance.html">Distance</a>
</td>
<td class="desc">计算两个碰撞体之间的最小距离。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.GetContacts.html">GetContacts</a>
</td>
<td class="desc">获取与 collider 接触的所有碰撞体。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.GetIgnoreCollision.html">GetIgnoreCollision</a>
</td>
<td class="desc">检查碰撞检测系统是否忽略 collider1 与 collider2 之间的所有碰撞/触发器。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.GetIgnoreLayerCollision.html">GetIgnoreLayerCollision</a>
</td>
<td class="desc">检查是否忽略指定层之间的碰撞。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.GetLayerCollisionMask.html">GetLayerCollisionMask</a>
</td>
<td class="desc">获取碰撞层遮罩，指示指定层可以与哪些层发生碰撞。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.GetRayIntersection.html">GetRayIntersection</a>
</td>
<td class="desc">向场景中的碰撞体投射 3D 射线，返回射线路径上的第一个碰撞体。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.GetRayIntersectionAll.html">GetRayIntersectionAll</a>
</td>
<td class="desc">向场景中的碰撞体投射 3D 射线，返回射线路径上的所有碰撞体。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.GetRayIntersectionNonAlloc.html">GetRayIntersectionNonAlloc</a>
</td>
<td class="desc">向场景中的碰撞体投射 3D 射线，返回射线路径上的碰撞体。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.IgnoreCollision.html">IgnoreCollision</a>
</td>
<td class="desc">使碰撞检测系统忽略 collider1 与 collider2 之间的所有碰撞/触发器。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.IgnoreLayerCollision.html">IgnoreLayerCollision</a>
</td>
<td class="desc">选择检测还是忽略指定层对之间的碰撞。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.IsTouching.html">IsTouching</a>
</td>
<td class="desc">检查是否与经过的碰撞体接触。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.IsTouchingLayers.html">IsTouchingLayers</a>
</td>
<td class="desc">检查 collider 是否正在接触指定 layerMask 上的任何碰撞体。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.Linecast.html">Linecast</a>
</td>
<td class="desc">向场景中的碰撞体投射线段。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.LinecastAll.html">LinecastAll</a>
</td>
<td class="desc">向场景中的碰撞体投射线条。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.LinecastNonAlloc.html">LinecastNonAlloc</a>
</td>
<td class="desc">向场景中的碰撞体投射线条。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.OverlapArea.html">OverlapArea</a>
</td>
<td class="desc">检查某碰撞体是否位于一个矩形区域内。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.OverlapAreaAll.html">OverlapAreaAll</a>
</td>
<td class="desc">获取位于某个矩形区域内的所有碰撞体的列表。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.OverlapAreaNonAlloc.html">OverlapAreaNonAlloc</a>
</td>
<td class="desc">获取位于指定矩形区域内的所有碰撞体的列表。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.OverlapBox.html">OverlapBox</a>
</td>
<td class="desc">检查某碰撞体是否位于一个盒形区域内。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.OverlapBoxAll.html">OverlapBoxAll</a>
</td>
<td class="desc">获取位于指定盒形区域内的所有碰撞体的列表。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.OverlapBoxNonAlloc.html">OverlapBoxNonAlloc</a>
</td>
<td class="desc">获取位于指定盒形区域内的所有碰撞体的列表。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.OverlapCapsule.html">OverlapCapsule</a>
</td>
<td class="desc">检查某碰撞体是否位于一个胶囊体区域内。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.OverlapCapsuleAll.html">OverlapCapsuleAll</a>
</td>
<td class="desc">获取位于某胶囊体区域内的所有碰撞体的列表。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.OverlapCapsuleNonAlloc.html">OverlapCapsuleNonAlloc</a>
</td>
<td class="desc">获取位于某胶囊体区域内的所有碰撞体的列表。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.OverlapCircle.html">OverlapCircle</a>
</td>
<td class="desc">检查某碰撞体是否位于一个圆形区域内。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.OverlapCircleAll.html">OverlapCircleAll</a>
</td>
<td class="desc">获取位于某圆形区域内的所有碰撞体的列表。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.OverlapCircleNonAlloc.html">OverlapCircleNonAlloc</a>
</td>
<td class="desc">获取位于某圆形区域内的所有碰撞体的列表。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.OverlapCollider.html">OverlapCollider</a>
</td>
<td class="desc">获取与 collider 重叠的所有碰撞体的列表。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.OverlapPoint.html">OverlapPoint</a>
</td>
<td class="desc">检查碰撞体是否与空间中的某个点重叠。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.OverlapPointAll.html">OverlapPointAll</a>
</td>
<td class="desc">获取与空间中的某个点重叠的所有碰撞体的列表。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.OverlapPointNonAlloc.html">OverlapPointNonAlloc</a>
</td>
<td class="desc">获取与空间中的某个点重叠的所有碰撞体的列表。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.Raycast.html">Raycast</a>
</td>
<td class="desc">向场景中的碰撞体投射射线。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.RaycastAll.html">RaycastAll</a>
</td>
<td class="desc">向场景中的碰撞体投射射线，返回与射线接触的所有碰撞体。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.RaycastNonAlloc.html">RaycastNonAlloc</a>
</td>
<td class="desc">向场景中投射一条射线。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.SetLayerCollisionMask.html">SetLayerCollisionMask</a>
</td>
<td class="desc">设置碰撞层遮罩，指示指定层可以与哪些层发生碰撞。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.Simulate.html">Simulate</a>
</td>
<td class="desc">在场景中进行物理模拟。</td>
                                    </tr>
                                    <tr>
<td class="lbl">
    <a href="Physics2D.SyncTransforms.html">SyncTransforms</a>
</td>
<td class="desc">同步。</td>
                                    </tr>
                                </table>
- public static RaycastHit2D[] **LinecastAll** ([Vector2](https://docs.unity.cn/cn/2018.4/ScriptReference/Vector2.html) **start**, [Vector2](https://docs.unity.cn/cn/2018.4/ScriptReference/Vector2.html) **end**, int **layerMask**= DefaultRaycastLayers, float **minDepth**= -Mathf.Infinity, float **maxDepth**= Mathf.Infinity);
  - start: 起点;
  - end: 终点;
  - layerMask: 过滤
- public static RaycastHit2D **CircleCast**(Vector2 **origin**, float **radius**, Vector2 direction, float distance = Mathf.Infinity, int layerMask = DafaultRaycastLayers, float minDepth = -Mathf.Infinity, float maxDepth = Mathf.Infinity);
- public static RaycastHit2D[] **CircleCastAll**(transform.position, radius, Vector2.zero);

<div style="background-color: cyan; height: 2px;"></div>

## [组件]

### Camera

- main:
  - ScreenToWorldPoint(Vector3): 将屏幕坐标转换为世界坐标; 
  - WorldToScreenPoint(Vector3): 将世界坐标转换为屏幕坐标;
  - ScreenPointToRay(Vector3): 将屏幕坐标转换为一条射线; 摄像机向目标位置发射射线至Vector3位置; 
  - orthographicSize -> 摄像机正交投影大小; 摄像机视口的高度的一半;

<div style="background-color: cyan; height: 2px;"></div>

### RectTransform

- sizeDelta: Vector2类型表示大小，可用于修改大小;

#### [变量]

<table class="list">
      <tbody><tr><td class="lbl"><a href="RectTransform-anchoredPosition.html">anchoredPosition</a></td><td class="desc">此 RectTransform 的轴心相对于锚点参考点的位置。</td></tr>
      <tr><td class="lbl"><a href="RectTransform-anchoredPosition3D.html">anchoredPosition3D</a></td><td class="desc">此 RectTransform 的轴心相对于锚点参考点的 3D 位置。</td></tr>
      <tr><td class="lbl"><a href="RectTransform-anchorMax.html">anchorMax</a></td><td class="desc">父 RectTransform 中右上角锚定到的标准化位置。</td></tr>
      <tr><td class="lbl"><a href="RectTransform-anchorMin.html">anchorMin</a></td><td class="desc">父 RectTransform 中左下角锚定到的标准化位置。</td></tr>
      <tr><td class="lbl"><a href="RectTransform-offsetMax.html">offsetMax</a></td><td class="desc">矩形右上角相对于右上锚点的偏移。</td></tr>
      <tr><td class="lbl"><a href="RectTransform-offsetMin.html">offsetMin</a></td><td class="desc">矩形左下角相对于左下锚点的偏移。</td></tr>
      <tr><td class="lbl"><a href="RectTransform-pivot.html">pivot</a></td><td class="desc">此 RectTransform 中围绕其旋转的标准化位置。</td></tr>
      <tr><td class="lbl"><a href="RectTransform-rect.html">rect</a></td><td class="desc">
          Transform 的本地空间中计算的矩形。</td></tr>
      <tr><td class="lbl"><a href="RectTransform-sizeDelta.html">sizeDelta</a></td><td class="desc">此 RectTransform 相对于锚点之间距离的大小。</td></tr>
    </tbody></table>

#### [函数]

<table class="list">
      <tbody><tr><td class="lbl"><a href="RectTransform.ForceUpdateRectTransforms.html">ForceUpdateRectTransforms</a></td><td class="desc">强制重新计算 RectTransform 内部数据。</td></tr>
      <tr><td class="lbl"><a href="RectTransform.GetLocalCorners.html">GetLocalCorners</a></td><td class="desc">获取计算的矩形在其 Transform 的本地空间中的各个角。</td></tr>
      <tr><td class="lbl"><a href="RectTransform.GetWorldCorners.html">GetWorldCorners</a></td><td class="desc">获取计算的矩形在世界空间中的各个角。</td></tr>
      <tr><td class="lbl"><a href="RectTransform.SetInsetAndSizeFromParentEdge.html">SetInsetAndSizeFromParentEdge</a></td><td class="desc">设置此矩形相对于父矩形指定边缘的距离，同时也会设置其大小。</td></tr>
      <tr><td class="lbl"><a href="RectTransform.SetSizeWithCurrentAnchors.html">SetSizeWithCurrentAnchors</a></td><td class="desc">使 RectTransform 计算的矩形在指定轴上具有给定大小。</td></tr>
    </tbody></table>

<div style="background-color: cyan; height: 2px;"></div>

### Rect

#### [变量]

- zero: 简写的new Rect(0, 0, 0, 0);

<table class="list">
      <tbody><tr><td class="lbl"><a href="Rect-center.html">center</a></td><td class="desc">矩形中心的位置。</td></tr>
      <tr><td class="lbl"><a href="Rect-height.html">height</a></td><td class="desc">矩形的高度（从 Y 位置进行测量）。</td></tr>
      <tr><td class="lbl"><a href="Rect-max.html">max</a></td><td class="desc">矩形最大角的位置。</td></tr>
      <tr><td class="lbl"><a href="Rect-min.html">min</a></td><td class="desc">矩形最小角的位置。</td></tr>
      <tr><td class="lbl"><a href="Rect-position.html">position</a></td><td class="desc">矩形的 X 和 Y 位置。</td></tr>
      <tr><td class="lbl"><a href="Rect-size.html">size</a></td><td class="desc">矩形的宽度和高度。</td></tr>
      <tr><td class="lbl"><a href="Rect-width.html">width</a></td><td class="desc">矩形的宽度（从 X 位置进行测量）。</td></tr>
      <tr><td class="lbl"><a href="Rect-x.html">x</a></td><td class="desc">矩形的 X 坐标。</td></tr>
      <tr><td class="lbl"><a href="Rect-xMax.html">xMax</a></td><td class="desc">矩形的最大 X 坐标。</td></tr>
      <tr><td class="lbl"><a href="Rect-xMin.html">xMin</a></td><td class="desc">矩形的最小 X 坐标。</td></tr>
      <tr><td class="lbl"><a href="Rect-y.html">y</a></td><td class="desc">矩形的 Y 坐标。</td></tr>
      <tr><td class="lbl"><a href="Rect-yMax.html">yMax</a></td><td class="desc">矩形的最大 Y 坐标。</td></tr>
      <tr><td class="lbl"><a href="Rect-yMin.html">yMin</a></td><td class="desc">矩形的最小 Y 坐标。</td></tr>
    </tbody></table>

#### [函数]

<table class="list">
      <tbody><tr><td class="lbl"><a href="Rect.Contains.html">Contains</a></td><td class="desc">如果 point 的 x 和 y 分量是此矩形内部的点，则返回 true。如果 allowInverse 存在并且为 true，则允许 Rect 的宽度和高度取负值（即，最小值大于最大值），测试仍然有效。</td></tr>
      <tr><td class="lbl"><a href="Rect.Overlaps.html">Overlaps</a></td><td class="desc">如果另一个矩形与此矩形重叠，则返回 true。如果 allowInverse 存在并且为 true，则允许 Rect 的宽度和高度取负值（即，最小值大于最大值），测试仍然有效。</td></tr>
      <tr><td class="lbl"><a href="Rect.Set.html">Set</a></td><td class="desc">设置现有 Rect 的分量。</td></tr>
      <tr><td class="lbl"><a href="Rect.ToString.html">ToString</a></td><td class="desc">对于此 Rect，返回整齐格式化的字符串。</td></tr>
    </tbody></table>

<table class="list">
      <tbody><tr><td class="lbl"><a href="Rect.MinMaxRect.html">MinMaxRect</a></td><td class="desc">通过最小/最大坐标值创建矩形。</td></tr>
      <tr><td class="lbl"><a href="Rect.NormalizedToPoint.html">NormalizedToPoint</a></td><td class="desc">根据给定的标准化坐标，返回矩形内的点。</td></tr>
      <tr><td class="lbl"><a href="Rect.PointToNormalized.html">PointToNormalized</a></td><td class="desc">返回与点对应的标准化坐标。</td></tr>
    </tbody></table>

<div style="background-color: cyan; height: 2px;"></div>

### Tilemap

- `using UnityEngine.Tilemaps;`
- GetSprite(Vector3Int Pos)
  - 获取Pos上的TileBase的Sprite;
  - 当前Tilemap中该位置不存在Tile时返回null;
- GetTile(Vector3Int Pos)
  - 获取Pos上的TileBase;
- SetTile(Vector3Int Pos, TileBase Tile)
  - 在位置上放置Tile;
  - Tile: 取值null时则删除Pos上的TileBase;

```cs
public Tilemap tilemap;
TileBase x = tilemap.GetTile(Pos);
```

<div style="background-color: cyan; height: 2px;"></div>

### CharacterController

- SimpleMove(Vector3 vec): 简单移动; 使用后启用重力; 以秒计算: `cc.SimpleMove(Vector3.forward * 5)`;
- isGrounded: 是否在地面上;
- Move(Vector3 vec): 复杂移动;  类似Transform.translate(Vector3 vec); 以帧计算: `cc.Move(Vector3.forward * Time.deltaTime * 5)`;

<div style="background-color: cyan; height: 2px;"></div>

### Rigidbody

- `freezeRotation = true;`:禁用刚体旋转; 
- gravityScale: 重力大小;

#### [变量]

<table class="list">
      <tbody><tr><td class="lbl"><a href="Rigidbody-angularDrag.html">angularDrag</a></td><td class="desc">对象的角阻力。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-angularVelocity.html">angularVelocity</a></td><td class="desc">刚体的角速度矢量（以弧度/秒为单位）。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-centerOfMass.html">centerOfMass</a></td><td class="desc">相对于变换原点的质心。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-collisionDetectionMode.html">collisionDetectionMode</a></td><td class="desc">刚体的碰撞检测模式。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-constraints.html">constraints</a></td><td class="desc">控制该刚体的模拟自由度。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-detectCollisions.html">detectCollisions</a></td><td class="desc">是否应启用碰撞检测？（默认情况下始终启用）。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-drag.html">drag</a></td><td class="desc">对象的阻力。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-freezeRotation.html">freezeRotation</a></td><td class="desc">控制物理是否会更改对象的旋转。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-inertiaTensor.html">inertiaTensor</a></td><td class="desc">质量相对于质心的对角惯性张量。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-inertiaTensorRotation.html">inertiaTensorRotation</a></td><td class="desc">惯性张量的旋转。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-interpolation.html">interpolation</a></td><td class="desc">插值可以平滑消除固定帧率运行物理导致的现象。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-isKinematic.html">isKinematic</a></td><td class="desc">控制物理是否影响刚体。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-mass.html">mass</a></td><td class="desc">刚体的质量。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-maxAngularVelocity.html">maxAngularVelocity</a></td><td class="desc">刚体的最大角速率（以弧度/秒为单位）。（默认值为 7）范围为 { 0, 无穷大 }。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-maxDepenetrationVelocity.html">maxDepenetrationVelocity</a></td><td class="desc">离开穿透状态时刚体的最大速度。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-position.html">position</a></td><td class="desc">刚体的位置。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-rotation.html">rotation</a></td><td class="desc">刚体的旋转。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-sleepThreshold.html">sleepThreshold</a></td><td class="desc">经过质量标准化的能量阈值 - 当低于该阈值时，对象开始进入睡眠状态。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-solverIterations.html">solverIterations</a></td><td class="desc">solverIterations 确定刚体关节与碰撞接触点的解析精确度。它将重写 Physics.defaultSolverIterations。必须为正值。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-solverVelocityIterations.html">solverVelocityIterations</a></td><td class="desc">solverVelocityIterations 影响刚体关节与碰撞接触点的解析精确度。它将重写 Physics.defaultSolverVelocityIterations。必须为正值。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-useGravity.html">useGravity</a></td><td class="desc">控制重力是否影响该刚体。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-velocity.html">velocity</a></td><td class="desc">刚体的速度矢量。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody-worldCenterOfMass.html">worldCenterOfMass</a></td><td class="desc">刚体在世界空间中的质心（只读）。</td></tr>
    </tbody></table>

#### [函数]

<table class="list">
      <tbody><tr><td class="lbl"><a href="Rigidbody.AddExplosionForce.html">AddExplosionForce</a></td><td class="desc">向模拟爆炸效果的刚体施加力。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.AddForce.html">AddForce</a></td><td class="desc">向 Rigidbody 添加力。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.AddForceAtPosition.html">AddForceAtPosition</a></td><td class="desc">在 position 处施加 /force/。这将向对象施加扭矩和力。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.AddRelativeForce.html">AddRelativeForce</a></td><td class="desc">向刚体添加力（相对于其坐标系）。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.AddRelativeTorque.html">AddRelativeTorque</a></td><td class="desc">向刚体添加扭矩（相对于其坐标系）。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.AddTorque.html">AddTorque</a></td><td class="desc">向刚体添加扭矩。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.ClosestPointOnBounds.html">ClosestPointOnBounds</a></td><td class="desc">与附加碰撞体的包围盒最接近的点。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.GetPointVelocity.html">GetPointVelocity</a></td><td class="desc">点 /worldPoint/（全局空间）处刚体的速度。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.GetRelativePointVelocity.html">GetRelativePointVelocity</a></td><td class="desc">相对于点 relativePoint 处的刚体的速度。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.IsSleeping.html">IsSleeping</a></td><td class="desc">刚体是否处于睡眠状态？</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.MovePosition.html">MovePosition</a></td><td class="desc">将刚体移动到 /position/。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.MoveRotation.html">MoveRotation</a></td><td class="desc">将刚体旋转到 /rotation/。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.ResetCenterOfMass.html">ResetCenterOfMass</a></td><td class="desc">重置刚体的质心。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.ResetInertiaTensor.html">ResetInertiaTensor</a></td><td class="desc">重置惯性张量的值和旋转。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.SetDensity.html">SetDensity</a></td><td class="desc">根据附加的碰撞体设置质量（假设密度恒定）。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.Sleep.html">Sleep</a></td><td class="desc">强制刚体进入睡眠状态至少一帧。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.SweepTest.html">SweepTest</a></td><td class="desc">测试如果刚体在场景中移动时，是否会与任何对象发生碰撞。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.SweepTestAll.html">SweepTestAll</a></td><td class="desc">与 Rigidbody.SweepTest 类似，但返回所有命中对象。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.WakeUp.html">WakeUp</a></td><td class="desc">强制唤醒刚体。</td></tr>
    </tbody></table>

#### [消息]

<table class="list">
      <tbody><tr><td class="lbl"><a href="Rigidbody.OnCollisionEnter.html">OnCollisionEnter</a></td><td class="desc">当该碰撞体/刚体已开始接触另一个刚体/碰撞体时，调用 OnCollisionEnter。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.OnCollisionExit.html">OnCollisionExit</a></td><td class="desc">当该碰撞体/刚体已停止接触另一个刚体/碰撞体时，调用 OnCollisionExit。</td></tr>
      <tr><td class="lbl"><a href="Rigidbody.OnCollisionStay.html">OnCollisionStay</a></td><td class="desc">对应正在接触刚体/碰撞体的每一个碰撞体/刚体，每帧调用一次 OnCollisionStay。</td></tr>
    </tbody></table>
<div style="background-color: cyan; height: 2px;"></div>

### LineRenderer

- positionCount
- SetPositions(Vector3[] Posisions)
- SetPosition(int Index, Vector3 Pos)
- GetPosition(int Index)


<div style="background-color: cyan; height: 2px;"></div>

### AudioSource

#### [变量]

<table class="list">
      <tbody><tr><td class="lbl"><a href="AudioSource-bypassEffects.html">bypassEffects</a></td><td class="desc">直通效果（从滤波器组件或全局监听器滤波器应用）。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-bypassListenerEffects.html">bypassListenerEffects</a></td><td class="desc">如果设置，则不将 AudioListener 上的全局效果应用于 AudioSource 生成的音频信号。不适用于 AudioSource 正在混合器组中播放的情况。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-bypassReverbZones.html">bypassReverbZones</a></td><td class="desc">如果设置，则不将来自 AudioSource 的信号路由到与混响区关联的全局混响。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-clip.html">clip</a></td><td class="desc">要播放的默认 AudioClip。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-dopplerLevel.html">dopplerLevel</a></td><td class="desc">设置该 AudioSource 的多普勒缩放。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-gamepadSpeakerOutputType.html">gamepadSpeakerOutputType</a></td><td class="desc">获取或设置音频源的游戏手柄音频输出类型。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-ignoreListenerPause.html">ignoreListenerPause</a></td><td class="desc">即使 AudioListener.pause 设置为 true，也允许 AudioSource 播放。这对于暂停菜单中的菜单元素声音或背景音乐很有用。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-ignoreListenerVolume.html">ignoreListenerVolume</a></td><td class="desc">这使得音频源不考虑音频监听器的音量。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-isPlaying.html">isPlaying</a></td><td class="desc">当前正在播放该 clip 吗？（只读）</td></tr>
      <tr><td class="lbl"><a href="AudioSource-isVirtual.html">isVirtual</a></td><td class="desc">如果 AudioSource 播放的所有声音（由 Play() 或 playOnAwake 以及单次播放启动的主声音）都被音频系统剔除，则为 true。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-loop.html">loop</a></td><td class="desc">是否循环播放该音频剪辑？</td></tr>
      <tr><td class="lbl"><a href="AudioSource-maxDistance.html">maxDistance</a></td><td class="desc">（对数衰减）MaxDistance 为声音停止衰减的距离。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-minDistance.html">minDistance</a></td><td class="desc">在最小距离内，AudioSource 将停止增大音量。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-mute.html">mute</a></td><td class="desc">使 AudioSource 静音/取消静音。静音时将音量设置为 0，取消静音则恢复原来的音量。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-outputAudioMixerGroup.html">outputAudioMixerGroup</a></td><td class="desc">AudioSource 应将其信号路由到的目标组。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-panStereo.html">panStereo</a></td><td class="desc">以立体声方式（左声道或右声道）平移正在播放的声音。仅适用于单声道或立体声。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-pitch.html">pitch</a></td><td class="desc">音频源的音高。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-playOnAwake.html">playOnAwake</a></td><td class="desc">如果设置为 true，音频源将在唤醒时自动开始播放。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-priority.html">priority</a></td><td class="desc">设置 AudioSource 的优先级。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-reverbZoneMix.html">reverbZoneMix</a></td><td class="desc">将来自 AudioSource 的信号混合到与混响区关联的全局混响中的量。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-rolloffMode.html">rolloffMode</a></td><td class="desc">设置/获取 AudioSource 随距离衰减的方式。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-spatialBlend.html">spatialBlend</a></td><td class="desc">设置 3D 空间化计算（衰减、多普勒效应等）对该 AudioSource 的影响程度。0.0 使声音变成全 2D 效果，1.0 使其变成全 3D。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-spatialize.html">spatialize</a></td><td class="desc">启用或禁用空间化。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-spatializePostEffects.html">spatializePostEffects</a></td><td class="desc">确定空间音响效果是在效果滤波器前还是后插入的。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-spread.html">spread</a></td><td class="desc">设置扬声器空间中 3D 立体声或多声道声音的扩散角度（以度为单位）。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-time.html">time</a></td><td class="desc">播放位置（以秒为单位）。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-timeSamples.html">timeSamples</a></td><td class="desc">PCM 样本中的播放位置。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-velocityUpdateMode.html">velocityUpdateMode</a></td><td class="desc">应以固定还是动态更新方式更新音频源。</td></tr>
      <tr><td class="lbl"><a href="AudioSource-volume.html">volume</a></td><td class="desc">音频源的音量（0.0 到 1.0）。</td></tr>
    </tbody></table>
#### [公共函数]

<table class="list">
      <tbody><tr><td class="lbl"><a href="AudioSource.DisableGamepadOutput.html">DisableGamepadOutput</a></td><td class="desc">禁用音频源的游戏手柄音频输出。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.GetAmbisonicDecoderFloat.html">GetAmbisonicDecoderFloat</a></td><td class="desc">读取附加到 AudioSource 的自定义立体混响声解码器效果的用户定义参数。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.GetCustomCurve.html">GetCustomCurve</a></td><td class="desc">获取给定 AudioSourceCurveType 的当前自定义曲线。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.GetOutputData.html">GetOutputData</a></td><td class="desc">提供当前播放源的输出数据块。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.GetSpatializerFloat.html">GetSpatializerFloat</a></td><td class="desc">读取附加到 AudioSource 的自定义空间音响效果的用户定义参数。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.GetSpectrumData.html">GetSpectrumData</a></td><td class="desc">提供当前播放音频源的频谱数据块。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.Pause.html">Pause</a></td><td class="desc">暂停播放 clip。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.Play.html">Play</a></td><td class="desc">播放 clip。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.PlayDelayed.html">PlayDelayed</a></td><td class="desc">按照指定的延时（以秒为单位）播放 clip。建议用户使用该函数代替旧的 Play(delay) 函数，Play(delay) 函数接受以样本（参考采样率为 44.1 kHz）数为单位指定的延时作为参数。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.PlayOneShot.html">PlayOneShot</a></td><td class="desc">播放 AudioClip，并根据 volumeScale 调整 AudioSource 音量。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.PlayOnGamepad.html">PlayOnGamepad</a></td><td class="desc">允许通过特定游戏手柄播放音频源。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.PlayScheduled.html">PlayScheduled</a></td><td class="desc">在 AudioSettings.dspTime 读取的绝对时间轴上的特定时间播放 clip。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.SetAmbisonicDecoderFloat.html">SetAmbisonicDecoderFloat</a></td><td class="desc">设置附加到 AudioSource 的自定义立体混响声解码器效果的用户定义参数。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.SetCustomCurve.html">SetCustomCurve</a></td><td class="desc">设置给定 AudioSourceCurveType 的自定义曲线。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.SetScheduledEndTime.html">SetScheduledEndTime</a></td><td class="desc">更改某个已计划播放的声音将结束的时间。注意，根据时间安排，并非所有重新计划的请求都能得到满足。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.SetScheduledStartTime.html">SetScheduledStartTime</a></td><td class="desc">更改某个已计划播放的声音将开始的时间。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.SetSpatializerFloat.html">SetSpatializerFloat</a></td><td class="desc">设置附加到 AudioSource 的自定义空间音响效果的用户定义参数。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.Stop.html">Stop</a></td><td class="desc">停止播放 clip。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.UnPause.html">UnPause</a></td><td class="desc">恢复播放该 AudioSource。</td></tr>
    </tbody></table>
#### [静态函数]

<table class="list">
      <tbody><tr><td class="lbl"><a href="AudioSource.GamepadSpeakerSupportsOutputType.html">GamepadSpeakerSupportsOutputType</a></td><td class="desc">检查平台是否在游戏手柄上支持音频输出类型。</td></tr>
      <tr><td class="lbl"><a href="AudioSource.PlayClipAtPoint.html">PlayClipAtPoint</a></td><td class="desc">在世界空间中的给定位置播放 AudioClip。</td></tr>
    </tbody></table>
<div style="background-color: cyan; height: 2px;"></div>

### ParticleSystem

#### [变量]

<table class="list">
      <tbody><tr><td class="lbl"><a href="ParticleSystem-collision.html">collision</a></td><td class="desc">粒子系统碰撞模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-colorBySpeed.html">colorBySpeed</a></td><td class="desc">粒子系统生命周期颜色模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-colorOverLifetime.html">colorOverLifetime</a></td><td class="desc">粒子系统颜色生命周期模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-customData.html">customData</a></td><td class="desc">粒子系统自定义数据模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-emission.html">emission</a></td><td class="desc">粒子系统发射模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-externalForces.html">externalForces</a></td><td class="desc">粒子系统外力模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-forceOverLifetime.html">forceOverLifetime</a></td><td class="desc">粒子系统力生命周期模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-inheritVelocity.html">inheritVelocity</a></td><td class="desc">粒子系统速度继承模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-isEmitting.html">isEmitting</a></td><td class="desc">确定粒子系统是否发射粒子。当粒子系统的发射模块已完成、已暂停或已使用 Stop 和 StopEmitting 标志来停止该系统时，粒子系统可能停止发射。可以调用 Play 来恢复发射。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-isPaused.html">isPaused</a></td><td class="desc">确定粒子系统是否已暂停。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-isPlaying.html">isPlaying</a></td><td class="desc">确定粒子系统是否在播放。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-isStopped.html">isStopped</a></td><td class="desc">确定粒子系统是否已停止。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-lights.html">lights</a></td><td class="desc">粒子系统光源模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-limitVelocityOverLifetime.html">limitVelocityOverLifetime</a></td><td class="desc">粒子系统生命周期速度限制 (Particle System Limit Velocity over Lifetime) 模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-main.html">main</a></td><td class="desc">访问主粒子系统设置。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-noise.html">noise</a></td><td class="desc">粒子系统噪声模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-particleCount.html">particleCount</a></td><td class="desc">当前粒子数（只读）。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-proceduralSimulationSupported.html">proceduralSimulationSupported</a></td><td class="desc">该系统是否支持程序化模拟？</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-randomSeed.html">randomSeed</a></td><td class="desc">重载用于粒子系统发射的随机种子。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-rotationBySpeed.html">rotationBySpeed</a></td><td class="desc">粒子系统速度旋转 (Rotation by Speed) 模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-rotationOverLifetime.html">rotationOverLifetime</a></td><td class="desc">粒子系统旋转生命周期 (Particle System Rotation over Lifetime) 模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-shape.html">shape</a></td><td class="desc">粒子系统形状模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-sizeBySpeed.html">sizeBySpeed</a></td><td class="desc">粒子系统速控大小 (Particle System Size by Speed) 模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-sizeOverLifetime.html">sizeOverLifetime</a></td><td class="desc">粒子系统大小生命周期 (Particle System Size over Lifetime) 模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-subEmitters.html">subEmitters</a></td><td class="desc">粒子系统子发射器模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-textureSheetAnimation.html">textureSheetAnimation</a></td><td class="desc">粒子系统纹理帧动画 (Particle System Texture Sheet Animation) 模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-time.html">time</a></td><td class="desc">播放位置（以秒为单位）。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-trails.html">trails</a></td><td class="desc">粒子系统轨迹模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-trigger.html">trigger</a></td><td class="desc">粒子系统触发模块的脚本接口。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-useAutoRandomSeed.html">useAutoRandomSeed</a></td><td class="desc">控制粒子系统是否使用自动生成的随机数作为随机数生成器的种子。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem-velocityOverLifetime.html">velocityOverLifetime</a></td><td class="desc">粒子系统速度生命周期 (Particle System Velocity over Lifetime) 模块的脚本接口。</td></tr>
    </tbody></table>

#### [函数]

<table class="list">
      <tbody><tr><td class="lbl"><a href="ParticleSystem.Clear.html">Clear</a></td><td class="desc">删除粒子系统中的所有粒子。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem.Emit.html">Emit</a></td><td class="desc">立即发射 count 个粒子。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem.GetCustomParticleData.html">GetCustomParticleData</a></td><td class="desc">获取自定义每粒子数据流。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem.GetParticles.html">GetParticles</a></td><td class="desc">获取该粒子系统的粒子。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem.IsAlive.html">IsAlive</a></td><td class="desc">粒子系统是否包含任何存活的粒子，还是会产生更多粒子？</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem.Pause.html">Pause</a></td><td class="desc">暂停系统，因此不再发射新粒子，也不再更新现有粒子。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem.Play.html">Play</a></td><td class="desc">启动粒子系统。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem.SetCustomParticleData.html">SetCustomParticleData</a></td><td class="desc">设置自定义每粒子数据流。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem.SetParticles.html">SetParticles</a></td><td class="desc">设置该粒子系统的粒子。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem.Simulate.html">Simulate</a></td><td class="desc">在给定时间段内模拟粒子以快进粒子系统，然后将其暂停。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem.Stop.html">Stop</a></td><td class="desc">使用提供的停止行为，停止播放粒子系统。</td></tr>
      <tr><td class="lbl"><a href="ParticleSystem.TriggerSubEmitter.html">TriggerSubEmitter</a></td><td class="desc">在粒子系统的所有粒子上触发指定的子发射器。</td></tr>
    </tbody></table>

#### main

- Duration;
- loop;
- Prewarm;

#### shape

- ```cs
  public class ExampleClass : MonoBehaviour {
      public Mesh myMesh;
  
      void Start() {
          ParticleSystem ps = GetComponent<ParticleSystem>();
          var sh = ps.shape;
          sh.enabled = true;
          sh.shapeType = ParticleSystemShapeType.Mesh;
          sh.mesh = myMesh;
      }
  }
  ```

- enabled;

- shapeType: ParticleSystemShapeType.Mesh;

- mesh;

- [Mesh]

  - Type: Vertex / Edge / Triangle;
  - mesh;
  - randomDirection: bool;
  
- [MeshRenderer]

  - meshRenderer;

<div style="background-color: cyan; height: 2px;"></div>

### ParticleSystemExtensions

<table class="list">
      <tbody><tr><td class="lbl"><a href="ParticlePhysicsExtensions.GetCollisionEvents.html">GetCollisionEvents</a></td><td class="desc">获取 GameObject 的粒子碰撞事件。返回写入数组的事件数。</td></tr>
      <tr><td class="lbl"><a href="ParticlePhysicsExtensions.GetSafeCollisionEventSize.html">GetSafeCollisionEventSize</a></td><td class="desc">与 ParticleSystem.GetCollisionEvents 一起使用的安全数组大小。</td></tr>
      <tr><td class="lbl"><a href="ParticlePhysicsExtensions.GetSafeTriggerParticlesSize.html">GetSafeTriggerParticlesSize</a></td><td class="desc">与 ParticleSystem.GetTriggerParticles 一起使用的安全数组大小。</td></tr>
      <tr><td class="lbl"><a href="ParticlePhysicsExtensions.GetTriggerParticles.html">GetTriggerParticles</a></td><td class="desc">获取粒子触发模块中满足条件的粒子。返回写入数组的粒子数。</td></tr>
      <tr><td class="lbl"><a href="ParticlePhysicsExtensions.SetTriggerParticles.html">SetTriggerParticles</a></td><td class="desc">在 OnParticleTrigger 调用过程中，将修改的粒子写回到粒子系统。</td></tr>
    </tbody></table>

<div style="background-color: cyan; height: 2px;"></div>


### ParticleSystemEvent

<table class="list">
      <tbody><tr><td class="lbl"><a href="ParticleCollisionEvent-colliderComponent.html">colliderComponent</a></td><td class="desc">粒子击中的 GameObject 的 Collider 或 Collider2D。</td></tr>
      <tr><td class="lbl"><a href="ParticleCollisionEvent-intersection.html">intersection</a></td><td class="desc">碰撞的交点（采用世界坐标）。</td></tr>
      <tr><td class="lbl"><a href="ParticleCollisionEvent-normal.html">normal</a></td><td class="desc">碰撞交点处的几何法线。</td></tr>
      <tr><td class="lbl"><a href="ParticleCollisionEvent-velocity.html">velocity</a></td><td class="desc">碰撞交点处的入射速度。</td></tr>
    </tbody></table>
<div style="background-color: cyan; height: 2px;"></div>

### Terrain

#### [变量]

<table class="list">
      <tbody><tr><td class="lbl"><a href="Terrain-activeTerrain.html">activeTerrain</a></td><td class="desc">激活的地形。这是一个便捷函数，用于获取场景中的主要地形。</td></tr>
      <tr><td class="lbl"><a href="Terrain-activeTerrains.html">activeTerrains</a></td><td class="desc">场景中激活的地形。</td></tr>
      <tr><td class="lbl"><a href="Terrain-heightmapRenderTextureFormat.html">heightmapRenderTextureFormat</a></td><td class="desc">地形高度贴图的 RenderTextureFormat。</td></tr>
      <tr><td class="lbl"><a href="Terrain-heightmapTextureFormat.html">heightmapTextureFormat</a></td><td class="desc">地形高度贴图的纹理格式。</td></tr>
    </tbody></table>

<table class="list">
      <tbody><tr><td class="lbl"><a href="Terrain-allowAutoConnect.html">allowAutoConnect</a></td><td class="desc">指定地形区块是否将自动连接到相邻区块。</td></tr>
      <tr><td class="lbl"><a href="Terrain-bakeLightProbesForTrees.html">bakeLightProbesForTrees</a></td><td class="desc">指定是否应为地形上的树烘焙内部光照探针数组。只能在 Editor 中使用。</td></tr>
      <tr><td class="lbl"><a href="Terrain-basemapDistance.html">basemapDistance</a></td><td class="desc">超出底图距离的高度贴图斑块将使用预先计算的低分辨率底图。</td></tr>
      <tr><td class="lbl"><a href="Terrain-bottomNeighbor.html">bottomNeighbor</a></td><td class="desc">地形底部邻居。</td></tr>
      <tr><td class="lbl"><a href="Terrain-castShadows.html">castShadows</a></td><td class="desc">地形是否应投射阴影？</td></tr>
      <tr><td class="lbl"><a href="Terrain-collectDetailPatches.html">collectDetailPatches</a></td><td class="desc">回收内存中的细节斑块。</td></tr>
      <tr><td class="lbl"><a href="Terrain-deringLightProbesForTrees.html">deringLightProbesForTrees</a></td><td class="desc">如果启用，则从树上的探针中消除振铃。</td></tr>
      <tr><td class="lbl"><a href="Terrain-detailObjectDensity.html">detailObjectDensity</a></td><td class="desc">细节对象的密度。</td></tr>
      <tr><td class="lbl"><a href="Terrain-detailObjectDistance.html">detailObjectDistance</a></td><td class="desc">如果不超出该距离，则显示细节对象。</td></tr>
      <tr><td class="lbl"><a href="Terrain-drawHeightmap.html">drawHeightmap</a></td><td class="desc">指定是否应绘制地形高度贴图。</td></tr>
      <tr><td class="lbl"><a href="Terrain-drawInstanced.html">drawInstanced</a></td><td class="desc">设置为 true 可启用地形实例渲染器。默认值为 false。</td></tr>
      <tr><td class="lbl"><a href="Terrain-drawTreesAndFoliage.html">drawTreesAndFoliage</a></td><td class="desc">指定是否应绘制地形树和细节。</td></tr>
      <tr><td class="lbl"><a href="Terrain-editorRenderFlags.html">editorRenderFlags</a></td><td class="desc">控制应渲染地形的哪个部分。</td></tr>
      <tr><td class="lbl"><a href="Terrain-freeUnusedRenderingResources.html">freeUnusedRenderingResources</a></td><td class="desc">如果在若干帧内未使用某些用于地形的每摄像机渲染资源，是否应将它们释放掉。</td></tr>
      <tr><td class="lbl"><a href="Terrain-groupingID.html">groupingID</a></td><td class="desc">用于自动连接的分组 ID。</td></tr>
      <tr><td class="lbl"><a href="Terrain-heightmapMaximumLOD.html">heightmapMaximumLOD</a></td><td class="desc">让您能够从本质上降低用于渲染的高度贴图的分辨率。</td></tr>
      <tr><td class="lbl"><a href="Terrain-heightmapPixelError.html">heightmapPixelError</a></td><td class="desc">切换细节级别时，最坏情况下地形将弹出多少个像素（近似值）。</td></tr>
      <tr><td class="lbl"><a href="Terrain-leftNeighbor.html">leftNeighbor</a></td><td class="desc">地形左侧邻居。</td></tr>
      <tr><td class="lbl"><a href="Terrain-legacyShininess.html">legacyShininess</a></td><td class="desc">地形的光泽度值。</td></tr>
      <tr><td class="lbl"><a href="Terrain-legacySpecular.html">legacySpecular</a></td><td class="desc">地形的镜面反射颜色。</td></tr>
      <tr><td class="lbl"><a href="Terrain-lightmapIndex.html">lightmapIndex</a></td><td class="desc">应用到该地形的烘焙光照贴图的索引。</td></tr>
      <tr><td class="lbl"><a href="Terrain-lightmapScaleOffset.html">lightmapScaleOffset</a></td><td class="desc">用于烘焙光照贴图的 UV 缩放和偏移。</td></tr>
      <tr><td class="lbl"><a href="Terrain-materialTemplate.html">materialTemplate</a></td><td class="desc">用于渲染地形的自定义材质。</td></tr>
      <tr><td class="lbl"><a href="Terrain-materialType.html">materialType</a></td><td class="desc">用于渲染地形的材质类型。可以是内置类型之一，也可以是自定义类型。请参阅 MaterialType。</td></tr>
      <tr><td class="lbl"><a href="Terrain-normalmapTexture.html">normalmapTexture</a></td><td class="desc">返回通过高度贴图采样计算出的法线贴图纹理。仅在使用实例化渲染地形时使用纹理。</td></tr>
      <tr><td class="lbl"><a href="Terrain-patchBoundsMultiplier.html">patchBoundsMultiplier</a></td><td class="desc">设置地形包围盒缩放。</td></tr>
      <tr><td class="lbl"><a href="Terrain-preserveTreePrototypeLayers.html">preserveTreePrototypeLayers</a></td><td class="desc">允许指定 Unity 如何为树实例选择层。</td></tr>
      <tr><td class="lbl"><a href="Terrain-realtimeLightmapIndex.html">realtimeLightmapIndex</a></td><td class="desc">应用到该地形的实时光照贴图的索引。</td></tr>
      <tr><td class="lbl"><a href="Terrain-realtimeLightmapScaleOffset.html">realtimeLightmapScaleOffset</a></td><td class="desc">用于实时光照贴图的 UV 缩放和偏移。</td></tr>
      <tr><td class="lbl"><a href="Terrain-reflectionProbeUsage.html">reflectionProbeUsage</a></td><td class="desc">如何在地形上使用反射探针。请参阅 ReflectionProbeUsage。</td></tr>
      <tr><td class="lbl"><a href="Terrain-rightNeighbor.html">rightNeighbor</a></td><td class="desc">地形右侧邻居。</td></tr>
      <tr><td class="lbl"><a href="Terrain-terrainData.html">terrainData</a></td><td class="desc">存储高度贴图、地形纹理、细节网格和树的地形数据。</td></tr>
      <tr><td class="lbl"><a href="Terrain-topNeighbor.html">topNeighbor</a></td><td class="desc">地形顶部邻居。</td></tr>
      <tr><td class="lbl"><a href="Terrain-treeBillboardDistance.html">treeBillboardDistance</a></td><td class="desc">到摄像机的距离（如果超过该距离，则仅将树渲染为公告牌）。</td></tr>
      <tr><td class="lbl"><a href="Terrain-treeCrossFadeLength.html">treeCrossFadeLength</a></td><td class="desc">使用树来从公告牌方向过渡到网格方向的总距离增量。</td></tr>
      <tr><td class="lbl"><a href="Terrain-treeDistance.html">treeDistance</a></td><td class="desc">渲染树木的最大距离。</td></tr>
      <tr><td class="lbl"><a href="Terrain-treeLODBiasMultiplier.html">treeLODBiasMultiplier</a></td><td class="desc">用于渲染细节级别树（即 SpeedTree 树）的当前细节级别偏差的乘数。</td></tr>
      <tr><td class="lbl"><a href="Terrain-treeMaximumFullLODCount.html">treeMaximumFullLODCount</a></td><td class="desc">以完整细节级别渲染的树的最大数量。</td></tr>
    </tbody></table>

<hr>

#### [函数]

<table class="list">
      <tbody><tr><td class="lbl"><a href="Terrain.AddTreeInstance.html">AddTreeInstance</a></td><td class="desc">向地形添加树实例。</td></tr>
      <tr><td class="lbl"><a href="Terrain.ApplyDelayedHeightmapModification.html">ApplyDelayedHeightmapModification</a></td><td class="desc">使用 TerrainData.SetHeightsDelayLOD 做出更改后，更新地形的细节级别和植被信息。</td></tr>
      <tr><td class="lbl"><a href="Terrain.Flush.html">Flush</a></td><td class="desc">刷新在地形中完成的任何更改，以使其生效。</td></tr>
      <tr><td class="lbl"><a href="Terrain.GetClosestReflectionProbes.html">GetClosestReflectionProbes</a></td><td class="desc">将其 AABB 与地形的 AABB 相交的反射探针填充到列表中。此外，还将提供其权重。权重表示探针对地形的影响程度，在多个反射探针之间发生混合时使用。</td></tr>
      <tr><td class="lbl"><a href="Terrain.GetPosition.html">GetPosition</a></td><td class="desc">获取地形的位置。</td></tr>
      <tr><td class="lbl"><a href="Terrain.GetSplatMaterialPropertyBlock.html">GetSplatMaterialPropertyBlock</a></td><td class="desc">通过复制到 dest MaterialPropertyBlock 对象来获取之前设置的泼溅材质属性。</td></tr>
      <tr><td class="lbl"><a href="Terrain.SampleHeight.html">SampleHeight</a></td><td class="desc">在相对于地形空间的给定位置（以世界空间定义）进行高度采样。</td></tr>
      <tr><td class="lbl"><a href="Terrain.SetNeighbors.html">SetNeighbors</a></td><td class="desc">允许您设置相邻地形之间的连接。</td></tr>
      <tr><td class="lbl"><a href="Terrain.SetSplatMaterialPropertyBlock.html">SetSplatMaterialPropertyBlock</a></td><td class="desc">在使用泼溅材质渲染地形高度贴图时设置其他材质属性。</td></tr>
    </tbody></table>
<table class="list">
      <tbody><tr><td class="lbl"><a href="Terrain.CreateTerrainGameObject.html">CreateTerrainGameObject</a></td><td class="desc">从 TerrainData 创建包含碰撞体的地形。</td></tr>
      <tr><td class="lbl"><a href="Terrain.SetConnectivityDirty.html">SetConnectivityDirty</a></td><td class="desc">将当前连接状态标记为无效。</td></tr>
    </tbody></table>
### SpriteShapeController

- `using UnityEngine.U2D;`

- RefreshSpriteShape();

- spline

  - GetPointCount();
  - GetPosition(int Index);

  ```cs
  Spline Spl = GetComponent<SpriteShapeController>().spline;
  for (int i = 1; i < Spl.GetPointCount() - 1; ++i)
  {
      print($"{i}:{Spl.GetPosition(i)}");
  }
  ```

  - SetPositions(int index, Vector3 Pos);
  - InsertPointAt(int index, Vector3 Pos);
  - RemovePointAt(int index, Vector3 Pos);
  - Clear();
    - 清除全部点;
  - GetCorner(int index);
  - SetCorner(int index, bool value);
  - GetHeight(int index);
  - SetHeight(int index, float value);
  - GetLeftTangent(int index);
  - SetLeftTangent(int index, Vector3 value);
  - GetRightTangent(int index);
  - SetRightTangent(int index, Vector3 value);
  - GetSpriteIndex(int index);
  - SetSpriteIndex(int index, int value);
  - GetTangentMode(int index);
  - SetTangentMode(int index, ShapeTangentMode mode);
    - TangentMode.Broken
    - TangentMode.Linear
    - TangentMode.Continuous
  - bool isOpenEnded;


<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

[TOC]

<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

# [- - -长代码块- - -]

### [2D刚体自行移动]

#### <追踪>

```cs
    void GoTo(Vector2 Dest, float Speed)
    {
        Vector2 currentPosition = transform.position;
        Vector2 directionOfTravel = Dest - currentPosition;
        directionOfTravel.Normalize();
        Vector2 velocity = directionOfTravel * Speed;
        transform.position = currentPosition + velocity * Time.deltaTime;
    }
```

#### <随机移动>

```cs
    void Movement()
    {
        float speed = Random.Range(10f, 10f);
        Vector2 direction = new Vector2(Random.Range(-1f, 1f), Random.Range(-1f, 1f));
        Vector2 velocity = direction * speed;
        rb2d.velocity = velocity;
        Vector2 position = rb2d.position;
    }
```



<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [2D鼠标位置获取]

```cs
Vector3 GetMousePos()
{
    Vector3 mousePos = Camera.main.ScreenToWorldPoint(Input.mousePosition);
    mousePos.z = -1;
    return mousePos;
}
```

<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [鼠标是否位于UI判断]

```cs
public RectTransform Rect;
public new Camera camera;
```

```cs
bool Res = RectTransformUtility.RectangleContainsScreenPoint(Rect, Input.mousePosition, camera);
```

<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [屏幕坐标转换为本地坐标]

```cs
public Vector3 ScreenToLocalPoint(Vector3 Pos)
    {
        Vector4 A = new Vector4(0, 0, 1920, 1080);
        Vector4 B = new Vector4(-400f, -225f, 400f, 225f);
        Vector2 Offset = new Vector2((B.x - A.x), (B.y - A.y));
        Vector2 Ratio = new Vector2(Pos.x / (A.x + A.z), Pos.y / (A.y + A.w));
        Vector2 Res = new Vector2(Ratio.x * (Mathf.Abs(B.x) + Mathf.Abs(B.z)) + Offset.x, Ratio.y * (Mathf.Abs(B.y) + Mathf.Abs(B.w)) + Offset.y);
        return Res;
    }
```

#### <鼠标点击UI位置获取>

```cs
public void OnPointerDown(PointerEventData Data){
    print(ScreenToLocalPoint(Data.position));
}
```

<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [屏幕坐标转换为世界坐标]

```cs
    public Vector3 GetMousePos()
    {
        Vector3 mousePos = Camera.main.ScreenToWorldPoint(Input.mousePosition);
        mousePos.z = 0; // 层级补偿;
        return mousePos;
    }
```

<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [2D刚体移动 / 动画]

```cs
public Rigidbody2D rb;
public float speed;
public float jumpforce;
public Animator anim;
public Collider2D coll;
public LayerMask ground;
```

```cs
void Update(){
	Movement();
    SwitchAnim();
}
```

```cs
void Movement(){
    float horizonmentalmove = Input.GetAxis("Horiziontal");
    float facedirection = Input.GetAxisRaw("Horizontal");
    if (horizonmentalmove != 0){
        anim.SetFloat("running", Mathf.Abs(facedirection));
        rb.velocity = new Vector2(horizonmentalmove * speed, rb.velocity.y);
    }
    if (facedirection != 0){
    transform.localScale = new Vector2(facedirection * Mathf.Abs(transform.localScale.x), 1 * Mathf.Abs(transform.localScale.y));
    }
    if (Input.GetButtonDown("Jump") || Input.GetKeyDown("w") || Input.GetKeyDown("up")){
        rb.velocity = new Vector2(rb.velocity.x, jumpforce);
        anim.SetBooll("jumping", true);
    }
}
```

```cs
void SwitchAnim(){
    anim.SetBool("idle", false);
    if (anim.GetBool("jumping")){
        if (rb.velocity.y < 0 ){
            anim.setBool("jumping", false);
            anim.SetBool("falling", true);
        }
    }
    else if (coll.IsTouchingLaters(ground)){
        anim.SetBool("falling", false);
        anim.SetBool("idle", true);
    }
}
```

<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [2D镜头跟随]

```cs
Transform target;
Vector3 velocity = Vector3.zero;

[Range(0, 1)]
public float smoothTime; // 设置相机跟随灵敏度; 取值越大镜头飘逸越明显; 
public Vector3 positionOffset = new Vector3(0, 0, -5); // 相机位移补偿, 避免z轴取值>=0时相机无法观测场景;

[Header("Axis Limitation")]
public Vector2 xLimit; // (x, y) - x: 最小x值; y: 最大x值;
public Vector2 yLimit; // (x, y) - x: 最小y值; y: 最大y值;

private void Awake(){
    target = GameObject.FindGameObjectWithTag("Player").transform;
}

private void LateUpdate(){
    Vector3 targetPosition = target.position + positionOffset;
    
    targetPosition = new Vector3(Mathf.Clamp(targetPosition.x, xLimit.x, xLimit.y), Mathf.Clamp(targetPosition.y, yLimit.x, yLimit.y), -10); // 镜头限制;
    
    transform.position = Vector3.SmoothDamp(transform.position, targetPosition, ref velocity, smoothTime);
}
```

<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [2D鼠标滑轮调整摄像机]

```cs
using UnityEngine;
public class CameraZoom : MonoBehaviour
{
    public float zoomSpeed = 10f;
    public float minZoom = 5f;
    public float maxZoom = 20f;
    void Update()
    {
        float scroll = Input.GetAxis("Mouse ScrollWheel");
        if (scroll != 0f)
        {
            float zoom = Camera.main.orthographicSize - scroll * zoomSpeed;
            zoom = Mathf.Clamp(zoom, minZoom, maxZoom);
            Camera.main.orthographicSize = zoom;
        }
    }
}

```

```cs
// 背景大小跟随屏幕; 
using UnityEngine;

public class CameraZoom : MonoBehaviour
{
    public float zoomSpeed = 10f;
    public float minZoom = 5f;
    public float maxZoom = 20f;
    public GameObject bg;
    void Update()
    {
        float scroll = Input.GetAxis("Mouse ScrollWheel");
        if (scroll != 0f)
        {
            float zoom = Camera.main.orthographicSize - scroll * zoomSpeed;
            zoom = Mathf.Clamp(zoom, minZoom, maxZoom);

            float size = Camera.main.orthographicSize;
            float rate = zoom / size;
            float res_x = bg.transform.localScale.x * rate;
            float res_y = bg.transform.localScale.y * rate;
            float res_z = bg.transform.localScale.z * rate;
            
            Camera.main.orthographicSize = zoom;
            bg.transform.localScale = new Vector3(res_x, res_y, res_z);
        }
    }
}

```



<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [2D组件控制移动]

```cs
public float speed;
public float clampLeft;
public float clampRight;
```

```cs
void Update(){
    if (Input.GetKey(KeyCode.RightArrow) && transform.position.x < clampRight){
        transform.Translate(new Vector3(speed * Time.deltaTime, 0, 0));
    }
    if (Input.GetKey(KeyCode.LeftArrow) && transform.position.x > clampLeft){
        transform.Translate(new Vector3(-speed * Time.deltaTime, 0, 0));
    }
}
```

- Input.GetKey(): 检测按键是否被**持续按下**;
- Input.GetKeyDown(): 仅检测按键是否被按下;

<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [2D碰撞检测]

```cs
void OnCollisionEnter2D(Collision2D collision){
    if (collision.gameObject.tag == "Enemy"){
        // Destroy(collision.gameObject);
        Debug.Log(collision.relativeVelocity.magnitude);
        collision.gameObject.SetActive(false); // 隐藏目标;
        gameObject.SetActive(false); // 隐藏本身;
    }
}
void OnTriggerEnter2D(Collider2D collision){ }
```

<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [2D Tile生成]

```cs
using UnityEngine.Tilemaps;
```

```cs
public Tilemap tilemap;
public Tile tile;
```

```cs
void func(){
    Vector3Int pos = new Vector3Int((int)rb.position.x, (int)rb.position.y, 0);
    tilemap.SetTile(pos, tile);
}
```

<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [2D Layer碰撞检测]

```cs
public Collider2D coll;
public LayerMask ground;
```

```cs
void func(){
    if (coll.IsTouchingLayers(ground)){ }
}
```

<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [动画转换]

```cs
    void SwitchAnim()
    {
        anim.SetBool("isStand", false);
        if (anim.GetBool("isJump"))
        {
            if (rb.velocity.y < 0)
            {
                anim.SetBool("isJump", false);
                anim.SetBool("isFall", true);
            }

        }
        else if (coll.IsTouchingLayers(ground))
        {
            anim.SetBool("isFall", false);
            anim.SetBool("isStand", true);
        }
    }
```



<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [摇杆轮盘]

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.EventSystems;
using UnityEngine.Events;
```

```cs
public struct JoyStickData // 结构体 - 摇杆数据;
{
    public Vector2 dir; // 移动方向;
    public float radius; // 移动半径;

    public JoyStickData(Vector2 d, float r)
    {
        this.dir = d;
        this.radius = r;
    }
    public Vector2 GetPos()
    {
        return dir * radius;
    }
}
```

```cs
public class JoyStick : MonoBehaviour, IPointerDownHandler, IPointerUpHandler, IDragHandler // 三个接口，点击、抬起、拖拽;
```

```cs
    public RectTransform bound; // 摇杆外圈;
    public RectTransform center; // 摇杆内圈;
    public float radius; // 移动限制的半径;
```

```cs
    private JoyStickData HandleEventData(PointerEventData eventData)
    {
        Vector2 dir;
        RectTransformUtility.ScreenPointToLocalPointInRectangle(bound, eventData.position, eventData.pressEventCamera, out dir);
        float r = dir.magnitude;
        dir = dir.normalized;
        r = Mathf.Clamp(r, 0, radius);
        
        return new JoyStickData(dir, r);
    }
```

```cs
    public void OnDrag(PointerEventData eventData)
    {
        var data = HandleEventData(eventData);
        center.localPosition = data.GetPos();
        onJoystickMove(data.dir, data.radius);
    }
```

```cs
    public void OnPointerDown(PointerEventData eventData)
    {
        var data = HandleEventData(eventData);
        center.localPosition = data.GetPos();
        onJoystickDown(data.dir, data.radius);

    }
```

```cs
    public void OnPointerUp(PointerEventData eventData)
    {
        var data = HandleEventData(eventData);
        center.localPosition = Vector2.zero; //抬起后回到0坐标
        onJoystickUp(data.dir, data.radius);
    }
```

```cs
    public virtual void onJoystickDown(Vector2 V, float R)
    {

    }
```

```cs
    public virtual void onJoystickUp(Vector2 V, float R)
    {
        rb.velocity = Vector2.zero;
    }
```

```cs
    public virtual void onJoystickMove(Vector2 V, float R)
    {
        Movement(V);
    }
```

<hr><hr><hr>


```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.EventSystems;
using UnityEngine.Events;


public struct JoyStickData
{
    public Vector2 dir;
    public float radius;
    
    public JoyStickData(Vector2 d, float r)
    {
        this.dir = d;
        this.radius = r;
    }
    public Vector2 GetPos()
    {
        return dir * radius;
    }
}



public class JoyStick : MonoBehaviour, IPointerDownHandler, IPointerUpHandler, IDragHandler
{
    public RectTransform bound;
    public RectTransform center;
    public float radius;
    
    public Rigidbody2D rb;
    public float speed;
    public float jumpforce;


    private JoyStickData HandleEventData(PointerEventData eventData)
    {
        Vector2 dir;
        RectTransformUtility.ScreenPointToLocalPointInRectangle(bound, eventData.position, eventData.pressEventCamera, out dir);
        float r = dir.magnitude;
        dir = dir.normalized;
        r = Mathf.Clamp(r, 0, radius);

        return new JoyStickData(dir, r);
    }
    
    public void OnDrag(PointerEventData eventData)
    {
        var data = HandleEventData(eventData);
        center.localPosition = data.GetPos();
        onJoystickMove(data.dir, data.radius);
    }

    public void OnPointerDown(PointerEventData eventData)
    {
        var data = HandleEventData(eventData);
        center.localPosition = data.GetPos();
        onJoystickDown(data.dir, data.radius);

    }

    public void OnPointerUp(PointerEventData eventData)
    {
        var data = HandleEventData(eventData);
        center.localPosition = Vector2.zero;
        onJoystickUp(data.dir, data.radius);
    }
    
    public virtual void onJoystickDown(Vector2 V, float R){ }
    
    public virtual void onJoystickUp(Vector2 V, float R){ rb.velocity = Vector2.zero; }
    
    public virtual void onJoystickMove(Vector2 V, float R){ Movement(V); }




    void Movement(Vector2 V)
    {
        float var_x = V.x;
        float var_y = V.y;
        float horizonmentalmove = var_x;
        if (horizonmentalmove != 0)
        {
            rb.velocity = new Vector2(horizonmentalmove * speed, rb.velocity.y);
        }
    }
}


```

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.EventSystems;
using UnityEngine.Events;


public struct JoyStickData
{
    public Vector2 dir;
    public float radius;

    public JoyStickData(Vector2 d, float r)
    {
        this.dir = d;
        this.radius = r;
    }
    public Vector2 GetPos()
    {
        return dir * radius;
    }
}



public class JoyStick : MonoBehaviour, IPointerDownHandler, IPointerUpHandler, IDragHandler
{
    public RectTransform bound;
    public RectTransform center;
    public float radius;

    public Rigidbody2D rb;
    public float speed;
    public float jumpforce;

    public Collider2D coll;
    public LayerMask ground;

    private bool flg = false;
    private Vector2 temp;


    private JoyStickData HandleEventData(PointerEventData eventData)
    {
        Vector2 dir;
        RectTransformUtility.ScreenPointToLocalPointInRectangle(bound, eventData.position, eventData.pressEventCamera, out dir);
        float r = dir.magnitude;
        dir = dir.normalized;
        r = Mathf.Clamp(r, 0, radius);

        return new JoyStickData(dir, r);
    }

    public void OnDrag(PointerEventData eventData)
    {
        var data = HandleEventData(eventData);
        center.localPosition = data.GetPos();
        onJoystickMove(data.dir, data.radius);
    }

    public void OnPointerDown(PointerEventData eventData)
    {
        var data = HandleEventData(eventData);
        center.localPosition = data.GetPos();
        onJoystickDown(data.dir, data.radius);

    }

    public void OnPointerUp(PointerEventData eventData)
    {
        var data = HandleEventData(eventData);
        center.localPosition = Vector2.zero;
        onJoystickUp(data.dir, data.radius);
    }

    public virtual void onJoystickDown(Vector2 V, float R) { }

    public virtual void onJoystickUp(Vector2 V, float R) { rb.velocity = Vector2.zero;flg = false; }

    public virtual void onJoystickMove(Vector2 V, float R) { /*Movement(V);*/flg = true;temp = V; }

    void Update()
    {
        if (flg)
        {
            Movement(temp);
        }
    }


    void Movement(Vector2 V)
    {
        float var_x = V.x;
        float var_y = V.y;
        float horizonmentalmove = var_x;
        Debug.Log(horizonmentalmove);
        Vector2 scale = rb.transform.localScale;
        if (horizonmentalmove > 0) { rb.transform.localScale = new Vector2(Mathf.Abs(scale.x), scale.y); }
        if (horizonmentalmove < 0) { rb.transform.localScale = new Vector2(-1 * Mathf.Abs(scale.x), scale.y); }


        if (horizonmentalmove != 0)
        {
            rb.velocity = new Vector2(horizonmentalmove * speed, rb.velocity.y);
        }


        if (var_y >= 0.8)
        {
            if (coll.IsTouchingLayers(ground))
            {
                rb.velocity = new Vector2(rb.velocity.x, jumpforce);
            }
        }
    }
}


```



<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [2D 物体拖拽]

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Drag : MonoBehaviour
{
    private void OnMouseDrag() 
    {
        transform.position = GetMousePos();
    }
    Vector3 GetMousePos()
    {
        Vector3 mousePos = Camera.main.ScreenToWorldPoint(Input.mousePosition);
        mousePos.z = 0;
        return mousePos;
    }

}

```

```cs
// 方法二; 
    void Update()
    {
        if (Input.GetMouseButtonDown(0))
        {
            RaycastHit2D hit = Physics2D.Raycast(Camera.main.ScreenToWorldPoint(Input.mousePosition), Vector2.zero);
            // 如果碰撞到了物体;
            if (hit.collider != null && hit.collider.gameObject == gameObject)
            {
                // 开始拖拽物体;
                isDragging = true;
                rb.isKinematic = true;
                // 设置物体为运动学物体，以便拖拽;
                mousePosition = Camera.main.ScreenToWorldPoint(Input.mousePosition);
                // 记录鼠标位置;
                objectPosition = transform.position - mousePosition;
                // 记录物体位置;
                distance = Vector3.Distance(transform.position, Camera.main.transform.position);
                // 记录鼠标与物体的距离;
            }
        }
        else if (Input.GetMouseButtonUp(0))
        {
            isDragging = false;
            rb.isKinematic = false;
        }

        if (isDragging)
        {
            mousePosition = Camera.main.ScreenToWorldPoint(Input.mousePosition);
            transform.position = new Vector3(mousePosition.x + objectPosition.x, mousePosition.y + objectPosition.y, distance);
        }
    }
```

- `Vector3.Distance(transform.position, Camera.main.transform.position)`: 物体与相机距离; 
- `Rigidbody2D.isKinematic = true`: 设置为运动学物体, 期间不受重力等其他力影响; 保留设置之前受到的力; 





<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [2D 朝向旋转]

```cs
    public void LookAt2D(float angles)
    {
        Vector3 playerRelativePosition = player.position - transform.position;

        Quaternion lookRotation = Quaternion.LookRotation(Vector3.forward, new Vector2(playerRelativePosition.x, playerRelativePosition.y));

        Vector3 lookRotationVector = lookRotation.eulerAngles;
        lookRotationVector.z -= angles;

        transform.rotation = Quaternion.Euler(lookRotationVector);
    }
```

<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [3D 朝向旋转]

```cs
    /// <summary>
    /// 用某个轴去朝向物体
    /// </summary>
    /// <param name="tr_self">朝向的本体</param>
    /// <param name="lookPos">朝向的目标</param>
    /// <param name="directionAxis">方向轴，取决于你用那个方向去朝向</param>
    /// <param name="OffsetZ">Z轴旋转数值补偿</param>
    void AxisLookAt(Transform tr_self, Vector3 lookPos, Vector3 directionAxis, float OffsetZ)
    {
        var rotation = tr_self.rotation;
        var targetDir = lookPos - tr_self.position;
        //指定哪根轴朝向目标,自行修改Vector3的方向
        var fromDir = tr_self.rotation * directionAxis;
        //计算垂直于当前方向和目标方向的轴
        var axis = Vector3.Cross(fromDir, targetDir).normalized;
        //计算当前方向和目标方向的夹角
        var angle = Vector3.Angle(fromDir, targetDir);
        //将当前朝向向目标方向旋转一定角度，这个角度值可以做插值
        tr_self.rotation = Quaternion.AngleAxis(angle, axis) * rotation;
        tr_self.localEulerAngles = new Vector3(0, tr_self.localEulerAngles.y, OffsetZ);
        //后来调试增加的，因为我想让x，z轴向不会有任何变化; Z轴旋转数值补偿;
    }
    void Update()
    {
    AxisLookAt(this.transform, Player.transform.position, Vector3.up);//朝向目标体
    }

```

<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [跟随玩家]

```cs
    void Follow(Vector2 Dest, float Speed)
    {
        Vector2 currentPosition = transform.position;
        Vector2 directionOfTravel = Dest - currentPosition;
        directionOfTravel.Normalize();
        Vector2 velocity = directionOfTravel * Speed;
        Vector2 TempPos = currentPosition + velocity * Time.deltaTime;
        transform.position = new Vector3(TempPos.x, TempPos.y, transform.position.z);

    }
```

<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [获取距离补偿坐标]

```cs
    Vector3 GetDestPos(Vector3 Dest, float num)
    {
        Vector3 SelfPos = transform.position;
        Vector3 Gap = Dest - SelfPos;
        Vector3 Direction = (Dest - SelfPos).normalized;
        float Distance = Vector3.Distance(Dest, SelfPos) + num;
        Vector3 Res = SelfPos + Direction * Distance;
        return Res;
    }
```

<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

### [LineRenderer连线]

```cs
using UnityEngine;

public class ConnectLine : MonoBehaviour
{
    public Transform objectA;
    public Transform objectB;

    private LineRenderer lineRenderer;

    private void Start()
    {
        lineRenderer = GetComponent<LineRenderer>();
    }

    private void Update()
    {
        if (objectA != null && objectB != null)
        {
            lineRenderer.SetPosition(0, objectA.position);
            lineRenderer.SetPosition(1, objectB.position);
        }
    }
}
```

### [天空球定时切换]

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SkyboxManager : MonoBehaviour
{
    [SerializeField]
    public List<Material> SkyboxMaterials;
    [Header("几秒后开始切换")]
    public float DelayTime = 3f;
    [Header("每隔几秒切换一次")]
    public float Interval = 10f;
    private int Index = 0;
    void Start()
    {
        InvokeRepeating(nameof(ChangeSkybox), DelayTime, Interval);
    }
    private void ChangeSkybox()
    {
        if (SkyboxMaterials != null)
        {
            RenderSettings.skybox = SkyboxMaterials[Index];
            if (Index < SkyboxMaterials.Count - 1) { Index++; }
            else { Index = 0; }
        }
        
    }
}
```

### [屏幕渐变变黑]

```cs
    public void GradualMask(float Time)
    {
        StartCoroutine("BeginGradualMask");
        Invoke("EndGradualMask", Time);
    }
    private IEnumerator BeginGradualMask()
    {
        while (true)
        {
            Color MyColor = GameObject.Find("ScreenMask").GetComponent<Image>().color;
            MyColor.a += 0.1f;
            GameObject.Find("ScreenMask").GetComponent<Image>().color = MyColor;
            yield return new WaitForSeconds(0.11f);
        }
    }
    private void EndGradualMask()
    {
        StopCoroutine("BeginGradualMask");
        GameObject.Find("ScreenMask").GetComponent<Image>().color = new Color(0f, 0f, 0f, 0f);
    }
```

### [PostProcess-Vignette插件控制DEMO]

```cs
using UnityEngine;
using UnityEngine.Rendering.PostProcessing;
public class VignettePulse : MonoBehaviour
{
PostProcessVolume m_Volume;
Vignette m_Vignette;
void Start()
{
   m_Vignette = ScriptableObject.CreateInstance<Vignette>();
   m_Vignette.enabled.Override(true);
   m_Vignette.intensity.Override(1f);
   m_Volume = PostProcessManager.instance.QuickVolume(gameObject.layer, 100f, m_Vignette);
}
void Update()
{
    m_Vignette.intensity.value = Mathf.Sin(Time.realtimeSinceStartup);
}
void OnDestroy()
{
   RuntimeUtilities.DestroyVolume(m_Volume, true, true);
}
}
```

### [音效播放时间控制]

```cs
using UnityEngine;
using System.Collections;

public class SoundPlayTime : MonoBehaviour {
	public bool playOnAwake = false;
	public bool loopCheck = false;
	private float timer;
	public float waitTime = 1.0f;
	private float loopTime = 0.0f;
	public float loopWaitTime = 0.0f;
	private bool flag = false;
	public  AudioClip sound01;
	private AudioSource audioSource;
	void Start  () {
		loopTime = loopWaitTime;
		audioSource = GetComponent<AudioSource>();
		audioSource.playOnAwake = playOnAwake ;
		if( audioSource.playOnAwake == true){
			audioSource.clip = sound01;
			audioSource.Play ();
			if(loopCheck == false){
				Destroy(this);
			}
		}else{
			loopTime = 0;
		}
	}
	void Update () {
		loopTime -= Time.deltaTime;
		timer += Time.deltaTime;
		if((timer >= waitTime) && (flag == false) && (loopTime <= 0)){
			//sound01.PlayOneShot(sound01.clip);
			audioSource.clip = sound01;
			audioSource.Play ();
			flag = false;
			loopTime = loopWaitTime;
			if( loopCheck == false){
				Destroy(this);
			}

		}
	}
}
```

### [随距离衰减音效播放]

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class CollisionSound : MonoBehaviour
{
    private AudioSource audio;
    public GameObject Player;
    public float DestroyDelay = 1f;
    public Vector2 Span = new Vector2(5f, 20f);
    void Start()
    {
        float Distance = Vector3.Distance(Player.transform.position, transform.position);
        audio = GetComponent<AudioSource>();
        if (Distance < Span.y)
        {
            if (Distance > Span.x)
            {
                audio.volume = Distance / Span.y;
            }
            audio.Play();
        }
        Invoke("DestroySelf", DestroyDelay);
    }
    void DestroySelf()
    {
        Destroy(gameObject);
    }
}
```

#### <粒子碰撞播放音效>

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayCollisionSound : MonoBehaviour
{
    private ParticleSystem Particle;
    public List<ParticleCollisionEvent> collisionEvents;
    public GameObject SoundEffect;
    void Start()
    {
        Particle = GetComponent<ParticleSystem>();
        collisionEvents = new List<ParticleCollisionEvent>();
    }
    void OnParticleCollision(GameObject other)
    {
        int num = Particle.GetCollisionEvents(other, collisionEvents);
        Vector3 Pos = collisionEvents[0].intersection;
        GameObject Obj = Instantiate(SoundEffect, Pos, Quaternion.identity);
        Obj.SetActive(true);
    }
}
```

### [PartickleSystem粒子击中刚体]

```cs
public ParticleSystem part;
public List<ParticleCollisionEvent> collisionEvents;
void Start()
{
        part = GetComponent<ParticleSystem>();
        collisionEvents = new List<ParticleCollisionEvent>();
}
void OnParticleCollision(GameObject other)
{
        int numCollisionEvents = part.GetCollisionEvents(other, collisionEvents);
        Rigidbody rb = other.GetComponent<Rigidbody>();
        int i = 0;
        while (i < numCollisionEvents)
        {
            if (rb)
            {
                Vector3 pos = collisionEvents[i].intersection;
                Vector3 force = collisionEvents[i].velocity * 10;
                rb.AddForce(force);
            }
            i++;
        }
}
```

### [延迟执行 / 仿写Invoke]

```cs
public delegate void Action();
public void Func(){    
    StartCoroutine(Delay.Do(delegate
    {
        // TODO;
    }, 3f));
}
public class Delay : MonoBehaviour
{
    public static IEnumerator Do(Action action, float delaySeconds)
    {
        yield return new WaitForSeconds(delaySeconds);
        action();
    }
}
```

### [水下视角]

```cs
using UnityEngine;
using System.Collections;

public class Underwater : MonoBehaviour
{
    public float UnderwaterLevel = 0;
    public Color FogColor = new Color(0, 0.4f, 0.7f, 1);
    public float FogDensity = 0.04f;
    public FogMode FogMode = FogMode.Exponential;

    private bool defaultFog;
    private Color defaultFogColor;
    private float defaultFogDensity;
    private FogMode defaultFogMod;
    private Material defaultSkybox;

    private void Start()
    {
        defaultFog = RenderSettings.fog;
        defaultFogColor = RenderSettings.fogColor;
        defaultFogDensity = RenderSettings.fogDensity;
        defaultFogMod = RenderSettings.fogMode;
    }

    void Update()
    {

        if (transform.position.y < UnderwaterLevel)
        {
            RenderSettings.fog = true;
            RenderSettings.fogColor = FogColor;
            RenderSettings.fogDensity = FogDensity;
            RenderSettings.fogMode = FogMode;
        }
        else
        {
            RenderSettings.fog = defaultFog;
            RenderSettings.fogColor = defaultFogColor;
            RenderSettings.fogDensity = defaultFogDensity;
            RenderSettings.fogMode = defaultFogMod;
            RenderSettings.fogStartDistance = -300;
        }
    }
}
```

### [双击]

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;


public class TestDoubleClick : MonoBehaviour
{
    float time = 0;
    void Start()
    {
        time = Time.time;
    }
    public void OnMouseDown()
    {
        //当第二次点击鼠标，且时间间隔小于0.3秒时，是双击鼠标
        if (Time.time - time <= 0.3f)
        {
            gameObject.SetActive(true);
        }
        //否则，是单击鼠标
        else
        {
            gameObject.SetActive(false);
            // targetFloor.SetActive(true);
            
        }
        time = Time.time;
    }
}

```

### [3D刚体移动|旋转]

```cs
forward = transform.forward;
right = transform.right;    
void MoveByForce()
    {
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");

        rb.AddForce(forward * vertical * Speed);
        print(Vector3.forward * vertical * Speed);
        rb.AddForce(right * horizontal * Speed);

    }
    void MoveByVelocity()
    {
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");
        if (Input.GetKey(KeyCode.W) | Input.GetKey(KeyCode.S))
        {
            rb.velocity = forward * vertical * Speed;
        }
        if (Input.GetKey(KeyCode.A) | Input.GetKey(KeyCode.D))
        {
            rb.velocity = right * horizontal * Speed;
        }
    }
    void RotateByMoveRotation()
    {
        if (Input.GetKey(KeyCode.A))
        {
            rb.MoveRotation(Quaternion.Euler(new Vector3(0f, RotateSpeed, 0f) + rb.rotation.eulerAngles));
        }
        if (Input.GetKey(KeyCode.D))
        {
            rb.MoveRotation(Quaternion.Euler(new Vector3(0f, RotateSpeed * -1f, 0f) + rb.rotation.eulerAngles));
        }
    }
```

### [点击动画]

#### [效果动画]

```cs
using UnityEngine;
using System.Linq;

public class MouseClickEffect : MonoBehaviour
{
    //点击效果动画
    Animation pointAnim;
    void Start()
    {
        //私有变量赋值
        pointAnim = GetComponentInChildren<Animation>();
        //确保显示点击效果的UI画布处于最顶层
        int canMaxIndex = FindObjectsOfType<Canvas>().Max((item) => item.sortingOrder);
        GetComponent<Canvas>().sortingOrder = canMaxIndex + 1;
    }
    void Update()
    {
        if (Input.GetMouseButtonDown(0) && pointAnim)
        {
            pointAnim.transform.position = Input.mousePosition;
            if (pointAnim.isPlaying)
                pointAnim.Stop();
            pointAnim.Play();
        }
    }
}

```

#### [帧动画]

```cs
[CreateAssetMenu]
public class CursorAnimation : ScriptableObject
{
    public CursorType cursorType;
    public Texture2D[] textureArray;
    public float frameRate;
    public Vector2 offset;
}
public class CursorMananger : MonoBehaviour
{
    public CursorAnimation[] cursorAnimations;
    private CursorAnimation currentAnimation;
    private float frameRate;
    private int frameCount;
    private int currentFrame;
    private float frameTimer;
    private void Start()
    {
        SetActiveCursorAnimation(cursorAnimations[0]);
    }
    private void Update()
    {
        frameTimer -= Time.deltaTime;
        if (frameTimer <= 0f)
        {
            frameTimer += frameRate;
            currentFrame = (currentFrame + 1) % frameCount;
            Cursor.SetCursor(currentAnimation.textureArray[currentFrame], currentAnimation.offset, CursorMode.Auto);
        }
        if (Input.GetKeyDown(KeyCode.A)) SetActiveCursorAnimation(cursorAnimations[(int)CursorType.Arrow]);
        if (Input.GetKeyDown(KeyCode.S)) SetActiveCursorAnimation(cursorAnimations[(int)CursorType.Star]);
    }
    private void SetActiveCursorAnimation(CursorAnimation value)
    {
        currentAnimation = value;
        currentFrame = 0;
        frameTimer = value.frameRate;
        frameCount = value.textureArray.Length;
    }
}

```

#### [两帧切换]

```cs
using UnityEngine;
public class CursorPress : MonoBehaviour
{
	public Texture2D PressedCursor;
	public Vector2 Offset;
    void Update()
    {
        if(Input.GetMouseButtonDown(0)){
			Cursor.SetCursor(PressedCursor, Offset, CursorMode.Auto);
		}
		if(Input.GetMouseButtonUp(0)){
			Cursor.SetCursor(null, Vector2.zero, CursorMode.Auto);
		}
    }
}

```

<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

# [- - -标签- - -]

## [常用]

### [Space]

```cs
[Space(30)]
public int HP;
[Space(50)]
public string name;
```

- 与上一个字段形成一个间隙;

### [Header]


```cs
[Header("Demo-1")]
public int HP;
public int MP;
[Header("Demo-2")]
public string name;
```

1. 给定义的字段加描述;

### [Range]

```cs
[Range(1, 10)]
public int Num;
```

### [ToolTip]

```cs
[ToolTip("Demo")]
public int Num;
```

- 鼠标悬停在字段上时弹出描述;

## [菜单]

### [ContextMenu("Func")]

- 在Inspector中右键当前脚本组件出现的菜单中可运行指定函数;

### [ContextMenuItem("显示的方法名", "方法名")]

```cs
[ContextMenuItem("add", "fun")]
public int num;
void fun(){
    num += 1;
}
```

- 标记字段, 给字段右键菜单段添加一个方法;

## [序列化]

### [SerializeField]

```cs
[SerializeField]
private int Num;
```

- 在Inspector面板中显示非Public属性并序列化;
- 如果一个字段或属性未被标记为 `[SerializeField]`，则该字段或属性在 Unity 中将不会被保存。这意味着，如果你在 Unity 编辑器中修改了这个字段或属性的值，它将不会在下一次启动应用程序时保持修改后的值。
- 标记字段或属性为 `[SerializeField]`，将会导致该字段或属性可以暴露给不小心或有恶意的代码。

### [NonSerialize]


- 防止该成员变量被序列化。
- 当一个字段或属性被标记为 `[NonSerialized]` 时，Unity 在序列化脚本对象时将跳过该成员变量的序列化，不会保存或还原它的值。

### [HideInInspector]


- 使属性在Inspector中隐藏, 仍可序化;

### [System.Serializable]


- 使自定义类可序列化, 即当作一个public成员时可在Inspector显示;

### [FormerlySerializedAs("")]


- 使变量以另外的名称序列化, 在变量自身修改名称时不会丢失之前的序列化的值;

### [MultilineAttribute]


- 在string类变量上使用, 标记后可在Editor上输入多行文字;

## [功能]

### [TextAreaAttribute]


- 把string在Inpector上的编辑区变成TextArea;

### [RequireComponent(typeof(ClassName))]


```cs
[RequireComponent(typeof(Rigidbody2D))]
public class MyAttribute: MonoBehaviour{
}
```

- 当被标记的类被拖到GameObject或者被AddComponent调用时自动为目标添加指定的类;

### [ExecuteInEditMode]


- 在编辑界面让被标记的类起作用;
- 被标记后无需运行程序即可执行当前脚本;

### [AddComponentMenu(".../.../...")]


```cs
[AddComponentMenu("Demo/First")]
public class Demo : MonoBehaviour{
}
```

- 在指定位置上添加该类到Component菜单;

### [CustomEditor(typeof(ClassName))]


```cs
[CustomEditor(typeof(Rigidbody2D))]
public class editortest : Editor{
    public override void OnInspectorGUI(){
        if (GUILayout.Button("Demo")){
            base.OnInspectorGUI();
        }
    }
}
// Rigidbody2D组件编辑界面重载后仅剩自定义"Demo"按钮;
```

- 声明一个Class为自定义Editor的Class, 可制作自定义编辑器;

### [MenuItem()]


- [MenuItem("一级菜单名/二级菜单名 _全局快捷键")]
  - 全局快捷键控制菜单选项;

- [MenuItem("一级菜单名/二级菜单名", false, 1)]

  - 参数true决定给菜单添加验证, 参数1决定菜单优先级;

```cs
[MenuItem("Window/UI Toolkit/Test")]
```

```cs
[MenuItem("Main/First/Second _b")]
public static void Demo(){
}
```

- 在主页面顶部菜单栏自定义选项栏, 执行对应功能;
- 指定函数必须static;

### [ContextMenu("菜单选项名")]

### [CreateAssetMenu()]


- [CreateAssetMenu(menuName = "MySubMenu/Create xxx")]

- [CreateAssetMenu(fileName = "Bullet", menuName = "New Bullet, order = 1")]

## [扩展]

### {Sirenix.OdinInspector}

- `using Sirenix.OdinInspector;`

- [BoxGroup("Title")]

  - 将一个变量放在对应标题的盒子中;

- [FoldoutGroup("Title")]

  - 将一个变量放在对应标题的折叠中;

- [HideIfGroup("Toggle")]

- [ShowIfGroup("Toggle")]

- [OnValueChanged("Func")]

  - 在标签标识的变量改变后直接调用函数Func;

  ```cs
  [OnValueChanged("Func")] public bool test = false;
  public void Func(){
  	print(test);
  }
  ```

# [- - -Shader- - -]

### [轮廓描边]

```cs
//描边Shader  
//by：puppet_master  
//2017.1.5  
Shader "Outline"  
{  
    Properties{  
        _Diffuse("Diffuse", Color) = (1,1,1,1)  
        _OutlineCol("OutlineCol", Color) = (1,0,0,1)  
        _OutlineFactor("OutlineFactor", Range(0,5)) = 0.1  
        _MainTex("Base 2D", 2D) = "white"{}  
    }
    SubShader  
    {
        //描边使用两个Pass，第一个pass沿法线挤出一点，只输出描边的颜色  
        Pass  
        {  
            //剔除正面，只渲染背面
            Cull Front  
              
            CGPROGRAM  
            #include "UnityCG.cginc"  
            fixed4 _OutlineCol;  
            float _OutlineFactor;  
              
            struct v2f  
            {  
                float4 pos : SV_POSITION;  
            };  
              
            v2f vert(appdata_full v)  
            {  
                v2f o;  
                //在vertex阶段，每个顶点按照法线的方向偏移一部分
                //v.vertex.xyz += v.normal * _OutlineFactor;  
                o.pos = mul(UNITY_MATRIX_MVP, v.vertex);  
                //将法线方向转换到视空间  
                float3 vnormal = mul((float3x3)UNITY_MATRIX_IT_MV, v.normal);  
                //将视空间法线xy坐标转化到投影空间
                float2 offset = TransformViewToProjection(vnormal.xy);  
                //在最终投影阶段输出进行偏移操作  
                o.pos.xy += offset * _OutlineFactor;  
                return o;  
            }  
              
            fixed4 frag(v2f i) : SV_Target  
            {  
                //这个Pass直接输出描边颜色  
                return _OutlineCol;  
            }  
              
            //使用vert函数和frag函数  
            #pragma vertex vert  
            #pragma fragment frag  
            ENDCG  
        }

        //正常着色的Pass  
        Pass  
        {  
            CGPROGRAM
            #include "Lighting.cginc"  
            //定义Properties中的变量  
            fixed4 _Diffuse;  
            sampler2D _MainTex;  
            //使用了TRANSFROM_TEX宏就需要定义XXX_ST  
            float4 _MainTex_ST;  
  
            //定义结构体：vertex shader阶段输出的内容  
            struct v2f  
            {  
                float4 pos : SV_POSITION;  
                float3 worldNormal : TEXCOORD0;  
                float2 uv : TEXCOORD1;  
            };  
  
            //定义顶点shader,参数直接使用appdata_base（包含position, noramal, texcoord）  
            v2f vert(appdata_base v)  
            {  
                v2f o;  
                o.pos = mul(UNITY_MATRIX_MVP, v.vertex);  
                //通过TRANSFORM_TEX宏转化纹理坐标
                o.uv = TRANSFORM_TEX(v.texcoord, _MainTex);  
                o.worldNormal = mul(v.normal, (float3x3)_World2Object);  
                return o;  
            }  
  
            //定义片元shader  
            fixed4 frag(v2f i) : SV_Target  
            {  
                //增加一下环境光  
                fixed3 ambient = UNITY_LIGHTMODEL_AMBIENT.xyz * _Diffuse.xyz;  
                //归一化法线
                fixed3 worldNormal = normalize(i.worldNormal);  
                //把光照方向归一化  
                fixed3 worldLightDir = normalize(_WorldSpaceLightPos0.xyz);  
                //根据半兰伯特模型计算像素的光照信息  
                fixed3 lambert = 0.5 * dot(worldNormal, worldLightDir) + 0.5;  
                //最终输出颜色为lambert光强*材质diffuse颜色*光颜色  
                fixed3 diffuse = lambert * _Diffuse.xyz * _LightColor0.xyz + ambient;  
                //进行纹理采样  
                fixed4 color = tex2D(_MainTex, i.uv);  
                color.rgb = color.rgb* diffuse;  
                return fixed4(color);  
            }  
  
            //使用vert函数和frag函数  
            #pragma vertex vert  
            #pragma fragment frag     
  
            ENDCG  
        }  
    }  
    //前面的Shader失效的话，使用默认的Diffuse  
    FallBack "Diffuse"  
}  

```

### [ShaderGraph Debug节点]

```cs
// This gist can be found at https://gist.github.com/bestknighter/660e6a53cf6a6643618d8531f962be2c
// I modified Aras Pranckevičius's awesome shader code to be able to handle Infinite and Not A Number numbers
// Tested on Unity 2023.1.0a15 with ShaderGraph 15.0.1.


// Quick try at doing a "print value" node for Unity ShaderGraph.
//
// Use with CustomFunction node, with two inputs:
// - Vector1 Value, the value to display,
// - Vector2 UV, the UVs of area to display at.
// And one output:
// - Vector4 Color, the color.
// Function name is DoDebug.

// "print in shader" based on this excellent ShaderToy by @P_Malin:
// https://www.shadertoy.com/view/4sBSWW

float DigitBin(const int x)
{
    return x==0?480599.0:x==1?139810.0:x==2?476951.0:x==3?476999.0:x==4?350020.0:x==5?464711.0:x==6?464727.0:x==7?476228.0:x==8?481111.0:x==9?481095.0:0.0;
}

float DigitLet(const int x)
{
    // 1=I, 2=n, 3=F, 4=a
    return x==1?467495.0:x==2?1877.0:x==3?463633.0:x==4?30069.0:0.0;
}

bool isnan_NonOptimizableAway(const float fValue) {
    return ((asuint(fValue) & 0x7FFFFFFF) > 0x7F800000);
}

bool isinf_NonOptimizableAway(const float fValue) {
    return ((asuint(fValue) & 0x7FFFFFFF) == 0x7F800000);
}

float GetDigit(const float fValue, const float fDigitIndex) {
    float res = fValue;
    for (int i = 0; i < fDigitIndex; i++) {
        res = res / 10;
    }
    for (int i = 0; i > fDigitIndex; i--) {
        res = res * 10;
    }
    return trunc(res % 10);
}

float PrintValue(float2 vStringCoords, float fValue, float fMaxDigits, float fDecimalPlaces)
{
    if ((vStringCoords.y < 0.0) || (vStringCoords.y >= 1.0))
        return 0.0;

    bool bNeg = (fValue < 0.0);
    bool bNan = isnan_NonOptimizableAway(fValue);
    bool bInf = isinf_NonOptimizableAway(fValue);
    if(bInf) fValue = 123.0;
    else if(bNan) fValue = 242.0;
    fValue = abs(fValue);

    float fLog10Value = log2(fValue) / log2(10.0);
    float fBiggestIndex = max(floor(fLog10Value), 0.0);
    float fDigitIndex = fMaxDigits - floor(vStringCoords.x);
    if (bInf || bNan) fDigitIndex += 2.0f; // Offset so Inf and nan are centralized
    float fCharBin = 0.0;
    if (fDigitIndex > (-fDecimalPlaces - 1.01))
    {
        if(fDigitIndex > fBiggestIndex)
        {
            if(fDigitIndex < (fBiggestIndex+1.5)) {
                if (bNeg) fCharBin = 1792.0; // Minus sign
                else if(bInf) fCharBin = 10016.0; // Plus sign
            }
        }
        else
        {
            if(fDigitIndex == -1.0)
            {
                if(fDecimalPlaces > 0.0 && !(bInf || bNan)) fCharBin = 2.0;
            }
            else
            {
                float fReducedRangeValue = fValue;
                if(fDigitIndex < 0.0) { fReducedRangeValue = frac( fValue ); fDigitIndex += 1.0; }
                //float fDigitValue = (abs(fReducedRangeValue / (pow(10.0, fDigitIndex)))); // Without workaround
                float fDigitValue = GetDigit(abs(fReducedRangeValue), fDigitIndex); // Workaround for precision issues found on more recent versions of Unity
                int arg = int(floor(fmod(fDigitValue, 10.0)));
                fCharBin = (bNan || bInf) ? DigitLet(arg) : DigitBin(arg);
            }
        }
    }
    return floor(fmod((fCharBin / pow(2.0, floor(frac(vStringCoords.x) * 4.0) + (floor(vStringCoords.y * 5.0) * 4.0))), 2.0));
}

float PrintValue(const in float2 fragCoord, const in float2 vPixelCoords, const in float2 vFontSize, const in float fValue, const in float fMaxDigits, const in float fDecimalPlaces)
{
    float2 vStringCharCoords = (fragCoord.xy - vPixelCoords) / vFontSize;
    return PrintValue( vStringCharCoords, fValue, fMaxDigits, fDecimalPlaces );
}

void DoDebug_float(float val, float2 uv, int decimalDigits, out float4 res)
{
    res = float4(0.3,0.2,0.1,1);
    res = PrintValue(uv*200, float2(10,100), float2(8,15), val, 10, decimalDigits);
}
```

#### [刚体碰撞Tilemap]

```cs
using UnityEngine.Tilemaps;
```

```cs
private void OnCollisionEnter2D(Collision2D coll){
    float Force = coll.relativeVelocity.magnitude;
    ContactPoint2D[] contacts = coll.contacts;
    Tilemap TheTilemap = coll.gameObject.GetComponent<Tilemap>();
    foreach(ContactPoint2D contact in contacts){
        Vector3Int Center = Vector3Int.RoundToInt(new Vector3(contact.point.x, contact.point.y, 0));
        if(TheTilemap != null){
            TheTilemap.SetTile(Center, null);
        }
    }
}
```



<div style="width: 100%; background-color: cornflowerblue; height: 5px;border: 1px blue groove;border-radius: 5px;"></div>

[TOC]

<hr>


