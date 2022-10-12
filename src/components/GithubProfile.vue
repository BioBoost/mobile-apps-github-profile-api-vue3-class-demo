<script setup lang="ts">
import { ref, defineProps, watch, toRefs } from 'vue'
import { Users } from '@/apis/github'

const props = defineProps({
  username: { type: String, default: '' }
})

const profile = ref({})
const error = ref(false)
const loading = ref(false)

const fetch_user = function() {
  error.value = false
  loading.value = true
  Users.get(props.username)
  .then((response) => {
    // Axios call made successfully and we have result
    console.log("Axios response received")
    console.log(response.data)    // JSON reply
    profile.value = response.data;
    loading.value = false
  })
  .catch(() => {
    error.value = true
    loading.value = false
  })
}

fetch_user()

// We need a watch for the username to re-invoke our API request
const username = toRefs(props).username
watch(username, async(newUsername, oldUsername) => {
  console.log("Fetching profile via Watch")
  fetch_user()
})

</script>

<template>
  <div v-if="error">
    Could not fetch profile of {{ username }}
  </div>
  <div v-else-if="loading">
    .... Loading profile ....
  </div>
  <div v-else>
    <h1>{{ profile.login }}</h1>
    <h3>{{ profile.name }}</h3>
    <img :src="profile.avatar_url" />
    <ul>
      <li>Number of public repos: <strong>{{ profile.public_repos }}</strong></li>
      <li>Number of followers: <strong>{{ profile.followers }}</strong></li>
    </ul>
  </div>
</template>