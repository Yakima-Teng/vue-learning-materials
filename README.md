# vue-learning-materials

本文先从以前那种使用script标签引入js然后用旧版js语法进行书写的传统方式讲VueJS的使用（这是关于vue的主要内容，但是这种开发方式会增加人工编码量，模块化也比较麻烦，不适合编写工程代码），然后再讲现在比较常见的开发方式（主要讲一些构建工具，其实不是关于vue的东西）。

VueJS跟jsp、jade、pug这些东西有个共同之处就是可以直接根据变量的值和模板里的html片段来填充内容生成最终的html文件。VueJS可以在服务端填充模板也可以在用户浏览器客户端填充模板内容，这里我们只讲在客户端填充内容的情况。

VueJS有中文版的官网，地址为[https://cn.vuejs.org/](https://cn.vuejs.org/)。

第一部分：先说Vue的基本用法（参考[vue-demo.html](./vue-demo.html)文件）：

1. 先在html里通过script标签引入vue.js文件；

2. 通过new Vue(配置参数)的方式构造vue实例接管html中指定节点下的内容；

3. 关键词：数据、计算属性、方法、生命周期（时间钩子）。

第二部分：构建工具

好处举例：

1. 减少手写代码量
以前你可能需要这样写css样式：
```css
.article {
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
}
```

现在你可以这么写（less），添加厂商前缀之类的活构建工具会帮你做好的。
```less
.article {
  user-select: none;
}
```

想再投篮点的话，如果你用sass，花括号和分号也是可以省略的：
```sass
.article
    user-selct: none
```

上面说的是css，关于html，以前你需要这么写：
```html
<header class="header">
    <h1 class="title">Title</h1>
</header>
<article class="article">
    <p class="paragraph">This is a single paragraph with meaningless letters.</p>
</article>
```
现在你可以这么写（用pug）：
```pug
.header
    .title Title
.article
    .paragraph This is a single paragraph with meaningless letters.
```

2. 简化一些常用操作
以前，发布前端静态文件可能需要先在电脑里装一个ftp/sftp软件，打开后选择本地文件再上传文件；
以前，可能需要用一些本地工具或者在线工具来压缩图片文件、css文件和js文件；
以前，本地开发时修改了代码后，需要手动刷新浏览器查看修改后的效果；
......
现在不需要这么干了。

3. 可以使用比较新的JS语法
新语法除了可以减少一些代码的书写量，还有个很大的好处是让你可以模块化地书写代码，不需要在单个文件里书写把所有js都写到一起，维护的时候会方便很多，通过Promise、asnyc/await等新特性，可以在形式上避免回调地狱的出现，下面是一些例子：

减少书写量的例子：
```es6
// 将一个数组里的偶数取出并对每个偶数都增加1来生成一个新数组，以前的写法：
var arr = [1, 2, 3, 4];
var newArr = [];
for (var i = 0, len = arr.length; i < len; i++) {
  var item = arr[i];
  if (item % 2 === 0) {
    newArr.push(item);
  }
}
console.log(newArr);

// 现在可以这么写：
var arr = [1, 2, 3, 4];
var newArr = arr.filter(item => item % 2 === 0).map(item => item + 1);
console.log(newArr);
```

模块化的例子：
文件math.js
```javascript 1.8
export const divide = (a, b) => a / b
export const multiply = (a, b) => a + b
```

文件b.js
```javascript 1.8
import { divide, multiply } from './math'
const a = 15
const b = 3
const c = divide(a, b)
const d = multiply(a, b)
console.log(c, d)
```

Promise和await/async的例子：
```javascript 1.8
// 用回调函数的形式去写：
a(function () {
  b(function () {
    c(function () {
      d(function () {
        /...
      })
    })
  })
})

// 用Promise的方式去写：
a.then(b).then(c).then(d);
```

Promise和await/async的例子：
```javascript 1.8
// 用回调函数的形式去写：
compressImage(fileBlob, function (minifiedImageBase64Data) {
  document.querySelector('#img').src = minifiedImageBase64Data
})

// 用await/async的方式去写：
const minifiedImageBase64Data = await compressImage(fileBlob)
document.querySelector('#img').src = minifiedImageBase64Data
```
