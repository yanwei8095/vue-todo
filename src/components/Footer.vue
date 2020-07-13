<template>
<div class="todo-footer">
        <label>
          <input type="checkbox" v-model="checkAll"/>
        </label>
        <span>
          <span>已完成{{completedCount}}</span> / 全部{{todos.length}}
        </span>
        <button class="btn btn-danger" v-show="completedCount>0">清除已完成任务</button>
      </div>
</template>
<script>
	export default {
    props: {
      todos: Array,
      selectAllTodos: Function
    },
    computed: {
      // 已完成的数量
      completedCount () {
        return this.todos.reduce((prev, todo) => prev + (todo.completed ? 1 : 0), 0)
      },
      // 是否全选
     /*  checkAll () {
        return this.todos.length===this.completedCount // 读取属性值completedCount
      } */
      checkAll: {
        get () {
          return this.todos.length === this.completedCount && this.completedCount > 0
        },
        set (val) { // 勾选状态已经发生了变化(监视input的勾选变化)
       //  更新todos中所有todo的completed的值
        this.selectAllTodos(val) // val是布尔值类型，根据input的勾选变化
        }
      }
      }
 }
</script>
<style lang='stylus' rel='stylesheet/stylus' scoped>
</style>
