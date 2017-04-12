
Vue 2017 现状与展望
--------------------------


![Alt text|800x0](https://zhongqiang1839.github.io/static/img/doc/1491814322591.png)




> **~~Just  a view layer library~~**

-----------------------------------


> **The Progressive Framework**


-----------------------------------

![Alt text |800x0](https://zhongqiang1839.github.io/static/img/doc/IMG_01.JPG)


-----------------------------------

![Alt text |800x0](https://zhongqiang1839.github.io/static/img/doc/IMG_02.JPG)

-----------------------------------

> Today's Stats
- 接近 50.000 GitHub stars(目前排名第12)
- NPM 每月50万次下载
-  Chrome 开发者插件14.6万周活跃用户



![Alt text|800x0](https://zhongqiang1839.github.io/static/img/doc/IMG_03.JPG)


-----------------------------------

> *2016.9.30*  vue2.0 Ghost in the shell

-----------------------------------


> VUE2.0
- 从头重写，但保留了绝对部分的 API
- 引入 [Flow](http://www.cnblogs.com/owenyang/p/4129366.html) 类型检查，提高了代码的健壮性
- 基于 [Virtral Dom](http://www.cnblogs.com/justany/archive/2015/04/08/4401118.html) 的渲染机制： 更轻，更快；
- 跨平台渲染： 服务端渲染（SSR） + 移动端原生渲染（Weex）
- 官方 TypeScript 类型声明

[* flow jslint typescrpt 的 difference](https://segmentfault.com/a/1190000005150319) 


-----------------------------------
> *模板预编译*

Template --[ parser ] -> AST --[codegen] -> Render Function


抽象语法树（Abstract Syntax Tree）也称为AST语法树，指的是源代码语法所对应的树状结构。也就是说，对于一种具体编程语言下的源代码，通过构建语法树的形式将源代码中的语句映射到树中的每一个节点上。

![Alt text](https://zhongqiang1839.github.io/static/img/doc/IMG_04.png)

-----------------------------------
- 两次编译模式，运行时 or 构建时
- [两段式编译：运行时用基于 with 的简易编译器，构建时额外一次编译去掉 with](https://www.zhihu.com/question/49929356?sort=created)
- [编译器可剥离：构建时模板不需要在运行时包含编译器，可以减少将近 8KB gzip](http://www.codesec.net/view/487394.html)

-----------------------------------
服务端渲染：

- 流式渲染： 充分利用 Node 和 HTTP 对 streaming 的支持；
- 组件级缓存 ： 大幅度提升抗压性能
- bundleRenderer ：解决同构代码在服务端的构建和部署

-----------------------------------
Scoped Slots

- 传递一个可复用的模板片段给子组件

![Alt text](https://zhongqiang1839.github.io/static/img/doc/IMG_05.png)


-----------------------------------

> *2016.12.16*  --- Vue 2.1

-----------------------------------

> *2016.12.22* --- weex 0.9.4 第一个正式包含 Vue 2.0 的 Weex 版本


-----------------------------------

> *2017.1.5* vue-devtools 3.0

-----------------------------------

> *2017.2.26* Vue2.2 Inital D

-----------------------------------
> *内置 Chrome Timeline 性能追踪支持*Î
- vue.config.performance = true

![Alt text](https://zhongqiang1839.github.io/static/img/doc/IMG_06.png)

Coming soon -Vue 2.3 Jojo's bizarre Adventrue

![Alt text](https://zhongqiang1839.github.io/static/img/doc/IMG_07.png)


> *2.3 异步组件改进*

- Loading / Error / Timeout fallback


``` javascript
		
	const Foo = () => ({
		component:import("./Foo.vue"),
		error: LoadingComponent,
		delay:200,
		timeout:3000	
	})

```


> *函数式组件改进*

- 不在需要显式声明 props
- 父组件添加的 v-on 会以 ctx.listeners 的形式提供

``` vbscript-html
	<bar
		:msg = "msg"
		@click="onBarClicked">
	</Bar>	
```

``` javascript
	const Bar = {

		function:true,
		render(h,{porps,listeners}){
			return h('div',{
				on：{click：listeners.click}
			},[props.msg])
		}
	}
```

-----------------------------------

> *2.3 的其他改进*

- passive 事件侦听：@touchmove.passive
- .sync 将会以 prop + listener 语法糖的形式回归


-----------------------------------

> *2017 展 望*

- 更好的 TypeScript 整合： TypeScript 团队为 vue 量身打造更好的类型推导
- 单文件组件 CSS 改进 : >>> 和 ::slotted 选择器， css variable theming
- SSR 性能进一步优化
- Vuex 与 Rx 的整合















