#  scss入门

**下载**

```javascript
npm i sass -g
```



紧接着初始化项目



##  开始

index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>scss入门学习</title>
</head>
<body>
    <div class="app">
        <h1>scss入门学习</h1>
        <div class="box">
            <div class="boxChild"></div>
            <div class="boxChild"></div>
            <div class="boxChild"></div>
            <div class="boxChild"></div>
        </div>
        <div class="extendBox">
            <div class="boxChild"></div>
            <div class="boxChild"></div>
            <div class="boxChild"></div>
            <div class="boxChild"></div>
            <div class="extendBoxChild"></div>
        </div>
    </div>
</body>
</html>
```



index.scss

```scss
body {
    margin: 0;
    padding: 0;
    h1 {
        color: #123456;
    }
}
```



打开cmd命令控制符输入

```
sass index.scss ouput.css
```



就会将index.scss输出成ouput.css

再将css引入html中



为了每次更新scss自动更新到css，输入

```
sass --watch index.scss:ouput.css
```

如果要监听文件夹的话

```
sass --watch scss的文件夹:css的文件夹
```



##  变量

```scss
$base_color: red;
$base_border: 1px solid red;

body {
    margin: 0;
    padding: 0;
    h1 {
        color: $base_color;
        border: $base_border;
    }
}
```



!global可以将局部变量转换为全局变量



```scss
body {
    margin: 0;
    padding: 0;
    h1 {
        $base_color: rgb(0, 255, 13) !global;
        color: $base_color;
        border: $base_border;
        font: {
            size: 36px;
            weight: bold;
        }
        &:hover {
            color: $change_color;
            cursor: pointer;
        }
    }
}
```





##  嵌套

&父选择器

```scss
$base_color: red;
$base_border: 1px solid red;

$change_color: blue;

body {
    margin: 0;
    padding: 0;
    h1 {
        color: $base_color;
        border: $base_border;
        &:hover {
            color: $change_color;
            cursor: pointer;
        }
    }
}
```



属性也可以嵌套

```scss
body {
    margin: 0;
    padding: 0;
    h1 {
        color: $base_color;
        border: $base_border;
        font: {
            size: 36px;
            weight: bold;
        }
        &:hover {
            color: $change_color;
            cursor: pointer;
        }
    }
}
```



##  支持多行注释



##  mixin混合



```scss
$base_color: red;
$base_border: 1px solid red;

$change_color: blue;

@mixin pStyle {
    color: pink;
    background: {
        color: rgb(124, 124, 0);
    }
}

body {
    margin: 0;
    padding: 0;
    h1 {
        $base_color: rgb(0, 255, 13) !global;
        color: $base_color;
        border: $base_border;
        font: {
            size: 36px;
            weight: bold;
        }
        &:hover {
            color: $change_color;
            cursor: pointer;
        }
    }
    p {
        @include pStyle;
    }
}
```

@mixin里还可以传入参数

@content用在mixin里面，当定义了一个mixin后，并且设置@content；@include的时候就可以传入相应的内容进去

```scss
   
@mixin pStyle {
    color: pink;
    background: {
        color: rgb(124, 124, 0);
    }
    @content;
}

   .title1 {
        @include pStyle {
            font-size: $base_fontSize_mlg;
        };
    }
```





##  继承扩展

@extend

```scss
$base_color: red;
$base_border: 1px solid red;

$change_color: blue;

@mixin pStyle {
    color: pink;
    background: {
        color: rgb(124, 124, 0);
    }
}

body {
    margin: 0;
    padding: 0;
    h1 {
        $base_color: rgb(0, 255, 13) !global;
        color: $base_color;
        border: $base_border;
        font: {
            size: 36px;
            weight: bold;
        }
        &:hover {
            color: $change_color;
            cursor: pointer;
        }
    }
    .title1 {
        @include pStyle;
    }
    .title2 {
        @extend .title1;
    }
}
```



##  @import引入

被引入的scss不会转换成css，需要对这类文件命名以下划线开头，如_base.scss,而引入它的时候不用写下划线

```scss
@import: "base.scss";
```

_base.scss里的内容

```scss
//字体
$base_fontSize: 16px;
$base_fontSize_lg: $base_fontSize * 1.5;
$base_fontSize_mlg: $base_fontSize * 1.75;

//字体颜色
$base_color1: red;
$base_color2: yellow;
$base_color3: rgb(42, 252, 206);
$base_color4: rgb(16, 60, 126);

//背景颜色
$base_backColor: rgb(224, 122, 255) rgb(131, 129, 255);
```



##  计算功能

```scss
@import "base.scss";

$base_color: red;
$base_border: 1px solid red;

$change_color: blue;

@mixin pStyle {
    color: pink;
    background: {
        color: rgb(124, 124, 0);
    }
}

body {
    margin: 0;
    padding: 0;
    h1 {
        $base_color: rgb(0, 255, 13) !global;
        color: $base_color;
        border: $base_border;
        font: {
            size: 36px;
            weight: bold;
        }
        &:hover {
            color: $change_color;
            cursor: pointer;
        }
    }
    .title1 {
        @include pStyle;
    }
    .title2 {
        @extend .title1;
        font-size: $base_fontSize_lg; //_base.scss里面
        height: 16px * 2;
    }
}
```



##  插值#{}



```scss
.title3 {
	#{$yanse}: red;
}
```



##  if判断



```scss
@if 判断条件 {
.......执行语句...
} @else {
  ...else有就写没就不写....
}
```



```scss
@import "base.scss";

$base_color: red;
$base_border: 1px solid red;

$change_color: blue;

$yanse: color;

@mixin pStyle {
    color: pink;
    background: {
        color: rgb(124, 124, 0);
    }
}

body {
    margin: 0;
    padding: 0;
    @if 2>3 {
        background-color: white;
    }@else{
        background-color: black;
    }
    h1 {
        $base_color: rgb(0, 255, 13) !global;
        color: $base_color;
        border: $base_border;
        font: {
            size: 36px;
            weight: bold;
        }
        &:hover {
            color: $change_color;
            cursor: pointer;
        }
    }
    .title1 {
        @include pStyle;
    }
    .title2 {
        @extend .title1;
        font-size: $base_fontSize_lg;
        height: 16px * 2;
    }
    .title3 {
        #{$yanse}: red;
    }
}
```



##  for循环

语法

```scss
结束值执行：
@for 变量 from 开始值 through 结束值 {
     ......
}
结束值不执行：
@for 变量 from 开始值 to 结束值 {
     ......
}
```





##  列表循环

```scss
@each 变量 in 列表{
...
}
```



##  &嵌套

当一个元素的样式在另一个容器中有其他指定的样式时，可以使用嵌套选择器让他们保持在同一个地方。

`.no-opacity &`相当于`.no-opacity .foo`。
