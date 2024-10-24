<template>
  <v-layout class="rounded rounded-md fill-height">
    <!-- Barra de navegación lateral (Sidebar) -->
    <Sidebar :drawer="drawer" @update:drawer="drawer = $event" />

    <!-- Barra de aplicación con el botón de menú hamburguesa -->
    <v-app-bar app>
      <v-app-bar-nav-icon @click="toggleDrawer" />
      <v-toolbar-title>Application bar</v-toolbar-title>
    </v-app-bar>

    <!-- Contenido principal -->
    <v-main class="d-flex align-center justify-center fill-height" style="min-height: 300px;">
      <v-container class="d-flex align-center justify-center">
        <ChatComponent />
      </v-container>
    </v-main>
  </v-layout>
</template>

<script>
import Sidebar from './SidebarChats.vue';
import ChatComponent from './ChatComponent.vue';

export default {
  components: {
    Sidebar,
    ChatComponent,
  },
  data() {
    return {
      drawer: false, // Controla si el sidebar está abierto o cerrado
    };
  },
  methods: {
    toggleDrawer() {
      this.drawer = !this.drawer; // Alterna el estado de abrir/cerrar del sidebar
    }
  }
};
</script>

<style scoped>
/* Estilos personalizados si los necesitas */
</style>
