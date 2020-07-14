<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="add">
  </div>
</template>
<script>
export default {
  props: {
    addTodo: {
      type: Function,
      required: true
    }
  },
  data () {
    return {
      title: ""
    };
  },
  methods: {
    add () {
      // 1.收集数据
      const title = this.title.trim();
      if (!title) {
        return alert("输入内容不能为空");
      }
      // 2.封装成todo对象
      const todo = {
        id: Date.now(),
        title,
        completed: false
      };
      // 3.调用addTodo添加todo并显示
      this.addTodo(todo);
      // 4.清空输入框
      this.title = "";
    }
  }
};
</script>
<style lang='stylus' rel='stylesheet/stylus' scoped>
</style>
