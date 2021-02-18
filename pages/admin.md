# 如何维护管理员列表

下面这行文本是最新的管理员列表（与Github Repository同步更新）。

<pre><code id="list" class="language-json line-numbers"></code></pre>

### 何为JSON？
>JSON (JavaScript Object Notation) is a lightweight data-interchange format. It is easy for humans to read and write. It is easy for machines to parse and generate. It is based on a subset of the JavaScript Programming Language Standard ECMA-262 3rd Edition - December 1999. JSON is a text format that is completely language independent but uses conventions that are familiar to programmers of the C-family of languages, including C, C++, C#, Java, JavaScript, Perl, Python, and many others. These properties make JSON an ideal data-interchange language. -摘自json.org

### 我们是如何实现的？

上文的文本是一个json文本。它由`键`与`值`组成。下面是是一个简单的json例子：
<pre><code class="language-json line-numbers">{
    "Key": "Value"
}
</code></pre>
你可以观察到，任何json文本都有一对花括号围起来，我们称一个这样的文本为`JSON对象`。很显然，花括号里面的内容是JSON的值，我们称这些内容为`JSON内容`。  
那么`JSON内容`的值自然是`键`和`值`了，我们称一组包含`键`与`值`的文本为`键对`。  
先从键讲起。键**只能**是`字符串`，而值有多种，分为如下几种：

+ 基本数据类型
    - String
    - Boolean
    - Int(Number)
+ 数组(Array)
+ 对象(Object)

那么再回到代码部分，/admin_inf.json是管理员的详细信息，在index.html中，解析部分是这样实现的：

<pre><code class="language-javascript line-numbers">$.get('https://cdn.jsdelivr.net/gh/zhihu-mclub/rules-and-reports@gh-pages/admin_inf.json',function (result) {
    var obj=result;
    var str;
    for(var i in obj){
        str=document.getElementById('inf_list').innerHTML+'<tr><td class="mdui-ripple">'+i+'</td><td class="mdui-ripple">'+obj[i].qq+'</td><td class="mdui-ripple">'+obj[i].email+'</td><td class="mdui-ripple">'+obj[i].main_page+'</td></tr>';
        document.getElementById('inf_list').innerHTML=str;
    }
});
</code></pre>
首先看第一行代码，调用jQuery的AJAX GET方法获取admin_inf.json的内容(为提高静态资源访问速度已经把链接换成jsDelivr的gh repo镜像链接)。接下来开始遍历获取到的json对象(jQuery AJAX GET方法会自动将string转换为json对象)，接下来获取每个键的值，然后转换为HTML格式代码再插入文档完成渲染。

### 如何增删<span class="del">查</span>改管理信息？
场景一：圈子第四次管理员选拨，增加了一位新管理员，但是ta还没被加入到github的页面里。  
场景二：圈子里一位管理员违反了圈规，需要删除ta的管理员身份。  
场景三：圈子里一位管理员的Email密码忘记了，决定换一个邮箱，但ta的github的页面上还没改回来。  
对于场景一，这很简单，只需要在json文本的末尾增加一句：
<pre><code class="language-json line-numbers">,{
"233333333": {
    "qq": "233333333",
    "email": "233333333@233.com",
    "main_page": "https://zhihu.com/people/233333333"
}
</code></pre>
对于场景二，这也很简单，只需要把原有的json键对删除即可，例如我们要删除233333334，只需要把原文本：
<pre><code class="language-json line-numbers">{
    "233333333":{
        "qq": "233333333",
        "email": "233333333@233.com",
        "main_page": "https://zhihu.com/people/233333333"
    },
    "233333334":{
        "qq": "233333333",
        "email": "233333333@233.com",
        "main_page": "https://zhihu.com/people/233333333"
    }
}
</code></pre>
改为：
<pre><code class="language-json line-numbers">{
    "233333333":{
        "qq": "233333333",
        "email": "233333333@233.com",
        "main_page": "https://zhihu.com/people/233333333"
    }
}
</code></pre>

对于场景三，这同样非常简单，只需要替换原有的键对，例如我们要把233333333的email换成233333333@java.com：
<pre><code class="language-json line-numbers">{
    "233333333":{
        "qq": "233333333",
        "email": "233333333@java.com",
        "main_page": "https://zhihu.com/people/233333333"
    }
}
</code></pre>