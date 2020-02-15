> ##### JQuery Selector是JQuery组件提供的根据条件定位页面元素的的功能


### 几种基础的定位方式

写在前面, 例子中的$()均是为了在JQuery中示意代码需要，并不属于Selector的一部分。

##### 使用"#" 通过元素id定位
例如html
```
    <div id="mark">
    </div>
```

该div可以通过 '#mark' 来获取到：
```js
    $("#mark").css("background", "yellow");
```

##### 使用"." 通过元素class定位
例如
```
    <div class="mark">
    </div>
```

该div可以通过'.mark' 来获取到
```js
    $(".mark").css("background", "yellow");
```
在面对多个class的元素时，可以通过顿号.间隔，添加多个例如：
```js
  $(".mark.selected.gray.touch")
```
但这样的多个class必须和元素中的class顺序个数保持一致，如果只是部分class的元素定位，将在后续的属性选择中讨论。

##### 使用Tag名字来定位 
例如定位span元素
```js
    $("p").css("background", "yellow");
```

##### 通过元素属性来定位
例如
```
    <input type="text">
    </input>
```
该input可以通过type属性来定位:
```js
    $('input[type="text"]').css("background", "yellow");
```


### 更多属性定位方式

在实际web中经常会面对复杂属性的元素，通过各种属性的关系表达来定位是很常见的情况，JQuery Selector提供了以下几种表达式：


##### 存在属性 [name]
[]加属性名称， 如果元素有该属性即成立
```
    <div>no id</div>
    <div id="hey">with id</div>
    <div id="there">has an id</div>
    <div>nope</div>
```
对于
```
    $( "div[id]" )
```
第2，3个div满足条件，存在id属性.

##### 包含属性 [name*=”value”]
*= 就是最简单的包含关系，属性值字符串中存在即成立
```
    <input name="man-news">
    <input name="milkman">
    <input name="letterman2">
    <input name="newmilk">
```
对于
```
    $( "input[name*='man']" )
```
其中前3个满足选中。

##### 包含完整属性 [name~=”value”]
~= 也是包含关系，但并不是字符串匹配的包含，而是目标值是该元素属性中独立的一项 (空格间隔)
```
    <input name="man-news">
    <input name="milk man">
    <input name="letterman2">
    <input name="newmilk">
```
对于
```
    $( "input[name~='man']" )
```
只有第2项满足

##### 后缀属性 [name$=”value”]

```
    <input name="newsletter">
    <input name="milkman">
    <input name="jobletter">
``` 
对于
```js
    $( "input[name$='letter']" )
```
第1和3项满足

##### 前缀属性 [name^=”value”]

```
    <input name="newsletter">
    <input name="milkman">
    <input name="jobletter">
``` 
对于
```js
    $( "input[name$='job']" )
```
第3项满足

##### 包含属性前缀 [name|=”value”]
|= 的意思是，该属性等于该值，或者以该值开头并连接 '-' 符号 （注意这和上一个前缀的区别）.  
```
    <a href="example.html" hreflang="en">Some text</a>
    <a href="example.html" hreflang="en-UK">Some other text</a>
    <a href="example.html" hreflang="english">will not be outlined</a>
    <a href="example.html" hreflang="zh-cn">中文</a>
```
对于:
```
    $( "a[hreflang|='en']" )
```
其选中的是第1和第2个a元素。 第3个en开头但没有'-'连接， 第四个没有en开头.


##### 不等于属性 [name!=”value”]
!= 表示目标元素或者没有该属性，或者有该属性但不等于指定值
```
    <div>
      <input type="radio" name="newsletter" value="Hot Fuzz">
      <span>name is newsletter</span>
    </div>
    <div>
      <input type="radio" value="Cold Fusion">
      <span>no name</span>
    </div>
    <div>
      <input type="radio" name="accept" value="Evil Plans">
      <span>name is accept</span>
    </div>
```
对于
```js
    $( "input[name!='newsletter']" )
```
第2，3个input满足条件


### 更多的扩展定位方式

JQuery Selector同时也提供了很多方便定位元素的小函数，这些函数不一定在每一种的爬虫工具中都支持，建议在编写使用前根据具体的爬虫工具确认。

##### 包含值 :contains() 
查找包含指定值的元素，例如:
```
    <div>John Resig</div>
    <div>George Martin</div>
    <div>Malcom John Sinclair</div>
    <div>J. Ohn</div>
```
对于
```
    $( "div:contains('John')" )
```
第1个和第3个div是满足条件的。

##### 元素位置选择 :eq() 
eq() 通过从0开始的数字队列排序目标元素，选择指定位置的元素。
```
    <table border="1">
      <tr><td>TD #0</td><td>TD #1</td><td>TD #2</td></tr>
      <tr><td>TD #3</td><td>TD #4</td><td>TD #5</td></tr>
    </table>
```
对于
```
    $( "td:eq( 2 )" )
```
第3个td标签(TD#2)是满足条件， 注意这里指数是从0开始


##### 第一个满足元素 :first() 
first() 会找到第一个满足条件的元素
```
    <table>
      <tr><td>Row 1</td></tr>
      <tr><td>Row 2</td></tr>
      <tr><td>Row 3</td></tr>
    </table>
```
对于 
```
    $( "tr:first" )
```
会找到第一个tr元素.


