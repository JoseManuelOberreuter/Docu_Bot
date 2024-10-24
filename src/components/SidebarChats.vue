<!-- Sidebar.vue -->
<template>
  <v-navigation-drawer
    :model-value="drawer"
    @update:model-value="$emit('update:drawer', $event)" 
    app
  >
    <v-list>
      <v-list-item title="Navigation drawer"></v-list-item>
      <!-- Agrega más elementos de navegación aquí -->
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
};
</script>

<style scoped>
/* Puedes agregar estilos personalizados aquí */
</style>
