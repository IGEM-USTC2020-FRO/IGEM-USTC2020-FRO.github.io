# 使用 vuex

`vuex` 是 `vue` 的一个状态管理库，详情请查阅[官方文档](https://vuex.vuejs.org/zh/guide/state.html)。

## 什么时候使用 vuex

以下情况你需要使用 `vuex`:

- 你的组件有多层嵌套，需要跨组件传递参数，并且希望参数的改变对组件产生影响。
- 你的组件需要与其他组件通信。
- 你的组件需要使用全局变量或者函数。



## 如何使用

请先从官方文档[了解概念](https://vuex.vuejs.org/zh/guide/state.html)，然后在本项目中使用。

### 使用全局变量

你可以通过下面两种方法使用它：

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



## 定义自己的变量

```
// src/store/modules/yourNameSpace.js/

let state = {
	data1: 2,
	data2: 3
}

let mutations = {
	 func1(params){
	 	console.log(params)
	 }
}

export default {
	namespaced: true,
	state,
	mutations
}

// src/store/index.js/
import yourNameSpace from './modules/yourNameSpace'

const store = new Vuex.STore({
	...	
	modules:{
		yourNameSpace
	}
	...
})


```

首先需要在 `modules` 文件夹下创建你的数据并导出，并在 `index.js` 中注册。

> 请确保 `namespaced` 选项为 `true`，这样可以防止与全局变量发生混淆



## 使用自己的变量

与使用全局变量相同，唯一的改变是命名空间引起的数据位置改变：

```
// method 1
console.log(this.$store.yourNameSpace.data1)

// method 2
import {mapState} from 'vuex'

computed:{
	...mapState('yourNameSpace', ['variableName'])
}

console.log(variableName)
```

除了变量， `mutations`， `actions` 皆可同理。详情请查阅[官方文档](https://vuex.vuejs.org/zh/guide/state.html)