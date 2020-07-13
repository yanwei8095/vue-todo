<template>
<li>
	<label>
		<input type="checkbox" v-model="todo.completed"/>
		<span>{{todo.title}}</span>
	</label>
	<button class="btn btn-danger" style="display:none">删除</button>
</li>
</template>
<script>
	export default {
		// 声明接收属性
		props: {
			todo: Object
		}
 }
</script>
<style lang='stylus' rel='stylesheet/stylus' scoped>
</style>
