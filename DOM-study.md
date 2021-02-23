#### **DOM的基本概念**

（DOM是JS操控HTML和CSS的桥梁  ）

DOM(Document Object Model,文档对象模型)是JavaScript操作HTML文档的接口，使文档操作变得非常优雅、简便。

最大的特点：将文档表示为节点树。

![image-20210220110122770](C:\Users\11869\AppData\Roaming\Typora\typora-user-images\image-20210220110122770.png)

#### 节点操作

1. nodeType常用属性值

   1. ![image-20210220190940317](C:\Users\11869\AppData\Roaming\Typora\typora-user-images\image-20210220190940317.png)

2. 访问元素节点==指“得到”、“获取”页面上的元素节点

   1. 访问元素节点主要依靠document对象

      1. document(文档): document对象是DOM中最重要的东西，几乎所有DOM的功能都封装在了document对象中
      2. document对象也表示整个HTML文档，它是DOM节点树的根
      3. document对象的nodeType属性值是9

   2. 访问元素节点的常用方法

      ![image-20210220210725836](C:\Users\11869\AppData\Roaming\Typora\typora-user-images\image-20210220210725836.png)

      1. getElementById()

         ```
         document.getElementById()//功能是通过id得到元素节点
         HTML代码:
         <div id="box">我是一个盒子</div>
         <p id="para">我是一个段落</p>
         JS代码:
         var box = document.getElementById('box');
         //参数就是元素节点的id，注意不要写#号,id要对应
         var para = document.getElementById('para');
         注意事项:
         1.如果页面上有相同id的元素，则只能得到一个
         2.不管元素藏的位置有多深，都能通过id吧它找到
         ```

         延迟运行：

         1. ​	在测试DOM代码时，通常JS代码一定要写到HTML节点的后面，否则JS无法找到相应HTML节点

         2. 可以使用window.onload = function(){}事件，使页面加载完毕之后，再执行指定代码（这是js写在html前面的时候的写法）,script标签对写在head里

            ![image-20210220214044340](../AppData/Roaming/Typora/typora-user-images/image-20210220214044340.png)

      2. getElementsByTagName()

         ```
         getElementsByTagName()方法的功能是通过标签名得到节点数组
         HTML代码:
         <p>我是段落</p>
         <p>我是段落</p>
         <p>我是段落</p>
         <p>我是段落</p>
         JS代码:
         var ps = document.getElementsByTagName('p');
         ps暗示是数组，不是一个普通的变量
         注意事项:
         1.数组方便遍历，从而可以批量操控元素节点(控制所有p标签，如果想操控指定p标签，要先调父元素)
         2.即使页面上只有一个指定标签名的节点，也将得到长度为1的数组
         3.任何一个节点元素也可以调用getElementsByTagName()方法，从而得到其内部的某种类的元素节点
         ```

      3. getElementsByClassName()

         ```
         getElementsByClassName()方法的功能是通过类名得到节点数组
         HTML代码:
         <div class="spec">我是盒子</div>
         <div>我是盒子</div>
         <div class="spec">我是盒子</div>
         <div class="spec">我是盒子</div>
         JS代码:
         var spec_divs = document.getElementsByClassName('spec');
         注意事项:
         1.getElementsByClassName()方法从IE9开始兼容
         2.某个节点元素也可以调用getElementsByClassName()方法，从而得到其内部的某类名的元素节点
         ```

      4. querySelector()

         ```
         querySelector()方法的功能是通过选择器得到元素
         HTML代码:
         <div id="box1">
         	<p>我是段落</p>
         	<p class="spec">我是段落</p>
         	<p>我是段落</P>
         </div>
         JS代码:
         var the_p = document.querySelector('#box1 .spec'); //正常写html代码，选择器
         注意事项:
         1.querySelector()方法只能得到页面上的一个元素，如果有多个元素符合条件，则只能得到第一个元素
         2.querySelector()方法从IE8开始兼容，但从IE9开始支持CSS3的选择器，如: nth-child()、:[src^='dog']等css3选择器形式都支持良好
         ```

      5. querySelectorAll()

         ```
         querySelectorAll()方法的功能是通过选择器得到元素数组
         
         即使页面上自由一个符合选择器的节点，也将得到长度为1的数组
         HTML代码:
         <ul id="list1">
         	<li>我是li</li>
         	<li>我是li</li>
         	<li>我是li</li>
         	<li>我是li</li>
         </ul>
         <ul id="list2">
         	<li>我是li</li>
         	<li>我是li</li>
         	<li>我是li</li>
         	<li>我是li</li>
         </ul>
         JS代码:
         var lis_inlist1 = document.querySelectorAll('#list li');
         console.log(lis_inlist1);
         ```

         