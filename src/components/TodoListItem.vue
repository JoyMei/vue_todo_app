<template>
  <div>
    <div class="todo-item" :class="{done:todoItem.completed}">
      <label>
        <!-- 包含了input的span ，点击label均可触发-->
         <!-- 注册change_state事件 -->
        <input type="checkbox" 
        :checked="todoItem.completed"
        @click="$emit('change-state',$event)"/>
        {{todoItem.content}}
        <span class="check-button"></span>
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoListItem",
  props:["todoItem"],
//   接收todoitem
};
</script>

<style>
.todo-item {
  background: white;
  padding: 16px;
  border-radius: 8px;
  color: #626262;
}
.todo-item label {
  position: relative;
  display: flex;
  align-items: center;
}
.todo-item.done label{
    text-decoration: line-through;
    font-style: italic;
}
.todo-item label span.check-button {
  position: absolute;
  top: 0;
}
.todo-item label span.check-button::before,
.todo-item label span.check-button::after {
  content: "";
  display: block;
  position: absolute;
  width: 18px;
  height: 18px;
  border-radius: 50%;
}
.todo-item label span.check-button::before {
  border: 2px solid #ccf02a;
}
.todo-item label span.check-button::after {
  transition: 0.4s;
  background: #f8c210;
  transform: translate(2px, 2px) scale(0.8);
  opacity: 0;
}
.todo-item input {
  margin-right: 16px;
  /* 隐藏原生的复选框 */
  opacity: 0;
}
/* 选择相邻的自定义的 span.check-button*/
.todo-item input:checked + span.check-button::after {
  opacity: 1;
}
</style>
