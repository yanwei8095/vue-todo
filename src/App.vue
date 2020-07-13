<template>
<div class="todo-container">
    <div class="todo-wrap">
      <Header/>
			<Main :todos='todos'/>
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
	components: {
		Header,
		Main,
		Footer
	}
}
</script>
<style lang='stylus' rel='stylesheet/stylus' scoped>
</style>
