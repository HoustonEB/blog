---
title: Node
tags: Node
date: 2019-05-04 12:09:00
# cover: /img/ml02cover2.jpg
---
# 全局变量
{% label primary@__dirname %}
当前模块的目录名。 与 __filename 的 path.dirname() 相同。

示例，从 /Users/mjr 运行 node example.js：
```js
console.log(__dirname);
// 打印: /Users/mjr
console.log(path.dirname(__filename));
// 打印: /Users/mjr
```
{% label primary@__filename %}
当前模块的文件名。 这是当前的模块文件的绝对路径（符号链接会被解析）。
对于主程序，这不一定与命令行中使用的文件名相同。
示例：
```js
从 /Users/mjr 运行 node example.js：

console.log(__filename);
// 打印: /Users/mjr/example.js
console.log(__dirname);
// 打印: /Users/mjr
给定两个模块：a 和 b，其中 b 是 a 的依赖文件，且目录结构如下：

/Users/mjr/app/a.js
/Users/mjr/app/node_modules/b/b.js
b.js 中的 __filename 的引用会返回 /Users/mjr/app/node_modules/b/b.js，而 a.js 中的 __filename 的引用会返回 /Users/mjr/app/a.js。
```
# path模块
除了目录结构有区别外，路径也是有区别的。windows是用反斜杠\分割目录或者文件的，而在类Unix的系统中是用的/。
```
windows的路径： C:\temp\myfile.html
类Unix的路径：  /tmp/myfile.html
```
### path.basename(path, ext)
path
ext 文件扩展名(可选)
获取路径中的文件名
```js
path.basename('/foo/bar/baz/asdf/quux.html');
// 返回: 'quux.html'

path.basename('/foo/bar/baz/asdf/quux.html', '.html');
// 返回: 'quux'
```
### path.dirname(path)
获取路径的文件夹,不获取文件名
```js
path.dirname('/foo/bar/baz/asdf/quux');
// 返回: '/foo/bar/baz/asdf'
```
### path.extname(path)
获取路径的扩展名即从 path 的最后一部分中的最后一个 .（句号）字符到字符串结束。
如果 path 的最后一部分没有 . 或 path 的文件名的第一个字符是 .，则返回一个空字符串。
```js
path.extname('index.html');
// 返回: '.html'
path.extname('/etc/a/index.html');
// 返回: '.html'

path.extname('index.coffee.md');
// 返回: '.md'

path.extname('index.');
// 返回: '.'

path.extname('index');
// 返回: ''

path.extname('.index');
// 返回: ''
```
### path.format(object)
path.format() 方法会从一个对象返回一个路径字符串。

语法：path.format(pathObject)

pathObject <Object> 要转换成路径字符串的设置对象
dir <string> 所在目录，提供了 pathObject.dir，则 pathObject.root 会被忽略
root <string> 根目录
base <string> 文件全名。如果pathObject.base 存在，则 pathObject.ext 和 pathObject.name 会被忽略
name <string> 文件名字（不带后缀）
ext <string> 文件后缀
返回: <string> 返回完整路径字符串

```js
path.format({
  dir: '/home/user/dir',
  base: 'file.txt'
});
// 返回: '/home/user/dir/file.txt'

path.format({
  root: '/',
  name: 'file',
  ext: '.txt'
});
// 返回: '/file.txt'
```
### path.parse(path)
path.parse() 方法返回一个对象，对象的属性表示 path 的元素。
parse方法跟 format方法正好相反，所以不赘述。直接看例子：
```js
let pathObj = path.parse('/users/home/aicoder/a.html');
console.dir(pathObj);

// 输出如下
{ root: '/',
  dir: '/users/home/aicoder',
  base: 'a.html',
  ext: '.html',
  name: 'a' }
```
### path.join()
path.join() 方法使用平台特定的分隔符把全部给定的 path 片段连接到一起，并规范化生成的路径。
长度为零的 path 片段会被忽略。 如果连接后的路径字符串是一个长度为零的字符串，则返回 '.'，表示当前工作目录。

参数说明：
...paths <string> 一个路径片段的序列。
返回: <string>

```js
path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');
// 返回: '/foo/bar/baz/asdf'
path.join('/foot', __filename); // __filename是模块内的变量，代表当前js文件
// 返回：/foot/xxx.js    

// 以下路径拼接的方式不推荐：
var strPath = '/foot/' + 'xxx.js';  //虽然跟上面实现的方式一致，但是不推荐。
```
### path.resolve() 
方法将路径或路径片段的序列解析为绝对路径。
给定的路径序列从右到左进行处理，每个后续的 path 前置，直到构造出一个绝对路径。 例如，给定的路径片段序列：/foo、 /bar、 baz，调用 path.resolve('/foo', '/bar', 'baz') 将返回 /bar/baz。

{% note primary %}
如果在处理完所有给定的 path 片段之后还未生成绝对路径，则再加上当前工作目录。
{% endnote %}
生成的路径已规范化，并且除非将路径解析为根目录，否则将删除尾部斜杠。

零长度的 path 片段会被忽略。

如果没有传入 path 片段，则 path.resolve() 将返回当前工作目录的绝对路径。
```js
path.resolve('/foo/bar', './baz');
// 返回: '/foo/bar/baz'

path.resolve('/foo/bar', '/tmp/file/');
// 返回: '/tmp/file'

path.resolve('wwwroot', 'static_files/png/', '../gif/image.gif');
// 如果当前工作目录是 /home/myself/node，
// 则返回 '/home/myself/node/wwwroot/static_files/gif/image.gif'
```
### path.normalize()
方法会规范化给定的 path，并解析 '..' 和 '.' 片段。
当发现多个连续的路径分隔符时（如 POSIX 上的 / 与 Windows 上的 \ 或 /），它们会被单个的路径分隔符（POSIX 上是 /，Windows 上是 \）替换。 末尾的多个分隔符会被保留。
如果 path 是一个长度为零的字符串，则返回 '.'，表示当前工作目录。

语法： path.normalize(path)

path <string> 要进行规范的路径字符串
返回: <string> 规范后的路径字符串
```js
path.normalize('/foo/bar//baz/asdf/quux/..');
// 返回: '/foo/bar/baz/asdf

// windows 上
path.normalize('C:\\temp\\\\foo\\bar\\..\\');
// 返回: 'C:\\temp\\foo\\'
```
<!-- more -->