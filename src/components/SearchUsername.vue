<script setup lang="ts">
import { ref, defineEmits, computed } from 'vue'

const props = defineProps({
  // username: { type: String, default: '' },
  // 2-way binding:
  modelValue: { type: String, default: '' }
})

// const emit = defineEmits(['search'])
// 2-way binding
const emit = defineEmits(['update:modelValue'])

const usernameInput = ref(props.modelValue)

// 2-way binding computed username
const username = computed({
  get: () => props.modelValue,
  set: (value) => emit('update:modelValue', value)
})

const search = function() {
//   console.log(`Searching for user ${usernameInput.value}`);
//   // Emit our own event
//   emit('search', usernameInput.value)
  username.value = usernameInput.value;
}

</script>

<template>
  <div>
    <input type="text" v-model="usernameInput" />
    <button @click="search">Search</button>
  </div>
</template>