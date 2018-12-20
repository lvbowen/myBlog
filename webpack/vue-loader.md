
## vue-loader  
给样式文件或图片目录设置别名后，在.vue文件引入的时候需要加~，[参考](https://github.com/vuejs/vue-loader/issues/193)
```
  alias: {
    '@src': path.resolve(__dirname, '../src'),
    '@assets': path.resolve(__dirname, '../src/assets'),
    '@components': path.resolve(__dirname, '../src/components')
  }
```
index.vue  
```
<template>
    <div class="box">
        <img src="~@assets/img/01.png" />
    </div>
</template>
<script>

</script>
<style lang="less" scoped>
@import '~@assets/styles/common.less';      //.less 后缀可以省略；不要在script里import样式文件，否则使用一些语法会报错，如mixin

.box{
    background:url('~@assets/img/02.png');
}
</style>
```
意思就是: 告诉加载器它是一个模块，而不是相对路径。