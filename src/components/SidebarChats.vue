<template>
  <v-navigation-drawer
    :model-value="drawer"
    @update:model-value="$emit('update:drawer', $event)"
    app
  >
    <v-list>
      <!-- Sección superior con íconos de lápiz y cruz -->
      <v-list-item>
        <v-row justify="space-between" align="center">
          <!-- Botón para editar (lápiz) -->
          <v-btn icon @click="startEditing">
            <v-icon>mdi-pencil</v-icon>
          </v-btn>
          <!-- Título del sidebar -->
          <span>Navigation drawer</span>
          <!-- Botón para agregar nuevo chat (cruz) -->
          <v-btn icon @click="addNewChat">
            <v-icon>mdi-plus</v-icon>
          </v-btn>
        </v-row>
      </v-list-item>

      <!-- Lista de chats históricos -->
      <v-list-item-group>
        <v-list-item
          v-for="(chat, index) in chats"
          :key="index"
        >
          <v-list-item-content>
            <!-- Edición del nombre del chat -->
            <v-list-item-title v-if="!editing || activeChatIndex !== index" @click="selectChat(index)">
              {{ chat.title }}
            </v-list-item-title>
            <v-text-field
              v-else
              v-model="chats[index].title"
              label="Editar nombre"
              append-icon="mdi-delete"
              @click:append="deleteChat(index)"
              @blur="stopEditing"
              @keyup.enter="stopEditing"
              dense
              hide-details
            />
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>
    </v-list>
  </v-navigation-drawer>
</template>

<script>
export default {
  props: {
    drawer: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      chats: [], // Lista de chats históricos
      activeChatIndex: null, // Índice del chat seleccionado actualmente
      activeChat: null, // Chat actual
      editing: false, // Bandera para activar/desactivar modo de edición
    };
  },
  methods: {
    // Inicia el modo de edición
    startEditing() {
      if (this.activeChatIndex !== null) {
        this.editing = true;
      } else {
        console.log("No hay ningún chat seleccionado para editar");
      }
    },
    // Detener el modo de edición
    stopEditing() {
      this.editing = false;
    },
    // Método para agregar un nuevo chat
    addNewChat() {
      const newChat = {
        title: `Chat ${this.chats.length + 1}`,
        messages: [], // Aquí se guardará el historial de mensajes
      };
      this.chats.push(newChat);
      this.activeChatIndex = this.chats.length - 1;
      this.activeChat = newChat;
      console.log("Nuevo chat agregado:", newChat);
    },
    // Seleccionar un chat del historial
    selectChat(index) {
      this.activeChatIndex = index;
      this.activeChat = this.chats[index];
      console.log("Chat seleccionado:", this.activeChat);
    },
    // Método para agregar un mensaje al chat actual
    addMessageToChat(message) {
      if (this.activeChat) {
        this.activeChat.messages.push(message);
        console.log("Mensaje agregado:", message);
      } else {
        console.log("No hay un chat activo");
      }
    },
    // Eliminar un chat de la lista
    deleteChat(index) {
      if (confirm("¿Estás seguro de que deseas eliminar este chat?")) {
        this.chats.splice(index, 1);
        if (this.activeChatIndex === index) {
          this.activeChatIndex = null; // Si eliminamos el chat activo, lo deseleccionamos
          this.activeChat = null;
        }
        console.log("Chat eliminado");
      }
    },
  },
};
</script>

<style scoped>
/* Puedes agregar estilos personalizados aquí */
</style>
