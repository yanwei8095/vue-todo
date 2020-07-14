<template>
<li :style="{background:bgColor}" @mouseenter="handleEnter(true)" @mouseleave="handleEnter(false)">
	<label>
		<input type="checkbox" v-model="completed"/>
		<span>{{todo.title}}</span>
	</label>
	<button class="btn btn-danger" v-show="isShow" @click="deleteItem">删除</button>
</li>
</template>
<script>
	export default {
		// 声明接收属性
		props: {
			todo: Object,
			deleteTodo: Function,
			index: Number,
			selectTodo: Function
		},
		data () {
			return {
				bgColor: 'white',
				isShow: false
			}
		},
		// 为第一次渲染显示做一个同步的准备工作
		beforeMount () {
			// 挂载前同步更新,根据接收的todo来指定completed
			this.completed = this.todo.completed
		},
		// 在第一次显示后，立即做一个异步的工作(发ajax请求,启动定时器)
		// mounted () {
		// 渲染两次,初始渲染和更新渲染,根据接收的todo来指定completed
		// this.completed = this.todo.completed
		// },
		methods: {
			handleEnter (isEnter) {
				if (isEnter) {
					this.bgColor = "#cccccc"
					this.isShow = true
				} else {
					this.bgColor = "#ffffff"
					this.isShow = false
				}
			},
			deleteItem () {
				if (window.confirm(`确认删除${this.todo.title}吗?`)) {
				this.deleteTodo(this.index)
				}
			}
		},
		computed: {
			completed: {
				get () {
					// console.log("get()")
					return this.todo.completed
					// 一旦todo中的completed发生改变,立即改变completed的值
				},
				set (value) {
					// console.log("set()")
					this.selectTodo(this.todo, value)
					// value是completed最新的值，是否勾选上,completed的值发生变化，就会调用下方的方法
				}
			}
		}
 }
</script>
<style lang='stylus' rel='stylesheet/stylus' scoped>
</style>
