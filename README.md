# Issues Tips

## 1. 解决vue调用第三方api跨域的问题

### 此处使用了axios 替换 vue-resource。
>a. 在项目/config/index.js 里面设置代理，即配置proxyTable项:

``` javascript
    dev: {
        env: require('./dev.env'),
        port: 8080,
        autoOpenBrowser: true,
        assetsSubDirectory: 'static',
        assetsPublicPath: '/',
        proxyTable: {
            '/api': {//使用url请求时使用/api 代替target
                target: 'http://lolapi.games-cube.com',
                changeOrigin: true,
                pathRewrite: {
                    '^/api': ''
                }
            }
        },
        cssSourceMap: false
    }
```
>b. 配置后，在使用 http 请求的时候  baseUrl  使用 /api 代替：

``` javascript
    this.$http({
                method: 'get',
                url: '/Free',
                baseURL: '/api',//使用/api 替换代理的target
                transformRequest: [function (data) {
                    // Do whatever you want to transform the data
                    return data
                }],
                // `transformResponse` allows changes to the response data to be made before
                // it is passed to then/catch
                transformResponse: [function (data) {
                    // Do whatever you want to transform the data
                    return data
                }]
            }).then(m => console.log(m.data))
```

## 2. vue 生命周期图示

> vue 生命周期阶段:
> beforeCreate, created, beforeMount, mouted, beforeUpdate, updated, beforeDestory, destoryed
> vue 2.x 生命周期示意图:
![vue生命周期](http://cn.vuejs.org/images/lifecycle.png)

## 3. npm 常用命令

``` javascript
    npm install xxx 安装模块

    npm install xxx -g 将模块安装到全局环境中 

    npm ls 查看安装的模块及依赖

    npm ls -g 查看全局安装的模块及依赖

    npm uninstall xxx  (-g) 卸载模块

    npm cache clean 清理缓存
```