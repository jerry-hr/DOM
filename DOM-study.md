

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


#### 节点的关系

1. ![image-20210223104559148](../../AppData/Roaming/Typora/typora-user-images/image-20210223104559148.png)

   ![image-20210223104640836](../../AppData/Roaming/Typora/typora-user-images/image-20210223104640836.png)

**注意：**

- DOM中，文本节点也属于节点，在使用节点的关系时一定要注意
- 在标准的W3C规范中，空白文本节点也应该算做节点，但是在IE8及以前的浏览器中会有一定的兼容问题，他们不把空文本节点当做节点

![image-20210223105207857](../../AppData/Roaming/Typora/typora-user-images/image-20210223105207857.png)

```
HTML代码:
<div id="box">
	<p>我是段落</p>
	<p id="para">我是段落</p>
	<p>我是段落</p>
</div>
JS代码:
var box = document.getElementById('box');
para = document.getElementById('para');
//所有子节点
console.log(box.childNodes);
//所有元素子节点(IE9开始兼容)
console.log(box.chileren);

//第一个子节点
console.log(box.firstChild);
console.log(box.firstChild.nodeType);
//第一个元素子节点(IE9开始兼容)
console.log(box.firstElementChild);

//最后一个子节点
console.log(box.lastChild);
console.log(box.lastChild.nodeType);
//最后一个元素子节点(IE9开始兼容)
console.log(box.lastElementChild);

//父节点
console.log(para.parentNode);

//前一个兄弟节点
console.log(para.previousSibling);
//前一个元素兄弟节点(IE9开始兼容)
console.log(para.previousElementSibling);

//后一个兄弟节点
console.log(para.nextSibling);
//后一个元素兄弟节点(IE9开始兼容)
console.log(para.nextElementSibling);

```

#### 封装节点关系函数

1. 书写常见的节点关系函数

   1. 书写IE6也能兼容的“寻找所有元素子节点”函数

      ```
      HTML代码:
      <div id="box">
      	<p>我是段落</p>
      	<p id="para">我是段落</p>
      	<p>我是段落</p>
      </div>
      JS代码:
      var box = document.getElementById('box');
      var para = document.getElementById('para');
      //封装一个函数，这个函数可以返回元素的所有子元素节点(兼容到IE6)，类似children的功能
      function getChildren(node) {
      	//结果数组
      	var children = [];
      	//遍历node这个节点的所有子节点，判断每一个子节点的nodeType属性是不是1
      	//如果是1，就推入结果数组(1代表元素节点)
      	for(var i = 0; i < node.childNodes.length; i++) {
      		if(node.childNodes[i].nodeType == 1) {
      			children.push(node.childNodes[i]);
      		}
      	}
      	return children;
      }
      console.log(getChildren(box));
      console.log(getChildren(para));
      ```

      2.书写IE6也能兼容的“寻找前一个元素兄弟节点”函数

      ```
      HTML代码:
      <div id="box">
      	<p id="fpara">我是段落</p>
      	<p id="para">我是段落</p>
      	<p>我是段落</p>
      </div>
      JS代码:
      var box = document.getElementById('box');
      var para = document.getElementById('para');
      var fpara = document.getElementById('fpara');
      //封装一个函数，这个函数可以返回元素的前一个元素兄弟节点(兼容到IE6),类似previousElementSibling的功能
      function 
      
      getElementPrevSibling(node) {
      	var o = node;
      	//使用while语句
      	while(o.previousSibling != null) {
      		if(o.previousSibling.nodeType == 1) {
      			//结束循环，找到了
      			return o.previousSibling;
      		}
      		//让o成为它的前一个节点
      		o = o.previousSibling;
      	}
      	return null;
      }
      console.log(getElementPrevSibling(para));
      ```

      3.如何编写函数，获得某元素的所有元素兄弟节点

      ```
      HTML代码:
      <div id="box">
      	<p>我是段落</p>
      	<p>我是段落</p>
      	<p>我是段落</p>
      	<p id="fpara">我是段落</p>
      	<p id="para">我是段落</p>
      	<p>我是段落</p>
      </div>
      JS代码:
      var box = document.getElementById('box');
      var para = document.getElementById('para');
      //封装一个函数，这个函数可以返回元素的所有元素兄弟节点
      function getAllElementSibling(node) {
      	//前面的元素兄弟节点
      	var prevs = [];
      	//后面的元素兄弟节点
      	var nexts = [];
      	var o = node;
      	//遍历node的前面的节点
      	while(o.previousSibling != null) {
      	if(o.previousSibling.nodeType == 1) {
      		//从头部插入	
      		prevs.unshift(o.previousSibling);
      	}
      	//类似把前一个当做现在继续遍历
      	o = o.previousSibling;
      	}
      	o = node;
      	//遍历node的后面的节点
      	while(o.nextSibling != null) {
      	if(o.nextSibling.nodeType == 1) {
      nexts.push(o.nextSibling);
      	}
      	o = o.nextSibling;
      	
      }
      //将两个数组进行合并，然后返回
      return prevs.concat(nexts);
      }
      console.log(getAllElementSibling(para));
      ```

2. 如何改变元素节点中的内容

   1. 改变元素节点中的内容可以使用两个相关属性

      1. innerHTML属性能以HTML语法设置节点中的内容

         ```
         HTML代码:
         <div id="box"></div>
         JS代码:
         var oBox = document.getElementById('box');
         oBox.innerHTML = '慕课网';
         oBox.innerHTML = '<ul><li>牛奶</li><li>咖啡</li></ul>';
         ```

         ![image-20210224120006266](../../AppData/Roaming/Typora/typora-user-images/image-20210224120006266.png)![image-20210224120034169](../../AppData/Roaming/Typora/typora-user-images/image-20210224120034169.png)

      2. innerText属性只能以纯文本的形式设置节点中的内容

         ```
         HTML代码:
         <div id="box"></div>
         JS代码:
         var oBox = document.getElementById('box');
         oBox.innerText = '<ul><li>牛奶</li><li>咖啡</li></ul>';//会直接输出
         oBox.innerText = '慕课网';
         ```

         ![image-20210224120122354](../../AppData/Roaming/Typora/typora-user-images/image-20210224120122354.png)![image-20210224120144520](../../AppData/Roaming/Typora/typora-user-images/image-20210224120144520.png)

   