<template>
  <div class="app">
    <h2>📞 Mes Contacts</h2>

    <!-- FORMULAIRE -->
    <form @submit.prevent="addContact">
      <input v-model="form.name" placeholder="Nom" required />
      <input v-model="form.phone" placeholder="Téléphone" required />
      <input v-model="form.email" placeholder="Email" type="email" required />
      <button type="submit">➕ Ajouter</button>
    </form>

    <!-- LISTE -->
    <div v-if="contacts.length === 0">📭 Aucun contact</div>
    
    <ContactCard 
      v-for="contact in contacts" 
      :key="contact.id"
      :contact="contact"
      @delete="deleteContact"
    >
      <!-- SLOT : nom du contact -->
       id : {{ contact.id }}
       <br>
      {{ contact.name }}
    </ContactCard>

    <p class="count">{{ contacts.length }} contact(s)</p>
  </div>
</template>
















<script setup>
import { ref } from 'vue'
import ContactCard from './components/ContactCard.vue'

const form = ref({ name: '', phone: '', email: '' })
const contacts = ref([
  { id: 1, name: 'Sophie Martin', phone: '06 12 34 56 78', email: 'sophie@email.com' },
  { id: 2, name: 'Thomas Dubois', phone: '07 98 76 54 32', email: 'thomas@email.com' }
])

function addContact() {
  let nextId = contacts.value.length + 1;
  if(form.value.name.trim() == '' || form.value.phone.trim() == ''){
    alert('Tout les champs sont obligatoires');
  }else{

    contacts.value.push({ 
      id: nextId, 
      name: form.value.name,
      phone: form.value.phone,
      email: form.value.email
    })
    form.value = { name: '', phone: '', email: '' }
  }
  
}
function deleteContact(id) {
  contacts.value = contacts.value.filter(c => c.id !== id)
}
</script>

<style>
.app { max-width: 500px; margin: 20px auto; font-family: Arial; }
form { display: flex; flex-direction: column; gap: 8px; margin-bottom: 20px; }
input { padding: 8px; border: 1px solid #ddd; border-radius: 4px; }
button { padding: 8px; background: #3498db; color: white; border: none; border-radius: 4px; cursor: pointer; }
.count { margin-top: 15px; color: #7f8c8d; text-align: center; }
</style>