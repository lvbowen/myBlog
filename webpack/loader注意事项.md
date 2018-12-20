
我们知道webpack 执行某种文件的loader是从右往左执行的，所以顺序很重要。  

1、编译.less 文件，postcss-loader一定要在less-loader上面或左边，即在less-loader后面执行  
```
{
    test: /\.less$/,
    exclude: /node_modules/,
    use: [
        'vue-style-loader',
        'css-loader',       
        'postcss-loader',
        'less-loader',
    ]
},
```