

​          // 这个loader取代style-loader。作用：提取js中的css成单独文件

​          MiniCssExtractPlugin.loader,



OptimizeCssAssetsWebpackPlugin



css-loader

对css中做处理,把css模块转化为js模块



style-loader

插入dom中



### vue-loader

将单文件编译成vue对象

用起来更加方便

Scoped CSS

热重载



##file-loader

 allows you to designate where to copy and place the asset file, and how to name it using version hashes for better caching.

，*file*-*loader* 就是在JavaScript 代码里import/require 一个文件时，会将该文件生成到输出目录，并且在JavaScript 代码里返回该文件的地址。



### `url-loader`

 allows you to conditionally inline a file as base-64 data URL if they are smaller than a given threshold. 