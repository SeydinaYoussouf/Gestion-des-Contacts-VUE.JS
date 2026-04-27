<template>
  <div class="contact">
    <div class="info">
      <!-- SLOT : le parent injecte le nom -->
      <strong><slot></slot></strong>
      <span>{{ contact.phone }}</span>
      <small>{{ contact.email }}</small>
    </div>
    <!-- EMIT : suppression -->
    <button @click="$emit('delete', contact.id)">✖</button>
  </div>
</template>

<script setup>
// PROP : l'objet contact complet
defineProps(['contact'])
defineEmits(['delete'])
</script>

<style scoped>
.contact {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px;
  background: #f5f5f5;
  margin: 8px 0;
  border-radius: 8px;
}
.info { display: flex; flex-direction: column; gap: 3px; }
small { color: #666; font-size: 0.8rem; }
button { background: none; border: none; color: #e74c3c; cursor: pointer; font-size: 18px; }
</style>