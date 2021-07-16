<p align="center">
  <a href="https://cangdu.org/micro-app/">
    <img src="https://cangdu.org/micro-app/_media/logo.png" alt="logo" width="180" />
  </a>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/@micro-zoe/micro-app"><img src="https://img.shields.io/npm/v/@micro-zoe/micro-app.svg?style=flat-square" alt="version" /></a>
  <a href="https://www.npmjs.com/package/@micro-zoe/micro-app"><img src="https://img.shields.io/npm/dt/@micro-zoe/micro-app.svg?style=flat-square" alt="downloads" /></a>
  <a href="https://www.npmjs.com/package/@micro-zoe/micro-app"><img src="https://img.shields.io/npm/l/@micro-zoe/micro-app.svg?style=flat-square" alt="license" /></a>
  <a href="https://codecov.io/gh/micro-zoe/micro-app"><img src="https://img.shields.io/codecov/c/github/micro-zoe/micro-app.svg?style=flat-square" alt="test:coverage" /></a>
  <a href="https://travis-ci.com/micro-zoe/micro-app"><img src="https://img.shields.io/github/workflow/status/micro-zoe/micro-app/CI.svg?style=flat-square" alt="travis" /></a>
</p>

## 简介
Micro App 是由京东零售iPaaS前端研发团队推出的一款微前端框架，不同于目前流行的开源框架，它从组件化的思维实现微前端，旨在降低上手难度、提升工作效率。Micro App借鉴了WebComponent的思想，通过CustomElement结合自定义的ShadowDom，将所有功能都封装到一个类WebComponent组件中，从而实现在基座应用中嵌入一行代码即可渲染一个微前端应用，它是目前市面上接入成本最低的微前端框架。

## 功能
`Micro App`提供了`JS沙箱`、`样式隔离`、`元素隔离`、`数据通信`等一系列完善的功能。

<p align="center">
  <a href="https://cangdu.org/micro-app/">
    <img src="https://cangdu.org/img/micro-app-functions.png" alt="logo" height="150" />
  </a>
</p>

## 开始使用
微前端分为基座应用和子应用，我们分别列出基座应用和子应用需要进行的修改，具体介绍`Micro App`的使用方式。

`下述以react代码为例`

#### 基座应用
1、安装依赖
```bash
yarn add @micro-zoe/micro-app
```

2、在入口处引入依赖
```js
// index.js
import microApp from '@micro-zoe/micro-app'

microApp.start()
```

3、分配一个路由给子应用
```js
import { BrowserRouter, Switch, Route } from 'react-router-dom'
import MyPage from './my-page'

export default function AppRoute () {
  return (
    <BrowserRouter>
      <Switch>
        // 👇 非严格匹配，/my-page/* 都将匹配到 MyPage 组件
        <Route path='/my-page'>
          <MyPage />
        </Route>
        ...
      </Switch>
    </BrowserRouter>
  )
}
```

4、在页面中使用组件
```js
// my-page.js
export function MyPage () {
  return (
    <div>
      <h1>加载子应用</h1>
      // 👇 micro-app为自定义标签，可以在任何地方使用
      <micro-app name='app1' url='http://localhost:3000/' baseurl='/my-page'></micro-app>
    </div>
  )
}
```

#### 子应用
添加路由前缀

```js
import { BrowserRouter, Switch, Route } from 'react-router-dom'

export default function AppRoute () {
  return (
    // 👇 添加路由前缀，子应用可以通过window.__MICRO_APP_BASE_URL__获取基座下发的baseurl
    <BrowserRouter basename={window.__MICRO_APP_BASE_URL__ || '/'}>
      <Switch>
        ...
      </Switch>
    </BrowserRouter>
  )
}
```
以上即完成了微前端的渲染。

**注意**: 子应用的静态资源需要支持跨域访问。

## 本地开发
1、下载项目
```
git clone https://github.com/micro-zoe/micro-app.git
```

2、安装依赖
```
yarn bootstrap
```

3、运行项目
```
yarn start # 访问 http://localhost:3000
```

默认启动react基座应用，如果想启动vue基座应用，可以运行`yarn start:main-vue2`

## FAQ
https://cangdu.org/micro-app/docs.html#/zh-cn/questions

## License
MIT
