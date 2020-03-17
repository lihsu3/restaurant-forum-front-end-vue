<template>
  <div class="card">
    <div class="card-header">
      <strong>{{ followings.numOfFollowings }}</strong> followings (追蹤者)
    </div>
    <div class="card-body">
      <router-link
        v-for="profile in followings.profiles"
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
    followings: {
      type: Object,
      required: true
    },
  }
}
</script>
