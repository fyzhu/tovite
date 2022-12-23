# Move to Vite
## 常用配置
### vue2
```bash
pnpm i vite-plugin-vue2 -D
```
### alias
```js
resolve: {
    alias: [
      {
        find: '@/',
        replacement: REPLACEMENT,
      },
      // {
      //   find: 'src/',
      //   replacement: REPLACEMENT,
      // },
    ],
  },
```
### define
```js
define: {
    APP_NAME: '"h5offline"',
  },
```

### proxy & port & fs
```js
server: {
    port: 80,
    proxy: {
      '/dyn': {
        target: 'http://umapopenapi-dev.jd.com:8888/',
        secure: false,
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/dyn/, '')
      },
    }
    // fs: {
    //   // Allow serving files from one level up to the project root
    //   allow: ['..'] // 允许处理 joyer-components 里的图片等静态资源
    // }
  },
```
## 常见报错
### 1.node builtin
`Module "xxx" has been externalized for browser compatibility. Cannot access "xxx" in client code.`

#### 解决方案：

1. 使用 polyfill 浏览器端版本，如：crypto -> crypto-browserify [demo](https://github.com/vitejs/vite/discussions/4479)
2. 使用对应的 browser 端 API，如：[crypto web api](https://developer.mozilla.org/en-US/docs/Web/API/Crypto)
3. 如果使用第三方包，可以寻找替换包
4. rollup-plugin-polyfill-node（rollup-plugin-node-polyfills、rollup-plugin-node-builtins） 部分支持，如：不支持 crypto.randomFillSync 方法


#### 遇到的
1. crypto -> crypto-browserify 需要设置 `alias: {'crypto': 'crypto-browserify'}`     
2. buffer
3. events
4. steam
5. util


#### webpack 是如何解决的

`node-libs-browser`  
v4 会自动引入   
v5 会给予提示，手动引入  
[webpack5 新特性](https://www.jianshu.com/p/eacdd98d25b0)

### 2.global is undefined
window.global = window

### 3.process is undefined
```js
export default defineConfig({
  define: {
    'process.env.NODE_DEBUG': 'false',
    'process.env.NODE_ENV': '"production"'
  }
}
```
### 4.URI malformed
删除 index.html 里的不规则 URL，如： `<%= BASE_URL %>`

### 5.公共 sass 引入
```
css: {
    preprocessorOptions: {
      scss: {
        additionalData: `
          @import "@/assets/scss/variable.scss";
          @import "@/assets/scss/mixin.scss";
        `
      }
    }
  }
```
## 课程

[慕课课程](https://coding.imooc.com/class/523.html)

[掘金小册](https://s.juejin.cn/ds/2dPSFtU/)

[vite 文档](https://vitejs.cn/)

[vite 仓库](https://github.com/vitejs/vite)
