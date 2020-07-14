<template>
<div class="todo-container">
    <div class="todo-wrap">
      <Header @addTodo='addTodo'/>
			<Main :todos='todos'  :selectTodo="selectTodo"/>
			<Footer :todos="todos" :selectAllTodos="selectAllTodos" :deleteAllCompleted="deleteAllCompleted"/>
    </div>
  </div>
</template>
<script>
// import Header from './components/Header'
import Main from './components/Main'
import Footer from './components/Footer'
import storageUtils from "./utils/storageUtils"
import PubSub from "pubsub-js"

export default{
	data () {
		return {
			// todos: JSON.parse(localStorage.getItem("todos_key") || "[]") // localStorage.getItem("todos_key")的值是字符串,也有可能是null
			todos: storageUtils.getTodos()
		}
	},
		mounted () {
			// 订阅消息
		PubSub.subscribe('deleteTodo', (msgName, index) => {
			this.deleteTodo(index)
		})
		},
	methods: {
			// 添加todo
			addTodo (todo) {
				this.todos.unshift(todo)
			},
			// 删除todo
			deleteTodo (index) {
				this.todos.splice(index, 1)
			},
			// 对所有todo进行全选或全不选
			selectAllTodos (isCheck) {
				this.todos.forEach(todo => { todo.completed = isCheck })
			},
			// 删除所有completed为true的对象
			deleteAllCompleted () {
			this.todos =	this.todos.filter(todo => !todo.completed) // 保留未勾选的,过滤掉勾选的
			},
			// 是否勾选或者不勾选
			selectTodo (todo, isCheck) {
				todo.completed = isCheck
			}
		},
	watch: {
		todos: {
			deep: true, // 深度监视
			handler: function (val) { // val:todos最新的值,todos发生任何变化时都会调用
			// 将todos最新的值保存到local
			storageUtils.saveTodos(val)
			// localStorage.setItem("todos_key", JSON.stringify(val))
			// local里面只能存文本,不能存对象，传入对象会调用对象的toString(),会得到[{object,object}],里面的对象没法再解析出来
			}
			// handler:storageUtils.saveTodos
		}
	},
		components: {
			// Header,
			Main,
			Footer
		}
}
</script>
<style lang='stylus' rel='stylesheet/stylus' scoped>
</style>
