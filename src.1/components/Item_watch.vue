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
				isShow: false,
				completed: false // 需要根据传进来的todo的completed值修改
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
		// 一旦data中的completed发生改变,立即改变todo中completed的值
		watch: { // 基本数据类型,没有深度监视
			completed (value) { // value是completed最新的值
			// 最终目的是为了this.todo.completed=value,不能在子组件中直接修改父组件的状态数据
			this.selectTodo(this.todo, value)
			// console.log('watch--completed')
			},
			// 监视性能不好，导致重复调用
			'todo.completed' (val) {
				this.completed = val
				// console.log('watch--todo.completed')
			}
		}
 }
</script>
<style lang='stylus' rel='stylesheet/stylus' scoped>
</style>
