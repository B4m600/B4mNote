

# java.io.File

```java
public class PracE {
    public static  void main(String[] args) {
        File f1=new File("d:\\code");
        listFiles(f1);
    }
    private static void listFiles(File f1) {
        File[] list=f1.listFiles();
        for(File i:list){
            if(i.isDirectory()){
                listFiles(i);
            }
            else if(i.getName().endsWith(".java")){
                System.out.println(i.getAbsolutePath());
            }
        }
    }
}
```

- new File():

  ```java
  //构造器1
          File file1 = new File("hello.txt");//相对于当前module
          File file2 =  new File("D:\\workspace_idea1\\JavaSenior\\day08\\he.txt");
  
          System.out.println(file1);
          System.out.println(file2);
  
          //构造器2：
          File file3 = new File("D:\\workspace_idea1","JavaSenior");
          System.out.println(file3);
  
          //构造器3：
          File file4 = new File(file3,"hi.txt");
          System.out.println(file4);
      }
  
  ```

- String getAbsolutePath():

  - 绝对路径;

- String getPath():

  - 路径;

- String getName()

- String getParent()

- long length():

  - 文件字节数;

- long lastModified():

  - 最后一次修改时间;
  - 毫秒值;

- String[] list():

  - 指定目录下所有文件或者文件目录的字符串数组;
  - `String[] list = file.list();for(String str:list){}`

- File[] listFiles():

  - 指定目录下的所有文件或者文件目录的File对象数组; 
  - `File[] files = file.listFiles();for(File i:Files){}`

- boolean renameTo(File dest):

  - 重命名至指定路径;
  - `boolean renameTo = file2.renameTo(file1);`

- boolean isDirectory();

- boolean isFile();

- boolean exists();

- boolean canRead();

- public boolean canWrite();

- boolean isHidden();

- boolean createNewFile();

  - `if(!file.exists()){file.createNewFile();}else file.delete();`

- boolean mkdir();

  - 创建文件目录。如果此文件目录存在，就不创建了。如果此文件目录的上层目录不存在，也不创建。

- boolean mkdirs();

  - 创建文件目录。如果上层文件目录不存在，一并创建;

- boolean delete();

# java.io.FileInputStream

- int read():
  - 从输入流中读取一个数据字节;
  - 返回-1则已经到达文件末尾;
- int read(byte[] data):
  - 从输入流中将最多data.length个字节的数据读入一个byte数组中;
- int read(byte[] data, int off, int len);
- void close():
  - 关闭此文件输入流并释放与此流有关的所有系统资源;

```java
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.File;
public class PracD {
    public static void main(String[] args) throws IOException {
        File file = new File("test.txt");if(!file.exists()){ file.createNewFile();}
        try {
            FileInputStream FIS = new FileInputStream("test.txt");
            int n = FIS.read();
            System.out.println((char)n); // 仅读取第一个字符;
            while(n!=-1) { // 读取全部内容; 方法 1;
                System.out.print((char)n);
                n=FIS.read();
            }
            while((n=FIS.read())!=-1) { System.out.print((char)n);} // 方法 2;
            byte[] data = new byte[100]; // 方法 3;
            if (FIS.read(data) != -1){ System.out.println(new String(data)); };

            FIS.close();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

```

# java.util.Scanner

- new  Scanner():

  - `Scanner sc = new Scanner(System.in);`

- int nextInt():

  - `int num = sc.nextInt();`

- double nextDouble();

- float nextFloat();

- String next():

  - `String s = sc.next();`
  - 只能获取空格之前的数据;

  ```java
  import java.util.Scanner;
  public class Main {
  	public static void main(String[] args) {
      Scanner  sc=new Scanner(System.in);
      String s=sc.next();
      System.out.println(s);
  	}
  }
  ```

- useDelimiter("\n"):

  - 修改输入数据的分隔符;

  ```java
  import java.util.Scanner;
  public class Main {
  	public static void main(String[] args) {
      Scanner  sc=new Scanner(System.in);//从键盘接收数据//
      sc.useDelimiter("\n"); //修改输入数据的分隔符//
      String s=sc.next();
      System.out.println(s);
  }
  ```

- boolean hasNextInt();

  - 判断输入的是否为整数;

- boolean hasNextFloat();

# java.util.ArrayList

```java
import java.util.ArrayList;
public class PracF {
    public static  void main(String[] args) {
        Student s1=new Student("张军",21,"男");
        Student s2=new Student("李虎",23,"男");
        Student s3=new Student("马鸣",22,"男");
        ArrayList List=new ArrayList();
        List.add(s1);
        List.add(s2);
        List.add(s3);
        for(Object i:List){
            System.out.println(i);
        }
    }
}
class Student {
    private String sex;
    private int age;
    private String name;
    public Student(String name,int age,String sex){
        this.name=name;
        this.age=age;
        this.sex=sex;
    }
    @Override
    public String toString() {
        return "sex='" + sex +
                ", age=" + age +
                ", name='" + name;
    }
}
```

- new ArrayList();
- boolean  remove(Object obj);
- E remove(int index):
  - 删除指定索引处的元素，返回被删除的元素;
- E set(int index, E element);
- E get(int index);
- int size();
- boolean add(E element);
- void add(int index, E element):
  - 在此集合中的指定位置插入指定的元素;

# java.lang.String

- new String();
- new String(String value);
- new String(char[] value);
- new String(byte[] value);
- int length();
- int  indexOf(int ch):
  - 返回指定字符ch在当前字符串中第一次出现的位置;
  - `int index = str.indexOf('1');`
- int lastIndexOf(int ch);
- int indexOf(String str);
- int lastIndexOf(String str);
- char charAt(int index);
- boolean endsWith(String suffix);
- boolean startsWith(String prefix);
- boolean equals(Object obj);
- boolean equalsIgnoreCase(String str):
  - 以忽略大小写的方式比较;
- int compareTo(String str):
  - 按照对应字符的Unicode编码比较str与当前字符串的大小；
  - 若当前字符串比str大，返回正整数；
  - 若当前字符串比str小，返回负整数；
  - 两者相等时返回0；
- int compareaToIgnoreCase(String str);
- boolean isEmpty();
- contains(CharSequence cs);
- String toLowerCase();
- String toUpperCase();
- static String valueOf(int i):
  - 将int变量i转换为字符串;
- char[] toCharArray();
- String replace(CharSequence oldstr, CharSequence newstr);
- String concat(String str):
  - 将指定的字符串str连接到当前字符串的末尾；
- String[] split(String regex);
- String substring(int beginIndex):
  - 从参数索引到末尾返回一个新字符串；
- String substring(int beginIndex, int endIndex);
- String trim():
  - 去掉首尾的空格；