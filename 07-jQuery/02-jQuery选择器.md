## 一、jQuery获取和操作元素属性

DOM中有很多方式获取元素，比如通过id，通过标签名，通过类名，通过name的值，通过选择器等方式。

**在 jQuery 中就只有一种方式：`$("选择器")`**

### 1、基本选择器

#### 1.1、id 选择器

**语法：** ` $("#id选择器的值")`

```js
$(function () {// 页面加载
  $("#btn").click(function () {
    console.log($(this).val());
    $(this).val("改变按钮");
    // this.value = "改变按钮";
  });
});
```

>   注意：this 是DOM对象。
>
>   this.value = "改变按钮"; // 是DOM的写法，没问题。
>
>   **PS：jQuery 中使用 `jQuery对象.val("内容")` 来设置表单标签的 value 属性。**





#### 1.2、标签选择器

**语法：** `$("标签名")`

```js
$(function () {// 页面加载
  $("#btn").click(function () {
    $("p").text("桃花依旧笑春风");
  });
});
```

>   **1、jQuery 中的 `.text()` ，如果括号中没有值的话，是获取文本内容；如果有值的话，就是设置文本内容。**
>
>   2、 $("p") 是获取所有的 p 标签，然后全部设置文本内容，我们并没有循环设置，但是全部的 p 标签的文本内容都改变了，这是 jQuery 内部自动循环了，这就是隐式迭代。



#### 1.3、类选择器

**语法：**`$(".类型选择器")`  ，注意前面的点。

```js
$(function () { // 页面加载
  $("#btn").click(function () {
    $(".cls").css("border", "1px solid red");
  });
});
```

>   点击按钮设置应用了 cls 类选择器的标签的边框样式。
>
>   **PS：jQuery中使用 `jQuery对象.css("属性":"值");`  的方式设置标签的样式。** 

#### 1.4、并集选择器

**语法：**`$("div,p,span")`，中间使用逗号隔开。

>   如果上面的 div 有 id 选择器 dv；span 有类选择器 cls；
>
>   上面的写法也可以这样写： `$("#dv, p, .cls")`

#### 1.5、交集选择器

**语法：**`$("div.cls")`

>   标签名 + 类样式的方式。
>
>   // 选择所有div标签中class属性名为.cls的所有div元素。



**小总结：jQuery中的一些方法**

```js
val(); // 获取或设置表单标签中的 value 值。
css(); // 设置元素的 css 样式属性值。
text(); // 获取或设置标签的文本内容----相当于DOM中的innerText
html(); // 获取或设置标签的html内容----相当于DOM中的innerHTML
```



#### 1.6、后代（层次）选择器

**语法：**`$("div ul span")`

>   选择 div 下面所有 ul 下的所有的 span 标签，不包括 div 下面的 span，必须在 ul 里面。



#### 1.7、子代选择器

**语法：**`$("div>span")`

>选择 div 的直接下一代的所有span，不能隔代。

#### 1.8、兄弟选择器

**语法：**`$("div~span")`

>   选择的是 div **后面**的所有兄弟标签为 span 的标签。

#### 1.9、直接兄弟选择器

**语法：**`$("div+span")`

>   选择的是div **后面**的直接兄弟标签，如果这个直接兄弟为 span 标签则选中，如果为其他标签则不选中。



**案例：隔行变色**

```html
// body 主要内容
<input type="button" value="按钮" id="btn">
<div>
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
        <li>6</li>
        <li>7</li>
        <li>8</li>
    </ul>
</div>

// jQuery 代码
$(function () {
  $("#btn").click(function () {
    $("div li:odd").css("backgroundColor", "red");
    $("div li:even").css("backgroundColor", "yellow");
  });
});
```

>   `:odd` 选择第奇数个 li 标签。
>
>   `：even` 选择第偶数个 li 标签。



**案例：下拉菜单**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        * {
            margin: 0 ;
            padding: 0;
        }
        li{
            list-style-type: none;
        }
        a {
            text-decoration: none;
        }
        #dv>ul>li {
            float: left;
            margin: 0 10px;
            width: 50px;
            height: 20px;
            background-color: pink;
        }

        #dv>ul>li ul {
            display: none;
        }

        #dv>ul>li li {
            background-color: #ff486b;
        }

    </style>

    <script src="jquery-1.12.4.js"></script>
    <script>
        $(function () {
            // 鼠标进入
            $("#dv>ul>li").mouseenter(function () {
                $(this).children("ul").stop().show(200);
            });
            // 鼠标离开
            $("#dv>ul>li").mouseleave(function () {
                $(this).children("ul").stop().hide(200);
            });
        });
    </script>

</head>
<body>

<!--<input type="button" value="按钮" id="btn">-->
<div id="dv">
    <ul>
        <li>
            <a href="javascript:void(0);">周杰伦</a>
            <ul>
                <li>1</li>
                <li>2</li>
                <li>3</li>
            </ul>
        </li>
        <li>
            <a href="javascript:void(0);">林俊杰</a>
            <ul>
                <li>1</li>
                <li>2</li>
                <li>3</li>
            </ul>
        </li>
        <li>
            <a href="javascript:void(0);">陈奕迅</a>
            <ul>
                <li>1</li>
                <li>2</li>
                <li>3</li>
            </ul>
        </li>
    </ul>
</div>

</body>
</html>
```

>   1、jQuery中鼠标进入事件是：`mouseenter`；鼠标离开事件是：`mouseleave`
>
>   2、css 中的 `display:none|block` 对应的隐藏和显示在 jQuery 中可以使用方法：`show()` 和  `hide()`;
>
>   3、show 和 hide 方法中可以添加参数，数字表示毫秒。表示的显示和隐藏的动画效果。
>
>   4、stop 方法表示在显示和隐藏之前先清除之前的动画效果，防止鼠标操作过快，动画的显示跟不上操作。



### 2、属性选择器

| 示例                     | 描述                                                         |
| ------------------------ | :----------------------------------------------------------- |
| `$("[class]")`           | 获取所有属性名为class的元素                                  |
| `$("div[class]")`        | 获取所有div中有class属性的元素                               |
| `$("div[class=dv]")`     | 获取所有div中有`class="dv"`属性的元素                        |
| `$("div[class^=d]")`     | 获取所有div中有class属性的值是以d开头的元素                  |
| `$("div[class$=dv]")`    | 获取所有div中有class属性的值是以d结尾的元素                  |
| `$("div[class|=dv]")`    | 获取所有div中有class=dv的元素或者class属性值是以`dv-`开头的元素 |
| `$("div[class!=dv]")`    | 获取所有div中有class!=dv的元素                               |
| `$("div[class~=dv]")`    | 获取所有div中有class=dv的元素，要求dv是以空格分割的属性值列表中的一个属性。类似`class='cls dv'` |
| `$("div[class*=dv]")`    | 获取所有div中有class的属性值表示的字符串中包含dv的元素       |
| `$("div[id][class=dv]")` | 获取所有div中同时满足具有id属性并且class=dv的元素            |











### 3、过滤选择器

这类选择器都带有冒号。

| 名称                         | 示例                                        | 描述                                   |
| ---------------------------- | ------------------------------------------- | -------------------------------------- |
| `:first`                     | `$("li:first") == $("li").first()`          | 选取所有li中第一个元素                 |
| `:last`                      | `$("li:last") == $("li").last()`            | 选取所有li中最后一个元素               |
| `:not(选择器)`               | `$("li:not(.a)") == $("li").not(.a)`        | 选取所有li中没有class=‘.a’的元素       |
| `:odd`                       | `$("li:odd")`                               | 选取所有li中索引为奇数的元素           |
| `:even`                      | `$("li:even")`                              | 选取所有li中索引为偶数的元素           |
| `:eq(index)`                 | `$("li:eq(1)")==$("li").eq(1)`              | 选取所有li中索引为1的元素              |
| `:gt(index)`                 | `$("li:gt(1)")==$("li").gt(1)`              | 选取所有li中索引大于1的元素            |
| `lt(index)`                  | `$("li:lt(1)")==$("li").lt(1)`              | 选取所有li中索引小于1的元素            |
| -----------------            | --------无节操的分界线🙃---------            | -------------------                    |
| `:header`                    | `$(":header")`                              | 获取所有h1-h6标签                      |
| `:animated`                  | `$(":animated")`                            | 获取所有正在运行动画的元素             |
| `:focus`                     | `$("input:focus")==$("input").focus()`      | 获取所有input中获取焦点的元素          |
| `:empty`                     | `$(":empty")`                               | 获取所有元素内部为空的元素             |
| `:has(选择器)`               | `$("div:has(.a)")`                          | 获取子元素中有class=.a的所有div元素    |
| `:parent`                    | `$("div:parent")`                           | 获取不为空的所有div元素（与empty相反） |
| `:hidden`                    | `$("div:hidden")`                           | 获取`display:none`的所有div元素        |
| `:visible`                   | `$("div:visible")`                          | 获取`visibility: visible`的所有div元素 |
| -----------------            | --------无节操的分界线🙃---------            | ------------------                     |
| `:first-child/first-of-type` | `$("li:first-child")/$("li:first-of-type")` | 所有li中第一个元素                     |
| `:last-child/last-of-type`   | `$("li:last-child")/$("li:last-of-type")`   | 所有li中最后一个元素                   |
| `:nth-child(index)`          | 略略略~                                     | 略略略~                                |
| `:nth-of-type(index)`        | 略略略`                                     | 略略略~                                |





**案例：淘宝精品展示**

效果：鼠标进入标签，标签的背景颜色改变，并且切换到对应的图片显示。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        li {
            list-style-type: none;
        }

        #dv {
            margin-left: 500px;
            margin-top: 200px;
        }
        .ul1 li, .ul3 li {
            width: 50px;
            height: 30px;
            /*background-color: #24bcff;*/
            border: 1px solid red;
            text-align: center;
            margin-top: -1px;
        }

        a {
            text-decoration: none;
        }
        ul {
            float: left;
        }

        img {
            width: 200px;
            height: 93px;
        }
        .ul2 {
            width: 200px;
            height: 93px;
            overflow: hidden;
        }
        .ul2 li {
            float: left;
        }
    </style>
</head>
<body>

<div id="dv">
    <ul class="ul1">
        <li><a href="javascript:void(0);">img1</a></li>
        <li><a href="javascript:void(0);">img2</a></li>
        <li><a href="javascript:void(0);">img3</a></li>
    </ul>
    <ul class="ul2">
        <li><img src="images/img1.jpg"></li>
        <li><img src="images/img2.jpg"></li>
        <li><img src="images/img3.jpg"></li>
    </ul>
</div>


<script src="common.js"></script>
<script src="jquery-1.12.4.min.js"></script>
<script>

    $(function () {

        // 左li 鼠标进入
        $(".ul1>li").mouseenter(function () {
            $(this).css("backgroundColor", "purple");
            // console.log($(this).index());

            // 隐藏所有的图片
            $(".ul2>li").hide();
            // 显示丢应的图片
            $(".ul2>li:eq("+ $(this).index() +")").show();
        });

        // 左li 鼠标离开
        $(".ul1>li").mouseleave(function () {
            $(this).css("backgroundColor", "");
        });
    });
    
</script>
</body>
</html>
```

>   1、`$(this).index()` 可以获取当前 li 的索引。
>
>   2、` :eq()`  选择器：匹配一个给定索引值的元素。
>
>   3、`.hide()` 隐藏一个元素； `.show()` 显示一个元素。



### 4、筛选选择器

| 名称               | 用法                           | 描述                                               |
| :----------------- | ------------------------------ | -------------------------------------------------- |
| `children`         | `$("ul").children("li")`       | （子类选择器）相当于`$("ul>li")`                   |
| `find`             | `$("ul").find("li")`           | （后代选择器）相当于`$("ul li")`                   |
| `eq(index)`        | `$("li").eq(2)`                | 相当于 `$("li:eq(2)")`                             |
| `parent`           | `$("li").parent()`             | 查找父亲**（只有一个）**                           |
| `parents`          | `$("li").parents()`            | 查找所有父亲及以上长辈                             |
| `parentsUntil`     | `$("li").parentsUntil("body")` | 查找所有父亲及以上直到body的长辈                   |
| `next`             | `$("li").next("li")`           | 查找下一个兄弟节点                                 |
| `prev`             | `$("li").prev("li")`           | 查找上一个兄弟节点                                 |
| `nextAll`          | `$("li").nextAll("li")`        | 查找后面所有的兄弟节点                             |
| `prevAll`          | `$("li").prevAll("li")`        | 查找上面所有的兄弟节点                             |
| `nextUntil`        | `$(".li1").nextUntil(".li3")`  | 查找从当前节点到后面指定兄弟节点之间的所有兄弟节点 |
| `prevUntil`        | `$(".li1").prevUntil(".li3")`  | 查找从当前节点到之前指定兄弟节点之间的所有兄弟节点 |
| `siblings`         | `$("li").siblings("li")`       | 查找除自身之外的所有兄弟节点                       |
| `slice(start,end)` | `$("li").slice(1,3)`           | 查找index从1到3所有的li元素                        |

>注意：
>
>1、虽然 find/children 选择器相当于 后代/子代选择器。**但是 find/children 的效率比 后代选择器效率高得多。**
>
>2、当 next， prev 系列的方法，如果没写参数，则查找所有的兄弟节点；如果有参数，则查找所有兄弟节点中的指定元素。





