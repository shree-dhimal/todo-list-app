<template>
    <div class="todo-container">
        <button @click="shoDiv(1)">TODO Application</button>
        <button @click="shoDiv(2)">Calculator</button>
        <button @click="shoDiv(3)">Play Reaction Game</button>
        <div v-if="showTodo">
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
                        <td v-if="!a.status"><button class="status-button" @click="deleteTask(a)">Delete</button></td>
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
        </div>
        <br>
        <br>
        <br>
        <hr>
        <div v-if="showCalculator">
        <div><CalculatorPRO /></div>
        </div>
        <br>
        <br>
        <br>
        <hr>
        <div v-if="showGame">
            <h1>Play Reaction Time</h1>
            <button @click="start" :disabled="isPlaying">Start</button>
            <BlockVue v-if="isPlaying" :delay="delay" @end="endGame" />
            <ResultsVue :score="score" v-if="showResult" @exit="showResult = !showResult"/>
        </div>
        
    </div>
</template>

<script>
import BackDrop from './Backdrop.vue';
import CalculatorPRO from './Calculator.vue';
import BlockVue from './reaction-timer/Block.vue';
import ResultsVue from './reaction-timer/Results.vue';


export default {
    name: 'ToDo',
    components: {
        BackDrop,CalculatorPRO,BlockVue,ResultsVue
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
            isPlaying: false,
            delay: null,
            score: null,
            showResult: false,
            showTodo:false,
            showCalculator:false,
            showGame:false,
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
        },
        deleteTask(a) {
            console.log(a.id);
            
            const index = this.arr.findIndex(item => item.id === a.id);
            if (index !== -1) {
            this.arr.splice(index, 1);
            console.log(this.arr)
            }
        },
        start() {
            this.isPlaying = true;
            this.delay = 2000 + Math.random() * 5000;
            console.log(this.delay);
            
        },
        endGame(reactionTime) {
            this.isPlaying = false;
            this.score = reactionTime;
            this.showResult = true;
        },
        shoDiv(num) {
            if (num == 1) {
                this.showTodo = !this.showTodo;
                this.showCalculator = false;
                this.showGame = false;
            } else if (num == 2) {
                this.showCalculator = !this.showCalculator;
                this.showTodo = false;
                this.showGame = false;
            } else if (num == 3) {
                this.showGame = !this.showGame;
                this.showTodo = false;
                this.showCalculator = false;
            }
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
/* General button styling */
button {
    padding: 10px 15px;
    font-size: 16px;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.2s;
}

button:hover {
    background-color: #0056b3;
    transform: scale(1.05);
}

button:disabled {
    background-color: #aaa;
    cursor: not-allowed;
}

/* Specific button styling */
.add-button {
    background-color: #28a745;
}

.add-button:hover {
    background-color: #218838;
}

.status-button {
    padding: 5px 10px;
    font-size: 14px;
    background-color: #007bff;
}

.status-button:hover {
    background-color: #0056b3;
}

/* Buttons in the top section */
.todo-container button {
    margin: 10px;
    font-size: 18px;
}

/* Additional style for completed task buttons */
.completed-section .status-button {
    background-color: #ffc107;
}

.completed-section .status-button:hover {
    background-color: #e0a800;
}

</style>
