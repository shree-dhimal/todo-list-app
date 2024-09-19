<template>
    <div class="container">
        <div class="block" @click="trigger">
            <h1 >Score</h1>
            <h3>{{score}}</h3>
        </div>
    </div>
</template>

<script>
export default {
    name: 'BlockVue',
    props: {
        score: Number
    },
    
    data() {
        return {
            
        }
    },

    methods: {
        trigger() {
            this.$emit('exit')
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
    background: rgba(122, 231, 187, 0.7); /* Dark block with transparency */
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
    background: rgba(236, 153, 153, 0.9); /* Darker on hover */
    transform: scale(1.05); /* Slightly grow the block on hover */
}
</style>
