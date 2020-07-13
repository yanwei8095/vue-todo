<template>
<!-- 组件中的模板能直接访问组件对象中的属性 -->
 <ul class="todo-main">
        <Item v-for="(todo,index) in todos" :key="index" :todo="todo" :deleteTodo="deleteTodo" :index="index" :selectTodo="selectTodo"/>
 </ul>
</template>
<script>
import Item from './Item'
	export default {
		// 声明接收属性
		props: ['todos', 'deleteTodo','selectTodo'],
		components: {
			Item
		}
 }
</script>
<style lang='stylus' rel='stylesheet/stylus' scoped>
</style>
