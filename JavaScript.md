[TOC]



### [工具函数]

- encodeURIComponent

  - 把字符串作为 URI 组件进行编码。
  - 所有主要浏览器都支持 encodeURIComponent() 函数。

  ```js
  var uri="https://www.runoob.com/my test.php?name=ståle&car=saab";
  document.write(encodeURIComponent(uri));
  ```

  ```js
  https%3A%2F%2Fwww.runoob.com%2Fmy%20test.php%3Fname%3Dst%C3%A5le%26car%3Dsaab
  ```

- 