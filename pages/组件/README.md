# 组件

你可以自由组织你的组件结构，在最后需要交付的的是与你组件文件夹同名的组件。

这里给大家提供一些风格指南。

## 命名规范

1. 组件文件夹使用驼峰式（首字母大写）连接，所有开发组件 `.vue` 文件同样以驼峰式命名，并在后缀加上 `View`。

2. 不论同一个组件文件夹下有多少 `.vue` 文件，最后暴露的组件（即 `App.vue` 或者 `vue-router` 可访问组件）为与组件文件夹下同名的组件。

3. 通俗来说，以与组件文件夹下同名 `.vue` 文件作为根组件。

   > 示例：
   >
   > ```
   > // src/FirstComponent/FirstComponentView.vue
   > // 这个组件可以在 App.vue 中以 <first-component></first-component> 调用
   > 
   > <template></template>
   > ...
   > 
   > // src/FirstComponent/SecondComponentView.vue
   > // 这个组件只能被该组件文件夹下的其他组件以 <second-component></second-component> 方式调用
   > 
   > <template></template>
   > ...
   > ```



## 减少 DOM 操作

`Vue` 的方法中也支持 `DOM` 操作，但是这是极不推荐的。因为 `DOM` 的直接操作不在 `Vue` 管辖内，可能出现未知错误。

`Vue` 本身提供了大量方法用以替代 `DOM` 操作。

**使用数据绑定**

一个常见需求是需要根据条件隐藏显示 类/元素，你可以这样完成

```
// template
<span :class="{active:isActive}" :click="active">
<div v-if:"isActive"></div>	

// script
data(){
	return {
		isActive: false
	}
},
methods:{
	active(){
		this.isActive = true
	}
}
```

这可以解决绝大多数 `DOM` 操作问题。

**列表循环**

当某个元素较多时，你需要列表渲染，同时对列表中的每一项进行一些数据处理。在这种情况下，我们推荐你将循环元素作为一个单独组件，并书写处理逻辑。每个组件都是一个独立的实例化对象。



## UI 库

默认使用 `BootstrapVue` 作为默认 `UI` 库。所有组件都可以使用，但是请一定记住要按需导入，而不要一次性全部导入，并删除无效引用。这样可以控制包大小。



## 数据传递

在你的组件内，任何数据传递方式都是可行的。如果你需要跨组件获取数据，你需要使用 `vuex`。如果你希望在你自己组件内使用 `vuex`，请参阅相关文档。



## 样式

`Sass` 虽然被强制导入，但是其语法是可选的。因为 `Sass` 完全支持原生 `CSS`。要了解更多，请查阅我们的样式文档。



## eslint

`eslint` 是一种语法规范，它会限制你的代码编写，使用它有利于你编写更高效代码。如果你的代码书写有错误，它将无法通过编译。你不需要特意关注它的内容，因为在你有书写错误代码时它会自动指出。如果你感兴趣，你可以自行了解更多。