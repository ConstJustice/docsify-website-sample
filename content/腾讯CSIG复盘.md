### 腾讯CSIG复盘

1. 在燃点设计器运行时，一屏或者多屏进行渲染时，组件十分多，如何进行优化？

2. 燃点项目中有使用到什么webpack优化？
   速度优化：

   1. 优化loader配置：缩小文件匹配范围/缓存loader的执行结果
   2. 优化resolve配置：优化模块路径查找resolve.modules/配置别名路径resolve.alias（可能会导致一下treeShaking无效）/resolve.extensions(后缀列表尽可能少，频率最高的往前放)
   3. module.noParse(用了noParse的模块将不会被loaders解析，所以当我们使用的库如果太大，并且其中不包含import require、define的调用，我们就可以使用这项配置来提升性能, 让 Webpack 忽略对部分没采用模块化的文件的递归解析处理)
   4. treeShaking

   大小优化：

   1. CommonsChunk  -> CommonsChunk虽然可以减少包的大小，但存在问题是：即使代码不更新，每次重新打包，vendor都会重新生成，不符合我们分离第三方包的初衷
   2. Externals -> 必须保证全局拥有这个库的，一般通过外部引用，比如index.html里直接script标签引用或者main.js里面引用，它不会被打包
   3. webpack DLL & DllReference

3. 建造者模式有什么特点，有什么亮点？
   定义：将一个复杂对象的构建与它的表示分离，使得同样的构建过程可以创建不同的表示。用户只需指定需要建造的类型就可以得到它们，建造过程及细节不需要知道。

   适用场景：

   1、如果一个对象有非常复杂的内部结构（很多属性）。

   2、想把复杂对象的创建和使用分离。

   优点：

   1、封装性好，创建和使用分离。

   2、扩展性好，建造类之间独立，一定程度上解耦。

   缺点

   1、产生多余的Builder对象。

   2、产品内部发生变化，建造者都要修改，成本较大。

4. 燃点使用了那种编码规范，ESLint使用的哪个库？（完全不懂，资料也没查找得到）