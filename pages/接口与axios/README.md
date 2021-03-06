# 接口与 axios

> 本文描述项目的接口管理策略



## 标准接口

除非遇到服务器宕机或者未找到，否则我们的服务器一定会向我们返回 `json` 回应。如果请求参数有误，会以错误码与消息提供：

```
// a basic form of response

{
	code: 200,
	msg: 'success',
	data: {
		...
	}
}
```

`code` 表示信息编号，`msg` 表示状态，`data` 则表示我们请求的数据。这些都由后端提供。

代号与消息的规则如下：

> 待协商完善



## 导入接口

本项目使用 `axios` 进行请求。但是你不能直接使用 `axios` 发送请求。这是因为请求往往带有登录需求，需要我们进一步封装。

你能直接使用的只有我们提供的接口，要使用它，首先请在 `/src/axios/api` 下找到你需要的 `api`。然后在你的组件中这样引入：

```
// path/to/your/component

import {APIName} from '@/axios'

```

大括号是必要的，因为你使用的不是默认导入 `export default`。

> 为什么不需要在 `api` 的指定文件导入呢？如果你查看 `src/axios/index.js` 文件，你会发现该文件将所有 `api` 进行了导出。这样的好处是方便引用，同时也方便管理。



## 使用接口

所有 `api` 的都是函数，它返回一个  `promise` 对象。这个过程是异步的。一些 `api` 可能需要传入参数，具体请查阅接口文档。

如果是组件初始化就需要请求数据，我们推荐将它放在 `mounted` 或者 `created` 钩子上。

一个典型的调用可以是这样：

```
// path/to/your/component

import {testAPI} from '@/axios'
...

// call the API, return a promise
testAPI()
	.then((rsp)=>{
	const data = rsp.data
	// process data
})
	.catch((err)=>{
	// process error
	})
```

除非服务器出现错误或者你的请求路由错误（这往往是你传入了错误的参数），否则后端都会返回请求。

`then` 中返回的是数据，你可以通过 `rsp.data` 获取。

`catch` 会拦截错误，常见的错误拦截有(x标识任意数字)：

- 不存在(404)
- 服务器错误(5xx)
- 用户未登录(401)

通过我们预先设置好的拦截器，我们会自动将未登录请求重定向到首页，你不需要处理跳转逻辑。

> 所有的登录管理都是 `API` 设计好的，使用 `API` 的重点是获取数据。用户验证则是 `API` 管理的事情。如果你对此感兴趣，可以参阅我们的接口与axios章节。

除了验证错误，最常见的错误是 `500` 与 `404`，为此，你可能需要在数据展示位置添加一个"服务器错误"的说明并要求用户重试。



## 开发接口

一个接口对应一个 `.js` 文件，位于 `src/axios/api` 目录下。一个标准的接口如下：

```
// src/axios/api/testAPI.js

import axios from '@/axios'

const base = 'api/test/'

function testAPI(params) {
	// concat params
	const url = base  + params.id
	
	// return promise
    return axios.get(url, params.params)
}

// export API
export {
    testAPI
}


// always remember to export your API
// src/axios/index.js
export * from './api/testAPI'
```

要求导出与文件同名 `js`。

这样就能暴露你开发的 `API` 了。

上面只是对 `params` 进行一个示例，具体的 `params` 请查阅相关 `api` 说明。