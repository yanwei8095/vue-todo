<template>
<div>
<h2>App组件</h2>
<img src="./assets/logo.png" alt="logo">
<HelloWorld/>
</div>
</template>
<script>
import HelloWorld from './components/HelloWorld'
export default{
	components: {
		HelloWorld
	}
}
</script>
<style lang='stylus' rel='stylesheet/stylus' scoped>
</style>
