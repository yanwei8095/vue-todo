<template>
<div class="todo-container">
    <div class="todo-wrap">
      <Header :addTodo='addTodo'/>
			<Main :todos='todos' :deleteTodo="deleteTodo"/>
			<Footer/>
    </div>
  </div>
</template>
<script>
import Header from './components/Header'
import Main from './components/Main'
import Footer from './components/Footer'
export default{
	data () {
		return {
			todos: [
				{completed: false, title: '吃饭'},
				{completed: true, title: '睡觉'},
				{completed: false, title: '写代码'}
			]
		}
	},
	methods: {
			// 添加todo
			addTodo (todo) {
				this.todos.unshift(todo)
			},
			// 删除todo
			deleteTodo (index) {
				this.todos.splice(index, 1)
			}
		},
	components: {
		Header,
		Main,
		Footer
	}
}
</script>
<style lang='stylus' rel='stylesheet/stylus' scoped>
</style>
