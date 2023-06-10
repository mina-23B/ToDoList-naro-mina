<script setup lang="ts">
import { ref } from 'vue'

interface ToDo {
  todo: string
  date: string
  finished: boolean
}

const newToDo = ref('')
const newdueDate = ref('')

const tasks = ref<ToDo[]>([
  { todo: 'A Tour of Go' , date: '6/11', finished:false }
])

const addToDo = () => {
  if (!newToDo.value) return
  tasks.value.push({ todo: newToDo.value  , date: newdueDate.value, finished: false })
}

</script>

<template>
  <div>
    <div>ToDoList</div>
    <div>ToDo</div>
    <ul>
      <li v-for="task in tasks.filter(v => !v.finished)" :key="task.todo" >
        <div>{{ task.date }} {{ task.todo }}</div>
        <div><button @click="task.finished = true">完了</button></div>
      </li>
      </ul>
      <div>完了済み</div>
    <ul>
      <li v-for="task in tasks.filter(v => v.finished)" :key="task.todo" >
        <div> {{ task.todo }}</div>
      </li>
    </ul>
    <div>
      <label>
        ToDo追加
        <input v-model="newToDo" type="text" />
      </label>
      <label>
        期日
        <input v-model="newdueDate" type="text" />
      </label>
      <button @click="addToDo">追加</button>
    </div>
  </div>
</template>


