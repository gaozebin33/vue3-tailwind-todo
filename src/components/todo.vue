<template>
  <div class="max-w-md mx-auto border shadow-xl px-10 py-20 rounded text-left">
    <img alt="Vue logo" src="../assets/logo.png" class="w-20 mb-5" />
    <h1 class="text-4xl text-left">代办</h1>
    <input
      v-model="todo"
      type="text"
      placeholder="填写事项"
      class="mt-3 base-input"
      @keyup.enter="addTodo"
    >
    <button class=" base-button__primary ml-2" @click="addTodo">添加事项</button>
    <!-- list部分 -->
    <ul>
      <li 
        v-for="(item, index) of todoList"
        :key="index" 
        class="flex justify-between items-center border-b p-2"
      >
        <span>{{item}}</span>
        <button class="base-button__error" @click="deleteTodo(index)">删除</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { reactive, ref } from 'vue'
export default {
  setup () {
    const todo = ref('')
    // todoList
    const todoList = reactive([123])
    // 新增todo
    const addTodo = () => {
      if(todo.value.trim()){
        todoList.push(todo.value.trim())
        todo.value = ''
      }
    }
    // 删除todo
    const deleteTodo = index => {
      todoList.splice(index,1)
    }

    return { todo, todoList, addTodo, deleteTodo }
  }
}
</script>

<style  scoped>
.base-input {
  @apply p-2 outline-none border focus:border-blue-400 rounded transition text-sm;
}

.base-button__primary {
  @apply px-3 py-2 box-border focus:outline-none bg-blue-500  focus:bg-blue-400 hover:bg-blue-400 rounded text-white  ;
}

.base-button__error {
  @apply px-3 py-2 box-border focus:outline-none bg-red-500 focus:bg-red-400 hover:bg-red-400 rounded text-white ;
}
</style>