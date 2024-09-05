<template>
    <div class="todo-container">
        <BackDrop v-if="showBackdrop" :showBackdrop="showBackdrop"/>
        <div class="title">
            <h1>{{task}}</h1>
        </div>
        <div class="input-container">
            <input type="text" v-model="message" @keyup.enter="updateMessage" placeholder="Add a new task" ref="input" />
            <button class="add-button" @click="updateMessage">Add Task</button>
        </div>
        <div class="tasks-section">
            <div class="not-completed-section">
                <h4>Not Completed Tasks</h4>
                <table>
                    <tr>
                        <th>Task</th>
                        <th>Status</th>
                    </tr>
                    <tr v-for="a in arr" :key="a.message" >
                        <td v-if="!a.status" :class="{ done: a.status }">{{ a.message }}</td>
                        <td v-if="!a.status"><span class="notcompleted"></span></td>
                        <td v-if="!a.status"><button class="status-button" @click="updateStatus(a)">Completed</button></td>
                    </tr>
                </table>
            </div>
            <div class="completed-section">
                <h4>Completed Tasks</h4>
                <table>
                    <tr>
                        <th>Task</th>
                        <th>Status</th>
                    </tr>
                    <tr v-for="a in arr" :key="a.message" >
                        <td v-if="a.status" :class="{ done: a.status }">{{ a.message }}</td>
                        <td v-if="a.status"><span class="completed"></span></td>
                        <td v-if="a.status"><button class="status-button" @click="updateStatus(a)">Redo</button></td>
                    </tr>
                </table>
            </div>
        </div>
        <br>
        <br>
        <br>
        <hr>
        <div><CalculatorPRO /></div>
        
    </div>
</template>

<script>
import BackDrop from './Backdrop.vue';
import CalculatorPRO from './Calculator.vue';

export default {
    name: 'ToDo',
    components: {
        BackDrop,CalculatorPRO
  },
    props: {
        task: String
    },
    data() {
        return {
            arr: [],
            status: false,
            id: 0,
            showBackdrop: false,
        };
    },
    methods: {
        updateMessage() {
            if (this.message) {
                this.arr.push({ "id": this.id++, "message": this.message, "status": this.status });
                this.message = "";
            } else {
                this.$refs.input.focus();
                this.showBackdrop = !this.showBackdrop;
            }
        },
        updateStatus(arr) {
            arr.status = !arr.status;
        }
    }
}
</script>

<style scoped>
.todo-container {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
    background: #f4f4f4;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.title h1 {
    text-align: center;
    color: #333;
    font-family: 'Arial', sans-serif;
}

.input-container {
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
}

input[type="text"] {
    padding: 10px;
    font-size: 16px;
    border: 2px solid #ddd;
    border-radius: 4px;
    width: 70%;
    margin-right: 10px;
}

.add-button {
    padding: 10px 15px;
    font-size: 16px;
    background-color: #28a745;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.add-button:hover {
    background-color: #218838;
}

.tasks-section {
    display: flex;
    justify-content: space-between;
    gap: 20px;
}

.not-completed-section,
.completed-section {
    width: 48%;
}

table {
    width: 100%;
    border-collapse: collapse;
}

th, td {
    padding: 10px;
    text-align: left;
    border-bottom: 1px solid #ddd;
}

th {
    background-color: #f8f8f8;
}

.done {
    text-decoration: line-through;
    color: #888;
}

.status-button {
    padding: 5px 10px;
    font-size: 14px;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.status-button:hover {
    background-color: #0056b3;
}

.completed {
    display: inline-block;
    height: 10px;
    width: 8px;
    border-bottom: 5px solid green;
    border-right: 5px solid green;
    transform: rotate(45deg);
    margin-left: 10px;
}
.notcompleted {
    display: inline-block;
    height: 10px;
    width: 10px;
    position: relative;
    margin-left: 10px;
}

.notcompleted::before,
.notcompleted::after {
    content: '';
    position: absolute;
    top: 0;
    left: 50%;
    width: 2px;
    height: 100%;
    background-color: red;
}

.notcompleted::before {
    transform: rotate(45deg);
}

.notcompleted::after {
    transform: rotate(-45deg);
}
</style>
