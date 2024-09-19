<template>
    <div class="container" v-if="showBlock" @click="stopTimer">
        <div class="block">
            <h1 >Click me!!!</h1>
        </div>
    </div>
</template>

<script>
export default {
    name: 'BlockVue',
    props: {
        delay: Number
    },
    mounted() {
        setTimeout(() =>  {
            this.showBlock = true
            this.startTimer()
            console.log(this.delay, 'delay')
        }, this.delay)
    },
    data() {
        return {
            showBlock: false,
            timer: null,
            reactionTime: 0,
            
        }
    },
    methods: {
        startTimer() {
            this.timer = setInterval(() =>  {
                this.reactionTime += 10
            }, 10)
        },
        stopTimer() {
            clearInterval(this.timer)
            this.$emit('end', this.reactionTime)
            console.log(this.reactionTime, 'reaction time')
        }
    },
    
}
</script>

<style scoped>
.container {
    margin-top: 20px; /* Full viewport height */
    display: flex;
    justify-content: center; /* Centers horizontally */
    align-items: center; /* Centers vertically */
    background: transparent; /* Transparent background */
}

.block {
    width: 200px;
    height: 200px;
    background: rgba(0, 0, 0, 0.7); /* Dark block with transparency */
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 10px;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out, transform 0.3s ease-in-out;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* Optional: shadow effect */
}

.block:hover {
    background: rgba(0, 0, 0, 0.9); /* Darker on hover */
    transform: scale(1.05); /* Slightly grow the block on hover */
}
</style>
