<script setup>

const props = defineProps({
    name: String,
    message: String,
    isRight: Boolean,
    color: String
});

</script>

<template>
    <div class="message">
        <label class="name" :class="{ 'message-right': isRight, 'message-left': !isRight }">{{ name }}</label>
        <div :class="{ 'message-right': isRight, 'message-left': !isRight }" :style="{ backgroundColor: color }"
            class="message-box">
            <span class="msg">{{ message }}</span>
        </div>
    </div>
</template>

<style scoped>
.message {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
}

.message-right {
    align-self: flex-end;
}

.message-left {
    align-self: flex-start;
}

.msg {
    padding: 8px;
    border-radius: 5px;
}

.message-box {
    padding: 5px;
    border-radius: 10px;
}
</style>
