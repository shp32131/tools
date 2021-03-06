# markdown

## 标题
> 使用#可以展示1-6级标题,所有的标记符后面需要接一个空格  
- \# 一级标题  
- \#\# 二级标题

## 段落格式
- markdown的段落没有特殊的格式
- 段落的换行是使用两个以上空格加上回车。  

## 列表
> markdown支持有序列表和无序列表
- 无序列表使用 \* 或 \+  或 \- 号作为标记。  
- 有序列表使用数字加上 \. 号来表示
1. 这是有序列表  

> 列表的嵌套只需在子列表中的选项添加四个空格即可  
1. 第一项父列表  
    \+ 第一项父列表的子列表  

## 区块
> markdown区块是在段落开关使用 > 符号
- 区块是可以嵌套的
```
> 这是一个区块引用

> 最外层
>> 第一层
>>> 第二层
```
> 最外层
> > 第一层
> > > 第二层

> 区块中可以使用列表
```
> 区块中使用列表
> 1. 第一项
> 2. 第二项
```

> 区块中使用列表
>
> 1. 第一项
> 2. 第二项    
> - 这是一个无序列表
> - 这也是一个无序列表

> 列表中使用区块,注意四个空格
```markdown
- 第一项
    > 列表中的区块(前面添加四个空格)
```
- 第一项
    > 列表中的区块(前面添加四个空格)

## 代码
> 如果是段落上的一个函数或片段可以直接用\` \`包起来。
`console.log()`
> 如果在markdown中插入代码块使用```三个漂号后面加上语言名称即可
```JavaScript
// javascript
console.log('hello world!');
```

## 链接
> 插入链接方法
```
    [链接名称](链接地址)
```
这是一个链接[markdown教程](https://www.runoob.com)  

**高级链接**  
- 链接地址也可以用变量代替，然后在文档后面为变量赋值
```markdown
这个链接用link1作为网址变量[百度](link1)
[link1]: https://www.baidu.com
```
[百度](link1)
[link1]: www.baidu.com

## 图片
```markdown
markdown图片格式如下：
![alt 属性文本](图片地址)
![属性文本](图片地址 "title")
```

**图片地址也可以使用变量代替**
```markdown
![一个图片](addr)
[addr]: http://www.baidu.com/***.png
```

## 表格 
```
markdown制作表格
使用|来分隔不同的单元格
使用-来分隔表头和其他行
|表头|表头|表头|
|:-|-:|:-:|
|单元格|单元格|单元格|
:-是左对齐
-:是右对齐
:-:剧中对齐
```
|表头|表头|表头|
|:-|-:|:-:|
|左对齐|右对齐|剧中对齐|

## 高级技巧
- 文本加粗，用 \*\*加粗内容\*\* 包裹要加粗的内容  
- 转义特殊符号，用 \\\* 转义正常显示\*符号  
- 插入数学公式，使用两个\$$包裹Tex或LaTex格式来插入数学公式  
- 下脚标，使用\<sub> \</sub>添加下脚标   
- 上脚标，使用\<sup> \</sup>添加上脚标 
