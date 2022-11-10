### 1、通用约定

#### 声明顺序

- 1、positioning(定位)
- 2、Box model(盒子模型)
- 3、Typographic(字体)
- 4、Visual(border)
- 5、Misc

---

样例:

```.declaration-order {
/_ Positioning _/
position: absolute;
top: 0;
right: 0;
bottom: 0;
left: 0;
z-index: 100;

/_ Box-model _/
display: block;
float: right;
width: 100px;
height: 100px;

/_ Typography _/
font: normal 13px "Helvetica Neue", sans-serif;
line-height: 1.5;
color: #333;
text-align: center;

/_ Visual _/
background-color: #f5f5f5;
border: 1px solid #e5e5e5;
border-radius: 3px;

/_ Misc _/
opacity: 1;
}
```

### 命名

#### 组成元素

- 命名元素使用英文、中划线或者数字
- 不建议使用拼音（缩写的拼音、拼音和英文的混合）

```
//不建议使用
.xiangqing { sRules; }
.news_list { sRules; }
.zhuti { sRules; }
```

```
建议使用的规范
.detail { sRules; }
.news-list { sRules; }
.topic { sRules; }
```

#### 词汇规范

- 不依据表现形式来命名
- 可以根据内容来命名
- 可根据功能命名

不推荐

```
left,right,center,red,black

```

推荐

```
nav,aside,news,type,search
```

#### 缩写规范

- 保证缩写后还能较为清晰保持原单词所表达的意思
- 使用业界熟知的或者约定俗成

不推荐

```
navigation   =>  navi
header       =>  head
description  =>  des
```

推荐

```
navigation   =>  nav
header       =>  hd
description  =>  desc
```

#### 前缀规范

| 前缀 | 示例         | 说明                                                        |
| ---- | ------------ | ----------------------------------------------------------- |
| g-   | g-mod        | 全局公用样式命名，一旦修改将会影响全局样式                  |
| m-   | m-detail     | 模块命名方式                                                |
| ui-  | 组件命名方式 | ui-selector                                                 |
| js-  | js-switch    | 用户纯交互的命名，不涉及任何样式规则，JSer 拥有全部定义权限 |

选择器必须是以某个前缀开头

```
<!-- 不推荐 -->
.info {sRules}
.current {sRules}
.news {sRules}
```

```
<!-- 推荐 -->
.m-detail .info{ sRules}
.m-detail .info {sRules}
```

### 提升 CSS 选择器性能

- CSS 选择器是从右到左进行规则匹配。只要当前选择符的左边还有其他选择符，样式系统就会继续向左移动，直到找到和规则匹配的选择符，或者因为不匹配而退出。最右边选择符称之为关键选择器。

#### CSS 选择器的执行效率从高到低做一个排序：

1.id 选择器（#myid） 2.类选择器（.myclassname） 3.标签选择器（div,h1,p） 4.相邻选择器（h1+p） 5.子选择器（ul < li） 6.后代选择器（li a） 7.通配符选择器（\*） 8.属性选择器（a[rel="external"]） 9.伪类选择器（a:hover, li:nth-child）

- 避免使用通用选择器

```
/* Not recommended */
.content * {color: red;}
```

- 避免使用多层标签选择器

```
/* Not recommended */
treeitem[mailfolder="true"] > treerow > treecell {…}
/* Recommended */
.treecell-mailfolder {…}
```

- 避免过度嵌套使用子选择器

```
/* Not recommended */
treehead treerow treecell {…}
/* Recommended */
treehead > treerow > treecell {…}
/* Much to recommended */
.treecell-header {…}
```

- 推荐使用继承

```
/* Not recommended */
#bookmarkMenuItem > .menu-left { list-style-image: url(blah) }
/* Recommended */
#bookmarkMenuItem { list-style-image: url(blah) }
```
