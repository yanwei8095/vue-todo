<template>
 <section class="jumbotron">
      <h3 class="jumbotron-heading">Search Github Users</h3>
      <div>
        <input type="text" placeholder="enter the name you search" v-model="searchName"/>
        <button @click="search">Search</button>
      </div>
    </section>
</template>
<script>
import PubSub from "pubsub-js"
	export default {
		data () {
			return {
				searchName: ''
			}
		},
		methods: {
			search () {
				// 取出搜索内容
				const searchName = this.searchName.trim()
			if (searchName) {
					// 发布消息
				PubSub.publish('search', searchName)
				// 清除输入
				this.searchName = ""
			}
			}
		}
 }
</script>
<style lang='stylus' rel='stylesheet/stylus' scoped>
</style>
