# 一、媒体查询用法 

 @media 媒体查询包含一个可选的[媒体类型](https://developer.mozilla.org/en-US/docs/CSS/@media)和，满足CSS3规范的条件下，包含零个或多个表达式，这些表达式描述了媒体特征，最终会被解析为true或false。如果媒体查询中指定的媒体类型匹配展示文档所使用的设备类型，并且所有的表达式的值都是true，那么该媒体查询的结果为true.

　　(1)500px-800px之间的设备 `@media screen and (min-width: 500px) and (max-width: 800px) { ... }`

​       (2)最小宽度500  @media screen and (min-width: 500px){... }

　　(3)在非打印设备下 @media not print and (max-width: 1200px)



# 二、常见的媒体查询尺寸

@media screen and (min-width:1200px)

@media screen and (min-width:992px)

@media screen and (min-width:768px)

@media screen and (min-width:480px)

在设置时，需要注意先后顺序，不然后面的会覆盖前面的样式。