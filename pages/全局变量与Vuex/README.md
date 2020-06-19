# 全局变量

部分数据作为公共的数据将被定义为全局变量。全局变量不得随意更改，你只能取得值。

全局变量是通过 `vuex` 实现的。

## 创建一个全局变量

```
// src/store/global.js

export default {
	variableName: 'name'
}
```

将全局变量导出即可



## 在项目中使用全局变量

全局变量通过 `vuex` 实现，你可以通过下面两种方法使用它：

```
// method 1
console.log(this.$store.variableName)

// method 2
import {mapState} from 'vuex'

computed:{
	...mapState(['variableName'])
}

console.log(variableName)
```

详细方法请查阅 [`vuex` 文档](https://vuex.vuejs.org/zh/guide/state.html)。

