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
      <span class="badge badge-secondary">追蹤人數：{{ updatedTopUser.FollowerCount }}</span>
      <p class="mt-3">
        <button
          v-if="updatedTopUser.isFollowed"
          type="button"
          class="btn btn-danger"
          @click.stop.prevent="deleteFollowing(user.id)"
        >
          取消追蹤
        </button>
        <button
          v-else
          type="button"
          class="btn btn-primary"
          @click.stop.prevent="addFollowing(user.id)"
        >
          追蹤
        </button>
      </p>
    </div>

</template>

<script>
import usersAPI from './../apis/users'
import { Toast } from './../utils/helpers'

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
  computed: {
    updatedTopUser: function () { 
      return this.topUser
    }
  },
  methods: {
    async deleteFollowing (userId) {
      try {
        const { data, statusText } = await usersAPI.deleteFollowing({
          userId
        })

        if (statusText !== 'OK' || data.status !== 'success') {
          throw new Error(statusText)
        }

        this.$emit('after-delete-following', userId)

      } catch (error) {
        Toast.fire({
          type: 'error',
          title: '無法delete追蹤，請稍後再試'
        })
      }

    },
    async addFollowing (userId) {
      try {
        const { data, statusText } = await usersAPI.addFollowing({
          userId
        })

        if (statusText !== 'OK' || data.status !== 'success') {
          throw new Error(statusText)
        }

        this.$emit('after-add-following', userId)

      } catch (error) {
        Toast.fire({
          type: 'error',
          title: '無法加入追蹤，請稍後再試'
        })
      }

    }
  }
}
</script>
