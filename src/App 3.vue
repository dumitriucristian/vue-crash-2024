<script setup>
import {ref} from  'vue';
import {onMounted} from 'vue';
//COMPOSITION
//in composition use ref
//replace this object.value eg: status.value

    const name = ref('john doe');
    const status = ref('active');
    const tasks = ref(['Task one', 'Task two', 'Task three']);
    const newTask = ref('');

    const toggleStatus = () => {
      if ( status.value === 'active') {
        status.value = 'pending';
      }else if(status.value === 'pending'){
        status.value = "inactive";
      }else{
        status.value = "active";
      }
    }

    const addTask = () => {
      if (newTask.value.trim() != '') {
        tasks.value.push(newTask.value);
        newTask.value = '';
      }
    }

    const deleteTask = (index) => {
      tasks.value.splice(index,1);
    }

    onMounted(async () => {
     try {
        const response = await fetch('https://my-json-server.typicode.com/typicode/demo/posts');
        const data = await response.json();
        tasks.value = data.map((task) => task.title);
      } catch (error ) {
        console.log('Error fetching data');
      }
    })
</script>

<template>
<h1>{{ name  }}</h1>  
<p v-if="status === 'active'">User is active</p>
<p v-else-if="status === 'pending'">User is pending</p>
<p v-else >User is inactive</p>

<form @submit.prevent="addTask">
  <label for="newTask">Add Task</label>
  <input type ="text" id="newTask" name="newTask" v-model="newTask">
  <button type="submit">Submit</button>

</form>
<h3>Tasks</h3>
<ul>
  <li v-for="(task , index) in tasks" :key="task">
    <span>{{task}}</span>
    <button @click="deleteTask(index)">x</button>
  </li>
</ul>
<a :href="link">Click For Google</a>
<button @click="toggleStatus()">Change Status</button>
</template>

<style scoped></style>


