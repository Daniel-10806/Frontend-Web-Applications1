<template>
  <div class="message-panel">
    <div class="side-panel">
      <h2>Messages</h2>
      <div class="contact" v-for="contact in contacts" :key="contact.id">
        <img :src="contact.avatar" alt="Avatar" class="avatar" />
        <p>{{ contact.name }}</p>
      </div>
    </div>
    <div class="main-panel">
      <div class="message-header">
        <p>{{ activeChat }}</p>
      </div>
      <div class="message-content">
        <p v-if="messages.length === 0">This chat is empty</p>
        <div v-for="message in messages" :key="message.id" class="message">
          <p>{{ message.text }}</p>
        </div>
      </div>
      <div class="message-input">
        <i class="pi pi-paperclip" @click="toggleMenu"></i>
        <div v-if="showMenu" class="menu">
          <div class="menu-item" @click="attachFile('image/*')">
            <i class="pi pi-image"></i>
            <span>Photos and Videos</span>
          </div>
          <div class="menu-item" @click="attachFile('*/*')">
            <i class="pi pi-file"></i>
            <span>Document</span>
          </div>
        </div>
        <input type="text" placeholder="Send a message..." v-model="newMessage" />
        <button @click="sendMessage">Send</button>
      </div>
    </div>
  </div>
</template>

<script>
import 'primeicons/primeicons.css';

export default {
  data() {
    return {
      newMessage: '',
      messages: [],
      activeChat: 'Monica',
      contacts: [
        {id: 1, name: 'Fidel', avatar: 'src/assets/images/avatar1.jpeg'},
        {id: 2, name: 'Monica', avatar: 'src/assets/images/avatar2.jpg'},
        {id: 3, name: 'Silvia', avatar: 'src/assets/images/avatar3.png'},
      ],
      showMenu: false,
    };
  },
  methods: {
    toggleMenu() {
      this.showMenu = !this.showMenu;
    },
    sendMessage() {
      if (this.newMessage.trim() !== '') {
        this.messages.push({id: this.messages.length + 1, text: this.newMessage});
        this.newMessage = '';
      }
    },
    attachFile(accept) {
      const input = document.createElement('input');
      input.type = 'file';
      input.accept = accept;
      input.onchange = (event) => {
        const file = event.target.files[0];
        if (file) {
          console.log('Archive adjutant:', file.name);
        }
      };
      input.click();
      this.showMenu = false;
    },
  },
};
</script>

<style scoped>
.message-panel {
  display: flex;
  border: 1px solid #ccc;
  height: 400px;
  width: 100%;
}

.side-panel {
  width: 30%;
  background-color: #f5f5f5;
  border-right: 1px solid #ccc;
  padding: 10px;
}

.contact {
  display: flex;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

.contact img.avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  margin-right: 10px;
}

.main-panel {
  width: 70%;
  display: flex;
  flex-direction: column;
}

.message-header {
  background-color: #6a1b9a;
  color: white;
  padding: 10px;
  text-align: center;
}

.message-content {
  flex-grow: 1;
  padding: 10px;
  background-color: #fff;
}

.message-content p {
  color: grey;
  margin-top: 210px;
  margin-left: 10px;
}

.message-input {
  display: flex;
  align-items: center;
  padding: 10px;
  border-top: 1px solid #ccc;
  position: relative;
}

.message-input i {
  font-size: 24px;
  color: grey;
  margin-right: 10px;
  cursor: pointer;
}

.message-input .menu {
  position: absolute;
  top: -80px;
  left: 0;
  background-color: white;
  border: 1px solid #ccc;
  padding: 10px;
  display: flex;
  flex-direction: column;
  z-index: 1;
}

.message-input .menu-item {
  display: flex;
  align-items: center;
  padding: 5px 10px;
  cursor: pointer;
}

.message-input .menu-item i {
  margin-right: 10px;
}

.message-input .menu-item:hover {
  background-color: #f0f0f0;
}

.message-input input {
  flex-grow: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.message-input button {
  margin-left: 10px;
  padding: 10px 20px;
  background-color: black;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.message-input button:hover {
  background-color: blue;
}
</style>