<template>
  <div class="input-add">
    <input
      type="text"
      name="todo"
      v-model="todoContent"
      @keyup.enter="emitAddTodo"
    />
    <button @click="emitAddTodo">
      <i class="plus"></i>
    </button>
  </div>
</template>

<script>
import {ref} from "vue";
export default {
  name: "TodoAdd",
  setup (props, context) {
    const todoContent = ref("");
    const emitAddTodo = () => {
      const todo = {
        id: props.tid,
        content: todoContent.value,
        completed: false,
      };
    context.emit("add-todo", todo);
    todoContent.value = "";
    };
 return{
      todoContent,
      emitAddTodo,
    };
  },
};
</script>

<style>
.input-add {
  position: relative;
  display: flex;
  align-items: center;
}
.input-add input {
  padding: 16px 52px 16px 18px;
  border-radius: 48px;
  border: none;
  /* 取消选中时的边框和外边线 */
  outline: none;
  box-shadow: 0px 0px 24px rgba(0, 0, 0, 0.08);
  width: 100%;
  font-size: 16px;
  color: #626262;
}
.input-add button {
  width: 46px;
  height: 46px;
  border-radius: 50%;
  /* background: red; */
  /* background: linear-gradient(45deg,#380a8f #1738cc); */
  background: linear-gradient(45deg, #f3e5a5, #ee7709);
  border: none;
  outline: none;
  color: white;
  position: absolute;
  right: 0px;
  cursor: pointer;
}
.input-add .plus {
  display: block;
  width: 100%;
  height: 100%;
  background: linear-gradient(#fff, #fff), linear-gradient(#fff, #fff);
  background-size: 50% 3px, 3px 50%;
  background-position: center;
  background-repeat: no-repeat;
  /* 不平铺后，剩下的50%就不会重复显示啦 */
}
</style>
