<script setup>
import { ref } from 'vue';

const items = ref([]);
const newItem = ref('');
const newItemHighPriority = ref(false);
const editing = ref(false);
const saveItems = () => {
  items.value.push({
    id: items.value.length + 1,
    label: newItem.value,
    purchased: false,
    highPriority: newItemHighPriority.value,
  });
  newItem.value = '';
  newItemHighPriority.value = '';
  console.log(items);
};
const doEdit = e => {
  editing.value = e;
  newItem.value = '';
};
const togglePurchased = item => {
  console.log(item);
  item.purchased = !item.purchased;
  console.log(item);
};
</script>

<template>
  <div class="header">
    <button v-if="editing" class="btn" @click="doEdit(false)">Cancel</button>
    <button v-else class="btn btn-primary" @click="doEdit(true)">
      Add Item
    </button>
  </div>
  <form v-if="editing" @submit.prevent="saveItems" class="add-item-form">
    <input v-model="newItem" type="text" placeHolder="saisir produit" />
    <label>
      <input v-model="newItemHighPriority" type="checkbox" />
      produit urgent
    </label>
    <button :disabled="!newItem.length" class="btn btn-primary">
      enregistrer produit
    </button>
  </form>
  <ul>
    <li
      v-for="item in items"
      @click="togglePurchased(item)"
      :key="item.id"
      :class="{ priority: item.highPriority, strikeout: item.purchased }"
    >
      {{ item.label }}
    </li>
  </ul>
  <p v-if="editing && !items.length">aucun produit ajouté</p>
</template>
