<template>
  <div class="todo-list">
    <todo-list-item 
    v-for="todo in todos" 
    :key="todo.id" 
    :todo-item="todo"
    @change-state="todo.completed=$event.target.checked"/>
    <!-- 通过todo-item把todo传递给todo-list-item子组件 -->
  </div>
</template>

<script>
import TodoListItem from "./TodoListItem";
export default {
  name: "TodoList",
  components: {TodoListItem},
//   接收副组件传来的todos
  props:["todos"],
};
</script>

<style>
.todo-list {
  /* Grid布局，方便设置每个todolist的间距,行间距是14px */
  display: grid;
  row-gap: 14px;
}
</style>
