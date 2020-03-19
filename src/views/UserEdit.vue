<template>
  <div class="container py-5">
    <UserForm
      :initial-user="user"
      @after-submit="handleAfterSubmit"
    />
  </div>
</template>

<script>
import UserForm from '../components/UserForm.vue'

const dummyData = {
  'profile': {
    name: 'root',
    image: 'https://i.imgur.com/58ImzMM.png',
  }
}

export default {
  components: {
    UserForm
  },
  data () {
    return {
      user: {
        name: '',
        image: ''
      }
    }
  },
  created () {
    console.log(this.$route.params)

    const { id } = this.$route.params
    this.fetchUser(id)
  },
  methods: {
    handleAfterSubmit (formData) {
      // 透過 API 將表單資料送到伺服器
      for (let [name, value] of formData.entries()) {
        console.log(name + ': ' + value)
      }
    },
    fetchUser(userId) {
      console.log(userId)

      const { profile } = dummyData
      this.user = {
        ...this.user,
        name: profile.name,
        image: profile.image
      }
    }
  }
}
</script>
