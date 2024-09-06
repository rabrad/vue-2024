<script setup>
import { ref, onMounted } from 'vue';

const name = ref("John Doe");
const status = ref(true); // ref() to make data reactive
const tasks = ref();
const link = "https://google.com";

const toggleStatus = () => {
    status.value = !status.value;
};
const newTask = ref('');

const addTask = () => {
    if (newTask.value) {
        tasks.value.push(newTask.value);
        newTask.value = '';
    }
};

const deleteTask = (index) => {
    tasks.value.splice(index, 1)
};
const error = ref('')

onMounted(async () => {
    try {
        const response = await fetch('https://jsonplaceholder.typicode.com/todos');
        const data = await response.json();
        tasks.value = data.map((task) => task.title);
        console.log(tasks.value)
    } catch (error) {
        console.error('Error fetching data:', err);
    }
});


</script>

<!---------------------------------->
<template>
    <h1>{{ name }}</h1>
    <p v-if="status">User is active </p>
    <p v-else>User is inactive</p>

    <h3>Tasks</h3>
    <ul>
        <li v-for="(task, index) in tasks" :key="task">
            <span>{{ task }} </span>
            <button @click="deleteTask(index)">X</button>
        </li>
    </ul>

    <div class="boarder"></div>
    <!-- <a v-bind:href="link" target="_blank">Click got google</a> -->
    <a :href="link" target="_blank">Click got google</a>

    <div class="boarder"></div>

    <!-- <button v-on:click="toggleStatus">Change statue</button> -->
    <button @click="toggleStatus">Change statue</button>

    <!--- Forms-->
    <form @submit.prevent="addTask">
        <label for="newTask">Add Task</label>
        <input type="text" id="newTask" name="newTask" v-model="newTask">
        <button type="submit">Submit</button>
    </form>

    <br>

</template>



<!---------------------------------->
<style scoped>
.boarder {
    padding-bottom: 1rem;
}

form {
    display: flex;
    flex-direction: column;
    padding-top: 1rem;
    max-width: fit-content;
    gap: .5rem;
}
</style>
