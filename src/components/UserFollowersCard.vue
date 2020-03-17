<template>
  <div class="card">
    <div class="card-header">
      <strong>{{ followers.numOfFollowers }}</strong> followers (追隨者)
    </div>
    <div class="card-body">
      <router-link
        v-for="profile in followers.profiles"
        :key="profile.id"
        :to="{ name: 'user', params: { id: profile.id }}"
      >
        <img :src="profile.image" width="60" height="60" class="avatar">
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    followers: {
      type: Object,
      required: true
    },
  }
}
</script>
