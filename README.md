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
