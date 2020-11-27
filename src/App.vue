<template>
  <main>
    <div class="container">
      <h1>欢迎使用todolist</h1>
      <todo-add :tid="todos.length" @add-todo="addTodo" />
      <!-- 给todo-add组件传递tid属性用于生成新的todo的ID -->
      <!-- 通过addtodo监听todo-add组建的事件，使用addtodo函数处理事件 -->
      <todo-filter :selected="filter" @change-filter="filter=$event"/>
      <todo-list :todos="filteredTodos" />
      <!-- 使用ref包装的数据需要访问value属性才能够得到数据。在template标签中vue会自动拆解出value属性 。所以这里直接把setup中返回的todos传递给它就行啦-->
    </div>
  </main>
</template>

<script>
import { computed,ref } from "vue";
import TodoAdd from "./components/TodoAdd.vue";
import TodoFilter from "./components/TodoFilter.vue";
import TodoList from "./components/TodoList.vue";
export default {
  name: "App",
  components: {
    TodoAdd,
    TodoFilter,
    TodoList,
  },
  setup() {
    // 如果普通变量定义数据的话，那么在后面更新数据，组件是不会刷新的。可以使用vue3中新提供的API：ref和reactive
    const todos = ref([]);
    const addTodo = (todo) => todos.value.push(todo);
    // 更新todo的信息追加到todos列表中。
    const filter=ref("all");
    const filteredTodos=computed(()=>{
      switch(filter.value){
        case "done":
          return todos.value.filter((todo)=>todo.completed);
          case "todo":
          return todos.value.filter((todo)=>!todo.completed);
          default:
            return todos.value;
      }
    });
    // 以对象的形式返回它们
    return {
      todos,
      addTodo,
      filter,filteredTodos,
    };
  },
};
</script>

<style>
* {
  /* 盒子模型，限制宽高 */
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Helvetica, "PingFang SC", "Microsoft Yahei", sans-serif;
}
/* 整个页面 */
main {
  width: 100vw;
  /* 如果添加很多todo，会把页面撑开，设置min-height,滚动条还是会一直向下，到浏览器最底部 
  This is a box where you can change the minimum height.
  If there is more content than the minimum the box will grow to the height needed by the content.*/
  min-height: 100vh;
  display: grid;
  align-items: center;
  justify-items: center;
  background: linear-gradient(45deg, #da4bbb, #e2f3b3);
}
.container {
  width: 60%;
  max-width: 400px;
  box-shadow: 0px 0px 24px rgba(0, 0, 0, 0.15);
  border-radius: 24px;
  padding: 48px 28px;
  background:linear-gradient(45deg, #c5da4b, #e9f3be);
}
h1 {
  margin: 24px 0;
  font-size: 28px;
  color: #414873;
}
</style>
