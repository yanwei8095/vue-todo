<template>
<div>
	<h2 v-if="firstView">请输入关键字搜索</h2>
	<h3 v-else-if="loading">Loading...</h3>
	<h3 v-else-if="errorMsg">{{errorMsg}}</h3>
	<div class="row" v-else>
      <div class="card" v-for="user in users" :key="user.name" >
        <a :href="user.url" target="_blank">
          <img :src="user.avatar_url" style='width: 100px'/>
        </a>
        <p class="card-text">{{user.username}}</p>
      </div>
    </div>
</div>
</template>
<script>
import PubSub from "pubsub-js"
import axios from 'axios'
	export default {
		data () {
			return {
				firstView: true, // 是否显示初始的默认界面
				loading: false, // 是否正在请求中
				users: [], // 搜索到的用户列表
				errorMsg: '' // 错误信息
			}
		},
		mounted () {
			// 订阅消息
			PubSub.subscribe('search', async (msgName, searchName) => { // 收到一个要进行搜索的消息
			// 1.更新状态数据
			this.firstView = false;
			this.loading = true
			// 2.发送异步ajax请求
			const url = `http://api.github.com/search/users?q=${searchName}`
			try {
			const response = await axios.get(url)
			// 3.1如果请求成功,更新状态数据(成功)
			const result = response.data
			const users = result.items.map(item => ({
				username: item.login,
				avatar_url: item.avatar_url,
				url: item.html_url
			}))
			this.loading = false
			this.users = users
			} catch (error) {
				// 3.2如果请求失败,更新状态数据(失败)
			this.loading = false
			this.errorMsg = "请求出错:" + error.message
			}
			})
		}
 }
</script>
<style scoped>
.card {
  float: left;
  width: 33.333%;
  padding: .75rem;
  margin-bottom: 2rem;
  border: 1px solid #efefef;
  text-align: center;
}

.card > img {
  margin-bottom: .75rem;
  border-radius: 100px;
}

.card-text {
  font-size: 85%;
}
</style>
