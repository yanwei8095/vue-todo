<template>
<li :style="{background:bgColor}" @mouseenter="handleEnter(true)" @mouseleave="handleEnter(false)">
	<label>
		<input type="checkbox" v-model="todo.completed"/>
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
			index: Number
		},
		data () {
			return {
				bgColor: 'white',
				isShow: false
			}
		},
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
			deleteItem (index) {
				if (window.confirm(`确认删除${this.todo.title}吗?`)) {
				this.deleteTodo(this.index)
				}
			}
		}
 }
</script>
<style lang='stylus' rel='stylesheet/stylus' scoped>
</style>
