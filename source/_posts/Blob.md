---
title: Blob
date: 2020-07-08 10:41:12
categories: Js
tags:
 - Blob
---
## Blob对象
Blob, Binary Large Object的缩写.代表二进制类型的大对象.
在Web中，Blob类型的对象表示不可变的类似文件对象的原始数据，通俗点说，就是Blob对象是二进制数据，但它是类似文件对象的二进制数据，因此可以像操作File对象一样操作Blob对象，实际上，File继承自Blob。
`Blob(blobParts[, options])`
参数说明：
blobParts：数组类型，数组中的每一项连接起来构成Blob对象的数据，数组中的每项元素可以是ArrayBuffer, ArrayBufferView, Blob, DOMString 。
options：可选项，字典格式类型，可以指定如下两个属性：
- type，默认值为 ""，它代表了将会被放入到blob中的数组内容的MIME类型。
- endings，默认值为"transparent"，用于指定包含行结束符\n的字符串如何被写入。 它是以下两个值中的一个： "native"，表示行结束符会被更改为适合宿主操作系统文件系统的换行符； "transparent"，表示会保持blob中保存的结束符不变。
<!-- more -->
```js
var data1 = "a";
    var data2 = "b";
    var data3 = "<div style='color:red;'>This is a blob</div>";
    var data4 = { "name": "abc" };

    var blob1 = new Blob([data1]);
    var blob2 = new Blob([data1, data2]);
    var blob3 = new Blob([data3]);
    var blob4 = new Blob([JSON.stringify(data4)]);
    var blob5 = new Blob([data4]);
    var blob6 = new Blob([data3, data4]);

    console.log(blob1);  //输出：Blob {size: 1, type: ""}
    console.log(blob2);  //输出：Blob {size: 2, type: ""}
    console.log(blob3);  //输出：Blob {size: 44, type: ""}
    console.log(blob4);  //输出：Blob {size: 14, type: ""}
    console.log(blob5);  //输出：Blob {size: 15, type: ""}
    console.log(blob6);  //输出：Blob {size: 59, type: ""}
```
size代表Blob 对象中所包含数据的字节数。这里要注意，使用字符串和普通对象创建Blob时的不同，blob4使用通过JSON.stringify把data4对象转换成json字符串，blob5则直接使用data4创建，两个对象的size分别为14和15。blob4的size等于14很容易理解，因为JSON.stringify(data4)的结果为："{"name":"abc"}"，正好14个字节(不包含最外层的引号)。blob5的size等于15是如何计算而来的呢？实际上，当使用普通对象创建Blob对象时，相当于调用了普通对象的toString()方法得到字符串数据，然后再创建Blob对象。所以，blob5保存的数据是"[object Object]"，是15个字节(不包含最外层的引号)。

### slice方法
Blob对象有一个slice方法，返回一个新的 Blob对象，包含了源 Blob对象中指定范围内的数据。
slice([start[, end[, contentType]]])
复制代码参数说明：
start： 可选，代表 Blob 里的下标，表示第一个会被会被拷贝进新的 Blob 的字节的起始位置。如果传入的是一个负数，那么这个偏移量将会从数据的末尾从后到前开始计算。
end： 可选，代表的是 Blob 的一个下标，这个下标-1的对应的字节将会是被拷贝进新的Blob 的最后一个字节。如果你传入了一个负数，那么这个偏移量将会从数据的末尾从后到前开始计算。
contentType： 可选，给新的 Blob 赋予一个新的文档类型。这将会把它的 type 属性设为被传入的值。它的默认值是一个空的字符串。
```js
例如：
    var data = "abcdef";
    var blob1 = new Blob([data]);
    var blob2 = blob1.slice(0,3);
    
    console.log(blob1);  //输出：Blob {size: 6, type: ""}
    console.log(blob2);  //输出：Blob {size: 3, type: ""}
```
复制代码通过slice方法，从blob1中创建出一个新的blob对象，size等于3。

## Blob使用场景
分片上传
前面已经说过，File继承自Blob，因此我们可以调用slice方法对大文件进行分片长传。代码如下：
```js
function uploadFile(file) {
  var chunkSize = 1024 * 1024;   // 每片1M大小
  var totalSize = file.size;
  var chunkQuantity = Math.ceil(totalSize/chunkSize);  //分片总数
  var offset = 0;  // 偏移量
  
  var reader = new FileReader();
  reader.onload = function(e) {
    var xhr = new XMLHttpRequest();
    xhr.open("POST","http://xxxx/upload?fileName="+file.name);
    xhr.overrideMimeType("application/octet-stream");
    
    xhr.onreadystatechange = function() {
      if(xhr.readyState === XMLHttpRequest.DONE && xhr.status === 200) {
        ++offset;
        if(offset === chunkQuantity) {
          alert("上传完成");
        } else if(offset === chunkQuantity-1){
          blob = file.slice(offset*chunkSize, totalSize);   // 上传最后一片
          reader.readAsBinaryString(blob);
        } else {
          blob = file.slice(offset*chunkSize, (offset+1)*chunkSize); 
          reader.readAsBinaryString(blob);
        }
      }else {
        alert("上传出错");
      }
    }
    
    if(xhr.sendAsBinary) {
      xhr.sendAsBinary(e.target.result);   // e.target.result是此次读取的分片二进制数据
    } else {
      xhr.send(e.target.result);
    }
  }
   var blob = file.slice(0, chunkSize);
   reader.readAsBinaryString(blob);
}
```
这段代码还可以进一步丰富，比如显示当前的上传进度，使用多个XMLHttpRequest对象并行上传对象（需要传递分片数据的位置参数给服务器端）等。
