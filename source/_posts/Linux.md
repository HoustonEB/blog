---
title: Linux
date: 2019-05-04 18:35:32
tags: Linux命令
---
#### Linux常用命令
---
```bash
cd 进入目录

pwd 列出当前的路径

ls 列出目录的结构
  -a 列出隐藏的文件

mkdir 创建文件夹

cat 查看文件的内容
<!-- more -->
touch 文件名.格式 创建指定的文件

echo '文件内容' >> 文件名.文件格式 创建文件内容和文件

cp 复制目录时不会复制子目录和子文件
  -r 递归复制,会复制子目录和子文件

mv 移动文件夹和目录, 还可以重命名文件和目录
eg: mv test.md test.txt 重命名
    mv test.md .. 移动到上一层目录
    mv test.md ../test2/ 移动到上一层的test2的目录下
    mv test.md ../test2 移动到上一层并重新命名为test2
    mv test1 test2 将目录test1重命名为test2

rm 删除文件和文件夹
  -rf 递归删除所有子目录和子文件

rmdir 只能删除空目录

vi 编辑文件
  i 编辑内容
  esc 退出操作
  shift+z+z 保存退出vi模式 
```