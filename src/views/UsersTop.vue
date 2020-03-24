<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">
      美食達人
    </h1>
    <hr>
    <div class="row text-center">
      <TopUserCard 
        v-for="topUser in topUsers"
        :key="topUser.id"
        :top-user="topUser"
        @after-add-following="afterAddFollowing"
        @after-delete-following="afterDeleteFollowing"
      />
    </div>
  </div>
</template>

<script>
import NavTabs from '../components/NavTabs'
import TopUserCard from '../components/TopUserCard'
import usersAPI from './../apis/users'
import { Toast } from './../utils/helpers'

export default {
  components: {
    NavTabs,
    TopUserCard
  },
  data () {
    return {
      topUsers: []
    }
  },
  created () {
    this.fetchTopUsers()
  },
  methods: {
    async fetchTopUsers () {
      try {
        const { data, statusText } = await usersAPI.getTopUsers()

        if (statusText !== 'OK') {
          throw new Error(statusText)
        }

        this.topUsers = data.users
      } catch (error) {
        Toast.fire({
          type: 'error',
          title: '無法取得美食達人，請稍後再試'
        })
      }
    },
    afterAddFollowing (userId) {
      this.topUsers = this.topUsers.map(user => {
        if (user.id !== userId) {
          return user
        }

        return {
          ...user,
          FollowerCount: user.FollowerCount + 1,
          isFollowed: true
        }
      }).sort((a, b) => b.FollowerCount - a.FollowerCount)
    },
    afterDeleteFollowing (userId) {
      this.topUsers = this.topUsers.map(user => {
        if (user.id !== userId) {
          return user
        }

        return {
          ...user,
          FollowerCount: user.FollowerCount - 1,
          isFollowed: false
        }
      }).sort((a, b) => b.FollowerCount - a.FollowerCount)
    },
  }
}
</script>
