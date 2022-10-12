<script setup lang="ts">
import GithubProfile from '@/components/GithubProfile.vue'
import SearchUsername from '../components/SearchUsername.vue'

import { ref } from 'vue'

const username = ref('BioBoost');

// const setUsername = function(un : string) {
//   console.log(`Need to search for ${un}`)
//   username.value = un
// }

</script>

<template>
  <div>
    <github-profile :username="username" />
    <hr />
    <search-username v-model="username" />
  </div>
</template>