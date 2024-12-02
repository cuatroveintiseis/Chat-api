<!--Código corregido, se incorpora Color picker -->

<script setup>


import { ref, onMounted } from 'vue';
import axios from 'axios';
import Chat from './components/Chat.vue'


const users = ref([]);
const messages = ref([]);
const messageUser1 = ref('');
const messageUser2 = ref('');
const colorUser1 = ref('#FFFFFF');
const colorUser2 = ref('#FFFFFF');


const getUser = async () => {
  const url = "https://randomuser.me/api?results=3";
  const { data } = await axios.get(url);
  users.value = data.results;
}

const sendMessage = (user) => {
  const message = user === 1 ? messageUser1 : messageUser2;
  const color = user === 1 ? colorUser1.value : colorUser2.value;


  if (message.value.trim() !== '') {
    messages.value.push({
      name: `${users.value[user].name.first} ${users.value[user].name.last}`,
      message: message.value,
      color: color,
      isRight: user === 2,
    });
    message.value = '';
  }
};





onMounted(getUser);


</script>

<template>
  <div id="App">



    <div class="user-container">
      <div class="user-card">
        <img v-if="users[1]" :src="users[1].picture.large" alt="Usuario 1" />
        <p v-if="users[1]">{{ users[1].name.first }} {{ users[1].name.last }}</p>
        <input type="color" v-model="colorUser1" />
        <textarea v-model="messageUser1" id="textareabox" name="textarea1"></textarea>
        <button @click="sendMessage(1)">Enviar</button>
      </div>
    </div>

    <div class="chat-container">
      <Chat v-for="(msg, index) in messages" :key="index" :name="msg.name" :message="msg.message" :color="msg.color"
        :is-right="msg.isRight" />
    </div>


    <div class="user-container">
      <div class="user-card">
        <img v-if="users[2]" :src="users[2].picture.large" alt="Usuario 2" />
        <p v-if="users[2]">{{ users[2].name.first }} {{ users[2].name.last }}</p>
        <input type="color" v-model="colorUser2" />
        <textarea v-model="messageUser2" id="tetareabox" name="textarea1"></textarea>
        <button @click="sendMessage(2)">Enviar</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
#App {
  display: flex;
  justify-content: center;
  text-align: center;
  margin-top: 100px;
}

.chat-container {
  width: 250px;
  padding: 20px;
  margin: 20px;
  border: 2px solid #ddd;
  border-radius: 8px;
  background-color: #f9f9f9;
  text-align: left;
}

.message p {
  margin: 8px 1;
  font-size: 14px;
}


input {
  width: 100%;
  margin-bottom: 5px;
  box-sizing: border-box;
}

textarea {
  width: 100%;
  box-sizing: border-box;

}

img {
  border-radius: 50%;
}
</style>