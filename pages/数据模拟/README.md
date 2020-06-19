# 数据模拟

本项目使用 `mock` 进行数据模拟。

## mock 模式

具体使用方法可以[查看文档](http://mockjs.com/)，`mockjs` 自带强大的随机数据生成功能。

你书写的模拟请求放在 `src/mock/modules` 文件夹下的相应位置。

下面给出一个示例：

```
// /src/mock/modules/test.js
// 定义数据
const listData = {
    'data': 'mock 测试成功'
}

function list() {
    return {
        code: 200,
        data: listData.data,
        msg: '请求成功'
    }
}

export default {list}

// /src/mock/index.js
// 别忘了注册,url支持正则
Mock.mock(/\/path\/to\/your\/url/, 'get',test_list.list)
```

> 实际上，书写一个可靠的模拟请求比较花费时间。但是考虑到我们项目请求不会很多，所以这种方法可行。
>
> 如果有机会，我会帮大家尝试书写一个模拟请求。

