<template>
  <v-card class="chat-container" >
    <v-card-title class="headline">ChatBot</v-card-title>

    <v-card-text class="messages-container">
      <div ref="messageContainer" class="messages">
        <div v-for="message in messages" :key="message.id" class="message" :class="{ 'user-message': message.isUser }">
          <strong v-if="message.isUser">You:</strong>
          <strong v-else>Bot:</strong> {{ message.text }}
        </div>
      </div>
    </v-card-text>

    <v-divider></v-divider>

    <v-card-actions>
      <v-text-field
        v-model="userInput"
        label="Type your message..."
        @keyup.enter="sendMessage"
        outlined
        clearable
        append-icon="mdi-send"
        @click:append="sendMessage"
        class="chat-input"
      ></v-text-field>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      userInput: '', // Texto del usuario
      messages: [
        { id: 1, text: 'Hello! How can I assist you today?', isUser: false },
      ], // Mensajes en el chat
    };
  },
  methods: {
    sendMessage() {
      if (this.userInput.trim() !== '') {
        // Agregar mensaje del usuario
        this.messages.push({ id: this.messages.length + 1, text: this.userInput, isUser: true });

        // Simular respuesta del bot
        setTimeout(() => {
          this.messages.push({
            id: this.messages.length + 1,
            text: 'This is a simulated response from the bot!',
            isUser: false,
          });
          this.scrollToBottom(); // Asegurar que el scroll esté abajo después de la respuesta
        }, 1000);

        // Limpiar el input
        this.userInput = '';

        this.scrollToBottom(); // Asegurar que el scroll esté abajo después de enviar el mensaje
      }
    },
    scrollToBottom() {
      // Desplazar el contenedor de mensajes hacia el final
      const container = this.$refs.messageContainer;
      container.scrollTop = container.scrollHeight;
    }
  },
  mounted() {
    this.scrollToBottom(); // Asegurar que el chat esté en el final al montar el componente
  },
};
</script>

<style scoped>
.chat-container {
  display: flex;
  flex-direction: column;
  height: 80vh;
  width: 65vh;
  background-color: #121212;
  color: white;
}

.messages-container {
  flex: 1;
  overflow-y: auto;
  display: flex;
  flex-direction: column-reverse; /* Asegura que los mensajes más recientes estén abajo */
}

.messages {
  display: flex;
  flex-direction: column;
  padding: 16px;
}

.message {
  margin: 8px 0;
}

.user-message {
  text-align: right;
  color: #42b983;
}

.message strong {
  margin-right: 8px;
}


</style>
