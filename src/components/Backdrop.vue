<template>
    <div>
        <div v-if="showBackdrop" class="backdrop">
            <div class="content">
                <h1>Please Add Some task <button @click="closeBackdrop">Close</button></h1>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'BackDrop',
    // props: {
    //     showBackdrop: Boolean
    // },
    data() {
        return {
            showBackdrop: true
        };
    },
    methods: {
        closeBackdrop() {
            this.showBackdrop = !this.showBackdrop
        }
    }
}
</script>

<style scoped>
.backdrop {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5); /* Semi-transparent black */
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000; /* Ensure it's on top of other content */
}

.content {
    background-color: #fff; /* Background color for the content */
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 15px rgba(0, 0, 0, 0.3);
    text-align: center;
}
</style>
