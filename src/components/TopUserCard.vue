<template>
    <div class="col-3">
      <router-link
        :to="{ name: 'user', params: { id: user.id }}"
      >
        <img
          :src="user.image"
          width="140px"
          height="140px"
        >
      </router-link>
      <h2>{{ user.name }}</h2>
      <span class="badge badge-secondary">追蹤人數：{{ user.FollowerCount }}</span>
      <p class="mt-3">
        <button
          v-if="user.isFollowed"
          type="button"
          class="btn btn-danger"
        >
          取消追蹤
        </button>
        <button
          v-else
          type="button"
          class="btn btn-primary"
        >
          追蹤
        </button>
      </p>
    </div>

</template>

<script>
export default {
  props: {
    topUser: {
      type: Object,
      required: true
    }
  },
  data () {
    return {
      user: this.topUser
    }
  },
}
</script>
