# 字节跳动
## 一面
1. git 缓存区工作区
1. 虚拟DOM diff 发散一下思维???
1. 回流 重绘
1. rem em
1. React新特性 新钩子 HOOKS HOC
1. SSL握手过程 对称加密非对称加密
1. 深拷贝
1. 箭头函数的this
1. node 事件循环
1. 数据库索引
1. fs读取文件转buffer
1. 性能优化 多种方案
1. http缓存
1. 打包的性能优化
将业务和依赖分开打包，依赖部分做缓存
1. 容器高度是宽度的两倍 多种写法
1. 自适应 多种办法
1. React的优秀之处 源码 发散一下思维???

## 二面
我主要有四个项目，一个是next搞的比赛系统(类似于OJ)，一个是自己实现了一个cli（npm install sacc-cli -g），一个是专利搜索系统，最后一个是社团主页
面试官主要针对的是我的cli这个项目

Q:我怎么去实现的

A:通过自己定义模板然后放到git上通过执行`git clone`来实现

Q:遇到的难点，怎么解决的

A:无法判断操作系统而准确的执行相应的shell命令，解决方法是通过让用户选择自己的操作系统，并不能自己判断（面试官建议我去看看vue-cli 3的源码 后面问了一下vue-cli 2的源码）

Q:打开我的git看了我的代码提出问题（有一个记不得了）

```
-----------------------------------------
async (err, projectName, tplName) => {
  spinner1.stop();
  console.log('√文件目录生成成功')
  if (err) {
    tip.fail('文件名称重复!');
    process.exit();
  }
  spinner2.start();
}
-----------------------------------------
//以上是我的代码 error-first callback

abc('close', cb)

完成一个 convert 函数
目标：将 error-first style cb 转成 Promise 调用的方式。
const abd = convert(abc);
try {
    const param = await abd('close');
}
catch (err) {
    // handle err
}


function convert() {
   //...
}
```
A:写的过程曲折离奇，面试官提示了好多次才写出来的，感觉整个人都懵了
```
function convert(fn){
    if(!fn){return }
    return function(str){
        return new Promise((resolve,reject)=>{
            fn(str,(err,arg)=>{
                if(err){
                    reject(err)
                }else{
                    resolve(arg)
                }
            })
            
        })
    }
}
```
Q:有没有什么想问的
A:没有了

总结下来，二面的时候前半段面试官还是对我比较欣赏的，开始写代码以后就没有什么特别亮眼的表现了，把自己前面的加分给扣完了，万幸还是过了。

## 三面
三面换了一个姐姐来面试我，主要也是针对我的项目，首先让我介绍了一下我做过的东西，挑简历上有的介绍没有的就随便提一下。

Q:看你简历上写着做过数据可视化，讲讲你是怎么去做的

A:主要还是调API，比较复杂的地方是去设计可视化部分怎么去展示以及数据的转换

Q:数据转换具体说一下

A:说的比较简单就是说了一下操作数组对象转换成相应的数据格式以及通过官方文档里给的transform

Q:当量级变大肯定会变慢，怎么去解决

A:首先量级变大肯定是数据量变大了，这个可以去做本地缓存（比如存localstorage），更新频率高的交给http缓存。渲染怎么去优化我没打上来就是简单说了一下为什么会变慢（触发回流什么的）以及怎么去解决减少触发回流

Q:你之前提到浏览器的渲染机制详细展开说一说

Q:为什么会去做cli

A:曾使用过`create-react-app`和`vue-cli`发现都有一个通病就是装了太多我不需要的东西，我自己制作出来的cli相对于会比较纯净只拥有一些基础的依赖，还有有时候我们并不需要最新版的依赖而是特定版本的依赖

Q:设计一个input组件类似于百度输入框

A:零碎的说了几点
1. 默认热词（网页生成时拿到）
2. 类下拉的一个提示框，当聚焦input的时候可以根据方向键使用，上下的时候分别聚焦选中部分
3. 对用户搜索词做一些浏览器缓存（感觉没啥用
4. 节流（提示词部分
5. 还有一些公式化的设计标准等等

Q:为什么会选择前端

Q:职业规划

总结三面虽然面试官看起来像是没有感情的杀手但是人还是挺好的，给了我很多解决问题的思路引导我提出解决方案。
