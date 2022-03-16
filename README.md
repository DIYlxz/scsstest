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

