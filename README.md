# Move to Vite
## error
### node builtin
`Module "xxx" has been externalized for browser compatibility. Cannot access "xxx" in client code.`

#### 解决方案：

1. 使用 polyfill 浏览器端版本，如：crypto -> crypto-browserify
2. 使用对应的 browser 端 API，如：http -> fetch
3. 如果使用第三方包，可以寻找替换包
4. rollup-plugin-polyfill-node（rollup-plugin-node-polyfills） 部分支持，如：不支持 crypto.randomFillSync 方法


#### 遇到的
1. crypto
2. buffer
3. events
4. steam
5. util


#### webpack 是如何解决的

`node-libs-browser`  
v4 会自动引入   
v5 会给予提示，手动引入  
[webpack5 新特性](https://www.jianshu.com/p/eacdd98d25b0)

## 课程

[慕课课程](https://coding.imooc.com/class/523.html)

[掘金小册](https://s.juejin.cn/ds/2dPSFtU/)

[vite 文档](https://vitejs.cn/)

[vite 仓库](https://github.com/vitejs/vite)
